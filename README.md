# Kecerdasan-Buatan-DFS-dan-BFS
Nama    : Wahyu Kurnia Sari
Kelas : D4TI3A
Npm    : 1184001

BFS sebuah algoritma pencarian jalur sederhana, dimana pencarian dimulai dari titik awal, kemudian dilanjutkan ke semua cabang titik tersebut secara terurut. Jika titik tujuan belum ditemukan, maka perhitungan akan diulang lagi ke masing-masing titik cabang dari masing-masing titik, sampai titik tujuan tersebut ditemukan.
#awal = B
#tujuan = F
#jalur

peta1 =  {'A':set(['B']),
         'B':set(['C','A']),
         'C':set(['B','D','E']),
         'D':set(['C','E']),
         'E':set(['C','D','F']),
         'F':set(['E','G']),
         'G':set(['F'])}

def bfs(graf, mulai, tujuan):
    antrian = [[mulai]]
    visited = set()

    while antrian:     
        # masukkan antrian paling depan ke variabel jalur
        jalur = antrian.pop(0)

        # simpan node yang dipilih ke variabel state, misal jalur = C,B maka simpan B ke variabel state
        state = jalur[-1]

        # cek state apakah sama dengan tujuan, jika ya maka return jalur
        if state == tujuan:
            return jalur
        # jika state tidak sama dengan tujuan, maka cek apakah state tidak ada di visited
        elif state not in visited:
            # jika state tidak ada di visited maka cek cabang
            for cabang in graf.get(state, []): #cek semua cabang dari state untuk menampung jalur selanjutnya
                jalur_baru = list(jalur) #masukkan isi dari variabel jalur ke variabel jalur_baru('C')
                jalur_baru.append(cabang) #update/tambah isi jalur_baru dengan cabang['B','C']
                antrian.append(jalur_baru) #update/tambah antrian dengan jalur_baru[['B','C']]
                print(jalur_baru)

            # tandai state yang sudah dikunjungi sebagai visited
            visited.add(state)

        #cek isi antrian
        isi = len(antrian)
        if isi == 0:
            print("Tidak ditemukan")

print(bfs(peta1,'B','F'))

DFS Pencarian dilakukan pada satu node dalam setiap level dari yang paling kiri. Jika pada level yang paling dalam, solusi belum ditemukan, maka pencarian dilanjutkan pada node sebelah kanan. Node yang kiri dapat dihapus dari memori. Jika pada level yang paling dalam tidak ditemukan solusi, maka pencarian dilanjutkan pada level sebelumnya.
DFS 
#contoh peta dari UDINUS(B) ke Lawang Sewu(F)
peta =  {'A':set(['B']),
         'B':set(['C','A']),
         'C':set(['B','D','E']),
         'D':set(['C','E']),
         'E':set(['C','D','F']),
         'F':set(['E','G']),
         'G':set(['F'])}


def dfs(graf, mulai, tujuan):
    stack = [[mulai]]
    visited = set()

    while stack:
        #hitung panjang tumpukan dan masukkan ke variabel panjang_tumpukan
        panjang_tumpukan = len(stack)-1
        
        # masukkan tumpukan palinif state == tujuan:g atas ke variabel jalur
        jalur = stack.pop(panjang_tumpukan)

        # simpan node yang dipilih ke variabel state, misal jalur = C,B maka simpan B ke variabel state
        state = jalur[-1]

        # cek state apakah sama dengan tujuan, jika ya maka return jalur
        if state == tujuan:
            return jalur
        # jika state tidak sama dengan tujuan, maka cek apakah state tidak ada di visited
        elif state not in visited:
            # jika state tidak ada di visited maka cek cabang
            for cabang in graf.get(state, []): #cek semua cabang dari state
                jalur_baru = list(jalur) #masukkan isi dari variabel jalur ke variabel jalur_baru
                jalur_baru.append(cabang) #update/tambah isi jalur_baru dengan cabang
                stack.append(jalur_baru) #update/tambah queue dengan jalur_baru
                print(jalur_baru)


            # tandai state yang sudah dikunjungi sebagai visited
            visited.add(state)


        #cek isi tumpukan
        isi = len(stack)
        if isi == 0:
            print("Tidak ditemukan")

print(dfs(peta,'B','F'))
