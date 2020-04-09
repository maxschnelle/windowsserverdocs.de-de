---
title: Erste Schritte mit der Ereignissammlung für Setup und Start
description: Einrichten der Sammler und Ziele für die Ereignissammlung für Setup und Start
ms.prod: windows-server
manager: DonGill
ms.technology: server-sbec
ms.localizationpriority: medium
ms.date: 10/16/2017
ms.topic: get-started-article
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247b3f8
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: 1160a5dcf2f647a335a22eba54501589db6695ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852073"
---
# <a name="get-started-with-setup-and-boot-event-collection"></a>Erste Schritte mit der Ereignissammlung für Setup und Start

>Gilt für: Windows Server

  
## <a name="overview"></a>Übersicht  
Die Setup-und Start Ereignis Sammlung ist ein neues Feature in Windows Server 2016, mit dem Sie einen Collector-Computer festlegen können, der eine Vielzahl wichtiger Ereignisse sammelt, die auf anderen Computern beim Starten oder durchlaufen des Setup Vorgangs auftreten. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren.  
  
Diese Ereignisse konnten bisher nicht überwacht werden, da die erforderliche Infrastruktur, um diese zu sammeln, nicht vorhanden war, bis ein Computer eingerichtet wurde. Die Arten von Ereignissammlung für Setup und Start umfassen:  
  
-   Laden von Kernel-Modulen und Treibern  
  
-   Enumeration von Geräten und Initialisierung Ihrer Treiber (einschließlich Geräte wie z. b. CPU-Typ)  
  
-   Überprüfung und Bereitstellung von Dateisystemen  
  
-   Starten der ausführbaren Dateien  
  
-   Starten und Fertigstellen von System-Updates  
  
-   Die Punkte, wenn das System für die Anmeldung verfügbar wird, eine Verbindung mit einem Domänencontroller herstellt, der Abschluss der Dienstbeginne und die Verfügbarkeit der Netzwerkfreigaben  
  
Der Sammelcomputer muss Windows Server 2016 ausführen (es kann ein Server mit Desktop Experience oder Server Core-Modus sein). Der Computer muss Windows 10 oder Windows Server 2016 ausführen. Sie können auch diesen Dienst auf einem virtuellen Computer ausführen, der auf einem Computer gehostet wird und **nicht** Windows Server 2016 ausführt. Die folgenden Kombinationen von virtualisierten Sammel- und Zielcomputern funktionieren:  
  
|Virtualisierungshost|Virtuelle Sammelcomputer|Virtuelle Zielcomputer|  
|-----------------------|-----------------------------|--------------------------|  
|Windows 8.1|Ja|Ja|  
|Windows 10|Ja|Ja|  
|Windows Server 2016|Ja|Ja|  
|Windows Server 2012 R2|Ja|no|  
  
## <a name="installing-the-collector-service"></a>Installieren des Sammeldiensts  
Ab Windows Server 2016 ist der Ereignissammlungsdienst eine optionale Funktion. In dieser Version können Sie ihn mit DISM.exe mit diesem Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten installieren:  
  
`dism /online /enable-feature /featurename:SetupAndBootEventCollection`  
  
Dieser Befehl erstellt einen Dienst namens BootEventCollector und eine leere Konfigurationsdatei wird gestartet.  
  
Vergewissern Sie sich durch `get-service -displayname *boot*`, dass die Installation erfolgreich war. Der Boot Event Collector sollte ausgeführt werden. Er wird unter dem Netzwerkdienstkonto ausgeführt und erstellt eine leere Konfigurationsdatei (Active.xml) unter **%SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config**.  
  
Sie können auch den Ereignissammlungsdienst für Setup und Start mit dem Assistenten "Rollen und Funktionen hinzufügen" im Server-Manager installieren.  
  
## <a name="configuration"></a>Konfiguration  
Sie müssen zwei Elemente zum Erfassen von Setup- und Start-Ereignissen konfigurieren.  
  
-   Auf den Zielcomputern, die die Ereignisse senden (d. h. der Computer, dessen Setup und Start Sie überwachen möchten), aktivieren Sie das Transportprotokoll KDNET/EVENT-NET und aktivieren Sie die Weiterleitung von Ereignissen.  
  
-   Geben Sie auf dem Sammelcomputer an, von welchen Computern Ereignisse erfasst werden sollen und wo Sie gespeichert werden.  
  
> [!NOTE]  
> Sie können keinen Computer konfigurieren, um Startereignisse an sich selbst zu senden. Wenn Sie zwei Computern überwachen möchten, können Sie diese so konfigurieren, dass sie die Ereignisse zu einander senden.  
  
### <a name="configuring-a-target-computer"></a>Konfigurieren des Zielcomputers  
Aktivieren Sie auf jedem Zielcomputer zunächst den KDNET/EVENT-NET-Transport und klicken Sie dann auf Aktivieren des Sendens von ETW-Ereignissen über das Transportprotokoll und starten Sie den Zielcomputer neu. EVENT-NET ist ein Transportprotokoll im Kernelmodus ähnlich wie KDNET (Kernel-Debugger-Protokoll). EVENT-NET überträgt nur Ereignisse und nicht den Debuggerzugriff. Diese beiden Protokolle schließen sich gegenseitig aus; Sie können nur eine der Adressen zu einem Zeitpunkt aktivieren.  
  
