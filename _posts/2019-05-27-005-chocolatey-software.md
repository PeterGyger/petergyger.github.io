---
title: "Chocolatey Software"
date: 2021-05-27T15:34:30-04:00
categories:
  - windows
tags:
  - tool
---

# Der Paketmanager für Windows

Paketmanager sind unter Linux etwas selbstverständliches wie z.B. "Advanced Packaging Tool" (apt-get / yum). Der in Windows 10 integrierte Paketmanager war ursprünglich unter dem Namen OneGet bekannt. [OneGet](https://github.com/OneGet/oneget) ist eine Erfindung des Open Source Technology Centers von Microsoft. Mit der festen Integration des Paketmanagers in Windows 10 bezeichnet Microsoft den Paketmanager nicht mehr als OneGet, sondern als Package Management Feature. Das  Microsofts Package Management nicht nur mit NuGet vollständig kompatibel, sondern auch mit dem NuGet-basierten Package Manager Chocolatey. 

Das von Rob Reynolds 2011 entwickelte Tool nennt sich Chocolatery. Einen ersten Eindruck kann man sich mit diesem [Video](https://www.youtube.com/watch?v=HlnTZF3H1Ac&list=PL84yg23i9GBhJKWDe1TcPAHG2qtxlJ9DT&index=2&t=0s
) von Andy Melton - "Chocolatey Demonstration" gewinnen. Die Software wird in verschiedenen [Editionen](https://chocolatey.org/compare) angeboten. Wobei die einfachste Variante "Open Source" kostenlos ist. Dieser Artikel bezieht sich auf die kostenlose Version. 

Programme unter Windows zu installieren, heisst über MSI (MS Installer) zu gehen. Oder man installiert aus dem Windows Store eine App. Was Microsoft als die Marschrichtung unter Windows 10 definiert. Beide Versionen sind komplex und fehleranfällig. Ein Paketmanager ist erheblich effizienter, was ich in diesem Artikel demonstrieren will. Unter Windows bietet Chocolatey die beste Integration in die Kommandozeile.  

Nachfolgend als Beispiel das Szenario eines frisch installierten PC`s.  

# Powershell initalisieren  

Analog Bash unter Linux ist Powershell die Shell die das arbeiten mit der Kommandozeile effizient macht. Dazu muss Powershell mit Administrator Privilegien gestartet werden. Man kann Chocolatey auch über das klassische Command Line Interface - CMD.EXE - installieren.   

![PSinitalisieren](/images/57-1.png)  

Danach kann die Ausführungsrichtlinie so konfiguriert werden, dass Skripte ausgeführt werden können. D.h. Option "Unrestricted" oder "Remote Signed".  

![PSinitalisieren](/images/57-2.png)  

Danach über die Powershell Chocolatery installieren. Die Installation dauert ein paar Minuten. Den Befehl zur Installation findet man auf der Website von Chocolatey (im Abschnitt "Quellen" aufgelistet). Zu beachten ist, dass es dafür eine Powershell Sitzung mit erhöhten Rechten ("als Administartor ausführen") benötigt.  

![Chocolatery](/images/57-3.png)  

# GUI  

Chocolatey hat eine grafische Oberfläche (GUI). Diese kann wie jedes andere Paket direkt aus der CLI - z.B. Powershell installiert werden:  

``
install chocolateygui
``  

# Pakete  

Die Syntax für die Installation über CLI ist wie folgt, wobei "xxx" "yyy" "zzz" für die Namen von drei Softwarepakten steht. Die Anzahl ist nicht limnitiert durch Chocolatery. Der Parameter "-y" akzeptiert die Lizenzbedinungen des Paketes.

``  
choco install  xxx yyy zzz -y
``  

Wo ist die Liste mit den Paketen bzw. den Namen der Paketen?  

* [Chocolatey Website](https://chocolatey.org/packages)  

Auf der Kommandozeile:  

Suchen nach einem Paket im Repository:  

``  
choco search sysinternals  
``  

Suchen (Beschreibung / Tags) nach einem Stichwort. Der Parameter "verbose" zeigt die komplette Beschreibung an.    

``  
choco list -verbose sysinternals
``  

Auch das [deinstallieren](https://chocolatey.org/docs/commands-uninstall) von Paketen ist elegant einfach. Dito für das [updaten](https://chocolatey.org/docs/commands-upgrade) aller Pakete. Hier liegt der Gedanke nahe, den Befehl über ein Powershell Skript in den Scheduler einzubinden.  


# Modular und erweitert  

Ideal aus meiner Sicht ist es, die zu installierenden Software Pakete in einer externen Liste zu führen. Dadurch hat man auch schnell die Möglichkeit mehrere Paketlisten - Anwender und IT Profi - zu nutzen. Diese Paket werden über den Befehl [install](https://chocolatey.org/docs/commandsinstall) aufgerufen:  

``
Install-Package d:\packages.config  
``

Die Datei "packages.config" sieht so aus:  

``
<?xml version="1.0" encoding="utf-8"?>  
<packages>  
    <package id="7zip" />  
    <package id="putty" />  
    <package id="vlc" />  
    <package id="notepadplusplus" />  
    <package id="paint.net " />  
    <package id="irfanview " />  
    <package id="calibre " />  
    <package id="sumatra" />  
    <package id="fax24" />  
    <package id="wireshark" />  
    <package id="ultravnc" />  
    <package id="nmap" />  
    <package id="sysinternals" />  
    <package id="foobar2000" />  
</packages>
``

# Microsoft

2021 hat Microsoft ihren eigenen Paketmanager für Windows vorgestellt: [App Installer](https://devblogs.microsoft.com/commandline/windows-package-manager-1-0/)

## Quellen  

1. [Chocolatery.org](https://chocolatey.org/)  
2. [Choco on Github](https://github.com/chocolatey/choco)
3. [WindowsPro: Programme installieren und entfernen mit PowerShell Package Management](https://www.windowspro.de/wolfgang-sommergut/programme-installieren-entfernen-powershell-package-management)  
4. [Scott Hanselmann - Is the Windows User ready for apt-get?](https://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx)
5. [https://www.developerfusion.com/article/137219/aptget-windows-lets-get-chocolatey-part-1/](https://www.developerfusion.com/article/137219/aptget-windows-lets-get-chocolatey-part-1/)  
