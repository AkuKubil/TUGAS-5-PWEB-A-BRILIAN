# TUGAS-5-PWEB-A-BRILIAN

## Nomor 1 
Membuat form registrasi yang terdiri dari nama mahasiswa, nim, mata kuliah, dan dosen.

### Description
Membuat form registrasi yang terdiri dari nama mahasiswa, nim, mata kuliah, dan dosen.

Implementasi : 
1. HTML
2. CSS
3. JavaScript

### Code 

index.html 

```
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Latihan JS: Form Registrasi Cerdas</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h2>Form Registrasi Mahasiswa</h2>
        <form id="regForm">
            
            <div class="form-group">
                <label>Nama Mahasiswa:</label>
                <input type="text" id="inputNama" placeholder="Ketik nama (misal: Budi)..." autocomplete="off">
                <div id="saranNama" class="autocomplete-list"></div> </div>

            <div class="form-group">
                <label>NIM:</label>
                <input type="number" id="inputNim" placeholder="Masukkan NIM">
            </div>

            <div class="form-group">
                <label>Jurusan:</label>
                <select id="selectJurusan">
                    <option value="">-- Pilih Jurusan --</option>
                    <option value="ti">Teknik Informatika</option>
                    <option value="si">Sistem Informasi</option>
                    <option value="dkv">Desain Komunikasi Visual</option>
                </select>
            </div>

            <div class="form-group">
                <label>Mata Kuliah (Berubah sesuai Jurusan):</label>
                <select id="selectMatkul" disabled>
                    <option value="">-- Pilih Jurusan Dulu --</option>
                </select>
            </div>

            <button type="submit" id="btnSubmit">Daftar Sekarang</button>
        </form>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

style.css

```
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    background-color: #ffffff; 
    padding: 2.5rem;
    border-radius: 20px; 
    width: 450px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1); 
    border: 1px solid rgba(255, 255, 255, 0.5);
}

h2 {
    text-align: center;
    color: #333;
    margin-bottom: 25px;
    font-weight: 700;
    letter-spacing: -0.5px;
}

.form-group {
    margin-bottom: 20px;
    position: relative;
}

label {
    display: block;
    margin-bottom: 8px;
    color: #555;
    font-weight: 600;
    font-size: 0.9rem;
}

input, select {
    width: 100%;
    padding: 12px 15px;
    border-radius: 10px;
    border: 2px solid #f0f2f5; 
    background-color: #f9fafb; 
    color: #333;
    font-size: 1rem;
    transition: all 0.3s ease;
    outline: none;
}

input:focus, select:focus {
    background-color: #fff;
    border-color: #4a90e2; 
    box-shadow: 0 0 0 4px rgba(74, 144, 226, 0.1);
}

button {
    width: 100%;
    padding: 14px;
    background: linear-gradient(to right, #4a90e2, #8e44ad);
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    font-size: 1rem;
    cursor: pointer;
    margin-top: 15px;
    transition: transform 0.2s;
}

button:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(74, 144, 226, 0.3);
}

.autocomplete-list {
    position: absolute;
    border: 1px solid #e1e4e8;
    border-top: none;
    z-index: 99;
    top: 100%;
    left: 0;
    right: 0;
    background-color: #ffffff;
    border-radius: 0 0 10px 10px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.05);
    overflow: hidden;
}

.autocomplete-list div {
    padding: 12px;
    cursor: pointer;
    background-color: #fff;
    color: #333;
    border-bottom: 1px solid #f0f0f0;
}

.autocomplete-list div:hover {
    background-color: #f0f7ff; 
    color: #4a90e2;
}
```

script.js

```
const databaseMahasiswa = [
    "Ahmad Dahlan", "Andi Saputra", "Anisa Rahma", 
    "Budi Santoso", "Bambang Pamungkas", 
    "Citra Kirana", "Chandra Wijaya",
    "Dimas Anggara", "Dewi Persik",
    "Eko Patrio", "Fajar Sadboy"
];

