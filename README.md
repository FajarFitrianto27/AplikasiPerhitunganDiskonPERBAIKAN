# AplikasiPerhitunganDiskonPERBAIKAN
 Berikut adalah **README** yang sudah dilengkapi dengan kode program untuk proyek **Perhitungan Diskon** menggunakan **JFrame Form** di NetBeans.

---

# **📌 Perhitungan Diskon - Java JFrame Form**

## **📜 Deskripsi Proyek**
Aplikasi **Perhitungan Diskon** ini dibuat menggunakan **Java JFrame Form** di **NetBeans**.  
Aplikasi ini memungkinkan pengguna untuk:  
✅ Memasukkan harga asli suatu barang  
✅ Memilih diskon menggunakan **JSlider** atau **ComboBox**  
✅ Memasukkan kode kupon untuk mendapatkan tambahan diskon  
✅ Menampilkan harga akhir setelah diskon  
✅ Menyimpan **riwayat perhitungan**  

---

## **📦 Fitur Utama**
### 1️⃣ **Perhitungan Diskon**  
- Pengguna dapat memasukkan harga asli dan memilih persentase diskon dengan **JSlider** atau **ComboBox**  
- Sistem akan menghitung harga akhir setelah diskon  

### 2️⃣ **Kode Kupon Diskon**  
- Pengguna dapat memasukkan **kode kupon tambahan** di **TextField**  
- Kupon yang tersedia:  
  - `"DISKON10"` → tambahan diskon **10%**  
  - `"DISKON20"` → tambahan diskon **20%**  
- **Maksimal total diskon yang bisa didapatkan adalah 50%**  

### 3️⃣ **Riwayat Perhitungan**  
- Setiap perhitungan akan **disimpan di JTextArea**, sehingga pengguna dapat melihat hasil sebelumnya  



---

## **📥 Instalasi dan Penggunaan**
### **🔹 1. Persyaratan**  
- **JDK 8+**  
- **NetBeans IDE atau IDE lain yang mendukung Java GUI**  

### **🔹 2. Cara Menjalankan**  
1. **Buka proyek di NetBeans**  
2. **Jalankan file `PerhitunganDiskonForm.java`**  
3. **Masukkan harga asli** pada `TextField`  
4. **Pilih diskon** dengan **JSlider** atau **ComboBox**  
5. (Opsional) Masukkan **Kode Kupon** dan tekan tombol `"Gunakan Kupon"`  
6. Tekan tombol **"HITUNG"** untuk mendapatkan hasil  
7. Riwayat perhitungan akan muncul di **JTextArea**  
8. Tekan tombol **"RESET"** untuk menghapus semua input dan hasil  

---

## **💻 Kode Program**
Berikut adalah kode program untuk **Perhitungan Diskon**:

```java
import javax.swing.JOptionPane;

public class PerhitunganDiskonForm extends javax.swing.JFrame {
    private int tambahanDiskon = 0;

    public PerhitunganDiskonForm() {
        initComponents();
        sliderDiskon.addChangeListener(evt -> sliderDiskonStateChanged(evt));
    }

   

    private void jButtonHitungActionPerformed(java.awt.event.ActionEvent evt) {                                             
        try {
            double hargaAsli = Double.parseDouble(jTextField1.getText());
            int persentaseDiskon = sliderDiskon.getValue();
            
            int totalDiskon = persentaseDiskon + tambahanDiskon;
            if (totalDiskon > 50) totalDiskon = 50;
            
            double penghematan = hargaAsli * (totalDiskon / 100.0);
            double hargaAkhir = hargaAsli - penghematan;

            jTextField2.setText(String.format("%.2f", hargaAkhir));
            lblPenghematan.setText("Penghematan: " + String.format("%.2f", penghematan));

            String riwayat = "Harga Asli: " + hargaAsli + "\n" +
                             "Diskon: " + persentaseDiskon + "% + Kupon: " + tambahanDiskon + "%\n" +
                             "Harga Akhir: " + hargaAkhir + "\n" +
                             "---------------------\n";
            riwayatTextArea.append(riwayat);
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Masukkan angka yang valid!", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    private void jButtonResetActionPerformed(java.awt.event.ActionEvent evt) {
        jTextField1.setText("");
        jTextField2.setText("");
        kuponTextField.setText("");
        sliderDiskon.setValue(0);
        lblPenghematan.setText("");
        riwayatTextArea.setText("");
        tambahanDiskon = 0;
        JOptionPane.showMessageDialog(this, "Data telah direset!", "Reset", JOptionPane.INFORMATION_MESSAGE);
    }

    private void sliderDiskonStateChanged(javax.swing.event.ChangeEvent evt) {
        labelDiskon.setText("Diskon: " + sliderDiskon.getValue() + "%");
    }

    private void buttonGunakanKuponActionPerformed(java.awt.event.ActionEvent evt) {
        String kodeKupon = kuponTextField.getText().trim().toUpperCase();
        
        if (kodeKupon.equals("DISKON10")) {
            tambahanDiskon = 10;
        } else if (kodeKupon.equals("DISKON20")) {
            tambahanDiskon = 20;
        } else {
            tambahanDiskon = 0;
            JOptionPane.showMessageDialog(this, "Kupon tidak valid!", "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }

        JOptionPane.showMessageDialog(this, "Kupon diterima! Diskon tambahan: " + tambahanDiskon + "%");
    }

    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(() -> new PerhitunganDiskonForm().setVisible(true));
    }
}
```

