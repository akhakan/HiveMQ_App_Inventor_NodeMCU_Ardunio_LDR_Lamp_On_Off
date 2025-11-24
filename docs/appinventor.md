# App Inventor – Tasarım ve Blok Kodlama

Bu doküman App Inventor içinde yapılan tasarım ve blok yapısını açıklar.

## 🟦 1) Arayüz Tasarımı

<table>
<tr>
<td>

<strong>Ekranda bulunan bileşenler:</strong>
<ul>
<li>MQTT AMP11A PROJECT yazan başlığını gösteren etiket <strong>(Label1)</strong></li>
<li>Lamba resmi <strong>(Image1)</strong></li>
<li>LAMBA KAPALI / LAMBA AÇIK  değerlerini gösteren etiket <strong>(Label2)</strong></li>
<li>LDR resmi <strong>(Image2)</strong></li>
<li>IŞIK ŞİDDETİ başlığını gösteren etiket <strong>(Label3)</strong></li>
<li>LDR değerini gösteren etiket <strong>(Label4)</strong></li>
<li>Bağlan / Bağlantıyı Kes butonu <strong>(Button1)</strong></li>
<li>MQTT Client komponenti <strong>(UrsPahoMqttClient1)</strong></li>
<li>Uyarılar göstermek için Notifier komponenti <strong>(Notifier1)</strong></li>
<li><strong>(Son 2 komponent görselde gözükmemektedir, gizlidir.)</strong></li>
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