const dataMatkul = {
    "ti": ["Algoritma", "Web Programming", "Basis Data", "Kecerdasan Buatan"],
    "si": ["Manajemen Proyek", "E-Business", "Akuntansi Dasar", "ERP"],
    "dkv": ["Tipografi", "Fotografi", "Animasi 2D", "Videografi"]
};

const inputNama = document.getElementById('inputNama');
const saranNama = document.getElementById('saranNama');
const selectJurusan = document.getElementById('selectJurusan');
const selectMatkul = document.getElementById('selectMatkul');
const form = document.getElementById('regForm');

inputNama.addEventListener('input', function() {
    const ketikan = this.value.toLowerCase();
    saranNama.innerHTML = ''; 

    if (!ketikan) return; 

    const hasilFilter = databaseMahasiswa.filter(nama => 
        nama.toLowerCase().includes(ketikan)
    );

    hasilFilter.forEach(nama => {
        const div = document.createElement('div');
        div.textContent = nama;

        div.addEventListener('click', function() {
            inputNama.value = nama;
            saranNama.innerHTML = '';
        });

        saranNama.appendChild(div);
    });
});

document.addEventListener('click', function(e) {
    if (e.target !== inputNama) {
        saranNama.innerHTML = '';
    }
});

selectJurusan.addEventListener('change', function() {
    const jurusanTerpilih = this.value;

    selectMatkul.innerHTML = '<option value="">-- Pilih Mata Kuliah --</option>';

    if (jurusanTerpilih) {
        selectMatkul.disabled = false; 
        const daftarMatkul = dataMatkul[jurusanTerpilih];

        daftarMatkul.forEach(matkul => {
            const option = document.createElement('option');
            option.value = matkul;
            option.textContent = matkul;
            selectMatkul.appendChild(option);
        });
    } else {
        selectMatkul.disabled = true; 
        selectMatkul.innerHTML = '<option value="">-- Pilih Jurusan Dulu --</option>';
    }
});

form.addEventListener('submit', function(e) {
    e.preventDefault(); 

    const nama = inputNama.value;
    const nim = document.getElementById('inputNim').value;
    const jurusan = selectJurusan.value;
    const matkul = selectMatkul.value;

    if (nama === '' || nim === '' || jurusan === '' || matkul === '') {
        alert("❌ ERROR: Semua data wajib diisi!");
        return;
    }

    alert(`✅ SUKSES!\nData Terkirim:\nNama: ${nama}\nNIM: ${nim}\nMatkul: ${matkul}`);
    form.reset();
    selectMatkul.disabled = true;
    selectMatkul.innerHTML = '<option value="">-- Pilih Jurusan Dulu --</option>';
});
```

### Web Result

<img width="1362" height="1436" alt="image" src="https://github.com/user-attachments/assets/12dab56a-fe3b-42d0-a5a3-622f7b599471" />

<img width="1627" height="1635" alt="image" src="https://github.com/user-attachments/assets/87099323-7578-4c70-b30d-b6760d4a4740" />

<img width="1087" height="1374" alt="image" src="https://github.com/user-attachments/assets/13b74120-98ce-41f6-b3cc-30b3cb2c2686" />

## Nomor 2

### Description
Membuat form pencarian kode pos Indonesia dengan inputan Provinsi, Kabupaten/ Kota, Kecamatan, kemudian outputnya kode pos dan informasi daerah.

### Kode 

kodepos.html
```
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cari Kode Pos Indonesia</title>
    <link rel="stylesheet" href="style-kodepos.css">
