---
title: "Packprogramm 7Zip in der Praxis"
date: 2019-09-12T09:34:30-04:00
categories:
  - windows
tags:
  - tool
---

# Das ultimative Pack / Unpack Utility  

7-Zip ist ein beliebtes Allround Packproramm, dass mit vielen Formaten umgehen kann. Es enthält einen Dateimanager und Kommandozeilen (CLI) Programme. Details was die Download Datei für Windows beinhaltet ist in der Datei "Readme.txt" im ausgepackten Verzeichnis zu finden.  

Die Funktion ist unter GNU LGPL von Igor Pavlov freigegeben und kann als Modul in andere Programme eingebunden werden. Da der Source Code frei ist, kann auch unter Windows selber kompiliert werden. Anleitung dazu [hier](https://github.com/SaxonZhang2/7za/blob/1a23ca6d624e96ed4a1144d96693f57e712d8e96/DOC/readme.txt). In diesem Post gehe ich auf den Einsatz auf der Windows Kommandozeile (CLI) ein. D.h. Cmd und Powershell

7-Zip hat zwei Kommandozeilenprogramme:  
- 7z.exe  
- 7za.exe (a = alone)  

Die Version 7za fand ich auf der ["Source Forge"](https://www.7-zip.org/a/7za920.zip) Site, wo er mit seinem Projekt gestartet ist. Die heisst "7z1900-extra.7z". Der Autor hat auch eine weitere CLI Version ["7zr"](https://www.7-zip.org/a/7zr.exe) veröffentlicht. Diese unterstützt nur das 7-Zip Format ohne Passwortschutz. Im SDK (lzma) hat es eine 42 KByte grosse Datei, welche nur auspacken kann: "7zDec". Quasi das Pendant zu der "Unrar.exe" von Winrar.  
![CLI Hilfe Anzeige](assets/images/62-7zdec.png)   

7za.exe unterstützt nur die Formate 7z, lzma, cab, zip, gzip, bzip2, Z and tar. Externe module werden nicht unterstützt. Wie üblich stehen die Details in der Datei "Readme.txt" des ausgepackten Verzeichnisses.  

Dieser Post handelt von CLI Beispielen in der Praxis. Der Aufruf des Programmes erfolgt ohne Pfadangabe, da ich alle zusätzlichen Programme ("Tools") in einem Verzeichnis abgelegt habe, dass in der "Path" Angabe integriert ist. Natürlich funktioniert es auch in einer anderen Shell wie "Powershell"  .

## Syntax  

Der Aufruf des Programmes wird über "Funktionen" und "Switches" gesteuert". Switches sind das Feintuning. Switches werden mit einem Bindestrich angegeben, die Buchstaben der Funktion nicht. Der Aufruf des Programmes ohne weitere Angaben zeigt die Hilfe zum Programm und das Copyright mit Datum der verwendeten Version an.  

**Funktionen**  
* a    Add 
* d   Delete 
* e   Extract 
* h   Calculate
* l    List 
* t    Test 
* u   Update 
* x   eXtract with full paths

**Einige Switches**  
* -h   	              "Help" zeigt Informationen zu den Parametern. Der einzige mir bekannte Switch der ohne Funktion verwendet werden kann.
* -o[Verzeichnis]    Verzeichnis in das die Dateien geschrieben werden
* -p[Password]       Zu setzendes Passwort
* -y                 Rückfragen werden mit Ja ("Yes") beantwortet

Nicht jeder Switch kann für jede Funktion angewendet werden. Ein Studium der Hilfedatei klärt einem auf. Beispiele:

**Funktion "a" (Add) - Archiv erstellen**  

<table>
<tr><td>-i (Include)</td></tr>
<tr><td>-m (Method)</td></tr>
<tr><td>-p (Set Password)</td></tr>
<tr><td>-r (Recurse)</td></tr>
<tr><td>-sdel (Delete files after including to archive)</td></tr>
<tr><td>-sfx (create SFX)</td></tr>
<tr><td>-si (use StdIn)</td></tr>
<tr><td>-sni (Store NT security information)</td></tr>
<tr><td>-sns (Store NTFS alternate Streams)</td></tr>
<tr><td>-so (use StdOut)</td></tr>
<tr><td>-spf (Use fully qualified file paths)</td></tr>
<tr><td>-ssw (Compress shared files)</td></tr>
<tr><td>-stl (Set archive timestamp from the most recently modified file)</td></tr>
<tr><td>-t (Type of archive)</td></tr>
<tr><td>-u (Update)</td></tr>
<tr><td>-v (Volumes)</td></tr>
<tr><td>-w (Working Dir)</td></tr>
<tr><td>-x (Exclude)</td></tr>
</table>


**Funktion "e" (Extract) und "x" (Extract with Tree) - Archiv auspacken**  

<table>
<tr><td>-ai (Include archives)</td></tr>
<tr><td>-an (Disable parsing of archive_name)</td></tr>
<tr><td>-ao (Overwrite mode)</td></tr>
<tr><td>-ax (Exclude archives)</td></tr>
<tr><td>-i (Include)</td></tr>
<tr><td>-m (Method)</td></tr>
<tr><td>-o (Set Output Directory)</td></tr>
<tr><td>-p (Set Password)</td></tr>
<tr><td>-r (Recurse)</td></tr>
<tr><td>-si (use StdIn)</td></tr>
<tr><td>-sni (Store NT security information)</td></tr>
<tr><td>-sns (Store NTFS alternate Streams)</td></tr>
<tr><td>-so (use StdOut)</td></tr>
<tr><td>-spf (Use fully qualified file paths)</td></tr>
<tr><td>-t (Type of archive)</td></tr>
<tr><td>-x (Exclude)</td></tr>
<tr><td>-y (Assume Yes on all queries)</td></tr>
</table>


## Beispiel 1  

Die Dateien eines Verzeichnis wurde in ein Archiv bestehend aus 3 Dateien gepackt:  

- bsp.part1.rar  
- bsp.part2.rar  
- bsp.part3.rar  

Nachfolgend verschiedene Möglichkeiten wie sie ausgepackt werden können  

## Variante 1

CMD  
```
7z e bsp.part1.rar  
```  
Der Inhalt der Archive wird in das lokale Verzeichnis ("WorkDir") ausgepackt

```  
7za e bsp.part1.rar  
```  
Schlägt fehl. Fehlermeldung: "Can not open the file as archive".  

```  
7z e -o"\kw19\" bsp.part1.rar  
```  
Der Inhalt der Archive wird im lokalen Laufwerk im Root Unterverzeichnis \kw19 geschrieben

```  
7za e -o"\kw19\" bsp.part1.rar  
```  
Schlägt fehl. Fehlermeldung: "Can not open the file as archive".  

## Beispiel 2  

Die Dateien eines Verzeichnis wurde in ein Archiv bestehend aus 2 Dateien die auf 5 Dateien aufgesplittet wurden:

- bsp.part1.rar.001
- bsp.part2.rar.002
- bsp.part3.rar.003
- bsp1.part1.rar.001
- bsp1.part2.rar.002

7Z kann gesplittete Dateien nicht zusammensetzen. Fehlermeldung: "Can not open the file as archive". Mit 7za müssen zuerst die 2 gesplitteteten Dateien zusammen geführt ("combine") werden.
``  
7za e bsp.part1.rar.001  
``  

oder mit einer Zielverzeichnis Angabe

``  
7za e *.part1.rar.001 -o\kw19\  

* steht für irgendetwas das vor dem Text steht. ACHTUNG: ``*.*`` versteht 7Zip als alle Dateien mit Erweiterung (.txt / .xlsm / etc.) ``*`` alleine ist also gleichbedeutend wie in der Windows Welt ``*.*``  
``  

7za erstellt aus den Datein 001 / 002 / 003 eine normales Archiv mit dem Dateinamen "bsp.part1.rar". Danach mit dem zweiten Splitt ("bsp1.") die Datei "bsp.part2.rar". Diese können wie in Beispiel 1 als Archiv entpackt werden. Über den Befehl "For" kann innerhalb der Shell CMD auch eine grössere Anzahl Dateien in einem Durchgang entpackt werden.

### Beispiel 3  

Wie sieht es aus, wenn als Shell "Powershell" verwendet wird?  Die Eingaben in den vorhergehenden Abschnitten funktionieren und führen zum gleichne Resultat. Natürlich muss für das lokale Verzeichnis der Prefix ".\" gesetzt werden. D.h. wenn ich eine Datei "bsp.part1.rar" im aktuellen Verzeichnis auspacken will, lautet der Befehl

``  
7za e .\bsp.part1.rar  
``  

Wenn mehrere Dateien ausgepackt werden sollen, dann sind die CMDLET von Powershell erheblich mächtiger als ein "For" Befehl der CMD Shell. Nachfolgend sollen alle RAR Dateien des aktuellen sowie der Unterverzeichnisse ("-Recurse") ausgepackt werden. Jedes Archiv das über mehrere Dateien gepackt ist, beginnt i.d.R. mit einer Datei welche die am Schluss "part1.rar" hat. Davon ausgehend ergibt sich folgender Befehl:

``  
Get-ChildItem -Recurse ".\*part1.rar" | ForEach-Object { 7z e $_ -o"$($_.Directory)\$($_.BaseName)" }
``  
Wenn mit 7za mehrere gesplitte Archive zusammen ("combine") geführt werden sollen, sieht die Eingabe so aus:

``  
Get-ChildItem -Recurse ".\*.rar.001" | ForEach-Object { 7zA e $_ - }
``  
Die ausgepackten RAR Dateien aus allen Unterverzeichnissen werden in das aktuelle Verzeichnis geschrieben.
Wenn die gepackten Dateien in den Unterverzeichnissen identische Namen haben oder man aus anderen Gründen die Dateien in den jeweiligen Verzeichnissen lassen will, muss der Befehl ergänzt werden.  

``  
Get-ChildItem -Recurse ".\*.rar.001" | ForEach-Object { 7zA e $_ -o"$_.Directory"}
``  
Für eine bitgenaue Kontrolle des Endresultates kennt das das 7-Zip Programm die Funktion "h".  

### Beispiel 4  

Ein Verzeichnis, darin die Dateien von 3 Archiven:  
* zuerich.part01.rar .. zuerich.part04.rar  
* bern.part01.rar .. bern.part03.rar  
* genf.part01.rar .. genf.part08.rar  

Natürlich will ich auf der CLI alle drei Archive mit einer Eingabe auspacken. Ferner soll jedes Archiv in einem eigenen Verzeichnis sein. Die einzige Lösung die funktionierte war einen Kombination mit dem For Befehl:  

``
for %a in (*.part01.rar) do 7z e *.part01.rar -ox:\kt-stat\%a
``

# Download

7-ZIP wird vom Entwickler auf SourceForge angeboten. Die neueste Version findet man im Tab "Files". Nicht in "Summary". Auch die Hashwerte findet man (nur) dort.  

![MD5](/images/007-md5.jpg)  

# Fazit

Die Beispiele wurden während des schreibens mit 7-Zip Version 19 unter Windows 10 positiv getestet. 

# Quellen  

* [7-Zip Website](https://www.7-zip.org/)  
* [7-Zip Command Line Commands](https://sevenzip.osdn.jp/chm/cmdline/commands/index.htm)
* [7-ZIP Command Line Examples^](https://www.dotnetperls.com/7-zip-examples)
* [Wikipedia EN](https://en.wikipedia.org/wiki/7-Zip)  
* [Portable Version](https://portableapps.com/de/apps/utilities/7-zip_portable)  
* [Chocolatey](https://chocolatey.org/packages/7zip.install)  
* [Linux Manpages](https://linux.die.net/man/1/7z)
* [PS: Get-ChildItem](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-6)  