Sie können den Ereignistransport (mit Windows PowerShell) remote oder lokal aktivieren.  
  
##### <a name="to-enable-event-transport-remotely"></a>So aktivieren Sie den Ereignistransport remote  
  
1.  Wenn Sie bereits Windows PowerShell-Remoting auf dem Zielcomputer festgelegt haben, fahren Sie mit Schritt 3 fort. Wenn dies nicht der Fall ist, öffnen Sie auf dem Zielcomputer ein Eingabeaufforderungsfenster, und führen Sie folgenden Befehl aus:  
  
    winrm quickconfig  
  
2.  Folgen Sie den Aufforderungen, und starten Sie den Zielcomputer neu. Wenn der Zielcomputer nicht in derselben Domäne wie der Sammelcomputer ist, müssen Sie ihn als vertrauenswürdigen Host definieren. Dazu gehen Sie folgendermaßen vor:  
  
3.  Führen Sie auf dem Sammelcomputer einen der folgenden Befehle aus:  
  
    -   An einer Windows PowerShell-Eingabeaufforderung: `Set-Item -Force WSMan:\localhost\Client\TrustedHosts <target1>,<target2>,...`, gefolgt von `Set-Item -Force WSMan:\localhost\Client\AllowUnencrypted true`, wo \<target1 > usw. die Namen oder IP-Adressen der Zielcomputer sind.  
  
    -   Oder an einer Eingabeaufforderung: **WinRM Set WinRM/config/Client @ {Treuhänder dhosts =\<target1 >,\<TARGET2 >,...; "Zuweisung" = true}**  
  
        > [!IMPORTANT]  
        > Dies richtet eine unverschlüsselte Kommunikation ein, führen Sie dies also nicht außerhalb einer Lab-Umgebung durch.  
  
4.  Testen Sie die Verbindung auf dem Sammelcomputer mit einem der folgenden Windows PowerShell-Befehle:  
  
    Wenn sich der Zielcomputer in derselben Domäne wie der Collector-Computer befindet, führen Sie `New-PSSession -Computer <target> | Remove-PSSession`  
  
    Wenn der Zielcomputer nicht in derselben Domäne ist, führen Sie `New-PSSession -Computer  <target>  -Credential Administrator | Remove-PSSession` aus, was die Anmeldeinformationen aufruft.  
  
    Wenn der Befehl keine Suchzeichenfolge zurückgibt, war Remoting erfolgreich.  
  
5.  Öffnen Sie auf dem Zielcomputer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, und führen Sie diesen Befehl aus:  
  
    `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d>`  
  
    Hier < target_name > der Name des Ziel Computers ist \<IP-> die IP-Adresse des Collector-Computers. \<Port > ist die Portnummer, an der der Collector ausgeführt wird. Der Schlüssel <a.b.c.d> ist ein erforderlicher Verschlüsselungsschlüssel für die Kommunikation mit vier alphanumerischen Zeichenfolgen, die durch Punkte getrennt sind. Dieser Schlüssel wird auf dem Sammelcomputer verwendet. Wenn Sie einen Schlüssel eingeben, wird ein zufälliger Schlüssel generiert; Sie benötigen diesen für den Sammelcomputer, notieren Sie diese.  
  
6.  Wenn Sie bereits einen Sammelcomputer eingerichtet haben, aktualisieren Sie die Konfigurationsdatei auf dem Sammelcomputer mit den Informationen für den neuen Zielcomputer. Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers.  
  
##### <a name="to-enable-event-transport-locally-on-the-target-computer"></a>So aktivieren Sie den Ereignistransport lokal auf dem Zielcomputer  
  
1.  Starten Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie diese Befehle aus:  
  
    **bcdedit/Event ja**  
  
    **bcdedit/eventsettings net HostIP: 1.2.3.4 Port: 50000 Key: a. b. c. d**  
  
    Hier ist 1.2.3.4 ein Beispiel: Ersetzen Sie dies durch die IP-Adresse des Collector-Computers. Ersetzen Sie 50000 auch durch die Portnummer, in der der Collector ausgeführt wird, und a. b. c. d mit dem erforderlichen Verschlüsselungsschlüssel für die Kommunikation. Dieser Schlüssel wird auf dem Sammelcomputer verwendet. Wenn Sie einen Schlüssel eingeben, wird ein zufälliger Schlüssel generiert; Sie benötigen diesen für den Sammelcomputer, notieren Sie diese.  
  
2.  Wenn Sie bereits einen Sammelcomputer eingerichtet haben, aktualisieren Sie die Konfigurationsdatei auf dem Sammelcomputer mit den Informationen für den neuen Zielcomputer. Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers.  
  
**Nachdem der Ereignis Transport selbst aktiviert ist, müssen Sie das System aktivieren, um etw-Ereignisse über diesen Transport tatsächlich zu senden.**  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-remotely"></a>So aktivieren Sie das Sendens von ETW-Ereignissen durch den Transport Remote  
  
1.  Öffnen Sie auf dem Sammelcomputer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.  
  
2.  Führen Sie `Enable-SbecAutologger -ComputerName <target_name>` aus, wobei <target_name> der Name des Zielcomputers ist.  
  
