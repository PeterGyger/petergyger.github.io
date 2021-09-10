---  
title: "PowerShell: Querbeet rund um das Datum"
date:  2020-12-12T5:34:30-04:00
categories:    
  - dev  
tags:  
  - powershell  
---  

# Notizen zu Zeit / Datum  

Datums- und Zeitformate sind immer ein Punkt der beachtet werden muss. Darum machte ich mir diese Notizen.

## Details  

Cmdlet "Get-Date" ist zuständig für Datumsinformationen. Mit ```get-date | get-member``` können die Funktionen aufgelistet werden. Z.B. ```(get-date).month```.  Alternativ kann man über eine Variable gehen:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
$datum = Get-Date
$datum.month
</div>

In Powershell sind alles Objekte. D.h. $datum ist keine Variable, sondern ein Objekt. Daher kann über die Variable die gleichen Methoden angewendet werden. Ich kann dem Objekt auch ein konkretes Datum vorgeben und z.B. fragen, was für ein Wochentag der 24. Dezember 2018 ist.

![get-culture](/images/010-get-culture.jpg)  

![get-culture](/images/010-ps-us.jpg)  

![get-culture](/images/010-ps-sg.jpg)  

Natürlich muss das in Windows eingestellte Datum berücksichtigt werden. Ein Datum im US Format erwartet an der ersten Stelle den Monat. D.h. Werte über 12 führen zu einem Fehler. Das kann mit Get-Culture eingestellt werden. Dieser Windows 10 Computer ist von der Tastaturbelegung bis hin zu den Datumsformaten auf "Swiss German" eingestellt. Da ich als verwendete Sprache US Englisch auf dem Computer definiert habe, erfolgt die Ausgabe von Powershell in Englisch.  

Der Befehl kann auch über die "[Standard Numeric Format Strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)" formatiert (Gross- / Kleinschreibung beachten) werden:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
C:\Users\info> Get-Date -Format F  
C:\Users\info> Get-Date -Format f
</div>

Das Argument Format kann auch mit .NET [- DateTimeFormatInfo Class -](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.datetimeformatinfo?view=netframework-4.7.2)] formatiert werden. Mit dem Argument -UFormat können Parameter im Unix Format verwendet werden. Das verwenden des Format Argumentes garantiert, dass unabhängig von den Ländereinstellungen in Windows die Angabe im gleichen Format angezeigt wird.  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
Get-Date -Format yyyy-MM-dd
</div>

Welcher Wochentag war der erste Tag des laufenden Monates?  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
Get-Date –Day 1 –Hour 0 –Minute 0 –Second 0
</div>

Wieviele Stunden des aktuellen Tages sind bereits vergangen?  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
(Get-Date).TimeOfDay.TotalHours
</div>  

Das Datum des Computers kann mit dem Cmdlet ["Set-Date"](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/Measure-Command?view=powershell-5.1) gesetzt werden.  

Das Datumsobjekt kann über die Methode "tostring" zu einem Text ("String") umgewandelt werden:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
`  
([datetime]::now).tostring("dd.MM.yyyy HH:mm:ss")  
([datetime]::now).tostring("MM\/dd\/yyyy|HH:mm:ss.fff")  
`  
</div>

