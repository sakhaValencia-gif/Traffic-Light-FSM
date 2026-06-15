Laporan Perancangan Finite State Machine (FSM) Lampu Lalu Lintas

Farell Edward Surya muler 

M Sakha Valencia Widianto 

Gilbert Sande Pabida 

LInk video: https://www.youtube.com/watch?v=GB4YWVHrWwE

1. Asumsi Sistem dan Siklus Transisi
Sistem ini dirancang untuk mengatur persimpangan empat arah dengan asumsi:
- Arah Utara dan Selatan bergerak bersamaan (disatukan sebagai **US**).
- Arah Timur dan Barat bergerak bersamaan (disatukan sebagai **TB**).
- Untuk mencegah tabrakan, arah US dan TB tidak boleh mendapatkan lampu hijau atau kuning di waktu yang bersamaan.

Sistem terdiri dari 4 status (State) yang berputar secara berurutan berkat dorongan sinyal Clock:
- **S0 (State 0):** Lampu Hijau US menyala, Lampu Merah TB menyala. (Utara-Selatan jalan, Timur-Barat berhenti).
- **S1 (State 1):** Lampu Kuning US menyala, Lampu Merah TB menyala. (Utara-Selatan siap-siap berhenti).
- **S2 (State 2):** Lampu Merah US menyala, Lampu Hijau TB menyala. (Utara-Selatan berhenti, Timur-Barat jalan).
- **S3 (State 3):** Lampu Merah US menyala, Lampu Kuning TB menyala. (Timur-Barat siap-siap berhenti).
- *Kembali lagi ke S0.*

2. Tabel Kebenaran (Truth Table)
Dua buah D Flip-Flop (FF1 dan FF0) digunakan sebagai memori untuk menyimpan 4 state (00, 01, 10, 11). Berikut adalah tabel kebenaran untuk logika Next State (D1, D0) dan Output (Lampu LED):

| Q1 (FF1) | Q0 (FF0) | D1 (Next) | D0 (Next) | Merah US | Kuning US | Hijau US | Merah TB | Kuning TB | Hijau TB |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 |
| 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |

3. Persamaan Logika (Boolean Expression)
Berdasarkan tabel kebenaran di atas, rancangan kabel pada Logisim disusun menggunakan persamaan gerbang logika murni (AND, NOT, XOR) berikut:

**Logika Transisi Memori (Input D Flip-Flop):**
- `D1 = Q1 XOR Q0`
- `D0 = NOT Q0`

**Logika Output Lampu (Utara-Selatan):**
- `Merah US = Q1`
- `Kuning US = NOT Q1 AND Q0`
- `Hijau US = NOT Q1 AND NOT Q0`

**Logika Output Lampu (Timur-Barat):**
- `Merah TB = NOT Q1`
- `Kuning TB = Q1 AND Q0`
- `Hijau TB = Q1 AND NOT Q0`
4. Kesimpulan
Implementasi FSM yang dirakit secara manual menggunakan kombinasi D Flip-Flop dan gerbang logika dasar ini telah berhasil mensimulasikan sistem lampu lalu lintas dengan akurat. Penggunaan sinyal Clock yang sinkron pada kedua Flip-Flop memastikan perpindahan state (dari 00 ke 11) berjalan konstan dan mencegah terjadinya kondisi eror di mana lampu yang salah menyala bersamaan.
