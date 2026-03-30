# Laporan Programming Assignment 1: Basic C++

# REPORT.md

## Program Perhitungan Umur dan Hari (C++)

---

## Deskripsi

Program ini dibuat menggunakan bahasa **C++** untuk menghitung:

* Umur dalam **tahun**
* Umur dalam **bulan**
* Hari dari tanggal lahir (**Senin – Minggu**)

Program menerima input berupa tanggal lahir dengan format:

```
DD/MM/YYYY
```

---

## Cara Kerja Program

Program memanfaatkan library:

* `<ctime>` → untuk mengambil waktu saat ini
* `<sstream>` → untuk parsing input string
* `struct tm` → untuk menyimpan data tanggal

---

## Penjelasan Fungsi

### 1. `yearsOld`

Menghitung umur dalam tahun.

**Algoritma:**

* Hitung selisih tahun sekarang dan tahun lahir
* Jika ulang tahun belum terjadi tahun ini → kurangi 1

---

### 2. `monthsOld`

Menghitung umur dalam bulan.

**Algoritma:**

* Hitung total bulan dari selisih tahun
* Tambahkan selisih bulan
* Jika tanggal sekarang < tanggal lahir → kurangi 1 bulan

---

### 3. `dayOfDate`

Menentukan hari dari tanggal lahir.

**Algoritma:**

* Gunakan `mktime()` untuk normalisasi tanggal
* Ambil nilai `tm_wday`
* Konversi ke nama hari

---

## Implementasi Kode

```cpp
int yearsOld(tm* inputTgl, tm* currentTgl)
{
    int year = currentTgl->tm_year - inputTgl->tm_year;

    if (currentTgl->tm_mon < inputTgl->tm_mon ||
       (currentTgl->tm_mon == inputTgl->tm_mon && currentTgl->tm_mday < inputTgl->tm_mday))
    {
        year--;
    }

    return year;
}

int monthsOld(tm* inputTgl, tm* currentTgl)
{
    int months = (currentTgl->tm_year - inputTgl->tm_year) * 12;
    months += (currentTgl->tm_mon - inputTgl->tm_mon);

    if (currentTgl->tm_mday < inputTgl->tm_mday)
    {
        months--;
    }

    return months;
}

string dayOfDate(tm* inputTgl)
{
    mktime(inputTgl);

    string days[] = {
        "Minggu", "Senin", "Selasa", "Rabu",
        "Kamis", "Jumat", "Sabtu"
    };

    return days[inputTgl->tm_wday];
}
```

---

## Contoh 

### Input

```
22/08/2006
```

### Output

```
19 235 Selasa
```

---

## Catatan Penting

* `tm_year` dihitung dari tahun 1900
* `tm_mon` dimulai dari 0 (Januari = 0)
* Fungsi `mktime()` wajib digunakan agar hari dapat dihitung

---

## Kesimpulan

Program ini berhasil:

* Menghitung umur dalam tahun dan bulan secara akurat
* Menentukan hari dari tanggal lahir
* Menggunakan struktur waktu (`tm`) dalam C++ dengan benar

Program ini dapat dikembangkan lebih lanjut untuk fitur manipulasi tanggal lainnya.

---
