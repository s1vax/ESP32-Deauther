# ESP32 Deauther (Vulnerability of the IEEE 802.11 [Wi-Fi] protocol)

<p align="center">
<img width="400" height="400" alt="WhatsApp Image 2026-04-24 at 13 24 49" src="https://github.com/user-attachments/assets/46b4acf7-1e7c-4fc7-942b-5421066de235" />
</p>

## ⚖️ Legal Disclaimer
The creator of this repository is not responsible for any malicious or inappropriate use of the device described. It is strictly prohibited to interfere with other Wi-Fi networks without consent or adequate security measures.

<br>
<br>

## ✅ Safe environments and measures
The Deauther attack can be directed at a personal network as a proof of use. The repository will explain in detail how to achieve this.

<br>
<br>

## 🛒 Things we need
- `ESP32 WROOM` (any version)
- `PC` for firmware flashing & attack configuration
- `USB Micro-USB a USB cable`

<br>
<br>


## ❓How it works?

- ***Comparison with other tools (BlueJammer and Pwnagotchi):*** <br>
Unlike a traditional jammer, which attacks the physical layer by flooding the environment with electromagnetic noise to prevent any signal transmission, or a Pwnagotchi, which attacks security by attempting to capture handshakes to crack passwords, an ESP32 Deauther doesn't make noise or steal keys. Its purpose is to perform a Denial-of-Service (DoS) attack by logically interfering with communication between a Wi-Fi router and the devices connected to it.


- ***¿How does it interfere? (Vulnerability):*** <br>
Deauther exploits a historical vulnerability in the IEEE 802.11 (WiFi) protocol. In traditional WPA and WPA2 networks, browsing data travels encrypted, but Management Frames (the messages the router and device use to say "I'm connecting" or "I'm disconnecting") travel in plain text and do not require identity validation.


- ***The attack process (MAC Spoofing):*** <br>
By taking advantage of the fact that these disconnection frames are not password-protected, the Deauther uses a MAC address spoofing technique. Let's consider a case where a router provides Wi-Fi to a device. When the Deauther is activated against that network, the following occurs:

   - The Deauther clones the device's identity and tells the router: "Hello, I am the device and I am going to disconnect."

   - Simultaneously, it clones the router's identity and tells the device: "Hello, I am the router and I am going to disconnect you."


- ***The scope of the attack:*** <br>
This process is carried out by sending these packets continuously and repeatedly. The deauther can do this against a single device (unicast attack) or send a global command (broadcast attack) to affect the entire network. As a result, it prevents any device from establishing or maintaining a Wi-Fi connection with the victim router.


- ***Clarification on modern networks:*** <br>
Cabe destacar que este ataque es infalible en redes WPA/WPA2 estándar, pero las redes más modernas que utilizan WPA3 o que tienen activada la protección PMF (Protected Management Frames / estándar 802.11w) son inmunes. En estos casos modernos, las tramas de desconexión sí están encriptadas, por lo que los dispositivos ignoran el ataque del ESP32.

<br>
<br>

## 💻 Firmware
- Existen varios firmwares que convierten ciertos dispositivos en un `Deauther`. En este caso utilizaremos el firmware siguiente:
  - `ESP32 Flash Tool`: https://drive.google.com/file/d/1UuULfBdo3wlgzL6Es9meEfsRHoHqnaKh/view 
  - `BIN Files`: https://drive.google.com/file/d/1CYqyvu_TVEcifmxE-ZX37RlV9JfTKWc7/view


A continuacion les dejo algunos links de videos en donde utilizan otros firmwares de desautenticacion (algunos mas avanzados, que en vez de ser un simple Deauther, pasan a convertir directamente un cierto dispositivo en un `Marauder`, es decir, un Deauther + un adicional de herramientas hacking/pentesting):
  - `ESP32 Marauder (por JustCallMeKoko)` --> https://www.youtube.com/watch?v=bHivs2c_o7I
  - `ESP32 Deauther / GhostESP` --> https://www.youtube.com/watch?v=dryQoQLEl90
  - `Bruce Firmware` --> https://www.youtube.com/watch?v=1dC_abmQvzA

<br>
<br>

## ⚙️ How to install & configure the firmware
En esta parte vamos a ver como instalar, configurar y utilizar el firmware básico seleccionado para este repositorio. 

El primer paso de todos es conectar nuestra ESP32 a nuestra PC, luego:

