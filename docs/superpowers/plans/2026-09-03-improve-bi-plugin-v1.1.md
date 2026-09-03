# Improve BI Plugin v1.1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update 3 SKILL.md files with self-validation, no-summary instruction, dan chain dependency eksplisit untuk meningkatkan konsistensi output plugin BI, serta naikkan versi plugin jadi 1.1.0.

**Architecture:** Perubahan hanya di instructional text di 3 SKILL.md — tidak ada kode baru, tidak ada test harness baru. Perubahan berbasis pada spec `docs/2026-09-03-improve-bi-plugin-design.md`.

**Tech Stack:** Markdown (SKILL.md files), Python (versi bump via sed/edit)

**Spec:** `docs/2026-09-03-improve-bi-plugin-design.md`

## Global Constraints

- Versi plugin naik ke 1.1.0 (dari 1.0.0)
- Tidak ada perubahan di kode — hanya instructional text di SKILL.md
- Test harness (`tests/run_bi_test.py`) tidak diubah — sudah ada dan berfungsi
- Output template yang sudah ditambahkan di versi 1.0.0 tetap dipertahankan, tidak dihapus
- Branch: `improvement` (sudah ada, commit terakhir 8a4af46)

---

### Task 1: Update business-strategist SKILL.md dengan self-validation dan no-summary instruction

**Files:**
- Modify: `skills/business-strategist/SKILL.md`

**Interfaces:**
- Produces: SKILL.md yang punya self-validation checklist dan no-summary instruction
- Konsumsi oleh: task 2 (tidak bergantung), task 4 (versi bump)

- [ ] **Step 1: Baca file saat ini**

Buka `skills/business-strategist/SKILL.md` dan identifikasi lokasi yang akan disisipi:
- Self-validation checklist disisip AFTER bagian "Output Template" (setelah catatan "Jika data tidak cukup...")
- "No summary" instruction disisip di awal, setelah deskripsi role di line 7

- [ ] **Step 2: Tambah self-validation checklist setelah Output Template**

Copy-paste konten berikut ke tepat setelah baris `**Catatan:** Jika data tidak cukup untuk satu komponen, tandai sebagai \"Asumsi\" atau \"Perlu divalidasi\" — jangan mengarang angka pasti.`:

```
## Self-Validation (lakukan sebelum output akhir)

Sebelum menyelesaikan output, lakukan checklist berikut dan perbaiki jika ada yang gagal:

- [ ] **Kelengkapan:** Apakah semua 10 section terisi? Jika ada section yang kosong atau hanya 1-2 kalimat, isi dengan konten yang lebih substantive. Jika benar-benar tidak ada data, tandai sebagai "Belum bisa diisi — perlu divalidasi" dan jelaskan apa data yang dibutuhkan.
- [ ] **Tidak ada ringkasan:** Apakah output adalah analisis lengkap sesuai template, BUKAN ringkasan atau overview dari analisis? Jika hanya ringkasan, regenerate dengan mengisi semua section.
- [ ] **Tidak ada klaim angka tanpa label:** Apakah setiap angka, estimasi, atau proyeksi memiliki label "Asumsi" atau "Estimasi"? Jika ada angka tanpa label, tambahkan labelnya.
- [ ] **USP dibedakan dari fitur:** Apakah USP secara eksplisit dibedakan dari fitur yang bisa diklaim kompetitor? Jika USP hanya sebut fitur, perbaiki dengan menjelaskan mengapa fitur tersebut menjadi unik dalam konteks positioning.
- [ ] **Tidak ada kontradiksi internal:** Apakah ada kontradiksi antara section (mis. target persona tapi pricing tidak cocok, positioning tapi value proposition bertentangan)? Jika ada, perbaiki.
- [ ] **Konsistensi dengan input:** Apakah analisis berbasis pada input yang diberikan, bukan asumsi yang tidak disebutkan? Jika ada asumsi baru yang tidak didukung input, tandai.
```

- [ ] **Step 3: Tambah "no summary" instruction di awal file**

Copy-paste konten berikut setelah baris `Kamu berperan sebagai business strategist. Tugasmu adalah mengubah data mentah tentang produk dan pasar menjadi kerangka bisnis (Business Knowledge Base) yang siap dipakai untuk pengambilan keputusan.`:

```
PERHATIAN: Skill ini menghasilkan analisis lengkap — bukan ringkasan. Jika pengguna meminta ringkasan, tawarkan untuk generate analisis lengkap dulu baru kemudian dibuatkan ringkasan dari analisis tersebut.
```

- [ ] **Step 4: Commit perubahan**

```bash
cd "/d/AryokPunya/Magang/BI/.claude/plugins/business-intelligence-layer"
git add skills/business-strategist/SKILL.md
git commit -m "improve(strategist): add self-validation checklist dan no-summary instruction
- tambah self-validation 6-item checklist sebelum output akhir
- tambah peringatan 'no summary' instruction di awal
- perbaiki konsistensi output struktural agar tidak hanya menghasilkan ringkasan"
```

- [ ] **Step 5: Verify**

Baca ulang `skills/business-strategist/SKILL.md` dan cek:
- [ ] Self-validation checklist ada setelah Output Template
- [ ] "No summary" instruction ada di awal file
- [ ] Output template yang lama tetap ada (tidak dihapus)

---

### Task 2: Update business-strategist-reviewer SKILL.md dengan self-validation dan chain input validation

**Files:**
- Modify: `skills/business-strategist-reviewer/SKILL.md`

**Interfaces:**
- Produces: SKILL.md dengan self-validation dan chain input validation
- Konsumsi oleh: task 3 (tidak bergantung skill lain), task 4 (versi bump)

- [ ] **Step 1: Baca file saat ini**

Buka `skills/business-strategist-reviewer/SKILL.md` dan identifikasi lokasi:
- Self-validation checklist disisip AFTER bagian "Output Template" (setelah catatan "Jangan sekadar merangkum ulang...")
- Chain input validation disisip di bagian "Input" setelah paragraf "Jika pengguna belum memberikan Business Knowledge Base..."

- [ ] **Step 2: Tambah chain input validation di bagian Input**

Copy-paste konten berikut setelah baris `Jika pengguna belum memberikan Business Knowledge Base, minta dokumen tersebut atau ringkasannya terlebih dahulu.`:

```
Jika Business Knowledge Base yang diberikan tidak lengkap (ada section yang kosong, tidak ada USP yang jelas, atau tidak ada rekomendasi go/no-go), TANYAKAN kepada pengguna sebelum melakukan review. Jangan review BKB yang tidak lengkap — hasil review akan tidak akurat.

Contoh pertanyaan: "Business Knowledge Base yang Anda berikan tidak memiliki section [X]. Sebelum saya review, apakah Anda ingin saya bantu generate section tersebut terlebih dahulu, atau Anda punya versi yang lebih lengkap?"
```

- [ ] **Step 3: Tambah self-validation checklist setelah Output Template**

Copy-paste konten berikut setelah baris `**Catatan:** Jangan sekadar merangkum ulang Business Knowledge Base — cari celah, kontradiksi, dan klaim yang tidak didukung bukti.`:

```
## Self-Validation (lakukan sebelum output akhir)

- [ ] **Kelengkapan:** Apakah semua 5 section terisi dengan analisis substantif? Jika ada yang kosong atau hanya pernyataan dangkal, perbaiki.
- [ ] **Tidak merangkum ulang:** Apakah output adalah analisis kritis (menemukan kelemahan, asumsi belum valid, risiko) dan bukan sekadar merangkum Business Knowledge Base? Jika hanya rangkuman, tambahkan analisis kritis.
- [ ] **Rujukan ke bagian spesifik:** Apakah setiap kelemahan/keunggulan yang disebut merujuk ke bagian spesifik di BKB? Jika tidak, tambahkan rujukan.
- [ ] **Konsistensi dengan BKB:** Apakah reviewer menemukan kontradiksi atau inkonsistensi dalam BKB? Jika BKB tidak ada masalah yang ditemukan, katakan mengapa (mis. "BKB cukup konsisten, tidak ada kontradiksi yang ditemukan").
- [ ] **Rekomendasi actionable:** Apakah tiap rekomendasi perbaikan konkret (bukan "perkuat analisis")? Jika masih general, spesifikkan.
```

- [ ] **Step 4: Commit perubahan**