</head>
<body>

    <div class="container">
        <div class="header">
            <h2>📮 Cek Kode Pos</h2>
            <p>Pilih wilayah secara berurutan untuk melihat kode pos.</p>
        </div>

        <form id="posForm">
            <div class="form-group">
                <label>Provinsi</label>
                <select id="selectProvinsi">
                    <option value="">-- Pilih Provinsi --</option>
                </select>
            </div>

            <div class="form-group">
                <label>Kota / Kabupaten</label>
                <select id="selectKota" disabled>
                    <option value="">-- Pilih Provinsi Dulu --</option>
                </select>
            </div>

            <div class="form-group">
                <label>Kecamatan</label>
                <select id="selectKecamatan" disabled>
                    <option value="">-- Pilih Kota Dulu --</option>
                </select>
            </div>
        </form>

        <div id="resultCard" class="result-box hidden">
            <h3>Hasil Pencarian</h3>
            <div class="result-content">
                <span class="badge">Ditemukan</span>
                <p>Kode Pos untuk daerah <strong id="resKecamatan">-</strong>, <span id="resKota">-</span> adalah:</p>
                <h1 id="resKodePos">00000</h1>
            </div>
        </div>

    </div>

    <script src="script-kodepos.js"></script>
</body>
</html>
```

style-kodepos.css
```
* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }

body {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    display: flex; justify-content: center; align-items: center;
    min-height: 100vh; padding: 20px;
}

.container {
    background: #fff;
    padding: 2.5rem;
    border-radius: 20px;
    width: 100%;
    max-width: 500px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.1);
}

