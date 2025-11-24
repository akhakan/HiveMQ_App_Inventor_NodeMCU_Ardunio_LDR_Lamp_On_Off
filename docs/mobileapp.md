# Mobil Uygulama – Ekran Görüntüleri ve Video

Bu dosya, App Inventor ile oluşturulan mobil uygulamanın çalışma görüntülerini içerir.

## 🟦 1) LED Durum Görselleri

* Gri ampul → LED kapalı
* Sarı ampul → LED açık

📷 Görseller:

<div style="display:flex; gap:10px;">
    <img src="../assets/mobile/turnoff.png" height="150" width="93">
    <img src="../assets/mobile/turnon.png" height="150" width="93">
</div>


## 🟦 2) LDR Sensör Verisi

Uygulama içinde canlı olarak güncellenir.
Örnek:

```
Işık Şiddeti: 412
```

📷 Görsel:

![App 1](../assets/mobile/app_1.png)
![App 2](../assets/mobile/app_2.png)
![App 3](../assets/mobile/app_3.png)


## 🟦 3) Uygulama Videosu

## 🎥 Uygulama Videosu

<video src="../assets/mobile/app_video.mp4" width="360" controls>
Tarayıcınız video oynatmayı desteklemiyor.
</video>

➡️ [Uygulama videosunu izlemek için tıklayın](../assets/mobile/app_video.mp4)

`https://github.com/kullanici/proje/blob/main/assets/mobile/app_video.mp4`


Video açıklaması:

* Lamba ikonuna tıklayınca LED yanıyor/sönüyor
* Ekrandaki sensör değeri gerçek zamanlı değişiyor

## 🟦 4) Tam Uygulama Akışı

1. Uygulama açılır → MQTT’ye bağlanır
2. LDR değerleri akar
3. Lamba ikonuna basılır → LED değişir
4. HiveMQ üzerinden tüm iletişim canlı gerçekleşir
