# DataSintesa DevOps Technical Test

## General Knowledge Check

**1. What is your favorite Linux distro and why?**

Setiap distro memiliki kelebihannya masing-masing dan cocok untuk kebutuhan pengguna yang berbeda. dan distro favorit saya yaitu ubuntu karena Populer karena kemudahan penggunaannya, dukungan komunitas yang kuat, dan repositori perangkat lunak yang besar. Ideal untuk pemula.

**2. What do you know about Container and Virtual Machine?**

- Virtual Machine (VM)
  
Bayangkan sebuah komputer di dalam komputer. Itulah konsep dasar dari VM. Sebuah VM pada dasarnya adalah tiruan dari sistem komputer lengkap, termasuk sistem operasinya sendiri (misalnya, Windows, macOS, atau Linux), aplikasi, dan sumber daya virtual (CPU, RAM, penyimpanan). VM berjalan di atas perangkat keras fisik dan dikelola oleh sebuah perangkat lunak yang disebut hypervisor.

- Container

Berbeda dengan VM, container tidak meniru seluruh sistem komputer. Container hanya mengemas aplikasi dan semua dependensinya (pustaka, file konfigurasi, dll.) menjadi satu unit yang portabel dan ringan. Container berbagi kernel sistem operasi dari mesin host, sehingga lebih efisien dalam hal penggunaan sumber daya.

**3. How is Container different from Virtual Machine?**

Container:

- Virtualisasi pada tingkat sistem operasi.
- Membungkus aplikasi dan dependensinya ke dalam unit mandiri.
- Berbagi kernel host OS, ringan dan efisien.
- Ideal untuk portabilitas dan skalabilitas aplikasi.


Virtual Machine (VM):

- Virtualisasi pada tingkat hardware.
- Mengemulasikan keseluruhan sistem komputer.
- Memiliki sumber daya terdedikasi dan terisolasi.
- Ideal untuk isolasi penuh dan menjalankan berbagai sistem operasi.

**4. How can you sync two local directories in Linux?**

Di Linux, Anda dapat menyinkronkan dua direktori lokal menggunakan ```rsync```. Rsync menyalin perbedaan antara direktori, menghemat waktu dan bandwidth.

1. Perintah Dasar:

```
rsync [opsi] sumber tujuan
```

2. opsi umum:
- ```-r```: Menyalin secara rekursif.
- ```-a```: Mempertahankan izin, kepemilikan, dll.
- ```-v```: Menampilkan informasi proses.
- ```-z```: Kompresi.
- ```--delete```: Menghapus file di tujuan yang tidak ada di sumber.

3. contoh :
```
rsync -avz --delete /path/ke/direktori1 /path/ke/direktori2
```

**5. What is swap in Linux and what is it used for?**

Swap pada Linux adalah ruang pada hard disk (HDD atau SSD) yang digunakan sebagai perpanjangan dari RAM fisik. Swap menyediakan memori virtual yang membantu menjaga kestabilan dan kinerja sistem.

Kegunaan Swap:

- Mengatasi RAM Penuh: Ketika RAM fisik penuh, swap memungkinkan sistem untuk memindahkan sementara halaman memori yang tidak aktif atau jarang digunakan dari RAM ke area yang ditentukan pada hard disk.
- Hibernasi: Swap juga digunakan dalam proses hibernasi (suspend-to-disk), di mana seluruh isi RAM disimpan ke swap sebelum komputer dimatikan.


**6. You have to find all files larger than 20 MB in your Linux OS. How you do it?**

Berikut adalah cara untuk menemukan berkas-berkas tersebut:

```
find / -type f -size +20M -exec ls -lh {} \;
```
Penjelasan:

- ```/```: Mencari di seluruh sistem berkas (mulai dari direktori root). Anda bisa mengganti ini dengan jalur direktori spesifik jika ingin membatasi pencarian.
- ```-type f```: Mencari hanya berkas (bukan direktori).
- ```-size +20M```: Mencari berkas yang lebih besar dari 20 MB.
- ```-exec ls -lh {} \;```: Menjalankan perintah ls -lh untuk setiap berkas yang ditemukan, menampilkan informasi detailnya.



**7. What is happening when the Linux kernel is starting the OOM killer and how does it
choose which process to kill first?**

Ketika sistem Linux mengalami kekurangan memori kritis, kernel akan mengaktifkan "OOM killer". OOM killer ini akan menghentikan satu atau beberapa proses untuk mengosongkan memori dan mencegah sistem crash.

OOM killer memilih proses berdasarkan "badness score". Nilai ini dipengaruhi oleh penggunaan memori, waktu eksekusi, prioritas, dan status root proses. Proses dengan nilai badness tertinggi akan dihentikan.


**8. Explain the following command : ```(date ; ps -ef | awk '{print $1}'| sort |
uniq | wc -l) >> Activity.log```**

Penjelasan:

Perintah ini menjalankan serangkaian tindakan, yang hasilnya akan dicatat dalam file bernama "Activity.log".

