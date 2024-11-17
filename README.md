# Aplikasi Penghitungan Hari  
Tugas 4 - Adrian Akhmad Firdaus (2210010491)

---

## Deskripsi

Aplikasi ini digunakan untuk menghitung jumlah hari dalam bulan tertentu pada tahun tertentu, serta menghitung selisih hari antara dua tanggal yang dipilih. Pengguna dapat memilih bulan melalui `JComboBox`, memasukkan tahun menggunakan `JSpinner`, dan memilih tanggal dengan `JCalendar`. Hasil berupa jumlah hari, hari pertama, dan hari terakhir dalam bulan ditampilkan pada antarmuka aplikasi.

---

## Fitur Aplikasi

1. **Perhitungan Jumlah Hari**:  
   - Menghitung jumlah hari dalam bulan tertentu berdasarkan input bulan dan tahun.  
   - Menampilkan informasi tambahan, yaitu hari pertama dan hari terakhir dari bulan tersebut.  
   - **Contoh Kode Implementasi**:  
     ```java
     private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {
         String namaBulan = cmbBulan.getSelectedItem().toString();
         int tahun = (int) spinnerTahun.getValue();
         int indexBulan = cmbBulan.getSelectedIndex() + 1;

         java.time.YearMonth ym = java.time.YearMonth.of(tahun, indexBulan);
         int hariDalamBulan = ym.lengthOfMonth();

         java.time.LocalDate hariPertama = ym.atDay(1);
         java.time.LocalDate hariTerakhir = ym.atEndOfMonth();

         String hariAwal = terjemahHari(hariPertama.getDayOfWeek());
         String hariAkhir = terjemahHari(hariTerakhir.getDayOfWeek());

         JOptionPane.showMessageDialog(this, 
             String.format("Jumlah Hari: %d\nHari Pertama: %s\nHari Terakhir: %s", 
             hariDalamBulan, hariAwal, hariAkhir)
         );
     }
     ```

2. **Menghitung Selisih Hari**:  
   - Menghitung jumlah hari antara dua tanggal yang dipilih pada dua `JCalendar`.  
   - **Contoh Kode Implementasi**:  
     ```java
     private void btnSelisihActionPerformed(java.awt.event.ActionEvent evt) {
         java.util.Date tglMulai = calenderTglAwal.getDate();
         java.util.Date tglAkhir = calenderTglAkihr.getDate();

         if (tglMulai != null && tglAkhir != null) {
             java.time.LocalDate mulai = tglMulai.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();
             java.time.LocalDate akhir = tglAkhir.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();

             long selisih = java.time.temporal.ChronoUnit.DAYS.between(mulai, akhir);
             JOptionPane.showMessageDialog(this, "Selisih Hari: " + Math.abs(selisih) + " hari");
         }
     }
     ```

---

## Komponen GUI

Aplikasi ini menggunakan komponen berikut:
- **JFrame**: Jendela utama aplikasi.  
- **JPanel**: Panel untuk menata elemen GUI.  
- **JLabel**: Label untuk input dan output informasi.  
- **JComboBox**: Memilih bulan.  
- **JSpinner**: Memasukkan tahun.  
- **JCalendar**: Memilih tanggal.  
- **JButton**: Tombol untuk menghitung jumlah hari dan selisih hari.  

---

## **Struktur Program**

### 1. **Komponen Utama**
   Aplikasi ini terdiri dari beberapa komponen utama yang bertanggung jawab untuk membangun antarmuka dan mengelola logika perhitungan:
   - **`JFrame`**: Jendela utama aplikasi yang mencakup semua komponen antarmuka.
   - **`JPanel`**: Digunakan untuk membagi antarmuka menjadi beberapa bagian logis:
     - **Panel Perhitungan Jumlah Hari**: Menghitung jumlah hari dalam bulan dan menampilkan hari pertama serta terakhir.
     - **Panel Perhitungan Selisih Hari**: Menghitung selisih antara dua tanggal yang dipilih.
   - **`JLabel`**: Menampilkan teks seperti label untuk input dan hasil.
   - **`JComboBox`**: Untuk memilih bulan dari daftar.
   - **`JSpinner`**: Untuk input tahun dengan batasan tertentu.
   - **`JCalendar`**: Untuk memilih tanggal pada kalender.
   - **`JButton`**: Tombol aksi untuk memproses perhitungan.

---