```bash
cd "/d/AryokPunya/Magang/BI/.claude/plugins/business-intelligence-layer"
git add skills/business-strategist-reviewer/SKILL.md
git commit -m "improve(reviewer): add self-validation checklist dan chain input validation
- tambah self-validation 5-item checklist sebelum output akhir
- tambah chain input validation: cegah review BKB yang tidak lengkap
- perbaiki konsistensi review agar tidak hanya merangkum ulang"
```

- [ ] **Step 5: Verify**

Baca ulang `skills/business-strategist-reviewer/SKILL.md` dan cek:
- [ ] Chain input validation ada di bagian Input
- [ ] Self-validation checklist ada setelah Output Template
- [ ] Output template yang lama tetap ada

---

### Task 3: Update brand-story-writer SKILL.md dengan self-validation dan chain konsistensi check

**Files:**
- Modify: `skills/brand-story-writer/SKILL.md`

**Interfaces:**
- Produces: SKILL.md dengan self-validation + chain konsistensi check + chain input validation
- Konsumsi oleh: task 4 (versi bump)

- [ ] **Step 1: Baca file saat ini**

Buka `skills/brand-story-writer/SKILL.md` dan identifikasi lokasi:
- Chain input validation disisip di bagian "Input" setelah paragraf "Jika salah satu dokumen belum ada, tanyakan atau tawarkan untuk membangunnya dulu..."
- Self-validation + cross-check checklist disisip AFTER bagian "Output Template"

- [ ] **Step 2: Tambah chain input validation di bagian Input**

Copy-paste konten berikut setelah baris `Jika salah satu dokumen belum ada, tanyakan atau tawarkan untuk membangunnya dulu memakai skill `business-strategist` (dan `business-strategist-reviewer`) sebelum lanjut menulis brand story — brand story yang baik butuh insight bisnis yang solid, bukan asumsi kosong.`:

```
PENTING: Brand story yang baik butuh Business Knowledge Base yang sudah di-review (memiliki Business Audit Report). Jika pengguna hanya memberikan BKB tanpa audit report, TANYAKAN apakah pengguna ingin saya generate audit report dulu sebelum membuat brand story.

Alasan: Tanpa audit report, brand story berisiko membuat klaim yang tidak sadar bahwa klaim tersebut lemah atau bertentangan dengan kelemahan yang belum teridentifikasi.

Jika pengguna tetap ingin brand story tanpa audit report, berikan dengan catatan bahwa brand story ini dibuat berdasarkan BKB saja dan mungkin mengandung klaim yang belum teruji — dan sarankan untuk review setelah audit report tersedia.
```

- [ ] **Step 3: Tambah self-validation + cross-check checklist setelah Output Template**

Copy-paste konten berikut setelah baris `**Catatan:** Narasi harus berakar pada insight dari Business Knowledge Base/Audit Report, bukan generik atau template marketing kosong.`:

```
## Self-Validation & Cross-Check (lakukan sebelum output akhir)

### Self-Validation Checklist

- [ ] **Kelengkapan:** Apakah semua 6 section terisi? Brand narrative, core message, key claims, tone of voice, messaging pillars, elevator pitch — semuanya harus ada.
- [ ] **Konsistensi dengan BKB:** Apakah persona, USP, dan positioning yang digunakan di brand story konsisten dengan Business Knowledge Base? Jika ada perbedaan, cek ulang dan perbaiki.
- [ ] **Tidak overclaim:** Apakah ada klaim yang bertentangan dengan kelemahan yang ditemukan di Business Audit Report? Jika ada, hapus atau tandai sebagai "klaim aspirasional" dengan penjelasan.
- [ ] **Klaim didukung:** Apakah setiap key claim memiliki dasar di Business Knowledge Base atau Audit Report? Jika ada klaim tanpa dukungan, tambahkan catatan "asumsi" atau hapus.
- [ ] **Tidak generic:** Apakah brand story terasa spesifik untuk produk ini dan tidak seperti template marketing umum? Jika terasa generic, perbaiki dengan memasukkan detail spesifik dari BKB/Audit.
- [ ] **Catatan konsistensi:** Apakah bagian "Catatan Konsistensi" diisi dengan explisit menyebutkan klaim yang diadopsi dari BKB/Audit dan bagaimana brand story tetap jujur terhadap kelemahan?

### Cross-Check (lakukan setelah self-validation)

Sebelum final output, lakukan cross-check:
1. Bandingkan persona di BKB dengan persona yang digunakan di brand story — sama?
2. Bandingkan USP di BKB dengan klaim di brand story — USP yang sama atau turunannya?
3. Cek apakah ada klaim di brand story yang bertentangan dengan poin "Apa yang Lemah" atau "Apa yang Belum Valid" di Audit Report.
4. Jika ada inkonsistensi, perbaiki atau tandai sebagai asumsi.
```