- Instalacion de la herramienta de flasheo
   - Una vez descargadas las carpetas de los links del drive de Google proporcionados mas arriba, vamos a comenzar con la instalacion del `ESP32 FLash Tool`
   - Abrimos la carpeta descomprimida `flash_download_tool_3.9.3`
   - Luego le damos doble click en el archivo `flash_download_tool_3.9.3.exe`
   - Se abriran 2 ventanas (un cmd y una mas pequeña), en la mas pequeña colocamos las opciones de: `ESP32` (en vez de ESP38266) y `Develop`. Le damos en `OK`
   - Cerramos el cmd, y veremos que se abrira otra ventana. Esta es la de la herramienta de flasheo
   
- Instalacion de archivos `.bin`
   - Ahora, abriremos la carpeta llamada `esp32-wifi-penetration-tool-master`
   - Luego vamos a la sub-carpeta llamada `build`. Aqui vamos a encontrar los archivos .bin necesarios
   - Ahora lo que hacemos es: en la ventana de la herramienta de flasheo, le vamos a dar click a los tres puntos que aparecen por cada fila y en una sola columna, para insertar los archivos .bin, y seguido a ello, colocaremos ciertas direcciones de memoria 
   - Al darle click a los tres puntos, se nos abrira el explorador de archivos para selccionar nuestros .bin. En los primeros tres puntos (primera fila) debemos elegir el archivo `partition-table.bin`
   - En los segundos, buscaremos y colocaremos el archivo `bootloader.bin`
   - Y por ultimo, en los puntos de la tercera fila, buscaremos y colocaremos el archivo `esp32-wifi-penetration-tool.bin`
   - Como mencionamos, ahora colocaremos las direcciones de memoria en la columna que esta al lado de la columna de los tres puntos. Las direcciones que debemos colocar son:
       - Primera fila --> 0x8000
       - Segunda fila --> 0x1000
       - Tercera fila --> 0x10000
   - Por ultimo, le damos click a las 3 casillas que se encuentran en la primera columna (deben salir en verde las filas luego de esto)

- En la parte de `SPIFlashConfig`, dejamos seleccionadas las opciones:
   - 40 MHz
   - DIO
   - DoNotChgBin

Nos deberia de haber quedado asi:

<p align="center">
<img width="436" height="486" alt="image" src="https://github.com/user-attachments/assets/83e9b2d6-eaaa-41a5-ae68-fb788a05b255" />
</p>

- Finalmente, en la parte inferior de la ventana de la herramienta de flasheo, debemos seleccionar el puerto COM en donde se encuentra conectada nuestra ESP32, y BAUD en `11520`
- Le damos en `START`

Hasta aca, ya tenemos nuestra ESP32 flasheada con el firmware para convertirlo en un Deauther ✅

<br>

Ahora, la ESP32 estando alimentada por su puerto, lo primero que hara es generar una red wifi llamada `Managment AP`. Nos debemos conectar a esta red desde nuestra PC u otro dispositivo, la contraseña es: `mgmtadmin`. Lo siguiente que haremos es entrar a cualquier navegador y colocar la siguiente direccion en el buscador: `192.168.4.1`. ¿Que hace todo este conjunto de pasos? Nos permite configurar desde la web a nuestro Deauther.

Entrando a la direccion en el navegador, observaremos varias opciones de configruacion y una lista de redes WIFI a nuestro alrededor.

   - En la lista de redes WIFI `Select Target`, debemos seleccionar una red, que sera la red victima de nuestro ataque de desautenticacion (con fines eticos y educativos, esta debe ser alguna red de nuestra propiedad)
   - En el apartado de `Attack Configuration` podemos encontrar:

      - Attack type --> Que tipo de ataque realizaremos (DoS, Handshake, PMKID, Passive). Nosotros seleccionaremos `ATTACK_TYPE_DOS`
        
      - Attack method --> Que metodo de ataque utilizaremos. Nosotros utilizaremos `ATTACK_COMBINE_ALL`. Lo que significa esto es que el ESP32 va a disparar con todo su arsenal al mismo tiempo: va a mandar órdenes de desconexión globales (Broadcast FF:FF:FF:FF:FF:FF) y también órdenes individuales a cada celular o PC que vea conectado (Unicast). Básicamente, inunda el aire con tantas órdenes falsas de desconexión que el router se colapsa y nadie puede usar el WiFi.
        
      - Attack timeout --> Durante cuantos segundos durara nuestro ataque

<br>

Y finalmente, para aplicar el ataque, le damos en `Attack` ✅



<br>
<br>

## 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
