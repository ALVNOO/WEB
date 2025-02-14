# WEB

## ANALISIS

### Analisis Routing dan Navigasi

- / =  Menampilkan halaman utama (index.html)
- /login = Halaman login dan proses autentikasi
- /logout	= Logout dan hapus sesi
- /students	= Menampilkan daftar mahasiswa (student.html)
- /add	= Menambahkan mahasiswa baru
- /delete/<int:id> = Menghapus mahasiswa berdasarkan ID
- /edit/<int:id>	= Mengedit informasi mahasiswa
- /users/create	= Membuat akun baru

---

### Impor Modul dan Konfigurasi Aplikasi
![IMPORT](https://github.com/user-attachments/assets/4dc31218-6692-42db-809c-d0d95235f363)

- Flask → Framework utama
- render_template → Untuk menampilkan HTML
- request → Mengambil data dari form
- redirect & url_for → Untuk berpindah halaman
- session → Menyimpan data user yang login
- flash → Menampilkan pesan notifikasi
- SQLAlchemy → ORM untuk mengelola database
- text → Eksekusi SQL dalam bentuk string
- HTTPBasicAuth → Untuk autentikasi berbasis HTTP
- werkzeug.security → Untuk hash password

---

### Routing, Redirecting

### /login
![LOGIN](https://github.com/user-attachments/assets/c3751424-7dca-4dbf-a831-c715827453de)

Proses
- User mengisi username dan password
- Jika cocok dengan database akan redirect ke /students (tampilan daftar mahasiswa) dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students
- Jika gagal tetap di /login dan menampilkan eror


### /logout
![LOGOUT](https://github.com/user-attachments/assets/5ea2b047-1791-4c9d-abb6-422c27c9f8fc)

Proses
- Session dihapus dengan menggunakan session.clear ()
- User akan redirect ke halaman utama (/) atau ke index.html


### /students
![STUDENTS](https://github.com/user-attachments/assets/ec2f6c9a-6681-4f1c-8b6b-21fb0582976e)

Proses
- Mengecek apakah user sudah login (if 'user_id' not in session:)
- Jika belum akan redirect ke /login
- Jika sudah akan ditampilkan daftar mahasiswa


### /add
![ADD](https://github.com/user-attachments/assets/f3cc2c52-43f0-4393-9287-102e58046a50)

Proses
- Mengecek apakah user sudah login (if 'user_id' not in session:)
- Jika belum, akan redirect ke /login
- Jika sudah, akan mengambil data request (request.form) dan akan menyimpannya di database
- Akan redirect ke /students setelah berhasil data disimpan 


### /edit/<int:id>
![EDIT](https://github.com/user-attachments/assets/b8398f9b-6ea5-4410-95b8-de9478368736)

Proses
- Mengecek apakah user sudah login (if 'user_id' not in session:)
- Jika belum akan redirect ke /login
- Jika sudah akan menampilkan form edit
- Jika sudah berhasil edit akan redirect ke /students dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students


### /delete/<id>
![DELETE](https://github.com/user-attachments/assets/cc42aea3-ac84-47d0-8bdf-7f473f7f0b57)

Proses
- Mengecek apakah user sudah login (if 'user_id' not in session:)
- Jika belum akan redirect ke /login
- Jika sudah mahasiswa akan dihapus berdasarkan id
- Setelah berhasil hapus mahasiswa akan redirect ke /students dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students

