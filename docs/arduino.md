# Arduino (NodeMCU) Kodları ve Açıklamalar

Bu dosya NodeMCU’nun HiveMQ’ya bağlanması, LDR okumaları göndermesi ve App Inventor’dan gelen LED kontrol komutlarını dinlemesi için hazırlanan kodu açıklar.

## 🟦 1) Kod Dosyası

Kodu Ardunio IDE'ye attıktan sonra: ***** içeren kısımlar yazılımı yükleyen kişinin değerleriyle değiştirilmelidir.

```cpp
// ---- WiFi Ayarları ----
const char* ssid = "***********************";
const char* password = "*******************";

// ---- HiveMQ Cloud ----
const char* mqtt_server = "****************************.s1.eu.hivemq.cloud";
const int mqtt_port = 8883;
const char* mqtt_user = "****************";
const char* mqtt_pass = "****************"; 
```

Kodun tamamı:
`src/ldr_btn_mqtt.ino`

```cpp
#include <ESP8266WiFi.h>
#include <WiFiClientSecureBearSSL.h>
#include <PubSubClient.h>

// ---- WiFi Ayarları ----
const char* ssid = "***********************";
const char* password = "*******************";

// ---- HiveMQ Cloud ----
const char* mqtt_server = "****************************.s1.eu.hivemq.cloud";
const int mqtt_port = 8883;
const char* mqtt_user = "****************";
const char* mqtt_pass = "****************";

// ---- MQTT ----
WiFiClientSecure espClient;
PubSubClient client(espClient);

// Topic'ler
const char* mqtt_topic_pub = "esp8266/ldr";     // LDR yayınlayan topic
const char* mqtt_topic_sub = "esp8266/client";  // ON/OFF dinlenen topic

// ---- LED ----
#define LED_PIN D5   // GPIO14

// ---- Callback ----
void callback(char* topic, byte* payload, unsigned int length) {

  String message = "";
  for (int i = 0; i < length; i++) {
    message += (char)payload[i];
  }

  Serial.print("Gelen mesaj -> ");
  Serial.println(message);

  // ----- LED KONTROL -----
  if (String(topic) == mqtt_topic_sub) {
    if (message == "ON") {
      digitalWrite(LED_PIN, HIGH);
      Serial.println("LED YAKILDI");
    } 
    else if (message == "OFF") {
      digitalWrite(LED_PIN, LOW);
      Serial.println("LED KAPATILDI");
    }
  }
}

// ---- MQTT Bağlantısı ----
void reconnect() {
  while (!client.connected()) {
    Serial.print("MQTT baglaniyor... ");

    String clientId = "ESP8266-" + String(ESP.getChipId());

    if (client.connect(clientId.c_str(), mqtt_user, mqtt_pass)) {
      Serial.println("Baglandi!");
      client.subscribe(mqtt_topic_sub);
    } else {
      Serial.print("Hata (rc=");
      Serial.print(client.state());
      Serial.println(") 5 sn sonra tekrar...");
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  delay(100);

  // ---- LED ----
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);  // başlangıçta kapalı

  // ---- WiFi ----
  WiFi.begin(ssid, password);
  Serial.print("WiFi baglaniyor...");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi BAGLANDI");

  // ---- TLS devre dışı ----
  espClient.setInsecure();

  // ---- MQTT ----
  client.setServer(mqtt_server, mqtt_port);
  client.setCallback(callback);
}

unsigned long lastMsg = 0;

void loop() {
  if (!client.connected()) reconnect();
  client.loop();

  // Her 3 saniyede bir LDR değeri gönder
  if (millis() - lastMsg > 3000) {
    lastMsg = millis();

    int ldrValue = analogRead(A0);

    // ---- JSON OLMADAN SADE METİN GÖNDER ----
    String payload = String(ldrValue);

    client.publish(mqtt_topic_pub, payload.c_str());

    Serial.print("LDR gönderildi: ");
    Serial.println(payload);
  }
}
```

## 🟦 2) Temel Özellikler

* Wi-Fi’ye bağlanır
* HiveMQ Cloud’a TLS üzerinden bağlanır
* `esp8266/ldr` topic’ine sensör verisi gönderir
* `esp8266/client` topic’inden LED komutu alır

## 🟦 3) LDR Okuma

A0 pininden analog değer okunur.
Veri publish edilir:

```cpp
client.publish("esp8266/ldr", String(ldrValue).c_str());
```

## 🟦 4) LED Kontrolü

App Inventor’dan gelen mesaj:

* `"ON"` → LED yanar
* `"OFF"` → LED söner