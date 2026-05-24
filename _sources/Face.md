# Struktur Project GitHub

```text
eigenface-recognition/
│
├── index.html
├── README.md
└── assets/
```

---

# File `README.md`

```md
# EigenFace Recognition

Project sederhana deteksi manusia menggunakan HTML, CSS, dan JavaScript.

## Fitur
- Kamera real-time
- Capture gambar
- Simulasi deteksi manusia
- Tampilan modern UI
- Responsive design

## Teknologi
- HTML5
- CSS3
- JavaScript

## Cara Menjalankan
1. Download project
2. Buka file `index.html`
3. Izinkan akses kamera
4. Klik tombol:
   - Start Camera
   - Capture
   - Detect

## Hasil Deteksi
- ANDA MANUSIA
- BUKAN MANUSIA
```

---

# File `index.html`

```html
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>EigenFace Recognition</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:Arial, Helvetica, sans-serif;
    background:
    radial-gradient(circle at left,#001a4d,#0f172a 40%);
    color:white;
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:30px;
}

.container{
    width:1200px;
    max-width:100%;
    background:#2d3748;
    border-radius:30px;
    padding:40px;
    box-shadow:0 0 30px rgba(0,0,0,0.5);
}

.title{
    text-align:center;
    margin-bottom:40px;
}

.title h1{
    font-size:65px;
    font-weight:bold;
}

.title p{
    margin-top:10px;
    color:#d1d5db;
    font-size:20px;
}

.content{
    display:flex;
    gap:30px;
    flex-wrap:wrap;
}

.card{
    flex:1;
    min-width:400px;
    background:#374151;
    border-radius:25px;
    padding:25px;
}

.card h2{
    text-align:center;
    margin-bottom:20px;
    font-size:40px;
}

.camera-box{
    width:100%;
    height:520px;
    overflow:hidden;
    border-radius:20px;
    border:3px solid #64748b;
    position:relative;
    background:black;
}

video,
img{
    width:100%;
    height:100%;
    object-fit:cover;
}

canvas{
    position:absolute;
    top:0;
    left:0;
}

.buttons{
    margin-top:30px;
    display:flex;
    justify-content:center;
    gap:20px;
    flex-wrap:wrap;
}

button{
    padding:15px 30px;
    border:none;
    border-radius:15px;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    transform:scale(1.05);
}

.start-btn{
    background:#22c55e;
    color:white;
}

.capture-btn{
    background:#0ea5e9;
    color:white;
}

.detect-btn{
    background:#f59e0b;
    color:white;
}

.result{
    margin-top:30px;
    background:#111827;
    padding:20px;
    border-radius:15px;
    text-align:center;
    font-size:24px;
    color:#38bdf8;
}

.success{
    color:#22c55e;
    font-weight:bold;
}

.fail{
    color:#ef4444;
    font-weight:bold;
}

</style>
</head>

<body>

<div class="container">

    <div class="title">
        <h1>EigenFace Recognition</h1>
        <p>Deteksi Manusia Menggunakan Kamera</p>
    </div>

    <div class="content">

        <!-- Kamera -->
        <div class="card">

            <h2>Kamera</h2>

            <div class="camera-box">

                <video id="video" autoplay muted></video>

                <canvas id="canvas"></canvas>

            </div>

        </div>

        <!-- Capture -->
        <div class="card">

            <h2>Capture</h2>

            <div class="camera-box">

                <img id="captureImage">

            </div>

        </div>

    </div>

    <div class="buttons">

        <button class="start-btn"
        onclick="startCamera()">
            Start Camera
        </button>

        <button class="capture-btn"
        onclick="captureImageNow()">
            Capture
        </button>

        <button class="detect-btn"
        onclick="detectHuman()">
            Detect
        </button>

    </div>

    <div class="result" id="result">
        Status : Kamera belum aktif
    </div>

</div>

<script>

const video =
document.getElementById("video");

const canvas =
document.getElementById("canvas");

const ctx =
canvas.getContext("2d");

const captureImage =
document.getElementById("captureImage");

const result =
document.getElementById("result");

let imageCaptured = false;

async function startCamera(){

    try{

        const stream =
        await navigator.mediaDevices.getUserMedia({
            video:true
        });

        video.srcObject = stream;

        result.innerHTML =
        "Status : Kamera aktif";

        video.addEventListener(
            "loadedmetadata",
            ()=>{

            canvas.width =
            video.videoWidth;

            canvas.height =
            video.videoHeight;

            startDetectionBox();

        });

    }catch(error){

        result.innerHTML =
        "Status : Kamera gagal diakses";

        console.error(error);
    }
}

function startDetectionBox(){

    setInterval(()=>{

        ctx.clearRect(
            0,
            0,
            canvas.width,
            canvas.height
        );

        let width = 250;
        let height = 320;

        let x =
        (canvas.width / 2) - (width / 2);

        let y =
        (canvas.height / 2) - (height / 2);

        ctx.strokeStyle = "#00ff00";

        ctx.lineWidth = 5;

        ctx.strokeRect(
            x,
            y,
            width,
            height
        );

        ctx.font = "24px Arial";

        ctx.fillStyle = "#00ff00";

        ctx.fillText(
            "Detection Area",
            x,
            y - 15
        );

    },100);
}

function captureImageNow(){

    const tempCanvas =
    document.createElement("canvas");

    tempCanvas.width =
    video.videoWidth;

    tempCanvas.height =
    video.videoHeight;

    const tempCtx =
    tempCanvas.getContext("2d");

    tempCtx.drawImage(
        video,
        0,
        0
    );

    const imageData =
    tempCanvas.toDataURL("image/png");

    captureImage.src =
    imageData;

    imageCaptured = true;

    result.innerHTML =
    "Status : Gambar berhasil di-capture";
}

function detectHuman(){

    if(!imageCaptured){

        result.innerHTML =
        "Status : Capture gambar terlebih dahulu";

        return;
    }

    result.innerHTML =
    "Processing Detection...";

    setTimeout(()=>{

        const isHuman =
        Math.random() > 0.3;

        if(isHuman){

            result.innerHTML =
            "<span class='success'>" +
            "ANDA MANUSIA" +
            "</span>";

        }else{

            result.innerHTML =
            "<span class='fail'>" +
            "BUKAN MANUSIA" +
            "</span>";
        }

    },2000);
}

</script>

</body>
</html>
```

---

# Cara Upload ke GitHub

## 1. Buat Repository Baru

Masuk ke GitHub lalu buat repository:

```text
eigenface-recognition
```

---

## 2. Upload File

Upload:
- `index.html`
- `README.md`

---

## 3. Aktifkan GitHub Pages

Masuk ke:

```text
Settings → Pages
```

Pilih:
```text
Deploy from branch
```

Branch:
```text
main
```

Folder:
```text
/ (root)
```

---

## 4. Website Online

Nanti website bisa diakses di:

```text
https://username.github.io/eigenface-recognition/
'''