#include <stdio.h>
#include <string.h>
#define MAX_BOOKS 100

//struct untuk menyimpan informasi buku
typedef struct Buku{
  char judul[100], pengarang[100], penerbit[100];
  int halaman, dipinjam;
} Buku;

//fungsi untuk mencari buku berdasarkan judul
int cariBuku(Buku books[], char judul[], int banyakBuku){
  int i;
  for(i = 0; i < banyakBuku; i++){
    if(strcmp(books[i].judul, judul) == 0){
    return i;
   }
  }
  return -1;
}

// Fungsi untuk menambah buku ke dalam array books
void tambahBuku(Buku books[], int* banyakBuku) {
    if (*banyakBuku >= MAX_BOOKS) {
        printf("Maaf, tidak dapat menambah buku lagi.\n");
        return;
    }
    Buku Bukubaru;
    printf("Judul: ");
    scanf(" %[^\n]s", Bukubaru.judul);
    printf("Pengarang: ");
    scanf(" %[^\n]s", Bukubaru.pengarang);
    printf("Penerbit: ");
    scanf(" %[^\n]s", Bukubaru.penerbit);
    printf("Jumlah halaman: ");
    scanf("%d", &Bukubaru.halaman);
    Bukubaru.dipinjam = 0; // set default status peminjaman ke false
    books[*banyakBuku] = Bukubaru;
    (*banyakBuku)++;
    printf("Buku berhasil ditambahkan.\n");
}

// Fungsi untuk meminjam buku
void pinjamBuku(Buku books[], int banyakBuku) {
    char judul[100];
    printf("Judul buku yang ingin dipinjam: ");
    scanf(" %[^\n]s", judul);
    int Indexbuku = cariBuku(books, judul, banyakBuku);
    if (Indexbuku == -1) {
        printf("Maaf, buku tidak ditemukan.\n");
        return;
    }
    if (books[Indexbuku].dipinjam) {
        printf("Maaf, buku sedang dipinjam.\n");
        return;
    }
    books[Indexbuku].dipinjam = 1;
    printf("Buku berhasil dipinjam.\n");
}

//fungsi untuk mengembalikan buku
void kembalikanBuku(Buku books[], int banyakBuku) {
    char judul[100];
    printf("Judul buku yang ingin dikembalikan: ");
    scanf(" %[^\n]s", judul);
    int Indexbuku = cariBuku(books, judul, banyakBuku);
    if (Indexbuku == -1) {
        printf("Maaf, buku tidak ditemukan.\n");
        return;
    }
    if (!books[Indexbuku].dipinjam) {
        printf("Maaf, buku belum dipinjam.\n");
        return;
    }
    books[Indexbuku].dipinjam = 0;
    printf("Buku berhasil dikembalikan.\n");
}

// Fungsi untuk menampilkan seluruh buku dalam array books
void tampilkansemuaBuku(Buku books[], int banyakBuku) {
    int i;
    if (banyakBuku == 0) {
        printf("Tidak ada buku yang tersimpan.\n");
        return;
    }
    for (i = 0; i < banyakBuku; i++) {
        printf("=====================\n");
        printf("Judul: %s\n", books[i].judul);
        printf("Pengarang: %s\n", books[i].pengarang);
        printf("Penerbit: %s\n", books[i].penerbit);
        printf("Jumlah halaman: %d\n", books[i].halaman);
        if (books[i].dipinjam) {
            printf("Status peminjaman: Dipinjam\n");
        } else {
            printf("Status peminjaman: Tersedia\n");
        }
    }
}

int main() {
Buku books[MAX_BOOKS];
int banyakBuku = 0;
int pilihan;
do {
  printf("\n======== Perpustakaan ========\n");
  printf("1. Tambah buku\n");
  printf("2. Pinjam buku\n");
  printf("3. Kembalikan buku\n");
  printf("4. Tampilkan seluruh buku\n");
  printf("0. Keluar\n");
  printf("Pilih: ");
  scanf("%d", &pilihan);
switch (pilihan) {
  case 1:
  tambahBuku(books, &banyakBuku);
  break;
  case 2:
  pinjamBuku(books, banyakBuku);
  break;
  case 3:
  kembalikanBuku(books, banyakBuku);
  break;
  case 4:
  tampilkansemuaBuku(books, banyakBuku);
  break;
  case 0:
  printf("Terima kasih telah menggunakan layanan perpustakaan.\n");
  break;
  default:
  printf("Pilihan tidak valid.\n");
  break;
}
} while (pilihan != 0);
return 0;
}
