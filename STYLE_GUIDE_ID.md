# Panduan Gaya Penulisan Kode Nginr

Dokumen ini memberikan panduan untuk menulis kode Nginr yang bersih, mudah dipelihara, dan konsisten. nginr adalah preprosesor ringan untuk Python yang menawarkan gaya sintaks alternatif.

## Daftar Isi
1. [Fungsi](#fungsi)
2. [Tipe Data](#tipe-data)
3. [Struktur Program](#struktur-program)
4. [Konvensi Penamaan](#konvensi-penamaan)
5. [Contoh Program](#contoh-program)
6. [Pengecualian dan Penanganan Error](#pengecualian-dan-penanganan-error)
7. [Dokumentasi](#dokumentasi)

## Fungsi

### Deklarasi Fungsi
Gunakan kata kunci `fn` untuk mendeklarasikan fungsi. Selalu sertakan anotasi tipe untuk parameter dan nilai kembalian.

```python
# Benar
fn tambah(a: int, b: int) -> int:
    return a + b

# Salah
def tambah(a, b):
    return a + b
```

### Fungsi Utama
Setiap program yg ada di nginr harus memiliki fungsi `main()` sebagai entry point.

```python
fn main() -> None:
    print("Halo, Dunia!")

if __name__ == "__main__":
    main()
```

### Nilai Default Parameter
Gunakan tanda sama dengan (`=`) untuk menentukan nilai default parameter.

```python
fn sapa(nama: str, salam: str = "Halo") -> str:
    return f"{salam}, {nama}!"
```

### Fungsi dengan Banyak Parameter
Untuk fungsi dengan banyak parameter, tulis setiap parameter dalam baris terpisah.

```python
fn buat_pengguna(
    nama: str,
    email: str,
    umur: int,
    aktif: bool = True,
    alamat: Optional[str] = None
) -> Dict[str, Any]:
    # Implementasi fungsi
    pass
```

## Tipe Data

### Anotasi Tipe
Selalu gunakan anotasi tipe untuk:
- Parameter fungsi
- Nilai kembalian fungsi
- Variabel (opsional, tapi sangat disarankan)

```python
# Benar
fn sapa(nama: str) -> str:
    return f"Halo, {nama}!"

# Opsional (tapi disarankan)
angka: int = 42
```

### Tipe Dasar
- `int`: Bilangan bulat
- `float`: Bilangan desimal
- `bool`: Nilai boolean (`True` atau `False`)
- `str`: Teks
- `None`: Nilai kosong

### Tipe Koleksi
- `List[tipe]`: Daftar nilai
- `Dict[kunci, nilai]`: Kamus
- `Set[tipe]`: Himpunan
- `Tuple[tipe1, tipe2, ...]`: Tuple

### Tipe Opsional
Gunakan `Optional[tipe]` untuk nilai yang bisa `None`.

```python
fn cari_anggota(id: int) -> Optional[Dict[str, Any]]:
    # Mengembalikan None jika tidak ditemukan
    pass
```

## Struktur Program

### Impor Modul
Letakkan semua pernyataan impor di bagian atas file.

```python
import math
from typing import List, Dict

# Kode lain mengikuti di sini
```

### Urutan Impor
1. Impor standar library
2. Impor pihak ketiga
3. Impor lokal

```python
# Impor standar
import os
import sys
from typing import List, Dict

# Impor pihak ketiga
import requests
from flask import Flask

# Impor lokal
from . import utils
from .models import User
```

### Spasi dan Indentasi
- Gunakan 4 spasi untuk indentasi
- Beri 2 baris kosong di antara definisi fungsi
- Gunakan 1 baris kosong di antara bagian logika yang berbeda

```python
# Benar
fn fungsi_satu() -> None:
    print("Fungsi satu")


fn fungsi_dua() -> None:
    print("Fungsi dua")
    
    # Baris kosong memisahkan bagian logika
    if kondisi:
        lakukan_sesuatu()
```

## Konvensi Penamaan

### Fungsi dan Variabel
Gunakan `snake_case` untuk nama fungsi dan variabel.

```python
# Benar
fn hitung_rata_rata(daftar_angka: List[float]) -> float:
    total: float = sum(daftar_angka)
    return total / len(daftar_angka)
```

### Konstanta
Gunakan `UPPER_SNAKE_CASE` untuk konstanta.

```python
PI: float = 3.14159
MAX_RETRIES: int = 3
```

### Kelas
Gunakan `PascalCase` untuk nama kelas.

```python
class ManajemenPengguna:
    fn __init__(self) -> None:
        self.pengguna: List[Dict[str, Any]] = []
```

## Pengecualian dan Penanganan Error

### Melempar Pengecualian
Gunakan pengecualian bawaan Python atau buat kelas pengecualian kustom.

```python
class KesalahanValidasi(Exception):
    """Dilempar ketika validasi gagal."""
    pass

fn validasi_umur(umur: int) -> None:
    if umur < 0:
        raise ValueError("Umur tidak boleh negatif")
    if umur < 18:
        raise KesalahanValidasi("Minimal umur 18 tahun")
```

### Menangani Pengecualian
Tangkap pengecualian spesifik terlebih dahulu.

```python
try:
    hasil = bagi(10, 0)
except ValueError as e:
    print(f"Error: {e}")
except ZeroDivisionError:
    print("Tidak bisa membagi dengan nol")
except Exception as e:
    print(f"Terjadi kesalahan: {e}")
else:
    print(f"Hasil: {hasil}")
finally:
    print("Proses selesai")
```

## Dokumentasi

### Docstring
Gunakan docstring untuk mendokumentasikan modul, kelas, dan fungsi.

```python
fn hitung_rata_rata(angka: List[float]) -> float:
    """
    Menghitung rata-rata dari daftar angka.
    
    Args:
        angka: Daftar angka yang akan dihitung rata-ratanya
        
    Returns:
        Rata-rata dari angka-angka yang diberikan
        
    Raises:
        ValueError: Jika daftar angka kosong
    """
    if not angka:
        raise ValueError("Daftar angka tidak boleh kosong")
    return sum(angka) / len(angka)
```

### Komentar
Gunakan komentar untuk menjelaskan "mengapa" bukan "apa".

```python
# Tidak perlu:
x = x + 1  # Menambahkan 1 ke x

# Lebih baik:
x = x + 1  # Kompensasi untuk indeks 0-based
```

## Contoh Program

### Program Sederhana
```python
# program_sederhana.xr

fn sapa(nama: str) -> str:
    """Mengembalikan salam untuk nama yang diberikan."""
    return f"Halo, {nama}! Selamat datang di Nginr!"


fn main() -> None:
    nama: str = input("Siapa namamu? ")
    pesan: str = sapa(nama)
    print(pesan)


if __name__ == "__main__":
    main()
```

### Program dengan Kelas
```python
# manajemen_pengguna.xr

from typing import List, Dict, Optional
from dataclasses import dataclass


@dataclass
class Pengguna:
    """Kelas untuk merepresentasikan data pengguna."""
    id: int
    nama: str
    email: str
    aktif: bool = True


class ManajemenPengguna:
    """Kelas untuk mengelola data pengguna."""
    
    fn __init__(self) -> None:
        self.pengguna: Dict[int, Pengguna] = {}
        self._pengguna_berikutnya: int = 1
    
    fn tambah_pengguna(self, nama: str, email: str) -> Pengguna:
        """Menambahkan pengguna baru."""
        if not self._validasi_email(email):
            raise ValueError("Format email tidak valid")
            
        pengguna = Pengguna(
            id=self._pengguna_berikutnya,
            nama=nama,
            email=email
        )
        
        self.pengguna[pengguna.id] = pengguna
        self._pengguna_berikutnya += 1
        return pengguna
    
    fn dapatkan_pengguna(self, id_pengguna: int) -> Optional[Pengguna]:
        """Mendapatkan pengguna berdasarkan ID."""
        return self.pengguna.get(id_pengguna)
    
    fn aktifkan_pengguna(self, id_pengguna: int) -> bool:
        """Mengaktifkan pengguna yang dinonaktifkan."""
        pengguna = self.dapatkan_pengguna(id_pengguna)
        if not pengguna:
            return False
            
        if pengguna.aktif:
            return False
            
        pengguna.aktif = True
        return True
    
    fn _validasi_email(self, email: str) -> bool:
        """Memvalidasi format email."""
        return "@" in email and "." in email.split("@")[1]


fn main() -> None:
    # Inisialisasi manajer pengguna
    manajer = ManajemenPengguna()
    
    # Tambah beberapa pengguna
    try:
        pengguna1 = manajer.tambah_pengguna("Budi Santoso", "budi@contoh.com")
        pengguna2 = manajer.tambah_pengguna("Ani Lestari", "ani@contoh.com")
        
        print(f"Berhasil menambahkan pengguna: {pengguna1.nama}")
        print(f"Berhasil menambahkan pengguna: {pengguna2.nama}")
        
        # Cari pengguna
        id_cari = 1
        pengguna = manajer.dapatkan_pengguna(id_cari)
        if pengguna:
            status = "aktif" if pengguna.aktif else "tidak aktif"
            print(f"Pengguna ditemukan: {pengguna.nama} (Status: {status})")
        else:
            print(f"Tidak menemukan pengguna dengan ID {id_cari}")
            
    except ValueError as e:
        print(f"Error: {e}")


if __name__ == "__main__":
    main()
```

### Program dengan Error Handling
```python
# penanganan_error.xr

fn baca_angka(prompt: str) -> float:
    """Membaca input angka dari pengguna dengan validasi."""
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Error: Masukan harus berupa angka. Silakan coba lagi.")


fn bagi(pembilang: float, penyebut: float) -> float:
    """Membagi dua angka dengan penanganan error."""
    if penyebut == 0:
        raise ValueError("Tidak bisa membagi dengan nol")
    return pembilang / penyebut


fn main() -> None:
    print("=== Kalkulator Pembagian ===\n")
    
    try:
        # Baca input dari pengguna
        angka1 = baca_angka("Masukkan angka pertama: ")
        angka2 = baca_angka("Masukkan angka kedua: ")
        
        # Lakukan pembagian
        hasil = bagi(angka1, angka2)
        print(f"\nHasil {angka1} / {angka2} = {hasil:.2f}")
        
    except KeyboardInterrupt:
        print("\n\nOperasi dibatalkan oleh pengguna.")
    except Exception as e:
        print(f"\nTerjadi kesalahan: {e}")
    finally:
        print("\nTerima kasih telah menggunakan kalkulator pembagian.")


if __name__ == "__main__":
    main()
```

---

Dokumen ini akan terus diperbarui seiring dengan perkembangan bahasa Nginr. Silakan berkontribusi dengan mengusulkan perubahan atau penambahan contoh program.
