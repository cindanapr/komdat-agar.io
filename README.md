# Aplikasi Web "Agar.io"
<h1 align="center"><img src="https://github.com/mhdsuryono/komdat-agar.io/blob/master/agario.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:

## Sekilas Tentang
[`^ kembali ke atas ^`](#aplikasi-web-agario)

  **Agar.io** merupakan permainan aksi *online multiplayer* yang diciptakan oleh **Matheus Valadares**. Pemain mengendalikan sebuah sel di peta menggunakan *mouse* untuk menunjuk kearah yang diinginkan dan pemain bisa membagi diri dengan menggunakan spasi. Tujuan dari permainan ini adalah untuk mendapatkan massa sebanyak-banyaknya dengan menelan sel yang lebih kecil tanpa ditelan oleh sel yang lebih besar. Nama permainan ini berasal dari bahan agar-agar, digunakan untuk kultur bakteri. Permaian **Agar.io** menjadi salah satu permainan yang paling populer di *web* dan *mobile games* pada tahun pertama dirilis. Permainan ini diunduh versi *steam* pada 3 Mei 2015 dan versi *mobile* untuk *iOS* dan *Android* dirilis pada 8 April 2015 oleh *Miniclip*.

***

## Instalasi
[`^ kembali ke atas ^`](#aplikasi-web-agario)

#### Kebutuhan Sistem:
- Unix, Linux, atau Windows
- Ubuntu *server*
- Node.js dan NPM
- Socket.io
- Express.io
  
#### Proses Instalasi:

1. **Membuat VM Ubuntu Server**

    Dalam instalasi, digunakan *Ubuntu Server 16.04*. Kemudian, buat *Virtual Machine* baru pada *VirtualBox* dengan tipe "Ubuntu 64-bit".
    - Jalankan *VirtualBox* lalu klik *New*. Berikan nama bebas, tapi pastikan *version: Ubuntu (64-bit)*.
    
      ![1](https://github.com/mhdsuryono/komdat-agar.io/blob/master/1.png)
      
    - *Memory Size (RAM)* cukup 8 MB, lalu klik *Use an Existing VH* dan pilih file *ubuntu-server.vdi*. *(Ubuntu Server dapat didownload [disini](https://drive.google.com/a/apps.ipb.ac.id/uc?id=1-Dr_iEdk3N3YRFnTEtWdJQcV49Sp13IQ&export=download))*, klik *Create*.
    
      ![2](https://github.com/mhdsuryono/komdat-agar.io/blob/master/2.png)
      

2. **Setting Port-Forwarding**

    *Port-forwarding* berfungsi agar server dapat diakses dari luar melalui alamat host (IP host).
    - Klik *setting* pada ``Ubuntu Server``, klik *Network*, pilih *Advance*, lalu klik *Port Forwarding*.
    
      ![3](https://github.com/mhdsuryono/komdat-agar.io/blob/master/3.png)
      
    - Tambah *port* dan atur seperti tabel dibawah ini:
    
      | Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
      |:----:|:--------:|:-------:|:---------:|:--------:|:----------:|
      | http | TCP      |         | 8888      |          | 3000         |
      | ssh  | TCP      |         | 2222      |          | 20         |

    Dengan demikian, ketika mengakses ``localhost:8888`` di *host*, maka akan diteruskan ke ``localhost:80`` di *guest (VM)*.
    ![9](https://raw.githubusercontent.com/mhdsuryono/komdat-agar.io/master/8.png)

3. **Update Paket Sistem dan Install ssh**

    *Update* seluruh paket dalam sistem agar *up-to-date*. Serta, install ssh agar dapat diakses melalui terminal ubuntu.
    ```
    $ sudo apt update
    $ sudo apt install ssh
    ```
4. **Akses melalui Terminal Ubuntu**

    Pertama, matikan VM terlebih dahulu, lalu nyalakan server dengan mode **headless**. Buka terminal ubuntu dan koneksikan dengan virtual server melalui ssh.
    ```
    $ ssh student@localhost -p 2222
    ```

5. **Install Node.js dan NPM**

    ```
    $ sudo apt-get install nodejs
    $ sudo apt-get install npm
    ```

6. **Install Socket.io dan Express.io**

    Pada saat proses instalasi dibutuhkan ``--save`` agar pada sesi-sesi selanjutnya tidak perlu melakukan instalasi ulang.
    ```
    $ npm install socket.io --save
    $ npm install express.io --save
    ```

7. **Download Agar.io**

    Setelah di *download*, kita masuk kedalam direktori *agar.io-clone*.
    ```
    $ git clone https://github.com/huytd/agar.io-clone.git
    $ cd agar.io-clone
    ```

8. **Install Agar.io**

    Pastikan bahwa posisi saat ini berada didalam direktori ``agar.io-clone``.
    ```
    $ npm install
    ```
    
9. **Menguhubungkan folder Node dengan Nodejs**

    Pada Agar.io yang di*download*, saat di jalankan akan *request* kedalam  folder ``node``. Untuk saat ini, *node* sudah digantikan oleh ``nodejs`` dan penamaan foldernya pun menjadi ``nodejs``, jadi perlu dilakukan *link* antar folder.
    ```
    $ sudo ln -s /usr/bin/nodejs /usr/bin/node
    ```

10. **Menjalankan Agar.io**

    Posisi masih berada didalam direktori *agar.io-clone*.
    ```
    $ npm start
    ```

11. **Kendala Instalasi**

    Dimungkinkan terjadi kendala saat instalasi, seperti adanya proses yang ter-*lock* sehingga tidak bisa meng-*install* komponen yang dibutuhkan. Cara melepas *lock*-nya adalah:
    ```
    $ sudo rm /var/lib/apt/lists/lock
    $ sudo rm /var/cache/apt/archives/lock
    $ sudo rm /var/lib/dpkg/lock
    ```
    Jika terjadi kendala yang diakibatkan dari errornya dpkg, kita harus melakukan konfigurasi dengan perintah:
    ```
    $ sudo dpkg --configure -a
    ```
***

## Cara Pemakaian
[`^ kembali ke atas ^`](#aplikasi-web-agario)

<h1 align="center"><img src="https://raw.githubusercontent.com/mhdsuryono/komdat-agar.io/master/6.png"></h1>

Tujuan dalam permainan adalah untuk mendapatkan massa dan tumbuh lebih besar dengan mengkonsumsi partikel makanan (pentagons kecil) dan pemain lain. Pemain lain bergerak dengan berbagai ukuran. Anda hanya bisa mengonsumsi pemain lain yang lebih kecil dari Anda, dan pemain yang lebih besar akan mengkonsumsimu. Hati-hati dan bertahan selama mungkin!

**Game Basics**
- Pengguna memasukkan nama pengguna pada kolom *Nick* sebagai identitas bakteri pengguna. Nama pengguna tidak terikat aturan apapun (bebas).
- Pengguna menekan tombol *Play* dan memulai permainan.
- Untuk mengontrol sel bakteri, pengguna dapat menggerakkan *mouse* ke segala arah. Aturannya, pengguna cukup memakan sel-sel bakteri berukuran kecil yang ada disekitarnya dan menghindari sel bakteri berukuran besar agar tidak dimakan oleh sel bakteri besar tersebut sehingga pengguna dapat bertahan hidup.
- Sel bakteri dapat membelah diri dengan menekan tombol *space* pada *keyboard*.
- Permainan ini berakhir jika sel bakteri pengguna dimakan oleh sel bakteri berukuran besar dari pemain lawan.
- ``Objective``: Cobalah untuk menumbuhkan bakteri sebesar mungkin dengan memakan pemain yang lain.

![7](https://raw.githubusercontent.com/mhdsuryono/komdat-agar.io/master/7.png)

***

## Pembahasan
[`^ kembali ke atas ^`](#aplikasi-web-agario)

**Kelebihan:**
- Sederhana ketika memulai permainan. Pengguna cukup mengisi nama pengguna pada kolom *Nick* dan menekan tombol *Play*.
- Memiliki desain *interface* yang responsif, sehingga dapat dijalankan di perangkat apapun.
- Mudah dimengerti dan dimainkan oleh pengguna awam.
- Setting yang mudah dimengerti.

**Kekurangan:**
- *User Interface game* terlalu *simple*.
- Permainan hanya bisa dimainkan secara *local*.
- Proses *game* masih ada sedikit *lag* (untuk *browser* tertentu, disarankan menggunakan *Mozilla Firefox*).

***

## Referensi
[`^ kembali ke atas ^`](#aplikasi-web-agario)

- [Agar.io Clone](https://github.com/huytd/agar.io-clone) - ``Agar.io`` *Clone* untuk Instalasi
- [How to Play](https://github.com/huytd/agar.io-clone/wiki/How-to-Play) - Aturan Permainan ``Agar.io``


