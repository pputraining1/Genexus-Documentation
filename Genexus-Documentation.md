# Getting Started

Dokumentasi ini menjelaskan dalam scope pada platform GeneXus 18, yang dokumentasi ini berfokus pada sisi front-end  seperti pengelolaan tampilan, interaksi, serta pengalaman pengguna.

Introduction
---
Pastikan anda sudah menginstall Genexus jika belum bisa lihat tutorial ini:
- [GeneXus 18 hardware and software requirements](https://docs.genexus.com/en/wiki?30900,GeneXus+18+hardware+and+software+requirements)
- [How to Install Genexus](https://hackmd.io/@9Jiq9WM9SIWJsYjajf9rHQ/rywchiAcex#Cara-Instal-Genexus)
- [Genexus Docs Search Engine](https://docs.genexus.com/en/hsearch)



Terminology
---
| Object               | Description                                                                 | When to use                                                                 |
|-----------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| API                  | Object untuk expose/mengonsumsi service (REST/SOAP).                        | Dipakai saat butuh integrasi dengan aplikasi lain.                          |
| Transaction          | Mendefinisikan tabel database, atribut, relasi, dan CRUD otomatis.          | Digunakan untuk membuat struktur data + ABM (Add, Browse, Modify).          |
| Data Provider        | Object untuk load, transformasi, dan return data dalam bentuk koleksi/struktur.| Dibutuhkan untuk menyiapkan data ke UI atau API.                             |
| Data Selector        | Object untuk Query reusable dengan filter tertentu.                        | Digunakan saat sering butuh query dengan kondisi spesifik.                  |
| Data View            | Object untuk mendefinisi view/tabel eksternal di database.                  | Dipakai kalau database sudah ada (legacy DB).                               |
| Domain               | Object untuk mendefinisikan tipe data dengan aturan khusus.                 | Digunakan untuk atribut/variabel agar konsisten validasinya (contoh: Email, Phone). |
| Procedure            | Object logic untuk implementasi algoritma terpisah yang bisa dipanggil.    | Digunakan untuk proses bisnis.                                              |
| Structured Data Type (SDT) | Object untuk mendefinisikan struktur data kompleks (mirip class).          | Digunakan untuk kirim/terima data di API.                                   |
| Subtype Group        | Object untuk mengelompokkan atribut dengan arti sama.                      | Digunakan agar bisa reuse rules & logika.                                   |
| Design System        | Object untuk berisi kumpulan style, layout, dan behavior standar.           | Digunakan untuk menjaga konsistensi UI di semua panel.                      |
| Master Panel         | Object template utama aplikasi web/mobile (misalnya: header, footer, menu).| Digunakan sebagai kerangka untuk layar lain.                                |
| Menu                 | Object untuk definisi navigasi/menu app.                                    | Digunakan untuk membuat daftar navigasi otomatis.                           |
| Panel                | Object untuk layar kustom, bebas desain & logic.                           | Digunakan untuk UI yang tidak otomatis dibuat oleh Transaction.             |
| Stencil              | Object template visual untuk mempercepat desain.                           | Digunakan saat butuh tampilan seragam (list, card, form).                   |
| Theme                | Kumpulan style visual (warna, font, ukuran).                               | Dipakai untuk branding aplikasi.                                            |
| URL Rewrite          | Aturan custom URL agar lebih ramah.                                         | Digunakan untuk SEO dan user friendly URL.                                  |
| User Control         | Object untuk komponen UI custom (misal calendar, map).                     | Digunakan saat kontrol bawaan GeneXus tidak cukup, kode dibuat manual.      |
| Web Component        | Object untuk membuat reusable component di banyak panel.                   | Digunakan untuk widget/partial screen.                                      |
| Web Master Panel     | Object template utama aplikasi web (khusus web).                           | Digunakan untuk konsistensi layout antar halaman web.                       |
| Web Panel            | Object layar web custom (tidak auto-generated).                            | Dipakai untuk form, laporan, dashboard, dll.                                |
| Web Theme            | Object tema khusus web (warna, CSS, style).                                | Digunakan untuk kustomisasi tampilan web app.                               |


| Feature        | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| Build<Panel>   | Generate dan Deploy App hanya panel tertentu.                               |
| BuildAll       | Generate dan Deploy App untuk yang ada perubahan saja.                      |
| Rebuild<Panel> | Generate ulang dan Deploy App hanya panel tertentu saja.                    |
| RebuildAll     | Generate ulang dan Deploy App seluruh Root Module dan dependencies.         |
| Attribute      | Sebuah field dari database / Transaction.                                   |
| Variable       | Sebuah field kosong untuk menampung data.                                   |
| Domain         | Sebuah template tipe data atau definisi tipe data kustom yang bisa dipakai ulang di seluruh aplikasi. |
| JSON Import    | Import JSON ke dalam GeneXus menjadi Structured Data Type (SDT) secara otomatis. |


Folder Structure
---
Dalam praktik terbaik GeneXus, meskipun platform ini tidak mewajibkan struktur folder khusus untuk front-end atau back-end, penerapan standarisasi internal tetap penting untuk memudahkan kolaborasi tim, mencakup penamaan objek, pengelompokan modul, serta pengelolaan sumber daya, sehingga meminimalkan konflik kode, mempercepat pengembangan, dan mendukung pemeliharaan serta dokumentasi proyek secara konsisten.

Berikut adalah Struktur folder Frontend 

![image](https://hackmd.io/_uploads/rJFvdM-jee.png)
```
GenexusDocumentation =>App Name
└── Root Module
    ├── General
    │   ├── UI
    │   │   └── GlobalEvents
    │   ├── **GlobalDataProvider => Folder kumpulan data relasi**
    │   │   └── DP_UserRelation
    │   ├── **GlobalSDT => Folder kumpulan struktur**
    │   │   └── SDT_User
    │   ├── **Interfaces => Folder kumpulan screen**
    │   │   └── Home
    │   ├── **Services => Folder kumpulan logic interfacing**
    │   │   ├── Proc_Users
    │   │   └── Proc_UserById
    │   ├── **Styles => Folder kumpulan style css**
    │   │   ├── GlobalStyles
    │   │   └── Images
    │   └── **UserControl => Folder kumpulan custom widget / Javascript**
    │       └── UC_Toast
```

    
Berikut adalah Struktur folder Backend

![image](https://hackmd.io/_uploads/rykMSfbogg.png)
```
GeneXusDocumentation => App name
└── Root Module
    ├── General
    ├── KnowledgeBase1 => Module Global Styling dan CSS
    ├── Transaction => Folder kumpulan object Transaction
    ├── SDT => Folder kumpulan SDT (Structured Data Type)
    ├── DataProvider => Folder kumpulan object untuk mengambil dan menyusun data
    ├── Procedure => Folder kumpulan logika atau proses bisnis
    └── API => Folder kumpulan object untuk expose service (REST API)
```
    
Component User Interface (UI)
---
Untuk Component UI pada Genexus secara default berada di pojok kanan yang bernama **Toolbox**
    
![image](https://hackmd.io/_uploads/H1MUazWoll.png)
    
- #### Attribute/Variable  
  Komponen untuk menampilkan atau menerima data dari atribut database atau variabel lokal.  

- #### Button  
  Tombol interaktif untuk mengeksekusi event atau aksi tertentu.  

- #### Embedded Page  
  Menyisipkan halaman web lain di dalam layar saat ini.  

- #### Error Viewer  
  Menampilkan pesan error atau validasi input data pengguna.  

- #### Horizontal Rule  
  Garis horizontal untuk memisahkan konten secara visual.  

- #### Hyperlink  
  Tautan yang mengarahkan pengguna ke halaman lain atau URL tertentu.  

- #### Image  
  Menyisipkan dan menampilkan gambar statis atau dinamis.  

- #### TextBlock  
  Menampilkan teks statis yang tidak terkait langsung dengan atribut/variabel.  

- #### User Control  
  Komponen kustom yang bisa digunakan ulang, dibuat oleh developer.  

- #### Web Component  
  Bagian layar independen yang dapat digunakan di dalam layar lain (seperti widget).  

- #### Canvas  
  Area bebas untuk menggambar atau menempatkan elemen visual secara fleksibel.  

- #### Flex  
  Kontainer berbasis *flexbox* untuk mengatur tata letak elemen secara responsif.  

- #### Free Style Grid  
  Grid fleksibel untuk menampilkan data dengan desain bebas.  

- #### Grid  
  Komponen tabel standar untuk menampilkan daftar data dari database.  

- #### Group  
  Kontainer untuk mengelompokkan beberapa elemen UI agar lebih terstruktur.  

- #### Html  
  Menyisipkan kode HTML kustom secara langsung ke dalam layar.  

- #### Responsive Table  
  Tabel yang otomatis menyesuaikan tampilan di berbagai ukuran layar.  

- #### Section  
  Bagian layar yang dapat dilipat (*collapsible*) untuk mengorganisasi konten.  

- #### SmartTable  
  Tabel interaktif dengan fitur tambahan seperti filter, pencarian, dan navigasi otomatis.  

- #### Stencil  
  Template desain visual siap pakai untuk mempercepat pembuatan layout.  

- #### Tab  
  Komponen untuk menampilkan konten dalam bentuk tab navigasi.  

- #### Table  
  Tabel sederhana untuk menata elemen secara baris dan kolom.  

    

Untuk comopnent yang tidak tersedia di toolbox, anda bisa mencarinya juga di [Genexus Marketplace.](https://marketplace.genexus.com/home.aspx?,en)

# Tutorial
    
### Reusable Component

Untuk membuat komponen yang dapat digunakan dibanyak tempat, anda perlu menambahkan Object Web Component.

Create New Web Component

> 💡 New > Object >User Interface > Web Component


Untuk menggunakannya pada halaman web, anda membutuhkan component  Web Component dari toolbox

Example :

> 💡 Web Panel > Toolbox > Web Component > Object > Pilih Reusable Component

    
### Use Design System
    
Design systems adalah object untuk berisi kumpulan style, layout, dan behavior standar. jadi anda bisa membuat custom style dengan design system.

Create New Design System

> 💡 New > Object > User Interface > Design System



Pada object design system, ada Tab Style dan pastikan dibuka dengan : 

```css
styles Base {
	// type your code css
}
```

Anda bisa digunakan kepada tiap component yang menggunakan design system ini, untuk mengatur design system pada aplikasi, web panel, transaction, web master panel dll. anda bisa mengaturnya pada properties style yang ada pada tiap object.

Example :


> 💡 Object Web Panel > Properties > Style

### Build Pagination
Untuk membuat pagination pada Grid, anda hanya perlu mengatur **Paging** dan **Rows** di properties Grid seperti ini:
![image](https://hackmd.io/_uploads/SkHNkXboxe.png)

### Adding Component to Grid Cell
Grid adalah sebuah component untuk melooping sebuah data, Pada Genexus, ada 2 tipe Grid seperti berikut:

- Grid
Berwarna hijau, tidak bisa menambah cell/row, cell tidak bisa ditambahkan component seperti button, hyperlink, tabel dll.
![image](https://hackmd.io/_uploads/B1RJxXbsxl.png)

- FreeStyleGrid
Berwarna biru, bisa menambahkan cell/row, cell bisa dimasukan component.
Untuk menambahkan component pada FreeStyleGrid, seret aja dari toolbox di cell yang anda buat.

![image](https://hackmd.io/_uploads/ByC7e7Wixl.png)


### Import JSON to SDT
Genexus menyediakan fitur import JSON yang secara otomatis membuat SDT berdasarkan struktur JSON.
- [Apa itu SDT (Structured Data Type)?](https://hackmd.io/@9Jiq9WM9SIWJsYjajf9rHQ/rywchiAcex#SDT-Structured-Data-Type)

> 💡 Tools > Application Integration > JSON Import

![image](https://hackmd.io/_uploads/BykosPUjlg.png)

Setelah terbuka jendela Json Import, anda bisa import json file dari file path/url atau text    
![image](https://hackmd.io/_uploads/Hy9hjvIige.png)
Jika klik oke, maka otomatis terbuat SDT
    
![image](https://hackmd.io/_uploads/ryiasPUjxx.png)

Jika contoh jsonnya berupa list, maka otomatis **Is Collection** tercentang.

>💡Harap Perhatikan Data Tipe tiap Attribute



###### tags: `Genexus` `Training` `Front-End`

### Object
---
Di GeneXus, hampir semua yang kita kerjakan itu berbentuk Object. Object ini semacam ‘komponen’ yang punya fungsi masing-masing. Nah, tiap jenis object dipakai untuk kebutuhan berbeda. Object yang akan digunakan nanti ada SDT (Structured Data Type), Transaction, Data Provider, Procedure, API

### Transaction
---
Transaction di GeneXus adalah object untuk mendefinisikan struktur data utama. Dari Transaction ini, GeneXus otomatis membuat tabel di database beserta operasi CRUD, sehingga pengelolaan data jadi lebih mudah tanpa harus menulis SQL manual.

![image](https://hackmd.io/_uploads/HkcCMmmoxx.png)

### Tab Structure
Berisi Attribute Transaction
    *  Type -> Jenis Attribute
                Notes : Untuk identifier dalam genexus itu tidak ada type nya, lalu untuk membuat id di genexus buatlah domain di genexus atau kalau gamau ribet di bagian type attribute yang merupakan identifier dari transaction tersebut, default type ketika membuat attribute itu numeric nah cara membuat identifier cukup tulis di depan numeric "id=", genexus langsung otomatis membuat domain, tapi ada satu lagi agar domain id sempurna yaitu membuat true autonumbernya caranya di bagian atas ada tab view -> klik -> muncul banyak menu -> klik domain -> scroll sampe bawah poll maka muncul nama id klik -> dibagian kanan layar muncul properties cari menu autonumber dan set ke true maka akan jadi identifier tanpa perlu inisiasi ulang, lalu untuk penggunaannya, genexus otomatis apabila penamaan attribute ada unsur id makan akan detect type data domain id 
    *  Formula -> Operasi Perhitungan 
    *  Nullable -> Attribute tersebut wajib di isi atau tidak

* Tab Web Layout 
Berfungsi untuk layouting dan styling (kalau semisal tidak ada design)

* Tab Rules (berfungsi ketika web layout digunakan, tapi semisal di rules nya di beri parameter namun web layout tidak digunakan tidak akan mempengaruhi transaction itu sendiri, yang akan mempengaruhi dio  web layout itu sendiri)
Berfungsi untuk membuat parameter variabel yang akan dimasukkan ke dalam web layout. Untuk format kodenya :

    ```
    Parm(in:&<nama_variabel>); // wajib titik koma
    ```
* Tab Event (berfungsi ketika web layout digunakan, tapi semisal di rules nya di beri parameter namun web layout tidak digunakan tidak akan mempengaruhi transaction itu sendiri, yang akan mempengaruhi dio  web layout itu sendiri)
berfungsi untuk membuat event atau sebuah kondisi front end seperti refresh, klik button dsb yang ada di Tab Web Layout. 
Untuk Format Penulisan :
    ```
    Event <Nama_Event>
	    <Logic>
    Endevent
    ```

* Tab Variabel 
Untuk membuat variabel yang akan digunakan di Rules, Event, Web Layout.

### SDT (Structured Data Type)
---
SDT adalah object yang berfungsi sebagai model data custom. Object ini memungkinkan kita mendefinisikan struktur data kompleks yang fleksibel dan tidak selalu terikat pada tabel database.
![image](https://hackmd.io/_uploads/HJaxvXQjxg.png)
* Tab Structure
Berisi Attribute Transaction
    *  Type -> Jenis Attribute
    *  Is Colection -> Apakah Attribute atau SDT tersebut ingi dibuat list atau tidak

### Data Provider
---
Data Provider adalah object yang digunakan untuk mengambil, menyusun, dan mengembalikan data sesuai kebutuhan. Biasanya dipakai untuk menampilkan data yang sudah diformat atau dikombinasikan dari berbagai sumber.
![image](https://hackmd.io/_uploads/SJoq9WEsgl.png)

* Tab Source 
  Berfungsi untuk menuliskan kode atau SDT untuk menampung data dari transaction
    Untuk Contoh :
    ```
        // Kalau Semisal Is Collection SDTnya di checklist
        
        SDT_Rooms
            {
                SDT_RoomsItem
                {
                    RoomsId = RoomsId
                    RoomNumber = RoomsNumber
                    AdultCapacity = RoomsAdultCapacity
                    ChildrenCapacity = RoomsChildrenCapacity
                    Price = RoomsPrice
                }
            }
            
            // Kalau Semisal Is Collection SDTnya di checklist
            
            SDT_Room
            where RoomsId = &RoomsId
            {
                RoomsId = RoomsId
                RoomNumber = RoomsNumber
                AdultCapacity = RoomsAdultCapacity
                ChildrenCapacity = RoomsChildrenCapacity
                Price = RoomsPrice
            }

            
    ```
* Tab Variabel 
    Sama seperti fungsi tab variabel yang ada di tab variabel object Transaction yaitu untuk membuat dan mengelola variable yang akan digunakan di Data Provider

* Di Bagian Kanan layar ada properties (Kalau semisal ga ada cukup tekan tab seperti browser maka akan muncul properties tersebut)
  Yang akan sering digunakan itu di bagian Output dan pastikan ouput ini sesuai dengan nama SDT yang di source, untuk berjaga jaga agar saat data provider ini dipakai di procedure dan di assign dengan variable yang akan dibutuhkan itu tidka error 
  
  
### Procedure
---
Procedure adalah object yang berisi logika atau proses yang dijalankan di server. Object ini dipakai untuk menjalankan perhitungan, validasi, atau proses bisnis tertentu yang tidak otomatis ditangani oleh Transaction.
![image](https://hackmd.io/_uploads/BJhoDW4ogl.png)

* Tab Source
  Berfungsi untuk menuliskan codingan logic
  
  Example :
  
  **Get Data From Provider** 
  
  
  ```
    &SDT_Rooms = DP_GetRoom()
    
    // &SDT_Rooms => Variabel yang disiapkan atau dibuat di tab variable dan untuk penulisan variable yang ada di source itu diawali dengan &
    // DP_GetRoom() -> merupakan Data provider yang sudah dibuat dan dipanggil di Procedure
  ```
  
  **Insert Or Update Transaction**
  
    >   Pastikan di transaction bagian kanan layar di properties cari Business Component itu dibuat True, Kalau Semisal Properties nya kosong cukup tekan tab Transaction tersebut maka akan muncul sendiri
    ![image](https://hackmd.io/_uploads/S1hSwvNsee.png)

    >   Buat Variabel yang bertype dengan nama Transaction, buat variabel yang typenya SDT untuk menerima data 
    
    >   Wajib membuat variabel yang type sdt menjadi parameter input di bagian tab rules
    
    ```
        // &Rooms => Variable Type data transaction
        // &SDT_Room => Variable type data SDT untuk menampung data sementara
        
        &Rooms = New() // Untuk memberi tahu genexus bahwa ini data baru 

        // untuk mengeset data ke dalam transaction
        &Rooms.RoomsId = &SDT_Room.RoomsId
        &Rooms.RoomsNumber = &SDT_Room.RoomNumber
        &Rooms.RoomsAdultCapacity = &SDT_Room.AdultCapacity
        &Rooms.RoomsChildrenCapacity = &SDT_Room.ChildrenCapacity
        &Rooms.RoomsPrice = &SDT_Room.Price
        
        // Kondisi untuk melakukan update atau delete data di transaction
        if &SDT_Room.RoomsId.IsEmpty()
            &Rooms.Insert()
        else
            &Rooms.Update()
        endif

        commit // ini wajib di tulis untuk melakukan sebuah commit pada database
    ```
  
  **Delete Data**
  
    >   Membuat Variable type data id dari transaction dan type data transaction tersebut
    
    >   Variable yang type data id ini wajib dibuat parameter 
  
      ```
        &Rooms.Load(&RoomsId) // untuk mengambil data berdasarkan id
        &Rooms.Delete() // untuk mendelete setelah di load
        commit // untuk commit dan wajib
      ```
 
*  Tab Rules
   Sama halnya seperti di tab rules yang ada di transaction, berfungsi sebagai set paramater untuk input dan output yang akan di keluarkan oleh procedure tersebut. Untuk membuat parameter input menggunakan in kalau output out dan kalau ingin banyak input dan output cukup kasih koma saja.
   
    ```
    Parm(in:&<nama_variabel>, out:&<nama_variabel>); // wajib titik koma
    ```
* Tab Variable 
  Sama Seperti fungsi tab variable di Data Provider, Transaction untuk mengelola variable yang akan digunakan atau dipakai.
  
* Tab Sisa Masih Di Explore lebih lanjut
  
### API Object
---
API Object digunakan untuk menyediakan layanan aplikasi melalui protokol HTTP. Dengan object ini, data atau logika yang ada di aplikasi bisa diekspos menjadi REST API agar dapat diakses oleh sistem atau aplikasi lain.
![image](https://hackmd.io/_uploads/BJbML4rjex.png)

* Tab Service Source 
  Berfungsi untuk penulisan api 
  
  ```
      RoomAPICRUD {      // inisiasi object terlebih dahulu untuk penamaan bebas
        
        GetRooms(out:&SDT_Rooms) // untuk method api get tidak perlu konfigurasi tambahan cukup buat naming apinya lalu buat parameter input atau output atau dua duanya 
        => GetRooms(); // pemamnggilan procedure yang akan di expose ke api

        [RestMethod(POST)] // kalau semisal method api nya dalam bentuk POS harus ada tambahan seperti ini
        RoomInsertUpdate(in:&SDT_Rooms)
        => Proc_InsertOrUpdateRooms(&SDT_Rooms); // bentuk procedure kalau semisal dipanggil dan ada parameter inputnya codenya seperti ini.
      }
  ```

* Tab Event
  berfungsi untuk menambah sebuah event custom apabila api yang ada di tab service source ketika di hit akan di menjalankan logic apa.
  
  ```
      Event RoomInsertUpdate.After // RoomInsertUpdate merupakan nama api yang kita buat di service source lalu .after merupakan sebuah event apabila api ini sudah di hit atau di access maka akan menjalankan logic dibawah ini
        if not &IsSuccess
            &RestCode = 400
        endif
	
      EndEvent
  ```

* Tab Variable
  Sama seperti fungsi tab variable yang ada di transaction, Data Provider, Procedure untuk mengelola variable yang akan digunakan oleh object tersebut

            
<br/><br/><br/>
# Cara Instal Genexus

Untuk memulai pembuatan api di genexus harus punya aplikasi genexus itu sendiri dan caranya sebagai berikut : 

1. Kunjungi Link https://www.genexus.com/en/products/genexus/try-genexus
2. Lalu isi form sesuai data kalian

    ![image](https://hackmd.io/_uploads/SkPDIgljxg.png)
3. Setelah isi form tunggu sampai genexus mengirim email untuk aplikasinya (biasanya dibagian tab promosi untuk letaknya emailnya)
 ![image](https://hackmd.io/_uploads/HkXEOeligl.png)

4. Setelah Dapat Emailnya Seperti ini klik link yang Trial of Genexus 18, setelah itu akan diarahkan ke halaman download dan genexus akan ke auto download sendiri
 ![image](https://hackmd.io/_uploads/Sydtwxgjlx.png)
5. Setelah berhasil download maka langkah selanjutnya tinggal install saja
6. Kalau muncul seperti ini maka langsung install dan tunggu sampai installnya selesai, kalau semisal ada pop up error dan ada tombol ok langsung klik ok saja

![image](https://hackmd.io/_uploads/B17SG-eogx.png)
7. Setelah selesai maka akan muncul seperti ini, lansung klik next aja

   ![image](https://hackmd.io/_uploads/BkvyNWlogl.png) !
8. Lanjut muncul seperti ini, langsung install saja dan tunggu sampai selesai

![image](https://hackmd.io/_uploads/rJNEEWeoee.png)
9. Kalau Sudah selesai maka akan muncul seperti ini dan tinggal run saja 

![image](https://hackmd.io/_uploads/S1cyBbeolg.png)
10. Maka akan lansung muncul seperti ini
![image](https://hackmd.io/_uploads/r1BBrbgoxl.png)
11. Untuk memulai pembuatan api nya klik file yang ada di pojok kiri atas pilih new -> knowledge base
    ![image](https://hackmd.io/_uploads/HkP5SZgole.png)
12. Maka akan muncul notif seperti ini, setelah itu tinggal beri nama saja, dan set location project dibagian Location untuk memudahkan management project yang akan dibuat kedepannya, lalu tinggal klik tombol Create.
   ![image](https://hackmd.io/_uploads/S1F2BWloxl.png)
13. Setelah selesai maka akan muncul seperti ini, dan tinggal dibuat apinya
    ![image](https://hackmd.io/_uploads/S1p4LZeigx.png)


<br/><br/><br/>

# Pembuatan Back End Booking di Genexus

Pembuatan back-end di GeneXus dilakukan dengan memanfaatkan berbagai object seperti Transaction untuk membangun struktur data, Procedure untuk logika bisnis, Data Provider untuk mengolah data, serta API Object untuk expose layanan. Semua komponen ini saling terintegrasi sehingga back-end dapat terbentuk secara otomatis tanpa perlu menulis kode manual yang rumit.

**1. 

**2. Membuat Object Transaction**
---
Untuk membuat transaction :
1. Klik kanan pada folder Transaction
2. Kalau mau rapi dan apabila transaction ini saling berkaitan dan bisa dibuat folder baru dan transaction di kelompokkan by nama transaction (opsional)
3. New Object 
4. Biasanya langsung muncul nama Transaction atau pilih Object maka akan muncul pop up dibagian kira pilih Data Management lalu dibagian kanan cari Transaction
5. Buat Attribute Transaction dengan sesuai dengan attribute database Booking, Untuk penamaan ada aturan dari pihak genexus yaitu 
    ```
        <Nama_Transaction>+<NamaAttribute> => RoomsId
    ```

**2. Membuat SDT atau Structured Data Type**
---
Setelah membuat transaction buat 2 SDT di folder SDT dan kalau bisa di     yang pertama SDT dengan attribute yang kurang lebih sama dengan attribut dari transaction untuk penamaan bebas tapi intinya sama dengan attribute transaction dengan catatan untuk id dari SDT namanya harus sama dengan id dari transaction tersebut sama jangan lupa iscollection di centang, lalu untuk SDT kedua cukup duplikat saja SDT pertama dan hasil duplikat ini rename jangan lupa dan iscollection centang dihapus

**3. Membuat Data Provider**
---
Setelah membuat langkah selanjutnya membuat Data Provider
untuk proses pembuatan Data Provider sudah dijelaskan diatas dan total pembuatan Data Provider ini 2 saja sama dengan sesuai dengan SDT dan sesuai dengan foldernya


**4. Membuat Procedure**
---
Setelah membuat Data Provider langkah selanjutnya buat Procedure untuk buat nya sudah ada contoh di atas tinggal disesuaikan dengan attribute dan transaction serta Data Providernya dan sesuai dengan foldernya

**5. Membuat Api**
---
Setelah membuat procedure langkah selanjutnya tinggal membuat api dan totalnya cukup 1 object api saja, lalu tinggal buat method apinya mau post atau get dan sesuai dengan foldernya

**6. Tinggal di build all atau run**
---
Tahap terakhir tinggal di build all saja atau di run untuk caranya cukup mudah, tinggal tekan tab build lalu muncul pilihan dan build all atau cukup klik tombbol play hijau

![image](https://hackmd.io/_uploads/ByOPZ6Jhgx.png)

apabila mengikuti tahap ini sampai selesai dan belum di run maka akan muncul tab Impact Analisys dan tombol Create dan cancel cukup tekan create aja karena disitu genexus akan mengkonfirmasi kita untuk menyuruh kita membuat database dari transaction yang sudah dibuat kalau semisal muncul seperti di bawah persis itu menandakan bahwa saat kita sudah run dan sudah buat database dan kita buat transaction baru maka genexus mengkonfirmasi bahwa di database ada reorganisasi atau ada pemabruan table baru atau ada perubahan attribute dari transaction
![image](https://hackmd.io/_uploads/BJqeQpyhgg.png)

**7. Selesai**
---

Untuk melihat hasil api nya itu di tab View -> Other Tools Windows -> Launchpad -> Maka langsung muncul tab Launchpad di view nya ada tab APIS nah di situ hasi apinya
