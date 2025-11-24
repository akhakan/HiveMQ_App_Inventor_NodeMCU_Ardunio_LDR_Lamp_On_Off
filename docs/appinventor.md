# App Inventor – Tasarım ve Blok Kodlama

Bu doküman App Inventor içinde yapılan tasarım ve blok yapısını açıklar.

## 🟦 1) Arayüz Tasarımı

<table>
<tr>
<td>

<strong>Ekranda bulunan bileşenler:</strong>
<ul>
<li>MQTT AMP11A PROJECT proje başlığını gösteren etiket (Label1)</li>
<li>Lamba resmi (Image1)</li>
<li>LAMBA KAPALI / LAMBA AÇIK  değerlerini gösteren etiket (Label2)</li>
<li>LDR resmi (Image2)</li>
<li>IŞIK ŞİDDETİ başlığımı gösteren etiket (Label3)</li>
<li>LDR değerini gösteren etiket (Label4)</li>
<li>Bağlan / Bağlantıyı Kes butonları</li>
<li>MQTT Client componenti (UrsPahoMqttClient1)</li>
<li>Uyarılar göstermek için Notifier componenti (Notifier1)</li>
<li>(Son 2 komponent görselde gözükmemektedir, gizlidir.)</li>
</ul>
</td>
<td>

<strong>📷 Görsel:</strong><br>
<img src="../assets/appinventor/app.png" height="450" width="252">

</td>
</tr>
</table>


## 🟦 2) Blok Kodlama

### MQTT Bağlantısı

- Sunucu adresi → HiveMQ cluster host
- Port → 8883
- Kullanıcı adı → oluşturulan credential
- Şifre → credential password

### LDR Değerini Dinleme

`esp8266/ldr` subscribe edilir.
Gelen değer Label içinde güncellenir.

### Lamba Kontrolü

Image tıklandığında:

- Eğer kapalı → `"ON"` publish edilir
- Eğer açık → `"OFF"` publish edilir

📷 Blok görselleri:
![UrsPahoMqttClient1 ConnectionStateChanged](../assets/appinventor/UrsPahoMqttClient1.ConnectionStateChanged.png)
![UrsPahoMqttClient1 MessageRecieved](../assets/appinventor/UrsPahoMqttClient1.MessageRecieved.png)
![Buton1 Click](../assets/appinventor/Buton1.Click.png)
![Image1 Click](../assets/appinventor/Image1.Click.png)
