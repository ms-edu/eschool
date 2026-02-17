# 📝 CBT Online E-School — Full Feature

Aplikasi Ujian Berbasis Komputer (CBT) lengkap dalam satu file HTML.  
Deploy ke Vercel, Netlify, atau GitHub Pages dalam hitungan menit.

---

## ✅ Fitur Lengkap

### Admin Panel
| Fitur | Status |
|-------|--------|
| Dashboard dengan chart statistik | ✅ |
| Manajemen Paket Soal (CRUD + duplikat + token) | ✅ |
| Preview Soal sebelum aktif | ✅ |
| 5 Tipe Butir Soal | ✅ |
| Filter & pencarian soal | ✅ |
| Hasil Ujian + filter | ✅ |
| Export hasil ke Excel (.xlsx) | ✅ |
| Koreksi soal Uraian manual (slider) | ✅ |
| Analisa Per-butir (tingkat kesulitan, chart) | ✅ |
| Data Siswa (CRUD) | ✅ |
| Import Siswa dari Excel | ✅ |
| Export Siswa ke Excel | ✅ |
| Kartu Peserta + cetak | ✅ |
| Monitor Ujian Real-time | ✅ |
| Paksa selesai ujian (satu/semua) | ✅ |
| Leaderboard Siswa & Game | ✅ |
| Cetak Daftar Hadir | ✅ |
| Chat Siswa (admin bisa balas) | ✅ |
| Manajemen User Admin (multi-user) | ✅ |
| Kelola FAQ | ✅ |
| Pengaturan Umum (chat, login, nilai) | ✅ |
| Reset Data Ujian | ✅ |

### Portal Siswa
| Fitur | Status |
|-------|--------|
| Dashboard dengan info akun | ✅ |
| Daftar Ujian Aktif | ✅ |
| Konfirmasi ujian + token | ✅ |
| Timer countdown otomatis | ✅ |
| Auto-save jawaban (30 detik) | ✅ |
| Navigasi soal (sidebar + tombol) | ✅ |
| Tandai ragu-ragu | ✅ |
| Keyboard shortcut (← → untuk navigasi) | ✅ |
| 5 Tipe Soal dengan UI berbeda | ✅ |
| Riwayat Nilai | ✅ |
| Chat dengan guru/admin | ✅ |
| Mini Game Math Puzzle (skor ke leaderboard) | ✅ |
| FAQ & Bantuan | ✅ |

### Tipe Soal (5 Tipe)
1. **Pilihan Ganda** — satu jawaban benar
2. **Pilihan Ganda Kompleks** — bisa lebih dari satu jawaban
3. **Benar/Salah** — tentukan benar/salah tiap pernyataan
4. **Uraian** — jawaban teks bebas (koreksi manual guru)
5. **Menjodohkan** — pasangkan kolom kiri dan kanan

---

## 🚀 Cara Deploy ke Vercel

### Metode 1: Upload Langsung (Paling Mudah)
1. Buka [vercel.com](https://vercel.com) → Login
2. Klik **"Add New → Project"**
3. Klik **"Upload"** (atau drag & drop folder ini)
4. Vercel otomatis deploy dalam ~30 detik
5. Anda mendapat URL seperti `https://cbt-online.vercel.app`

### Metode 2: Via GitHub
1. Upload folder ini ke repositori GitHub
2. Buka Vercel → Import dari GitHub
3. Pilih repo → Deploy
4. Setiap push ke GitHub otomatis update

### Metode 3: Vercel CLI
```bash
npm install -g vercel
cd folder-ini
vercel
# Ikuti instruksi, pilih "Other" untuk framework
```

---

## 🗄️ Setup Supabase Database

### Langkah 1: Buat Project Supabase
1. Buka [supabase.com](https://supabase.com) → Buat akun
2. Klik **"New Project"** → isi nama dan password
3. Pilih region terdekat (Singapore direkomendasikan)
4. Tunggu ~2 menit project siap

### Langkah 2: Jalankan SQL Schema
1. Di Supabase: **SQL Editor → New Query**
2. Salin SQL dari tombol "📋 SQL Setup" di halaman login aplikasi
3. Klik **"Run"**
4. Semua tabel otomatis terbuat

### Langkah 3: Ambil Kredensial
1. **Project Settings → API**
2. Salin:
   - **Project URL**: `https://xxxx.supabase.co`
   - **anon/public key**: `eyJhbGci...`

### Langkah 4: Konfigurasi Aplikasi
1. Buka aplikasi yang sudah di-deploy
2. Klik **"⚙️ Konfigurasi Supabase"**
3. Isi URL dan Key → Simpan
4. Refresh halaman

### Langkah 5: Setup Row Level Security (Opsional)
Untuk development, jalankan SQL ini di Supabase:
```sql
-- Buat semua tabel bisa diakses (development mode)
do $$
declare t text;
begin
  for t in select tablename from pg_tables where schemaname = 'public'
  loop
    execute 'alter table ' || t || ' enable row level security';
    execute 'create policy "allow_all_' || t || '" on ' || t || ' for all using (true) with check (true)';
  end loop;
end $$;
```
> ⚠️ Untuk production, buat policy yang lebih ketat!

---

## 🔑 Login Default

| Role | Username | Password |
|------|----------|----------|
| Admin | `admin` | `admin` |
| Siswa (demo) | `123456` | `123456` |
| Siswa (demo) | `123457` | `123457` |

**Ganti password admin segera setelah login pertama!**

---

## 📋 Format Kunci Jawaban

| Tipe Soal | Format Kunci |
|-----------|--------------|
| Pilihan Ganda | `pilihan_1` |
| PG Kompleks | `pilihan_1,pilihan_3` |
| Benar/Salah | `Benar\|Salah\|Benar\|Salah` |
| Uraian | Teks referensi (untuk panduan koreksi) |
| Menjodohkan | `Kiri1:Kanan1\|Kiri2:Kanan2\|Kiri3:Kanan3` |

---

## 🎮 Mode Demo
Tanpa Supabase, klik **"🎮 Mode Demo"** untuk mencoba semua fitur dengan data sampel.  
Data demo tersimpan di memori browser dan hilang saat halaman di-refresh.

---

## 📁 Struktur File

```
├── index.html      ← Seluruh aplikasi (HTML + CSS + JS)
├── vercel.json     ← Konfigurasi deployment Vercel
└── README.md       ← Dokumentasi ini
```

---

## 🔧 Troubleshooting

**Q: Koneksi Supabase gagal**  
A: Pastikan URL dan Key benar. Cek browser console untuk error detail. Pastikan RLS policy sudah diset.

**Q: Data tidak tersimpan**  
A: Mode demo tidak menyimpan ke database. Hubungkan Supabase untuk data permanen.

**Q: Timer berhenti saat browser di-minimize**  
A: Normal behavior browser. Timer backend tersimpan di `waktu_sisa` pada database, ujian bisa dilanjutkan.

**Q: Gambar soal tidak muncul**  
A: Gunakan URL gambar yang bisa diakses publik (contoh: Google Drive, Imgur, atau Supabase Storage).

**Q: Import siswa gagal**  
A: Pastikan format header kolom Excel persis: `nama_siswa`, `username`, `password`, `kelas`, `rombel`
