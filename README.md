🍜 MamieJago – Premium Street Food Modern

MamieJago adalah platform website e-commerce untuk makanan siap saji (mie jebew, wonton, dimsum) dengan desain elegan, modern, dan user-friendly. Dibangun dengan Node.js, Express, MongoDB Atlas, Tailwind CSS, dan Vanilla JavaScript, dilengkapi fitur lengkap seperti keranjang belanja, checkout, invoice otomatis, integrasi pembayaran QRIS (Pakasir), serta panel admin yang aman.

---

✨ Fitur Utama

· Frontend Responsif – Mobile-first, dark mode, animasi halus.
· Manajemen Produk – CRUD produk dengan gambar, level pedas, rating.
· Sistem Review – Pengguna dapat memberi rating & komentar, dimoderasi admin.
· Keranjang Belanja – Tersimpan di localStorage, update kuantitas, hapus item.
· Checkout & Invoice – Form pemesan, generate nomor invoice unik, download invoice (HTML).
· Pembayaran QRIS – Integrasi dengan Pakasir, menampilkan QR code, webhook untuk update status.
· Admin Panel – Login dengan JWT, dashboard statistik, kelola produk, moderasi review.
· WhatsApp Integration – Tombol pesan via WhatsApp, otomatis terformat rapi.

---

🛠️ Teknologi yang Digunakan

Backend

· Node.js + Express.js
· MongoDB Atlas (Mongoose ODM)
· JWT untuk autentikasi
· Bcrypt untuk hashing password
· Axios untuk HTTP request
· Dotenv untuk konfigurasi environment

Frontend

· HTML5, Tailwind CSS
· Vanilla JavaScript
· Lucide Icons
· LocalStorage untuk cart & theme

Pembayaran

· Pakasir API (QRIS)

---

📋 Prasyarat

Sebelum memulai, pastikan Anda memiliki:

· Node.js (v18 atau lebih baru)
· MongoDB Atlas akun dan cluster (gratis)
· Akun Pakasir untuk mendapatkan API Key (opsional, bisa di-skip dulu dengan mock)

---

🚀 Cara Instalasi & Menjalankan

1. Clone Repository

git clone https://github.com/username/mamiejago.git
cd mamiejago


2. Install Dependencies

npm install


3. Setup Environment Variable

Buat file .env di root folder dan isi dengan:

PORT=5000
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/mamieJago?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_key_change_this
BCRYPT_ROUNDS=10
PAKASIR_API_KEY=your_pakasir_api_key
PAKASIR_WEBHOOK_SECRET=your_webhook_secret
BASE_URL=http://localhost:5000

Catatan: Ganti <username>, <password>, dan nilai lainnya ganti sama api key punya lu

4. Buat User Admin (Seeder)

Kirim request POST ke endpoint /api/auth/register menggunakan Postman atau cURL:

