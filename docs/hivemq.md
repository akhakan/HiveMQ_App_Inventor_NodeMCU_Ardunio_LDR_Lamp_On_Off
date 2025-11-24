# NodeMCU + App Inventor + HiveMQ — Proje

## Kısa açıklama

Bu proje, bir NodeMCU (ESP8266) cihazından gelen LDR/veri verilerini HiveMQ üzerinden App Inventor ile görüntülemeyi/işlemeyi gösterir. Bu repo hem NodeMCU tarafı kodunu, hem App Inventor uzantı/ayarlarını hem de HiveMQ üzerinde nasıl bağlantı kurup topic dinleneceğini içerir.

## İçindekiler

- [NodeMCU + App Inventor + HiveMQ — Proje](#nodemcu--app-inventor--hivemq--proje)
  - [Kısa açıklama](#kısa-açıklama)
  - [İçindekiler](#i̇çindekiler)
  - [Proje hakkında](#proje-hakkında)
  - [Hızlı Başlangıç](#hızlı-başlangıç)
  - [HiveMQ — kısa özet (README için)](#hivemq--kısa-özet-readme-için)
  - [Dosya yapısı önerisi](#dosya-yapısı-önerisi)
  - [Katkıda bulunma](#katkıda-bulunma)
  - [Lisans](#lisans)

## Proje hakkında

Bu repo, NodeMCU ile MQTT üzerinden veri göndermeyi, HiveMQ Cloud/Cloud demo paneli ile bu verileri dinlemeyi ve App Inventor ile mobil arayüzde göstermeyi adım adım gösterir. Amacım: yeni başlayanların HiveMQ üzerinde güvenli (credential/auth) bağlantı kurmasını kolaylaştırmak.

## Hızlı Başlangıç

1. Gereksinimler

   * NodeMCU (ESP8266) + USB kablo
   * Arduino IDE (ESP8266 kart paketi yüklü)
   * App Inventor (proje dosyaları / .aia)
   * HiveMQ hesabı (ücretsiz plan yeterli)

2. NodeMCU kodunu yükle

   * `src/` klasöründeki `.ino` dosyasındaki Wi-Fi ve MQTT bilgilerini kendi değerlerinle değiştir.
   * Seri monitör üzerinden cihazın bağlandığını ve publish/subscribe işlemlerini doğrula.

3. App Inventor

   * `app/` klasöründeki blokları kullanarak MQTT uzantısı ile broker'a bağlan.
   * LDR değerlerini ekranda göster.

4. HiveMQ (özet)

   * HiveMQ'ya üye ol, bir cluster oluştur, Access Management ve Authentication Credentials ayarlarını yap.
   * Web Client veya Connection Settings kullanarak oluşturduğun credential ile broker'a bağlan ve `esp8266/ldr` gibi topicleri dinle.
   * Bu adımların detaylı resimli açıklaması için: **[HiveMQ detaylı rehberi → hivemq.md](./hivemq.md)**

## HiveMQ — kısa özet (README için)

HiveMQ tarafında temel akış:

* Hesap oluşturma → Oturum açma.
* Yeni bir cluster (veya sandbox) oluşturma.
* Access Management (kullanıcı/role/permission) ile topic izni tanımlama.
* Authentication Credentials (username/password veya token) oluşturma.
* Web Client sekmesinden ya da kendi Connection Settings'inden (MQTT client) broker'a bağlanıp topicleri dinleme.
  Detaylı, ekran görüntülü adımlar ve örnek ekranlar için `hivemq.md` dosyasına bakın.

## Dosya yapısı önerisi

```
/ (repo root)
├─ README.md
├─ hivemq.md
├─ src/
│  └─ esp8266_ldr.ino
├─ app/
│  └─ app_inventor_export.aia
├─ assets/
│  └─ hivemq/
│     ├─ 01_signup.png
│     ├─ 02_create_cluster.png
│     ├─ 03_access_management.png
│     ├─ 04_create_credentials.png
│     ├─ 05_webclient_listen.png
│     └─ ...
└─ LICENSE
```

## Katkıda bulunma

Pull request ve issue’lara açığım. Lütfen sensör/uzantı/ek açıklama eklemeden önce bir issue açıp ne ekleyeceğini belirt.

## Lisans

[MIT](LICENSE) — serbestçe kullanabilirsiniz.

---

Daha detaylı HiveMQ kurulum/ekran görüntüleri için: **[hivemq.md](./hivemq.md)**
İstersen bu README'i repo ayarlarına göre kısaltıp rozetler (badges) veya GIF ekleyebilirim.


