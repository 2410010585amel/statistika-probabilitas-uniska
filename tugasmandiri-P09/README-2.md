# Projek Statistika — Milestone 1: EDA Gym Members Exercise Tracking

**Mata kuliah:** Statistika dan Probabilitas (TIF1501), Teknik Informatika, Uniska MAB Banjarmasin
**Penulis:** Fadliatul Amaliyah (NIM 2410010585)

## 1. Deskripsi Dataset

Dataset berisi catatan latihan **973 anggota gym** dengan **15 kolom**: data tubuh, detak jantung, sesi latihan, asupan air, dan tingkat pengalaman. Tidak ada data kosong dan tidak ada baris duplikat.

| Kolom asli | Nama di notebook | Jenis data | Keterangan |
|---|---|---|---|
| Age | `age` | Rasio | Umur (18-59 tahun) |
| Gender | `gender` | Nominal | Male / Female |
| Weight (kg) | `weight` | Rasio | Berat badan |
| Height (m) | `height` | Rasio | Tinggi badan |
| Max_BPM | `max_bpm` | Rasio | Detak jantung maksimum |
| Avg_BPM | `avg_bpm` | Rasio | Detak jantung rata-rata saat latihan |
| Resting_BPM | `rest_bpm` | Rasio | Detak jantung istirahat |
| Session_Duration (hours) | `duration` | Rasio | Durasi sesi (jam) |
| Calories_Burned | `calories` | Rasio | Kalori terbakar per sesi |
| Workout_Type | `workout` | Nominal | Cardio / HIIT / Strength / Yoga |
| Fat_Percentage | `fat_pct` | Rasio | Persentase lemak tubuh |
| Water_Intake (liters) | `water` | Rasio | Asupan air per hari |
| Workout_Frequency (days/week) | `freq` | Rasio | Hari latihan per minggu (2-5) |
| Experience_Level | `exp` | Ordinal | 1 Beginner, 2 Intermediate, 3 Expert |
| BMI | `bmi` | Rasio | Indeks massa tubuh |

**Syarat Milestone 1:** 973 baris (≥ 500), 15 kolom (≥ 5), bukan dataset Mall Customers.

## 2. Sumber Data

Kaggle: *Gym Members Exercise Dataset* (file `gym_members_exercise_tracking.csv`).
Konteks: pengelola gym ingin mengetahui faktor yang berkaitan dengan kalori terbakar dan persentase lemak agar program latihan dan saran kepada anggota lebih tepat sasaran.

## 3. Cara Menjalankan

1. Unduh `gym_members_exercise_tracking.csv` dari halaman dataset di Kaggle.
2. Buka `Milestone1-EDA-GymMembers-FadliatulAmaliyah.ipynb` di Google Colab (**File → Upload notebook**).
3. Jalankan **Runtime → Run all**. Saat muncul tombol unggah di Langkah 1, pilih file CSV.
4. Setelah selesai, `dashboard_milestone1.html` (interaktif) dan `dashboard_static.png` (gambar) tersimpan di Colab. Unduh keduanya.

Library: `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly` (semua tersedia di Colab).

## 4. Struktur Repositori

```
projek-statistika-fadliatul-amaliyah/
├── README.md
├── Milestone1-EDA-GymMembers-FadliatulAmaliyah.ipynb
├── gym_members_exercise_tracking.csv   (opsional)
├── dashboard_milestone1.html
└── screenshots/
    └── dashboard.png
```

![Dashboard](screenshots/dashboard.png)

## 5. Ringkasan Insight

1. **Durasi sesi adalah faktor yang paling berkaitan dengan kalori terbakar.** Korelasi durasi dengan kalori sangat kuat (r = 0,908), jauh di atas detak jantung rata-rata (r = 0,340) dan berat badan (r = 0,095).
2. **Persentase lemak turun tajam pada tingkat Expert.** Rata-rata lemak Beginner 27,6%, Intermediate 27,3%, Expert 14,8%. Anggota Expert berlatih 4,5 hari per minggu selama 1,76 jam dan membakar 1.265 kalori (Beginner: 2,5 hari, 1,01 jam, 726 kalori).
3. **Pria membakar lebih banyak kalori** (944 vs 862), lebih berat (85,5 vs 60,9 kg), lemak lebih rendah (22,6% vs 27,7%), dan minum lebih banyak (3,01 vs 2,21 L). Durasi sesi hampir sama (1,25 vs 1,26 jam).
4. **Jenis latihan hampir tidak membedakan kalori.** Terendah Cardio (885), tertinggi HIIT (926); selisih hanya 41 kalori (4,6% dari rata-rata).
5. **BMI kurang menggambarkan kebugaran.** Korelasi BMI dengan fat_pct hanya r = −0,119 dan dengan calories r = 0,060. Sebaran BMI: Normal 38,0%, Overweight 25,0%, Obese 19,7%, Underweight 17,3%.

**Keterbatasan data:** ada 23 baris dengan `max_bpm` lebih kecil dari `avg_bpm` (secara fisiologis janggal; dicatat, tidak dibuang). Pola data juga sangat rapi (misal persentase lemak Expert selalu 10-20% dan tingkat lain 20-35%), sehingga kemungkinan data hasil simulasi. Semua hubungan di atas adalah **korelasi**, bukan bukti sebab-akibat.

## 6. Hipotesis untuk Milestone 2 (Modul 10)

| No | H₀ | H₁ | Uji |
|---|---|---|---|
| H1 | μ_calories(Male) = μ_calories(Female) | μ_calories(Male) ≠ μ_calories(Female) | Welch t-test + Cohen's d |
| H2 | Rata-rata calories sama di semua jenis latihan | Minimal satu jenis berbeda | One-way ANOVA (+ Tukey) |
| H3 | Rata-rata fat_pct sama di tiga tingkat pengalaman | Minimal satu tingkat berbeda | One-way ANOVA + Tukey |
| H4 (opsional) | ρ(duration, calories) = 0 | ρ ≠ 0 | Pearson r |

Semua uji memakai α = 0,05.