.header { text-align: center; margin-bottom: 30px; }
.header h2 { color: #333; font-size: 1.8rem; margin-bottom: 5px; }
.header p { color: #777; font-size: 0.9rem; }

.form-group { margin-bottom: 20px; }
label { display: block; margin-bottom: 8px; font-weight: 600; color: #555; }

select {
    width: 100%; padding: 12px; border-radius: 10px;
    border: 2px solid #f0f2f5; background: #f9fafb;
    font-size: 1rem; color: #333; outline: none; transition: 0.3s;
}

select:focus { border-color: #4a90e2; background: #fff; }
select:disabled { background: #eee; cursor: not-allowed; opacity: 0.6; }

.result-box {
    margin-top: 30px;
    padding: 20px;
    background: #e8f5e9;
    border-left: 5px solid #2ecc71; 
    border-radius: 8px;
    animation: fadeIn 0.5s ease;
}

.hidden { display: none; } 

.result-box h3 { font-size: 1rem; color: #2ecc71; margin-bottom: 10px; }
.result-content p { font-size: 0.9rem; color: #555; margin-bottom: 5px; }
.result-content h1 { font-size: 2.5rem; color: #2d3436; letter-spacing: 2px; }

.badge {
    display: inline-block; padding: 4px 8px; background: #2ecc71;
    color: white; font-size: 0.7rem; border-radius: 4px; margin-bottom: 10px;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}
```

script-kodepos.js
```
const databaseIndonesia = {
    "Jawa Timur": {
        "Surabaya": {
            "Sukolilo": "60111",
            "Gubeng": "60281",
            "Rungkut": "60293",
            "Tegalsari": "60262"
        },
        "Malang": {
            "Klojen": "65111",
            "Blimbing": "65126",
            "Lowokwaru": "65141"
        }
    },
    "DKI Jakarta": {
        "Jakarta Pusat": {
            "Gambir": "10110",
            "Tanah Abang": "10240",
            "Menteng": "10310"
        },
        "Jakarta Selatan": {
            "Kebayoran Baru": "12110",
            "Cilandak": "12430",
            "Tebet": "12810"
        }
    },
    "Jawa Barat": {
        "Bandung": {
            "Cicendo": "40171",
            "Coblong": "40132",
            "Andir": "40181"
        },
        "Bekasi": {
            "Bekasi Barat": "17131",
            "Bekasi Timur": "17111"
        }
    }
};

const selectProvinsi = document.getElementById('selectProvinsi');
const selectKota = document.getElementById('selectKota');
const selectKecamatan = document.getElementById('selectKecamatan');

const resultCard = document.getElementById('resultCard');
const resKecamatan = document.getElementById('resKecamatan');
const resKota = document.getElementById('resKota');
const resKodePos = document.getElementById('resKodePos');

window.addEventListener('DOMContentLoaded', () => {
    const listProvinsi = Object.keys(databaseIndonesia);
    
    listProvinsi.forEach(prov => {
        const option = document.createElement('option');
        option.value = prov;
        option.textContent = prov;
        selectProvinsi.appendChild(option);
    });
});


selectProvinsi.addEventListener('change', function() {
    const provTerpilih = this.value;

    resetDropdown(selectKota, "-- Pilih Kota --");
    resetDropdown(selectKecamatan, "-- Pilih Kota Dulu --");
    resultCard.classList.add('hidden'); 
    selectKecamatan.disabled = true;

    if (provTerpilih) {
        selectKota.disabled = false;
        const dataKota = databaseIndonesia[provTerpilih];
        const listKota = Object.keys(dataKota);

        listKota.forEach(kota => {
            const option = document.createElement('option');
            option.value = kota;
            option.textContent = kota;
            selectKota.appendChild(option);
        });
    } else {
        selectKota.disabled = true;
    }
});

selectKota.addEventListener('change', function() {
    const provTerpilih = selectProvinsi.value;
    const kotaTerpilih = this.value;

    resetDropdown(selectKecamatan, "-- Pilih Kecamatan --");
    resultCard.classList.add('hidden');

    if (kotaTerpilih) {
        selectKecamatan.disabled = false;
        const dataKecamatan = databaseIndonesia[provTerpilih][kotaTerpilih];
        const listKecamatan = Object.keys(dataKecamatan);

        listKecamatan.forEach(kec => {
            const option = document.createElement('option');
            option.value = kec;
            option.textContent = kec;
            selectKecamatan.appendChild(option);
        });
    } else {
        selectKecamatan.disabled = true;
    }
});

selectKecamatan.addEventListener('change', function() {
    const provTerpilih = selectProvinsi.value;
    const kotaTerpilih = selectKota.value;
    const kecTerpilih = this.value;

    if (kecTerpilih) {
        const kodePos = databaseIndonesia[provTerpilih][kotaTerpilih][kecTerpilih];

        resKecamatan.textContent = kecTerpilih;
        resKota.textContent = kotaTerpilih;
        resKodePos.textContent = kodePos;
        
        resultCard.classList.remove('hidden'); 
    } else {
        resultCard.classList.add('hidden');
    }
});

function resetDropdown(element, defaultText) {
    element.innerHTML = ''; 
    const defaultOption = document.createElement('option');
    defaultOption.value = "";
    defaultOption.textContent = defaultText;
    element.appendChild(defaultOption);
}
```

### Web Result
<img width="1372" height="1541" alt="image" src="https://github.com/user-attachments/assets/471b7bc1-b043-4157-a61e-abdb46cec44a" />

<img width="1194" height="1483" alt="image" src="https://github.com/user-attachments/assets/1a8899de-0794-42ee-9cef-bfd7aeee047a" />

## Nomor 3 

### Description
Membuat List Dropdown dinamis

### Code

produk.html
```
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Dropdown Produk</title>
    <link rel="stylesheet" href="style-produk.css">
</head>
<body>

    <div class="container">
        <div class="header">
            <h2>🛍️ Katalog Produk</h2>
            <p>Pilih kategori untuk melihat merk yang tersedia.</p>
        </div>

        <form id="productForm">
            <div class="form-group">
                <label>Jenis Produk</label>
                <select id="selectKategori">
                    <option value="">-- Pilih Jenis Produk --</option>
                    <option value="desktop">Desktop PC</option>
                    <option value="laptop">Laptop</option>
                    <option value="smartphone">Smartphone</option>
                    <option value="tablet">Tablet</option>
                </select>
            </div>

            <div class="form-group">
                <label>Merk / Brand</label>
                <select id="selectMerk" disabled>
                    <option value="">-- Pilih Jenis Dulu --</option>
                </select>
            </div>
        </form>

        <div id="resultBox" class="result-card hidden">
            <p>Kamu memilih:</p>
            <h3 id="textHasil">-</h3>
            <button class="btn-checkout">Lanjut ke Pembayaran</button>
        </div>

    </div>

    <script src="script-produk.js"></script>
</body>
</html>
```

style-produk.css

```
* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }

body {
    background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%); 
    display: flex; justify-content: center; align-items: center;
    min-height: 100vh;
}

.container {
    background: #fff;
    padding: 2.5rem;
    border-radius: 15px;
    width: 400px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.05);
    border: 1px solid #eee;
}

.header { text-align: center; margin-bottom: 25px; }
.header h2 { color: #2c3e50; margin-bottom: 5px; }
.header p { color: #95a5a6; font-size: 0.9rem; }

.form-group { margin-bottom: 20px; }
label { display: block; margin-bottom: 8px; font-weight: 600; color: #34495e; }

select {
    width: 100%; padding: 12px; border-radius: 8px;
    border: 2px solid #ecf0f1; background: #fcfcfc;
    color: #2c3e50; outline: none; transition: 0.3s; cursor: pointer;
}

select:focus { border-color: #3498db; background: #fff; }
select:disabled { background: #f0f3f4; cursor: not-allowed; opacity: 0.7; }

.result-card {
    margin-top: 25px;
    padding: 20px;
    background: #eaf2f8; 
    border-radius: 10px;
    text-align: center;
    border: 1px dashed #3498db;
    animation: slideUp 0.4s ease;
}

.hidden { display: none; }

.result-card h3 { color: #2980b9; margin: 10px 0; font-size: 1.4rem; }

.btn-checkout {
    background: #27ae60;
    color: white; border: none; padding: 10px 20px;
    border-radius: 20px; font-weight: bold; cursor: pointer;
    margin-top: 10px; width: 100%;
    transition: 0.2s;
}

.btn-checkout:hover { background: #219150; transform: scale(1.02); }

@keyframes slideUp {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}
```

script-produk.js
```
const dataProduk = {
    "desktop": [
        "Dell Inspiron All-in-One",
        "HP Pavilion Gaming",
        "iMac 24 inch",
        "Lenovo IdeaCentre"
    ],
    "laptop": [
        "MacBook Pro M3",
        "Asus ROG Zephyrus",
        "Lenovo ThinkPad X1",
        "Acer Swift 5"
    ],
    "smartphone": [
        "iPhone 15 Pro",
        "Samsung Galaxy S24 Ultra",
        "Google Pixel 8",
        "Xiaomi 14"
    ],
    "tablet": [
        "iPad Air",
        "Samsung Galaxy Tab S9",
        "Microsoft Surface Go"
    ]
};

const selectKategori = document.getElementById('selectKategori');
const selectMerk = document.getElementById('selectMerk');
const resultBox = document.getElementById('resultBox');
const textHasil = document.getElementById('textHasil');

selectKategori.addEventListener('change', function() {
    const kategori = this.value;

    selectMerk.innerHTML = '<option value="">-- Pilih Merk --</option>';
    selectMerk.disabled = true;
    resultBox.classList.add('hidden'); 

    if (kategori && dataProduk[kategori]) {
        selectMerk.disabled = false;

        const daftarMerk = dataProduk[kategori];

        daftarMerk.forEach(merk => {
            const option = document.createElement('option');
            option.value = merk;
            option.textContent = merk;
            selectMerk.appendChild(option);
        });
    }
});

selectMerk.addEventListener('change', function() {
    const merk = this.value;
    if (merk) {
        textHasil.textContent = merk;
        resultBox.classList.remove('hidden');
    } else {
        resultBox.classList.add('hidden');
    }
});
```

### Web Result
<img width="1009" height="1279" alt="image" src="https://github.com/user-attachments/assets/53f110d6-fd47-49ad-9dd5-dff400e36271" />

<img width="897" height="1123" alt="image" src="https://github.com/user-attachments/assets/d7fc29fd-2898-4031-adb8-c69ed064dd67" />






