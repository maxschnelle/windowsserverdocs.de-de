---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: 'Windows-Zeitdienst: Tools und Einstellungen'
author: Teresa-Motiv
ms.author: v-tea
ms.date: 02/24/2020
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 2f6ba34381e813247d0838853f688abf13fbd2fa
ms.sourcegitcommit: 1d83ca198c50eef83d105151551c6be6f308ab94
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605540"
---
# <a name="windows-time-service-tools-and-settings"></a>Windows-Zeitdienst: Tools und Einstellungen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

In diesem Thema erfährst du mehr über Tools und Einstellungen für den Windows-Zeitdienst (W32Time).  

Wenn du die Zeit nur für einen einer Domäne beigetretenen Clientcomputer synchronisieren möchtest, findest du weitere Informationen unter [Konfigurieren eines Clientcomputers für die automatische Domänenzeitsynchronisierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29). Weitere Themen zum Konfigurieren des Windows-Zeitdiensts findest du unter [Wo finde ich Konfigurationsinformationen zum Windows-Zeitdienst?](windows-time-service-top.md).  

> [!CAUTION]  
> Du solltest nicht den Befehl **Net time** verwenden, um die Zeit zu konfigurieren oder zu stellen, wenn der Windows-Zeitdienst ausgeführt wird.  
>
> Auf älteren Computern, auf denen Windows XP oder niedriger ausgeführt wird, zeigt der Befehl **Net time /querysntp** auch den Namen eines NTP-Servers (Network Time Protocol) an, mit dem ein Computer synchronisiert werden soll, doch dieser NTP-Server wird nur verwendet, wenn der Zeitclient des Computers als NTP oder AllSync konfiguriert ist. Dieser Befehl ist seitdem veraltet.  

Die meisten Domänenmitgliedscomputer verfügen über einen Zeitclient vom Typ NT5DS, was bedeutet, dass sie die Zeit aus der Domänenhierarchie synchronisieren. Die einzige typische Ausnahme hierbei ist der Domänencontroller, der als Betriebsmaster der Stammdomäne der Gesamtstruktur des PDC-Emulators (Primärer Domänencontroller) fungiert. Der PDC-Emulator ist in der Regel so konfiguriert, dass er die Zeit mit einer externen Zeitquelle synchronisiert. Zum Anzeigen der Zeitclientkonfiguration eines Computers (beginnend mit Windows Server 2008 und Windows Vista) führst du den Befehl **W32tm /query /configuration** in einer Eingabeaufforderung mit erhöhten Rechten aus, und liest die Zeile **Typ** in der Befehlsausgabe. Weitere Informationen findest du unter [Funktionsweise des Windows-Zeitdiensts](How-the-Windows-Time-Service-Works.md). Du kannst zusätzlich den Befehl **reg query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** ausführen und den Wert von **NtpServer-** in der Befehlsausgabe lesen.  

> [!IMPORTANT]  
> Vor Windows Server 2016 war der W32Time-Dienst nicht so konzipiert, dass er die Anforderungen zeitabhängiger Anwendungen erfüllte. Updates für Windows Server 2016 ermöglichen es jetzt jedoch, eine Lösung für eine Genauigkeit von einer Millisekunde in deiner Domäne zu implementieren. Weitere Informationen findest du unter [Windows 2016: Genaue Zeit](accurate-time.md) und [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md).  

## <a name="windows-time-service-tools"></a>Windows-Zeitdiensttools  

Das folgenden Tool ist dem Windows-Zeitdienst zugeordnet.  

### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows-Zeitdienst  

**Kategorie**  

Dieses Tool ist Teil der Standardinstallation von Windows (Windows XP und höhere Versionen) und Windows Server (Windows Server 2003 und höhere Versionen).  

**Versionskompatibilität**  

Dieses Tool funktioniert mit der Standardinstallation von Windows (Windows XP und höhere Versionen) und Windows Server (Windows Server 2003 und höhere Versionen).  

Mit „W32tm.exe“ kannst du Einstellungen des Windows-Zeitdiensts konfigurieren und Zeitdienstprobleme diagnostizieren. „W32tm.exe“ ist das bevorzugte Befehlszeilentool zum Konfigurieren und Überwachen von sowie zum Behandeln von Problemen mit dem Windows-Zeitdienst.  

In den folgenden Tabellen werden die Parameter beschrieben, die mit „W32tm.exe“ verwendet werden können.  

**Primäre Parameter von „W32tm.exe“**  

