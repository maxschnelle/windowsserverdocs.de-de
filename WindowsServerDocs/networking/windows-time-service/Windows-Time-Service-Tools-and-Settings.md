---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: 'Windows-Zeitdienst: Tools und Einstellungen'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 70b7ee4a9955e023d1664a3c29295a22cd5dc75b
ms.sourcegitcommit: fd6a46b702b235f38d90814dd769106ab37cd61b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="windows-time-service-tools-and-settings"></a>Windows-Zeitdienst: Tools und Einstellungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


**In diesem Abschnitt**  
  
-   [Windows-Zeitdienst: Tools](#w2k3tr_times_tools_dyax)  
  
-   [Registrierungseinträge Windows-Zeitdienst](#w2k3tr_times_tools_uhlp)  
  
-   [Windows Time Service mithilfe von Gruppenrichtlinieneinstellungen](#w2k3tr_times_tools_vwtt)  
  
-   [Netzwerk-Ports, die von der Windows-Zeitdienst verwendet](#w2k3tr_times_tools_suxb)  
  
-   [Verwandte Informationen](#w2k3tr_times_tools_qoep)  
  
> [!NOTE]  
> Dieses Thema enthält Informationen, die nur über Tools und Einstellungen für Windows-Zeitdienst (W32Time). Wenn Sie nur die Zeit für eine Domäne eingebundenen Clientcomputer synchronisieren möchten, finden Sie unter [Konfigurieren eines Clientcomputers für automatischen Synchronisierung](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29). Zusätzliche Themen zur Vorgehensweise beim Konfigurieren der Windows-Zeitdienst finden Sie in der Liste der Themen im Abschnitt [, wo Sie Windows Time Service-Konfigurationsinformationen finden](https://technet.microsoft.com/library/cc773061.aspx).  
  
> [!CAUTION]  
> Sie sollten nicht mit dem Befehl Net Time verwenden, konfigurieren oder Festlegen der Uhrzeit, wenn der Windows-Zeitdienst ausgeführt wird.  

Darüber hinaus auf älteren Computern mit Windows XP oder früher: der Befehl Net Time /querysntp zeigt den Namen eines Servers Netzwerkzeitprotokoll (NTP), mit dem ein Computer für die Synchronisierung konfiguriert, aber die NTP-Server wird verwendet, nur dann, wenn der Computer Zeit Client als NTP oder AllSync konfiguriert ist. Dieser Befehl ist mittlerweile veraltet.  
  
Die meisten Domänenmitgliedscomputer ist eine Zeit Client NT5DS, was bedeutet, dass sie Zeit aus der Domäne zu synchronisieren. Nur normalerweise eine Ausnahme ist der Domänencontroller, der als primärer Domänencontroller (PDC) Emulationsbetriebsmaster des der Stammdomäne der Gesamtstruktur, der in der Regel konfiguriert ist fungiert, Zeit mit einer externen Zeitquelle synchronisieren. Führen Sie zum Anzeigen der Konfiguration eines Computers Client W32tm//query /configuration Befehl von einer Eingabeaufforderung mit erhöhten Rechten in Windows Server 2008 und Windows Vista ab, und Lesen Sie die **Typ** Zeile in der Ausgabe des Befehls. Weitere Informationen finden Sie unter [wie Windows-Dienst kann](https://go.microsoft.com/fwlink/?LinkId=117753). Sie können den Befehl ausführen **Reg Query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** und den Wert der **NtpServer** in der Ausgabe des Befehls.  
  
> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht für zeitabhängige Anwendung Anforderungen entwickelt.  Updates für Windows Server 2016 jetzt können Sie jedoch zum Implementieren einer Lösung für 1ms Genauigkeit in Ihrer Domäne.  Weitere Informationen finden Sie unter [Windows 2016 genau Zeit](accurate-time.md) und [Unterstützung Grenze so konfigurieren Sie die Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](https://go.microsoft.com/fwlink/?LinkID=179459) Weitere Informationen.  
  
## <a name="w2k3tr_times_tools_dyax"></a>Windows-Zeitdienst: Tools  
Die folgenden Tools sind Windows-Zeitdienst zugeordnet.  
  
#### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows-Zeitdienst  
**Kategorie**  

Dieses Tool wird als Teil des Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 Standard-Installationen installiert.  
  
**Versionskompatibilität**  
  
Dieses Tool kann auf Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 Standard-Installationen.  
  
W32tm.exe wird verwendet, um Windows-Zeitdienst-Dienst zu konfigurieren. Sie können auch zur diagnose von Problemen mit der Zeitdienst verwendet werden. W32tm.exe ist die bevorzugte Befehlszeilentool für Konfiguration, Überwachung und Fehlerbehebung für Windows-Zeitdienst.  
  
Die folgenden Tabellen beschreiben die Parameter, die mit W32tm.exe verwendet werden.  
  
**Primäre W32tm.exe-Parameter**  
  
|Parameter|Beschreibung|  
|-------------|---------------|  
|W32tm /?|Befehlszeilenhilfe w32tm|  
|W32tm//register|Registriert den Zeitdienst für als Dienst ausgeführt werden, und die Registrierung Standardkonfiguration hinzugefügt.|  
|W32tm//unregister|Hebt die Registrierung des Zeitdiensts und entfernt alle Konfigurationsinformationen aus der Registrierung.|  
|W32tm//monitor<br /><br />[/domain:<domain name>] [/computers:<name>[,<name>[,<name>...]]] [/Threads:<num>]|Domäne - gibt an, welche Domäne zu überwachen. Wenn kein Domänenname erhält oder weder die Computer der Domäne angegeben wurde, wird die Standard-Domäne verwendet. Diese Option kann mehrmals verwendet werden.<br /><br />Computer - überwacht die angegebenen Liste von Computern. Computernamen werden durch Kommas, ohne Leerzeichen getrennt. Wenn Sie ein Namen mit dem Präfix ist ein "*", wird er als PDC behandelt. Diese Option kann mehrmals verwendet werden.<br /><br />Threads – gibt die Anzahl der Computer gleichzeitig analysiert. Der Standardwert ist 3. Zulässige Bereich ist 1 bis 50.|  
|W32tm /ntte <NT time epoch>|Konvertieren Sie eine NT-Systemzeit (10 ^-7) s-Intervallen 0 h 1. Januar 1601 in einem lesbaren Format.|  
|W32tm /ntpte <NTP time epoch>|Konvertieren der Systemzeit, in (2 ^-32) s-Intervallen 0 h 1. Jan 1900, in einem lesbaren Format.|  
|w32tm//resync<br /><br />[/computer:<computer>]<br /><br />[/nowait]<br /><br />[/Rediscover]<br /><br />[/Soft]|Erfahren einem Computer, dass sie ihre Uhr so bald wie möglich, synchronisiert auslösen neu.<br /><br />Computer:<computer> -gibt an, der Computer, der neu. Wenn nicht angegeben, wird der lokale Computer erneut synchronisieren.<br /><br />NOWAIT - warten Sie nicht die erneut synchronisieren, auftreten. sofort zurückgegeben. Warten Sie andernfalls die erneut synchronisieren, um vor der Rückgabe abzuschließen.<br /><br />kennenzulernen - ermittelt die Netzwerkkonfiguration und Netzwerkquellen kennenzulernen und anschließend erneut zu synchronisieren.<br /><br />Synchronisieren Sie weiche - mit vorhandenen Fehlerstatistiken. Nicht hilfreich, der für die Kompatibilität.|  
|W32tm /stripchart<br /><br />/computer:<target><br /><br />[/Period:<refresh>]<br /><br />[/dataonly]<br /><br />[/Samples:<count>]<br/><br/>[/rdtsc]<br/>|Zeigt ein Diagramm für den Offset zwischen diesem Computer und einem anderen Computer.<br /><br />Computer:<target> -der Computer der Offset gemessen.<br /><br />Zeitraum:<refresh> – die Zeit zwischen abtastungen, in Sekunden. Der Standardwert ist 2 s.<br /><br />DataOnly - zeigt nur Daten ohne Grafiken.<br /><br />Beispiele:<count> - sammelt <count> Beispiele beenden. Wenn nicht angegeben, werden Beispiele erfasst werden, bis **STRG+C** gedrückt wird.<br/><br/>Rdtsc: für jedes Beispiel druckt durch Trennzeichen getrennte Werte zusammen mit den Headern RdtscStart, RdtscEnd, FileTime, RoundtripDelay, NtpOffset anstelle der Grafik Text.<br/><ul><li>[RdtscStart – RDTSC (Lesen Zeitstempel Zähler)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) Wert gesammelt werden, kurz bevor die NTP-Anforderung generiert wurde.</li><li>RdtscEnd – RDTSC (Lesen Zeitstempel Zähler) Wert gesammelten nur nach die NTP-Antwort empfangen und verarbeitet wurde.</li><li>FileTime – lokale FILETIME Wert, der in der NTP-Anforderung.</li><li>RoundtripDelay – Zeit vergangen in Sekunden zwischen der NTP-Anforderung wird erstellt und Verarbeitung der empfangenen NTP-Antwort gemäß NTP Übersetzungsdateien Berechnungen berechnet.</li><li>NTPOffset – Zeit in Sekunden zwischen dem lokalen Computer und dem NTP-Server offset berechnet gemäß Offset NTP-Berechnungen.</li></ul>|
|W32tm /config<br /><br />[/computer:<target>]<br /><br />[/Update]<br /><br />[/manualpeerlist:<peers>]<br /><br />[/syncfromflags:<source>]<br /><br />[/LocalClockDispersion:<seconds>]<br /><br />[/Reliable: (Ja & #124; Nein)]<br /><br />[/largephaseoffset:<milliseconds>]|Computer:<target> -passt die Konfiguration des <target>. Wenn nicht angegeben, ist der Standardwert der lokale Computer.<br /><br />Update - benachrichtigt den Zeitdienst, die die Konfiguration geändert wurde, verursacht die Änderungen wirksam werden,.<br /><br />Manualpeerlist:<peers> -wird die manuelle Peer-Liste auf <peers>, dies ist eine durch Leerzeichen getrennte Liste der DNS- bzw. IP-Adressen. Wenn Sie mehrere Peers angeben, muss diese Option in Anführungszeichen eingeschlossen werden.<br /><br />Syncfromflags:<source> -legt die Quellen der NTP-Client aus synchronisiert werden sollten. <source> sollte eine durch Kommas getrennte Liste der diese Schlüsselwörter (ohne Beachtung von Groß-/Kleinschreibung):<br /><br />Manuelle - Peers aus der Liste der manuelle Peer enthalten.<br /><br />DOMHIER - von einem Domänencontroller (DC) in der Domänenhierarchie synchronisieren.<br /><br />Abweichung der lokalen Uhrzeit:<seconds> -die Genauigkeit der internen Uhr, die W32Time wird davon ausgegangen wird, wenn es von den konfigurierten Quellen abrufen kann nicht konfiguriert.<br /><br />zuverlässige: ("Ja" & #124; Nein) – festgelegt, ob dieser Computer eine zuverlässige Zeitquelle ist.<br /><br />Diese Einstellung gilt nur für Domänencontroller.<br /><br />Dieser Computer ist Ja – einem zuverlässigen Zeitdienst.<br /><br />NICHT - gehört der Computer nicht über einen zuverlässigen Zeitdienst.<br /><br />großer Phasenoffset:<milliseconds> -legt den Zeitunterschied zwischen lokalen und Netzwerk-Zeit ist, die W32Time eine Spitze berücksichtigt wird.|  
|W32tm /tz|Zeigen Sie die aktuellen Einstellungen für die Zeitzone.|  
|W32tm /dumpreg<br /><br />[/Subkey:<key>]<br /><br />[/computer:<target>]|Zeigt die Werte, die einem Registrierungsschlüssel zugeordnet.<br /><br />Der Standardschlüssel ist HKLM\System\CurrentControlSet\Services\W32Time<br /><br />(der Stammschlüssel für den Zeitdienst).<br /><br />Unterschlüssel:<key> -zeigt die Werte von Unterschlüssel <key> des Standardschlüssels.<br /><br />Computer:<target> -Abfragen registrierungseinstellungen für Computer <target>|  
|W32tm//query [/computer:<target>] {/source & #124; /configuration & #124; /Peers & #124; /status} [/verbose]|Dieser Parameter wurde zuerst in der Windows-Zeitdienst-Clientversionen von Windows Vista und Windows Server 2008 zur Verfügung gestellt.<br /><br />Anzeigen des Computers Windows Time Service-Informationen.<br /><br />**Computer:<target> ** -Fragen Sie den ** <target> **. Wenn nicht angegeben, ist der Standardwert der lokale Computer.<br /><br />**Quelle** -Zeitquellen anzuzeigen.<br /><br />**Konfiguration** -zeigen Sie die Konfiguration der Laufzeit und der Ursprung der Einstellung. In den ausführlichen Modus der nicht definiert oder nicht verwendete Einstellung angezeigt zu.<br /><br />**Peers** – eine Liste von Peers und deren Status angezeigt.<br /><br />**Status** -Dienststatus Anzeigezeit für Windows.<br /><br />**Ausführliche** -die ausführlichen Modus, um weitere Informationen anzuzeigen.|  
|W32tm//debug {/disable & #124; {/Enable /file:<name> /size:<bytes> /entries:<value> [/truncate]}}|Dieser Parameter wurde zuerst in der Windows-Zeitdienst-Clientversionen von Windows Vista und Windows Server 2008 zur Verfügung gestellt.<br /><br />Aktivieren Sie oder deaktivieren Sie den lokalen Computer Windows-Zeitdienst-private Protokoll.<br /><br />**Deaktivieren Sie** -private Protokoll zu deaktivieren.<br /><br />**Aktivieren Sie** -das private Protokoll aktivieren.<br /><br />-   **Datei:<name> ** -den absoluten Dateinamen angeben.<br />-   **Größe:<bytes> ** -Geben Sie die maximale Größe für die zirkuläre Protokollierung.<br />-   **Einträge:<value> ** -enthält eine Liste von Flags, die von der Anzahl und getrennt durch Kommas, die die Typen von Informationen angeben, die protokolliert werden sollen. Gültige Werte sind 0 bis 300. Eine Reihe von Zahlen ist gültig, zusätzlich zu den einzelnen Zahlen wie 0-100,103, 106. Der Wert 0 und 300 ist für die Protokollierung aller Informationen.<br /><br />**Kürzen** -verkürzen Sie die Datei, sofern vorhanden.|  
  
Weitere Informationen zu **W32tm.exe**, finden Sie unter Hilfe- und Supportcenter in Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2.  
  
## <a name="w2k3tr_times_tools_uhlp"></a>Registrierungseinträge Windows-Zeitdienst  
Die folgenden Registrierungseinträge sind Windows-Zeitdienst zugeordnet.  
  
Diese Informationen wird als Referenz bereitgestellt, für die Verwendung in der Problembehandlung oder überprüfen, dass die erforderlichen Einstellungen angewendet werden. Es wird empfohlen, dass Sie nicht direkt die Registrierung bearbeiten, sofern es keine andere Alternative. Änderungen an der Registrierung werden durch den Registrierungs-Editor oder durch Windows nicht überprüft, bevor sie angewendet werden, daher können falsche Werte gespeichert werden. Dies kann nicht behebbaren Fehlern im System führen.  
  
Verwenden Sie nach Möglichkeit Gruppenrichtlinien oder anderen Windows-Tools, z. B. Microsoft Management Console (MMC) zum Ausführen von Aufgaben und nicht als direkte Bearbeitung der Registrierung. Wenn Sie die Registrierung bearbeiten müssen, verwenden Sie äußerst vorsichtig vor.  
  
> [!WARNING]  
> Einige der voreingestellten Werte, die in das System Administrative Vorlage Datei (System.adm) konfiguriert sind, für die gruppenrichtlinieneinstellungen (Object, GPO) die entsprechenden Standard-Registrierungseinträge unterscheiden. Wenn Sie ein GPO verwenden, die keine Windows-Zeitdienst-Einstellung konfigurieren möchten, achten Sie darauf, dass Sie überprüfen, [Voreinstellung Werte für die Windows Time Service-gruppenrichtlinieneinstellungen unterscheiden sich von der entsprechenden Windows-Zeitdienst-Registrierungseinträge in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). Dieses Problem betrifft Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 und Windows Server 2003.  
  
Viele Registrierungseinträge für den Windows-Zeitdienst sind identisch mit der Gruppenrichtlinien-Einstellung mit dem gleichen Namen. Die gruppenrichtlinieneinstellungen entsprechen die Registry-Einträge mit demselben Namen befindet sich unter:  
  
>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**

  
Es gibt mehrere Registrierungsschlüssel an diesem Registrierungsspeicherort ein. Die Windows-Zeitdienst-Einstellungen werden Werte für diese Schlüssel gespeichert:
* [Parameter](#Parameters)
* [Config](#Configuration)
* [NtpClient](#NtpClient)
* [NtpServer](#NtpServer)
  
> [!NOTE]  
> Viele der Werte in der W32Time-Abschnitt der Registrierung werden intern von W32Time verwendet, um Informationen zu speichern. Diese Werte sollten nicht manuell zu einem beliebigen Zeitpunkt geändert werden. Ändern Sie nicht die Einstellungen in diesem Abschnitt, wenn Sie mit der Einstellung vertraut sind und sicher sind, dass der neue Wert wie erwartet funktioniert. Die folgenden Registrierungseinträge befinden sich unter:

>>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**  
  
Einige der Parameter werden in Zeiteinheiten in der Registrierung gespeichert, und einige werden in Sekunden angegeben. So konvertieren die Zeit von Zeiteinheiten in Sekunden:  
  
-   1 Minute = 60 Sekunden  
  
-   1 s = 1000 ms  
  
-   1 ms = 10.000 Takts auf einem Windows-System unter [DateTime.Ticks Eigenschaft](https://msdn.microsoft.com/en-us/library/system.datetime.ticks.aspx).  
  
Beispielsweise werden 5 Minuten 5 * 60\ * 1000\ * 10000 = 3000000000 Takts. 

Alle Versionen enthalten Windows 7, Windows 8, Windows 10, Windows Server 2008 und Windows Server 2008 R2, Windows Server 2012, Windows Server-2012R2, Windows Server 2016.  Einige Einträge sind nur auf neueren Windows-Versionen verfügbar.


#### <a name="Parameters"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters

|Registrierungseintrag|Version|Beschreibung|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Alle|Dieser Eintrag bedeutet, dass bei der Synchronisierung zwischen Peers nicht standardmäßigen Modus Kombinationen zulässig sind. Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.|
|NtpServer|Alle|Dieser Eintrag gibt eine durch Leerzeichen getrennte Liste von Peers, von denen ein Computer die Zeitstempel, erhält, bestehend aus einem oder mehreren DNS-Namen oder IP-Adressen pro Zeile. Jeder DNS-Namen oder die IP-Adresse muss eindeutig sein. Computer mit einer Domäne verbunden sind, müssen mit zuverlässiger Zeitquelle, z. B. die offizielle US Zeit Uhr synchronisieren.  <ul><li>0 x 01 SpecialInterval </li><li>0 x 02 UseAsFallbackOnly</li><li>0 x 04 SymmetricActive - finden Sie weitere Informationen zu diesem Modus [Windows Zeitserver: 3,3 Modi der Vorgang](https://go.microsoft.com/fwlink/?LinkId=208012).</li><li>0 x 08-client</li></ul><br />Es gibt keinen Standardwert für diesen Registrierungseintrag auf Mitglieder der Domäne ein. Der Standardwert für eigenständige Clients und Server ist time.windows.com, 0 x 1.<br /><br />Hinweis: Weitere Informationen zu verfügbaren NTP-Server, finden Sie unter [Microsoft Knowledge Base-Artikel 262680 – eine Liste der Zeitserver das Simple Network Time Protocol (SNTP)-, die im Internet verfügbar sind](https://go.microsoft.com/fwlink/?LinkId=186067)|
|ServiceDll|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden, und alle Änderungen an dieser Einstellung können zu unerwarteten Ergebnissen führen. Der Standardspeicherort für diese DLL-Datei auf Mitglieder der Domäne und eigenständige Clients und Servern ist % windir%\System32\W32Time.dll.  |
|ServiceMain|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden, und alle Änderungen an dieser Einstellung können zu unerwarteten Ergebnissen führen. Der Standardwert auf Mitglieder der Domäne ist SvchostEntry_W32Time. Der Standardwert für eigenständige Clients und Server ist SvchostEntry_W32Time.  "|
|Typ|Alle|Dieser Eintrag gibt an, dass die Synchronisierung von akzeptieren peers:  <ul><li>**NoSync**. Der Zeitdienst wird nicht mit anderen Datenquellen synchronisiert.</li><li>**NTP.** Der Zeitdienst synchronisiert wird von den Servern, die gemäß dem **NtpServer**. der Registrierungseintrag.</li><li>**Nt5DS**. Der Zeitdienst synchronisiert aus der Domäne.  </li><li>**AllSync**. Der Zeitdienst verwendet alle verfügbaren Synchronisierungsmechanismus.  </li></ul>Der Standardwert auf Mitglieder der Domäne ist **NT5DS**. Der Standardwert für eigenständige Clients und Server ist **NTP**.   |

#### <a name="Configuration"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config

|Registrierungseintrag|Version|Beschreibung|
|------------------------------------|---------------|----------------------------|
|AnnounceFlags|Alle|Dieser Eintrag steuert, ob dieser Computer als ein zuverlässiger Zeitserver gekennzeichnet ist. Ein Computer ist nicht als zuverlässig gekennzeichnet, es sei denn, sie auch als einen Server markiert ist.<br /> – 0 x 00 nicht mit einem Zeitserver  <br /> – 0 x 01 immer Zeitserver  <br /> -Automatische Zeitserver 0 x 02  <br /> – 0 x 04 immer zuverlässigen Zeitserver  <br /> – 0 x 08 automatische zuverlässigen Zeitserver  <br />Der Standardwert für Mitglieder der Domäne ist 10. Der Standardwert für eigenständige Clients und Server ist 10.|
|EventLogFlags|Alle|Dieser Eintrag steuert die Ereignisse, die der Zeitdienst protokolliert.  <br />-Zeit Sprung: 0 x 1  <br />-Quelle ändern: 0 x 2  <br />Der Standardwert für Mitglieder der Domäne ist 2. Der Standardwert für eigenständige Clients und Server ist 2.  |
|FrequencyCorrectRate|Alle|Dieser Eintrag steuert die Rate, mit der die Uhr korrigiert wird. Wenn dieser Wert zu klein ist, wird die Uhr nicht stabil und overcorrects. Wenn der Wert zu groß ist, dauert die Uhr lange zu synchronisieren. Der Standardwert für Mitglieder der Domäne ist 4. Der Standardwert für eigenständige Clients und Server beträgt 4.  <br /><br />Beachten Sie, dass 0 einen ungültigen Wert für den Registrierungseintrag FrequencyCorrectRate. Auf Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2-Computer Wenn der Wert auf 0 festgelegt ist ändert der Windows-Zeitdienst automatisch es auf 1.  |
|HoldPeriod|Alle|Dieser Eintrag steuert die Zeitspanne, für die Sammlung Erkennung deaktiviert ist, um die Uhr des lokalen schnell in die Synchronisierung zu versetzen. Eine Sammlung ist, der angibt, Zeit mit dem Beispiel für Zeit ist deaktiviert eine Anzahl von Sekunden und empfangen wird in der Regel nach rechtzeitig Beispiele konsistent zurückgegeben wurden. Der Standardwert für Mitglieder der Domäne ist 5. Der Standardwert für eigenständige Clients und Server ist 5.  |
|Großer Phasenoffset|Alle|Dieser Eintrag gibt an, dass eine Zeit offset größer als oder gleich diesem Wert 10<sup>-7</sup> Sekunden ist eine Sammlung betrachtet. Eine Störung z. B. eine große Menge an Datenverkehr im Netzwerk möglicherweise eine Sammlung. Eine Sammlung wird ignoriert, es sei denn, er für einen längeren Zeitraum beibehalten. Der Standardwert auf Mitglieder der Domäne ist 50000000. Der Standardwert für eigenständige Clients und Server ist 50000000.  |
|LastClockRate|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden, und alle Änderungen an dieser Einstellung können zu unerwarteten Ergebnissen führen. Der Standardwert auf Mitglieder der Domäne ist 156250. Der Standardwert für eigenständige Clients und Server ist 156250.  |
|Abweichung der lokalen Uhrzeit|Alle|Dieser Eintrag steuert die Verbreitung (in Sekunden), die Sie beim davon ausgehen müssen nur Zeitquelle die integrierte CMOS-Uhr wird. Der Standardwert für Mitglieder der Domäne ist 10. Der Standardwert für eigenständige Clients und Server ist 10.|
|Max. zugelassener Phasenoffset|Alle|Dieser Eintrag gibt das maximale Offset (in Sekunden) die W32Time versucht, die Computeruhr anhand der Taktfrequenz anzupassen. Wenn der Offset diese Begrenzung überschreitet, stellt W32Time die Computeruhr direkt ein. Der Standardwert für Mitglieder der Domäne ist 300. Der Standardwert für eigenständige Clients und Server ist 1.  [Weitere Informationen finden Sie unter](#MaxAllowedPhaseOffset).|
|MaxClockRate|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden, und alle Änderungen an dieser Einstellung können zu unerwarteten Ergebnissen führen. Der Standardwert für Mitglieder der Domäne ist 155860. Der Standardwert für eigenständige Clients und Server ist 155860.  |
|MaxNegPhaseCorrection|Alle|Dieser Eintrag gibt die größte negative Zeitkorrektur in Sekunden an, denen der Dienst durchführt. Wenn der Dienst feststellt, dass eine größere Änderung erforderlich ist, protokolliert er stattdessen ein Ereignis. Sonderfall: bei 0xFFFFFFFF ist immer. Der Standardwert für Mitglieder der Domäne ist 0xFFFFFFFF. Der Standardwert für eigenständige Clients und Server ist 54.000 (15 Stunden).  |
|MaxPollInterval|Alle|Dieser Eintrag gibt die größte zulässige für das System Abfrageintervall in Sekunden an log2, an. Beachten Sie, dass ein System gemäß dem festgelegten Intervall die Abfragen, zwar muss ein Anbieter zurückweisen kann zu Beispiele, wenn Sie dazu aufgefordert. Der Standardwert für Domänencontroller ist 10. Der Standardwert für Mitglieder der Domäne ist 15. Der Standardwert für eigenständige Clients und Server ist 15.  |
|MaxPosPhaseCorrection|Alle|Dieser Eintrag gibt die größte positive Zeitkorrektur in Sekunden an, denen der Dienst durchführt. Wenn der Dienst feststellt, dass eine größere Änderung erforderlich ist, protokolliert er stattdessen ein Ereignis. Sonderfall: bei 0xFFFFFFFF ist immer. Der Standardwert für Mitglieder der Domäne ist 0xFFFFFFFF. Der Standardwert für eigenständige Clients und Server ist 54.000 (15 Stunden).  |
|MinClockRate|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden, und alle Änderungen an dieser Einstellung können zu unerwarteten Ergebnissen führen. Der Standardwert für Mitglieder der Domäne ist 155860. Der Standardwert für eigenständige Clients und Server ist 155860.  |
|MinPollInterval|Alle|Dieser Eintrag gibt das kleinste Intervall in Sekunden an log2, für das System Abrufintervall zulässig ist. Beachten Sie, dass während ein Systems Beispiele nicht häufiger als diese anfordern, ein Anbieter Beispiele zu anderen Zeiten als das geplante Intervall erzeugen kann. Der Standardwert für Domänencontroller ist 6. Der Standardwert für Mitglieder der Domäne ist 10. Der Standardwert für eigenständige Clients und Server ist 10.  |
|PhaseCorrectRate|Alle|Dieser Eintrag steuert die Rate, mit der die Phasenfehler behoben ist. Angeben eines niedrigen Werts den Phasenfehler schnell korrigiert, aber möglicherweise dazu führen, dass die Uhr instabil wird. Wenn der Wert zu groß ist, wird eine längere Zeit zum Beheben des Fehlers Phase dauert. <br /><br />Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 7.<br /><br />Hinweis: 0 ist ein ungültiger Wert für den Registrierungseintrag PhaseCorrectRate. Auf Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2-Computer Wenn der Wert auf 0 festgelegt ist wird der Windows-Zeitdienst automatisch in 1.  |
|PollAdjustFactor|Alle|Dieser Eintrag steuert die Entscheidung zum Vergrößern oder verkleinern das Abrufintervall für das System. Je größer der Wert ist, je kleiner die Menge an Fehler, der das Abrufintervall, verringert werden. Der Standardwert für Mitglieder der Domäne ist 5. Der Standardwert für eigenständige Clients und Server ist 5. |
|SpikeWatchPeriod|Alle|Dieser Eintrag gibt die Zeitspanne, die ein verdächtige Offset beibehalten werden muss, bevor sie (in Sekunden) als richtig akzeptiert wird. Der Standardwert für Mitglieder der Domäne ist 900. Der Standardwert für eigenständige Clients und Arbeitsstationen beträgt 900.  |
|TimeJumpAuditOffset|Alle|Eine Ganzzahl ohne Vorzeichen, die angibt, die Zeitschwellenwert Sprunglisten überwachen, in Sekunden. Wenn der Zeitdienst die lokale Uhr passt durch Einstellen der Uhr direkt und die Zeitkorrektur als dieser Wert ist, protokolliert der Zeitdienst ein Überwachungsereignis.|
|UpdateInterval|Alle|Dieser Eintrag gibt die Anzahl der Zeiteinheiten zwischen Phase Korrektur Anpassungen. Der Standardwert für Domänencontroller ist 100. Der Standardwert für Mitglieder der Domäne ist 30.000. Der Standardwert für eigenständige Clients und Server ist 360,000.  <br /><br />**Hinweis:**: 0 (null) ist ein ungültiger Wert für den Registrierungseintrag UpdateInterval. Auf Computern unter Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 und Windows Server 2008 R2 Wenn der Wert auf 0 festgelegt ist wird der Windows-Zeitdienst automatisch in 1.<br /><br />Die folgenden drei Registrierungseinträge sind nicht in der Standardkonfiguration W32Time jedoch an der Registrierung erhalten Sie eine höhere Protokollierungsfunktionen hinzugefügt werden können. Die Informationen in das Systemereignisprotokoll protokolliert kann geändert werden, indem der Wert für die EventLogFlags-Einstellung in der Gruppenrichtlinien-Editors. Standardmäßig erstellt der Zeitdienst ein Protokoll in der Ereignisanzeige, jedes Mal, wenn sich um eine neue Zeitquelle wechselt.<br /><br />**Warnung**: einige der voreingestellten Werte, die in das System Administrative Vorlage Datei (System.adm) konfiguriert sind, für die gruppenrichtlinieneinstellungen (Object, GPO) die entsprechende unterscheiden Standard-Registry-Einträge. Wenn Sie ein GPO verwenden, die keine Windows-Zeitdienst-Einstellung konfigurieren möchten, achten Sie darauf, dass Sie überprüfen, [Voreinstellung Werte für die Windows Time Service-gruppenrichtlinieneinstellungen unterscheiden sich von der entsprechenden Windows-Zeitdienst-Registrierungseinträge in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). Dieses Problem betrifft Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 und Windows Server 2003. |
|UtilizeSslTimeData|Bereitstellen von Windows 10 Build 1511|Eintrag 1 bedeutet, dass der W32Time mehrere SSL-Zeitstempel verwendet wird, um eine Uhr anzulegen, die überaus ungenau ist.|

Die folgenden Registrierungseinträge müssen hinzugefügt werden, um W32Time-Protokollierung zu aktivieren:  

|Registrierungseintrag|Version|Beschreibung|
|------------------------------------|---------------|----------------------------|
|FileLogEntries|Alle|Dieser Eintrag steuert die Dauer der Einträge in der Windows-Zeitdienst-Protokolldatei erstellt. Der Standardwert ist keine, die keine Windows-Zeitdienst-Aktivitäten protokolliert werden. Gültige Werte sind 0 bis 300. Dieser Wert wirkt sich nicht auf der Einträge im Ereignisprotokoll, die normalerweise von Windows-Zeitdienst erstellt|
|FileLogName|Alle|Dieser Eintrag steuert den Speicherort und den Namen des Windows-Zeitdienst-Protokolls. Der Standardwert ist leer, und sollte nicht geändert werden, es sei denn, **FileLogEntries** geändert wird. Ein gültiger Wert ist, einen vollständigen Pfad und Dateinamen, mit dem Windows-Zeitdienst die Protokolldatei erstellt. Dieser Wert wirkt sich nicht auf die Einträge im Ereignisprotokoll, die normalerweise von Windows-Zeitdienst erstellt aus.  |
|FileLogSize|Alle|Dieser Eintrag steuert das Verhalten zirkuläre Protokollierung der Windows-Zeitdienst-Protokolldateien. Wenn **FileLogEntries** und **FileLogName** sind definiert, diesen Eintrag definiert die Größe in Bytes an, die vor dem überschreiben die älteste Protokolleinträge durch neue Einträgen zu erreichen können. Beliebige positive Zahl gültig ist, und 3000000 wird empfohlen. Dieser Wert wirkt sich nicht auf die Einträge im Ereignisprotokoll, die normalerweise von Windows-Zeitdienst erstellt aus.  |



#### <a name="NtpClient"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient

|Registrierungseintrag|Version|Beschreibung|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Alle|Dieser Eintrag bedeutet, dass bei der Synchronisierung zwischen Peers nicht standardmäßigen Modus Kombinationen zulässig sind. Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.|
|CompatibilityFlags|Alle|Dieser Eintrag gibt die folgenden Kompatibilitätsflags und Werte an: <br /><br />-DispersionInvalid: 0 x 00000001  <br />-IgnoreFutureRefTimeStamp: 0 x 00000002  <br /> -AutodetectWin2K: 0 x 80000000  <br />-AutodetectWin2KStage2: 0 x 40000000  <br /><br />Der Standardwert für Mitglieder der Domäne ist 0 x 80000000. Der Standardwert für eigenständige Clients und Server ist 0 x 80000000.  |
|CrossSiteSyncFlags|Alle|Dieser Eintrag legt fest, ob der Dienst Synchronisierungspartner außerhalb der Domäne des Computers auswählt. Die Optionen und Werte sind:  <br /><br />-Keine: 0  <br />-PdcOnly: 1  <br />-Alle: 2  <br /><br />Dieser Wert wird ignoriert, wenn die NT5DS Wert nicht festgelegt ist. Der Standardwert für Mitglieder der Domäne ist 2. Der Standardwert für eigenständige Clients und Server ist 2.  |
|DLL-Name|Alle|Dieser Eintrag gibt den Speicherort der DLL für den Zeitanbieter.  <br /><br />Der Standardspeicherort für diese DLL-Datei auf Mitglieder der Domäne und eigenständige Clients und Servern ist % windir%\System32\W32Time.dll.|
|Aktiviert|Alle|Dieser Eintrag gibt an, ob der NtpClient Anbieter in der aktuellen Zeitdienst aktiviert ist.  <br /><ul><li>Ja, 1</li><li>0 für Nein</li></ul>Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.|
|EventLogFlags|Alle|Dieser Eintrag gibt an, die von der Windows-Zeitdienst protokollierten Ereignisse.<ul><li>0 x 1 Erreichbarkeit Änderungen</li><li>0 x 2 große Stichprobe neigen (Dies gilt für Windows Server2003, Windows Server2003 R2, Windows Server2008 und Windows Server2008 R2 nur)</li></ul>Der Standardwert auf Mitglieder der Domäne ist 0 x 1. Der Standardwert für eigenständige Clients und Server ist 0 x 1.|
|InputProvider|Alle|Dieser Eintrag gibt an, ob der Anbieter NtpClient aktiviert ist.  <ul><li>Ja, 1  </li><li>0 für Nein </li></ul>Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.  |
|LargeSampleSkew|Alle|Dieser Eintrag gibt die Scherung große Beispiel für die Protokollierung in Sekunden an. Um die Einhaltung von Sicherheits- und Exchange Commission (SEC)-Spezifikationen sollte dies auf drei Sekunden festgelegt werden. Ereignisse werden für diese Einstellung werden nur protokolliert, wenn EventLogFlags für große Stichprobe 0 x 2 Zeitversatz explizit konfiguriert ist. Der Standardwert für Mitglieder der Domäne ist 3. Der Standardwert für eigenständige Clients und Server ist 3.  |
|ResolvePeerBackOffMaxTimes|Alle|Dieser Eintrag gibt an, dass die maximale Anzahl von Wiederholungen an, die die Wartezeit beim wiederholt Doppelklicken versucht, einen Peer zum Synchronisieren mit Fehler zu finden. Der Wert 0 (null) bedeutet, dass die Wartezeit für immer mindestens. Der Standardwert für Mitglieder der Domäne ist 7. Der Standardwert für eigenständige Clients und Server ist 7. |
|ResolvePeerBackoffMinutes|Alle|Dieser Eintrag gibt das erste Intervall in Minuten, bevor Sie versuchen, suchen Sie einen Peer zum Synchronisieren mit warten. Der Standardwert für Mitglieder der Domäne ist 15. Der Standardwert für eigenständige Clients und Server ist 15.  |
|SpecialPollInterval|Alle|Dieser Eintrag gibt das spezielle Abfrageintervall in Sekunden für die manuelle Peers. Wenn die Kennzeichen SpecialInterval 0 x 1 aktiviert ist, W32Time verwendet diese Abrufintervall anstelle eines ermitteln, indem das Betriebssystem. Der Standardwert für Domänenmitglieder ist 3.600. Der Standardwert für eigenständige Clients und Server ist 604.800.<br/><br/>Neue ist für Build 1702 SpecialPollInterval die Registrierungswerte MinPollInterval und MaxPollInterval Config enthalten.|
|SpecialPollTimeRemaining|Alle|Dieser Eintrag wird vom W32Time verwaltet. Reservierte Daten enthält, die von der Windows-Betriebssystem verwendet werden. Es gibt die Zeit in Sekunden, bevor W32Time synchronisieren wird nach dem Neustart des Computers. Alle Änderungen an dieser Einstellung können zu unvorhersehbaren Ergebnissen führen. Der Standardwert für beide Mitglieder der Domäne und auf eigenständigen Clients und Servern ist leer.  |

#### <a name="NtpServer"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer

|Registrierungseintrag|Version|Beschreibung|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Alle|Dieser Eintrag bedeutet, dass bei der Synchronisierung zwischen Clients und Servern nicht standardmäßigen Modus Kombinationen zulässig sind. Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.|
|DLL-Name|Alle|Dieser Eintrag gibt den Speicherort der DLL für den Zeitanbieter.<br /><br />Der Standardspeicherort für diese DLL-Datei auf Mitglieder der Domäne und eigenständige Clients und Servern ist % windir%\System32\W32Time.dll.  |
|Aktiviert|Alle|Dieser Eintrag gibt an, ob der NtpServer Anbieter in der aktuellen Zeitdienst aktiviert ist. <ul><li>Ja, 1</li><li>0 für Nein</li></ul>Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.  |
|InputProvider|Alle|Dieser Eintrag gibt an, ob der Anbieter NtpServer aktiviert ist.  <ul><li>Ja, 1  </li><li>0 für Nein </li></ul>Der Standardwert für Mitglieder der Domäne ist 1. Der Standardwert für eigenständige Clients und Server ist 1.  |

#### <a name="MaxAllowedPhaseOffset"></a>Max. zugelassener Phasenoffset Informationen
Damit W32Time die Computeruhr schrittweise festlegen muss der Offset kleiner sein als der Wert für die Max. zugelassener Phasenoffset und erfüllen die folgende Gleichung zur gleichen Zeit:  
```  
|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2  
``` 
Die CurrentTimeOffset wird in Zeiteinheiten, gemessen, in denen 1ms = 10.000 Teilstriche auf einem Windows-System Uhr.  
  
SystemClockRate und PhaseCorrectRate werden auch in Zeiteinheiten gemessen. Um die SystemClockRate zu erhalten, können Sie den folgenden Befehl verwenden und Konvertieren von Sekunden, um anhand der Formel Sekunden Ticks Uhr * 1000\ * 10000:  
  
```  
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  
  
SystemclockRate ist die Rate der Uhr auf dem System. 156000Sekunden als Beispiel verwenden, die SystemclockRate würde werden = 0.0156000 * 1000 \ * 10000 = 156000 Takts.  
  
Max. zugelassener Phasenoffset ist auch in Sekunden. Multiplizieren Sie zum konvertieren, um die Uhr Ticks Max. zugelassener Phasenoffset * 1000\ * 10000.  
  
Die folgenden beiden Beispiele veranschaulichen die anwenden  
  
**Beispiel 1**: Zeit unterscheidet sich von 4Minuten (z.B. Ihre Zeit ist 11:05 Uhr und im Beispiel Zeit von einem Peer empfangen und 09 11 Uhr ist vermutlich eine korrekt zu sein).  
```
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
|currentTimeOffset| = 4mins = 4*60\*1000\*10000 = 2400000000 ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
2400000000 < 6000000000 = TRUE  
```
UND erfüllt die oben genannten Gleichung? 
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 2,400,000,000 / (30000*1) < 156000/2  
  
Is 100,000 < 78,000  
  
NO/FALSE  
```  
Aus diesem Grund würde W32tm die Uhr sofort zurückgesetzt.  
  
> [!NOTE]  
> Wenn Sie die Uhr wieder langsam festlegen möchten, müssen Sie in diesem Fall würde passen Sie die Werte der PhaseCorrectRate oder UpdateInterval in der Registrierung als auch, um sicherzustellen, dass die Ergebnisse der Gleichung in "true" fest.  
  
**Beispiel 2**: Zeit unterscheidet sich in drei Minuten.  
```  
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
currentTimeOffset = 3mins = 3*60\*1000\*10000 = 1800000000 clock ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
1800000000 < 6000000000 = TRUE  
```  
UND erfüllt die oben genannten Gleichung?
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 3 mins (1,800,000,000) / (30000*1) < 156000/2  
  
Is 60,000 < 78,000  
  
YES/TRUE  
```  
In diesem Fall wird die Uhr wieder langsam festgelegt werden.  
  
## <a name="w2k3tr_times_tools_vwtt"></a>Windows Time Service mithilfe von Gruppenrichtlinieneinstellungen  
Sie können die meisten W32Time-Parameter konfigurieren, mithilfe der Gruppenrichtlinien-Editor. Dies beinhaltet das Konfigurieren eines Computers für ein NTPServer oder NTPClient, konfigurieren die Zeit Synchronisierungsmechanismus und Konfigurieren eines Computers, um eine zuverlässige Zeitquelle sein.  
  
> [!NOTE]  
> Gruppenrichtlinieneinstellungen für Windows-Zeitdienst auf Windows Server2003, Windows Server2003 R2, Windows Server2008 und Windows Server2008 R2-Domänencontrollern konfiguriert werden können und können nur auf Computern unter Windows Server2003, Windows Server2003 R2, Windows Server2008 und Windows Server2008 R2 angewendet werden.  
  
Sie finden die Gruppenrichtlinie Einstellungen zur Konfiguration von W32Time in das Gruppenrichtlinienobjekt-Editor-Snap-In in den folgenden Speicherorten verwendet:  
  
-   Computer Configuration\Administrative Templates\System\Windows Zeitdienst  
  
    Konfigurieren Sie **globale Konfigurationseinstellungen** hier.  
  
-   Computer Configuration\Administrative Templates\System\Windows Zeit Service\Time Anbieter  
  
    Konfigurieren Sie **Windows NTP-Client** hier Einstellungen.  
  
    Aktivieren Sie **Windows NTP-Client** hier.  
  
    Aktivieren Sie **Windows NTP-Server** hier.  
  
> [!WARNING]  
> Einige der voreingestellten Werte, die in das System Administrative Vorlage Datei (System.adm) konfiguriert sind, für die gruppenrichtlinieneinstellungen (Object, GPO) die entsprechenden Standard-Registrierungseinträge unterscheiden. Wenn Sie ein GPO verwenden, die keine Windows-Zeitdienst-Einstellung konfigurieren möchten, achten Sie darauf, dass Sie überprüfen, [Voreinstellung Werte für die Windows Time Service-gruppenrichtlinieneinstellungen unterscheiden sich von der entsprechenden Windows-Zeitdienst-Registrierungseinträge in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). Dieses Problem betrifft Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 und Windows Server 2003.  
  
Die folgende Tabelle enthält die globalen Gruppenrichtlinieneinstellungen, die Windows-Zeitdienst und jede Einstellung zugeordnete vorab festgelegten Wert zugeordnet sind. Weitere Informationen zu den einzelnen Einstellungen finden Sie unter der entsprechenden Registrierungseinträge in "[Registrierungseinträge Windows-Zeitdienst](#w2k3tr_times_tools_uhlp)" weiter oben in diesem Thema. Die folgenden Einstellungen befinden sich in einem Gruppenrichtlinienobjekt namens **globale Konfigurationseinstellungen**.  
  
**Globale Gruppe in der Richtlinieneinstellungen im Zusammenhang mit Windows-Zeitdienst**  
  
|Gruppenrichtlinieneinstellung|Vorab festgelegten Wert|  
|------------------------|------------------|  
|AnnounceFlags|10|  
|EventLogFlags|2|  
|FrequencyCorrectRate|4|  
|HoldPeriod|5|  
|Großer Phasenoffset|1280000|  
|Abweichung der lokalen Uhrzeit|10|  
|Max. zugelassener Phasenoffset|300|  
|MaxNegPhaseCorrection|54.000 (15 Stunden)|  
|MaxPollInterval|15|  
|MaxPosPhaseCorrection|54.000 (15 Stunden)|  
|MinPollInterval|10|  
|PhaseCorrectRate|7|  
|PollAdjustFactor|5|  
|SpikeWatchPeriod|90|  
|UpdateInterval|100|  
  
Die folgende Tabelle listet die verfügbaren Einstellungen für die **Windows NTP-Client konfigurieren** Gruppenrichtlinienobjekt und die voreingestellten Werte, die Windows-Zeitdienst zugeordnet sind. Weitere Informationen zu den einzelnen Einstellungen finden Sie unter der entsprechenden Registrierungseinträge in "[Registrierungseinträge Windows-Zeitdienst](#w2k3tr_times_tools_uhlp)" weiter oben in diesem Thema.  
  
**NTP-Client mithilfe von Gruppenrichtlinieneinstellungen zugeordnete Windows-Zeitdienst**  
  
|Gruppenrichtlinieneinstellung|Standardwert|  
|------------------------|-----------------|  
|NtpServer|time.windows.com, 0 x 1|  
|Typ|Standardoptionen:<br /><br />-   **NTP.** Verwenden Sie auf Computern, die nicht mit einer Domäne verbunden sind.<br />-   **NT5DS.** Verwenden Sie auf Computern, die einer Domäne angehören.|  
|CrossSiteSyncFlags|2|  
|ResolvePeerBackoffMinutes|15|  
|ResolvePeerBackoffMaxTimes|7|  
|SpecialPollInterval|3600|  
|EventLogFlags|0|  
  
## <a name="w2k3tr_times_tools_suxb"></a>Netzwerk-Ports, die von der Windows-Zeitdienst verwendet  
Windows-Zeitdienst folgt die NTP-Spezifikation die Verwendung von UDP-Port 123 für die gesamte Zeit Synchronisierung Kommunikation erfordert. Dieser Port wird von Windows-Zeitdienst reserviert und bleibt reserviert. Wenn der Computer die Uhr synchronisiert oder Zeit auf einen anderen Computer enthält, wird diese Kommunikation UDP-Port 123 ausgeführt.  
  
> [!NOTE]  
> Wenn Sie einen Computer mit mehreren Netzwerkadaptern (auch als einen mehrfach vernetzten Computer bezeichnet) verfügen, können Sie Windows-Zeitdienst basierend auf den Netzwerkadapter nicht selektiv aktivieren.  
  
## <a name="w2k3tr_times_tools_qoep"></a>Verwandte Informationen  
Die folgenden Ressourcen enthalten weitere relevante Informationen in diesem Abschnittbeschrieben.  
  
-   RFC *1305* in der IETF RFC-Datenbank  

