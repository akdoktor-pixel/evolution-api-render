# Evolution API Render.com Kurulumu

## Adım Adım Kurulum

### 1. GitHub Repo Oluştur
1. GitHub.com'a gidin
2. Yeni repository oluşturun: `evolution-api-render`
3. Bu dizindeki dosyaları yükleyin:
   - Dockerfile
   - .env.example
   - render.yaml

### 2. Render.com Hesabı Oluştur
1. Render.com'a gidin: https://render.com
2. Ücretsiz hesap oluşturun
3. GitHub hesabınızı bağlayın

### 3. Render.com'da Web Service Oluştur
1. "New +" → "Web Service" tıklayın
2. GitHub repository'nizi seçin (`evolution-api-render`)
3. Branch: `main`
4. Runtime: `Docker`
5. Build Command: Boş bırakın (Dockerfile kullanılacak)
6. Start Command: Boş bırakın
7. Environment Variables ekleyin:
   - `SERVER_PORT`: `8080`
   - `AUTHENTICATION_TYPE`: `apikey`
   - `AUTHENTICATION_API_KEY`: `RerNpJI26t0D5z9gkeqPvTntAcctt-_8WWjdSjEwJKM`
   - `AUTHENTICATION_EXAMPLE_INSTANCE`: `api`
   - `DATABASE_TYPE`: `sqlite`
   - `DATABASE_SQLITE_PATH`: `/tmp/database.sqlite`
8. Plan: Free
9. Region: Oregon (veya size en yakın)
10. "Create Web Service" tıklayın

### 4. Oluşturma Bekleyin
- Render Evolution API'yi indirecek
- Docker imajını oluşturacak
- Deploy edecek
- Bu işlem 5-10 dakika sürebilir

### 5. URL Alın
- Deploy tamamlandığında Render size bir URL verecek
- Örnek: `https://evolution-api.onrender.com`

### 6. Projenin .env Dosyasını Güncelle
Projenizin .env dosyasında:
```
EVOLUTION_API_BASE_URL=https://evolution-api-xxxx.onrender.com
EVOLUTION_API_INSTANCE=api
EVOLUTION_API_KEY=RerNpJI26t0D5z9gkeqPvTntAcctt-_8WWjdSjEwJKM
```

### 7. Instance Oluştur
Render deploy URL'inize gidin:
```
https://evolution-api-xxxx.onrender.com
```
- API Key ile giriş yapın
- "api" instance'ını oluşturun
- QR kod ile WhatsApp'ı bağlayın

### 8. Test Edin
```bash
python test_whatsapp_integration.py
```

## Önemli Notlar

- Render Free Plan: 512MB RAM, 0.1 CPU
- Evolution API minimum gereksinim: ~500MB RAM
- Render Free Plan yeterli olacaktır
- Uptime: 7/24 (Render otomatik yeniden başlatır)
- Cold Start: İlk istekte 30-60 saniye başlatma süresi

## Sorun Giderme

### Deploy Başarısız Olursa
1. Dockerfile'ı kontrol edin
2. Environment variables'ı kontrol edin
3. Render loglarını kontrol edin

### Instance Bağlantı Sorunu
1. Render URL'inin doğru olduğundan emin olun
2. API Key'in doğru olduğundan emin olun
3. QR kod ile tekrar bağlayın

### Cold Start (Yavaş Başlama)
- Render Free Plan'da normaldir
- İlk istekte 30-60 saniye bekleyebilir
- Sonraki istekler hızlı olacaktır

## API Key
Bu kurulum için oluşturulan API Key: `RerNpJI26t0D5z9gkeqPvTntAcctt-_8WWjdSjEwJKM`
