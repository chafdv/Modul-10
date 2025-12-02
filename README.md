# <h1 align="center">Laporan Praktikum Struktur Data<br> Modul 10 TREE (BAGIAN PERTAMA) </h1>
<p align="center">Osha Alfida Valyana / 103112430202</p>

## Dasar Teori

Tree adalah tipe struktur data non-linier yang mengorganisir elemen data dalam bentuk hierarki, dengan istilah-istilah penting seperti node, root, leaf, dan ancestor. Tree digunakan untuk merepresentasikan hubungan hierarkis, seperti kategori produk dalam toko online atau silsilah keluarga. Binary tree adalah jenis khusus dari tree yang membatasi setiap node untuk memiliki maksimal dua subtree.

## Guided

### Soal 1

```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);
    
    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = insert(root->kanan, nilai);

    return root;
}

Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;

    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);
}

Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;

        return current;
}

Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL){
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
}

Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama);
        root = insert(root, baru);
        cout << "Data " << Lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << Lama << " tidak ditemukan!" << endl;
    }
    return root;
}

void preOrder(Node *root)
{
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukan.\n" << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVELSAL) ===" << endl;
    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root,cari1) ? "Ketemu" : "Tidak Aada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root,cari2) ? "Ketemu" : "Tidak Aada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    root = update(root, 5, 8);
    cout << "Hasil Order setelah update: ";
    cout << endl;
    cout << endl;

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "== 5. TEST DELETE ===" << endl;
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    return 0;
}
```
Output
⁠![Output guided](https://github.com/chafdv/Modul-10/blob/main/Output/guided10.png)

Program ini mengimplementasikan Binary Search Tree (BST) dengan beberapa operasi utama, yaitu memasukkan data (insert), menampilkan isi tree dengan traversal PreOrder, InOrder, dan PostOrder, mencari data (search), memperbarui data dengan mekanisme hapus dan tambah ulang (update), serta menghapus node sesuai aturan BST. Setiap data disimpan secara terurut di mana nilai lebih kecil berada di kiri dan nilai lebih besar berada di kanan, sehingga proses pencarian dan pengolahan data menjadi lebih efisien.
---

## Unguided

### Soal 1

Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file “bstree.h”, Buatlah implementasi ADT Binary Search Tree pada file “bstree.cpp” dan cobalah hasil implementasi ADT pada file “main.cpp”

```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 7);

    cout << "InOrder : ";
    InOrder(root);
    cout << endl;

    return 0;
}
```
 ⁠
Output
	⁠![Output Soal 1](https://github.com/chafdv/Modul-10/blob/main/Output/unguided1.png)

Program ini membuat Binary Search Tree dan memasukkan beberapa data ke dalamnya. Setelah tree terbentuk, data ditampilkan menggunakan traversal PreOrder, InOrder, dan PostOrder untuk menunjukkan urutan penelusuran yang berbeda dalam struktur tree.
---

### Soal 2

Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.
➢ fungsi hitungJumlahNode( root:address ) : integer
/* fungsi mengembalikan integer banyak node yang ada di dalam BST*/
➢ fungsi hitungTotalInfo( root:address, start:integer ) : integer
/* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/
➢ fungsi hitungKedalaman( root:address, start:integer ) : integer
/* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */

```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 7);

    cout << "kedalaman   : " << hitungKedalaman(root) << endl;
    cout << "jumlah node : " << hitungJumlahNode(root) << endl;
    cout << "total info  : " << hitungTotalInfo(root) << endl;

    return 0;
}
```

Output 
	⁠![Output Soal 2](https://github.com/chafdv/Modul-10/blob/main/Output/unguided2.png)

Program ini menghitung informasi pada Binary Search Tree yang telah dibuat, yaitu jumlah seluruh node, total nilai data dalam tree, dan kedalaman atau tinggi tree. Semua perhitungan dilakukan secara rekursif dengan menelusuri node dari akar hingga daun.
---

### Soal 3

Print tree secara pre-order dan post-order.

```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;

    address root = NULL;
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 2);
    insertNode(root, 1);
    insertNode(root, 3);
    insertNode(root, 5);
    insertNode(root, 7);

    cout << "Tampilan PreOrder  : ";
    PreOrder(root);
    cout << endl;

    cout << "Tampilan InOrder   : ";
    InOrder(root);
    cout << endl;

    cout << "Tampilan PostOrder : ";
    PostOrder(root);
    cout << endl;

    return 0;
}
```
 
Output 
	⁠![Output Soal 3](https://github.com/chafdv/Modul-10/blob/main/Output/unguided3.png)

Program ini kembali membentuk Binary Search Tree dan menampilkan datanya dengan dua jenis traversal, yaitu PreOrder dan PostOrder. Perbandingan hasilnya menunjukkan perbedaan cara penelusuran node dalam struktur tree.
## Referensi

1.⁠ ⁠[https://www.scribd.com/document/879449917/Struktur-Data-Tree-muthia-2317020099] [diakses 01-12-2025]
