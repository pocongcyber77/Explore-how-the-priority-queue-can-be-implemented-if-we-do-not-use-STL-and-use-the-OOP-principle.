# Priority Queue Mahasiswa (Tanpa STL) - C++ dan OOP

Pendahuluan:
----
Priority Queue adalah struktur data di mana elemen dengan prioritas tertinggi akan diproses lebih dahulu.
Dalam kehidupan nyata, ini bisa digunakan untuk sistem antrean pelayanan mahasiswa berdasarkan prioritas,
misalnya prioritas berdasarkan IPK atau tingkat urgensi kebutuhan layanan.
----
Studi Kasus Nyata: Sistem Layanan Akademik Mahasiswa

Misalnya, mahasiswa datang ke layanan akademik. Mereka dilayani berdasarkan prioritas:
- Mahasiswa tingkat akhir (prioritas tinggi)
- Mahasiswa semester awal (prioritas rendah)
  
Desain OOP:
Kita menggunakan dua kelas:
- Mahasiswa: menyimpan nama, NIM, dan prioritas.
- PriorityQueue: menyimpan antrean mahasiswa dengan struktur heap.
  
```cpp
class Mahasiswa {
public:
 string nama;
 string nim;
 int prioritas;
 Mahasiswa(string n = "", string ni = "", int p = 0) {
 nama = n;
 nim = ni;
 prioritas = p;
 }
};
class PriorityQueue {
private:
 Mahasiswa* heap;
 int size;
 int capacity;
 void swap(int i, int j) {
 Mahasiswa temp = heap[i];
 heap[i] = heap[j];
 heap[j] = temp;
 }
 void heapifyUp(int idx) {
 while (idx > 0 && heap[(idx - 1)/2].prioritas < heap[idx].prioritas) {
 swap(idx, (idx - 1)/2);
 idx = (idx - 1)/2;
 }
 }
 void heapifyDown(int idx) {
 int maxIdx = idx;
 int l = 2 * idx + 1;
 int r = 2 * idx + 2;
 if (l < size && heap[l].prioritas > heap[maxIdx].prioritas)
 maxIdx = l;
 if (r < size && heap[r].prioritas > heap[maxIdx].prioritas)
 maxIdx = r;
 if (idx != maxIdx) {
 swap(idx, maxIdx);
 heapifyDown(maxIdx);
 }
 }
public:
 PriorityQueue(int c = 100) {
 capacity = c;
 heap = new Mahasiswa[capacity];
 size = 0;
 }
 void enqueue(string nama, string nim, int prioritas) {
 if (size == capacity) return;
 heap[size] = Mahasiswa(nama, nim, prioritas);
 heapifyUp(size);
 size++;
 }
 Mahasiswa dequeue() {
 if (size == 0) return Mahasiswa();
 Mahasiswa result = heap[0];
 heap[0] = heap[--size];
 heapifyDown(0);
 return result;
 }
 bool isEmpty() {
 return size == 0;
 }
 ~PriorityQueue() {
 delete[] heap;
 }
};
Contoh Penggunaan:
int main() {
 PriorityQueue pq;
 pq.enqueue("Ani", "5026220012", 3);
 pq.enqueue("Budi", "5026220001", 5);
 pq.enqueue("Cici", "5026220033", 2);
 while (!pq.isEmpty()) {
 Mahasiswa mhs = pq.dequeue();
 cout << mhs.nama << " - " << mhs.nim << " dilayani.\n";
 }
 return 0;
}
```

# Output:

```
Budi - 5026220001 dilayani.
Ani - 5026220012 dilayani.
Cici - 5026220033 dilayani.
```

# Kesimpulan:
Dengan pendekatan OOP dan tanpa STL, kita bisa membuat Priority Queue berbasis binary heap untuk aplikasi nyata
seperti layanan mahasiswa.
Implementasi ini efisien (O(log n)) dan fleksibel untuk berbagai skenario dunia nyata.