MQTT bağlantısını gerçekleştirebilmek için <strong>UrsPahoMqttClient.aix</strong> eklentisinin App Inventor projesine eklenmesi gerekmektedir.
Öncelikle eklentiyi indirmek için şu bağlantıya tıklayın:
[UrsPahoMqttClient.aix indirme sayfası](https://ullisroboterseite.de/android-AI2-PahoMQTT.html)

İndirme tamamlandıktan sonra, Görsel 2’de gösterildiği gibi App Inventor arayüzünde:

Extensions → Import Extension → Choose File adımlarını izleyerek .aix dosyasını projenize dahil edebilirsiniz.

<table>
<tr>
<td width="875">
<strong>MQTT Bağlantısı (UrsPahoMqttClient1 özellikleri doldurulacaktır)</strong>
<ul>
<li>Sunucu adresi → HiveMQ cluster host<br/><strong>Broker :</strong> ****************************.s1.eu.hivemq.cloud</li>
<li>ClientID → Rastgele(random) bir isim verilebilir.<br/><strong>ClientID :</strong> AI2-Phone</li>
<li>Port(TLS) → 8883<br/><strong>Port :</strong> 8883</li>
<li>Kullanıcı adı → oluşturulan credential username<br/><strong>UserName :</strong> ****************</li>
<li>Şifre → credential userpassword<br/><strong>UserPassword :</strong> ****************</li>
</ul>
</td>
<td width="104">
<strong>📷 Görsel 1:</strong><br>
<img src="../assets/appinventor/UrsPahoMqttClient1.jpg" height="473" width="84">
</td>
</tr>
</table>

<table>
<tr>
<td>
<strong>📷 Görsel 2:</strong><br>
<img src="../assets/appinventor/appinventor1.png" height="382" width="953">
</td>
</tr>
<tr>
<td>
<strong>📷 Görsel 3:</strong><br>
<img src="../assets/appinventor/appinventor2.png" height="382" width="953">
</td>
</tr>
</table>

# App Inventor – MQTT Bloklarının Ayrıntılı Açıklaması

Aşağıdaki bloklar, uygulamanın MQTT bağlantısını yönetme, LDR değerini alma ve lambayı kontrol etme işlevlerini yerine getirir. Her blok kendi görseliyle birlikte ayrı bölümde açıklanmıştır.

---

## 1️⃣ MQTT Oturum Kontrolü – `Button1.Click`

Kullanıcı butona bastığında MQTT broker’a bağlanma veya bağlantıyı kesme işlemi burada yönetilir.

### 📷 Blok Görseli

![Buton1 Click](../assets/appinventor/Buton1.Click.png)

### 🔍 Teknik Açıklama
- **IsConnected** → MQTT istemcisinin broker ile aktif oturumu var mı?
- **Connect()** → TLS kullanarak güvenli MQTT bağlantısı kurar.
- **Disconnect()** → Mevcut MQTT oturumunu temiz şekilde kapatır.
- **CleanSession = true**  
  - Önceki MQTT oturumu silinir.  
  - Eski abonelikler ve bekleyen mesajlar temizlenir.

### 🧠 Ne İşe Yarar?
Kullanıcı uygulamadan HiveMQ Cloud’a bağlanır → Arduino verileri gönderebilir, uygulama mesaj alabilir.

---

## 2️⃣ Bağlantı Durumu İzleme ve Abone Olma – `UrsPahoMqttClient1.ConnectionStateChanged`

Bu blok, bağlantı kurulunca veya kopunca otomatik tetiklenir.

### 📷 Blok Görseli

![UrsPahoMqttClient1 ConnectionStateChanged](../assets/appinventor/UrsPahoMqttClient1.ConnectionStateChanged.png)

### 🔍 Teknik Açıklama

**Bağlantı başarılı ise:**
- `Button1.Text` ine **BAĞLANTIYI KES** yazılır.
- `esp8266/ldr` topic’ine **Subscribe** edilir.
- **QoS = 0** → hızlı, tekrarsız, “best effort” iletim.

**Bağlantı başarısız ise:**
- `Button1.Text` ine **BAĞLAN** yazılır.

### 🧠 Ne İşe Yarar?
Uygulama broker’a bağlandığını anlar → sensör verilerini almaya başlar.

---

## 3️⃣ LDR Değerini Dinleme – `UrsPahoMqttClient1.MessageReceived`

ESP8266 tarafından gönderilen LDR ölçüm değeri burada yakalanır.

### 📷 Blok Görseli

![UrsPahoMqttClient1 MessageRecieved](../assets/appinventor/UrsPahoMqttClient1.MessageRecieved.png)

### 🔍 Teknik Açıklama

| Parametre | Açıklama |
|----------|----------|
| **Topic** | Mesajın geldiği MQTT kanalı |
| **Message / Payload** | Gönderilen veri içeriği (örn: `"412"`) |
| **RetainFlag** | Broker mesajı saklıyor mu? |
| **DupFlag** | Mesaj tekrar mı gönderildi? |

### 🧠 Ne İşe Yarar?
- **Topic `esp8266/ldr` ise** → gelen veri LDR ölçümüdür.  
- Bu değer Label4 üzerinde gösterilir.  
- Arduino genelde her 2–3 saniyede bir LDR değeri yayınlar → App Inventor bu blokta yakalar.

---

## 4️⃣ Lamba Kontrolü – `Image1.Click`

Kullanıcı lamba resmine tıkladığında ESP8266’ya `"ON"` veya `"OFF"` komutu gönderilir.

### 📷 Blok Görseli

![Image1 Click](../assets/appinventor/Image1.Click.png)

### 🔍 Teknik Açıklama
İki görsel durum bulunur:

- `turnon.png` → lamba **açık**
- `turnoff.png` → lamba **kapalı**

Tıklama sonrası:

- Eğer lamba kapalı ise `"esp8266/client"` → `"ON"` publish edilir → Görsel(Image1.Picture) açık lambayla değiştirilir → “Lamba Açık” yazısı Label2.Text'te güncellenir
- Eğer lamba açık ise `"esp8266/client"` → `"OFF"` publish edilir → Görsel(Image1.Picture) kapalı lambayla değiştirilir → “Lamba Kapalı” yazısı Label2.Text'te güncellenir
- Eğer bağlantı yoksa → Bildirimde “MQTT aracısına bağlanamadı” mesajı görüntülenir

### 🧠 Ne İşe Yarar?
- `"esp8266/client" → "ON"` → Arduino LED pini HIGH → lamba yanar  
- `"esp8266/client" → "OFF"` → Arduino LED pini LOW → lamba söner  

App Inventor üzerinden gerçek donanım kontrolü bu blok sayesinde yapılır.

---

# 📌 Özet Tablo

| Blok | Amacı | Topic | Yayın / Abone | Beklenen Payload |
|------|--------|--------|----------------|------------------|
| **Button1.Click** | MQTT Connect / Disconnect | — | — | — |
| **ConnectionStateChanged** | Bağlantı sonrası abonelik | `esp8266/ldr` | Subscribe (QoS0) | — |
| **MessageReceived** | Gelen LDR değerini ekrana yaz | `esp8266/ldr` | Alıcı | `"412"` (string sayı) |
| **Image1.Click** | Lambayı aç/kapa komutu gönder | `esp8266/client` | Publish | `"ON"` / `"OFF"` |