- ```date```: Menampilkan tanggal dan waktu saat ini. Output ini akan menjadi bagian pertama dari catatan di dalam file log.
- ```ps -ef```: Menampilkan semua proses yang sedang berjalan di sistem, termasuk detail seperti ID pengguna, ID proses, dan perintah yang menjalankan proses tersebut.
- ```awk '{print $1}'```: Memfilter output dari ps -ef. Bagian ini akan mengambil kolom pertama dari setiap baris output ps -ef, yang merupakan ID pengguna yang menjalankan proses.
- ```sort```: Mengurutkan ID pengguna yang dihasilkan secara alfabetis atau numerik.
- ```uniq```: Menghilangkan ID pengguna yang duplikat, sehingga hanya menyisakan satu kemunculan dari setiap ID pengguna.
- ```wc -l```: Menghitung jumlah baris yang tersisa, yang menunjukkan jumlah pengguna unik yang menjalankan proses pada saat itu.
- ```( ... ) >> Activity.log```: Mengelompokkan semua perintah sebelumnya dalam satu unit, kemudian mengarahkan output gabungan dari perintah-perintah tersebut ke file "Activity.log". Tanda >> berarti output akan ditambahkan di akhir file log, sehingga catatan aktivitas sebelumnya tidak akan ditimpa.

Contoh Output di Activity.log:
```
Sel 02 Jul 2024 17:43:25 WITA
5
```

Perintah ini pada dasarnya mencatat tanggal, waktu, dan jumlah pengguna unik yang sedang menjalankan proses di sistem Anda ke dalam file "Activity.log".

**9. Server A cannot talk to Server B. Describe possible reasons!**

Server A tidak dapat berkomunikasi dengan Server B karena beberapa kemungkinan:

Jaringan:
- Kabel atau port rusak
- Alamat IP salah atau subnet berbeda
- Firewall memblokir lalu lintas
- Rute jaringan tidak benar
- Masalah pada switch atau router

Perangkat Lunak:
- Layanan jaringan tidak berjalan
- Konfigurasi layanan salah
- Konflik perangkat lunak

**10. How to know which process in Linux listens on a specific port?**

disini saya menggunakan perintah ```ss``` untuk mencari tahu proses yang menggunakan port tertentu:

- Semua port TCP: ```ss -ltn```
- Port tertentu (misal, port 80): ```ss -ltn '( sport = :80 )'```

**11. An engineer type http://www.yahoo.com in the browser and he/she presses enter.
What happens next? (hint: describe activities happening at every OSI layer - physical,
data link, network, transport, session, presentation, application layer)**

- Lapisan Fisik: Frame Ethernet diubah menjadi sinyal listrik/cahaya yang dikirim melalui kabel.
- Lapisan Data Link: Paket-paket IP diubah menjadi frame Ethernet dengan alamat MAC.
- Lapisan Jaringan (IP): Menambahkan alamat IP tujuan (Yahoo) dan sumber (komputer Anda) ke setiap paket.
- Lapisan Transportasi (TCP): Membagi permintaan menjadi paket-paket data kecil dan memastikan semuanya sampai dengan benar.
- Lapisan Sesi: Mengelola sesi komunikasi antara peramban dan server Yahoo.
- Lapisan Presentasi: Jika HTTPS, data permintaan dienkripsi untuk keamanan.
- Lapisan Aplikasi: Peramban menerima "http://www.yahoo.com", menentukan protokol (HTTP/HTTPS), dan membuat permintaan untuk situs tersebut.

**12. What about if the engineer change from http://www.yahoo.com into
https://www.yahoo.com ? (hint : describe activities related to public/private
certificates, CAs, proxying, MiTM, etc)**

Perubahan dari HTTP ke HTTPS pada www.yahoo.com berdampak signifikan pada keamanan. Ketika beralih ke HTTPS, browser pengguna akan meminta sertifikat digital dari situs web Yahoo. Sertifikat ini, yang dikeluarkan oleh Otoritas Sertifikat (CA) terpercaya, bertindak sebagai tanda pengenal digital Yahoo dan memastikan keaslian situs web.

Sertifikat tersebut berisi kunci publik yang digunakan untuk memulai proses enkripsi, mengamankan data yang dikirim antara browser pengguna dan server Google. Hanya server Google yang memiliki kunci privat yang cocok untuk mendekripsi data tersebut, sehingga melindungi data dari serangan Man-in-the-Middle (MiTM). HTTPS juga memastikan integritas data, artinya data yang diterima adalah data asli yang dikirim.

**13. A web developer is creating a new web application and you have to store the user’s
passwords in a database. How would you store the passwords securely?**

