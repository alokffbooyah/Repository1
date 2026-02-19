# Repository1
import random

# =====================================
# BAGIAN 1 - CEK KHODAM
# =====================================

khodam_tipe_a = ["Macan Ompong", "Nyi Blorong", "Fuad Racing", "Kelinci Banyuwangi"]
khodam_tipe_b = ["Tutup Panci", "Sapu Lidi", "Kucing Kayang", "Ambatron"]

riwayat_khodam = []

def tes_kepribadian():
    skor_a = 0
    skor_b = 0

    pertanyaan = [
        "1. (A) Es Teh Manis / (B) Es Teh Panas? ",
        "2. (A) Nasi Padang / (B) Nasi Uduk? ",
        "3. (A) Cukurukuk / (B) Ambatron? "
    ]

    for soal in pertanyaan:
        while True:
            jawab = input(soal).upper()
            if jawab == "A":
                skor_a += 1
                break
            elif jawab == "B":
                skor_b += 1
                break
            else:
                print("Pilih A atau B!")

    return "A" if skor_a >= skor_b else "B"


def cek_khodam():
    nama = input("Masukkan nama Anda: ")

    if nama.strip() == "":
        print("Nama tidak boleh kosong!")
        return

    tipe = tes_kepribadian()

    if tipe == "A":
        hasil = random.choice(khodam_tipe_a)
    else:
        hasil = random.choice(khodam_tipe_b)

    print(f"\n>>> {nama} memiliki khodam: {hasil} <<<")
    riwayat_khodam.append(f"{nama}: {hasil}")


def lihat_riwayat_khodam():
    if not riwayat_khodam:
        print("Belum ada riwayat.")
    else:
        for i, data in enumerate(riwayat_khodam, 1):
            print(f"{i}. {data}")


# =====================================
# BAGIAN 2 - TO DO LIST
# =====================================

DATA_FILE = "data.txt"

def load_data():
    tasks = []
    try:
        with open(DATA_FILE, "r") as file:
            for line in file:
                line = line.strip().split("|")
                if len(line) == 2:
                    tasks.append({"nama": line[0], "status": line[1]})
    except FileNotFoundError:
        pass
    return tasks


def save_data(tasks):
    with open(DATA_FILE, "w") as file:
        for task in tasks:
            file.write(f"{task['nama']}|{task['status']}\n")


def tambah_tugas(tasks):
    nama = input("Masukkan nama tugas: ")
    tasks.append({"nama": nama, "status": "Belum"})
    save_data(tasks)
    print("Tugas ditambahkan.")


def lihat_tugas(tasks):
    if not tasks:
        print("Belum ada tugas.")
        return

    for i, task in enumerate(tasks, 1):
        print(f"{i}. {task['nama']} - {task['status']}")


def tandai_selesai(tasks):
    lihat_tugas(tasks)
    try:
        nomor = int(input("Nomor tugas selesai: "))
        tasks[nomor-1]["status"] = "Selesai"
        save_data(tasks)
        print("Tugas ditandai selesai.")
    except:
        print("Input tidak valid.")


def hapus_tugas(tasks):
    lihat_tugas(tasks)
    try:
        nomor = int(input("Nomor tugas dihapus: "))
        tasks.pop(nomor-1)
        save_data(tasks)
        print("Tugas dihapus.")
    except:
        print("Input tidak valid.")


# =====================================
# MENU UTAMA GABUNGAN
# =====================================

def main():
    tasks = load_data()

    while True:
        print("\n=== APLIKASI GABUNGAN ===")
        print("1. Cek Khodam")
        print("2. Lihat Riwayat Khodam")
        print("3. Tambah Tugas")
        print("4. Lihat Tugas")
        print("5. Tandai Tugas Selesai")
        print("6. Hapus Tugas")
        print("7. Keluar")

        try:
            pilih = int(input("Pilih menu: "))

            if pilih == 1:
                cek_khodam()
            elif pilih == 2:
                lihat_riwayat_khodam()
            elif pilih == 3:
                tambah_tugas(tasks)
            elif pilih == 4:
                lihat_tugas(tasks)
            elif pilih == 5:
                tandai_selesai(tasks)
            elif pilih == 6:
                hapus_tugas(tasks)
            elif pilih == 7:
                print("Program selesai.")
                break
            else:
                print("Menu tidak tersedia.")

        except ValueError:
            print("Masukkan angka yang benar!")


if __name__ == "__main__":
    main()
