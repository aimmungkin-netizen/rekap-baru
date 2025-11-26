<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Rekap Harian</title>
<style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    h1 { text-align: center; }
    .row { display: flex; align-items: center; margin-bottom: 8px; }
    .label { width: 30px; font-weight: bold; }
    textarea {
        width: 260px;
        height: 30px;
        resize: none;
        font-size: 14px;
    }
    button { margin-left: 5px; padding: 4px 8px; }
</style>
</head>
<body>

<h1>Rekap Harian</h1>

<select id="pasaranSelect">
    <option value="">-- Pilih Pasaran --</option>
    <option>TOTO WUHAN</option>
    <option>OREGON</option>
    <option>KINGSTON</option>
    <option>CAMBODIA</option>
    <option>SYDNEY</option>
    <option>SINGAPORE</option>
    <option>TAIWAN</option>
    <option>HONGKONG</option>
</select>

<div id="container" style="margin-top:20px;"></div>

<script>
const letters = "ABCDEFGHIJKLMNOPQRST".split("");

function loadRows(pasaran) {
    const container = document.getElementById("container");
    container.innerHTML = "";

    if (!pasaran) return;

    letters.forEach(letter => {
        const row = document.createElement("div");
        row.className = "row";

        const label = document.createElement("div");
        label.className = "label";
        label.textContent = letter;

        const textarea = document.createElement("textarea");
        textarea.maxLength = 50;
        
        // Load data dari localStorage
        const key = pasaran + "_" + letter;
        textarea.value = localStorage.getItem(key) || "";

        const btnSave = document.createElement("button");
        btnSave.textContent = "Simpan";
        btnSave.onclick = () => {
            localStorage.setItem(key, textarea.value);
            alert("Disimpan ✔");
        };

        const btnCopy = document.createElement("button");
        btnCopy.textContent = "Salin";
        btnCopy.onclick = () => {
            navigator.clipboard.writeText(textarea.value);
            alert("Disalin ✔");
        };

        const btnDelete = document.createElement("button");
        btnDelete.textContent = "Hapus";
        btnDelete.onclick = () => {
            textarea.value = "";
            localStorage.removeItem(key);
        };

        row.appendChild(label);
        row.appendChild(textarea);
        row.appendChild(btnSave);
        row.appendChild(btnCopy);
        row.appendChild(btnDelete);

        container.appendChild(row);
    });
}

document.getElementById("pasaranSelect").addEventListener("change", function() {
    loadRows(this.value);
});
</script>

</body>
</html>
