---  
title: "MS DevCon und Nirsoft DevManView für die Geräteverwaltung"
date:  2019-10-25T5:34:30-04:00
categories:    
  - windows  
tags:  
  - tool
---  

# Windows Device Management auf der CLI 

Wenn ich nachfolgend auf das Microsoft Kommanozeilen (Administrator Rechte) Programm DevCon (DevCon = "Device Console") eingehen, ist immer auch die Nirsoft Variante DevManView gemeint. Die Programme sind für denselben Zweck konzipiert. Auf die Unterschiede gerade in den Befehlen und Parametergehe ich weiter unten ein.  

Analog dem Gerätemanager, aber weit mächtiger ermöglicht DevCon die Geräteverwaltung. Geräte können einzeln oder als Gruppe angesprochen (aktivieren, deinstallieren, etc.) werden. Gerade für den Supporter / Administrator ist es in der Werkzeugkiste nicht verzichtbar.  

Die Hardware-ID dient auch zum suchen von Treibern in einer Internet Suchmaschine. Der Teil "VEN_XXXXX" der HW-ID ist ein Code, welches den Hersteller der Hardware nennt. Z.B. "14E4" (VEN_14E4) für Broadcom.	

# Installation  

Dir NirSoft Tool [DevManView](http://www.nirsoft.net/utils/device_manager_view.html) hat eine eigene Website und kann wie bei allen Tools des Entwicklers Nir Sofer dort downgeloaded gewerden. Die NirSoft Tools sind analog den SysInternals Tool Bais für den Windows Support / Administration. Es versteht sich von selbst, dass solche System Tools über einen Benutzer mit Administrationsrechten genutzt werden müssen.  

"DevCon.exe" ist afuwändiger zu finden und installieren. Aktuell (Oktober 2019) ist der einfachste Weg folgende Schritte:  
1. "WDK for Windows 10" [downlaoden](https://docs.microsoft.com/de-de/windows-hardware/drivers/download-the-wdk)  
2. WDK installieren. Die Daten werden nach "C:\Program Files\Windows Kits\10" geschrieben.
3. Im Installationsverzeichnis hat es einUnterverzeichnis "Tools". Für die x64 Window OS (94%) ist die Datei im Verzeichnis "x64".
4. Empfehlung: Diese wie andere CLI Tools in ein Verzeichnis kopieren, dass in der Variable "Path" eingebunden ist.  

## DevCon

Microsoft hat eine Website für die Befehle und eine für Beispiele im Netz:  
* [Befehle](https://docs.microsoft.com/de-de/windows-hardware/drivers/devtest/devcon-general-commands)  
* [Beispiele](https://docs.microsoft.com/de-de/windows-hardware/drivers/devtest/devcon-examples)  

**CLI**  

Hilfetext anzeigen:  
``devcon help``  

Das Gerät wird über die Hardware-ID angesprochen. Der Aufbau dieser HW-ID ist im Dokument "Device Identification Strings" (Quellen) beschrieben. Natürlich kann diese auch über den Gerätemanager (CMD: devmgmt.msc) angezeigt werden. Der Klammeraffe "@" zeigt auch ausgeblendete Geräte. Was gerade für USB Devices ein wichtiger Punkt ist.  

CMD interpretiert einige Zeichen wie "&" (kaufmännisches Und). Und das kann auch nicht wie in vielen anderen Shells mit "" oder Doppelten Anführungszeichen kompensiert werden. Man muss dazu das Escape Zeichen ("^") verwenden. D.h. anstatt  
``devcon disable HID\VID_1B96&PID_AF16&COL93``  
muss der Befehl mit dem ESC Zeichen vor dem Steuerzeichen - & - ergänzt werden:  
``devcon disable HID\VID_1B96^&PID_AF16^&COL93``  

[Detailierte Erklärung zu ESC Sequenz in der CMD Shell von Rob van der Woude EN](https://www.robvanderwoude.com/escapechars.php)  

Alle Geräte anzeigen:  
``devcon hwids *``  

Alle Geräte anzeigen inkl. den nicht angeschlossenen
``devcon findall *``  

Alle Geräteklassen anzeigen:  
``devcon classes``

Über den CMD Befehle kann natürlich nach bestimten Textmustern gesucht werden:  
``devcon classes | find "Monitor"``

Geräte einer Klasse anzeigen:  
``devcon listclass Monitor``  

Geräte (auch ausgeblendete) der PCI Klasse Status anzeigen lassen  
``devcon status @pci\*``

Geräte einer bestimmten Klasse suchen:
``devcon find *Monitor*``  

Ein Gerät (Klasse\Hardware-ID) anzeigen:  
``devcon hwids MONITOR\SAM0B67"  

"Reale" Netzwerkkarten - d.h. über PCI verbunden finden:  
``devcon find =Net PCI\*``  

Treiber eines Gerätes anzeigen. Das & wurde nicht als Steuersequenz interpretiert, somit kein ^ davon. Nicht logisch, aber soeben beim testen erlebt.    
``devcon driverfiles "PCI\VEN_10EC&DEV_8168&SUBSYS_2A9C103C&REV_03"``  
![Screenshot](../images/devcon/1.png)  

Installation eine Treiber Datei (INF-Datei)
``devcon dp_add "ChinaAir-Cam.inf"``  

Ein Treiber ist üblicherweise Teil eines Paketes. Dieses beinhaltet:  
Die .INF Datei (Konfigurationsdatei a la INI)  
Dateien die in der INF Datei referenziert werden (DLL)  
"Driver Catalog" (.CAT Datei) welche die digitale Signatur enthält.  

Die Windows 64 Bit Version erlaubt nur die Installation von signierten Treibern. Diese sind in Windows im Verzeichnis "%SystemRoot%\System32\DriverStore" gespeichert.  

## DebManView  

DevCon verlangt die Hardwware-ID, um das Gerät anzusprechen. Die Schnittstelle von DebManView erlaubt auch die Angabe des Namens.
Die Ausgabe erfolgt nicht auUf der CLI. D.h. es wird ein Fenster geöffnet. Alternativ kann die Ausgabe mit dem Parameter "/stext" in eine Datei umgeleitet werden. Die Ausgabe auf ein Handle wie "con" funktioniert nicht.  

``debmanview /stext geraete.txt``  

Das Tool erlaubt auch den Zugriff auf entferne Computer. Analog den PS Tools von SysInternals.  



# Fazit

DevCon ist ein sehr altes Tool von MS. Ein Erbstück aus den Resource Kits und SDK (WDK). Powershell hat CMDLETS dafür, welche ich noch nicht geprüft habe. Beispiele mit "Get-PnpDevice" nachfolgend. "PnP" steht für Plug and Play. 

*Cmdlet* | / | *Description* |
Enable-PnpDevice | | Einschalten eines PnP Gerätes |
Disable-PnpDevice | | Ausschalten eines PnP Gerätes |
Get-PnpDevice | | Zeigt information eines PnP Gerätes an |
Get-PnpDeviceProperty | | Zeigt detailierte information eines PnP Gerätes an |


**Beispiele:**  

Alle Geräte anzeigen:  
``Get-PnpDevice``  

Alle Geräte anzeigen, welche "USB" im Namen beinhalten:  
``Get-PnpDevice | Where-Object { $_.FriendlyName -match 'USB' }``  

Alle Geräte anzeigen, welche "USB" im Namen beinhalten sollen ausgeschaltet werden *(VORSICHT!!!)*  
``Get-PnpDevice | Where-Object { $_.FriendlyName -match 'USB' } | Disable-PnpDevice``  

# Sysinternal Tool WinObj

In diesen Kontext gehört auch das Sysinternal Tool [WinObj V3.11](https://docs.microsoft.com/en-us/sysinternals/downloads/winobj).  

# Quellen  

1. [NirSoft DevManView](http://www.nirsoft.net/utils/device_manager_view.html) 
2. [WDK download](https://docs.microsoft.com/de-de/windows-hardware/drivers/download-the-wdk)
3. [Windows Device Console (Devcon.exe)](https://docs.microsoft.com/de-de/windows-hardware/drivers/devtest/devcon)
4. [Device Identification Strings](https://docs.microsoft.com/de-de/windows-hardware/drivers/install/device-identification-strings)
5. [Liste der Hardware-IDs nach Hersteller](https://www.driverscloud.com/de/drivers)
6. [SS64.com:DevCon](https://ss64.com/nt/devcon.html)
7. [SS64.com:Escape Characters, Delimiters and Quotes](https://ss64.com/nt/syntax-esc.html)
8. [INF Files](https://docs.microsoft.com/de-ch//windows-hardware/drivers/install/inf-files)
9. [DevCon Dp_add](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/devcon-dp-add)
10. [Fehlercodes im Geräte-Manager in Windows](https://support.microsoft.com/de-de/help/310123/error-codes-in-device-manager-in-windows)
11. [OT: dventures in Windows Driver Development](https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2016/april/adventures-in-windows-driver-development-part-1/)