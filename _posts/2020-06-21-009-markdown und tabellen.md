---  
title: "Markdown und Tabellen"
date:  2020-06-21T5:34:30-04:00
categories:  
  - netzwerk  
tags:  
  - markdown  
  - 
---  

# Welche Möglichkeiten bietet mir Markdown um Tabellen darzustellen?

Mit der Auszeichnungssprache Markdown (GitHub) habe ich verschiedene Möglichkeiten Tabellen darzustellen. Optisch bietet Markdown wenig Möglichkeiten. Aber mit den W3C Sprachen (HTML / CSS) erreiche ich sehr viel mehr. Etwas Webdesign für Markdown.  

Im weiteren Sinne sind (unsichtbare) Tabellen schon immer auch Gestaltungswerkzeuge einer Website gewesen. Hier geht es in zweiter Linie auch darum, die Darstellung einer Markdown Site mit HTML / CSS zu verbessern.  

# Index  

<a name="start"></A>  
🔝 Start

1. [Markdown pur](#markdown)  
2. [HTML Tabelle in Markdown einbetten](#htmlmd)  
3. [HTML Tabellen mit CSS aufhübschen](#htmlcssmd)  

<a name="markdown"></A>  
# 1. Markdown pur

Die Code Beispiele sind aus der GitHub Markdown Hilfe  

## Beispiel 1   

### Code  

`````
| First Header  | Second Header | Third Header  | Fourth Header |
| ------------- | ------------- | ------------- | ------------- |
| Content Cell  | Content Cell  | Content Cell  | Content Cell  |
| Content Cell  | Content Cell  | Content Cell  | Content Cell  |
| Content Cell  | Content Cell  | Content Cell  | Content Cell  |
| Content Cell  | Content Cell  | Content Cell  | Content Cell  |
`````

#### Ausgabe  

| First Header | Second Header | Third Header | Fourth Header |
| ------------ | ------------- | ------------ | ------------- |
| Content Cell | Content Cell  | Content Cell | Content Cell  |
| Content Cell | Content Cell  | Content Cell | Content Cell  |
| Content Cell | Content Cell  | Content Cell | Content Cell  |
| Content Cell | Content Cell  | Content Cell | Content Cell  |

Der Titel einer Spalte wird durch Bindestriche von den Zellen mit Daten getrennt. Drei Bindestriche sind das Minium. Die Spaltenbreite wird automatisch gesetzt.  

## Beispiel 2  

### Code  

 ```
\| First Header  | Second Header | Third Header  | Fourth Header |  
\| --- | --- | --- | --- |  
\| Content Cell  | Content Cell  | Content Cell  | Content Cell  |  
 ```

### Ausgabe  

| First Header | Second Header | Third Header | Fourth Header |
| ------------ | ------------- | ------------ | ------------- |
| Content Cell | Content Cell  | Content Cell | Content Cell  |

## Beispiel 3  

### Code  

 ```
| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|-----------------------------|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=============================|
| Foot1   | Foot2   | Foot3   | 
 ```

### Ausgabe  

| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|-----------------------------|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=============================|
| Foot1   | Foot2   | Foot3   |  


Text kann auch als Block formatiert werden. Dafür verwendet man [Gravis](https://de.wikipedia.org/wiki/Gravis_(Typografie)#Darstellung_auf_dem_Computer): `  
Das Beispiel aus der GitHub Hilfedatei:

![NoText](/images/14-1.png)  

Markierungsmöglichkeiten sind dieselben wie in Markdown allgemein. * für kursiv, ** für fett, kann man auch kombinieren. Details dazu stehen in der [GitHub Helpdatei](https://help.github.com/en/articles/basic-writing-and-formatting-syntax#styling-text).

<a name="htmlmd"></A>  
# HTML Tabelle in Markdown einbetten  

Unter Quellen Punkt 3 erläutert der Erfinder von Markdown - John Gruber - auf seiner Website Daringfireball, wie weit die Unterstützung von HTML / CSS in Markdown geht. VS Code kann den HTML Code in einer Markdown Datei nicht prüfen. D.h. wenn Fehler auftreten, kopiere ich den HTML Teil in eine HTML Datei und debuge sie mit VS Code.  

HTML kennt abschliessend folgende Elemente für eine Tabelle:  
- table (die Tabelle selbst)  
- caption (die Tabellenüberschrift)  
- thead, tbody, tfoot (Zeilengruppen)  
- colgroup, col (Spaltengruppen)  
- tr (Tabellenzeilen)  
- th / td (Tabellenzellen)  

Der Zebralook der Beispiele entsteht dadurch, dass weiter unten über CSS der TR Tag entsprechend konfiguriert wurde. Natürlich wirkt sich der Code auf alle TR Tags in diesem Dokument aus.  

### Beispiel 1: *Eine einfache HTML Tabelle*  

Die Titel der Spalten (First / Second / ...) werden von Markdown automatisch dunkel eingefärbt, wenn man das HTML Tag "th" verwendet.  

#### Code 

 ```
\<table>  
  \<tr>  
    \<th>First</th>  
    \<th>Second</th>  
    \<th>Third</th>  
    \<th>Fourth</th>  
  \</tr>  
  \<tr>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
  \</tr>  
  \<tr>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
  \</tr>  
  \<tr>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
  \</tr>  
  \<tr>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
    \<td>  Content Cell</td>  
  \</tr>  
\</table>  
 ```

#### Ausgabe  

<table>
  <tr>
    <th>First </th>
    <th>Second</th>
    <th>Third</th>
    <th>Fourth</th>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
</table>


### Beispiel 2: *Eine HTML Tabelle zusätzlich mit den Elementen "Kopf", "Inhalt" und "Fuss"*  

#### Code 

 ```
\<table>  
    \<thead>  
        \<tr>  
          \<th>Head</th>  
        \</tr>  
    \</thead>  
    \<tbody>  
        \<tr>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
        \</tr>  
    \</tbody>  
    \<tfoot>  
        \<tr>  
          \<td>Foot</td>  
        \</tr>  
    \</tfoot>  
\</table>  
 ```

#### Ausgabe  

<table>  
    <thead>  
        <tr>  
          <th>Head</th>  
        </tr>  
    </thead>  
    <tbody>  
        <tr>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
        </tr>  
    </tbody>  
    <tfoot>  
        <tr>  
          <td>Foot</td>  
        </tr>  
    </tfoot>  
</table>  


### Beispiel 3:  *Mit dem Element "colspan" können Zellen zu einer zusammengefasst werden*  

#### Code  
 
 ```
\<table>  
    \<thead>  
        \<tr>  
          \<th>Head</th>  
        \</tr>  
    \</thead>  
    \<tbody>  
        \<tr>  
          \<td colspan="3">Content Cell 1</td>  
          \<td>Content Cell 4</td>  
        \</tr>  
    \</tbody>  
    \<tfoot>  
        \<tr>  
          \<td>Foot</td>  
        \</tr>  
    \</tfoot>  
\</table>  
 ```

#### Ausgabe  

<table>  
    <thead>  
        <tr>  
          <th>Head</th>  
        </tr>  
    </thead>  
    <tbody>
        <tr>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
        </tr>    
        <tr>  
          <td colspan="3">Content Cell 1</td>  
          <td>Content Cell 4</td>  
        </tr>  
    </tbody>  
    <tfoot>  
        <tr>  
          <td>Foot</td>  
        </tr>  
    </tfoot>  
</table>  

### Beispiel 4: Mit dem Element "rowspan" können Spalten zusammengefasst werden.  

#### Code 

 ```
\<table>  
    \<thead>  
        \<tr>  
          \<th>Head\</th>  
        </tr>  
    \</thead>  
    \<tbody>
        \<tr>  
          \<td rowspan="2">Content Cell Row 1\</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
        \</tr>  
        \<tr>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
          \<td>Content Cell</td>  
        \</tr>    
    \</tbody>  
    \<tfoot>  
        \<tr>  
          \<td>Foot</td>  
        \</tr>  
    \</tfoot>  
\</table>  
 ```

#### Ausgabe

<table>  
    <thead>  
        <tr>  
          <th>Head</th>  
        </tr>  
    </thead>  
    <tbody>
        <tr>  
          <td rowspan="2">Content Cell Row 1</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
        </tr>  
        <tr>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
          <td>Content Cell</td>  
        </tr>    
    </tbody>  
    <tfoot>  
        <tr>  
          <td>Foot</td>  
        </tr>  
    </tfoot>  
</table>  

<a name="htmlcssmd"></A>  
#   HTML Tabellen mit CSS aufhübschen

Tabellen sollten mit CSS formatiert werden. Folgende HTML Attribute werden z.B. nicht mehr von HTML5 unterstützt:  

* bgcolor → CSS: background-color
* border → CSS: border
* cellpadding → CSS:padding
* cellspacing → CSS: border-spacing
* frame → CSS: border
* rules → CSS: border
* summary → Zusammenfassung_des_Tabelleninhalts 
* width

Die einzelnen HTML Elemente werden am einfachsten mit Klassen formatiert. "Klasse" kann man sich als Vorlage vorstellen, auf die im HTML Element verwiesen wird.  

Die einzelnen Tags können aber auch direkt formatiert werden. In dem Beispiel 1 wird der Zebra Look der Tabelle über das formatieren des Tags "TR" erreicht.  Der Tag "tr" wird hier zweifach definiert, was für einen CSS Laien verwirrend macht. Unter dem Strich geht es in diesem Post primär darum zu zeigen, was mit HTML und CSS in einer Markdown Datei erreichdet werden kann.  

Dieses CSS Verfahren wird [Pseudoklasse](https://wiki.selfhtml.org/wiki/CSS/Selektoren/Pseudoklasse) genannt. Das hier verwendete Element "nth-child" mit dem Wert "odd" kann man z.B. auf der [Mozilla Website](https://developer.mozilla.org/de/docs/Web/CSS/:nth-child) nachlesen.  

Im Beispeil unten hat es im CSS Abschnitt \<style type="text/css"> eine CSS Klasse namens ".zahl". Damit kann eine HTML Aufzählung (Tag OL / UL) über den Befehl \list-style anders formatiert werden. Dieser CSS [Artikel](https://css-tricks.com/almanac/properties/l/list-style/) listet die verschiedenen Möglichkeiten auf, wie Listen anders dargestellt werden können. Um eine Liste absteigend zu nummerieren und die Ziffern mit einer führenden Null (01 / 02 / etc.) mit der oben definierten CSS Klasse "zahl" darzustellen, muss das ol tag so aussehen:  

 ```\<ol reversed="reversed" class="zahl" > ```

Wenn der Google Font ["Space Mono"](https://google-webfonts-helper.herokuapp.com/fonts/space-mono?subsets=latin) initialisiert wurde, kann ich für die Aufzählung auch diese Schrift definieren:  

 ```\style="font-family: 'Space Mono';" ```

Die CSS Angaben sind hierarchisch organisiert. Grundlegende Angaben die für das ganze Repository ("Jeckyl Now" Build) gelten, stehen in der Datei "style.css". Diese werden ggf. überschrieben, wenn ich in einer MD Datei (Blogpost) zum gleichen HTML Tag Angaben mache. Kug (Kurz und gut): Wenn in der Datei "style.css" steht, dass der Tag H1 (Titel) grün sein soll, jedoch in einer MD Datei H1 ist rot definiert ist, dann wird in dieser Datei der Titel in rot angezeigt.  

Dasselbe gilt, wenn ich zu einem einzelnen Tag eine CSS Anweisung setze. Diese wird die globale und auch die CSS Anweisungen in der Datei selber überschreiben. Da die Stlye.css anhand der Endung als W3C (HTML / CSS / etc.) Datei von VS Code erkannt wird, kann ich dort auch mit den integrierten Tools und Modulen arbeiten. Z.B. um einen Farbcode auszuwählen.  
![NoText](/images/14-2.png)  

Die CSS Klasse die im Beispiel angegeben ist, wirkt für die nachfolgenden Beispiele weiter. D.h. der farbige Hintergrund der Titelzeile in Beispiel 2 und nachfolgend wird durch die CSS Befehle in Beispiel 1 bewirkt.  

## Beispiel 1  

### Code

 ```
\<style type="text/css">  
      th {
        background-color: #666; 
        color: #fff;
      }
      tr {
        background-color: #fffbf0;
        color: #000;
      }
      tr:nth-child(odd) {
        background-color: #e4ebf2 ;
      }
      .zahl {
  list-style: square inside;
}      
\</style>  
\<table>  
  \<tr>  
    \<th>First </th>  
    \<th>Second</th>  
    \<th>Third</th>  
    \<th>Fourth</th>  
  \</tr>  
  \<tr>  
    \<td>Content Cell</td>  
    \<td>Content Cell</td>  
    \<td>Content Cell</td>  
    \<td>Content Cell</td>  
  \</tr>  
  \<tr>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
  \</tr>  
  \<tr>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
  \</tr>  
  \<tr>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
    \<td></td>  
  \</tr>  
\</table>  
 ```

### Ausgabe

<style type="text/css">
      table {width: 95%;}
      th {
        background-color: #666; 
        color: #fff;
      }
      tr {
        background-color: #fffbf0;
        color: #000;
      }
      tr:nth-child(odd) {
        background-color: #e4ebf2 ;
      }
      .zahl {
        list-style: square inside;
      }      
</style>
<table>
  <tr>
    <th>First</th>
    <th>Second</th>
    <th>Third</th>
    <th>Fourth</th>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
  <tr>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
    <td>Content Cell</td>
  </tr>
</table>  

## Beispiel 2 Colspan mit individueller Breite der Spalten  

Allgemein gesprochen, kann ich in Markdown in vielen HTML Tages die Breite mit diesen Anweisungen fixieren:

```
style="width: 40px;"
```

Konkret verwende ich es z.B. um in einer Tabelle die Breite einer Spalte festzulegen:  

```
<table>
    <thead>
        <tr style="font-weight: bold;">
            <th style="width: 40px;">Nr</th>
            <th style="width: 600px;">Titel</th>
            <th style="width: 160px;">Datum Erstellt</th>
            <th style="width: 160px;">Datum Geändert</th>
        </tr>
    </thead>
...
```

### Code  

 ```
\<table style="border-collapse: collapse;" border="0"><colgroup><col style="width: 42px;" /><col style="width: 561px;" /><col style="width: 111px;" /><col style="width: 75px;" /><col style="width: 75px;" /><col style="width: 75px;" /></colgroup>  
    \<tr style="height: 21px;">  
        \<td>1</td>  
        \<td>2</td>  
        \<td>3</td>  
        \<td>4</td>  
        \<td>5</td>  
        \<td>6</td>  
    \</tr>  
    \<tr style="height: 21px;">  
        \<td></td>  
        \<td>Acer</td>  
        \<td>Asus</td>  
        \<td>Dell</td>  
        \<td>Huawei</td>  
        \<td>Thinkpad</td>  
    \</tr>  
\</table>  
 ```

### Ausgabe   

<table style="border-collapse: collapse;" border="0"><colgroup><col style="width: 42px;" /><col style="width: 561px;" /><col style="width: 111px;" /><col style="width: 75px;" /><col style="width: 75px;" /><col style="width: 75px;" /></colgroup>
    <tr style="height: 21px;">
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
    </tr>
    <tr style="height: 21px;">
        <td></td>
        <td>Acer</td>
        <td>Asus</td>
        <td>Dell</td>
        <td>Huawei</td>
        <td>Thinkpad</td>
    </tr> 
</table>

## Beispiel 3: Tabellenzellen direkt formatiert

### Code  

 ```
\<table>  
\<tbody valign="top">  
    \<tr style="height: 21px;">  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;"> </td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Klang</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Pynyin</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">traditionell</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">simpel</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Zeichen</td>  
    \</tr>  
    \<tr style="height: 21px;">  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;">1</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom"><a href="https://de.wikipedia.org/wiki/T%C3%B6ne_des_Hochchinesischen">Hoch</a></td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">dì yī shēng</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">第一聲</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">第一声</td>  
        \<td style="padding-left: 5px; padding-right: 5px; border: none;" valign="bottom">¯</td>  
    \</tr>  
\</tbody>  
\</table>  
 ```
 
 ### Ausgabe   

<table>
<tbody valign="top">
    <tr style="height: 21px;">
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;"> </td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Klang</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Pynyin</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">traditionell</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">simpel</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: solid 1.0pt; border-right: none;" valign="bottom">Zeichen</td>
    </tr>
    <tr style="height: 21px;">
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;">1</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom"><a href="https://de.wikipedia.org/wiki/T%C3%B6ne_des_Hochchinesischen">Hoch</a></td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">dì yī shēng</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">第一聲</td>
        <td style="padding-left: 5px; padding-right: 5px; border-top: none; border-left: none; border-bottom: none; border-right: solid 0.5pt;" valign="bottom">第一声</td>
        <td style="padding-left: 5px; padding-right: 5px; border: none;" valign="bottom">¯</td>
    </tr>
</tbody>
</table>  

### Beispiel 4

Die Hintergrund Farbe kann man auch mit dem Befehl "rgba" festlegen. Diese Farbe ist transparent. Farbdefinitionen über RGB bestehen ja aus den drei Werten (Red / Green / Blue). Der vierte Wert des RGBA Befehls definiert den Alphakanal. Dieser definiert die Deckkraft der 3 Farbwerte.  
Details hier auf ["css-tricks.com"](https://css-tricks.com/rgba-browser-support/)  

### Code  

 ```
<style type="text/css">
    table {
        font-family: 'Cascadia Code', 'Fira Code', Consolas, 'Courier New', Courier, monospace;
        font-size: 13px;
        white-space: nowrap;
    }

    thead th {
        background-color: rgba(255, 165, 0, 0.62)
    }

    tbody tr td {
        background-color: #f7f7f7
    }
</style>
<table>
    <thead>
        <tr>
            <th>Spalte Eins</th>
            <th>Spalte Zwei</th>
            <th>Spalte Drei</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="2">Class<br>Zeile 1 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td rowspan="2">Class<br>Zeile 2 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td rowspan="2">Class<br>Zeile 3 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
    </tbody>
</table>
```

### Ausgabe   

<table>
    <thead>
        <tr>
            <th>Spalte Eins</th>
            <th>Spalte Zwei</th>
            <th>Spalte Drei</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="2">Class<br>Zeile 1 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td rowspan="2">Class<br>Zeile 2 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td rowspan="2">Class<br>Zeile 3 </td>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
        <tr>
            <td>brown fox jumps over the lazy dog</td>
            <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
        </tr>
    </tbody>
</table>

HSLA ist eine weitere Variante

<style type="text/css">
  td {
        background-color: hsla(120, 100%, 50%, 0.25);
    }
</style> 
<table>
    <tr>
        <td>brown fox jumps over the lazy dog</td>
        <td>Franz jagt im komplett verwahrlosten Taxi quer durch Bayern</td>
    </tr>
</table>


## Fazit  

Mit dem ["HTML Table Style Generator"](http://tablestyler.com) von Eli Geske können auch "nicht Webentwickler" wie ich sich schöne CSS Tabellen Design zusammen klicken. Danke an dieser Stelle an Eli Geske für den tollen Webservice!  

Mit der Auszeichnungssrpache Markdown (GitHub) habe ich verschiedene Möglichkeiten Tabellen darzustellen. Optisch bietet Markdown wenig Möglichkeiten. Aber mit den W3C Sprachen (HTML / CSS) erreiche ich sehr viel mehr. Etwas Webdesign für Markdown.  

# Quellen  

* [GitHub Help:  Organizing information with tables](https://help.github.com/en/articles/organizing-information-with-tables)  
* [GitHub Help:  Organizing information with tables](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)  
* [Daringfireball.net:HTML](https://daringfireball.net/projects/markdown/syntax#html)  
* [Tables Online Generator](https://www.tablesgenerator.com/html_tables)  
* [SelfHTML Aufbau einer Tabelle](https://wiki.selfhtml.org/wiki/HTML/Tabellen/Aufbau_einer_Tabelle)  
* [css-tricks.com: A Complete Guide to the Table Element](https://css-tricks.com/complete-guide-table-element/)  
* [W3C Markdown Syntax](https://www.w3.org/community/markdown/wiki/Syntax)  
* [TU-Dresden: Markdown - Eine Übersicht - Tabellen](https://elvis.inf.tu-dresden.de/wiki/index.php/Markdown_-_Eine_%C3%9Cbersicht#Tabellen)  
* [WP: Tabellen für Fortgeschrittene](https://de.wikipedia.org/wiki/Hilfe:Tabellen_f%C3%BCr_Fortgeschrittene)  
* [Farbnamen, Farbcodes und numerische Farbwerte]](https://www.mediaevent.de/tutorial/farbcodes.html)  
* [Devoth‘s HEX 2 RGBA Color Calculator](http://hex2rgba.devoth.com/)  

