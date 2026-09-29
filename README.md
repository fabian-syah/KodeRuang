# 🧩 KodeRuang

Platform komunitas untuk developer — berbagi resource coding (tools, repositori, tutorial, artikel) dengan sistem voting, komentar, bookmark, dan profil pengembang. Dibangun dengan Next.js App Router, Supabase, dan deploy ke Cloudflare Workers via OpenNext.

Live: [koderuang.fabian-syah.workers.dev](https://koderuang.fabian-syah.workers.dev) *(sesuaikan bila URL berubah)*

---

## ✨ Fitur

**Konten & penemuan**
- **Feed resource** dengan voting (upvote/downvote) dan skor reputasi.
- **Kategori & stack** — halaman `/category/[slug]` dan `/stack/[slug]` untuk menelusuri berdasarkan topik atau teknologi.
- **Halaman Trending** — resource terpopuler berdasarkan aktivitas komunitas.
- **Pencarian & filter** — penyaringan daftar resource.

**Interaksi sosial**
- **Komentar** pada setiap resource.
- **Bookmark** — simpan resource ke halaman `/saved`.
- **Profil publik** — `/user/[username]` dan `/user/me`, lengkap dengan daftar kontribusi dan peringkat.
- **Sistem reputasi** — poin bertambah dari kontribusi yang divalidasi komunitas.

**Kontribusi & moderasi**
- **Kirim resource** lewat `/submit`.
- **Panel admin** — `/admin` untuk moderasi, plus `/admin/reports` untuk menangani laporan.
- **Laporan konten** — pengguna bisa melaporkan resource bermasalah.

**Asisten AI**
- **Chat AI terintegrasi** (Vercel AI SDK + Groq) untuk membantu menjawab pertanyaan seputar resource.

## 🧰 Teknologi

| Lapisan | Teknologi |
|---|---|
| Framework | Next.js (App Router), React, TypeScript |
| Basis data & Auth | Supabase (Postgres + Auth + RLS) |
| AI | Vercel AI SDK (`ai`, `@ai-sdk/react`), Groq |
| Deploy | Cloudflare Workers via `@opennextjs/cloudflare` |
| UI | Tailwind CSS, Lucide, React Syntax Highlighter |

## 🚀 Cara Menjalankan Lokal

```bash
# 1. Clone
git clone https://github.com/fabian-syah/KodeRuang.git
cd KodeRuang

# 2. Pasang dependensi
npm install

# 3. Variabel lingkungan
cp .env.example .env.local
```

Isi `.env.local`:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
GROQ_API_KEY=your_groq_key
```

```bash
# 4. Siapkan skema basis data
#    Jalankan salah satu dump SQL berikut di SQL Editor Supabase Anda:
#    - supabase_schema.sql      (skema utama)
#    - update_schema_roles_ranking.sql
#    - fix_reputation_glitch.sql
#    (schema_dump.sql adalah snapshot lengkap untuk referensi)

# 5. Jalankan
npm run dev
```

Buka [http://localhost:3000](http://localhost:3000).

### Skrip tersedia

| Perintah | Fungsi |
|---|---|
| `npm run dev` | Server pengembangan |
| `npm run build` | Build produksi |
| `npm run preview` | Build + preview Cloudflare secara lokal |
| `npm run deploy` | Build + deploy ke Cloudflare Workers |
| `npm run cf-typegen` | Menghasilkan tipe untuk binding Cloudflare |

## 🗄️ Catatan Basis Data

Repositori ini memuat beberapa file SQL di root. Urutan penerapannya:

1. `supabase_schema.sql` — skema dasar (tabel, relasi, kebijakan RLS).
2. `update_schema_roles_ranking.sql` — penambahan peran dan sistem peringkat.
3. `fix_reputation_glitch.sql` — perbaikan perhitungan reputasi.
4. `schema_dump.sql` — snapshot lengkap, untuk referensi/verifikasi saja.

## 🔐 Keamanan

- RLS Supabase harus aktif pada semua tabel yang menyimpan data pengguna.
- Jangan pernah commit `.env.local` atau kunci `SERVICE_ROLE`.
- Kebijakan moderasi admin bergantung pada kolom peran di tabel profil — pastikan hanya peran yang sah yang bisa mengubahnya.

## 📄 Lisensi

MIT
