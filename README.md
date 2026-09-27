<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Absensi Siswa</title>

<style>

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial,sans-serif;
}

body{
    background:#111;
    color:white;
    min-height:100vh;
}

header{
    background:#d90429;
    padding:18px;
    text-align:center;
    border-bottom:5px solid #ffd60a;
}

header h1{
    font-size:25px;
}

header p{
    margin-top:5px;
    color:#ffd60a;
    font-weight:bold;
}

.container{
    max-width:900px;
    margin:auto;
    padding:20px;
}

.card{
    background:#1c1c1c;
    border:2px solid #ffd60a;
    border-radius:18px;
    padding:20px;
    margin-bottom:20px;
    box-shadow:0 5px 15px #000;
}

h2{
    color:#ffd60a;
    margin-bottom:15px;
}

input{
    width:100%;
    padding:13px;
    margin:7px 0;
    border:none;
    border-radius:10px;
    font-size:16px;
}

button{
    width:100%;
    padding:14px;
    margin-top:10px;
    border:none;
    border-radius:10px;
    background:#d90429;
    color:white;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

button:hover{
    background:#ef233c;
}

.btn-pulang{
    background:#ffd60a;
    color:#111;
}

.btn-pulang:hover{
    background:#ffe45c;
}

.admin-btn{
    background:#ffd60a;
    color:#111;
}

.logout{
    background:#555;
}

.hidden{
    display:none !important;
}

.jam{
    text-align:center;
    font-size:30px;
    color:#ffd60a;
    font-weight:bold;
    margin:10px 0;
}

.tanggal{
    text-align:center;
    color:#ddd;
}

.status{
    margin-top:12px;
    padding:12px;
    border-radius:10px;
    text-align:center;
    background:#222;
    color:#ffd60a;
    font-weight:bold;
    line-height:1.7;
}

.info{
    margin-top:15px;
    padding:12px;
    background:#222;
    border-left:4px solid #ffd60a;
    border-radius:8px;
    line-height:1.7;
    color:#ddd;
}

.stats{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
    margin-bottom:20px;
}

.stat{
    background:#222;
    border:2px solid #ffd60a;
    padding:15px 5px;
    text-align:center;
    border-radius:12px;
}

.stat b{
    display:block;
    font-size:25px;
    color:#ffd60a;
}

.table-wrap{
    overflow-x:auto;
}

table{
    width:100%;
    border-collapse:collapse;
    min-width:900px;
}

th{
    background:#d90429;
    color:white;
    padding:12px;
}

td{
    padding:10px;
    border-bottom:1px solid #555;
    text-align:center;
}

tr:hover{
    background:#292929;
}

.hadir{
    color:#00ff88;
    font-weight:bold;
}

.kesiangan{
    color:#ff9800;
    font-weight:bold;
}

.kabur{
    color:#ff3333;
    font-weight:bold;
}

.pulang{
    color:#00ff88;
    font-weight:bold;
}

@media(max-width:600px){

    .stats{
        grid-template-columns:repeat(2,1fr);
    }

    header h1{
        font-size:21px;
    }

}

</style>
</head>

<body>

<header>

<h1>🔴 ABSENSI SISWA</h1>

<p>SMK • SISTEM ABSENSI DIGITAL</p>

</header>


<div class="container">


<!-- ================= SISWA ================= -->

<div id="halamanSiswa">

<div class="card">

<h2>👨‍🎓 Data Siswa</h2>

<input
id="nama"
type="text"
placeholder="Nama lengkap">

<input
id="nis"
type="text"
placeholder="NIS">

<input
id="kelas"
type="text"
placeholder="Kelas">

</div>


<div class="card">

<h2>🕐 Waktu Sekarang</h2>

<div
id="jamSekarang"
class="jam">
00:00:00
</div>

<div
id="tanggalSekarang"
class="tanggal">
-
</div>

</div>


<div class="card">

<h2>📝 Absensi</h2>

<button onclick="absenMasuk()">
🏫 ABSEN MASUK
</button>

<button
class="btn-pulang"
onclick="absenPulang()">
🏠 ABSEN PULANG
</button>

<div class="info">

<b>Ketentuan:</b><br>

• Sampai <b>06:15</b> = Hadir<br>

• <b>06:16–13:59</b> = Kesiangan<br>

• Pulang sebelum <b>15:00</b> = Kabur<br>

• Pulang <b>15:00+</b> = Pulang

</div>

</div>


<div class="card">

<h2>📋 Status Absensi</h2>

<div
id="hasil"
class="status">

Belum melakukan absensi

</div>

</div>


<div class="card">

<button
class="admin-btn"
onclick="bukaLoginAdmin()">

🔐 LOGIN ADMIN

</button>

</div>

</div>



<!-- ================= LOGIN ADMIN ================= -->

<div
id="halamanLogin"
class="hidden">

<div class="card">

<h2>🔐 LOGIN ADMIN</h2>

<input
id="kodeAdmin"
type="password"
placeholder="Masukkan kode admin"
autocomplete="off">

<button
type="button"
onclick="loginAdmin()">

MASUK ADMIN

</button>

<button
class="logout"
type="button"
onclick="kembaliSiswa()">

← Kembali

</button>

<div
id="loginStatus"
class="status">

Masukkan kode admin

</div>

</div>

</div>



<!-- ================= ADMIN ================= -->

<div
id="halamanAdmin"
class="hidden">

<div class="card">

<h2>📊 DASHBOARD REKAP ABSENSI</h2>

<div class="stats">

<div class="stat">

<b id="jumlahHadir">0</b>

Hadir

</div>

<div class="stat">

<b id="jumlahKesiangan">0</b>

Kesiangan

</div>

<div class="stat">

<b id="jumlahKabur">0</b>

Kabur

</div>

<div class="stat">

<b id="jumlahPulang">0</b>

Pulang

</div>

</div>

<input
id="cari"
type="text"
placeholder="🔎 Cari nama, NIS, atau kelas..."
oninput="tampilkanData()">

</div>



<div class="card">

<h2>📑 Data Absensi</h2>

<div class="table-wrap">

<table>

<thead>

<tr>

<th>No</th>
<th>Nama</th>
<th>NIS</th>
<th>Kelas</th>
<th>Tanggal</th>
<th>Masuk</th>
<th>Status Masuk</th>
<th>Pulang</th>
<th>Status Pulang</th>

</tr>

</thead>

<tbody id="tabelAbsensi">
</tbody>

</table>

</div>


<button onclick="exportCSV()">

📥 DOWNLOAD REKAP CSV

</button>


<button onclick="hapusSemuaData()">

🗑️ HAPUS SEMUA DATA

</button>


<button
class="logout"
onclick="logoutAdmin()">

🚪 KELUAR ADMIN

</button>

</div>

</div>

</div>



<script>

/* =====================================
   KODE ADMIN
===================================== */

const KODE_ADMIN = "Nabhanalip";


/* =====================================
   DATA ABSENSI
===================================== */

let dataAbsensi = JSON.parse(
    localStorage.getItem("dataAbsensi") || "[]"
);


/* =====================================
   JAM REAL TIME
===================================== */

function updateJam(){

    const sekarang = new Date();

    const jam =
        String(sekarang.getHours()).padStart(2,"0");

    const menit =
        String(sekarang.getMinutes()).padStart(2,"0");

    const detik =
        String(sekarang.getSeconds()).padStart(2,"0");

    document.getElementById(
        "jamSekarang"
    ).innerText =
        jam + ":" + menit + ":" + detik;

    document.getElementById(
        "tanggalSekarang"
    ).innerText =
        sekarang.toLocaleDateString(
            "id-ID",
            {
                weekday:"long",
                year:"numeric",
                month:"long",
                day:"numeric"
            }
        );
}

setInterval(updateJam,1000);

updateJam();


/* =====================================
   SUARA
===================================== */

function suaraBerhasil(nama){

    if("speechSynthesis" in window){

        speechSynthesis.cancel();

        const ucapan =
            new SpeechSynthesisUtterance(
                nama + " berhasil"
            );

        ucapan.lang = "id-ID";
        ucapan.rate = 0.9;

        speechSynthesis.speak(ucapan);
    }
}


/* =====================================
   SIMPAN DATA
===================================== */

function simpanData(){

    localStorage.setItem(
        "dataAbsensi",
        JSON.stringify(dataAbsensi)
    );
}


/* =====================================
   ABSEN MASUK
===================================== */

function absenMasuk(){

    const nama =
        document.getElementById("nama").value.trim();

    const nis =
        document.getElementById("nis").value.trim();

    const kelas =
        document.getElementById("kelas").value.trim();


    if(
        nama === "" ||
        nis === "" ||
        kelas === ""
    ){

        alert(
            "Lengkapi Nama, NIS, dan Kelas terlebih dahulu!"
        );

        return;
    }


    const sekarang = new Date();

    const tanggal =
        sekarang.toLocaleDateString("id-ID");

    const jam =
        String(sekarang.getHours()).padStart(2,"0");

    const menit =
        String(sekarang.getMinutes()).padStart(2,"0");

    const detik =
        String(sekarang.getSeconds()).padStart(2,"0");

    const jamLengkap =
        jam + ":" + menit + ":" + detik;


    const sudahAda =
        dataAbsensi.find(function(data){

            return (
                data.nis === nis &&
                data.tanggal === tanggal
            );

        });


    if(sudahAda){

        alert(
            "Kamu sudah absen masuk hari ini!"
        );

        return;
    }


    let statusMasuk;


    if(
        sekarang.getHours() < 6 ||

        (
            sekarang.getHours() === 6 &&
            sekarang.getMinutes() <= 15
        )
    ){

        statusMasuk = "Hadir";

    }else{

        statusMasuk = "Kesiangan";

    }


    const dataBaru = {

        nama:nama,

        nis:nis,

        kelas:kelas,

        tanggal:tanggal,

        masuk:jamLengkap,

        statusMasuk:statusMasuk,

        pulang:"-",

        statusPulang:"-"

    };


    dataAbsensi.push(dataBaru);

    simpanData();


    document.getElementById(
        "hasil"
    ).innerHTML =

        "✅ ABSEN MASUK BERHASIL<br>" +

        "<b>" + nama + "</b><br>" +

        "Jam: " + jamLengkap + "<br>" +

        "Status: " + statusMasuk;


    suaraBerhasil(nama);

}


/* =====================================
   ABSEN PULANG
===================================== */

function absenPulang(){

    const nama =
        document.getElementById("nama").value.trim();

    const nis =
        document.getElementById("nis").value.trim();

    const kelas =
        document.getElementById("kelas").value.trim();


    if(
        nama === "" ||
        nis === "" ||
        kelas === ""
    ){

        alert(
            "Lengkapi Nama, NIS, dan Kelas terlebih dahulu!"
        );

        return;
    }


    const sekarang = new Date();

    const tanggal =
        sekarang.toLocaleDateString("id-ID");

    const jam =
        String(sekarang.getHours()).padStart(2,"0");

    const menit =
        String(sekarang.getMinutes()).padStart(2,"0");

    const detik =
        String(sekarang.getSeconds()).padStart(2,"0");

    const jamLengkap =
        jam + ":" + menit + ":" + detik;


    const data =
        dataAbsensi.find(function(item){

            return (
                item.nis === nis &&
                item.tanggal === tanggal
            );

        });


    if(!data){

        alert(
            "Kamu belum melakukan absen masuk hari ini!"
        );

        return;
    }


    if(data.pulang !== "-"){

        alert(
            "Kamu sudah melakukan absen pulang hari ini!"
        );

        return;
    }


    let statusPulang;


    if(
        sekarang.getHours() >= 15
    ){

        statusPulang = "Pulang";

    }else{

        statusPulang = "Kabur";

    }


    data.pulang = jamLengkap;

    data.statusPulang = statusPulang;

    simpanData();


    document.getElementById(
        "hasil"
    ).innerHTML =

        "✅ ABSEN PULANG BERHASIL<br>" +

        "<b>" + nama + "</b><br>" +

        "Jam: " + jamLengkap + "<br>" +

        "Status: " + statusPulang;


    suaraBerhasil(nama);

}


/* =====================================
   BUKA LOGIN ADMIN
===================================== */

function bukaLoginAdmin(){

    document.getElementById(
        "halamanSiswa"
    ).classList.add("hidden");


    document.getElementById(
        "halamanLogin"
    ).classList.remove("hidden");


    document.getElementById(
        "halamanAdmin"
    ).classList.add("hidden");


    document.getElementById(
        "kodeAdmin"
    ).value = "";


    document.getElementById(
        "loginStatus"
    ).innerText =
        "Masukkan kode admin";


    setTimeout(function(){

        document.getElementById(
            "kodeAdmin"
        ).focus();

    },100);

}


/* =====================================
   LOGIN ADMIN — DIPERBAIKI
===================================== */

function loginAdmin(){

    const input =
        document.getElementById(
            "kodeAdmin"
        );


    const kode =
        input.value.trim();


    if(kode === KODE_ADMIN){

        document.getElementById(
            "halamanLogin"
        ).classList.add("hidden");


        document.getElementById(
            "halamanSiswa"
        ).classList.add("hidden");


        document.getElementById(
            "halamanAdmin"
        ).classList.remove("hidden");


        document.getElementById(
            "loginStatus"
        ).innerText = "";


        document.getElementById(
            "kodeAdmin"
        ).value = "";


        tampilkanData();

    }else{

        document.getElementById(
            "loginStatus"
        ).innerText =
            "❌ Kode admin salah!";


        input.value = "";

        input.focus();

    }

}


/* =====================================
   ENTER UNTUK LOGIN
===================================== */

document.getElementById(
    "kodeAdmin"
).addEventListener(
    "keydown",
    function(event){

        if(event.key === "Enter"){

            event.preventDefault();

            loginAdmin();

        }

    }
);


/* =====================================
   KEMBALI SISWA
===================================== */

function kembaliSiswa(){

    document.getElementById(
        "halamanLogin"
    ).classList.add("hidden");


    document.getElementById(
        "halamanAdmin"
    ).classList.add("hidden");


    document.getElementById(
        "halamanSiswa"
    ).classList.remove("hidden");

}


/* =====================================
   LOGOUT ADMIN
===================================== */

function logoutAdmin(){

    document.getElementById(
        "halamanAdmin"
    ).classList.add("hidden");


    document.getElementById(
        "halamanLogin"
    ).classList.add("hidden");


    document.getElementById(
        "halamanSiswa"
    ).classList.remove("hidden");


    document.getElementById(
        "kodeAdmin"
    ).value = "";

}


/* =====================================
   TAMPILKAN DATA
===================================== */

function tampilkanData(){

    dataAbsensi =
        JSON.parse(
            localStorage.getItem(
                "dataAbsensi"
            ) || "[]"
        );


    const pencarian =
        document.getElementById(
            "cari"
        ).value.toLowerCase();


    const hasil =
        dataAbsensi.filter(
            function(data){

                return (

                    data.nama
                    .toLowerCase()
                    .includes(pencarian)

                    ||

                    data.nis
                    .toLowerCase()
                    .includes(pencarian)

                    ||

                    data.kelas
                    .toLowerCase()
                    .includes(pencarian)

                );

            }
        );


    const tabel =
        document.getElementById(
            "tabelAbsensi"
        );


    tabel.innerHTML = "";


    hasil.forEach(
        function(data,index){

            const kelasMasuk =
                data.statusMasuk === "Hadir"
                ? "hadir"
                : "kesiangan";


            const kelasPulang =
                data.statusPulang === "Pulang"
                ? "pulang"
                : "kabur";


            const baris =
                document.createElement("tr");


            baris.innerHTML =

                "<td>" +
                (index + 1) +
                "</td>" +

                "<td>" +
                data.nama +
                "</td>" +

                "<td>" +
                data.nis +
                "</td>" +

                "<td>" +
                data.kelas +
                "</td>" +

                "<td>" +
                data.tanggal +
                "</td>" +

                "<td>" +
                data.masuk +
                "</td>" +

                "<td class='" +
                kelasMasuk +
                "'>" +
                data.statusMasuk +
                "</td>" +

                "<td>" +
                data.pulang +
                "</td>" +

                "<td class='" +
                kelasPulang +
                "'>" +
                data.statusPulang +
                "</td>";


            tabel.appendChild(baris);

        }
    );


    hitungStatistik();

}


/* =====================================
   STATISTIK
===================================== */

function hitungStatistik(){

    document.getElementById(
        "jumlahHadir"
    ).innerText =

        dataAbsensi.filter(
            function(data){

                return data.statusMasuk === "Hadir";

            }
        ).length;


    document.getElementById(
        "jumlahKesiangan"
    ).innerText =

        dataAbsensi.filter(
            function(data){

                return data.statusMasuk === "Kesiangan";

            }
        ).length;


    document.getElementById(
        "jumlahKabur"
    ).innerText =

        dataAbsensi.filter(
            function(data){

                return data.statusPulang === "Kabur";

            }
        ).length;


    document.getElementById(
        "jumlahPulang"
    ).innerText =

        dataAbsensi.filter(
            function(data){

                return data.statusPulang === "Pulang";

            }
        ).length;

}


/* =====================================
   EXPORT CSV
===================================== */

function exportCSV(){

    if(dataAbsensi.length === 0){

        alert(
            "Belum ada data absensi!"
        );

        return;
    }


    let csv =
        "No,Nama,NIS,Kelas,Tanggal,Masuk,Status Masuk,Pulang,Status Pulang\n";


    dataAbsensi.forEach(
        function(data,index){

            csv +=

                (index + 1) +
                ',"' +
                data.nama +
                '","' +
                data.nis +
                '","' +
                data.kelas +
                '","' +
                data.tanggal +
                '","' +
                data.masuk +
                '","' +
                data.statusMasuk +
                '","' +
                data.pulang +
                '","' +
                data.statusPulang +
                '"\n';

        }
    );


    const blob =
        new Blob(
            [csv],
            {
                type:"text/csv"
            }
        );


    const url =
        URL.createObjectURL(blob);


    const link =
        document.createElement("a");


    link.href = url;

    link.download =
        "rekap_absensi.csv";


    document.body.appendChild(link);

    link.click();

    document.body.removeChild(link);


    URL.revokeObjectURL(url);

}


/* =====================================
   HAPUS SEMUA DATA
===================================== */

function hapusSemuaData(){

    const yakin =
        confirm(
            "Yakin ingin menghapus SEMUA data absensi?"
        );


    if(yakin){

        const kode =
            prompt(
                "Masukkan kode admin:"
            );


        if(kode === KODE_ADMIN){

            localStorage.removeItem(
                "dataAbsensi"
            );


            dataAbsensi = [];


            tampilkanData();


            alert(
                "Semua data berhasil dihapus!"
            );

        }else{

            alert(
                "Kode admin salah!"
            );

        }

    }

}

</script>

</body>
</html>
