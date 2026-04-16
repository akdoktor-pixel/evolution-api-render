# Render.com Dockerfile Hatası Çözümü

**Hata:** error: failed to solve: failed to read dockerfile: open Dockerfile: no such file or directory

## Sorun Analizi
Bu hata Render.com'ın Dockerfile'ı bulamamasından kaynaklanıyor.

## Çözüm Adımları

### 1. GitHub Repo Yapısını Kontrol Edin
GitHub repository'nizi açın ve şunları kontrol edin:

**DOĞRU Yapışma (Dosyalar kök dizinde):**
```
your-repo/
├── Dockerfile
├── .env.example
├── render.yaml
└── README.md
```

**YANLIŞ Yapışma (Dosyalar klasör içinde):**
```
your-repo/
└── evolution-render-setup/
    ├── Dockerfile
    ├── .env.example
    ├── render.yaml
    └── README.md
```

### 2. Dosyaları Kök Dizine Taşıyın

Eğer dosyalar `evolution-render-setup/` klasörü içindeyse:
1. GitHub repository'nizi açın
2. Dosyaları kök dizine taşıyın
3. Commit edin

### 3. Render.com Ayarlarını Düzeltin

Render.com'da:
1. Web Service'inize gidin
2. Settings sekmesine tıklayın
3. "Dockerfile path" alanını kontrol edin

**Eğer dosyalar kök dizindeyse:**
- Dockerfile path: `Dockerfile` (veya `./Dockerfile`)

**Eğer dosyalar klasör içindeyse:**
- Dockerfile path: `evolution-render-setup/Dockerfile`

### 4. Alternatif: GitHub'dan Doğrudan Kullanın

Dockerfile ve diğer dosyaları GitHub'dan yüklemek yerine, Evolution API'nin resmi Docker imajını kullanabilirsiniz.

**render.yaml dosyasını güncelleyin:**
```yaml
services:
  - type: web
    name: evolution-api
    env: docker
    plan: free
    region: oregon
    image: evolution/api:latest
    envVars:
      - key: SERVER_PORT
        value: 8080
      - key: AUTHENTICATION_TYPE
        value: apikey
      - key: AUTHENTICATION_API_KEY
        generateValue: true
      - key: AUTHENTICATION_EXAMPLE_INSTANCE
        value: api
```

### 5. En Basit Çözüm: Dockerfile Kullanmadan

Render.com'da "Build & Deploy" ayarlarında:
- Runtime: Docker yerine "Node" seçin
- Build Command: `git clone https://github.com/EvolutionAPI/evolution-api.git && cd evolution-api && npm install`
- Start Command: `cd evolution-api && npm start`

## Hızlı Test

GitHub repo'nuzun URL'ini verirseniz, yapıyı kontrol edip size net çözüm söyleyebilirim.
