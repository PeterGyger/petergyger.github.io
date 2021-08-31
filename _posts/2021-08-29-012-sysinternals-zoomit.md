---  
title: "Sysinternals: Zoom IT"
date:  2021-08-22T5:34:30-04:00
categories:    
  - windows  
tags:  
  - tool
---  

# SysInternals kleines Helferlein...

Mark Russinovich hat mit der Tool Suite "Sysinternals" die bekannteste Windows Tool Suite erstellt. Eines der Tool im Schatten von "Autoruns", "Process Monitor" etc. ist "Zoom IT". Da die Tools ohnehin über "path" eingebunden sind, habe ich mir dieses Programm näher angeschaut.  

Viel zu oft sehe ich, dass man Tools von anderen Firmen verwendet, obwohl das Betriebssytem diese Funktion auch beinhaltet. Dasselbe gilt für die Tool Suiten von SysInternals und Nirsoft. Mir ist es ein Anliegen, jedes der Tools zu kennen bzw. die Entwicklung der Suiten zu verfolgen. 

# Um was geht es?

Den Bildschirm zu fotografieren, hat man früher über die Printscreen bzw. "Alt + Printscreen" erledigt. Später kam der Shortcut "Shift+WinTaste+s" dazu. Wobei damit auch die Möglichkeit geschaffen wurde, den fotografierten Bildschirm in der Microsoft Cloude (Onedrive) abzulegen.  