### 2. **Fungsi Utama**
   - **Menerjemahkan Nama Hari**:  
     Fungsi `terjemahHari` menerjemahkan nama hari dari bahasa Inggris ke bahasa Indonesia menggunakan `switch-case`.

     ```java
     private String terjemahHari(java.time.DayOfWeek hari) {
         switch (hari) {
             case MONDAY: return "Senin";
             case TUESDAY: return "Selasa";
             case WEDNESDAY: return "Rabu";
             case THURSDAY: return "Kamis";
             case FRIDAY: return "Jumat";
             case SATURDAY: return "Sabtu";
             case SUNDAY: return "Minggu";
             default: return "";
         }
     }
     ```

   - **Menghitung Jumlah Hari dalam Bulan**:  
     Tombol **Hitung Jumlah Hari** memproses input bulan dan tahun untuk menghitung jumlah hari, hari pertama, dan hari terakhir.

     ```java
     private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {
         String namaBulan = cmbBulan.getSelectedItem().toString();
         int tahun = (int) spinnerTahun.getValue();
         int indexBulan = cmbBulan.getSelectedIndex() + 1;

         java.time.YearMonth ym = java.time.YearMonth.of(tahun, indexBulan);
         int hariDalamBulan = ym.lengthOfMonth();

         java.time.LocalDate hariPertama = ym.atDay(1);
         java.time.LocalDate hariTerakhir = ym.atEndOfMonth();

         String hariAwal = terjemahHari(hariPertama.getDayOfWeek());
         String hariAkhir = terjemahHari(hariTerakhir.getDayOfWeek());

         JOptionPane.showMessageDialog(this, 
             String.format("Jumlah Hari: %d\nHari Pertama: %s\nHari Terakhir: %s", 
             hariDalamBulan, hariAwal, hariAkhir)
         );
     }
     ```

   - **Menghitung Selisih Hari**:  
     Tombol **Hitung Selisih Hari** menghitung perbedaan hari antara dua tanggal.

     ```java
     private void btnSelisihActionPerformed(java.awt.event.ActionEvent evt) {
         java.util.Date tglMulai = calenderTglAwal.getDate();
         java.util.Date tglAkhir = calenderTglAkihr.getDate();

         if (tglMulai != null && tglAkhir != null) {
             java.time.LocalDate mulai = tglMulai.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();
             java.time.LocalDate akhir = tglAkhir.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();

             long selisih = java.time.temporal.ChronoUnit.DAYS.between(mulai, akhir);
             JOptionPane.showMessageDialog(this, "Selisih Hari: " + Math.abs(selisih) + " hari");
         }
     }
     ```

   - **Sinkronisasi Kalender dan Input**:  
     Fungsi `sinkronkanComboBoxDanSpinner` dan `perbaruiKalender` menjaga agar input dari `JComboBox` dan `JSpinner` selalu konsisten dengan `JCalendar`.

---

### 3. **Tata Letak Antarmuka**
   - **GridBagLayout**: Digunakan untuk memberikan fleksibilitas dalam penempatan komponen GUI di dalam `JPanel`.
   - **BorderLayout**: Membagi area utama jendela menjadi beberapa bagian: `PAGE_START`, `PAGE_END`, `CENTER`, dll.

---

### 4. **Events**
   - **ActionListener**:  
     - `btnHitung` untuk menghitung jumlah hari dalam bulan.
     - `btnSelisih` untuk menghitung selisih hari antara dua tanggal.

   - **ChangeListener**:  
     - `spinnerTahun` untuk memperbarui kalender saat tahun berubah.

   - **ItemListener**:  
     - `cmbBulan` untuk memperbarui kalender saat bulan berubah.

   - **PropertyChangeListener**:  
     - `calenderPilihTgl` untuk memperbarui input bulan dan tahun berdasarkan pilihan tanggal.
  

---

## Cara Menjalankan Aplikasi

1. Clone atau unduh repositori ini.  
2. Buka proyek di NetBeans IDE 8.2.  
3. Jalankan file utama `AplikasiPenghitunganHari.java`.  
4. Pilih bulan, masukkan tahun, dan tekan tombol **Hitung Jumlah Hari** untuk melihat hasilnya.  
5. Pilih dua tanggal dan tekan tombol **Hitung Selisih Hari** untuk mengetahui perbedaan hari.

## Tampilan Aplikasi Saat Dijalankan
![image](https://github.com/user-attachments/assets/9e39213a-ea83-481a-9760-4a35c108042e)

---

## Indikator Penilaian

| No  | Komponen           | Persentase |
|-----|---------------------|------------|
| 1   | Komponen GUI       | 20%        |
| 2   | Logika Program     | 20%        |
| 3   | Events             | 15%        |
| 4   | Kesesuaian UI      | 15%        |
| 5   | Memenuhi Variasi   | 30%        |
| **TOTAL** |               | **100%**   |

---

## Pembuat

- **Nama**: Adrian Akhmad Firdaus  
- **NPM**: 2210010491  
- **Kelas**: 5A Reguler Pagi  
- **Tugas**: Tugas 4 - Aplikasi Penghitungan Hari  
- **Fakultas**: Fakultas Teknologi Informasi (FTI)  
- **Universitas**: Universitas Islam Kalimantan Muhammad Arsyad Al Banjari Banjarmasin  

---
