# 🚀 **ESP32 OTA Firmware Update via MQTT** 📡

Bem-vindo ao projeto de **atualização de firmware OTA no ESP32**! 🛠️ Este código permite que você realize a atualização do firmware do ESP32 remotamente, usando o protocolo **MQTT** e o serviço **GitHub** para armazenar os arquivos de firmware. 😎

## 🌐 **Funcionalidades do Projeto**

- **Conexão Wi-Fi** 📶: O ESP32 conecta-se automaticamente à rede Wi-Fi configurada.
- **Atualização OTA** 🔄: Realiza atualizações de firmware diretamente do GitHub.
- **Controle MQTT** 📲: Controle remoto via mensagens MQTT.
- **Base de Firmware no GitHub** 📁: Os arquivos de firmware estão armazenados no GitHub e podem ser acessados dinamicamente.

---

## 🛠️ **Requisitos**

Antes de começar, você precisará:

- **ESP32**
- **Arduino IDE** (ou outro ambiente de desenvolvimento para ESP32)
- **Bibliotecas do Arduino**:
  - `WiFi.h`
  - `WiFiClientSecure.h`
  - `PubSubClient.h`
  - `HTTPClient.h`
  - `Update.h`

---

## ⚙️ **Configuração do Código**

### 1️⃣ **Conectar à Rede Wi-Fi** 📶
Altere os valores de `ssid` e `password` para as credenciais da sua rede Wi-Fi.

```cpp
const char* ssid = "seu_ssid";
const char* password = "sua_senha_wifi";
```

### 2️⃣ **Configuração do MQTT** 💬
Defina o servidor MQTT e o tópico que o ESP32 irá usar para ouvir as mensagens de atualização de firmware.

```cpp
const char* mqtt_server = "broker.hivemq.com";  // Servidor MQTT
const int mqtt_port = 1883;                      // Porta MQTT
const char* mqtt_topic = "firmware_git";         // Tópico MQTT
```

### 3️⃣ **URL Base do Firmware** 🔗
O código está configurado para baixar o firmware diretamente do GitHub. Se você preferir outra URL, altere a variável `firmware_base_url`.

```cpp
const char* firmware_base_url = "https://raw.githubusercontent.com/PedroKutski/ESP_OTA_MQTT/main/";
```

### 4️⃣ **Configuração do LED** 💡
O LED está configurado para o pino GPIO 2, mas você pode mudar esse valor para outro pino, se necessário.

```cpp
const int ledPin = 2; // Pino GPIO para LED
```

---

## 📱 **Usando o Atom Dashboard para Enviar Comandos MQTT**

### Passo a Passo:

1. **Instalar o Atom Dashboard**:
   - Baixe o aplicativo Atom Dashboard no seu dispositivo (disponível para Android).

2. **Configurar o Broker MQTT**:
   - Defina o servidor MQTT: `broker.hivemq.com`
   - Defina a porta MQTT: `1883`

3. **Enviar Comando MQTT**:
   - Publique uma mensagem com o nome do arquivo de firmware para o tópico `firmware_git`.
   
   Exemplo de mensagem:
   ```
   firmware_v1.bin
   ```
   O ESP32 irá automaticamente baixar o arquivo do GitHub e iniciar a atualização.

---

## 🔄 **Fluxo de Atualização OTA**

1. **Conexão Wi-Fi** 📡: O ESP32 conecta-se à rede Wi-Fi configurada.
2. **Conexão MQTT** 🔗: O ESP32 conecta-se ao broker MQTT e escuta o tópico `firmware_git`.
3. **Recebendo a Mensagem** 💬: Quando o ESP32 recebe a mensagem MQTT com o nome do arquivo de firmware, ele inicia o download.
4. **Atualização de Firmware** 🔄: O ESP32 baixa o firmware, grava na memória e reinicia automaticamente para concluir a atualização.

---

## 📚 **Bibliotecas Usadas**

- [WiFi.h](https://github.com/esp8266/Arduino/tree/master/libraries/WiFi) – Para conectar o ESP32 à rede Wi-Fi.
- [WiFiClientSecure.h](https://github.com/esp8266/Arduino/tree/master/libraries/WiFiClientSecure) – Para usar conexões seguras (HTTPS).
- [PubSubClient.h](https://github.com/knolleary/pubsubclient) – Cliente MQTT para o ESP32.
- [HTTPClient.h](https://github.com/esp8266/Arduino/tree/master/libraries/ESP8266HTTPClient) – Para realizar requisições HTTP.
- [Update.h](https://github.com/espressif/arduino-esp32/tree/master/libraries/Update) – Para realizar a atualização OTA.

---

## 📝 **Precauções**

⚠️ **Cuidado ao Enviar o Arquivo de Firmware!**  
Verifique se o arquivo de firmware que você está enviando é compatível com o seu ESP32. Certifique-se de que o arquivo esteja corretamente armazenado no repositório GitHub.

🔒 **Segurança**  
Este projeto utiliza comunicação HTTPS (via `WiFiClientSecure`), mas como a conexão MQTT não é criptografada neste exemplo, é recomendável usá-lo em redes seguras ou configurar TLS/SSL no broker MQTT para garantir uma comunicação segura.

---

## 🖊️ **Licença**

Este projeto está licenciado sob a [MIT License](LICENSE).  
Sinta-se à vontade para modificar e distribuir este código!

---

## 🎉 **Contribua!**

Se você encontrar algum erro ou tiver sugestões de melhorias, abra uma **issue** ou envie um **pull request**! 😊
  
