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


**8. Explain the following command : (date ; ps -ef | awk '{print $1}'| sort |
uniq | wc -l) >> Activity.log**



9. Server A cannot talk to Server B. Describe possible reasons!
10. How to know which process in Linux listens on a specific port?
11. An engineer type http://www.yahoo.com in the browser and he/she presses enter.
What happens next? (hint: describe activities happening at every OSI layer - physical,
data link, network, transport, session, presentation, application layer)
12. What about if the engineer change from http://www.yahoo.com into
https://www.yahoo.com ? (hint : describe activities related to public/private
certificates, CAs, proxying, MiTM, etc)
13. A web developer is creating a new web application and you have to store the user’s
passwords in a database. How would you store the passwords securely?
14. A DevOps engineer have added a public ssh key of a developer into
authorized_keys but the developer is still getting a password prompt, what can be
wrong?
15. Describe the Linux boot process with as much detail as possible, starting from when
the system is powered on and ending when you get a prompt!
