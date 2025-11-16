# 🚀 Panduan Deploy ke GitHub & Online

Panduan lengkap untuk deploy aplikasi Laravel ini ke GitHub dan platform online.

---

## 📦 Langkah 1: Siapkan Repository GitHub

### 1.1. Buat Repository di GitHub

1. Login ke **GitHub.com**
2. Klik tombol **"+"** di kanan atas → **"New repository"**
3. Isi:
   - **Repository name:** `laravel-products-integration` (atau nama lain)
   - **Description:** "Laravel Products Integration dengan DummyJSON API"
   - **Visibility:** Public atau Private (pilih sesuai kebutuhan)
   - **JANGAN** centang "Initialize with README"
4. Klik **"Create repository"**

### 1.2. Inisialisasi Git di Project

Buka terminal/command prompt di folder project Anda:

```bash
cd "c:\xampp\htdocs\Materi Programming\intregation"

# Inisialisasi Git
git init

# Tambahkan semua file
git add .

# Commit pertama
git commit -m "Initial commit - Laravel Products Integration"

# Tambahkan remote GitHub
git remote add origin https://github.com/USERNAME/REPO_NAME.git

# Ganti USERNAME dengan username GitHub Anda
# Ganti REPO_NAME dengan nama repository yang dibuat

# Push ke GitHub
git branch -M main
git push -u origin main
```

**Catatan:** Jika diminta login, gunakan:
- **Username:** username GitHub Anda
- **Password:** Gunakan **Personal Access Token** (bukan password GitHub)

**Cara buat Personal Access Token:**
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token
3. Beri nama dan centang scope `repo`
4. Copy token dan gunakan sebagai password

---

## 🌐 Langkah 2: Deploy ke Platform Online

Karena Laravel memerlukan server PHP, kita tidak bisa deploy langsung ke GitHub Pages. Gunakan platform berikut:

---

### **Opsi 1: Railway.app (PALING MUDAH & GRATIS)**

Railway terintegrasi langsung dengan GitHub dan sangat mudah digunakan.

#### Langkah-langkah:

1. **Daftar di Railway**
   - Kunjungi: https://railway.app
   - Klik **"Start a New Project"**
   - Pilih **"Deploy from GitHub repo"**
   - Login dengan GitHub account Anda

2. **Pilih Repository**
   - Pilih repository yang baru saja dibuat
   - Railway akan otomatis detect Laravel

3. **Setup Environment Variables**
   Di Railway dashboard, klik pada service → **Variables** tab, tambahkan:
   ```
   APP_NAME=Products Integration
   APP_ENV=production
   APP_KEY=base64:YOUR_KEY_HERE
   APP_DEBUG=false
   APP_URL=https://your-app.railway.app
   ```

   **Generate APP_KEY:**
   ```bash
   php artisan key:generate --show
   ```
   Copy hasilnya dan paste ke `APP_KEY` di Railway.

4. **Deploy**
   - Railway akan otomatis build dan deploy
   - Tunggu beberapa menit
   - Setelah selesai, klik **"Settings"** → **"Generate Domain"**
   - Anda akan mendapat link seperti: `https://your-app.railway.app`

5. **Update APP_URL**
   - Setelah mendapat domain, update `APP_URL` di Railway dengan domain yang baru

**Keuntungan:**
- ✅ Gratis tier tersedia ($5 credit/bulan)
- ✅ Auto-deploy dari GitHub
- ✅ SSL otomatis
- ✅ Mudah digunakan

---

### **Opsi 2: Render.com (GRATIS)**

Render juga terintegrasi dengan GitHub.

#### Langkah-langkah:

1. **Daftar di Render**
   - Kunjungi: https://render.com
   - Klik **"Get Started for Free"**
   - Login dengan GitHub account

2. **Create New Web Service**
   - Klik **"New +"** → **"Web Service"**
   - Connect GitHub repository
   - Pilih repository Anda

3. **Konfigurasi:**
   - **Name:** `laravel-products` (atau nama lain)
   - **Environment:** `PHP`
   - **Build Command:**
     ```bash
     composer install --optimize-autoloader --no-dev && php artisan config:cache && php artisan route:cache
     ```
   - **Start Command:**
     ```bash
     php artisan serve --host=0.0.0.0 --port=$PORT
     ```

4. **Environment Variables:**
   Klik **"Environment"** tab, tambahkan:
   ```
   APP_NAME=Products Integration
   APP_ENV=production
   APP_KEY=base64:YOUR_KEY_HERE
   APP_DEBUG=false
   APP_URL=https://your-app.onrender.com
   ```

