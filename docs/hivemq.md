# HiveMQ Cloud – Adım Adım Kurulum ve Kullanım Rehberi

Bu rehber, HiveMQ Cloud üzerinde ücretsiz bir MQTT broker oluşturma, erişim yönetimi (Access Management), kullanıcı adı/şifre (Credentials) oluşturma ve WebClient üzerinden bağlanarak topic mesajlarını dinleme işlemlerini anlatır.

Her adım, oluşturduğunuz ekran görüntüleriyle birebir uyumludur.

---

## 1. HiveMQ Cloud’a Kayıt Olma

### **1.1. Anasayfa – Start Free**
HiveMQ Cloud ana sayfasında **Start Free** butonuna basın.  
![Görsel 1](../assets/hivemq/HiveMQ01.png)

### **1.2. Get Started – Sign Up Free Now**
Açılan sayfada **Sign Up Free Now** butonuna tıklayın.  
![Görsel 2](../assets/hivemq/HiveMQ02.png)

### **1.3. E-posta Adresi Girme**
E-posta adresinizi yazıp **Continue** butonuna tıklayın.  
![Görsel 3](../assets/hivemq/HiveMQ03.png)

### **1.4. Hesap Şifresi Oluşturma**
Karşınıza gelen “Create your account” ekranında şifrenizi belirleyip **Continue** butonuna basın.  
![Görsel 4](../assets/hivemq/HiveMQ04.png)

### **1.5. E-posta Doğrulama Uyarısı**
HiveMQ, e-posta adresinize gönderilen doğrulama mesajını onaylamanızı ister.  
![Görsel 5](../assets/hivemq/HiveMQ05.png)

### **1.6. Mail Üzerinden Hesap Doğrulama**
E-posta kutunuza gelen mesajdaki **Confirm my Account** butonuna tıklayın.  
![Görsel 6](../assets/hivemq/HiveMQ06.png)

---

## 2. İlk Bilgilerin Girilmesi

### **2.1. Kullanıcı Bilgileri Formu**
Ad, soyad, job title ve company bilgilerinizi girerek **Continue** butonuna basın.  
![Görsel 7](../assets/hivemq/HiveMQ07.png)

### **2.2. Plan Seçimi Ekranı**
“Select the HiveMQ Cloud Plan you need” ekranı açılır; aşağıya kaydırarak Serverless bölümüne ulaşın.  
![Görsel 8](../assets/hivemq/HiveMQ08.png)

---

## 3. Serverless Cluster Oluşturma

### **3.1. Create Serverless Cluster**
“Compare Features” bölümünde **Serverless** planı altında **Create Serverless Cluster** butonuna tıklayın.  
![Görsel 9](../assets/hivemq/HiveMQ09.png)

### **3.2. Cluster Oluşturuldu – Yönetim Paneli**
Cluster oluşturulduktan sonra “Your Clusters” ekranında **Manage Cluster** butonu görünür.  
![Görsel 10](../assets/hivemq/HiveMQ10.png)

---

## 4. Cluster Bilgileri ve Access Management

### **4.1. Broker Bilgilerini Not Alma**
Cluster panelinde:

- Broker URL  
- TLS Port  

bilgilerini not edin ve **Access Management** sekmesine geçin.  
![Görsel 11](../assets/hivemq/HiveMQ11.png)

---

## 5. Authentication → Credentials Oluşturma

### **5.1. Authentication Ekranı**
Access Management bölümünde **Authentication** sekmesine girip **Edit** butonuna basın.  
![Görsel 12](../assets/hivemq/HiveMQ12.png)

### **5.2. Add Credentials**
Açılan pencerede **Add Credentials** butonuna tıklayın.  
![Görsel 13](../assets/hivemq/HiveMQ13.png)

### **5.3. Kullanıcı Bilgilerini Doldurma**
Açılan formda:

- Username  
- Password  
- Confirm Password  
- Permissions: **Publish & Subscribe**

bilgilerini doldurun ve **Save** butonuna basın.  
![Görsel 14](../assets/hivemq/HiveMQ14.png)

### **5.4. Hesap Oluşturuldu**
Credentials başarıyla oluşturuldu. Şimdi **WebClient** sekmesine geçin.  
![Görsel 15](../assets/hivemq/HiveMQ15.png)

---

## 6. WebClient ile MQTT Bağlantısı

### **6.1. Connection Settings**
WebClient bölümünde oluşturduğunuz username ve password bilgilerini girip **Connect** butonuna basın.  
![Görsel 16](../assets/hivemq/HiveMQ16.png)

### **6.2. Bağlantı Başarılı – Mesajlara Abone Olma**
Bağlantı başarılı olduğunda WebClient “Connected” yazar.  
**Subscribe to all messages** seçeneğini aktif edin.  
![Görsel 17](../assets/hivemq/HiveMQ17.png)

### **6.3. Topic Mesajlarının Görüntülenmesi**
ESP8266 gibi bir cihazdan gönderilen mesajlar artık WebClient üzerinde görünür. Örnek:

- Topic: `esp8266/ldr`
- QoS: 0  
- İçerik: ışık şiddeti değerleri  

![Görsel 18](../assets/hivemq/HiveMQ18.png)