# Halisaha-
# ⚽ HalıSaha PRO — Profesyonel Halı Saha Yönetim Sistemi

> Toplu para toplama derdini bitiren, her oyuncunun kendi ücretini bireysel ödediği  
> modern halı saha rezervasyon ve yönetim platformu.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.32+-FF4B4B?style=flat&logo=streamlit&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=flat&logo=sqlite&logoColor=white)
![OOP](https://img.shields.io/badge/Tasarım-OOP-34d399?style=flat)
![License](https://img.shields.io/badge/Lisans-MIT-green?style=flat)

---

## 📋 İçindekiler

- [Özellikler](#özellikler)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)
- [Proje Yapısı](#proje-yapısı)
- [OOP Mimarisi](#oop-mimarisi)
- [Ekran Görüntüleri](#ekran-görüntüleri)
- [Geliştirici](#geliştirici)

---

## ✨ Özellikler

| Özellik | Açıklama |
|---------|----------|
| 🔐 **Login Sistemi** | Rol tabanlı erişim (Admin / Oyuncu) |
| 🏟️ **Canlı Saha Haritası** | 22 formanın anlık ödeme durumu |
| ✍️ **Bireysel Rezervasyon** | Kişiye özel ekstra hizmet seçimi ve fatura |
| 💳 **Ödeme Takibi** | Filtreleme, arama, tek tıkla güncelleme |
| ⚽ **Maç Sonucu & İstatistik** | Skor, gol, asist, kart kaydı |
| 🏆 **Liderlik Tablosu** | XP sistemi, seviye ve rozet |
| 👤 **Oyuncu Profili** | Avatar, biyografi, kariyer istatistikleri |
| 📣 **WhatsApp Bildirimleri** | Maç hatırlatma ve ödeme uyarı mesajları |
| 📈 **Analitik Dashboard** | Gelir, katılım ve doluluk grafikleri |
| 👀 **Gözleme Listesi** | Forma doluyken sıraya girme |
| ⚙️ **Yönetim Paneli** | Maç ekleme/silme, sistem yönetimi |

---

## 🚀 Kurulum

### Gereksinimler

- Python 3.10 veya üzeri
- pip paket yöneticisi

### Adım 1 — Depoyu klonlayın

```bash
git clone https://github.com/kullanici_adi/halisaha-pro.git
cd halisaha-pro
```

### Adım 2 — Sanal ortam oluşturun (önerilen)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### Adım 3 — Bağımlılıkları yükleyin

```bash
pip install -r requirements.txt
```

### Adım 4 — Uygulamayı başlatın

```bash
streamlit run halisaha_pro.py
```

Tarayıcınızda otomatik olarak `http://localhost:8501` açılır.

---

## 🎮 Kullanım

### Demo Hesaplar

| Kullanıcı Adı | Şifre | Rol |
|--------------|-------|-----|
| `admin` | `admin123` | 🛡️ Yönetici |
| `hoca` | `hoca2026` | 🛡️ Yönetici |
| `oyuncu1` | `oyun1234` | ⚽ Oyuncu |
| `oyuncu2` | `oyun5678` | ⚽ Oyuncu |

### Temel Kullanım Akışı

```
1. Giriş yapın (admin veya oyuncu)
2. Sol panelden müsabaka seçin
3. "Rezervasyon" sekmesinden forma alın
4. Ekstra hizmetleri seçin → fatura otomatik hesaplanır
5. Ödeme yöntemini belirleyin ve rezerve edin
6. Yönetici "Ödemeler" sekmesinden takip eder
7. Maç sonrası "Maç Sonucu" sekmesine skor girin
8. "Liderlik" sekmesinde XP sıralamasını görün
```

---

## 📁 Proje Yapısı

```
halisaha-pro/
│
├── halisaha_pro.py      # Ana uygulama dosyası
├── halisaha_pro.db      # SQLite veritabanı (otomatik oluşur)
├── requirements.txt     # Python bağımlılıkları
├── .gitignore           # Git dışlama kuralları
└── README.md            # Bu dosya
```

---

## 🏗️ OOP Mimarisi

Proje **4 ana sınıf** üzerine inşa edilmiştir:

```
┌─────────────────────────────────────────────────────────┐
│                    Veritabani                           │
│  + tablolari_hazirla()                                  │
│  + varsayilan_verileri_ekle()                           │
│  + baglanti_al() → sqlite3.Connection                   │
└──────────────────────┬──────────────────────────────────┘
                       │ kullanır (Dependency Injection)
          ┌────────────┼────────────┬──────────────┐
          ▼            ▼            ▼              ▼
      ┌───────┐   ┌─────────┐  ┌────────┐  ┌────────────┐
      │  Mac  │   │ Oyuncu  │  │ Profil │  │EkstraHizmet│
      └───────┘   └─────────┘  └────────┘  └────────────┘
```

### Sınıflar

| Sınıf | Sorumluluk | Metodlar |
|-------|-----------|---------|
| `Veritabani` | DB bağlantısı, tablo yönetimi | `baglanti_al`, `tablolari_hazirla`, `varsayilan_verileri_ekle` |
| `Mac` | Maç CRUD, istatistik, sonuç | `ekle`, `sil`, `sifirla`, `istatistik_getir`, `sonuc_kaydet` |
| `Oyuncu` | Rezervasyon, ödeme, istatistik | `kaydet`, `odeme_guncelle`, `sil`, `gol_kaydet`, `ucret_hesapla` |
| `Profil` | XP, seviye, rozet, liderlik | `xp_ekle`, `seviye_hesapla`, `badge_hesapla`, `liderlik_tablosu` |
| `EkstraHizmet` | Hizmet yönetimi | `ekle`, `sil`, `tumu_getir` |

### Hata Yönetimi

Her veritabanı metodu **try/except** bloğu içerir:

```python
def kaydet(self, ...):
    try:
        if not ad.strip():
            raise ValueError("Oyuncu adı boş olamaz.")   # Validasyon
        conn = self.db.baglanti_al()
        conn.execute("INSERT INTO ...", (...))
        conn.commit()
        return True
    except ValueError as e:
        st.error(f"Geçersiz giriş: {e}")                 # Kullanıcı hatası
        return False
    except sqlite3.IntegrityError:
        st.error("Bu forma numarası zaten alınmış!")      # DB kısıtı
        return False
    except sqlite3.Error as e:
        st.error(f"Veritabanı hatası: {e}")               # DB hatası
        return False
```

---

## 🗄️ Veritabanı Şeması

```
maclar          oyuncular         oyuncu_profiller
──────────      ──────────        ────────────────
id (PK)         id (PK)           id (PK)
tarih           mac_id (FK)       kullanici_adi
saha_adi        ad                ad
saha_ucreti     telefon           xp
max_oyuncu      takim             mac_sayisi
durum           forma_no          gol / asist
notlar          pozisyon          sari_kart
                ekstralar         davam_serisi
                temel_ucret       avatar_ikon
                toplam_ucret
                odeme_durumu      gol_kayitlari
                odeme_yontemi     ─────────────
                                  mac_id (FK)
ekstra_hizmetler                  oyuncu_adi
────────────────                  gol_sayisi
id (PK)         mac_sonuclari     asist_sayisi
ad              ─────────────     sari_kart
ucret           mac_id (FK)
ikon            takim_a_skor      gozleme_listesi
aktif           takim_b_skor      ───────────────
                en_iyi_oyuncu     mac_id (FK)
                notlar            ad / telefon
```

---

## ⚙️ Bağımlılıklar (requirements.txt)

```
streamlit>=1.32.0
pandas>=2.0.0
```

---

## 👨‍💻 Geliştirici

**Ramiz Samed**  
Python + Streamlit + SQLite  
Akıllı Halı Saha Bireysel Ödeme Sistemi  

---

## 📄 Lisans

MIT License — özgürce kullanabilir, değiştirebilir ve dağıtabilirsiniz.