berikut cara untuk menyimpan password pengguna dengan aman di dalam database
- Jangan Simpan Password dalam Teks Biasa (Plain Text):
Menyimpan password dalam teks biasa sangat tidak aman. Jika database diretas, semua password pengguna akan terbuka.
- Gunakan Hashing:
Hashing adalah proses mengubah password menjadi string unik yang tidak bisa dikembalikan ke bentuk aslinya. Gunakan algoritma hashing yang kuat seperti bcrypt, Argon2, atau scrypt.
- Tambahkan Salt:
Salt adalah data acak yang ditambahkan ke password sebelum di-hash. Ini bertujuan untuk memastikan bahwa password yang sama tidak menghasilkan hash yang sama.
- Gunakan Iterasi yang Cukup:
Algoritma hashing modern seperti bcrypt, Argon2, dan scrypt memungkinkan penambahan jumlah iterasi untuk meningkatkan keamanan.
- Pembaruan dan Pengelolaan:
Secara berkala, periksa dan perbarui metode hashing yang digunakan. Algoritma yang aman hari ini mungkin tidak aman di masa depan, jadi penting untuk tetap mengikuti perkembangan terbaru dalam keamanan kriptografi.
- Keamanan Server:
Selain mengamankan password, pastikan server dan aplikasi web memiliki keamanan yang baik. Gunakan HTTPS untuk enkripsi data dalam perjalanan, perbarui perangkat lunak secara berkala, dan terapkan kebijakan keamanan yang ketat.

**14. A DevOps engineer have added a public ssh key of a developer into**
authorized_keys but the developer is still getting a password prompt, what can be
wrong?

Kemungkinan Masalah:

- Izin File yang Salah: File "authorized_keys" atau direktori ".ssh" mungkin memiliki izin yang terlalu terbuka.
- Konfigurasi SSH Server: Opsi ```PubkeyAuthentication``` dan ```AuthorizedKeysFile``` mungkin tidak diaktifkan dalam konfigurasi SSH server.
- Penggunaan Kunci yang Salah: Pengembang mungkin menggunakan kunci privat yang tidak sesuai.
- Masalah pada Kunci SSH: Kunci SSH mungkin rusak atau tidak valid.
- Masalah Jaringan: Firewall atau masalah konektivitas lainnya mungkin mengganggu proses otentikasi.
- Otentikasi Multi-Faktor: Server mungkin memerlukan otentikasi tambahan selain kunci SSH.

**15. Describe the Linux boot process with as much detail as possible, starting from when
the system is powered on and ending when you get a prompt!**

berikut proses boot Linux secara detail, dimulai dari saat komputer dinyalakan hingga muncul prompt:

1. Power On Self Test (POST):

Saat tombol power ditekan, BIOS (Basic Input/Output System) atau UEFI (Unified Extensible Firmware Interface) melakukan POST untuk memeriksa hardware dasar (RAM, CPU, penyimpanan) dan memastikannya berfungsi.

2. Boot Loader:

Setelah POST berhasil, BIOS/UEFI mencari bootloader. Biasanya, bootloader yang umum digunakan adalah GRUB (Grand Unified Bootloader). GRUB menampilkan menu yang memungkinkan pengguna memilih sistem operasi mana yang akan di-boot (jika ada beberapa sistem operasi yang terpasang) atau langsung memulai Linux jika hanya satu yang ada.

3. Kernel Loading:

Ketika opsi Linux dipilih, bootloader memuat kernel Linux (inti dari sistem operasi) dari hard drive atau media penyimpanan lain ke dalam memori (RAM).

4. Kernel Decompression and Initialization:

Setelah dimuat ke memori, kernel Linux mendekompresi dirinya sendiri (karena biasanya dikompres untuk menghemat ruang) dan memulai proses inisialisasi. Ini termasuk pengaturan hardware dasar, memori virtual, inisialisasi perangkat keras yang penting (misalnya, keyboard, mouse), dan memuat driver perangkat keras dasar.

5. initramfs (optional):

Beberapa distribusi Linux menggunakan initramfs (initial RAM filesystem), yaitu sistem file sementara yang dimuat ke RAM untuk membantu inisialisasi perangkat keras yang lebih kompleks sebelum sistem file root sebenarnya dimuat.

6. Root Filesystem Mounting:

Kernel kemudian memasang (mount) root filesystem (biasanya /) dari hard drive atau media penyimpanan lainnya. Sistem file ini berisi semua file dan direktori yang diperlukan untuk sistem operasi berfungsi.

7. System Initialization (init):

Proses init (biasanya systemd pada distribusi Linux modern) dimulai. Proses ini adalah "induk" dari semua proses lain dalam sistem dan bertanggung jawab untuk memulai layanan-layanan penting (daemon) yang dibutuhkan untuk operasi sistem, seperti jaringan, tampilan grafis, login, dan sebagainya.

8. Runlevel/Target Execution:

Systemd menjalankan "target" tertentu (setara dengan runlevel pada sistem init lama). Target ini menentukan layanan mana yang akan dimulai dan dalam mode apa sistem akan berjalan. Misalnya, target "graphical.target" memulai lingkungan desktop grafis.

9. Login Prompt:

Setelah semua layanan yang diperlukan dimulai, Anda akan disajikan dengan layar login di mana Anda dapat memasukkan nama pengguna dan kata sandi untuk mengakses sistem.

10. Shell Prompt:

Setelah login berhasil, Anda akan mendapatkan shell prompt (biasanya $ atau #), menandakan Anda siap untuk berinteraksi dengan sistem dan menjalankan perintah.

