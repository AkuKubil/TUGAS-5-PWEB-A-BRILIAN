# TUGAS-5-PWEB-A-BRILIAN
Membuat form registrasi yang terdiri dari nama mahasiswa, nim, mata kuliah, dan dosen.

## Description
Membuat form registrasi yang terdiri dari nama mahasiswa, nim, mata kuliah, dan dosen.
Implementasi : 
1. HTML
2. CSS
3. JavaScript

## Kode 

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

## Hasil 

<img width="1362" height="1436" alt="image" src="https://github.com/user-attachments/assets/12dab56a-fe3b-42d0-a5a3-622f7b599471" />

<img width="1627" height="1635" alt="image" src="https://github.com/user-attachments/assets/87099323-7578-4c70-b30d-b6760d4a4740" />


