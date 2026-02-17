# CRM / Teknik Servis Uçtan Uca Süreç Tablosu

Bu tablo, satıştan kurulum ve arıza/ikame/tamir döngüsüne kadar anlattığınız akışı tek bir operasyon şemasında toplar.

## 1) Yüksek Seviye Süreç Tablosu

| Aşama | Tetikleyici | Sorumlu Ekip | Yapılan İş | Lokasyon Kuralı | Çıktı / Sonraki Aşama |
|---|---|---|---|---|---|
| 1. Satışın kapanması | Yeni satış | Satış Ekibi | Müşteri satışı tamamlanır | - | Proje destek ekibine devir |
| 2. Sipariş oluşturma | Satış devir | Proje Destek | Logo'da sipariş açılır, Donanım'a bildirim geçilir | - | Cihaz hazırlık süreci başlar |
| 3. Cihaz hazırlık ve test | Donanım talebi | Donanım Birimi | Cihaz işletmeye uygun hazırlanır ve test edilir | - | Kurulum planına geçilir |
| 4. Kurulum lojistiği | Cihaz hazır | Donanım + Saha/Kargo | Kurulum sevkiyat modeli belirlenir | İstanbul içi: Saha ekip araçla götürür. Şehir dışı: Kargo ile gönderim | Kurulum tamamlanır, cihaz aktif olur |
| 5. Arıza bildirimi | Cihaz arızası | İşletme + Çağrı Merkezi | Arıza kaydı açılır, uzaktan müdahale denenir | - | Çözülürse kayıt kapanır; çözülmezse Donanım'a atanır |
| 6. Uzaktan çözülemeyen arıza | Remote çözüm başarısız | Çağrı Merkezi + Donanım | Servis kaydı donanıma yönlendirilir, muadil hazırlığı başlatılır | - | Muadil gönderim aşaması |
| 7. Muadil cihaz gönderimi/değişimi | Donanım ataması | Donanım + Saha/Kargo + Çağrı Merkezi | Muadil cihaz müşteriye ulaştırılır, veriler yedeklenip muadile aktarılır | İstanbul içi: Saha ekip yerinde değişim yapar, arızalıyı alır. Şehir dışı: Muadil kargo ile gider; müşteri değiştirir, arızalıyı kargo ile yollar | İşletme kesintisiz çalışmaya devam eder |
| 8. Arızalı cihaz kabul | Arızalı ürünün geri gelişi | RobotPOS Teknik Servis | Gelen kargo kabul/servis giriş işlemi yapılır | - | Ürün tipine göre onarım akışı |
| 9A. RobotPOS ürünü onarım | Ürün RobotPOS'a ait | Teknik Servis | Arıza tespiti ve onarım yapılır | Masraf varsa müşteri onayı alınır. Garanti kapsamındaysa hızlı onarım | Tamir sonrası müşteriye geri gönderim |
| 9B. Tedarikçi ürünü onarım | Ürün dış tedarik | Donanım + Tedarikçi + Çağrı Merkezi/Satış Operasyon | Cihaz tedarikçiye yönlendirilir, maliyet çıkarsa müşteriye teklif iletilir | Müşteri onayı sonrası onarım | Tamir sonrası müşteriye geri gönderim |
| 10. Muadil geri toplama ve kapanış | Asıl cihaz geri gönderime hazır | Saha/Kargo + Donanım + Çağrı Merkezi | Tamirli cihaz işletmeye ulaştırılır, muadil geri alınır | İstanbul içi: Saha ekip geri alır. Şehir dışı: Kargo ile dönüş | Servis kaydı kapanır, SLA ve raporlama güncellenir |

---

## 2) Karar Noktaları (Kısa)

| Karar | Seçenek | İş Kuralı |
|---|---|---|
| Kurulum tipi | İstanbul içi / Şehir dışı | İstanbul içi => Saha kurulum, şehir dışı => Kargo |
| Arıza çözümü | Uzaktan çözülür / çözülmez | Çözülmezse donanım birimine servis ataması |
| Muadil değişim | Yerinde / Kargo | Lokasyona göre saha veya kargo modeli |
| Ürün sahipliği | RobotPOS / Tedarikçi | RobotPOS: iç servis, Tedarikçi: dış servis süreci |
| Masraf | Var / Yok | Varsa müşteri onayı zorunlu |
| Garanti | Garantili / Garanti dışı | Garantili ürün öncelikli onarım ve hızlı dönüş |

---

## 3) CRM'de Önerilen Durum (Status) Akışı

1. `SATIS_TAMAMLANDI`
2. `SIPARIS_OLUSTURULDU`
3. `CIHAZ_HAZIRLANIYOR`
4. `KURULUM_PLANLANDI`
5. `KURULUM_TAMAMLANDI`
6. `ARIZA_BILDIRIMI_ALINDI`
7. `UZAKTAN_DESTEK_DEVAM`
8. `DONANIMA_ATANDI`
9. `MUADIL_GONDERIMDE`
10. `VERI_AKTARIM_TAMAMLANDI`
11. `ARIZALI_CIHAZ_SERVISTE`
12. `ONARIM_BEKLIYOR_MUSTERI_ONAYI` (masraflıysa)
13. `ONARIMDA`
14. `MUSTERIYE_GERI_GONDERILDI`
15. `MUADIL_GERI_ALINDI`
16. `KAYIT_KAPANDI`

---

## 4) Takip Edilecek KPI Önerileri

- İlk kurulum süresi (satış -> aktif kullanım)
- Uzaktan çözüm oranı
- Muadil gönderim süresi
- Servis çevrim süresi (MTTR)
- Müşteri onay bekleme süresi
- Garanti içi / garanti dışı arıza dağılımı
- Tedarikçi kaynaklı servis gecikme oranı