Wenn Sie Windows PowerShell-Remoting nicht einrichten können, können Sie Ereignisse direkt an den Zielcomputer senden.  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-locally"></a>So aktivieren Sie das Sendens von ETW-Ereignissen durch den Transport lokal  
  
1.  Starten Sie auf dem Zielcomputer Regedit.exe, und suchen Sie nach dem Registrierungsschlüssel:  
  
    **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\AutoLogger**. Verschiedene Protokoll-Sitzungen werden als Unterschlüssel unter diesem Schlüssel aufgelistet. **Setup-Plattform**, **NT Kernel-Protokollierung**und **Einrichten von Microsoft Windows** sind Auswahlmöglichkeiten für die Verwendung der Setup und Start-Ereignissammlung, die empfohlene Option ist **EventLog-System**. Diese Schlüssel werden in [Configuring and Starting an AutoLogger Session](https://msdn.microsoft.com/library/windows/desktop/aa363687(v=vs.85).aspx) beschrieben.  
  
2.  Im Schlüssel EventLog-System ändern Sie den Wert der **LogFileMode** von **0x10000180** auf **0x10080180**. Weitere Informationen zu den Details dieser Einstellungen finden Sie unter [Logging Mode Constants](https://msdn.microsoft.com/library/windows/desktop/aa364080(v=vs.85).aspx).  
  
3.  Optional können Sie auch das Senden von Fehlerüberprüfungsdaten an den Sammelcomputer aktivieren. Suchen Sie nach dem Registrierungsschlüssel HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager, und erstellen Sie den Schlüssel **Debug Print Filter** mit dem Wert **0x1**.  
  
4.  Starten Sie den Zielcomputer neu.  
  
### <a name="choosing-the-network-adapter"></a>Auswählen des Netzwerkadapters  
Wenn auf dem Zielcomputer mehr als ein Netzwerkadapter vorhanden ist, wählt der Treiber KDNET den ersten unterstützten aus der Liste aus. Sie können einen speziellen Netzwerkadapter zum Weiterleiten des Setups von Ereignissen mit folgenden Schritten angeben:  
  
##### <a name="to-specify-a-network-adapter"></a>Angabe des Netzwerkadapters  
  
1.  Öffnen Sie auf dem Zielcomputer den Geräte-Manager, erweitern Sie **Netzwerkadapter**, suchen Sie nach dem Netzwerkadapter, den Sie verwenden möchten und klicken Sie mit der rechten Maustaste darauf.  
  
2.  Klicken Sie im Menü, das geöffnet wird auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Details**, erweitern Sie im Menü das Feld **Eigenschaft** und scrollen Sie zu **Standortinformationen** (die Liste ist wahrscheinlich nicht in alphabetischer Reihenfolge), und klicken Sie dann auf. Der Wert ist eine Zeichenfolge des Formulars **PCI-Bus X, Y, Funktion Z Gerät**sein. Notieren Sie sich X.Y.Z; Dies sind die Bus-Parameter, die Sie für den folgenden Befehl benötigen.  
  
3.  Führen Sie einen der folgenden Befehle aus:  
  
    An einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten: `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d> -BusParams <X.Y.Z>`  
  
    Von einer Eingabeaufforderung mit erhöhten Rechten: **bcdedit /eventsettings net hostip:aaa port:50000 key:bbb busparams:X.Y.Z**  
  
### <a name="validate-target-computer-configuration"></a>Überprüfen der Konfiguration des Zielcomputers  
Zum Überprüfen der Einstellungen auf dem Zielcomputer: Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie **bcdedit /enum** aus. Wenn dieser Schritt abgeschlossen ist, führen Sie **bcdedit /eventsettings** aus. Überprüfen Sie die folgenden Werte:  
  
-   Key  
  
-   Debugtyp = NET  
  
-   HostIP = \<IP-Adresse des Sammlers >  
  
-   Port = \<Portnummer, die Sie für den zu verwendenden Collector angegeben haben >  
  
-   DHCP = Ja  
  
Überprüfen Sie auch, dass **bcdedit /event** aktiviert ist, da **/debug** und **/event** sich gegenseitig ausschließen. Sie können nur eine oder die andere ausführen. Sie können auch nicht /eventsettings mit /debug oder /dbgsettings mit /event verwenden.  
  
Beachten Sie außerdem, dass die Ereignissammlung nicht funktioniert, wenn Sie sie auf einem seriellen Anschluss festlegen.  
  
### <a name="configuring-the-collector-computer"></a>Konfigurieren des Sammelcomputers  
Der Sammlungsdienst empfängt die Ereignisse und speichert sie in ETL-Dateien. Diese ETL-Dateien können dann von anderen Tools, wie beispielsweise der Ereignisanzeige, Nachrichtenanalyse, Wevtutil und Windows PowerShell-Cmdlets gelesen werden.  
  
Da Sie im ETW-Format den Namen des Zielcomputers nicht angeben können, müssen die Ereignisse für jeden Zielcomputer als separate Datei gespeichert werden. Die Anzeigetools zeigen möglicherweise einen Computernamen an, aber es ist der Name des Computers, auf dem das Tool ausgeführt wird.  
  
Genauer gesagt, wird jeder Zielcomputer einem Ring von ETL-Dateien zugewiesen. Jeder Dateiname enthält einen Index von 000 bis zu einem Höchstwert, den Sie konfigurieren können (bis zu 999). Wenn die Datei die konfigurierte maximale Größe erreicht, werden Ereignisse in die nächste Datei geschrieben. Nach der höchsten möglichen Datei wird der Dateiindex erneut auf 000 zurückgesetzt. Auf diese Weise werden die Dateien automatisch wiederverwendet, was weniger Speicherplatz erfordert. Sie können auch zusätzliche externe Aufbewahrungsrichtlinien für die Datenträgerverwendung festgelegt. Beispielsweise können Sie Dateien, die älter als eine festgelegte Anzahl von Tagen haben, löschen.  
  
Gesammelte ETL-Dateien werden in der Regel im Verzeichnis **c:\ProgramData\Microsoft\BootEventCollector\Etl** gespeichert (dies hat möglicherweise zusätzliche Unterverzeichnisse). Finden Sie die aktuelle Protokolldatei, indem Sie diese dem Zeitpunkt der letzten Änderung sortieren. Es gibt auch ein Statusprotokoll (normalerweise unter **c:\ProgramData\Microsoft\BootEventCollector\Logs**), das aufzeichnet, wenn der Sammelcomputer in eine neue Datei schreibt.  
  
Es gibt auch ein Sammelprotokoll, das Informationen über den Sammelcomputer selbst aufzeichnet. Sie können dieses Protokoll im ETW-Format speichern (in dem Windows-Protokollierungsdienstereignisse berichtet werden; dies ist die Standardeinstellung) oder in einer Datei (normalerweise unter **c:\ProgramData\Microsoft\BootEventCollector\Logs**). Eine Datei ist möglicherweise nützlich, wenn Sie ausführliche Modi aktivieren, die eine große Datenmenge erzeugen. Sie können auch das Protokoll so festlegen, dass es in eine Standardausgabe durch Ausführen des Sammelcomputers über die Befehlszeile schreibt.  
  
**Erstellen der sammlerkonfigurationsdatei**  
  
Wenn Sie den Dienst aktivieren, werden drei XML-Konfigurationsdateien erstellt und in " **c:\programdata\microsoft\booteventcollector\config**" gespeichert:  
  
-   **Active.XML** diese Datei enthält die derzeit aktive Konfiguration des Sammeldiensts.  Nach der Installation hat diese Datei den gleichen Inhalt wie Empty.xml. Wenn Sie eine neue Konfiguration für die Sammlung festlegen, speichern Sie diese in dieser Datei.  
  
-   **Empty.XML** diese Datei enthält die Mindestkonfigurationselemente, die ihre Standardwerte erfordern. Eine Sammlung ist nicht möglich; es kann nur den Sammlungsdienst im Leerlaufmodus starten.  
  
-   **Example.XML** diese Datei enthält Beispiele und Erklärungen möglicher Konfigurationselemente.  
  
**Auswählen einer Dateigrößen Beschränkung**  
  
Eine Entscheidungen ist das Festlegen der Größe der Datei. Die beste maximale Dateigröße hängt von der erwarteten Menge der Ereignisse und dem verfügbaren Speicherplatz ab. Kleinere Dateien sind zum Löschen der alten Daten besser geeignet. Allerdings enthält jede Datei den Aufwand für einen Header mit 64 KB, und das Lesen vieler Dateien, um den kombinierten Verlauf zu erhalten, kann unpraktisch sein. Die absolute Mindestgröße für die Dateigröße beträgt 256 KB. Angemessene praktische Begrenzung für die Dateigröße sollte über 1 MB und 10 MB ist wahrscheinlich einen guten normalen Wert. Eine höhere Grenze ist möglicherweise sinnvoll, wenn Sie viele Ereignisse erwarten.  
  
Hier sind einige wichtige Punkte bezüglich der Konfigurationsdatei:  
  
-   Die Zielcomputeradresse. Sie können seine IPv4-Adresse, MAC-Adresse oder SMBIOS-GUID verwenden. Berücksichtigen Sie diese Faktoren bei der Auswahl der zu verwendenden Adresse:  
  
    -   Die IPv4-Adresse funktioniert am besten mit statischen Zuweisungen von IP-Adressen. Allerdings müssen auch statische IP-Adressen über DHCP verfügbar sein.  
  
    -   Eine MAC-Adresse oder SMBIOS-GUID ist komfortable, wenn sie im Voraus bekannt sind, aber die IP-Adressen dynamisch zugewiesen werden.  
  
    -   IPv6-Adressen werden vom EVENT-NET-Protokoll nicht unterstützt.  
  
    -   Es ist möglich, mehrere Arten zum Identifizieren des Computers anzugeben. Wenn z. B. die physische Hardware ersetzt werden soll, können Sie die alte und neue MAC-Adresse eingeben und beide werden akzeptiert.  
  
-   Der Schlüssel für die Kommunikation mit dem Sammelcomputer  
  
-   Name des Zielcomputers. Sie können IP-Adresse, Hostname oder einen beliebigen anderen Namen als Name für den Computer verwenden.  
  
-   Der Name der verwendeten ETL-Datei und die Konfiguration der Ringgröße  
  
##### <a name="to-create-the-configuration-file"></a>So erstellen Sie die Konfigurationsdatei  
  
1.  Öffnen Sie eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, und wechseln Sie zu % SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config.  
  
2.  Geben Sie `notepad .\newconfig.xml` ein und drücken Sie die EINGABETASTE.  
  
3.  Kopieren Sie diese Konfiguration in das Editor-Fenster:  
  
    ```  
    <collector configVersionMajor=1 statuslog=c:\ProgramData\Microsoft\BootEventCollector\Logs\statuslog.xml>  
      <common>  
        <collectorport value=50000/>  
        <forwarder type=etl>  
          <set name=file value=c:\ProgramData\Microsoft\BootEventCollector\Etl\{computer}\{computer}_{#3}.etl/>  
          <set name=size value=10mb/>  
          <set name=nfiles value=10/>  
          <set name=toxml value=none/>  
        </forwarder>  
        <target>  
          <ipv4 value=192.168.1.1/>  
          <key value=a.b.c.d/>  
          <computer value=computer1/>  
        </target>  
        <target>  
          <ipv4 value=192.168.1.2/>  
          <key value=d1.e2.f3.g4/>  
          <computer value=computer2/>  
        </target>  
      </common>  
    </collector>  
    ```  
  
    > [!NOTE]  
    > Der Stamm Knoten ist \<Collector >. Dessen Attribute geben die Version der Syntax für die Konfiguration und den Namen der Statusprotokolldatei an.  
    >   
    > Das \<common >-Element gruppiert mehrere Ziele und gibt dabei die allgemeinen Konfigurationselemente an. ähnlich wie eine Benutzergruppe kann verwendet werden, um die allgemeinen Berechtigungen für mehrere Benutzer anzugeben.  
    >   
    > Das \<collectorport-> Element definiert die UDP-Portnummer, an der der Collector auf eingehende Daten lauscht. Dies ist der Port, der im Zielkonfigurationsschritt für Bcdedit angegeben wurde. Die Sammlung unterstützt nur einen Port, und alle Ziele müssen zu demselben Port eine Verbindung herstellen.  
    >   
    > Das \<Weiterleitungs >-Element gibt an, wie ETW-Ereignisse, die von den Ziel Computern empfangen werden, weitergeleitet werden. Es gibt nur eine Weiterleitungsart, die in ETL-Dateien schreibt. Die Parameter geben das Dateinamensmuster, die maximale Größe für jede Datei im Ring und die Größe des Rings für jeden Computer an. Die Einstellung "dexml" gibt an, dass die ETW-Ereignisse in der Binär Form geschrieben werden, während Sie empfangen wurden, ohne in XML zu konvertieren. Weitere Informationen zur Entscheidung, ob die Ereignisse XML-Daten in XML konvertiert werden sollen, finden Sie im Abschnitt XML-Ereignis Konvertierung. Das Dateinamenmuster enthält diese Platzhalter: {Computer} für den Namen des Computers und {#3} für den Index der Datei im Ring.  
    >   
    > In dieser Beispieldatei werden zwei Zielcomputer mit dem \<Target >-Element definiert. Jede Definition gibt die IP-Adresse mit \<IPv4-> an, Sie können jedoch auch die Mac-Adresse (z. b. `<mac value=11:22:33:44:55:66/>` oder `<mac value=11-22-33-44-55-66/>`) oder die SMBIOS-GUID (z. b. `<guid value={269076F9-4B77-46E1-B03B-CA5003775B88}/>`) verwenden, um den Zielcomputer zu identifizieren. Beachten Sie außerdem den Verschlüsselungsschlüssel (identisch mit Bcdedit auf dem Zielcomputer) und den Namen des Computers.  
  
4.  Geben Sie die Details für jeden Bereitstellungs Zielcomputer als separates \<Ziel > Element in der Konfigurationsdatei ein, und speichern Sie dann newconfig. XML, und schließen Sie den Editor.  
  
5.  Wenden Sie die neue Konfiguration mit `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result` an. Die Ausgabe sollte mit dem Erfolgs Feld true zurückgegeben werden. Wenn Sie ein anderes Ergebnis erzielen, lesen Sie den Abschnitt Problembehandlung in diesem Thema.  
  
Sie können die derzeit aktive Konfiguration mit `(Get-SbecActiveConfig).text` überprüfen.  
  
Sie können eine Überprüfung der Gültigkeit für die Konfigurationsdatei mit `$result = (Get-Content .\newconfig.xml | Check-SbecConfig); $result` ausführen.  
  
Obwohl Windows PowerShell-Befehl, um eine neue Konfiguration automatisch angewendet werden soll die Dienstupdates Festnetztelefon, sodass Sie ihn neu starten, können Sie immer den Dienst selbst mit einem der folgenden Befehle neu starten:  
  
-   Mit Windows PowerShell: `Restart-Service BootEventCollector`  
  
-   In einer normalen Eingabeaufforderung: **sc BootEventCollector beenden; sc BootEventCollector starten**  
  
## <a name="configuring-nano-server-as-a-target-computer"></a>Konfigurieren von Nano Servern als Zielcomputer  
Die minimale Schnittstelle von Nano Server kann manchmal Problemen schwer erkennen. Sie können Nano Server automatisch für Ereignissammlung für Setup und Start konfigurieren, und Diagnosedaten an einen Sammelcomputer ohne weitere Benutzereingriffe von Ihnen senden. Gehen Sie hierzu folgendermaßen vor:  
  
#### <a name="to-configure-nano-server-as-a-target-computer"></a>So konfigurieren Sie Nano Server als Zielcomputer  
  
1.  Erstellen des grundlegenden Nano Server-Bilds. Einzelheiten finden Sie unter [Erste Schritte mit Nano Server](https://technet.microsoft.com/library/mt126167.aspx) .  
  
2.  Richten Sie einen Collector-Computer wie im Abschnitt Konfigurieren des Collector-Computers in diesem Thema ein.  
  
3.  Fügen Sie AutoLogger-Registrierungsschlüssel zum Senden von Diagnosenachrichten hinzu. Binden Sie die Nano Server virtuelle Festplatte, die in Schritt 1 erstellt wurde, laden Sie die Registrierungsstruktur und fügen Sie bestimmte Registrierungsschlüssel hinzu. In diesem Beispiel befindet sich das Nano Server-Bild unter C:\NanoServer. Der Pfad kann möglicherweise unterschiedlich sein, also passen Sie die Schritte entsprechend an.  
  
    1.  Kopieren Sie auf dem Sammelcomputer den Ordner **..\Windows\System32\WindowsPowerShell\v1.0\Modules\BootEventCollector** und fügen Sie ihn in das Verzeichnis **..\Windows\System32\WindowsPowerShell\v1.0\Modules** auf dem Computer ein, das Sie verwenden, um die virtuelle Festplatte des Nano-Servers zu ändern.  
  
    2.  Starten Sie eine Windows PowerShell-Konsole mit erhöhten Berechtigungen, und führen Sie `Import-Module BootEventCollector` aus.  
  
    3.  Aktualisieren Sie die Nano Server VHD-Registrierung, um AutoLoggers zu aktivieren. Führen Sie hierzu `Enable-SbecAutoLogger -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd` aus. Dadurch wird eine einfache Liste der am häufigsten verwendeten Setup- und Start-Ereignisse hinzugefügt; Sie können andere Benutzer unter [Controlling Event Tracing Sessions](https://msdn.microsoft.com/library/windows/desktop/aa363694(v=vs.85).aspx) recherchieren.  
  
4.  Aktualisieren Sie die BCD-Einstellungen im Nano Server-Bild zum Aktivieren der Kennzeichen für Ereignisse und Festlegen des Sammelcomputers, um sicherzustellen, dass die Ereignisse an den richtigen Server gesendet werden. Beachten Sie die IPv4-Adresse, TCP-Port und Verschlüsselungsschlüssel des Sammelcomputers, die Sie in der Active.XML-Datei (an anderer Stelle in diesem Thema beschrieben) der Sammlung konfiguriert haben. Verwenden Sie diesen Befehl in einer Windows PowerShell-Konsole mit erhöhten Berechtigungen: `Enable-SbecBcd -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd -CollectorIp 192.168.100.1 -CollectorPort 50000 -Key a.b.c.d`  
  
5.  Aktualisieren Sie den Collector-Computer auf das empfangene Ereignis, das vom Nano Server-Computer gesendet wird, indem Sie entweder den IPv4-Adressbereich, die angegebene IPv4-Adresse oder die Mac-Adresse von Nano Server zur Active. XML-Datei auf dem Collector-Computer hinzufügen (Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers in diesem Thema)  
  
## <a name="starting-the-event-collector-service"></a>Starten Sie den Ereignissammlungsdienst  
Nachdem eine gültigen Konfigurationsdatei auf dem Sammelcomputer gespeichert ist, und ein Zielcomputer konfiguriert ist und der Zielcomputer gestartet wird, wird die Verbindung mit der Sammlung erstellt und Ereignisse werden erfasst.  
  
Das Protokoll für den Collector-Dienst selbst (die sich von Setup und Start des vom Dienst erfassten Daten unterscheidet) finden Sie unter Microsoft-Windows-BootEvent-Collector/Admin. Verwenden Sie die Ereignisanzeige für eine grafische Benutzeroberfläche der Ereignisse. Erstellen Sie eine neue Ansicht: Erweitern Sie **Anwendungs- und Dienstprotokolle**, dann **Microsoft** und klicken Sie dann auf **Windows**. Finden Sie **BootEvent Collector**, erweitern Sie ihn und suchen Sie nach **Admin**.  

-   Mit Windows PowerShell: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin`  
  
-   In einer normalen Eingabeaufforderung: **wevtutil qe Microsoft-Windows-BootEvent-Collector/Admin**  
  
## <a name="troubleshooting"></a>Problembehandlung  
  
### <a name="troubleshooting-installation-of-the-feature"></a>Problembehandlung bei der Installation des Features  
  
||Error|Beschreibung des Fehlers|Symptom|Mögliche Probleme|  
|-|---------|---------------------|-----------|---------------------|  
|Dism.exe|87|Die Featurenamenoption wird in diesem Kontext nicht erkannt.||-   Dies kann vorkommen, wenn Sie den Featurenamen falsch schreiben. Stellen Sie sicher, dass die richtige Schreibweise verwenden und versuchen Sie es erneut.<br />-   Vergewissern Sie sich, dass dieses Feature mit der Version des Betriebssystems verfügbar ist, die Sie verwenden. Führen Sie in Windows PowerShell das Skript **/Online &#124; /Get-Features? { $ _-Match-Start}** . Wenn keine Übereinstimmung zurückgegeben wird, wird wahrscheinlich eine Version ausgeführt, die dieses Feature nicht unterstützt.|  
|Dism.exe|0x800f080c|Der Name > der Funktions \<ist unbekannt.||Wie oben|  
  
### <a name="troubleshooting-the-collector"></a>Problembehandlung bei der Sammlung  
  
**Schlags**  
Die Sammlung protokolliert die eigenen Ereignisse als ETW-Anbieter für die Microsoft-Windows-BootEvent-Sammlung. Zuerst sollten Sie zum Beheben von Problemen in der Sammlung suchen. Sie befinden sich in der Ereignisanzeige unter Anwendungs- und Dienstprotokolle > Microsoft > Windows > BootEvent Collector > Admin, oder Sie können sie in einem Befehlsfenster mit einem der folgenden Befehle aufrufen:  
  
In einer normalen Eingabeaufforderung: **wevtutil qe Microsoft-Windows-BootEvent-Collector/Admin**  
  
In einer Windows PowerShell-Eingabeaufforderung: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin` (Sie können `-Oldest` anfügen, um zuerst die Liste in der zeitlichen Reihenfolge mit den ältesten Ereignissen zurückzugeben)  
  
Sie können den Detailgrad in den Protokollen von "Fehler", "Warnung", "Info" (Standard), "Verbose" und "Debug" anpassen. Ausführlichere Ebenen als Informationen sind nützlich für die Diagnose von Problemen mit Ziel Computern, die keine Verbindung herstellen. Sie können jedoch eine große Datenmenge generieren. verwenden Sie Sie daher mit Bedacht.  
  
Sie legen den mindestprotokolliergrad im \<Collector > Element der Konfigurationsdatei fest. Beispiel: < Collector configversionmajor = 1 minlog\=Verbose >.  
  
Die Ebene "ausführlich" protokolliert einen Eintrag für jedes Paket, das sie verarbeitet. Die Debugebene fügt ausführliche Verarbeitungsdetails hinzu und sichert den Inhalt aller empfangenen ETW-Pakete.  
  
Auf der Debugebene kann es hilfreich sein, eine Datei zu protokollieren, anstatt sie im üblichen Protokollierungssystem anzuzeigen. Fügen Sie zu diesem Zweck im \<Collector > Element der Konfigurationsdatei ein zusätzliches Element hinzu:  
  
< Collector configversionmajor = 1 minlog = Debugprotokoll\=c:\programdata\microsoft\booteventcollector\logs\log.txt >  
      
 **Eine empfohlene Vorgehensweise bei der Problembehandlung für den Collector:**  
   
1. Zunächst stellen Sie sicher, dass die Sammlung die Verbindung vom Zielcomputer empfängt (es wird die Datei nur dann erstellt, wenn der Zielcomputer die Nachrichten sendet) mit   
   ```  
   Get-SbecForwarding  
   ```  
   Wenn er zurückgibt, dass eine Verbindung von diesem Ziel besteht, liegt das Problem möglicherweise in den Einstellungen des Autologgers. Wenn nichts zurückgegeben wird, ist das Problem die KDNET-Verbindung. Versuchen Sie zur Diagnose von Problemen mit KDNET die Verbindung an beiden Enden zu überprüfen (d. h., von der Sammlung und dem Ziel).  
  
2. Um die erweiterte Diagnose aus dem Collector anzuzeigen, fügen Sie diese dem \<Collector > Element der Konfigurationsdatei hinzu:  
   \<Collector... minlog = Verbose >  
   Dadurch werden Nachrichten über jedes empfangene Paket aktiviert.  
3. Überprüfen Sie, ob alle Pakete empfangen werden. Sie können optional das Protokoll im ausführlichen Modus über ETW statt direkt in eine Datei schreiben. Fügen Sie hierzu dem \<Collector > Element der Konfigurationsdatei hinzu:  
   \<Collector... minlog = Verbose Log = c:\programdata\microsoft\booteventcollector \logs\log.txt >  
      
4. Überprüfen Sie die Ereignisprotokolle für Nachrichten über die empfangenen Pakete. Überprüfen Sie, ob alle Pakete empfangen werden. Wenn die Pakete empfangen, aber falsch sind, überprüfen Sie Ereignisnachrichten für Details.  
5. Von der Zielseite gibt KDNET Diagnoseinformationen an die Registrierung. Suchen in   
   **HKLM\SYSTEM\CurrentControlSet\Services\kdnet** nach Nachrichten.  
   KdInitStatus (DWORD) gibt = 0 bei Erfolg und einen Fehlercode bei Fehlern zurück.  
   KdInitErrorString = Beschreibung des Fehlers (enthält informative Nachrichten, wenn kein Fehler)  
  
6. Führen Sie Ipconfig.exe auf dem Ziel aus und überprüfen Sie den Gerätenamen. Wenn KDNet ordnungsgemäß geladen wurde, sollte der Gerätename in etwa wie folgt lauten: kdnic anstelle des Namens des ursprünglichen Herstellers.  
7. Überprüfen Sie, ob DHCP für das Ziel konfiguriert ist. DHCP ist für KDNET absolut erforderlich.  
8. Vergewissern Sie sich, dass die Sammlung im gleichen Netzwerk wie das Ziel ist. Wenn nicht, überprüfen Sie, ob das routing ordnungsgemäß funktioniert, insbesondere ob die Einstellung für DHCP-Standardgateways konfiguriert ist.  
  
  
**Verbindungsstatus**  
  
Sie können die aktuelle Liste der vorhandenen Verbindungen sowie Informationen überprüfen, von wo die Daten weitergeleitet werden mit `Get-SbecForwarding`.  
  
Sie können auch den aktuellen Status Änderungsverlauf abrufen, Verbindungen mit `Get-SbecHistory`.  
  
### <a name="troubleshooting-setting-a-new-configuration"></a>Problembehandlung, wenn eine neue Konfiguration festgelegt wird  
Wenn Sie die Konfiguration mit den Windows PowerShell-Befehl angewendet haben `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result`, enthält die Variable `$result` Informationen über die Bereitstellung. Sie können diese Variable nach verschiedenen Informationen abfragen:  
  
Abrufen von Informationen zu Fehlern mit `$result.ErrorString`. Wenn Fehler gemeldet werden, wird die neue Konfiguration nicht angewendet, und die alte Konfiguration wird nicht geändert.  
  
Abrufen von Warnungen mit `$result.WarningString`.  
  
Abrufen von Informationen zu den Details der Konfiguration mit `$result.InfoString`.  
  
Sie können das vollständige Ergebnis mit `$result | fl *`abrufen.  
Wenn Sie das Ergebnis nicht in einer Variablen speichern möchten, können Sie `Get-Content .\newconfig.xml | Set-SbecActiveConfig | fl *` verwenden.  
  
### <a name="troubleshooting-target-computers"></a>Problembehandlung von Zielcomputern  
  
||Error|Beschreibung des Fehlers|Symptom|Mögliche Probleme|  
|-|---------|---------------------|-----------|---------------------|  
|Bereitstellungszielcomputer||Ziel kann nicht mit der Sammlung verbunden werden||-   Der Zielcomputer wurde nicht neu gestartet, nachdem er konfiguriert wurde. Starten Sie den Zielcomputer neu.<br />-Der Zielcomputer verfügt über falsche BCD-Einstellungen. Überprüfen Sie die Einstellungen im Abschnitt Zielcomputer Einstellungen überprüfen. Korrigieren Sie nach Bedarf, und starten Sie dann den Zielcomputer neu.<br />-   Der KDNET/EVENT-NET-Treiber konnte nicht an einen Netzwerkadapter verbunden werden oder wurde mit dem falschen Netzwerkadapter verbunden. Führen Sie in Windows PowerShell `gwmi Win32_NetworkAdapter` aus, und überprüfen Sie die Ausgabe für eine mit dem ServiceName **Kdnic**. Wenn der falsche Netzwerkadapter ausgewählt ist, führen Sie die Schritte in erneut aus, um einen Netzwerkadapter anzugeben. Wenn der Netzwerkadapter überhaupt nicht angezeigt wird, ist es möglich, dass der Treiber den Netzwerkadapter nicht unterstützt.<br>**Siehe auch** Eine empfohlene Vorgehensweise für die Problembehandlung des obigen Sammlers, insbesondere die Schritte 5 bis 8.|  
|Sammlung||Ich kann keine Ereignisse sehen, nach der Migration des VMs, auf dem meine Sammlung gehostet wird.||Stellen Sie sicher, dass die IP-Adresse des Sammelcomputers nicht geändert wurde. Wenn dies der Fall ist, überprüfen Sie, um das Senden von ETW-Ereignissen über den Transport Remote zu ermöglichen|  
|Sammlung||ETL-Dateien werden nicht erstellt.|`Get-SbecForwarding` zeigt an, dass das Ziel ohne Fehler verbunden ist, die ETL-Dateien aber nicht erstellt werden.|Der Zielcomputer hat wahrscheinlich nicht noch keine Daten gesendet werden. ETL-Dateien werden nur erstellt, wenn Daten empfangen werden.|  
|Sammlung||Ein Ereignis wird nicht in der ETL-Datei angezeigt.|Der Zielcomputer hat das Ereignis gesendet, aber beim Lesen der ETL-Datei mit der Ereignisanzeige des Message Analyzer ist das Ereignis nicht vorhanden.|-   Das Ereignis ist möglicherweise noch im Puffer. Ereignisse werden nicht in die ETL-Datei geschrieben, bis ein vollständiger 64 KB Puffer erfasst wird oder ein Timeout von etwa 10-15 Sekunden ohne neuen Ereignisse auftritt. Warten Sie, bis das Timeout abläuft oder leeren Sie den Puffer mit `Save-SbecInstance`.<br />-   Das Manifest-Ereignis ist nicht auf dem Sammelcomputer oder dem Computer verfügbar, auf dem die Ereignisanzeige oder der Message Analyzer ausgeführt wird.  In diesem Fall kann die Sammlung möglicherweise das Ereignis nicht verarbeiten (überprüfen Sie das Sammlungsprotokoll) oder der Viewer kann es möglicherweise nicht anzeigen.  Es ist ratsam, alle Manifeste auf dem Sammelcomputer installiert zu haben, und Updates auf dem Sammelcomputer vor deren Installation auf den Zielcomputern zu installieren.|
