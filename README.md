# 🎮 SecretBoard — OBS Soundboard Web App

Web app 3-halaman untuk menggantikan soundboard di OBS.

---

## File Structure

```
soundboard/
├── widget.html    → OBS Browser Source (transparent bg)
├── control.html   → Controller (HP / device lain)
├── admin.html     → Admin panel (manage list)
└── README.md
```

---

## Setup Firebase (5 menit)

### 1. Buat project Firebase
- Buka https://console.firebase.google.com
- Klik **Add Project** → beri nama → **Create**

### 2. Aktifkan Realtime Database
- Di sidebar: **Build → Realtime Database**
- Klik **Create Database**
- Pilih region terdekat (asia-southeast1 untuk Indonesia)
- Mode: **Start in test mode** (untuk development)

### 3. Daftar Web App
- Di sidebar: **Project Overview → </> (Web)**
- Register app → copy firebaseConfig object

### 4. Setup Environment Variables (.env)
Buka terminal dan instal dependensi terlebih dahulu:
```bash
npm install
```
Kemudian, salin file `.env.example` menjadi `.env` baru:
```bash
cp .env.example .env
```
Buka file `.env` dan masukkan konfigurasi dari Firebase Console:
```env
VITE_FIREBASE_API_KEY=konfigurasi_api_key_anda
VITE_FIREBASE_AUTH_DOMAIN=project_anda.firebaseapp.com
VITE_FIREBASE_DATABASE_URL=https://project_anda-default-rtdb.firebaseio.com
VITE_FIREBASE_PROJECT_ID=project_anda
VITE_FIREBASE_STORAGE_BUCKET=project_anda.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=id_sender_anda
VITE_FIREBASE_APP_ID=app_id_anda
```

### 5. Atur Database Rules (opsional, untuk keamanan)
Di Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

*(Untuk production, perketat rules-nya)*

---

## Menjalankan Aplikasi & Setup OBS

1. Jalankan server lokal Vite:
```bash
npm run dev
```
Secara default aplikasi akan berjalan di `http://localhost:5173`.
2. Di OBS, Tambah **Browser Source** baru
3. URL: `http://localhost:5173/widget.html` (atau URL hasil deploy hosting)
4. Width/Height: sesuaikan resolusi stream (misal 1920x1080)
5. Centang **"Shutdown source when not visible"** → OFF
6. Centang **"Refresh browser when scene becomes active"** → opsional

---

## Cara Pakai

### Admin (sekali setup)
1. Buka `admin.html` di browser PC
2. Isi **Name** dan **URL** untuk setiap soundboard
   - GIF: paste URL dari Giphy (`https://media.giphy.com/media/...`)
   - Video: paste URL `.mp4` yang bisa diakses publik
   - Image: URL gambar biasa
3. Untuk GIF, isi **GIF Duration** (berapa detik GIF diputar)

### Controller (saat live)
1. Buka `control.html` di HP (atau device lain)
2. Pastikan terhubung ke internet (dot hijau di pojok kanan)
3. Tap thumbnail untuk play — widget di OBS akan langsung tampil
4. Tap lagi atau tekan **■ STOP** untuk interrupt

---

## Tips URL Media

| Source   | Contoh URL |
|----------|-----------|
| Giphy    | `https://media.giphy.com/media/[ID]/giphy.gif` |
| Imgur    | `https://i.imgur.com/[ID].gif` |
| Catbox   | `https://files.catbox.moe/[ID].mp4` |
| Github | Share file → ubah link ke direct: `https://raw.githubusercontent.com/username/repository/main/nama-video.mp4` |

---

## Deploy ke Hosting (Rekomendasi)

Agar bisa diakses dari HP tanpa perlu jaringan lokal:

1. **Netlify Drop** (paling mudah):
   - Buka https://app.netlify.com/drop
   - Drag & drop folder `soundboard/`
   - Dapat URL publik instant

2. **GitHub Pages**:
   - Upload ke repo GitHub
   - Aktifkan Pages di Settings

---
# soundboards
