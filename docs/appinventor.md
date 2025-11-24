# App Inventor – Tasarım ve Blok Kodlama

Bu doküman App Inventor içinde yapılan tasarım ve blok yapısını açıklar.

## 🟦 1) Arayüz Tasarımı

Ekranda bulunan bileşenler:

* Lamba resmi (Image)
* LDR değerini gösteren Label
* MQTT Client component (UrsPahoMqttClient)
* Connect / Disconnect butonları

📷 Görsel:

 <img src="../assets/appinventor/app.png" height="450" width="252">

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
![UrsPahoMqttClient1 ConnectionStateChanged](../assets/appinventor/UrsPahoMqttClient1.ConnectionStateChanged.png)
![UrsPahoMqttClient1 MessageRecieved](../assets/appinventor/UrsPahoMqttClient1.MessageRecieved.png)
![Buton1 Click](../assets/appinventor/Buton1.Click.png)
![Image1 Click](../assets/appinventor/Image1.Click.png)