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

- Comparación con otras herramientas (BlueJammer y Pwnagotchi):
A diferencia de un Jammer tradicional, que ataca la capa física inundando el entorno con ruido electromagnético para que ninguna señal pueda transmitirse, o de un Pwnagotchi, que ataca la seguridad intentando capturar los handshakes para descifrar contraseñas, un ESP32 Deauther no hace ruido ni roba claves. Su objetivo es realizar un ataque de Denegación de Servicio (DoS) interfiriendo lógicamente en la comunicación entre un router WiFi y los dispositivos conectados a él.

- ¿Cómo interfiere? (La vulnerabilidad):
El Deauther aprovecha una vulnerabilidad histórica en el protocolo IEEE 802.11 (WiFi). En las redes WPA y WPA2 tradicionales, los datos de navegación viajan encriptados, pero las llamadas Tramas de Gestión (Management Frames —los mensajes que el router y el dispositivo usan para decir "me conecto" o "me desconecto"—) viajan en texto plano y no requieren validación de identidad.

- El proceso de ataque (MAC Spoofing):
Al aprovechar que estas tramas de desconexión no tienen contraseña, el Deauther utiliza una técnica de falsificación de identidad (MAC Spoofing). Supongamos un caso en donde un router le brinda WiFi a un dispositivo. Al activar el Deauther contra esa red, sucede lo siguiente:

  - El Deauther clona la identidad del dispositivo y le dice al router: "Hola, soy el dispositivo y me voy a desconectar".

  - Simultáneamente, clona la identidad del router y le dice al dispositivo: "Hola, soy el router y te voy a desconectar".

- El alcance del ataque:
Este proceso lo realiza enviando estos paquetes de forma continua y repetitiva. El Deauther puede hacer esto contra un solo equipo en particular (ataque Unicast) o enviar una orden global (ataque Broadcast) para afectar a toda la red. Como resultado, provoca que no se pueda entablar o mantener una comunicación WiFi con el router víctima desde ningún dispositivo.

- Aclaración sobre redes modernas:
Cabe destacar que este ataque es infalible en redes WPA/WPA2 estándar, pero las redes más modernas que utilizan WPA3 o que tienen activada la protección PMF (Protected Management Frames / estándar 802.11w) son inmunes. En estos casos modernos, las tramas de desconexión sí están encriptadas, por lo que los dispositivos ignoran el ataque del ESP32.

<br>

### 💻 Firmware
- Existen varios firmwares que convierten ciertos dispositivos en un `Deauther`. En este caso utilizaremos el firmware siguiente:
  - `ESP32 Flash Tool`: https://drive.google.com/file/d/1UuULfBdo3wlgzL6Es9meEfsRHoHqnaKh/view 
  - `BIN Files`: https://drive.google.com/file/d/1CYqyvu_TVEcifmxE-ZX37RlV9JfTKWc7/view


A continuacion les dejo algunos links de videos en donde utilizan otros firmwares de desautenticacion (algunos mas avanzados, que en vez de ser un simple Deauther, pasan a convertir directamente un cierto dispositivo en un `Marauder`, es decir, un Deauther + un adicional de herramientas hacking/pentesting):
  - `ESP32 Marauder (por JustCallMeKoko)` --> https://www.youtube.com/watch?v=bHivs2c_o7I
  - `ESP32 Deauther / GhostESP` --> 
  - `Bruce Firmware` --> https://www.youtube.com/watch?v=1dC_abmQvzA

<br>

### ⚙️ How to install & configure the firmware
En esta parte vamos a ver como instalar, configurar y utilizar el firmware básico seleccionado para este repositorio.
- Una vez descargadas las carpetas de los links de drive de Google proporcionados arriba, vamos a comenzar con la instalacion del `ESP32 FLash Tool`.
- 


<br>

### 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