|Parameter |Beschreibung |
| --- | --- |
|**w32tm /?** |Zeigt die W32tm-Befehlszeilenhilfe an. |
|**w32tm /register** |Registriert den Zeitdienst zur Ausführung als Dienst und fügt der Registrierung die Informationen seiner Standardkonfiguration hinzu. |
|**w32tm /unregister** |Hebt die Registrierung des Zeitdiensts auf und entfernt alle seine Konfigurationsinformationen aus der Registrierung. |
|**w32tm /monitor [/domain:\<*Domänenname*>] [/computers:\<*Name*>[,\<*Name*>[,\<*Name*>...]]] [/threads:\<*Anzahl*>]** |Überwacht den Windows-Zeitdienst.<p>**/domain**: Gibt die zu überwachende Domäne an. Wenn kein Domänenname angegeben oder weder die Option **/domain** noch **/computers** angegeben wird, wird die Standarddomäne verwendet. Diese Option kann mehrfach verwendet werden.<p>**/computers**: Überwacht die angegebene Liste von Computern. Computernamen werden ohne Leerzeichen durch Kommas getrennt. Wenn ein Name ein **\*** -Präfix besitzt, wird er als PDC behandelt. Diese Option kann mehrfach verwendet werden.<p>**/threads**: Gibt die Anzahl der gleichzeitig zu analysierenden Computer an. Der Standardwert ist „3“. Der zulässige Bereich ist 1–50. |
|**w32tm /ntte \<NT *time epoch*>** |Konvertiert eine Windows NT-Systemzeit (gemessen in 10<sup>-7</sup>-Sekunden-Intervallen ab 0h 1-Jan 1601) in ein lesbares Format. |
|**w32tm /ntpte \<NTP *time epoch*>** |Konvertiert eine NTP-Zeit (gemessen in 2<sup>-32</sup>-Sekunden-Intervallen ab 0h 1-Jan 1900) in ein lesbares Format. |
|**w32tm /resync [/computer:\<*Computer*>] [/nowait] [/rediscover] [/soft]** |Weist einen Computer an, seine Uhr so bald wie möglich neu zu synchronisieren, wobei alle gesammelten Fehlerstatistiken ausgegeben werden.<p>**/computer:\<*Computer*>** : Gibt den Computer an, der neu synchronisiert werden soll. Wenn der Parameter nicht angegeben ist, wird der lokale Computer neu synchronisiert.<p>**/nowait**: Nicht auf das Auftreten der Neusynchronisierung warten; sofort zurückgeben. Andernfalls auf Abschluss der Neusynchronisierung warten, bevor zurückgegeben wird.<p>**/rediscover**: Die Netzwerkkonfiguration erneut erkennen sowie Netzwerkquellen neu ermitteln, dann neu synchronisieren.<p>**/soft**: Neusynchronisierung mithilfe vorhandener Fehlerstatistiken. Nicht hilfreich; nur aus Kompatibilitätsgründen bereitgestellt. |
|**w32tm /stripchart /computer:\<*Ziel*> [/period:\<*Aktualisierung*>] [/dataonly] [/samples:\<*Anzahl*>] [/rdtsc]** |Zeigt ein Stripchart der Differenz zwischen diesem und einem anderen Computer an.<p>**/computer:\<*Ziel*>** : Der Computer gegenüber dem die Differenz gemessen werden soll.<p>**/period:\<*Aktualisierung*>** : Die Zeit zwischen Abtastungen, in Sekunden. Der Standardwert ist zwei Sekunden.<p>**/dataonly**: Zeigt nur die Daten an, ohne Grafiken.<p>**/samples:\<*Anzahl*>** : Erfasst \<*Anzahl*> Stichproben und hört dann auf. Wenn nicht angegeben, werden Stichproben erfasst, bis **STRG+C** gedrückt wird.<br/><br/>**/rdtsc**: Für jede Stichprobe gibt diese Option durch Kommas getrennte Werte zusammen mit den Headern **RdtscStart**, **RdtscEnd**, **FileTime**, **RoundtripDelay** und **NtpOffset** anstelle der Textgrafik aus.<br/><ul><li>**RdtscStart**: [Der RDTSC-Wert (Zähler für gelesene Zeitstempel)](https://en.wikipedia.org/wiki/Time_Stamp_Counter), der unmittelbar vor dem Generieren der NTP-Anforderung erfasst wurde.</li><li>**RdtscEnd**: Der RDTSC-Wert (Zähler für gelesene Zeitstempel), der unmittelbar nach dem Empfang und der Verarbeitung der NTP-Anforderung erfasst wurde.</li><li>**FileTime**: Der lokale FILETIME-Wert, der in der NTP-Anforderung verwendet wird.</li><li>**RoundtripDelay**: Die verstrichene Zeit in Sekunden zwischen dem Generieren der NTP-Anforderung und der Verarbeitung der empfangenen NTP-Antwort, berechnet gemäß den NTP-Roundtripberechnungen.</li><li>**NTPOffset**: Die Zeitdifferenz in Sekunden zwischen dem lokalen Computer und dem NTP-Server, berechnet gemäß den NTP-Differenzberechnungen.</li></ul> |
|**w32tm /config [/computer:\<*Ziel*>] [/update] [/manualpeerlist:\<*Peers*>] [/syncfromflags:\<*Quelle*>] [/LocalClockDispersion:\<*Sekunden*>] [/reliable:(YES\|NO)] [/largephaseoffset:\<*Millisekunden*>]** |**/computer:\<*Ziel*>** : Passt die Konfiguration von \<*Ziel*> an. Wenn nicht angegeben, ist der Standardwert der lokale Computer.<p>**/update**: Benachrichtigt den Zeitdienst, dass sich die Konfiguration geändert hat, wodurch die Änderungen wirksam werden.<p>**/manualpeerlist:\<*Peers*>** : Legt die manuelle Peerliste auf \<*Peers*> fest, wobei es sich um eine durch Leerzeichen getrennte Liste von DNS- und/oder IP-Adressen handelt. Wenn du mehrere Peers angibst, muss diese Option in Anführungszeichen stehen.<p>**/syncfromflags:\<*Quelle*>** : Legt fest, mit welchen Quellen der NTP-Client synchronisiert werden soll. \<*Quelle*> sollte eine durch Kommas getrennte Liste dieser Schlüsselwörter sein (ohne Berücksichtigung von Groß-/Kleinschreibung):<ul><li>**MANUAL**: Schließt Peers aus der manuellen Peerliste ein.</li><li>**DOMHIER**: Synchronisierung mit einem Domänencontroller (DC) in der Domänenhierarchie.</li></ul>**/LocalClockDispersion:\<*Sekunden*>** : Konfiguriert die Genauigkeit der internen Uhr, die W32Time verwendet, wenn keine Zeit aus den konfigurierten Quellen abgerufen werden kann.<p>**/reliable:(YES\|NO)** : Festlegen, ob dieser Computer eine zuverlässige Zeitquelle ist. Diese Einstellung ist nur auf Domänencontrollern sinnvoll.<ul><li>**YES**: Dieser Computer ist ein zuverlässiger Zeitdienst.</li><li>**NO**: Dieser Computer ist kein zuverlässiger Zeitdienst.</li></ul>**/largephaseoffset:\<*Millisekunden*>** : Legt den Zeitunterschied zwischen lokaler und Netzwerkzeit fest, den W32Time als Spitze interpretiert. |
|**w32tm /tz** |Zeigt die aktuellen Zeitzoneneinstellungen an. |
|**w32tm /dumpreg [/subkey:\<*Schlüssel*>] [/computer:\<*Ziel*>]** |Zeigt die einem angegebenen Registrierungsschlüssel zugeordneten Werte an.<p>Der Standardschlüssel ist **HKLM\System\CurrentControlSet\Services\W32Time** (der Stammschlüssel für den Zeitdienst).<p>**/subkey:\<*Schlüssel*>** : Zeigt die Werte an, die dem Unterschlüssel <key> des Standardschlüssels zugeordnet sind.<p>**/computer:\<*Ziel*>** : Fragt Registrierungseinstellungen für den Computer \<*Ziel*> ab. |
|**w32tm /query [/computer:\<*Ziel*>] {/source \| /configuration \| /peers \| /status} [/verbose]** |Zeigt die Informationen zum Windows-Zeitdienst eines Computers an. Dieser Parameter wurde zunächst im Windows-Zeitclient von Windows Vista und Windows Server 2008 zur Verfügung gestellt.<p>**/computer:\<*Ziel*>** : Fragt die Informationen von \<*Ziel*> ab. Wenn nicht angegeben, ist der Standardwert der lokale Computer.<p>**/source**: Zeigt die Zeitquelle an.<p>**/configuration**: Zeigt die Konfiguration der Laufzeit an sowie woher die Einstellung stammt. Zeigt im ausführlichen Modus („verbose“) auch die nicht definierte oder nicht verwendete Einstellung an.<p>**/peers**: Zeigt eine Liste von Peers und deren Status an.<p>**/status**: Zeigt den Status des Windows-Zeitdiensts an.<p>**/verbose**: Legt den ausführlichen Modus fest, um weitere Informationen anzuzeigen. |
|**w32tm /debug {/disable \| {/enable /file:\<*Name*> /size:/<*Bytes*> /entries:\<*Wert*> [/truncate]}}** |Aktivieren oder Deaktivieren des privaten Protokolls des Windows-Zeitdiensts auf dem lokalen Computer. Dieser Parameter wurde zunächst im Windows-Zeitclient von Windows Vista und Windows Server 2008 zur Verfügung gestellt.<p>**/disable**: Deaktiviert das private Protokoll.<p>**/enable**: Aktiviert das private Protokoll.<ul><li>**file:\<*Name*>** : Gibt den absoluten Dateinamen an.</li><li>**size:\<*Bytes*>** : Gibt die maximale Größe für die Umlaufprotokollierung an.</li><li>**entries:\<*Wert*>** : Enthält eine Liste von Kennzeichen, durch Nummern angegeben und durch Kommas getrennt, die die Typen von Informationen angeben, die protokolliert werden sollen. Gültige Nummern sind 0 bis 300. Ein Bereich von Nummern ist, zusätzlich zu einzelnen Nummern, gültig, z. B. 0–100,103,106. Der Wert 0–300 dient zum Protokollieren aller Informationen.</li></ul>**/truncate**: Die Datei abschneiden, falls vorhanden. |

Weitere Informationen zu **W32tm.exe** findest du in der [Windows-Hilfe](https://support.microsoft.com/hub/4338813/windows-help?os=windows-10).  

**Beispiele**

Wenn du den lokalen Windows-Zeitclient so einstellen möchtest, dass er auf zwei verschiedene Zeitserver verweist (einen mit dem Namen „ntpserver.contoso.com“ und einen mit dem Namen „clock.adatum.com“), gib den folgenden Befehl in die Befehlszeile ein und drücke dann die EINGABETASTE:

```cmd
w32tm /config /manualpeerlist:"ntpserver.contoso.com clock.adatum.com" /syncfromflags:manual /update
```

Eine Liste gültiger NTP-Server, die im Internet für die externe Zeitsynchronisierung verfügbar sind, findest du unter [Eine Liste der im Internet verfügbaren SNTP-Zeitserver (Simple Network Time Protocol)](https://go.microsoft.com/fwlink/?linkid=60401).

Wenn du die Konfiguration des Windows-Zeitclients von einem Windows-basierten Clientcomputer mit dem Hostnamen CONTOSOW1 aus überprüfen möchtest, führe den folgenden Befehl aus:

```cmd
W32tm /query /computer:contosoW1 /configuration
```

Die Ausgabe dieses Befehls ist eine Liste von Konfigurationsparametern, die für den Windows-Zeitclient eingestellt werden.

## <a name="using-group-policy-to-configure-the-windows-time-service"></a>Verwenden von Gruppenrichtlinien zur Konfiguration des Windows-Zeitdiensts

Der Windows-Zeitdienst speichert eine Reihe von Konfigurationseigenschaften als Registrierungseinträge. Du kannst Gruppenrichtlinienobjekte verwenden, um die meisten dieser Informationen zu konfigurieren. Du kannst z. B. GPOs verwenden, um einen Computer als NTPServer oder NTPClient zu konfigurieren, den Zeitsynchronisationsmechanismus zu konfigurieren oder einen Computer als zuverlässige Zeitquelle zu konfigurieren.  

> [!NOTE]  
> Gruppenrichtlinieneinstellungen für den Windows-Zeitdienst können unter Windows Server 2003-, Windows Server 2003 R2-, Windows Server 2008- und Windows Server 2008 R2-Domänencontrollern konfiguriert und nur auf Computer unter Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 angewendet werden.  

Windows speichert die Richtlinieninformationen des Windows-Zeitdiensts in der administrativen Vorlagendatei „W32Time.admx“ unter **Computer Configuration\Administrative Templates\System\Windows Time Service**. Es speichert die Konfigurationsinformationen, die die Richtlinien in der Registrierung definieren, und verwendet diese Registrierungseinträge, um die Registrierungseinträge für den Windows-Zeitdienst zu konfigurieren. Infolgedessen überschreiben die durch die Gruppenrichtlinie definierten Werte alle bereits vorhandenen Werte im Abschnitt des Windows-Zeitdiensts der Registrierung.

> [!IMPORTANT]  
> Einige der voreingestellten GPO-Einstellungen unterscheiden sich von den entsprechenden standardmäßigen Registrierungseinträgen. Wenn du beabsichtigst, ein Gruppenrichtlinienobjekt zum Konfigurieren von Windows-Zeiteinstellungen zu verwenden, stelle sicher, dass du [Voreingestellten Werte für den Gruppenrichtlinieneinstellungen des Windows-Zeitdiensts unterscheiden sich von den entsprechenden Registrierungseinträgen für den Windows-Zeitdienst in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066) liest. Dieses Problem liegt vor bei: Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 und Windows Server 2003.

Nimm z. B. an, du bearbeitest Richtlinieneinstellungen in der Richtlinie **Windows-NTP-Client konfigurieren**.

Die Änderungen werden an der folgenden Stelle in der administrativen Vorlage gespeichert:

> **Computer Configuration\Administrative Templates\System\Windows Time Service\Time Providers\Configure Windows NTP Client**

Windows lädt diese Einstellungen in den Richtlinienbereich der Registrierung unter dem folgenden Unterschlüssel:

> **HKLM\Software\Policies\Microsoft\W32time\TimeProviders\NtpClient**

Dann verwendet Windows die Richtlinieneinstellungen, um die zugehörigen Registrierungseinträge des Windows-Zeitdiensts unter dem folgenden Unterschlüssel zu konfigurieren:

> **HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Time Providers\NTPClient\\**

In der folgenden Tabelle sind die Richtlinien aufgeführt, die du für den Windows-Zeitdienst konfigurieren kannst, sowie die Registrierungsunterschlüssel, die von diesen Richtlinien betroffen sind.

> [!NOTE]  
> Wenn du eine Gruppenrichtlinieneinstellung entfernst, entfernt Windows den entsprechenden Eintrag aus dem Richtlinienbereich der Registrierung.

|Richtlinie<sup>1</sup> |Registrierungsspeicherorte<sup>2,</sup> <sup>3</sup> |
| --- | --- |
|Globale Konfigurationseinstellungen |W32Time<br />W32Time\Config<br />W32Time\Parameters |
|Time Providers\Configure Windows NTP Client |W32Time\TimeProviders\NtpClient |
|Time Providers\Enable Windows NTP Client |W32Time\TimeProviders\NtpClient |
|Time Providers\Enable Windows NTP Server |W32Time\TimeProviders\NtpServer |

> <sup>1</sup> Kategoriepfad: **Computer Configuration\Administrative Templates\System\Windows Time Service**  
> <sup>2</sup> Unterschlüssel: **HKLM\SOFTWARE\Policies\Microsoft**  
> <sup>3</sup> Unterschlüssel: **HKLM\SYSTEM\CurrentControlSet\Services**

## <a name="enabling-w32time-logging"></a>Aktivieren der W32Time-Protokollierung

Die folgenden drei Registrierungseinträge sind nicht Teil der W32Time-Standardkonfiguration, können der Registrierung aber hinzugefügt werden, um erweiterte Protokollierungsfunktionen zu erhalten. Die im Systemereignisprotokoll protokollierten Informationen können angepasst werden, indem der Wert für die **EventLogFlags**-Einstellung im Gruppenrichtlinienobjekt-Editor geändert wird. Standardmäßig protokolliert der Zeitdienst jedes Mal ein Ereignis, wenn er zu einer neuen Zeitquelle wechselt.

Füge die folgenden Registrierungseinträge hinzu, um die W32Time-Protokollierung zu aktivieren:  

|Registrierungseintrag |Versionen |Beschreibung |
| --- | --- | --- |
|**FileLogEntries** |Alle Versionen |Kontrolliert die Anzahl der Einträge, die in der Windows-Zeitprotokolldatei erstellt werden. Der Standardwert ist „None“ (Keine), bei dem keine Windows-Zeitaktivitäten protokolliert werden. Gültige Werte sind **0** bis **300**. Dieser Wert hat keine Auswirkungen auf die Ereignisprotokolleinträge, die normalerweise von Windows-Zeit erstellt werden. |
|**FileLogName** |Alle Versionen |Kontrolliert den Speicherort und Dateinamen des Windows-Zeitprotokolls. Der Standardwert ist leer und sollte nur geändert werden, wenn **FileLogEntries** geändert wird. Ein gültiger Wert ist ein vollständiger Pfad und Dateiname, die Windows-Zeit zum Erstellen der Protokolldatei verwendet. Dieser Wert hat keine Auswirkungen auf die Ereignisprotokolleinträge, die normalerweise von Windows-Zeit erstellt werden. |
|**FileLogSize** |Alle Versionen |Kontrolliert das Verhalten der Umlaufprotokollierung von Windows-Zeitprotokolldateien. Wenn **FileLogEntries** und **FileLogName** definiert sind, definiert der Eintrag die Größe (in Bytes), die die Protokolldatei erreichen darf, bevor die ältesten Protokolleinträge mit neuen Einträgen überschrieben werden. Verwende **1000000** oder einen größeren Wert für diese Einstellung. Dieser Wert hat keine Auswirkungen auf die Ereignisprotokolleinträge, die normalerweise von Windows-Zeit erstellt werden. |

## <a name="configuring-how-windows-time-service-resets-the-computer-clock"></a>Konfigurieren, wie der Windows-Zeitdienst die Computeruhr zurücksetzt

Damit W32Time die Computeruhr graduell stellt, muss die Differenz kleiner als der Wert von **MaxAllowedPhaseOffset** sein und gleichzeitig die folgende Gleichung erfüllen:  

- Windows Server 2016 und höhere Versionen:

  > |**CurrentTimeOffset**| &divide; (16 &times; **PhaseCorrectRate** &times; **pollIntervalInSeconds**) &le; **SystemClockRate** &divide; 2  

- Windows Server 2012 R2 und frühere Versionen:

  > |**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2  

Der **CurrentTimeOffset**-Wert wird in Zeiteinheiten gemessen, wobei 1 ms = 10.000 Zeiteinheiten in einem Windows-System ist.  

**SystemClockRate** und **PhaseCorrectRate** werden ebenfalls in Zeiteinheiten gemessen. Um den **SystemClockRate**-Wert zu erhalten, kannst du folgenden Befehl verwenden und ihn von Sekunden in Zeiteinheiten konvertieren, indem du die Formel *Sekunden* &times; 1.000 &times; 10.000 verwendest:  

```cmd
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  

**SystemClockRate** ist die Taktfrequenz der Systemuhr. Bei Verwendung von 156,000 Sekunden als Beispiel wäre der Wert von **SystemClockRate** = 0,0156000 &times; 1.000 &times; 10.000 = 156.000 Zeiteinheiten.  

**MaxAllowedPhaseOffset** wird ebenfalls in Sekunden gemessen. Um den Wert in Zeiteinheiten umzuwandeln, multipliziere **MaxAllowedPhaseOffset** &times; 1.000 &times; 10.000.  

In den folgenden Beispielen wird gezeigt, wie diese Berechnungen angewendet werden, wenn du Windows Server 2012 R2 oder eine niedrigere Version verwendest.

**Beispiel 1: Die Zeit weicht um vier Minuten ab**

Deine Zeit ist 11:05 Uhr und die Zeitstichprobe, die du von einem Peer erhalten hast, und die du für richtig hältst, ist 11:09 Uhr.

> **PhaseCorrectRate** = 1  
>  
> **UpdateInterval** = 30.000 Zeiteinheiten  
>  
> **SystemClockRate** = 156.000 Zeiteinheiten  
>  
> **MaxAllowedPhaseOffset** = 10 Minuten = 600 Sekunden = 600 &times; 1.000 &times; 10.000 = 6.000.000.000 Zeiteinheiten  
>  
> |**CurrentTimeOffset**| = 4 Minuten = 4 &times; 60 &times; 1.000 &times; 10.000 = 2.400.000.000 Zeiteinheiten  
>  
> Ist **CurrentTimeOffset** &le; **MaxAllowedPhaseOffset**?  
>  
> 2\.400.000.000 &le; 6.000.000.000: TRUE  

UND erfüllt sie die obige Gleichung?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)  

Ist 2.400.000.000 / (30.000 &times; 1) &le; 156.000 &divide; 2  

80.000 &le; 78.000: FALSE  

Deshalb würde W32tm die Uhr sofort zurückstellen.  

> [!NOTE]  
> Wenn du in diesem Fall die Uhr wieder langsam zurückstellen möchtest, müsstest du auch die Werte von **PhaseCorrectRate** oder **UpdateInterval** in der Registrierung anpassen, um sicherzustellen, dass das Ergebnis der Gleichung **TRUE** ist.  

**Beispiel 2: Die Zeit weicht um drei Minuten ab**

> **PhaseCorrectRate** = 1  
> 
> **UpdateInterval** = 30.000 Zeiteinheiten  
> 
> SystemClockRate = 156.000 Zeiteinheiten  
> 
> **MaxAllowedPhaseOffset** = 10 Minuten = 600 Sekunden = 600 &times; 1.000 &times; 10.000 = 6.000.000.000 Zeiteinheiten  
> 
> |**CurrentTimeOffset**| = 3 Minuten = 3 &times; 60 &times; 1.000 &times; 10.000 = 1.800.000.000 Zeiteinheiten  
> 
> Ist |**CurrentTimeOffset**| &le; **MaxAllowedPhaseOffset**?  
> 
> 1\.800.000.000 &le; 6.000.000.000: TRUE  

UND erfüllt sie die obige Gleichung?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)  
> 
> Ist 3 Minuten &times; (1.800.000.000) &divide; (30.000 &times; 1) &le; 156.000 &divide; 2  
> 
> Ist 60.000 &le; 78.000: TRUE  

In diesem Fall wird die Uhr langsam zurückgestellt.  

## <a name="reference-windows-time-service-registry-entries"></a>Referenz: Registrierungseinträge des Windows-Zeitdiensts

> [!WARNING]  
> Die Informationen zu diesen Registrierungseinträgen dienen als Referenz, die du bei einer Problembehandlung oder der Überprüfung, ob die erforderlichen Einstellungen angewendet sind, verwenden kannst. Viele der Werte im Abschnitt „W32Time“ der Registrierung werden intern von W32Time verwendet, um Informationen zu speichern. Ändere diese Werte nicht manuell. Änderungen an der Registrierung werden weder vom Registrierungs-Editor noch von Windows überprüft, bevor sie angewendet werden. Wenn die Registrierung ungültige Werte enthält, kann es unter Windows zu nicht behebbaren Fehlern kommen.  

Der Windows-Zeitdienst speichert Informationen unter den folgenden Registrierungsunterschlüsseln:

- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config**](#config)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters**](#parameters)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient**](#ntpclient)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer**](#ntpserver)

Zusätzlich kannst du zu Zwecken der Problembehandlung [Einträge hinzufügen, um Protokolle zu konfigurieren](#enabling-w32time-logging).

In den folgenden Tabellen bezieht sich „Alle Versionen“ auf Windows-Versionen, zu denen Windows 7, Windows 8, Windows 10, Windows Server 2008 und Windows Server 2008 R2, Windows Server 2012 und Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 gehören. Einige Einträge sind nur in höheren Windows-Versionen verfügbar.

> [!NOTE]  
> Einige der Parameter in der Registrierung werden in Zeiteinheiten und andere in Sekunden gemessen. Verwende die folgenden Konvertierungsfaktoren, um die Zeit von Zeiteinheiten in Sekunden umzuwandeln:  
> - 1 Minute = 60 Sek.  
> - 1 Sek. = 1.000 ms  
> - 1 ms = 10.000 Zeiteinheiten bei einem Windows-System, wie unter [DateTime.Ticks-Eigenschaft](https://docs.microsoft.com/dotnet/api/system.datetime.ticks) beschrieben.  
>  
> Beispielsweise werden 5 Minuten zu 5 &times; 60 &times; 1000 &times; 10000 = 3.000.000.000 Zeiteinheiten.  

### <a name="hklmsystemcurrentcontrolsetservicesw32timeconfig-subkey-entries"></a><a id="config"></a>„HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config“ – Unterschlüsseleinträge

|Registrierungseintrag |Versionen |Beschreibung |
| --- | --- | --- |
|**AnnounceFlags** |Alle Versionen |Kontrolliert, ob dieser Computer als zuverlässiger Zeitserver markiert ist. Um als zuverlässig markiert zu werden, muss ein Computer auch als Zeitserver gekennzeichnet sein.<ul><li>**0x00**. Kein Zeitserver</li><li>**0x01**. Immer Zeitserver</li><li>**0x02**. Automatischer Zeitserver</li><li>**0x04**. Immer zuverlässiger Zeitserver</li><li>**0x08**. Automatischer zuverlässiger Zeitserver</li></ul><br />Der Standardwert für Domänenmitglieder ist **10**. Der Standardwert für eigenständige Clients und Server ist **10**. |
|**ChainDisable** | |Kontrolliert, ob der Verkettungsmechanismus deaktiviert ist. Wenn die Verkettung deaktiviert ist (auf 0 gesetzt), kann sich ein schreibgeschützter Domänencontroller (RODC) mit jedem beliebigen Domänencontroller synchronisieren, aber Hosts, deren Kennwörter nicht auf dem RODC zwischengespeichert sind, können nicht mit dem RODC synchronisiert werden. Dies ist eine boolesche Einstellung und der Standardwert ist **0**.|
|**ChainEntryTimeout** | |Gibt die maximale Zeitspanne an, die ein Eintrag in der Verkettungstabelle verbleiben kann, bevor der Eintrag als abgelaufen betrachtet wird. Abgelaufene Einträge können bei der Verarbeitung der nächsten Anforderung oder Antwort entfernt werden. Der Standardwert ist **16** (Sekunden). |
|**ChainLoggingRate** | |Kontrolliert die Häufigkeit, mit der ein Ereignis, das die Anzahl der erfolgreichen und erfolglosen Verkettungsversuche anzeigt, im Systemprotokoll der Ereignisanzeige protokolliert wird. Der Standardwert ist **30** (Minuten). |
|**ChainMaxEntries** | |Kontrolliert die maximale Anzahl von Einträgen, die in der Verkettungstabelle zulässig sind. Wenn die Verkettungstabelle voll ist und keine abgelaufenen Einträge entfernt werden können, werden alle eingehenden Anforderungen verworfen. Der Standardwert ist **128** (Einträge). |
|**ChainMaxHostEntries** | |Kontrolliert die maximale Anzahl von Einträgen, die in der Verkettungstabelle für einen bestimmten Host zulässig sind. Der Standardwert ist **4** (Einträge). |
|**ClockAdjustmentAuditLimit** |Windows Server 2016, Version 1709 und höhere Versionen; Windows 10, Version 1709 und höhere Versionen |Gibt die kleinsten lokalen Zeitanpassungen an, die im Ereignisprotokoll des W32time-Diensts auf dem Zielcomputer protokolliert werden können. Der Standardwert ist **800** (Teile pro Million – PPM). |
|**ClockHoldoverPeriod** |Windows Server 2016, Version 1709 und höhere Versionen; Windows 10, Version 1709 und höhere Versionen |Gibt die maximale Anzahl von Sekunden an, die eine Systemuhr nominell ihre Genauigkeit beibehalten kann, ohne sich mit einer Zeitquelle zu synchronisieren. Wenn diese Zeitspanne vergeht, ohne dass W32time neue Proben von einem seiner Eingabeanbieter erhält, leitet W32time eine erneute Erkennung von Zeitquellen ein. Standardwert: 7.800 Sekunden. |
|**EventLogFlags** |Alle Versionen |Kontrolliert die Ereignisse, die der Zeitdienst protokolliert.<ul><li>**0x1**. Zeitsprung</li><li>**0x2**. Änderung der Quelle</li></ul>Der Standardwert für Domänenmitglieder ist **2**. Der Standardwert für eigenständige Clients und Server ist **2**. |
|**FrequencyCorrectRate** |Alle Versionen |Kontrolliert die Häufigkeit, mit der die Uhr korrigiert wird. Wenn dieser Wert zu klein ist, ist die Uhr instabil und wird zu häufig korrigiert. Wenn der Wert zu groß ist, dauert es zu lange, bis die Uhr synchronisiert wird. Der Standardwert für Domänenmitglieder ist **4**. Der Standardwert für eigenständige Clients und Server ist **4**.<p>**Hinweis** <br />„0“ ist ein ungültiger Wert für den Registrierungseintrag **FrequencyCorrectRate**. Auf Computern unter Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 ändert der Windows-Zeitdienst den Wert automatisch in **1**, wenn er auf **0** festgelegt ist. |
|**HoldPeriod** |Alle Versionen |Kontrolliert den Zeitraum, über den die Spitzenerkennung deaktiviert ist, um die lokale Uhr schnell wieder zu synchronisieren. Eine Spitze ist eine Zeitstichprobe, die anzeigt, dass die Zeit eine Anzahl von Sekunden abweicht, und wird normalerweise empfangen, nachdem gute Zeitstichproben konsistent zurückgegeben wurden. Der Standardwert für Domänenmitglieder ist **5**. Der Standardwert für eigenständige Clients und Server ist **5**. |
|**LargePhaseOffset** |Alle Versionen |Gibt an, dass eine Zeitdifferenz von mehr als oder gleich diesem Wert in 10<sup>-7</sup> Sekunden als Spitze interpretiert wird. Eine Netzwerkstörung, wie z. B. eine hohe Menge an Datenverkehr, könnte eine Spitze verursachen. Eine Spitze wird ignoriert, wenn sie nicht über einen längeren Zeitraum besteht. Der Standardwert für Domänenmitglieder ist **50000000**. Der Standardwert für eigenständige Clients und Server ist **50000000**. |
|**LastClockRate** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Außerdem können Änderungen an dieser Einstellung zu unvorhersehbaren Ergebnissen führen. Der Standardwert für Domänenmitglieder ist **156250**. Der Standardwert für eigenständige Clients und Server ist **156250**. |
|**LocalClockDispersion** |Alle Versionen |Kontrolliert die Streuung (in Sekunden), die du voraussetzen musst, wenn die einzige Zeitquelle die integrierte CMOS-Uhr ist. Der Standardwert für Domänenmitglieder ist **10**. Der Standardwert für eigenständige Clients und Server ist **10**. |
|**MaxAllowedPhaseOffset** |Alle Versionen |Gibt die maximale Differenz (in Sekunden) an, bei der W32Time versucht, die Computeruhr mithilfe der Taktfrequenz anzupassen. Wenn die Differenz diese Frequenz übersteigt, stellt W32Time die Computeruhr direkt ein. Der Standardwert für Domänenmitglieder ist **300**. Der Standardwert für eigenständige Clients und Server ist **1**. Weitere Informationen findest du unter [Konfigurieren, wie der Windows-Zeitdienst die Computeruhr zurücksetzt](#configuring-how-windows-time-service-resets-the-computer-clock). |
|**MaxClockRate** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Außerdem können Änderungen an dieser Einstellung zu unvorhersehbaren Ergebnissen führen. Der Standardwert für Domänenmitglieder ist **155860**. Der Standardwert für eigenständige Clients und Server ist **155860**. |
|**MaxNegPhaseCorrection** |Alle Versionen |Gibt die größte negative Zeitkorrektur in Sekunden an, die der Dienst vornimmt. Wenn der Dienst feststellt, dass eine größere Änderung erforderlich ist, protokolliert er stattdessen ein Ereignis.<p>**Hinweis**<br />Der Wert **0xFFFFFFFFFF** ist ein Sonderfall. Dieser Wert bedeutet, dass der Dienst die Zeit immer korrigiert.<p>Der Standardwert für Domänenmitglieder ist **0xFFFFFFFF**. Der Standardwert für eigenständige Clients und Server ist **54.000**0 (15 Stunden).|
|**MaxPollInterval** |Alle Versionen |Gibt das größte Intervall in log2 Sekunden an, das für das Systemabrufintervall zulässig ist. Beachte, dass ein Anbieter, auch wenn ein System nach dem geplanten Intervall abfragen muss, die Erstellung von Stichproben ablehnen kann, wenn er dazu aufgefordert wird. Der Standardwert für Domänencontroller ist **10**. Der Standardwert für Domänenmitglieder ist **15**. Der Standardwert für eigenständige Clients und Server ist **15**. |
|**MaxPosPhaseCorrection** |Alle Versionen |Gibt die größte positive Zeitkorrektur in Sekunden an, die der Dienst vornimmt. Wenn der Dienst feststellt, dass eine größere Änderung erforderlich ist, protokolliert er stattdessen ein Ereignis.<p>**Hinweis**<br />Der Wert **0xFFFFFFFFFF** ist ein Sonderfall. Dieser Wert bedeutet, dass der Dienst die Zeit immer korrigiert.<p>Der Standardwert für Domänenmitglieder ist **0xFFFFFFFF**. Der Standardwert für eigenständige Clients und Server ist **54.000**0 (15 Stunden). |
|**MinClockRate** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Außerdem können Änderungen an dieser Einstellung zu unvorhersehbaren Ergebnissen führen. Der Standardwert für Domänenmitglieder ist **155860**. Der Standardwert für eigenständige Clients und Server ist **155860**. |
|**MinPollInterval** |Alle Versionen |Gibt das kleinste Intervall in log2 Sekunden an, das für das Systemabrufintervall zulässig ist. Beachte, dass ein Anbieter, auch wenn ein System Stichproben nicht häufiger als diesen Wert anfordert, Stichproben zu anderen Zeiten als dem geplanten Intervall erzeugen kann. Der Standardwert für Domänencontroller ist **6**. Der Standardwert für Domänenmitglieder ist **10**. Der Standardwert für eigenständige Clients und Server ist **10**. |
|**PhaseCorrectRate** |Alle Versionen |Kontrolliert die Häufigkeit, mit der der Phasenfehler korrigiert wird. Wenn du einen kleinen Wert angibst, wird der Phasenfehler schnell korrigiert, kann aber zur Instabilität der Uhr führen. Wenn der Wert zu groß ist, dauert es länger, den Phasenfehler zu beheben.<p>Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **7**.<p>**Hinweis**<br />„0“ ist ein ungültiger Wert für den Registrierungseintrag **PhaseCorrectRate**. Auf Computern unter Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 ändert der Windows-Zeitdienst den Wert automatisch in **1**, wenn er auf **0** festgelegt ist. |
|**PollAdjustFactor** |Alle Versionen |Kontrolliert die Entscheidung, das Abrufintervall für das System zu vergrößern oder zu verkleinern. Je größer der Wert ist, desto geringer ist das Fehlerausmaß, das bewirkt, dass das Abrufintervall verringert wird. Der Standardwert für Domänenmitglieder ist **5**. Der Standardwert für eigenständige Clients und Server ist **5**. |
|**RequireSecureTimeSyncRequests** |Windows 8 oder höher |Kontrolliert, ob der DC auf Zeitsynchronisierungsanforderungen reagiert, die ältere Authentifizierungsprotokolle verwenden. Wenn aktiviert (auf **1** gesetzt), reagiert der DC nicht auf Anforderungen, die solche Protokolle verwenden. Dies ist eine boolesche Einstellung und der Standardwert ist **0**. |
|**SpikeWatchPeriod** |Alle Versionen |Gibt die Zeitspanne an, die eine verdächtige Differenz vorhanden sein muss, bevor sie als richtig (in Sekunden) akzeptiert wird. Der Standardwert für Domänenmitglieder ist **900**. Der Standardwert für eigenständige Clients und Arbeitsstationen ist **900**. |
|**TimeJumpAuditOffset** |Alle Versionen |Eine ganze Zahl ohne Vorzeichen, die den Überwachungsschwellenwert für den Zeitsprung in Sekunden angibt. Wenn der Zeitdienst die lokale Uhr anpasst, indem die Uhr direkt gestellt wird, und die Zeitkorrektur höher als dieser Wert ist, protokolliert der Zeitdienst ein Überwachungsereignis. |
|**UpdateInterval** |Alle Versionen |Gibt die Anzahl der Zeiteinheiten zwischen Phasenkorrekturanpassungen an. Der Standardwert für Domänencontroller ist **100**. Der Standardwert für Domänenmitglieder ist **30.000**. Der Standardwert für eigenständige Clients und Server ist **360.000**.<p>**Hinweis**<br />„0“ ist kein ungültiger Wert für den Registrierungseintrag **UpdateInterval**. Auf Computern unter Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 ändert der Windows-Zeitdienst den Wert automatisch in **1**, wenn er auf **0** festgelegt ist.|
|**UtilizeSslTimeData** |Windows-Versionen, die höher als Windows 10 Build 1511 sind |Der Wert **1** gibt an, dass W32Time mehrere SSL-Zeitstempel verwendet, um ein Seeding einer Uhr vorzunehmen, die äußerst ungenau ist. |

### <a name="hklmsystemcurrentcontrolsetservicesw32timeparameters-subkey-entries"></a><a id="parameters"></a>„HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters“ – Unterschlüsseleinträge

| Registrierungseintrag | Versionen | Beschreibung |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |Alle Versionen |Gibt an, dass bei der Synchronisierung zwischen Peers nicht standardmäßige Moduskombinationen zulässig sind. Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **1**. |
|**NtpServer** |Alle Versionen |Gibt eine durch Leerzeichen getrennte Liste von Peers an, von denen ein Computer Zeitstempel einholt, bestehend aus einem/r oder mehreren DNS-Namen oder IP-Adressen pro Zeile. Jede/r aufgeführte DNS-Name oder IP-Adresse muss eindeutig sein. Computer, die mit einer Domäne verbunden sind, müssen sich mit einer zuverlässigeren Zeitquelle synchronisieren, z. B. der offiziellen Uhr der USA.  <ul><li>0x01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive: Weitere Informationen zu diesem Modus findest du unter [Windows-Zeitserver: 3.3 Betriebsmodi](https://go.microsoft.com/fwlink/?LinkId=208012).</li><li>0x08 Client</li></ul><br />Es gibt keinen Standardwert für diesen Registrierungseintrag für Domänenmitglieder. Der Standardwert für eigenständige Clients und Server ist „time.windows.com,0x1“.<p>**Hinweis**<br />Weitere Informationen zu verfügbaren NTP-Servern findest du in KB 262680 [Eine Liste der im Internet verfügbaren SNTP-Zeitserver (Simple Network Time Protocol)](https://support.microsoft.com/help/262680/a-list-of-the-simple-network-time-protocol-sntp-time-servers-that-are). |
|**ServiceDll** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Außerdem können Änderungen an dieser Einstellung zu unvorhersehbaren Ergebnissen führen. Der Standardort für diese DLL sowohl für Domänenmitglieder als auch für eigenständige Clients und Server ist „%windir%\System32\W32Time.dll“. |
|**ServiceMain** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Außerdem können Änderungen an dieser Einstellung zu unvorhersehbaren Ergebnissen führen. Der Standardwert für Domänenmitglieder ist **SvchostEntry_W32Time**. Der Standardwert für eigenständige Clients und Server ist **SvchostEntry_W32Time**. |
|**Type** |Alle Versionen |Gibt an, von welchen Peers Synchronisierung akzeptiert werden soll:  <ul><li>**NoSync**. Der Zeitdienst synchronisiert sich nicht mit anderen Quellen.</li><li>**NTP**. Der Zeitdienst synchronisiert sich mit den in **NtpServer** angegebenen Servern. Registrierungseintrag.</li><li>**NT5DS**. Der Zeitdienst synchronisiert sich mit der Domänenhierarchie.  </li><li>**AllSync**. Der Zeitdienst verwendet alle verfügbaren Synchronisierungsmechanismen.  </li></ul>Der Standardwert für Domänenmitglieder ist **NT5DS**. Der Standardwert für eigenständige Clients und Server ist **NTP**. |

### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpclient-subkey-entries"></a><a id="ntpclient"></a>„HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient“ – Unterschlüsseleinträge

|Registrierungseintrag |Version |Beschreibung |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |Alle Versionen |Gibt an, dass bei der Synchronisierung zwischen Peers nicht standardmäßige Moduskombinationen zulässig sind. Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **1**.|
|**CompatibilityFlags** |Alle Versionen |Gibt die folgenden Kompatibilitätskennzeichen und -werte an:<ul><li>**0x00000001** – DispersionInvalid</li><li>**0x00000002** – IgnoreFutureRefTimeStamp</li><li>**0x80000000** – AutodetectWin2K</li><li>**0x40000000** – AutodetectWin2KStage2</li></ul>Der Standardwert für Domänenmitglieder ist **0x80000000**. Der Standardwert für eigenständige Clients und Server ist **0x80000000**. |
|**CrossSiteSyncFlags** |Alle Versionen |Bestimmt, ob der Dienst Synchronisierungspartner außerhalb der Domäne des Computers auswählt. Die Optionen und Werte lauten wie folgt:<ul><li>**0** – None</li><li>**1** – PdcOnly</li><li>**2** – All</li></ul>Dieser Wert wird ignoriert, wenn der NT5DS-Wert nicht festgelegt ist. Der Standardwert für Domänenmitglieder ist **2**. Der Standardwert für eigenständige Clients und Server ist **2**. |
|**DllName** |Alle Versionen |Gibt den Speicherort der DLL für den Zeitanbieter an.<p>Der Standardort für diese DLL sowohl für Domänenmitglieder als auch für eigenständige Clients und Server ist **%windir%\System32\W32Time.dll**. |
|**Aktiviert** |Alle Versionen |Gibt an, ob der NtpClient-Anbieter im aktuellen Zeitdienst aktiviert ist.<ul><li>**1** – Ja</li><li>**0** – Nein</li></ul>Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **1**.|
|**EventLogFlags** |Alle Versionen |Gibt die vom Windows-Zeitdienst protokollierten Ereignisse an.<ul><li>**0x1** – Erreichbarkeitsänderungen</li><li>**0x2** – Große Stichprobenabweichung (Dies liegt nur bei Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 vor.)</li></ul>Der Standardwert für Domänenmitglieder ist **0x1**. Der Standardwert für eigenständige Clients und Server ist **0x1**.|
|**InputProvider** |Alle Versionen |Gibt an, ob der NtpClient als „InputProvider“ aktiviert werden soll, der Zeitinformationen vom NtpServer abruft. Der NtpServer ist ein Zeitserver, der auf Zeitanforderungen von Clients im Netzwerk reagiert, indem er Zeitstichproben zurückgibt, die für die Synchronisierung der lokalen Uhr nützlich sind. <ul><li>**1** – Ja</li><li>**0** – Nein</li></ul>Der Standardwert für Domänenmitglieder und eigenständige Clients ist **1**. |
|**LargeSampleSkew** |Alle Versionen |Gibt die große Stichprobenabweichung für die Protokollierung in Sekunden an. Um die SEC-Spezifikationen (Security and Exchange Commission) einzuhalten, sollte dieser Wert auf drei Sekunden festgelegt werden. Ereignisse werden nur dann für diese Einstellung protokolliert, wenn **EventLogFlags** explizit für „0x2-große Stichprobenabweichung“ konfiguriert ist. Der Standardwert für Domänenmitglieder ist 3. Der Standardwert für eigenständige Clients und Server ist 3. |
|**ResolvePeerBackOffMaxTimes** |Alle Versionen |Gibt an, wie oft das Wartezeitintervall maximal verdoppelt werden soll, wenn wiederholte Versuche, einen Peer für die Synchronisierung aufzufinden, fehlschlagen. Ein Wert von 0 bedeutet, dass das Warteintervall immer das Minimum ist. Der Standardwert für Domänenmitglieder ist **7**. Der Standardwert für eigenständige Clients und Server ist **7**. |
|**ResolvePeerBackoffMinutes** |Alle Versionen |Gibt das anfängliche Intervall in Minuten an, das gewartet werden soll, bevor versucht wird, einen Peer für die Synchronisierung aufzufinden. Der Standardwert für Domänenmitglieder ist **15**. Der Standardwert für eigenständige Clients und Server ist **15**.  |
|**SpecialPollInterval** |Alle Versionen |Gibt das spezifische Abrufintervall in Sekunden für manuelle Peers an. Wenn das Flag **SpecialInterval** 0x1 aktiviert ist, verwendet W32Time dieses Abrufintervall anstelle eines vom Betriebssystem festgelegten Abrufintervalls. Der Standardwert für Domänenmitglieder ist **3.600**. Der Standardwert für eigenständige Clients und Server ist **604.800**.<br/><br/>Neu für Build 1703; **SpecialPollInterval** ist in den Konfigurationsregistrierungswerten **MinPollInterval** und **MaxPollInterval** enthalten.|
|**SpecialPollTimeRemaining** |Alle Versionen |Wird von W32Time verwaltet. Er enthält reservierte Daten, die vom Windows-Betriebssystem verwendet werden. Gibt die Zeit in Sekunden an, nach der W32Time nach einem Neustart des Computers erneut synchronisiert wird. Änderungen an dieser Einstellung können zu unvorhersehbaren Ergebnissen führen. Als Standardwert für Domänenmitglieder sowie eigenständige Clients und Server bleibt die Einstellung leer. |

### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpserver-subkey-entries"></a><a id="ntpserver"></a>„HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer“ – Unterschlüsseleinträge

|Registrierungseintrag |Versionen |Beschreibung |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |Alle Versionen |Gibt an, dass bei der Synchronisierung zwischen Clients und Servern nicht standardmäßige Moduskombinationen zulässig sind. Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **1**. |
|**DllName** |Alle Versionen |Gibt den Speicherort der DLL für den Zeitanbieter an. Der Standardort für diese DLL sowohl für Domänenmitglieder als auch für eigenständige Clients und Server ist **%windir%\System32\W32Time.dll**.  |
|**Aktiviert** |Alle Versionen |Gibt an, ob der NtpServer-Anbieter im aktuellen Zeitdienst aktiviert ist. <ul><li>**1** – Ja</li><li>**0** – Nein</li></ul>Der Standardwert für Domänenmitglieder ist **1**. Der Standardwert für eigenständige Clients und Server ist **1**. |
|**InputProvider** |Alle Versionen |Gibt an, ob der NtpClient als „InputProvider“ aktiviert werden soll, der Zeitinformationen vom NtpServer abruft. Der NtpServer ist ein Zeitserver, der auf Zeitanforderungen von Clients im Netzwerk reagiert, indem er Zeitstichproben zurückgibt, die für die Synchronisierung der lokalen Uhr nützlich sind. <ul><li>**1** – Ja</li><li>**0** – Nein = 0 </li></ul>Der Standardwert für Domänenmitglieder und eigenständige Clients ist: 1 |

## <a name="reference-pre-set-values-for-the-windows-time-service-gpo-settings"></a>Referenz: Voreingestellte Werte für die GPO-Einstellungen des Windows-Zeitdiensts  

In der folgenden Tabelle sind die globalen Gruppenrichtlinieneinstellungen aufgelistet, die dem Windows-Zeitdienst zugeordnet sind, sowie die vorab festgelegten Werte, die jeder einzelnen Einstellung zugeordnet sind. Weitere Informationen zu den einzelnen Einstellungen findest du in den entsprechenden Registrierungseinträgen unter [Referenz: Registrierungseinträge des Windows-Zeitdiensts](#reference-windows-time-service-registry-entries) weiter oben in diesem Artikel. Die folgenden Einstellungen befinden sich in einem einzelnen Gruppenrichtlinienobjekt namens **Globale Konfigurationseinstellungen**.  

### <a name="pre-set-values-for-global-group-policy-settings"></a>Voreingestellte Werte für Einstellungen für „Globale Gruppenrichtlinien“

|Gruppenrichtlinieneinstellung|Voreingestellter Wert|  
| --- | --- |
|**AnnounceFlags**|**10**|  
|**EventLogFlags**|**2**|  
|**FrequencyCorrectRate**|**4**|  
|**HoldPeriod**|**5**|  
|**LargePhaseOffset**|**1.280.000**|  
|**LocalClockDispersion**|**10**|  
|**MaxAllowedPhaseOffset**|**300**|  
|**MaxNegPhaseCorrection**|**54.000** (15 Stunden)|  
|**MaxPollInterval**|**15**|  
|**MaxPosPhaseCorrection**|**54.000** (15 Stunden)|  
|**MinPollInterval**|**10**|  
|**PhaseCorrectRate**|**7**|  
|**PollAdjustFactor**|**5**|  
|**SpikeWatchPeriod**|**90**|  
|**UpdateInterval**|**100**|  

### <a name="pre-set-values-for-configure-windows-ntp-client-settings"></a>Voreingestellte Werte für die Einstellungen für „Windows-NTP-Client konfigurieren“

In der folgenden Tabelle sind die verfügbaren Einstellungen für das Gruppenrichtlinienobjekt **Windows-NTP-Client konfigurieren** sowie die vorab festgelegten Werte, die dem Windows-Zeitdienst zugeordnet sind, aufgelistet. Weitere Informationen zu den einzelnen Einstellungen findest du in den entsprechenden Registrierungseinträgen unter [Referenz: Registrierungseinträge des Windows-Zeitdiensts](#reference-windows-time-service-registry-entries) weiter oben in diesem Artikel.  

|Gruppenrichtlinieneinstellung|Voreingestellter Wert|  
|------------------------|-----------------|  
|**NtpServer**|time.windows.com, **0x1**|  
|**Type**|Standardoptionen:<ul><li>**NTP.** Zur Verwendung auf Computern, die keiner Domäne beigetreten sind.</li><li>**NT5DS.** Zur Verwendung auf Computern, die einer Domäne beigetreten sind.</li></ul>|  
|**CrossSiteSyncFlags**|**2**|  
|**ResolvePeerBackoffMinutes**|**15**|  
|**ResolvePeerBackoffMaxTimes**|**7**|  
|**SpecialPollInterval**|**3.600**|  
|**EventLogFlags**|**0**|  

## <a name="reference-network-ports-that-the-windows-time-service-uses"></a>Referenz: Vom Windows-Zeitdienst verwendete Netzwerkports

Die Windows-Zeit hält die NTP-Spezifikation ein, die die Verwendung des UDP-Ports 123 für die gesamte Zeitsynchronisierungskommunikation erfordert. Dieser Port ist für die Windows-Zeit reserviert und bleibt jederzeit reserviert. Immer wenn der Computer seine Uhr synchronisiert oder einem anderen Computer die Zeit bereitstellt, erfolgt diese Kommunikation über den UDP-Port 123.  

> [!NOTE]  
> Wenn du über einen Computer mit mehreren Netzwerkadaptern verfügst (auch als *mehrfach vernetzter* Computer bezeichnet), kannst du den Windows-Zeitdienst nicht selektiv, basierend auf dem Netzwerkadapter aktivieren.  

## <a name="related-information"></a>Verwandte Informationen  

Die folgenden Ressourcen enthalten weitere Informationen, die für diesen Abschnitt relevant sind.  

- RFC *1305* in der IETF RFC-Datenbank  
