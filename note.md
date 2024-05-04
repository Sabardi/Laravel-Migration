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
