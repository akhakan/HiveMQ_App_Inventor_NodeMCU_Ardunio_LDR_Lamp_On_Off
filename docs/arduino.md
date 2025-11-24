# Arduino (NodeMCU) Kodları ve Açıklamalar

Bu dosya NodeMCU’nun HiveMQ’ya bağlanması, LDR okumaları göndermesi ve App Inventor’dan gelen LED kontrol komutlarını dinlemesi için hazırlanan kodu açıklar.

## 🟦 1) Kod Dosyası

Kodun tamamı:
`src/ldr_btn_mqtt.ino`

*(Kodun içeriğini buraya da ekleyebilirsin.)*

## 🟦 2) Temel Özellikler

* Wi-Fi’ye bağlanır
* HiveMQ Cloud’a TLS üzerinden bağlanır
* `esp8266/ldr` topic’ine sensör verisi gönderir
* `esp8266/client` topic’inden LED komutu alır

## 🟦 3) LDR Okuma

A0 pininden analog değer okunur.
Veri publish edilir:

```
client.publish("esp8266/ldr", String(ldrValue).c_str());
```

## 🟦 4) LED Kontrolü

App Inventor’dan gelen mesaj:

* `"ON"` → LED yanar
* `"OFF"` → LED söner

## 📷 Kod ekran görüntüsü

![arduino kodu](../assets/arduino/arduino_code.png)
