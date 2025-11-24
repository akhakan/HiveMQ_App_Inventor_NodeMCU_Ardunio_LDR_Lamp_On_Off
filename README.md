# NodeMCU – App Inventor – HiveMQ Akıllı Aydınlatma Projesi

<table>
<tr>
<td>
Bu proje; **NodeMCU**, **LDR** sensörü, **LED lamba**, **HiveMQ MQTT brokeri** ve **App Inventor Android uygulaması** kullanılarak oluşturulmuş bir IoT uygulamasıdır.
<li>Sensörden okunan **ışık şiddeti verileri** HiveMQ’ya gönderilir.</li>
<li>App Inventor uygulaması HiveMQ üzerinden bu değeri **canlı olarak** takip eder.</li>
<li>Uygulamadaki **lamba ikonuna basıldığında**, MQTT üzerinden NodeMCU’ya komut gönderilir ve fiziksel LED açılır/kapanır.</li>
</ul>
</td>
<td>
<img src="assets/appinventor/app.png" height="450" width="252">
</td>
<td>
<img src="assets/hardware/nodeMCU.png" height="450" width="427">
</td>
</tr>
</table>


Bu proje; **NodeMCU**, **LDR** sensörü, **LED lamba**, **HiveMQ MQTT brokeri** ve **App Inventor Android uygulaması** kullanılarak oluşturulmuş bir IoT uygulamasıdır.

* Sensörden okunan **ışık şiddeti verileri** HiveMQ’ya gönderilir.
* App Inventor uygulaması HiveMQ üzerinden bu değeri **canlı olarak** takip eder.
* Uygulamadaki **lamba ikonuna basıldığında**, MQTT üzerinden NodeMCU’ya komut gönderilir ve fiziksel LED açılır/kapanır.

## 🚀 Özellikler

* Gerçek zamanlı MQTT haberleşmesi
* LDR sensör verisi izleme
* Mobil uygulamadan LED kontrolü
* HiveMQ Cloud ile güvenli bağlantı
* Tam açık kaynak kod

## 📘 Detaylı Belgelendirme

Aşağıdaki teknik dokümanlarla proje adım adım açıklanmıştır:

| Bölüm                            | Açıklama                                | Dosya                                   |
| -------------------------------- | --------------------------------------- | --------------------------------------- |
| Donanım ve devre şeması          | LDR + LED + NodeMCU bağlantıları        | [hardware.md](./docs/hardware.md)       |
| Arduino/ESP8266 MQTT kodları     | Kodlar + satır satır açıklama           | [arduino.md](./docs/arduino.md)         |
| App Inventor arayüz & bloklar    | Tasarım + block ekranı                  | [appinventor.md](./docs/appinventor.md) |
| HiveMQ kurulum rehberi           | Üyelik, cluster, credential, web client | [hivemq.md](./docs/hivemq.md)           |
| Mobil uygulama ekran görüntüleri | Açma-kapama, sensör verisi, video       | [mobileapp.md](./docs/mobileapp.md)     |

## 🎥 Demo Videosu

🟡 Video: Mobil uygulama üzerinden LED aç/kapa + canlı sensör verisi
(YouTube linki ekleyebilirsiniz)

## 📦 Proje Klasör Yapısı

```
/docs/*.md          → Ayrıntılı anlatımlar
/assets/...         → Tüm görseller
/src/               → Arduino/ESP8266 kodları
/app/               → App Inventor .aia dosyası
```