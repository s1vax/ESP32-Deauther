# ESP32 Deauther (Vulnerability of the IEEE 802.11 [Wi-Fi] protocol)

<p align="center">
<img width="400" height="400" alt="WhatsApp Image 2026-04-24 at 13 24 49" src="https://github.com/user-attachments/assets/46b4acf7-1e7c-4fc7-942b-5421066de235" />
</p>

## ⚖️ Legal Disclaimer
The creator of this repository is not responsible for any malicious or inappropriate use of the device described. It is strictly prohibited to interfere with other Wi-Fi networks without consent or adequate security measures.

<br>

## ✅ Safe environments and measures
The Deauther attack can be directed at a personal network as a proof of use. The repository will explain in detail how to achieve this.

<br>

## 🛒 Things we need
- `ESP32 WROOM` (any version)
- `PC` for firmware flashing & attack configuration
- `USB Micro-USB a USB cable`

<br>


## 🔎 Step by step

### ❓How it works?
Comparison with a "Pwnagotchi" and a "BlueJammer". 

Este dispositivo no interfiere con ruido electromagnetico, como el BlueJammer, ni tampoco ataca a los handshakes, como el Pwnagotchi. Este ESP32 Deauther interfiere en la comunicacion de un router WIFI y otro dispositivo. 

¿Como interfiere? Aprovechando la vulnerabilidad en el protocolo IEEE 802.11 (WIFI). De una forma sencilla realiza lo siguiente:
- Suponemos un caso en donde un router brinda WIFI a un dispositivo en concreto. Al activar el Deauther con un SSID objetivo (proporcionado por el router) sucede que:
  - El Deuather al router, le dice: "Hola, soy el dispositivo y me voy a desconectar"
  - Y el Deauther al dispositivo, le dice: "Hola, soy el router y te voy a desconectar"

Este proceso lo realiza de forma repetitiva, provocando que no se pueda entablar una comunicacion WIFI con el router victima, desde ningun dispositivo que se intente conectar o estaba conectado a la red.

<br>

### 💻 Firmware

<br>


### 🧊 3D Cases

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
