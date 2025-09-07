Dokumentasi Praktikum

Lifecycle Events with Java Code

1. Pendahuluan

Pada praktikum ini dipelajari mengenai activity lifecycle pada Android. Lifecycle adalah serangkaian metode yang dijalankan oleh sistem Android untuk mengatur siklus hidup sebuah activity, mulai dari dibuat, tampil di layar, masuk ke latar belakang, hingga dihentikan. Memahami lifecycle sangat penting bagi pengembang aplikasi karena dapat menentukan perilaku aplikasi sesuai kondisi perangkat dan interaksi pengguna.

2. Alat dan Bahan

Android Studio (versi terbaru)

JDK (Java Development Kit)

Ponsel Android dengan USB debugging aktif / Android Emulator

Kabel USB (jika menggunakan perangkat fisik)

3. Langkah Praktikum

Membuat project baru dengan nama LifecycleEventsNanda menggunakan bahasa Java.

Menambahkan kode Log.d("MainActivity", "onCreate"); pada method onCreate().

Melakukan refactor pada string "MainActivity" menjadi konstanta LOG_TAG.

Menambahkan metode onStart(), onResume(), onPause(), dan onStop(), masing-masing berisi Log.d(LOG_TAG, "...").

Menjalankan aplikasi dan mengamati keluaran log pada Logcat.

Menguji perbedaan perilaku aplikasi ketika ditutup menggunakan tombol Back dan tombol Home.

Menambahkan konfigurasi android:configChanges="orientation|screenSize" pada file AndroidManifest.xml.

Menambahkan method onConfigurationChanged() untuk menangani perubahan orientasi (portrait ↔ landscape).

Menjalankan kembali aplikasi dan mengamati perubahan log saat perangkat dirotasi.

4. Hasil Pengamatan

Saat aplikasi pertama kali dijalankan, urutan log yang muncul adalah: onCreate → onStart → onResume.

Saat aplikasi ditutup dengan tombol Back, log yang muncul adalah onPause → onStop. Ketika dibuka kembali, sistem memanggil ulang onCreate.

Saat aplikasi dipindahkan ke latar belakang dengan tombol Home, log yang muncul adalah onPause → onStop. Namun ketika dibuka kembali, sistem hanya memanggil onStart → onResume, tanpa melalui onCreate.

Saat rotasi dilakukan tanpa konfigurasi tambahan, activity direstart sehingga urutan onCreate dipanggil ulang.

Setelah menambahkan configChanges, rotasi layar tidak lagi memanggil ulang lifecycle, tetapi men-trigger method onConfigurationChanged() yang menampilkan log "Dalam kondisi portrait" atau "Dalam kondisi landscape".

5. Pembahasan

Perbedaan yang muncul saat aplikasi ditutup dengan tombol Back dan Home menunjukkan bagaimana sistem Android mengelola memori. Tombol Back menandakan aplikasi diakhiri sehingga memori dilepas, sementara tombol Home hanya memindahkan aplikasi ke latar belakang sehingga memori tetap tersimpan.

Konfigurasi configChanges memberikan kendali lebih besar kepada pengembang untuk menangani perubahan orientasi. Tanpa konfigurasi ini, sistem akan merestart activity sehingga semua data sementara hilang. Dengan konfigurasi tersebut, aplikasi dapat mempertahankan state dan hanya merespons perubahan orientasi melalui onConfigurationChanged().

6. Kesimpulan

Melalui praktikum ini dapat disimpulkan bahwa:

Activity lifecycle pada Android terdiri atas beberapa tahapan penting seperti onCreate, onStart, onResume, onPause, dan onStop.

Tombol Back menghentikan aplikasi sepenuhnya, sedangkan tombol Home hanya memindahkan aplikasi ke latar belakang.

Perubahan orientasi secara bawaan menyebabkan activity direstart, namun dapat ditangani dengan menambahkan konfigurasi configChanges.

Pemahaman lifecycle membantu pengembang dalam mengelola state aplikasi dan mengoptimalkan pengalaman pengguna.
