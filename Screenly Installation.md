# Installation Screenly OSE

## Resourcen
RaspberryPi 3B+ oder 4B 
SD karte ab 8GB, am besten die geichen für mehrere Displays
Stromversorgung mit USB Netzteil mit ausreichend Leistung
HDMI bzw. Micro HDMI Kabel

## Installation
- Raspberry Pi Imager (<https://www.raspberrypi.com/software/>)   
- Installation Raspberry PI OS Lite (Legacy)
- SSH aktivieren
- nicht den Standardbenutzer (Pi) verändern

Raspberry booten und einloggen

- Screenly OSE installieren ([Link](https://github.com/Screenly/screenly-ose))  
```
  $ bash <(curl -sL https://www.screenly.io/install-ose.sh)

```

## Ausschalten Bildschirm

### Variante 1 (TVservice)

`Crontab -e`

```
    0 17 * * 1-5 sudo tvservice -o  
    0 6 * * 1-5 sudo reboot     
    */5 * * * * ping -c 1 8.8.8.8 > /dev/null 2>&1   

```
Beispiel: 

Um 17 Uhr Bildschirm ausschalten und um 6 Uhr für wieder aktivieren 

### Variante 2 (CEC)


[Using HDMI-CEC on a Raspberry Pi - Pi My Life Up](https://pimylifeup.com/raspberrypi-hdmi-cec/)	

```
sudo apt install cec-utils	

echo 'scan' | cec-client -s -d 1	



echo 'standby 0.0.0.0' | cec-client -s -d 1	

echo 'on 0.0.0.0' | cec-client -s -d 1


```

```
0 6 * * 1-5 sudo reboot
0 17 * * 1-5 sudo echo 'standby 0.0.0.0' | cec-client -s -d 1
*/5 * * * * ping -c 1 8.8.8.8 > /dev/null 2>&1
```

## Image erstellen

Wenn alles fertig konfiguriert ist (inklusive Assets)
Am besten gleich alle Assets vorkonfigureien die auf den verschiedenen Bildschirmen gebraucht werden.

Mit dem [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) ein Image erstellen und auf die anderen SD Karten klonen.

## Zusätzliches

Zum Monitoring bzw. Steuern mehrerer Screenly Instanzen 
[SOMO](https://github.com/didiatworkz/screenly-ose-monitoring/wiki/Installation-of-SOMO)

Screenly OSE Api ([Link](https://ose.demo.screenlyapp.com/api/docs/#/))

Beispiel:       
Per Script weiterschalten 

`curl -u user:password -X GET "https://url or ip/api/v1/assets/control/next%20" -H  "accept: application/json"`

Liste der Assets

`curl -u user:password -X GET "http://192.168.248.82/api/v1/assets `



