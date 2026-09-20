# Kurikulum: Expert Agentic AI untuk RumahExcel/Analyset
**Dibuat:** 20 September 2026 | **Status:** Siap dieksekusi, review tiap 4-6 minggu
**Terkait:** brainstorm_kurikulum_expert_agentic_ai_2026-09-20.md (rasionalnya di sana), Learn_Hermes/00_Roadmap (fondasi power-user), brainstorm_tujuan_hidup_karier_2026-09-19.md (RumahExcel butuh growth engine aktif)

## Prinsip Desain
- Pace realistis: **2-4 jam/minggu**, bukan bootcamp intensif — total estimasi ±6-7 bulan sampai punya 1 pilot produk nyata
- Jalur: **power-user dulu → builder** — cepat dapat value dari tools yang sudah ada, baru investasi bikin agent sendiri
- Tiap stage ditutup **milestone konkret yang dites**, bukan sekadar "sudah nonton course"
- Produk akhir TIDAK ditentukan di awal — muncul organik dari eksplorasi Stage 2-3, divalidasi di Stage 4

---

## Stage 0 — Fondasi Konsep (2 minggu, ±6-8 jam)
**Tujuan:** paham beda agentic AI vs chatbot vs RPA/automasi biasa, dan bisa jelaskan ke calon klien dalam bahasa awam.

- Baca: Anthropic blog "Building Effective Agents" (anthropic.com/research/building-effective-agents) — kerangka pola agent (workflow vs agent, kapan pakai yang mana)
- Baca: OpenAI whitepaper "A Practical Guide to Building Agents" (gratis, PDF)
- Konsep inti yang harus dikuasai: LLM sbg "otak", tools sbg "tangan", memory/state, orchestration loop, human-in-the-loop
- **Milestone:** tulis 1 paragraf (bisa buat pitch klien) yang menjelaskan beda "agentic AI" vs automasi Excel/macro biasa yang RumahExcel sudah kerjakan selama ini

## Stage 1 — Power-User Tools Existing (4-6 minggu)
**Tujuan:** maksimalkan kapabilitas agentic yang SUDAH dipakai (Hermes) sebelum bangun sendiri — lanjutkan roadmap Learn_Hermes yang sudah ada.

- Lanjutkan Level 2 (memory & skill management aktif), Level 3 (delegate_task batch, cron lanjutan: monitor_url/monitor_script, continuity, context_from), Level 4 (computer-use, session_search, prompting presisi) dari `Learn_Hermes/00_Roadmap_dan_Asesmen_Level_Saat_Ini.md`
- Latihan per level sudah didefinisikan di roadmap itu — jalankan langsung
- **Milestone:** minimal 1 skill custom dibuat sendiri, 1 cron watchdog jalan (monitor_url/script), 1 delegate_task batch paralel dipakai nyata untuk pekerjaan RumahExcel/Analyset

## Stage 2 — Building Blocks Agentic AI (6-8 minggu)
**Tujuan:** paham & bisa pakai komponen dasar di balik agent — LLM API, tool-calling, RAG — level developer pemula.

- DeepLearning.AI (gratis, short course): "LangChain for LLM Application Development"
- DeepLearning.AI: "Building and Evaluating Advanced RAG"
- Hugging Face Agents Course, Unit 1 (huggingface.co/learn/agents-course) — konsep tool use & ReAct pattern
- Anthropic docs: Tool Use / function calling dgn Claude API
- **Praktik:** bikin 1 script Python sendiri (di luar Hermes) yang manggil Claude/OpenAI API + minimal 1 tool call nyata (mis. baca file Excel klien, kasih ringkasan otomatis)
- **Milestone:** 1 agent sederhana buatan sendiri (bukan no-code, bukan Hermes) yang bisa baca data dan ambil 1 keputusan/tindakan dasar

## Stage 3 — Builder Track: Framework (6-8 minggu)
**Tujuan:** pilih & kuasai 1 framework no-code + 1 framework code, untuk bisa bangun produk lebih cepat & robust.

Dua jalur paralel (boleh selang-seling per minggu, bukan sekuensial):
- **No-code — n8n**: self-host di server sendiri, connect ke email/Google Sheets/API. Cepat buat validasi ide ke klien tanpa banyak coding. Sumber: n8n Academy (gratis)
- **Code — LangGraph** (atau lanjut Claude Agent SDK karena sudah familiar Claude/Hermes): multi-step agent dengan state management. Sumber: DeepLearning.AI "AI Agents in LangGraph", "Multi AI Agent Systems with crewAI"
- **Praktik:** pilih 1 use case nyata kecil (mis. agent yang cek email masuk RumahExcel → klasifikasi → draft balasan), bangun versi no-code (n8n) DAN versi code (LangGraph), lalu banding
- **Milestone:** 2 prototype agent (1 no-code, 1 code) untuk use case yang sama — punya basis keputusan mana yang lebih pas jadi produk RumahExcel/Analyset

## Stage 4 — Terapan: Dari Prototype ke Produk (8-12 minggu awal, lanjut ongoing)
**Tujuan:** validasi produk agentic AI nyata dengan klien/internal — bukan lagi belajar, tapi eksekusi bisnis.

- Pilih 1-2 pilot: klien RumahExcel kecil, atau internal Analyset dulu (lebih aman utk uji coba)
- Bangun guardrails: akurasi, cost per run, latency, **human-in-the-loop untuk audit trail** (relevan dgn background Arseno sbg auditor — agent yang salah tanpa jejak = risiko besar utk klien korporat)
- Rancang pricing model: recurring subscription vs project-based — sejalan dgn isu terbuka growth RumahExcel (butuh kaki recurring, bukan cuma project musiman — lihat brainstorm karier 2026-09-19)
- **Milestone:** 1 pilot project agentic AI berjalan dengan klien nyata atau internal Analyset, ada feedback loop terdokumentasi

---

## Timeline Ringkas (pace 2-4 jam/minggu)
| Stage | Durasi | Kumulatif |
|---|---|---|
| 0. Fondasi Konsep | 2 minggu | Minggu 1-2 |
| 1. Power-User Hermes | 4-6 minggu | Minggu 3-8 |
| 2. Building Blocks | 6-8 minggu | Minggu 9-16 |
| 3. Builder Framework | 6-8 minggu | Minggu 17-24 |
| 4. Terapan/Pilot | 8-12 minggu (awal) | Minggu 25-36+ |

**Total sampai pilot pertama: ±6-8 bulan.** Review checkpoint tiap 4-6 minggu (apakah pace cukup, apakah stage perlu di-adjust) — catat progresnya sbg file baru di folder `data_pribadi/Kurikulum_Agentic_AI/` mengikuti pola `Learn_Hermes` (NN_Stage-X_topik.md).

## Catatan Penting
- Stage 1 SUDAH punya roadmap detail terpisah — jangan duplikat, langsung lanjutkan `Learn_Hermes/00_Roadmap_dan_Asesmen_Level_Saat_Ini.md`
- Produk akhir sengaja tidak ditentukan sekarang — biarkan muncul dari pengalaman nyata di Stage 2-3, supaya bukan solusi yang dipaksakan cari masalah
- Jangan skip Stage 4 guardrails/audit-trail — ini pembeda penting mengingat positioning Analyset ke klien korporat yang sensitif thd akurasi & jejak audit
