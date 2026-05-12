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
It's worth noting that this attack is foolproof on standard WPA/WPA2 networks, but more modern networks using WPA3 or with PMF (Protected Management Frames / 802.11w standard) enabled are immune. In these modern cases, the disconnection frames are encrypted, so the devices ignore the ESP32 attack.

<br>
<br>

## 💻 Firmware
- There are several firmwares that can turn certain devices into a `Deauther`. In this case, we will use the following firmware:
  - `ESP32 Flash Tool`: https://drive.google.com/file/d/1UuULfBdo3wlgzL6Es9meEfsRHoHqnaKh/view 
  - `BIN Files`: https://drive.google.com/file/d/1CYqyvu_TVEcifmxE-ZX37RlV9JfTKWc7/view


Below are some links to videos where they use other deauthentication firmwares (some more advanced, which instead of being a simple Deauther, directly convert a certain device into a `Marauder`, that is, a Deauther + an additional set of hacking/pentesting tools):

  - `ESP32 Marauder (by JustCallMeKoko)` --> https://www.youtube.com/watch?v=bHivs2c_o7I
  - `ESP32 Deauther / GhostESP` --> https://www.youtube.com/watch?v=dryQoQLEl90
  - `Bruce Firmware` --> https://www.youtube.com/watch?v=1dC_abmQvzA

<br>
<br>

## ⚙️ How to install & configure the firmware
In this section we will see how to install, configure and use the basic firmware selected for this repository.

The first step is to connect our ESP32 to our PC, then:

- Installing the flashing tool
   - Once you have downloaded the folders from the Google Drive links provided above, we will begin installing the `ESP32 Flash Tool`
   - We open the unzipped folder `flash_download_tool_3.9.3`
   - Then we double-click on the file `flash_download_tool_3.9.3.exe`
   - Two windows will open (a command prompt and a smaller one). In the smaller window, enter the options: `ESP32` (instead of ESP38266) and `Develop`. Click `OK`
   - We close the command prompt, and another window will open. This is the flashing tool window

<br>
   
- Installing `.bin` files
   - Now, we will open the folder called `esp32-wifi-penetration-tool-master`
   - Next, we go to the subfolder called `build`. Here we will find the necessary .bin files
   - Now what we do is: in the flashing tool window, we're going to click on the three dots that appear for each row and in a single column, to insert the .bin files, and then we'll place certain memory addresses
   - Clicking the three dots will open the file explorer, allowing you to select your .bin files. In the first three dots (first row), you should choose the file `partition-table.bin`.
   - In the second step, we will search for and place the `bootloader.bin` file.
   - And finally, in the points of the third row, we will look for and place the file `esp32-wifi-penetration-tool.bin`
   - As mentioned, we will now place the memory addresses in the column next to the column with the three dots. The addresses we need to place are:
       - First row --> 0x8000
       - Second row --> 0x1000
       - Third row --> 0x10000
   - Finally, click on the 3 boxes in the first column (the rows should turn green after this)

<br>

- In the `SPIFlashConfig` section, we leave the following options selected:
   - 40 MHz
   - DIO
   - DoNotChgBin

It should have looked like this:

<p align="center">
<img width="436" height="486" alt="image" src="https://github.com/user-attachments/assets/83e9b2d6-eaaa-41a5-ae68-fb788a05b255" />
</p>

- Finally, at the bottom of the flashing tool window, we must select the COM port where our ESP32 is connected, and set the BAUD to `11520`
- We press `START`

So far, we have our ESP32 flashed with the firmware to turn it into a Deauther ✅

<br>

Now, with the ESP32 powered by its port, the first thing it will do is generate a wifi network called `Management AP`. We need to connect to this network from our PC or another device; the password is: `mgmtadmin`. Next, we'll open any web browser and enter the following address in the address bar: `192.168.4.1`. What does all these steps do? They allow us to configure our Deauther from the web.

By entering the address in the browser, we will see several configuration options and a list of WIFI networks around us.

   - In the WIFI network list `Select Target`, we must select a network, which will be the victim of our deauthentication attack (for ethical and educational purposes, this should be a network we own).
   - In the `Attack Configuration` section we can find:

      - ***Attack type*** --> What type of attack will we perform (DoS, Handshake, PMKID, Passive)? We will select `ATTACK_TYPE_DOS`
        
      - ***Attack method*** --> Que metodo de ataque utilizaremos. Nosotros utilizaremos `ATTACK_COMBINE_ALL`. Lo que significa esto es que el ESP32 va a disparar con todo su arsenal al mismo tiempo: va a mandar órdenes de desconexión globales (Broadcast FF:FF:FF:FF:FF:FF) y también órdenes individuales a cada celular o PC que vea conectado (Unicast). Básicamente, inunda el aire con tantas órdenes falsas de desconexión que el router se colapsa y nadie puede usar el WiFi.
        
      - ***Attack timeout*** --> Durante cuantos segundos durara nuestro ataque

<br>

And finally, to apply the attack, we click on `Attack` ✅



<br>
<br>

## 🧊 3D Cases (📌 in progress)

<br>

### I hope you found this helpful and enjoyable. If so, leave a star ⭐ Best wishes and much success!
