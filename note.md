Pengaksesan database menjadi salah satu fitur terpenting dari setiap web application. Dan
konsep MVC sendiri sudah mengakomodasi komponen bernama Model untuk memprosesnya.
Laravel menyediakan cukup banyak fitur pengelolaan database seperti migration, DB facade,
query builder, serta eloquent.

untuk

1. Pengaturan Database Laravel
hal pertama yang kita lakukan adalah mengatur .env biasa nya kalo kita melakukan clone dari github atau membuat projek baru dikarenakan kita butuh tempat untuk menyimpan data nya. Untuk aplikasi web berbasis PHP, yang paling
sering dipakai adalah MySQL/MariaDB, SQLite, PostgreSQL serta SQL Server.
Keempat jenis database ini sudah didukung Laravel secara bawaan. 

di dalam file .env kita akan menemukan ini. yng di ubah hanyalah bagian DB_database dengan nama database yang kita berikan.
 DB_HOST: Dipakai untuk mengatur alamat server database. Secara bawaan sudah
berisi 127.0.0.1, yakni alamat localhost.
 DB_PORT: Dipakai untuk mengatur port dari aplikasi server database. Secara bawaan
berisi angka 3306, yakni port default bawaan MySQL.
 DB_DATABASE: Nama database yang akan dipakai. Secara bawaan sudah berisi
'laravel', yang artinya Laravel akan langsung mencari sebuah database bernama
'laravel'.
 DB_USERNAME dan DB_PASSWORD: Dipakai untuk membuat nama user dan
password login ke database server. Secara bawaan nama user adalah root, dan
password tidak diisi.

2. . Pengertian Migration
migration ini digunakan untuk mengerate tabel yang kita buat dan nanti nya kita tidak perlu melakukan nya manual karna sudah kita buat struktur tabel nya seperti apa yang kita inginkan atau hasil dari desain data kita. dan perlu di ketahui laravel itu sudah mempunyai file data bawaan nya sendiri. nah perlu di ingat setiap 1 file migration itu memilki 1 tabel saja. jadi nya jika kita memiliki banyak tabel berarti banyak pula migration yang kita punya.


perintah untuk melakukan migration adalah
php artisan migrate. 
kenapa sih ini perlu dilakukan? dikarenakan kita akan mengisi tabel yang ada di database yang sudah kita buat di mysql

3. Membuat Migration
sebelum nya kita sudah tau tujuan dari migration ini apa dan sekarang bagaimana sih caranya membuat migration ini dan perintah nya apa hehe.

    1. php artisan make:migration <nama_migration> --create=<nama_tabel>
    contoh nya : php artisan make:migration create_mahasiswas_table --create=mahasiswas
    atau bisa hanya mengetikan seperti ini
    hp artisan make:migration create_mahasiswas_table 

    nanti nya akan di buatkan nama file nya sama namun yang membedakan hanya tanggal dan waktu pembuatan nya. dikarenakan time nya berbeda dan perlu di ingat di tambahkan s di belakang kata nya 
Tambahan flag --create=mahasiswas boleh saja tidak ditulis dan Laravel akan membuat
tabel berdasarkan nama file. Misal jika dijalankan php artisan make:migration create_
dosens_table, maka Laravel akan men-generate nama tabel dosens.
Penamaan tabel dengan akhiran 's' ini sudah kita bahas sebelumnya, yakni untuk
mengikuti aturan Laravel dimana nama tabel sebaiknya dibuat plural.
Ini bukan kewajiban karena Laravel tetap mengizinkan kita membuat nama tabel dengan
kata biasa, namun nanti perlu sedikit konfigurasi jika ingin menggunakan fitur Eloquent.
Agar lebih mudah dan terbiasa dengan penamaan umum di aplikasi Laravel, saya akan
buat semua nama tabel dengan akhiran 's', seperti mahasiswas, gurus, barangs, dst.
Alternatif lain yang juga banyak di pilih programmer indonesia adalah memakai kata
bahasa inggris seperti students, teachers, items, dst.


nah setelah membuat 
isi tabel nya kita langsung melakukan migration ke database nya langsung dengan printah php artisan migrate
nah perlu di inget nama file tabel nya tidak boleh sama ya.
 

 ada beberapa printah migration yang perlu kita ketahui 
     1. Migration Rollback
     melakukan migration seperti sebelum nya dikarenakan ada kesalahan atau penambahan dalam membuat tabel kita bisa melakukan perintah seperti ini
     php artisan migrate:rollback

     nah terkadang kita ingin mengembalikan satu tabel saja kita bisa menggunakan php artisan migrate:rollback --step=1
     sebelum melakukan ini liat dulu nih step yg berapa kita ingin  rollback
    dengan printah  php artisan migrate:status. nanti nya akan muncul status nya yg ke berapa tinggal kita pilih saja mana yang ingin kita rollback



     2. migration reset
     ini digunakan jika kita tidak sengaja melakukn drop table atau hapus tabel yang ada di database printah nya
     php artisan migrate:reset

     3. migration fresh
     migration ini adalah gabungan dari php artisan migrate dan artisan migrate:reset dia akan memperbarui semua nya kembali. 

nah sekarang kita coba isi 
tabel migration yang sudah kita buat tadi

$table->string('nama');
$table->string('tempat_lahir');
$table->date('tanggal_lahir');
$table->string('fakultas');
$table->string('jurusan');
$table->decimal('ipk',3,2);

table yang kita buat ini dar nama sampai jurusan kita membuat tipe data nya string / varchar
dan tgl lahir bertipe tanggal dan ipk bertipe decimal

selanjut nya kita melakukan migartion. eit perlu di ingat karna sebelum nya kita sudah melakukan migration nah sekarang biar sukses kita menggunakan migrate reset , rollback, ataupun refresh/fresh 

4. migration alter table 
migration ini di gunakan jika ingin melakukan edit table ataupub penambahan
nah disini kita membutuhkan sebuah library 
bernama Doctrine DBAL nama nya ngeri juga ya........
perintah untuk memasang nya composer require doctrine/dbal

setelah sukses kita membuat file untuk al
ter table yang ingin kita ubah atau tambahkan dengan perintah  php artisan make:migration alter_mahasiswas_table --table=mahasiswas

nah setelah sukses kita bisa melihat di file up and down

Di dalam method up() saya membuat 3 buah perintah modifikasi:
 Method $table->renameColumn('nama','nama_lengkap') dipakai untuk mengubah
nama kolom 'nama' menjadi 'nama_lengkap'.
 Method $table->text('alamat')->after('tanggal_lahir') dipakai untuk menambah
kolom 'alamat' dengan tipe data TEXT, yang posisinya ditempatkan setelah kolom
'tanggal_lahir'.
 Method $table->dropColumn('ipk') dipakai untuk menghapus kolom 'ipk'.
Ketiga perubahan di method up() ini harus kita balik di method down():
 Method $table->renameColumn('nama_lengkap','nama') dipakai untuk mengubah
kembali nama kolom dari 'nama_lengkap' menjadi 'nama'.
335
Migration
 Method $table->dropColumn('alamat') dipakai untuk menghapus kolom 'alamat'.
 Method $table->decimal('ipk',3,2)->default(1.00) dipakai untuk membuat kembali
kolom 'ipk' dengan tipe data DECIMAL(3,2) dan nilai default 1.00.
Kode program di dalam method up() dan down() harus berpasangan agar proses rollback bisa
berlangsung dengan baik.

dan selanjut nya kita melakukan migrate
php artisan migrate dan tara sukses
note nya harus di tentukaan ya dan di down nya harus di bali.
