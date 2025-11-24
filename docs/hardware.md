# Donanım ve Devre Şeması

Bu dosyada NodeMCU, LDR ve LED devresinin bağlantıları açıklanmaktadır.

## 🟦 1) Devre Şeması

**Kullanılan bileşenler:**

* NodeMCU ESP8266
* LDR (foto direnç)
* 10kΩ direnç
* LED (lamba)
* USB güç

**Bağlantılar:**

### 📌 LDR + 10k Direnç

* LDR’nin bir ucu → **3.3V**
* LDR’nin diğer ucu → **A0** ve **10k direncin bir ucu**
* 10k direncin diğer ucu → **GND**

Özetle:
LDR ve 10k direnç seri bağlı → ara noktası A0 girişine gidiyor.

### 📌 LED (Lamba)

* LED + (anot) → **D5 GPIO14**
* LED – (katot) → **GND**

> LED ileri yön akımı için 220Ω direnç kullanılması önerilir (NodeMCU 3.3V çıkış verdiği için dirençsiz kullanılmıştır).

## 📷 Devre Görseli

Görseli şu yere yükleyin:
`assets/hardware/nodeMCU.png`
