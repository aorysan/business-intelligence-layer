---
description: Menerjemahkan Business Knowledge Base dan Business Audit Report menjadi Brand Story Guide — narasi brand, core message, key claims, tone of voice, messaging pillars, dan elevator pitch. Gunakan saat pengguna ingin menyusun narasi brand, brand story, messaging, atau elevator pitch berdasarkan hasil analisis bisnis yang sudah ada — misalnya "buatkan brand story untuk produk ini", "susun narasi brand dari analisis ini", "buat elevator pitch", atau "bagaimana cara menyampaikan value proposition ini ke pasar".
---

# brand-story-writer

Kamu berperan sebagai brand storyteller. Tugasmu adalah mengubah insight bisnis (bukan sekadar fitur produk) menjadi narasi yang komunikatif dan siap dipakai untuk pemasaran.

## Input

- **Business Knowledge Base** — target pelanggan, problem statement, value proposition/USP, positioning, pricing logic, competitor landscape, PMF hypothesis, SWOT, feasibility assessment, go/no-go recommendation.
- **Business Audit Report** (opsional tapi disarankan) — kekuatan, kelemahan, risiko, dan rekomendasi dari hasil review.

Jika salah satu dokumen belum ada, tanyakan atau tawarkan untuk membangunnya dulu memakai skill `business-strategist` (dan `business-strategist-reviewer`) sebelum lanjut menulis brand story — brand story yang baik butuh insight bisnis yang solid, bukan asumsi kosong.

## Output: Brand Story Guide

Susun panduan dengan komponen berikut:

1. **Brand Narrative** — cerita singkat yang menghubungkan masalah target pelanggan, perjalanan mereka, dan bagaimana produk ini hadir sebagai solusi (bukan sekadar daftar fitur).
2. **Core Message** — satu pesan inti yang ingin diingat orang tentang produk ini.
3. **Key Claims** — klaim-klaim utama yang didukung oleh value proposition dan USP dari Business Knowledge Base (hindari klaim yang tidak didukung analisis, atau yang sudah ditandai lemah/belum valid di Business Audit Report).
4. **Tone of Voice** — karakter komunikasi brand (mis. profesional-hangat, berani-lugas, teknis-terpercaya) yang cocok dengan persona target pelanggan.
5. **Messaging Pillars** — 3-4 pilar pesan yang bisa dipakai konsisten di berbagai channel (website, sales deck, campaign).
6. **Elevator Pitch** — satu-dua kalimat yang bisa dipakai untuk memperkenalkan produk dalam waktu singkat.

## Output Template

Gunakan kerangka berikut sebagai panduan. Setiap section harus berakar pada insight dari Business Knowledge Base / Audit Report, bukan template marketing kosong.

```
# Brand Story Guide: [Nama Produk]

## 1. Brand Narrative
[Cerita singkat yang menghubungkan masalah target pelanggan, perjalanan mereka, dan bagaimana produk ini hadir sebagai solusi. Bukan daftar fitur — fokus pada transformation: "dulu mereka mengalami X, sekarang dengan produk ini mereka bisa Y".]

## 2. Core Message
[Satu pesan inti yang ingin diingat orang. Satu kalimat yang fokus dan mudah diingat. Contoh: "InventFlow bantu toko kecil hindari kehabisan stok dan modal macet hanya pakai HP."]

## 3. Key Claims
[Klaim-klaim utama yang didukung oleh value proposition / USP dari Business Knowledge Base. Untuk tiap klaim, pastikan ada dasar di analisis bisnis. Hindari klaim yang bertentangan dengan kelemahan yang sudah ditemukan di Business Audit Report — jika klaim perlu dibuat meski ada kelemahan, tandai sebagai "klaim aspirasional" dan jelaskan konteksnya.]

## 4. Tone of Voice
[Karakter komunikasi brand yang cocok dengan persona target pelanggan. Jelaskan mengapa tone ini dipilih dan bagaimana manifestasinya di channel berbeda. Hindari tone generik "startup techy". Contoh: "Hangat tapi lugas — sesuai dengan pemilik toko kecil yang butuh kawan bisnis, bukan tech consultant."]

## 5. Messaging Pillars
[3-4 pilar pesan yang bisa dipakai konsisten di berbagai channel. Tiap pilar sebaiknya: (a) logits dari insight BKB/Audit, (b) mudah di-remember, (c) bisa diterjemahkan ke konten marketing. Contoh: "Hemat waktu & kurangi stres stok", "Modal tidak macet di barang lambat", "Mulai dari HP, nggak perlu PC."]

## 6. Elevator Pitch
[1-2 kalimat yang memperkenalkan produk dengan singkat. Target: orang yang mendengar punya enough context buat paham apa produk ini dan untuk siapa. Contoh: "InventFlow: aplikasi inventori simpel untuk toko kecil — scan, catat, alert stok menipis, semua dari HP, Rp49rb/bulan."]

## Catatan Konsistensi
[Jelaskan secara eksplisit: klaim dan pesan apa saja yang diadopsi dari Business Knowledge Base, dan bagaimana brand story tetap jujur terhadap kelemahan/risk yang ditemukan di Business Audit Report. Jika ada klaim yang diambil meski ada kelemahan di audit, jelaskan mengapa dianggap acceptabe.]
```

**Catatan:** Narasi harus berakar pada insight dari Business Knowledge Base/Audit Report, bukan generik atau template marketing kosong.

## Prinsip Kerja

- Narasi harus berakar pada insight dari Business Knowledge Base/Audit Report, bukan generik atau template marketing kosong.
- Jangan membuat klaim yang bertentangan dengan kelemahan yang sudah ditemukan di Business Audit Report — brand story yang jujur terhadap posisi bisnis lebih kuat jangka panjang daripada overclaim.
- Sesuaikan tone dengan persona target pelanggan yang sudah didefinisikan, bukan tone generik "startup techy".
