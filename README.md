# Dockerized Microservice Architecture: FastAPI, Redis & PostgreSQL

Bu proje, modern web geliştirme standartlarına ve **Security-by-Design** (Tasarımdan İtibaren Güvenlik) prensiplerine uygun olarak tasarlanmış 5 bileşenli bir mikroservis mimarisidir. İçerisinde veri kalıcılığı, önbellekleme (caching) mekanizmaları ve konteyner orkestrasyonu barındırır.

## Kullanılan Teknolojiler

- **Backend:** Python, FastAPI (RESTful API tasarımı)
- **Veritabanı:** PostgreSQL (İlişkisel veri yönetimi)
- **Önbellek (Cache):** Redis (Cache-Aside Pattern)
- **Frontend:** Nginx (Statik dosya sunumu)
- **Veritabanı Yönetimi:** pgAdmin 4
- **Konteynerizasyon:** Docker & Docker Compose

## Öne Çıkan Özellikler

- **Tam İzolasyon (5 Konteyner):** Frontend, Backend, Database, Cache ve DB Admin servisleri birbirinden izole edilmiş konteynerlerde çalışır ve sadece belirlenen ağlar üzerinden haberleşir.
- **Cache-Aside Stratejisi:** Veritabanı yükünü hafifletmek ve yanıt sürelerini hızlandırmak için Redis entegrasyonu yapılmıştır. Veriler önce önbellekte aranır, yoksa veritabanından çekilip Redis'e yazılır.
- **Güvenlik Odaklı Yapı:**
  - Veritabanı şifreleri ve hassas bilgiler koda gömülmemiş, `.env` dosyası üzerinden çevre değişkenleri (environment variables) ile sisteme aktarılmıştır.
  - `.dockerignore` ve `.gitignore` yapılandırmalarıyla gereksiz/hassas dosyaların imajlara ve versiyon kontrol sistemine sızması engellenmiştir.
- **Veri Kalıcılığı:** Docker Volume kullanılarak, PostgreSQL verileri konteyner silinse dahi korunacak şekilde yapılandırılmıştır.

## Proje Yapısı

```text
docker-compose-mastery/
├── backend/
│   ├── app.py              # FastAPI uç noktaları ve Redis/DB mantığı
│   ├── Dockerfile          # Backend konteyner inşa talimatları
│   ├── requirements.txt    # Python bağımlılıkları
│   └── .dockerignore       # Docker imaj optimizasyonu
├── frontend/
│   └── index.html          # Nginx tarafından sunulan kullanıcı arayüzü
├── docker-compose.yml      # Mikroservis orkestrasyon dosyası
├── .gitignore              # Git tarafından takip edilmeyecek dosyalar
└── README.md               # Proje dokümantasyonu
```
