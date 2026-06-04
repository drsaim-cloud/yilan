# 🐍 Yılan Harf Oyunu

Nokia tarzı Türkçe kelime oyunu. Her açılışta yapay zeka yeni kelimeler üretir.

## Kurulum & APK Build

### 1. Gereksinimler
- Node.js 20+
- Java 17
- Android Studio (yerel test için)

### 2. Bağımlılıkları Kur
```bash
npm install
```

### 3. Capacitor Sync
```bash
npx cap sync android
```

### 4. Yerel Debug Build
```bash
cd android
./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/
```

---

## CodeMagic ile Otomatik Build

### Adım 1 — GitHub'a Push
```bash
git init
git add .
git commit -m "ilk commit"
git remote add origin https://github.com/KULLANICI/yilan-harf-oyunu.git
git push -u origin main
```

### Adım 2 — CodeMagic Kurulumu
1. [codemagic.io](https://codemagic.io) → "Add application"
2. GitHub hesabını bağla → bu repoyu seç
3. "Flutter/React Native/Other" → **Other** seç
4. `codemagic.yaml` kullanılacak otomatik

### Adım 3 — Keystore (Release için)
1. CodeMagic → App → **Code Signing** → Android
2. Yeni keystore oluştur veya mevcut `.jks` yükle
3. Referans adını `codemagic.yaml` içindeki `keystore_reference` ile eşleştir

### Adım 4 — Build Başlat
- **Debug APK**: `android-debug` workflow'unu seç → Start build
- **Release APK**: `android-release` workflow'unu seç → Start build

APK build bitince e-posta gelir, CodeMagic panelinden indirilir.

---

## Oyun Özellikleri
- Her açılışta AI (Claude) yeni Türkçe kelime deposu üretir
- Yılanı yönlendir, harfleri sırayla ye
- Harf sayısı × 6 saniye süre
- Doğru harf → +2 sn | Yanlış → −4 sn
- Turlar ilerledikçe kelimeler uzar
- 4 farklı skin: Nokia / Cyberpunk / Amber / Game Boy
- Web Audio API ses efektleri

## Proje Yapısı
```
yilan-harf-oyunu/
├── www/
│   └── index.html          # Oyun (tek dosya)
├── android/                # Capacitor Android projesi
│   ├── app/
│   │   ├── build.gradle
│   │   └── src/main/
│   │       ├── AndroidManifest.xml
│   │       ├── java/com/yilanharf/oyunu/MainActivity.java
│   │       └── res/
│   ├── build.gradle
│   └── settings.gradle
├── capacitor.config.ts
├── package.json
├── codemagic.yaml          # CI/CD config
└── .gitignore
```
