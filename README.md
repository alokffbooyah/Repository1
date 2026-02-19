#Repository1

import random

khodam_tipe_a = ["Macan Ompong", "Nyi Blorong", "Sapu Lidi", "Kelinci Banyuwangi"]
khodam_tipe_b = ["Tutup Panci", "Pohon Pisang", "Kak Gem", "Awewe Gombel"]

riwayat = []

def tes_kepribadian():
    skor_a = 0
    skor_b = 0

    pertanyaan = [
        "1. (A) Es Teh Manis atau (B) Es Teh Panas? ",
        "2. (A) Naspad Padang atau (B) Nasduk Uduk? ",
        "3. (A) Windah Tol Cipularang atau (B) Lato-Lato Mojokerto? ",
        "4. (A) Preketekketek atau (B) Blakutakkutuk? ",
        "5. (A) Anggrek Mekar Pontianak atau (B) Kayu Jati Solo? ",
        "6. (A) Cukurukuk atau (B) Ambatron? ",
        "7. (A) Cumi Hitam Pakde Kris atau (B) Bumbu Kacang Kabumen? ",
        "8. (A) Puding Coklat Pak Hambali atau (B) Kapucino Bejo? ",
        "9. (A) Tung Tung Sahur atau (B) Tralaleo Trelelala? ",
        "10. (A) Fuad Racing atau (B) Roti O Lempuyangan? "
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
    tipe = tes_kepribadian()

    if tipe == "A":
        hasil = random.choice(khodam_tipe_a)
    else:
        hasil = random.choice(khodam_tipe_b)

    print(f"\n>>> {nama} memiliki khodam: {hasil} <<<")
    riwayat.append(f"{nama}: {hasil}")


def lihat_riwayat():
    if not riwayat:
        print("Belum ada riwayat.")
    else:
        for i, data in enumerate(riwayat, 1):
            print(f"{i}. {data}")


def main():
    while True:
        print("\n=== APLIKASI CEK KHODAM ===")
        print("1. Cek Khodam")
        print("2. Lihat Riwayat")
        print("3. Keluar")

        pilih = input("Pilih menu: ")

        if pilih == "1":
            cek_khodam()
        elif pilih == "2":
            lihat_riwayat()
        elif pilih == "3":
            break
        else:
            print("Menu tidak tersedia.")


if __name__ == "__main__":
    main()
