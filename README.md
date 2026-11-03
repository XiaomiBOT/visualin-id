# visualin.id — PHP 8.2 + Supabase + Gemini

## Persyaratan
PHP 8.2+, ekstensi cURL dan mbstring, HTTPS, project Supabase, Gemini API key.

## Setup Supabase
1. Buat project di https://supabase.com/dashboard
2. Ambil Project URL dan **Secret API Key** (`sb_secret_...`) dari Project Settings > API Keys.
3. Buka SQL Editor, jalankan seluruh isi file `supabase.sql`.
4. Secret Key hanya disimpan di PHP server. Jangan taruh di browser, HTML, JavaScript, atau repositori publik. Key ini memiliki akses istimewa dan melewati RLS.

## Konfigurasi
Edit `config/config.php`:
```php
const SUPABASE_URL = 'https://PROJECT-REF.supabase.co';
const SUPABASE_SECRET_KEY = 'sb_secret_...';
const GEMINI_API_KEY = 'API_KEY_GEMINI';
const GEMINI_MODEL = 'gemini-3.8-flash';
```
Gemini key: https://aistudio.google.com/app/apikey. Model dapat diganti sesuai model yang tersedia pada project Google AI.

## Upload cPanel
1. Upload ZIP ke `public_html`, extract, lalu pastikan `index.php` berada langsung di document root.
2. Aktifkan HTTPS.
3. Buka `/admin/create-admin.php`, buat username dan password unik minimal 12 karakter.
4. Setelah berhasil, **hapus `admin/create-admin.php` dari hosting**.
5. Login di `/admin/login.php`.

## Error umum
- Supabase belum dikonfigurasi: cek Project URL dan Secret API Key.
- HTTP 401/403: pastikan key dari project yang benar; jangan gunakan publishable key sebagai secret.
- HTTP 404 / relation not found: jalankan `supabase.sql`.
- cURL error: aktifkan ekstensi cURL dan periksa koneksi keluar hosting.
- Gemini HTTP 502: cek API key, kuota, nama model, dan koneksi hosting.
- mb_strlen undefined: aktifkan ekstensi mbstring.
- CSRF/session error: gunakan HTTPS konsisten lalu muat ulang.

## Keamanan
Secret Key hanya di server. RLS aktif dan akses role publik dicabut. Backend PHP melakukan autentikasi admin. Gunakan HTTPS, password kuat, backup berkala, dan rotasi key jika bocor. Tambahkan CAPTCHA/WAF jika komentar diserang spam.
