[^1]# Stage 0 — Tutorial Praktik: Bikin Agent Paling Sederhana
**Tujuan:** dalam 30-45 menit, punya 1 program Python yang benar-benar "agentic" (bukan cuma chatbot) — LLM yang bisa BACA data & AMBIL keputusan sendiri.
**Gaya:** tutorial step-by-step, dikerjakan sendiri (Jarvis siap bantu kalau stuck di langkah manapun — tinggal kirim pesan error/screenshot).

---

## Langkah 1 — Siapkan API Key (5 menit)
Pilih salah satu (boleh dua-duanya untuk dibandingkan nanti):

**Opsi A — Anthropic (Claude)**
1. Buka https://console.anthropic.com → Sign up/login
2. Menu "API Keys" → Create Key → copy (simpan aman, hanya muncul sekali)
3. Ada free credit awal utk akun baru; setelah itu bayar per pemakaian (murah utk belajar, ~$5 cukup lama)

**Opsi B — Google Gemini (free tier lebih generous, cocok kalau mau gratis dulu)**
1. Buka https://aistudio.google.com/apikey → login Google
2. Create API Key → copy

> Simpan key ini di tempat aman. JANGAN kirim ke saya (Jarvis) lewat chat — kalau nanti mau saya bantu run kode otomatis, simpan sendiri sbg env var di server dan beri tahu nama variabelnya saja.

## Langkah 2 — Install Package (2 menit)
Buka terminal di laptop (bukan di server Hermes, supaya kamu latihan environment sendiri):
```bash
python3 -m venv agentic-env
source agentic-env/bin/activate   # Windows: agentic-env\Scripts\activate
pip install anthropic             # atau: pip install google-generativeai
```

## Langkah 3 — Versi 1: Chatbot Biasa (BUKAN agent, buat pembanding) (5 menit)
Buat file `v1_chatbot.py`:
```python
import anthropic

client = anthropic.Anthropic(api_key="ISI_API_KEY_KAMU")

response = client.messages.create(
    model="claude-3-5-haiku-20241022",
    max_tokens=200,
    messages=[{"role": "user", "content": "Ringkas dalam 2 kalimat: apa itu rekonsiliasi keuangan?"}]
)
print(response.content[0].text)
```
Jalankan: `python3 v1_chatbot.py`
👉 Ini baru **LLM biasa** — tanya-jawab satu arah, tidak baca data apapun, tidak ambil tindakan.

## Langkah 4 — Versi 2: Agent Sungguhan (Tool Use) (15-20 menit)
Bedanya agent: LLM diberi **tools** (fungsi Python nyata) dan LLM sendiri yang MEMUTUSKAN kapan panggil tool itu.

Buat file kecil `data_transaksi.csv` (data dummy, simulasi data klien RumahExcel):
```csv
tanggal,keterangan,jumlah
2026-09-01,Transfer masuk PT ABC,15000000
2026-09-03,Biaya admin bank,50000
2026-09-05,Transfer keluar vendor,-8000000
2026-09-10,Selisih tidak diketahui,-250000
```

Buat file `v2_agent.py`:
```python
import anthropic
import csv
import json

client = anthropic.Anthropic(api_key="ISI_API_KEY_KAMU")

# TOOL 1: baca file transaksi
def baca_transaksi(nama_file):
    with open(nama_file) as f:
        rows = list(csv.DictReader(f))
    return json.dumps(rows)

# Definisi tool untuk Claude (skema, bukan kode Python langsung)
tools = [
    {
        "name": "baca_transaksi",
        "description": "Membaca isi file CSV transaksi keuangan dan mengembalikan semua baris data",
        "input_schema": {
            "type": "object",
            "properties": {"nama_file": {"type": "string", "description": "nama file csv"}},
            "required": ["nama_file"]
        }
    }
]

messages = [{
    "role": "user",
    "content": "Baca file data_transaksi.csv, lalu identifikasi transaksi yang mencurigakan (misal: keterangan tidak jelas / selisih) dan jelaskan kenapa."
}]

# Loop agent: Claude bisa panggil tool berkali-kali sampai selesai
while True:
    response = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        tools=tools,
        messages=messages
    )

    if response.stop_reason == "tool_use":
        # Claude MEMUTUSKAN sendiri untuk pakai tool
        tool_call = next(b for b in response.content if b.type == "tool_use")
        print(f"[AGENT] Claude minta panggil tool: {tool_call.name}({tool_call.input})")

        if tool_call.name == "baca_transaksi":
            hasil = baca_transaksi(tool_call.input["nama_file"])

        messages.append({"role": "assistant", "content": response.content})
        messages.append({
            "role": "user",
            "content": [{"type": "tool_result", "tool_use_id": tool_call.id, "content": hasil}]
        })
    else:
        # Claude sudah selesai, kasih jawaban final
        final_text = next(b.text for b in response.content if b.type == "text")
        print("\n[HASIL AKHIR]\n", final_text)
        break
```
Jalankan: `python3 v2_agent.py`

**Yang harus kamu perhatikan saat run:**
- Ada baris `[AGENT] Claude minta panggil tool: baca_transaksi(...)` — ini bukti Claude SENDIRI yang memutuskan perlu baca file, bukan kamu yang hardcode alur-nya
- Loop `while True` = pola dasar SEMUA agent framework (LangGraph, CrewAI, n8n AI Agent node — semuanya bungkus loop yang sama ini)
- Coba ganti data CSV / pertanyaan, lihat apakah Claude tetap masuk akal mendeteksi anomali

## Langkah 5 — Refleksi (5 menit)
Jawab sendiri (boleh diskusikan hasilnya dgn Jarvis):
1. Apa BEDA nyata antara v1_chatbot.py dan v2_agent.py yang kamu rasakan saat run?
2. Kalau mau tambah tool ke-2 (misal: `kirim_email_notifikasi`), bagian kode mana yang perlu diubah?
3. Coba bayangkan: gimana pola `while True` + tools ini bisa dipakai utk kasus nyata RumahExcel/Analyset?

## Kalau Stuck
Kirim pesan error/screenshot ke saya kapan saja — saya bantu debug tanpa perlu API key kamu (cukup lihat error message-nya).

## Setelah Selesai
Update `Kurikulum_Agentic_AI/00_Progress_Tracker.md` — tulis apa yang berhasil/kendala, lalu kita lanjut sisa Stage 0 (pitch 1 paragraf) atau maju ke Stage 1.