Das Cmdlet "Get-Date" unterstützt kein Remoting. Dafür ist das [Invoke Command](https://docs.microsoft.com/de-de/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-6) erforderlich.  

Die Microsoft Tech Net Serie ["Scripting Guide"](https://blogs.technet.microsoft.com/heyscriptingguy/2013/11/11/powertip-use-powershell-to-format-dates/) hat noch einen Überblick geschrieben

# Timespan Objekt  

Ein TimeSpan Wert stellt ein Zeitintervall dar und kann als eine bestimmte Anzahl von Tagen, Stunden, Minuten, Sekunden und Millisekunden ausgedrückt werden. Da es sich um eine allgemeine Intervall ohne Verweis auf einen bestimmten Start- oder Endpunkt darstellt, kann nicht es im Hinblick auf Jahren und Monaten, die eine Variable Anzahl von Tagen jeweils ausgedrückt werden. Es unterscheidet sich von einem DateTime -Wert, der ein Datum und Uhrzeit ohne Verweis auf eine bestimmte Zeitzone darstellt, oder ein DateTimeOffset Wert, der einem bestimmten Zeitpunkt darstellt.  

Beispiele:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
Wann wurde die Datei zuletzt geändert?    new-timespan -start (ls .\.gitconfig).lastwritetime  

</div>

# Rechnen

Welcher Wochentag dieses Jahr Wehnachten ist, wurde weiter oben bereits angezeigt. Mit "rechnen" kann man auch ermitteln welcher Wochentag Sylvester dieses Jahr sein wird:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
(Get-Date "24.12.2018").AddDays(7).DayOfWeek  

(Get-Date "24.12.2018").AddDays(7).AddHours(7)  

</div>

Weitere verwandte Funktionen:  

* AddDays
* AddHours
* AddMilliseconds
* AddMinutes
* AddMonths
* AddSeconds  
* AddTicks
* AddYears  

Und wieviele Tage es noch bis Weihnachten sind, ermittelt dieser Befehl:  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
(Get-Date "24.12.2018").DayOfYear - (Get-Date).DayOfYear  

</div>

Wie bekannt, kann das Resultat der Rechnung formatiert ausgegeben werden.  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
C:\Users\info> (Get-Date "24.12.2018").AddDays(7).ToString(“dd.MM.yyyy”)  

(Get-Date "24.12.2018").AddDays(7).AddHours(7).ToString(“dd.MM.yyyy_HH:mm”)  

</div>

# Codesnippets


## Jahrestag in Datum konvertieren

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
$TempDate = ([datetime]"01/01/$((Get-Date).Year)").AddDays(140-1) $ShortDate =  

$TempDate.ToShortDateString()

</div>

## Laufzeit eines Skriptes messen  

<div style="color: teal; font-family: 'Courier New', Courier; text-indent: 3em;">
`
$Start = Get-Date  

[Skript das durchläuft]  

$Ende = Get-Date  

$Resultat = $Start - $Ende  

write-host "$($Resultat.Hours)h:$($Resultat.Minutes)m:$($Resultat.Seconds)s"
`  

</div>

In diesem Zusammenhang sind noch folgende Funktionen relevant:
* TotalMilliseconds
* TotalMinutes
* TotalHours
* TotalDays

Mit dem [Measure Command / Objekt}(https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/Measure-Command?view=powershell-5.1) kann direkt die Laufzeit eines Skriptes ermittelt werden.  

# Fazit

Zeit / Datum sind nicht nur in den klassischen Anwenderprogrammen wie Microsoft Excel ein tückisches Detail.  

# Quellen  

* [WindowsPro.de: Get-Date: Datum berechnen und formatieren in Powershell](https://www.windowspro.de/script/datum-berechnen-formatieren-powershell-get-date)  
* [Microsoft Docs: Get-Date](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-date?view=powershell-6) 
* [MS Windows PowerShell Tip of the Week: Formatting Numbers and Dates Using the CultureInfo Object](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-powershell-1.0/ff730954(v%3dtechnet.10))
* [TimeSpan Objekt](https://docs.microsoft.com/de-de/dotnet/api/system.timespan?view=netframework-4.7.2)
* [Hey, Scripting Guy! - Use PowerShell to Modify File Access Time Stamps](https://blogs.technet.microsoft.com/heyscriptingguy/2012/06/01/use-powershell-to-modify-file-access-time-stamps/)
* [Hey, Scripting Guy! - Use PowerShell to Find Files Modified by Month and Year](https://blogs.technet.microsoft.com/heyscriptingguy/2012/06/06/use-powershell-to-find-files-modified-by-month-and-year/)
* [The lonely Administrator - Extending Powershell Datetime Objects](https://jdhitsolutions.com/blog/powershell/5850/extending-powershell-datetime-objects/)
* [leedesmond.com - Get List of Two-letter Country ISO 3166 Code (alpha-2), Currency, Language and more](https://www.leedesmond.com/2018/02/powershell-get-list-of-two-letter-country-iso-3166-code-alpha-2-currency-language-and-more/#more-1586)
* [MS DOCS: Standard Date and Time Format Strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings)
* [MSDN: Standard DateTime Format Strings](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-3.0/az4se3k1(v=vs.85))
* [MS DOCS: Custom Date and Time Format Strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)