{
  "username": "admin",
  "password": "admin123"
}
```

Contoh cURL:


curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username": "admin", "password": "admin123"}

Penting: Setelah berhasil, segera hapus atau nonaktifkan route /register di routes/auth.routes.js agar tidak dapat diakses publik.

5. Jalankan Aplikasi

Mode Development (dengan nodemon)

npm run dev

Mode Production

npm start


Akses website di http://localhost:5000

---

📁 Struktur Folder

mamieJago/
├── .env
├── .gitignore
├── package.json
├── server.js
├── /public
│   ├── index.html
│   ├── product.html
│   ├── checkout.html
│   ├── invoice.html
│   ├── admin-login.html
│   ├── admin.html
│   ├── /css
│   │   └── style.css
│   └── /js
│       └── script.js
├── /routes
│   ├── auth.routes.js
│   ├── product.routes.js
│   ├── order.routes.js
│   ├── review.routes.js
│   └── payment.routes.js
├── /controllers
│   ├── auth.controller.js
│   ├── product.controller.js
│   ├── order.controller.js
│   ├── review.controller.js
│   └── payment.controller.js
├── /models
│   ├── User.js
│   ├── Product.js
│   ├── Order.js
│   ├── Review.js
│   └── Payment.js
├── /middlewares
│   ├── auth.middleware.js
│   └── error.middleware.js
└── /utils
    ├── jwt.js
    ├── bcrypt.js
    ├── generateInvoice.js
    └── pakasir.js



📡 API Endpoints

Autentikasi

· POST /api/auth/login – Login admin, mengembalikan token JWT.

Produk

· GET /api/products – Mendapatkan semua produk (public)
· GET /api/products/:id – Detail produk (public)
· POST /api/products – Tambah produk (admin only)
· PUT /api/products/:id – Update produk (admin only)
· DELETE /api/products/:id – Hapus produk (admin only)

Order

· POST /api/orders – Buat pesanan baru (public)
· GET /api/orders/invoice/:invoiceNumber – Ambil data order berdasarkan nomor invoice (public)
· GET /api/orders – Mendapatkan semua order (admin only)

Review

· POST /api/reviews – Tambah review (public)
· GET /api/reviews/product/:productId – Ambil review per produk (public, hanya yang disetujui)
· GET /api/reviews/pending – Ambil review yang belum disetujui (admin only)
· PUT /api/reviews/:id/approve – Setujui review (admin only)
· DELETE /api/reviews/:id – Hapus review (admin only)

Payment

· POST /api/payments/create-qris – Generate QRIS untuk order tertentu
· POST /api/payments/webhook – Webhook dari Pakasir untuk update status pembayaran

---

🖥️ Cara Penggunaan

Untuk Pengunjung / Pembeli

1. Buka halaman utama, lihat menu di grid.
2. Klik gambar menu untuk melihat detail.
3. Tambahkan ke keranjang, atur kuantitas.
4. Klik ikon keranjang, lalu Checkout.
5. Isi nama dan nomor WhatsApp, buat pesanan.
6. Setelah pesanan dibuat, akan diarahkan ke halaman invoice dengan QRIS.
7. Scan QRIS untuk membayar (simulasi atau integrasi Pakasir).
8. Status pembayaran akan berubah menjadi PAID setelah diverifikasi webhook.
9. Unduh invoice atau kirim via WhatsApp.

Untuk Admin

1. Akses /admin-login.html, login dengan kredensial yang telah dibuat.
2. Di dashboard, lihat statistik (total pesanan, menu terlaris, pendapatan hari ini).
3. Kelola produk: tambah, edit, hapus (termasuk upload gambar).
4. Moderasi review: setujui atau tolak ulasan masuk.
5. Lihat daftar pesanan (belum diimplementasikan detail di frontend, tapi endpoint tersedia).

---

👨‍💻 Credit Developer

Proyek MamieJago dikembangkan oleh:

· Nama Developer: Vio Atmajaya Saputra
    Peran: Full-stack Developer
    Kontak: vioatmajaya@gmail.com
    GitHub: github.com/vioatmaja88

Terima kasih kepada semua pihak yang telah mendukung terciptanya platform ini.

---

📄 Lisensi

Proyek ini dilisensikan di bawah MIT License – Anda bebas menggunakan, memodifikasi, dan mendistribusikan kembali dengan menyertakan atribusi kepada pengembang asli.
Jadi boleh lu edit tapi jangan hapus creditnya lah, hargai developer yang buatnya terus jangan lupa start di githubnya klik

---

🐛 Troubleshooting

· Error MongoDB connection error – Pastikan koneksi internet stabil, IP Address Anda diizinkan di MongoDB Atlas (Network Access), dan MONGODB_URI benar.
· Error JWT_SECRET not set – Periksa file .env sudah terisi dengan benar.
· QRIS tidak muncul – Jika tidak menggunakan Pakasir sungguhan, Anda bisa mengganti qrCodeUrl dengan gambar dummy.
· Gambar produk tidak tampil – Gunakan URL gambar yang valid atau simpan gambar di folder /public/assets.

Jika menemui kendala lain, silakan fix sendiri karna gue juga udah cape bikin nih project

---

Selamat menikmati MamieJago! 🍜✨