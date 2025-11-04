# Praktikum 7: Mengelola Data dengan Room dan Compose (To-Do List)
Nama: Hanidura Ayatulloh
NIM: 225150207111005

---

## TUGAS 2: Menambahkan Fungsionalitas Mengubah Nama Tugas

### 🎯 Tujuan
Mengimplementasikan operasi **UPDATE** pada Room Database untuk mengubah judul (nama) tugas yang sudah ada di dalam daftar. Fungsionalitas ini diakses melalui interaksi UI berupa **tekan lama** (*Long Click*) pada item tugas.

### 💡 Pendekatan Implementasi
1.  **ViewModel Logic:** Menambahkan fungsi `updateTaskTitle` di `TaskViewModel.kt` yang memanggil `repository.update()` dengan data `Task` yang judulnya telah diperbarui.
2.  **UI Interaction:** Mengganti *modifier* `.clickable` pada `TaskItem` menjadi **`.combinedClickable`** untuk mendeteksi aksi **`onLongClick`**.
3.  **Dialog Input:** Menampilkan `AlertDialog` (`EditTaskDialog`) saat `onLongClick` terdeteksi, memungkinkan pengguna memasukkan judul tugas yang baru.

### ⚙️ Source Code Modifikasi (Inti Perubahan)

#### 1. TaskViewModel.kt (Fungsi Update Judul)

Fungsi baru ini bertanggung jawab untuk membuat salinan objek `Task` dengan judul yang diperbarui dan meluncurkan *coroutine* untuk menyimpan perubahan di database.

```kotlin
// Di dalam class TaskViewModel

fun updateTaskTitle(task: Task, newTitle: String) {
    // Membuat salinan tugas dengan judul yang baru. Status isCompleted tetap.
    val updatedTask = task.copy(title = newTitle)
    
    viewModelScope.launch {
        repository.update(updatedTask) // Memanggil update di repository
    }
}