[Zoom](https://docs.microsoft.com/en-us/sysinternals/downloads/zoomit) IT kann mehr. Das Tool beinhaltet folgende Funktionen:  

►	Zoom  
►	LiveZoom  
►	Draw  
►	Text (Unterfunktion von „Draw“)  
►	Break  

Das Zool hängt sich als "System Hook" in das Windows ein. D.h. unabhängig welches Programm gerade im Vordergrund läuft, wird es seine Hotkeys abfangen. D.h. wenn in einer Anwendung z.B. "CTRL + 2 für eine Funktion genutzt wird, ist das nicht mehr möglich. Oder man ändert in Zoom It die Konfiguration und bestimmt einen anderen Hotkey. 
 
# Shortcuts  

Auszug aus der Dokumentation:  

| Function | Shortcut |
| --- | --- |
| Zoom Mode | Ctrl + 1 |
| Zoom In | Mouse Scroll Up or Up Arrow |
| Zoom Out | Mouse Scroll Down or Down Arrow |
| Start Drawing (While In Zoom Mode) | Left-Click |
| Stop Drawing (While In Zoom Mode) | Right-Click |
| Start Drawing (While Not In Zoom Mode) | Ctrl + 2 |
| Increase/Decrease Line And Cursor Size (Drawing Mode) | Ctrl + Mouse Scroll Up/Down or Arrow Keys |
| Center The Cursor (Drawing Mode) | Space Bar |
| Whiteboard (Drawing Mode) | W   |
| Blackboard (Drawing Mode) | K   |
| Type in Text | T   |
| Increase/Decrease Font Size (Typing Mode) | Ctrl + Mouse Scroll Up/Down or Arrow Keys |
| Red Pen | R   |
| Green Pen | G   |
| Blue Pen | B   |
| Yellow Pen | Y   |
| Orange Pen | O   |
| Pink Pen | P   |
| Draw a Straight Line | Hold Shift |
| Draw a Rectangle | Hold Ctrl |
| Draw an Ellipse | Hold Tab |
| Draw an Arrow | Hold Ctrl + Shift |
| Erase Last Drawing | Ctrl + Z |
| Erase All Drawings | E   |
| Copy Screenshot to Clipboard | Ctrl + C |
| Save Screenshot as PNG | Ctrl + S |
| Show Countdown Timer | Ctrl + 3 |
| Increase/Decrease Time | Ctrl + Mouse Scroll Up/Down or Arrow Keys |
| Minimize Timer (Without Pausing It) | Alt + Tab |
| Show Timer When Minimized | Left-Click On The ZoomIt Icon |
| Live Zoom Mode | Ctrl + 4 |
| Exit | Esc or Right-Click |  
| ---------------------------|------------------------------------------------|

# Initialisierung

Wenn das Programm zum ersten Mal gestartet wird, erscheit das Konfigurationsmenu. Für jede Funktion wird über ein Register der Hotkey definiert. Sobald ein anderes Register aktiviert wird, fokussiert der Cursor das Hotkeyfeld. Es übernimmt dabei eine gedrückte Taste wie „Alt“.  Wie man sieht, besteht die Möglichkeit das Symbol im SysTray anzuzeigen und / oder das Tool automatisch zu laden.

![](/images/12-init.jpg)  

Die Hotkeys von Windows können nicht übersteuert werden. Anders als auf einer Tastur in Deutschland sind die Sondertasten auf einer schweizer Tastatur englisch beschriftet. Die „Strg“ ist die CTRL, die Umschalttaste ist die Shifttaste.  

Die Hotkeys funktionieren wie Ein / Aus Schalter. Die Alternativ ist wie immer unter Windows die Taste ESC. Ausgenommen bei der Funktion „“LiveZoom“.

Ein Klick mit der rechten Maustaste auf das Symbol im SysTray ermöglicht den direkten Aufruf von Funktionen. Das Programm unterstützt einem Pen Stift (Tablet PC) für die Steuerung.  

# Zoom  

Die Funktion Zoom entspricht einer Lupe. Wie man es unter Windows (CTRL und Mausrad bzw. CTRL und + / - )bzw Software wie Browsern bereits kennt.

| Funktion | Shortcut |
| --- | --- |
| Hotkey | CTRL und 1 |
| Beenden | Hotkey („Ein / Aus“) |
|  | Rechte Maustaste klicken |
|  | ESC |
| ---------------------------|------------------------------------------------|

Windows hat ja seit Jahren eine eigene "Lupe" in seinen Tools: ["magnify.exe"](https://support.microsoft.com/de-de/windows/bildschirmlupe-verwenden-damit-elemente-auf-dem-bildschirm-besser-sichtbar-sind-414948ba-8b1c-d3bd-8615-0e5e32204198#ID0EBBF=Windows_10). ZoomIT benutze ich schon viele Jahre bevor Windows dieses Tool erhielt. Daher habe ich es nie angeschaut.  

# Live Zoom  

Der Unterschied der Funktion „Zoom“ und „LiveZioom“ ist folgender.  Die Funktion „Zoom“ friert das Bild ein. Was während einer Präsentation oder einem Film nicht erwünscht ist. Töne und andere Hintergrundaktivitäten laufen normal weiter. 
„LiveZoom“  kann den laufenden Bildschirminhalt zoomen. Der Hinweis auf dieser Registerseite als auch verschiedene Anfragen im SysInternals  Forum belgen, dass diese Funktion auf gewissen Computern nicht funktioniert.  Den Zoomfaktor konnte auf einer Standard Cherry Tastatur nicht wie angeben mit CTRL UP / DOWN, sonder CTRL –  Pfeiltaste oben / unten steuern.

Anders als die Funktion „Zoom“ kann die Funktion NUR über den Hotkey beendet werden. Diese Funktion ist nicht mit den anderen Funktionen kombinierbar. Jedoch konnte ich über das Kontextmenu im SysTray die Funktion „Break“ aktivieren. Was von geringem praktischen Wert sein dürfte.

LiveZoom ist das zweite Register im Programm. Dennoch hat es als Hotkey Nummer die 4 erhalten. Aus meiner Sicht eine sehr gute Entscheidung. Die Funktionen auf den Hotkeys 1 bis 3 ergänzen sich ideal und sind auch für Präsentationen oder Ausbidlung praktisch. „LiveZoom“ ist weniger alltagstauglich.

Sowohl auf verschiedenen  PC / Laptops, als auch unter Citrix / Terminal Server arbeitete das Programm zuverlässig.

| Funktion | Shortcut |
| --- | --- |
| Hotkey | CTRL und 4 |
| Grösser | CTRL - Pfeil Taste oben |
|  | CTRL – PageUp |
| Beenden | Hotkey („Ein / Aus“) |
| ---------------------------|------------------------------------------------|

# Draw

Diese Funktion kann auf zwei verschiedenen Wegen aktiviert werden. Direkt über den Hotkey oder wenn die „Zoom“ Funktion aktiv ist, über einen Klick mit der linken Maustaste. 

Jeder der gerne mit der Tastatur arbeitet, wird begeistert sein welche Funktionen in diesem schlichten Tool stecken. Für den Maus und GUI gewohnten Anwender wird es eine gewisse Einarbeitungszeit bedeuten.

Die Funktion „kopieren“ bzw. „speichern“ macht eine 1:1 Bildschirmkopie („PrintScreen“) und legt es im PNG Format an einem beliebigen Ort ab. 

| Funktion | Shortcut |
| --- | --- |
| Hotkey | CTRL und 2 |
| Zeichnen | Linke Maustaste gedrückt halten |
| Zeichenfläche - weiss | W |
| Zeichenfläche - schwarz | K |
| Zoomen | Pfeil Taste oben / unten |
| Strichdichte ändern | Links CTRL und Mausrad |
|  | Links CTRL und Pfeiltaste oben / unten |
| Strichfarbe ändern | Hotkey „Draw“, Farbe über Buchstabe: |
|  | r(ed), g(reen), b(lue), o(range), y(ellow), p(ink) |
|  | ESC |
| Linientyp bestimmen | Gerade Linie = Shift + linke Maustaste |
|  | Rechteck = CTRL  + linke Maustaste |
|  | Ellipse = TAB + linke Maustaste |
|  | Pfeil = Shift + CTRL+ linke Maustaste |
| Zeichnung kopieren | CTRL – C |
| Zeichnung speichern | CTRL – S |
| Beenden | Rechte Maustaste klicken |
|  | ESC |
| ---------------------------|------------------------------------------------|

# Text

Wenn der „Draw“ Modus aktiviert wurde, kann mit „t“ die Funktion „Text gestartet werden.  Mit ESC bzw. der linken Maustaste kehrt man zum „Draw“ Mode zurück.

Die Farbe wird von der Funktion „Draw“ übernommen. D.h. für eien Farbänderung ruft man den Hotkey von „Draw“ auf und drückt den Buchstaben der gewünschten Farbe. Danach mit „t“ wieder in den Textmode wechseln. 
Die einzige Option die man einstellen kann, ist die Schriftart.

![](/images/12-zoomit-3.jpg)  

# Break

Die Funktion Break ist in erster Linie ein „Countdown“. D.h. man sieht im Vollbildmodus wie die Sekunden vergehen. Maximaler Intervall ist 99 Minunten. Im Menu definiert man den Hotkey, die vorgegebene Zeit und ob die Uhr nach der abgelaufenen Zeit weiterzählen soll.  

![](/images/12-zoomIt-4.jpg)

Im Untermenu „Advanced“ kann die Darstellung bzw. das Verhalten variert werden. Ein nettes Feature ist hier, ist die Möglichkeit eine Klangdatei (WAV – Format) abzuspielen.  

![](/images/12-zoomIt-5.jpg)  

Wenn mit mit Alt Tab bzw. Windows Tab (Aero) zu einer anderen Applikation wechselt, läuft der Countdown weiter. D.h. wenn man danach den Countdown über Hotkey oder Systray wieder aktiviert, sieht man dass er weitergezählt hat. Über den Hotkey kann man einen laufenden Countdown erneut starten. Wenn der Hotkey für „Zoom“ oder „Draw“ gedrückt wird, bricht der Countdown ab ohne die entsprechende Funktion zu starten.

Natürlich bietet auch hier die Tastatur verschiedene Funktionen an

| Funktion | Shortcut |
| --- | --- |
| Minuten erhöhen | Pfeil Taste oben |
|  | Mausrad |
| Sekunden erhöhen | Pfeil Taste rechts |
| Minuten reduzieren | Pfeil Taste unten |
|  | Mausrad |
| Sekunden reduzieren | Pfeil Taste links |
|  | Links CTRL und Pfeiltaste oben / unten |
| Farbe ändern | Farbe über Buchstabe: |
|  | r(ed), g(reen), b(lue), o(range), y(ellow), p(ink) |
| Beenden | Rechte Maustaste klicken |
|  | ESC |
| ------------------------|------------------------------------------------------|

# Resourcen

* [Stuart Hasic: Zoomit - a great little tool for Windows](https://www.youtube.com/watch?v=O4oK-xcYKw8)  
* [SysInternals - ZoomIt - Q&A](
https://docs.microsoft.com/en-us/answers/search.html?c=&includeChildren=&f=&type=question+OR+idea+OR+kbentry+OR+answer+OR+topic+OR+user&redirect=search%2Fsearch&sort=relevance&q=zoomit)  
* [live.sysinternals.com: ZoomIt64.exe](https://live.sysinternals.com/ZoomIt64.exe)
* [Sysinternals Suite download (inkl. ARM / Nano Server Variante)](https://docs.microsoft.com/en-us/sysinternals/downloads/)









