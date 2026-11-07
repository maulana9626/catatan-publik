# Ruang Catatan Publik

Aplikasi statis untuk berbagi catatan publik. Catatan disimpan di Supabase (Postgres), bukan di `localStorage`. Pengunjung bisa membaca dan menerbitkan catatan; pengunjung tidak mendapat hak mengedit atau menghapus.

## 1. Siapkan Supabase

1. Buat project di [supabase.com](https://supabase.com/) dan tunggu sampai database siap.
2. Di **SQL Editor**, jalankan seluruh isi [`supabase/schema.sql`](supabase/schema.sql). Ini membuat tabel `public.notes`, mengaktifkan Row Level Security (RLS), serta menambahkan kebijakan untuk membaca dan membuat catatan.
3. Dari pengaturan API project, salin **Project URL** dan **anon/public key** (bisa disebut `anon` atau `publishable`).
4. Di repo, edit `config.js`, ganti `YOUR_SUPABASE_PROJECT_URL` dan `YOUR_SUPABASE_ANON_OR_PUBLISHABLE_KEY` dengan nilai dari Supabase, lalu commit perubahan.

**Jangan pernah masukkan `service_role` atau secret key ke `config.js` atau frontend.** Anon/publishable key memang terlihat di browser; keamanan akses data ditentukan oleh RLS. Karena semua orang bisa mengirim catatan tanpa login, konten akan langsung terlihat publik. Jangan kirim data pribadi/rahasia. Untuk penggunaan ramai, tambahkan CAPTCHA/rate limiting dan moderasi.

## 2. Deploy di Vercel

1. Push repo ini ke GitHub.
2. Masuk ke [Vercel](https://vercel.com/), pilih **Add New → Project**, lalu import `maulana9626/catatan-publik`.
3. Karena ini situs HTML statis, biarkan **Framework Preset: Other**. Kosongkan **Build Command** dan **Output Directory**; root repo berisi `index.html`.
4. Tekan **Deploy**. Setiap push berikutnya ke branch yang terhubung akan memicu deployment baru.

Setelah deploy selesai, gunakan URL `.vercel.app` yang diberikan Vercel. Untuk mengubah domain atau pengaturan deployment, buka **Project → Settings** di Vercel.

## Pengembangan lokal

Setelah mengisi `config.js`, jalankan server statis dari root repo, misalnya `python -m http.server 8000`, lalu buka `http://localhost:8000`.
