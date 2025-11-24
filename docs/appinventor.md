# App Inventor – Tasarım ve Blok Kodlama

Bu doküman App Inventor içinde yapılan tasarım ve blok yapısını açıklar.

## 🟦 1) Arayüz Tasarımı

Ekranda bulunan bileşenler:

* Lamba resmi (Image)
* LDR değerini gösteren Label
* MQTT Client component (UrsPahoMqttClient)
* Connect / Disconnect butonları

📷 Görsel:
`assets/appinventor/app.png`

## 🟦 2) Blok Kodlama

### MQTT Bağlantısı

* Sunucu adresi → HiveMQ cluster host
* Port → 8883
* Kullanıcı adı → oluşturulan credential
* Şifre → credential password

### LDR Değerini Dinleme

`esp8266/ldr` subscribe edilir.
Gelen değer Label içinde güncellenir.

### Lamba Kontrolü

Image tıklandığında:

* Eğer kapalı → `"ON"` publish edilir
* Eğer açık → `"OFF"` publish edilir

📷 Blok görselleri:
`assets/appinventor/UrsPahoMqttClient1.ConnectionStateChanged.png`
`assets/appinventor/UrsPahoMqttClient1.MessageRecieved.png`
`assets/appinventor/Buton1.Click.png`
`assets/appinventor/Image1.Click.png`