- [ ] **Step 4: Commit perubahan**

```bash
cd "/d/AryokPunya/Magang/BI/.claude/plugins/business-intelligence-layer"
git add skills/brand-story-writer/SKILL.md
git commit -m "improve(brand-story): add self-validation, cross-check, dan chain input validation
- tambah self-validation 6-item checklist + cross-check 4 langkah sebelum output akhir
- tambah chain input validation: tanya dulu kalau tanpa audit report
- perbaiki konsistensi brand story agar tidak overclaim dari BKB/Audit"
```

- [ ] **Step 5: Verify**

Baca ulang `skills/brand-story-writer/SKILL.md` dan cek:
- [ ] Chain input validation ada di bagian Input
- [ ] Self-validation checklist ada setelah Output Template
- [ ] Cross-check checklist ada setelah self-validation
- [ ] Output template yang lama tetap ada

---

### Task 4: Naikkan versi plugin ke 1.1.0

**Files:**
- Modify: `.claude-plugin/plugin.json`

**Interfaces:**
- Produces: plugin.json dengan version 1.1.0
- Konsumsi oleh: tidak ada (final task)

- [ ] **Step 1: Baca file saat ini**

Buka `.claude-plugin/plugin.json` dan cek isi saat ini:
```json
{
  "name": "business-intelligence-layer",
  "description": "...",
  "version": "1.0.0",
  "author": { "name": "Aryo Adi Putro" }
}
```

- [ ] **Step 2: Update versi**

Ganti `"version": "1.0.0"` dengan `"version": "1.1.0"`.

- [ ] **Step 3: Commit perubahan**

```bash
cd "/d/AryokPunya/Magang/BI/.claude/plugins/business-intelligence-layer"
git add .claude-plugin/plugin.json
git commit -m "chore: bump plugin version to 1.1.0
- naikkan versi dari 1.0.0 ke 1.1.0
- mencerminkan penambahan self-validation, no-summary instruction,
  dan chain dependency eksplisit di 3 skill"
```

- [ ] **Step 4: Verify**

Baca ulang `.claude-plugin/plugin.json` dan cek:
- [ ] `"version": "1.1.0"` ada

---

## Self-Review Checklist

Setelah menulis rencana ini, cek:

- [ ] **Spec coverage:** Setiap bagian di spec `docs/2026-09-03-improve-bi-plugin-design.md` punya task yang mengimplementasikannya?
  - Spec bagian 3.1 (business-strategist) → Task 1 ✓
  - Spec bagian 3.2 (reviewer) → Task 2 ✓
  - Spec bagian 3.3 (brand-story-writer) → Task 3 ✓
  - Spec bagian 5 (prioritas) → Task 1-3 sudah tertangani, yang tertunda (multi-run test, automated scoring, scenario coverage) tidak masuk scope v1.1 ✓
  - Spec bagian 7 (success criteria) — tidak ada task spesifik untuk verifikasi, tapi Bisa dicek manual setelah implementasi ✓
- [ ] **Placeholder scan:** Tidak ada "TBD", "TODO", "implement later", atau "fill in details" di langkah-langkah ✓
- [ ] **Type consistency:** Tidak ada fungsi/metode yang didefinisikan dalam task berbeda dengan nama berbeda ✓
- [ ] **File structure:** Hanya 3 SKILL.md diubah + 1 plugin.json untuk versi ✓

---

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-09-03-improve-bi-plugin-v1.1.md`.

**Execution options:**

**1. Subagent-Driven (recommended)** — I dispatch a fresh subagent per task (4 tasks), review each before next

**2. Inline Execution** — Execute tasks in this session one by one

Mana yang diinginkan?
