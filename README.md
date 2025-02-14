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


![FLASK](https://github.com/user-attachments/assets/0d13c742-a4e6-4533-b5ec-99a3eda43a67)

- Membuat objek Flask
- secret_key → Digunakan untuk session
- Konfigurasi database SQLite (students.db)
- Inisialisasi SQLAlchemy (db)
- Inisialisasi HTTP Authentication (auth)

---

## Model

### Model User
![USER MODEL AUTH](https://github.com/user-attachments/assets/7ad63ca1-8b5d-489e-9690-8dc9e952423c)

Penjelasan:
- Membuat model User
- set_password() =  Mengubah password menjadi hash
- check_password() =  Memverifikasi password
- __repr__ =  Untuk debugging


### Model Student
![STUDENT DB](https://github.com/user-attachments/assets/1024035d-be69-4d7a-80cb-4b4662b212f3)

Model ini menyimpan data siswa seperti nama, umur, dan kelas

---

## Authentication
![USER AUTH](https://github.com/user-attachments/assets/e0c0d78b-e0ae-4691-a698-68f325605dce)

Penjelasan : 
- Autentikasi berbasis HTTP
- Mengecek apakah username & password cocok di database

---

## Routing and Redirecting

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


---

## USE CASE DIAGRAM
![USE CASE DIAGRAM drawio](https://github.com/user-attachments/assets/eaac02e4-f360-4c0f-8972-4465336525d6)

Admin/User berinteraksi dengan sistem dalam tiga skenario utama:
- Login/Logout :
  - dapat masuk ke dalam sistem dengan memasukkan username dan password
  - bisa logout untuk keluar dari sistem
- Create Account:
  - Admin/User dapat membuat akun baru dalam sistem
- CRUD Mahasiswa :
  - Admin/User yang sudah login dapat menambah, mengedit, menghapus, dan melihat data mahasiswa dalam sistem

---


## CLASS DIAGRAM
![CLASS DIAGRAM drawio](https://github.com/user-attachments/assets/46880e5a-4382-43a7-af72-9a98e18ab796)

- Class Student (Mahasiswa) : Data mahasiswa yang dikelola dalam sistem
- Class User : Pengguna yang dapat login ke dalam sistem
- Class FlaskApp : aplikasi utama berbasis Flask yang menangani request pengguna
- Class Database (SQLAlchemy) : database yang menyimpan data mahasiswa dan user

Hubungan antar class:

- Student dengan FlaskApp (Asosiasi) : FlaskApp mengelola data mahasiswa dengan menyediakan fitur CRUD
- FlaskApp dengan User (Dependency) : FlaskApp menangani login/logout dan memverifikasi autentikasi user
- FlaskApp dengan Database (SQLAlchemy) (Dependency) : FlaskApp berinteraksi dengan database untuk menyimpan dan mengambil data user serta mahasiswa
- Student & User dengan Database (SQLAlchemy) (Agregasi) : Database menyimpan informasi mahasiswa dan user, dan dapat diakses melalui FlaskApp


---


## SEQUENCE DIAGRAM
![sequence diagram drawio](https://github.com/user-attachments/assets/e790e400-68d5-4e6c-b0b7-afd2f05cdded)


Registrasi User (/user/create)

- User/Admin mengakses /user/create → FlaskApp menampilkan form registrasi
- User mengisi form → Data dikirim ke FlaskApp
- FlaskApp mengecek username ke Database melalui Controller
- Jika username belum ada, FlaskApp membuat user baru di Database
- Database mengonfirmasi bahwa user berhasil dibuat
- FlaskApp menampilkan notifikasi sukses dan redirect ke halaman utama /index


Login User (/login)

- User memasukkan kredensial login → FlaskApp memproses permintaan
- FlaskApp meminta validasi kredensial ke Controller
- Controller mengambil data user dari Database
- Jika kredensial valid, status autentikasi dikembalikan
- User diarahkan ke halaman /students setelah login berhasil


Logout User (/logout)

- User melakukan logout → FlaskApp memproses permintaan
- Controller menghapus sesi user dari sistem
- Setelah logout berhasil, user diarahkan ke halaman login (/login)


Menampilkan Daftar Mahasiswa (GET /students)

- User mengakses /students → FlaskApp meminta daftar mahasiswa dari Controller
- Controller mengambil data mahasiswa dari Database
- Database mengembalikan daftar mahasiswa ke Controller
- Controller meneruskan data ke FlaskApp
- FlaskApp menampilkan daftar mahasiswa ke user


Menambahkan Mahasiswa (POST /students)

- User mengirimkan data mahasiswa baru ke FlaskApp
- FlaskApp meneruskan data ke Controller
- Controller menyimpan data ke Database
- Database mengonfirmasi penyimpanan data
- FlaskApp mengembalikan respons sukses ke user


Mengedit Mahasiswa (PUT /students/{id})
- User mengirim permintaan untuk mengedit mahasiswa tertentu
- FlaskApp meneruskan data ke Controller
- Controller mengupdate data mahasiswa di Database
- Database mengonfirmasi update
- FlaskApp mengembalikan hasil ke user dan melakukan redirect ke /students


Menghapus Mahasiswa (DELETE /students/{id})

- User mengirim permintaan untuk menghapus mahasiswa tertentu
- FlaskApp meneruskan permintaan ke Controller
- Controller menghapus data mahasiswa dari Database
- Database mengonfirmasi bahwa data telah dihapus
- FlaskApp mengembalikan hasil ke user dan melakukan redirect ke /students