5. **Deploy**
   - Klik **"Create Web Service"**
   - Render akan build dan deploy
   - Setelah selesai, Anda akan mendapat link: `https://your-app.onrender.com`

**Keuntungan:**
- ✅ Gratis tier tersedia
- ✅ Auto-deploy dari GitHub
- ✅ SSL otomatis

**Catatan:** Render free tier akan sleep setelah 15 menit tidak aktif.

---

### **Opsi 3: Heroku (GRATIS dengan Limit)**

#### Langkah-langkah:

1. **Install Heroku CLI**
   - Download: https://devcenter.heroku.com/articles/heroku-cli
   - Install dan restart terminal

2. **Login ke Heroku**
   ```bash
   heroku login
   ```

3. **Create App**
   ```bash
   cd "c:\xampp\htdocs\Materi Programming\intregation"
   heroku create your-app-name
   ```

4. **Setup Buildpack**
   ```bash
   heroku buildpacks:set heroku/php
   ```

5. **Setup Environment Variables**
   ```bash
   heroku config:set APP_KEY=$(php artisan key:generate --show)
   heroku config:set APP_ENV=production
   heroku config:set APP_DEBUG=false
   heroku config:set APP_URL=https://your-app-name.herokuapp.com
   ```

6. **Deploy**
   ```bash
   git push heroku main
   ```

7. **Buka Aplikasi**
   ```bash
   heroku open
   ```

---

## 🔧 File Konfigurasi yang Diperlukan

Saya sudah membuat file-file berikut untuk memudahkan deploy:

### 1. `.gitignore`
File ini memastikan file sensitif tidak di-commit ke GitHub.

### 2. `Procfile` (untuk Heroku)
```
web: php artisan serve --host=0.0.0.0 --port=$PORT
```

### 3. `railway.json` (untuk Railway)
Konfigurasi build dan deploy untuk Railway.

### 4. `render.yaml` (untuk Render)
Konfigurasi untuk Render.com.

---

## 📝 Checklist Sebelum Deploy

Sebelum push ke GitHub, pastikan:

- [ ] File `.env` **TIDAK** di-commit (cek `.gitignore`)
- [ ] File `.env.example` ada (template untuk production)
- [ ] Semua file penting sudah di-commit
- [ ] Repository GitHub sudah dibuat
- [ ] Personal Access Token sudah dibuat (jika perlu)

---

## 🚀 Quick Start (Railway - Paling Mudah)

```bash
# 1. Inisialisasi Git
cd "c:\xampp\htdocs\Materi Programming\intregation"
git init
git add .
git commit -m "Initial commit"

# 2. Push ke GitHub
git remote add origin https://github.com/USERNAME/REPO_NAME.git
git branch -M main
git push -u origin main

# 3. Deploy ke Railway
# - Kunjungi railway.app
# - Login dengan GitHub
# - Pilih repository
# - Setup environment variables
# - Deploy!
```

---

## 🔗 Link yang Akan Anda Dapatkan

Setelah deploy, Anda akan mendapat link seperti:

- **Railway:** `https://your-app.railway.app`
- **Render:** `https://your-app.onrender.com`
- **Heroku:** `https://your-app-name.herokuapp.com`

Link ini bisa dibagikan ke siapa saja untuk mengakses aplikasi Anda!

---

## 🐛 Troubleshooting

### Error: "Repository not found"
- Pastikan repository sudah dibuat di GitHub
- Pastikan URL repository benar
- Pastikan Anda sudah login ke GitHub

### Error: "Authentication failed"
- Gunakan Personal Access Token, bukan password
- Pastikan token memiliki permission `repo`

### Error: "APP_KEY not set"
- Generate key: `php artisan key:generate --show`
- Set di environment variables platform

### Error: "500 Internal Server Error"
- Cek log di platform dashboard
- Pastikan semua environment variables sudah di-set
- Pastikan `APP_DEBUG=false` di production

---

## 📚 Resources

- **GitHub Docs:** https://docs.github.com
- **Railway Docs:** https://docs.railway.app
- **Render Docs:** https://render.com/docs
- **Heroku PHP:** https://devcenter.heroku.com/articles/getting-started-with-php

---

## ✅ Setelah Deploy

1. **Test aplikasi** di link yang diberikan
2. **Share link** ke teman/klien
3. **Monitor** di dashboard platform
4. **Update** dengan push ke GitHub (auto-deploy)

**Selamat! Aplikasi Anda sudah online! 🎉**

