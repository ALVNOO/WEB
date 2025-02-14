# WEB

##ANALISA

###Analisis Routing dan Navigasi

/ =  Menampilkan halaman utama (index.html)
/login = Halaman login dan proses autentikasi
/logout	= Logout dan hapus sesi
/students	= Menampilkan daftar mahasiswa (student.html)
/add	= Menambahkan mahasiswa baru
/delete/<int:id> = Menghapus mahasiswa berdasarkan ID
/edit/<int:id>	= Mengedit informasi mahasiswa
/users/create	= Membuat akun baru

### Routing, Redirecting

/Login

Proses
- User mengisi username dan password
- Jika cocok dengan database akan redirect ke /students (tampilan daftar mahasiswa) dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students
- Jika gagal tetap di /login dan menampilkan eror


/Logout

Proses
- Session dihapus dengan menggunakan session.clear ()
- User akan redirect ke halaman utama (/) atau ke index.html


/students

Proses
- Mengecek apakah user sudah login
- Jika belum akan redirect ke /Login
- Jika sudah akan ditampilkan daftar mahasiswa


/add
Proses
- Mengecek apakah user sudah login
- Jika belum, akan redirect ke /Login
- Jika sudah, akan mengambil data request dan akan menyimpannya di database
- Akan redirect ke /students setelah data disimpan 


/edit/<int:id>

Proses
- Mengecek apakah user sudah login
- Jika belum akan redirect ke /Login
- Jika sudah akan menampilkan form edit
- Jika sudah berhasil edit akan redirect ke /students dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students


/delete/<id>

Proses
- Mengecek apakah user sudah login
- Jika belum akan redirect ke /Login
- Jika sudah mahasiswa akan dihapus berdasarkan id
- Setelah berhasil hapus mahasiswa akan redirect ke /students dengan redirect(url_for('student')) yang dimana student adalah fungsi yang ada di dalam route /students

