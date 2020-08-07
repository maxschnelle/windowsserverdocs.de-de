---
title: Erste Schritte mit der Ereignissammlung für Setup und Start
description: Einrichten von Sammlungs-und Start Ereignis Sammlungs-Sammlern und-Zielen
manager: DonGill
ms.localizationpriority: medium
ms.date: 10/16/2017
ms.topic: get-started-article
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247b3f8
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: e5e18ed5f5cc4cba319042f1a5da84acae8e5fd5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879529"
---
# <a name="get-started-with-setup-and-boot-event-collection"></a>Erste Schritte mit der Ereignissammlung für Setup und Start

> Gilt für: Windows Server

## <a name="overview"></a>Übersicht
Die Setup-und Start Ereignis Sammlung ist ein neues Feature in Windows Server 2016, mit dem Sie einen Collector-Computer festlegen können, der eine Vielzahl wichtiger Ereignisse sammelt, die auf anderen Computern beim Starten oder durchlaufen des Setup Vorgangs auftreten. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren.

Bisher war es nicht möglich, diese Ereignisse zu überwachen, da die für die Erfassung erforderliche Infrastruktur erst vorhanden ist, wenn ein Computer bereits eingerichtet ist. Folgende Arten von Setup-und Start Ereignissen können überwacht werden:

-   Laden von Kernel Modulen und-Treibern

-   Enumeration von Geräten und Initialisierung Ihrer Treiber (einschließlich Geräte wie z. b. CPU-Typ)

-   Überprüfung und Einbindung von Dateisystemen

-   Starten von ausführbaren Dateien

-   Starten und vervollständigen von Systemupdates

-   Die Punkte, an denen das System für die Anmeldung zur Verfügung steht, die Verbindung mit einem Domänen Controller herstellt, den Abschluss des Dienst Starts sowie die Verfügbarkeit von Netzwerkfreigaben

Auf dem Collector-Computer muss Windows Server 2016 ausgeführt werden (er kann sich entweder auf einem Server mit Desktop Darstellung oder Server Core-Modus befinden). Auf dem Zielcomputer muss entweder Windows 10 oder Windows Server 2016 ausgeführt werden. Sie können diesen Dienst auch auf einer virtuellen Maschine ausführen, die auf einem Computer gehostet wird, auf dem **nicht** Windows Server 2016 ausgeführt wird. Die folgenden Kombinationen von virtualisierten Collector-und Ziel Computern sind bekanntermaßen funktionsfähig:

|Virtualisierungshost|Virtueller Collector-Computer|Virtueller Zielcomputer|
|-----------------------|-----------------------------|--------------------------|
|Windows 8.1|ja|ja|
|Windows 10|ja|ja|
|Windows Server 2016|ja|ja|
|Windows Server 2012 R2|ja|nein|

## <a name="installing-the-collector-service"></a>Installieren des Collector-Dienstanbieter
Ab Windows Server 2016 ist der Ereignis Sammler Dienst als optionales Feature verfügbar. In dieser Version können Sie Sie mithilfe DISM.exe mit diesem Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten installieren:

`dism /online /enable-feature /featurename:SetupAndBootEventCollection`

Dieser Befehl erstellt einen Dienst mit dem Namen booteventcollector und startet ihn mit einer leeren Konfigurationsdatei.

Überprüfen Sie, ob die Installation erfolgreich war `get-service -displayname *boot*` . Der Start Ereignis Sammler sollte ausgeführt werden. Er wird unter dem Netzwerkdienst Konto ausgeführt und erstellt eine leere Konfigurationsdatei (Active.xml) in **%systemdrive%\programdata\microsoft\booteventcollector\config**.

Sie können den Setup-und Start Ereignis Sammlungs Dienst auch mit dem Assistenten zum Hinzufügen von Rollen und Features in Server-Manager installieren.

## <a name="configuration"></a>Konfiguration
Sie müssen zwei Elemente konfigurieren, um Setup-und Start Ereignisse zu erfassen.

-   Aktivieren Sie auf den Ziel Computern, von denen die Ereignisse gesendet werden (d. h. die Computer, deren Setup und Start Sie überwachen möchten), den KDNet-/Ereignis-Netzwerktransport, und aktivieren Sie die Weiterleitung von Ereignissen.

-   Geben Sie auf dem Collector-Computer an, von welchen Computern Ereignisse angenommen werden sollen und wo Sie gespeichert werden sollen.

> [!NOTE]
> Ein Computer kann nicht so konfiguriert werden, dass Start-oder Start Ereignisse an sich selbst gesendet werden. Wenn Sie jedoch zwei Computer überwachen möchten, können Sie diese so konfigurieren, dass die Ereignisse an einander gesendet werden.

### <a name="configuring-a-target-computer"></a>Konfigurieren eines Bereitstellungs Ziel Computers
Auf jedem Bereitstellungs Zielcomputer aktivieren Sie zuerst den KDNet-/Ereignis-Netzwerktransport, aktivieren dann das Senden von ETW-Ereignissen über den Transport und starten dann den Zielcomputer neu. Event-net ist ein in-Kernel-Transportprotokoll, das mit KDNet (dem Kernel Debugger-Protokoll) vergleichbar ist. Event-NET überträgt nur Ereignisse und gestattet keinen Debugger-Zugriff. Diese beiden Protokolle schließen sich gegenseitig aus. Sie können jeweils nur eine der beiden Elemente gleichzeitig aktivieren.

Sie können den Ereignis Transport Remote (mit Windows PowerShell) oder lokal aktivieren.

##### <a name="to-enable-event-transport-remotely"></a>So aktivieren Sie den Ereignis Transport Remote

1.  Wenn Sie Windows PowerShell-Remoting bereits auf dem Zielcomputer eingerichtet haben, fahren Sie mit Schritt 3 fort. Wenn dies nicht der Wert ist, öffnen Sie auf dem Zielcomputer eine Eingabeaufforderung, und führen Sie den folgenden Befehl aus:

    winrm quickconfig

2.  Antworten Sie auf die Eingabe Aufforderungen, und starten Sie den Zielcomputer neu. Wenn sich die Zielcomputer nicht in derselben Domäne wie der Collector-Computer befinden, müssen Sie Sie möglicherweise als vertrauenswürdige Hosts definieren. Gehen Sie dazu folgendermaßen vor:

3.  Führen Sie auf dem Collector-Computer einen der folgenden Befehle aus:

    -   An einer Windows PowerShell-Eingabeaufforderung: `Set-Item -Force WSMan:\localhost\Client\TrustedHosts <target1>,<target2>,...` , gefolgt von `Set-Item -Force WSMan:\localhost\Client\AllowUnencrypted true` Where \<target1> usw., sind die Namen oder IP-Adressen der Zielcomputer.

    -   Oder an einer Eingabeaufforderung: **WinRM Set WinRM/config/Client @ {treuhändhosts = \<target1> , \<target2> ,...; "Zuweisung" = true}**

        > [!IMPORTANT]
        > Dadurch wird eine unverschlüsselte Kommunikation eingerichtet. Sie sollten dies nicht außerhalb einer Lab-Umgebung tun.

4.  Testen Sie die Remote Verbindung, indem Sie auf den Collector-Computer wechseln und einen dieser Windows PowerShell-Befehle ausführen:

    Wenn sich der Zielcomputer in derselben Domäne wie der Collector-Computer befindet, führen Sie aus.`New-PSSession -Computer <target> | Remove-PSSession`

    Wenn sich der Bereitstellungs Zielcomputer nicht in derselben Domäne befindet, führen `New-PSSession -Computer  <target>  -Credential Administrator | Remove-PSSession` Sie aus, wodurch Sie zur Eingabe von Anmelde Informationen aufgefordert werden.

    Wenn der Befehl nichts zurückgibt, war das Remoting erfolgreich.

5.  Öffnen Sie auf dem Zielcomputer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, und führen Sie diesen Befehl aus:

    `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d>`

    Hier <target_name> der Name des Ziel Computers ist, \<ip> ist die IP-Adresse des Collector-Computers. \<port>die Portnummer, an der der Collector ausgeführt wird. Der Schlüssel <a. b. c. d> ist ein erforderlicher Verschlüsselungsschlüssel für die Kommunikation, bestehend aus vier alphanumerischen Zeichen folgen, die durch Punkte getrennt sind. Dieser Schlüssel wird auf dem Collector-Computer verwendet. Wenn Sie keinen Schlüssel eingeben, generiert das System einen zufälligen Schlüssel. Sie benötigen dies für den Collector-Computer. Notieren Sie sich den Computer.

6.  Wenn Sie bereits einen Collector-Computer eingerichtet haben, aktualisieren Sie die Konfigurationsdatei auf dem Collector-Computer mit den Informationen für den neuen Bereitstellungs Zielcomputer. Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers.

##### <a name="to-enable-event-transport-locally-on-the-target-computer"></a>So aktivieren Sie den Ereignis Transport lokal auf dem Bereitstellungs Zielcomputer

1.  Starten Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie dann die folgenden Befehle aus:

    **bcdedit/Event ja**

    **bcdedit/eventsettings net HostIP: 1.2.3.4 Port: 50000 Key: a. b. c. d**

    Hier ist 1.2.3.4 ein Beispiel: Ersetzen Sie dies durch die IP-Adresse des Collector-Computers. Ersetzen Sie 50000 auch durch die Portnummer, in der der Collector ausgeführt wird, und a. b. c. d mit dem erforderlichen Verschlüsselungsschlüssel für die Kommunikation. Dieser Schlüssel wird auf dem Collector-Computer verwendet. Wenn Sie keinen Schlüssel eingeben, generiert das System einen zufälligen Schlüssel. Sie benötigen dies für den Collector-Computer. Notieren Sie sich den Computer.

2.  Wenn Sie bereits einen Collector-Computer eingerichtet haben, aktualisieren Sie die Konfigurationsdatei auf dem Collector-Computer mit den Informationen für den neuen Bereitstellungs Zielcomputer. Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers.

**Nachdem der Ereignis Transport selbst aktiviert ist, müssen Sie das System aktivieren, um etw-Ereignisse über diesen Transport tatsächlich zu senden.**

##### <a name="to-enable-sending-of-etw-events-through-the-transport-remotely"></a>So aktivieren Sie das Senden von ETW-Ereignissen über den Transport Remote

1.  Öffnen Sie auf dem Collector-Computer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.

2.  Führen Sie `Enable-SbecAutologger -ComputerName <target_name>` aus, wobei <target_name> der Name des Ziel Computers ist.

Wenn Sie Windows PowerShell-Remoting nicht einrichten können, können Sie das Senden von Ereignissen jederzeit direkt auf dem Zielcomputer aktivieren.

##### <a name="to-enable-sending-of-etw-events-through-the-transport-locally"></a>So aktivieren Sie das Senden von ETW-Ereignissen über den lokalen Transport

1.  Starten Sie auf dem Zielcomputer Regedit.exe, und suchen Sie den folgenden Registrierungsschlüssel:

    **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\wmi\autologger**. Verschiedene Protokoll Sitzungen werden unter diesem Schlüssel als Unterschlüssel aufgeführt. **Setup Platform**, **NT Kernel Logger**und **Microsoft-Windows-Setup** sind möglicherweise für die Verwendung mit der Setup-und Start Ereignis Sammlung geeignet. die empfohlene Option ist jedoch **EventLog-System**. Diese Schlüssel werden unter [Konfigurieren und Starten einer autologger-Sitzung](https://msdn.microsoft.com/library/windows/desktop/aa363687(v=vs.85).aspx)ausführlich erläutert.

2.  Ändern Sie im Schlüssel "EventLog-System" den Wert von " **logfilemode** " von " **0x10000180** " in " **0x10080180**". Weitere Informationen zu diesen Einstellungen finden Sie unter [Protokollierungs Modus-Konstanten](https://msdn.microsoft.com/library/windows/desktop/aa364080(v=vs.85).aspx).

3.  Optional können Sie auch die Weiterleitung von Fehler Prüf Daten an den Collector-Computer aktivieren. Suchen Sie hierzu den Registrierungsschlüssel HKEY_LOCAL_MACHINE \system\currentcontrolset\control\session Manager, und erstellen Sie den **schlüsseldebugdruckfilter** mit dem Wert **0x1**.

4.  Starten Sie den Zielcomputer neu.

### <a name="choosing-the-network-adapter"></a>Auswählen des Netzwerkadapters
Wenn der Zielcomputer über mehrere Netzwerkadapter verfügt, wählt der KDNet-Treiber den ersten unterstützten Eintrag aus. Sie können einen bestimmten Netzwerkadapter angeben, der zum Weiterleiten von Setup Ereignissen mit den folgenden Schritten verwendet wird:

##### <a name="to-specify-a-network-adapter"></a>So geben Sie einen Netzwerkadapter an

1.  Öffnen Sie auf dem Zielcomputer Geräte-Manager, erweitern Sie **Netzwerkadapter**, suchen Sie den gewünschten Netzwerkadapter, und klicken Sie mit der rechten Maustaste darauf.

2.  Klicken Sie im geöffneten Menü auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Details** . erweitern Sie das Menü im **Eigenschafts** Feld, Scrollen Sie zu **Speicherort Informationen** (die Liste ist wahrscheinlich nicht in alphabetischer Reihenfolge), und klicken Sie dann auf die Registerkarte. Der Wert ist eine Zeichenfolge der Form **PCI Bus X, Gerät Y, Function Z**. Notieren Sie sich X. Y. Z; Dies sind die Busparameter, die Sie für den folgenden Befehl benötigen.

3.  Führen Sie einen der folgenden Befehle aus:

    An einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten:`Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d> -BusParams <X.Y.Z>`

    An einer Eingabeaufforderung mit erhöhten Rechten: **Bcdedit/eventsettings net HostIP: AAA Port: 50000 Key: BBB busparams: X. Y. Z**

### <a name="validate-target-computer-configuration"></a>Zielcomputer Konfiguration überprüfen
Öffnen Sie zum Überprüfen der Einstellungen auf dem Zielcomputer eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie **bcdedit/enum**aus. Wenn dies abgeschlossen ist, führen Sie **Bcdedit/eventsettings**aus. Sie können die folgenden Werte überprüfen:

-   Key

-   DebugType = net

-   HostIP =\<IP address of the collector>

-   Port = \<port number you specified for the collector to use>

-   DHCP = ja

Überprüfen Sie auch, ob **Bcdedit/Event**aktiviert ist, da sich **/Debug** und **/Event** gegenseitig ausschließen. Sie können nur eine oder die andere ausführen. Ebenso können Sie/eventsettings nicht mit/Debug oder/dbgsettings mit/Event. kombinieren.

Beachten Sie auch, dass die Ereignis Sammlung nicht funktioniert, wenn Sie Sie auf einen seriellen Anschluss festlegen.

### <a name="configuring-the-collector-computer"></a>Konfigurieren des Collector-Computers
Der Collector-Dienst empfängt die Ereignisse und speichert Sie in ETL-Dateien. Diese ETL-Dateien können dann von anderen Tools gelesen werden, z. b. Ereignisanzeige, Message Analyzer, wevtutil und Windows PowerShell-Cmdlets.

Da das ETW-Format nicht zulässt, dass der Name des Ziel Computers angegeben wird, müssen die Ereignisse für die einzelnen Bereitstellungs Zielcomputer in einer separaten Datei gespeichert werden. Die Anzeige Tools zeigen möglicherweise einen Computernamen an, aber der Name des Computers, auf dem das Tool ausgeführt wird.

Genauer gesagt wird jedem Bereitstellungs Zielcomputer ein Ring von ETL-Dateien zugewiesen. Jeder Dateiname enthält einen Index von 000 bis zu einem von Ihnen konfigurierten maximalen Wert (bis zu 999). Wenn die Datei die maximal konfigurierte Größe erreicht, schaltet Sie das Schreiben von Ereignissen in die nächste Datei um. Nach der größtmöglichen Datei wechselt sie zurück in den Datei Index 000. Auf diese Weise werden die Dateien automatisch wieder verwendet, was die Nutzung des Speicherplatzes einschränkt. Sie können auch zusätzliche externe Aufbewahrungs Richtlinien festlegen, um die Datenträger Verwendung weiter einzuschränken. Beispielsweise können Sie Dateien löschen, die älter als eine festgelegte Anzahl von Tagen sind.

Gesammelte ETL-Dateien werden in der Regel im Verzeichnis " **c:\programdata\microsoft\booteventcollector\etl** " gespeichert (die möglicherweise über zusätzliche Unterverzeichnisse verfügen). Sie finden die aktuelle Protokolldatei, indem Sie Sie nach dem Zeitpunkt der letzten Änderung sortieren. Es gibt auch ein Status Protokoll (in der Regel in " **c:\programdata\microsoft\booteventcollector\logs**"), das erfasst, wann der Collector in eine neue Datei schreibt.

Es gibt auch ein Collector-Protokoll, das Informationen über den Collector selbst aufzeichnet. Sie können dieses Protokoll im etw-Format aufbewahren (in dem Ereignisse an den Windows-Protokolldienst gemeldet werden, dies ist die Standardeinstellung) oder in einer Datei (normalerweise in " **c:\programdata\microsoft\booteventcollector\logs**"). Die Verwendung einer Datei kann nützlich sein, wenn Sie ausführliche Modi aktivieren möchten, die viele Daten liefern. Sie können auch festlegen, dass das Protokoll in eine Standardausgabe geschrieben wird, indem Sie den Collector über die Befehlszeile ausführen.

**Erstellen der sammlerkonfigurationsdatei**

Wenn Sie den Dienst aktivieren, werden drei XML-Konfigurationsdateien erstellt und in " **c:\programdata\microsoft\booteventcollector\config**" gespeichert:

-   **Active.xml** Diese Datei enthält die aktuelle aktive Konfiguration des Collector-Dienstanbieter.  Direkt nach der Installation hat diese Datei denselben Inhalt wie Empty.xml. Wenn Sie eine neue Sammler Konfiguration festlegen, speichern Sie Sie in dieser Datei.

-   **Empty.xml** Diese Datei enthält die minimalen Konfigurationselemente, die erforderlich sind, damit ihre Standardwerte festgelegt sind. Es werden keine Sammlungen aktiviert; der Collector-Dienst kann nur im Leerlauf Modus gestartet werden.

-   **Example.xml** Diese Datei enthält Beispiele und Erläuterungen der möglichen Konfigurationselemente.

**Auswählen einer Dateigrößen Beschränkung**

Eine der Entscheidungen, die Sie treffen müssen, besteht darin, eine Dateigrößen Beschränkung festzulegen. Die beste Dateigröße hängt von der erwarteten Anzahl von Ereignissen und dem verfügbaren Speicherplatz ab. Kleinere Dateien sind aus der Sicht der Bereinigung der alten Daten besser geeignet. Allerdings enthält jede Datei den Aufwand für einen Header mit 64 KB, und das Lesen vieler Dateien, um den kombinierten Verlauf zu erhalten, kann unpraktisch sein. Die absolute Mindestgröße für die Dateigröße beträgt 256 KB. Eine vernünftige praktische Dateigrößen Beschränkung sollte mehr als 1 MB betragen, und 10 MB ist wahrscheinlich ein guter typischer Wert. Ein höheres Limit kann sinnvoll sein, wenn Sie viele Ereignisse erwarten.

Im Hinblick auf die Konfigurationsdatei sind einige Details zu beachten:

-   Die Zielcomputer Adresse. Sie können die IPv4-Adresse, eine Mac-Adresse oder eine SMBIOS-GUID verwenden. Beachten Sie diese Faktoren bei der Auswahl der zu verwendenden Adresse:

    -   Die IPv4-Adresse funktioniert am besten mit der statischen Zuweisung der IP-Adressen. Allerdings müssen auch statische IP-Adressen über DHCP verfügbar sein.

    -   Eine Mac-Adresse oder eine SMBIOS-GUID ist praktisch, wenn Sie im Voraus bekannt sind, aber die IP-Adressen dynamisch zugewiesen werden.

    -   IPv6-Adressen werden vom Ereignis-net-Protokoll nicht unterstützt.

    -   Es ist möglich, mehrere Möglichkeiten zum Identifizieren des Computers anzugeben. Wenn z. b. die physische Hardware gerade ersetzt wird, können Sie sowohl die alte als auch die neue Mac-Adresse eingeben. beide werden akzeptiert.

-   Der Verschlüsselungsschlüssel, der für die Kommunikation mit dem Collector-Computer verwendet wird.

-   Name des Zielcomputers. Sie können die IP-Adresse, den Hostnamen oder einen beliebigen anderen Namen als Computernamen verwenden.

-   Der Name der zu verwendenden ETL-Datei und die Ringgrößen Konfiguration.

##### <a name="to-create-the-configuration-file"></a>So erstellen Sie die Konfigurationsdatei

1.  Öffnen Sie eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, und wechseln Sie zum Verzeichnis%SystemDrive%\programdata\microsoft\booteventcollector\config.

2.  `notepad .\newconfig.xml`Und drücken Sie die EINGABETASTE.

3.  Kopieren Sie diese Beispielkonfiguration in das Editor-Fenster:

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
    > Der Stamm Knoten ist \<collector> . Die Attribute geben die Version der Konfigurationsdatei Syntax und den Namen der Status Protokolldatei an.
    >
    > Das- \<common> Element gruppiert mehrere Ziele und gibt dabei die allgemeinen Konfigurationselemente an. ähnlich wie eine Benutzergruppe kann verwendet werden, um die allgemeinen Berechtigungen für mehrere Benutzer anzugeben.
    >
    > Das- \<collectorport> Element definiert die UDP-Portnummer, an der der Collector auf eingehende Daten lauscht. Dabei handelt es sich um den Port, der im Ziel Konfigurationsschritt für bcdedit angegeben wurde. Der Collector unterstützt nur einen Port, und alle Ziele müssen eine Verbindung mit dem gleichen Port herstellen.
    >
    > Das- \<forwarder> Element gibt an, wie von den Ziel Computern empfangene ETW-Ereignisse weitergeleitet werden. Es gibt nur einen Weiterleitungstyp, der Sie in die ETL-Dateien schreibt. Die Parameter geben das Dateinamen Muster, das Größenlimit für jede Datei im Ring und die Größe des Rings für jeden Computer an. Die Einstellung "dexml" gibt an, dass die ETW-Ereignisse in der Binär Form geschrieben werden, während Sie empfangen wurden, ohne in XML zu konvertieren. Weitere Informationen zur Entscheidung, ob die Ereignisse XML-Daten in XML konvertiert werden sollen, finden Sie im Abschnitt XML-Ereignis Konvertierung. Das Dateinamen Muster enthält diese Ersetzungen: {Computer} für den Computernamen und {#3} für den Index der Datei im Ring.
    >
    > In dieser Beispieldatei werden zwei Zielcomputer mit dem- \<target> Element definiert. Jede Definition gibt die IP-Adresse mit an \<ipv4> . Sie können jedoch auch die Mac-Adresse (z. b. `<mac value=11:22:33:44:55:66/>` oder `<mac value=11-22-33-44-55-66/>` ) oder die SMBIOS-GUID (z `<guid value={269076F9-4B77-46E1-B03B-CA5003775B88}/>` . b.) verwenden, um den Zielcomputer zu identifizieren. Beachten Sie auch den Verschlüsselungsschlüssel (der mit bcdedit auf dem Zielcomputer angegeben oder generiert wurde) und den Computernamen.

4. Geben Sie die Details für jeden Bereitstellungs Zielcomputer als separates \<target> Element in der Konfigurationsdatei ein, und speichern Sie Newconfig.xml, und schließen Sie dann den Editor.

5. Wenden Sie die neue Konfiguration mit an `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result` . Die Ausgabe sollte mit dem Erfolgs Feld true zurückgegeben werden. Wenn Sie ein weiteres Ergebnis erhalten, finden Sie weitere Informationen im Abschnitt zur Problembehandlung in diesem Thema.

Sie können die aktuelle aktive Konfiguration immer mit überprüfen `(Get-SbecActiveConfig).text` .

Sie können eine Gültigkeits Überprüfung für die Konfigurationsdatei mit ausführen `$result = (Get-Content .\newconfig.xml | Check-SbecConfig); $result` .

Obwohl der Windows PowerShell-Befehl zum Anwenden einer neuen Konfiguration den Dienst automatisch aktualisiert, ohne dass ein Neustart erforderlich ist, können Sie den Dienst mit einem der folgenden Befehle jederzeit neu starten:

- Mit Windows PowerShell:`Restart-Service BootEventCollector`

- An einer normalen Eingabeaufforderung: **SC beenden booteventcollector; SC Start booteventcollector**

## <a name="configuring-nano-server-as-a-target-computer"></a>Konfigurieren von Nano Server als Bereitstellungs Zielcomputer

Die minimale von Nano Server angebotene Schnittstelle kann es manchmal schwierig machen, Probleme mit dieser zu diagnostizieren. Sie können Ihr Nano Server-Image so konfigurieren, dass es automatisch an der Setup-und Start Ereignis Sammlung teilnimmt und Diagnosedaten ohne weiteren Eingriff an einen Collector-Computer sendet. Gehen Sie hierzu folgendermaßen vor:

### <a name="to-configure-nano-server-as-a-target-computer"></a>So konfigurieren Sie nano Server als Bereitstellungs Zielcomputer

1. Erstellen Sie Ihr grundlegendes Nano Server-Image. Weitere Informationen finden Sie [unter "Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx) ".

2. Richten Sie einen Collector-Computer wie im Abschnitt Konfigurieren des Collector-Computers in diesem Thema ein.

3. Fügen Sie autologger-Registrierungsschlüssel hinzu, um das Senden von Diagnosemeldungen zu ermöglichen Hierzu stellen Sie die in Schritt 1 erstellte Nano Server-VHD ein, laden die Registrierungs Struktur und fügen dann bestimmte Registrierungsschlüssel hinzu. In diesem Beispiel befindet sich das Nano Server-Image unter c:\nanoserver; der Pfad ist möglicherweise anders, passen Sie die Schritte also entsprechend an.

    1. Kopieren Sie auf dem Collector-Computer die **. Ordner \Windows\System32\WindowsPowerShell\v1.0\modules\booteventcollector** , und fügen Sie ihn in die-Datei ein **. \Windows\System32\WindowsPowerShell\v1.0\modules** Verzeichnis auf dem Computer, den Sie zum Ändern der Nano Server-VHD verwenden.

    2. Starten Sie eine Windows PowerShell-Konsole mit erhöhten Berechtigungen, und führen Sie aus `Import-Module BootEventCollector` .

    3. Aktualisieren Sie die Nano Server-VHD-Registrierung, um autologger zu aktivieren. Führen Sie dazu aus `Enable-SbecAutoLogger -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd` . Dadurch wird eine einfache Liste der typischen Setup-und Start Ereignisse hinzugefügt. Weitere Untersuchungen finden Sie unter [Steuern von Ereignis Ablauf Verfolgungs Sitzungen](https://msdn.microsoft.com/library/windows/desktop/aa363694(v=vs.85).aspx).

4. Aktualisieren Sie die BCD-Einstellungen im Nano Server-Abbild, um das Ereignis Flag zu aktivieren, und legen Sie den Collector-Computer fest, damit Diagnose Ereignisse an den richtigen Server gesendet werden. Notieren Sie sich die IPv4-Adresse, den TCP-Port und den Verschlüsselungsschlüssel des Collector-Computers, die Sie in der Active.XML Datei des Sammlers konfiguriert haben (in diesem Thema beschrieben). Verwenden Sie diesen Befehl in einer Windows PowerShell-Konsole mit erhöhten Berechtigungen:`Enable-SbecBcd -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd -CollectorIp 192.168.100.1 -CollectorPort 50000 -Key a.b.c.d`

5. Aktualisieren Sie den Collector-Computer so, dass vom Nano Server-Computer gesendete Ereignisse empfangen werden, indem Sie entweder den IPv4-Adressbereich, die angegebene IPv4-Adresse oder die Mac-Adresse von Nano Server zur Active.XML Datei auf dem Collector-Computer hinzufügen (Weitere Informationen finden Sie im Abschnitt Konfigurieren des Collector-Computers in diesem Thema).

## <a name="starting-the-event-collector-service"></a>Der Ereignis Sammler Dienst wird gestartet.

Sobald eine gültige Konfigurationsdatei auf dem Collector-Computer gespeichert und ein Bereitstellungs Zielcomputer konfiguriert ist, wird die Verbindung mit dem Collector hergestellt, und es werden Ereignisse gesammelt, sobald der Zielcomputer neu gestartet wird.

Das Protokoll für den Sammlungs Dienst (unterscheidet sich von den Setup-und Startdaten, die vom Dienst gesammelt werden) finden Sie unter Microsoft-Windows-bootevent-Collector/admin. Verwenden Sie Ereignisanzeige für eine grafische Oberfläche für die Ereignisse. Erstellen Sie eine neue Ansicht. Erweitern Sie **Anwendungs-und Dienst Protokolle**, und erweitern Sie dann **Microsoft** und dann **Windows**. Suchen Sie den Eintrag **bootevent-Collector**, erweitern Sie ihn, und suchen Sie nach **Admin**.

- Mit Windows PowerShell:`Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin`

- An einer normalen Eingabeaufforderung: **wevtutil QE Microsoft-Windows-bootevent-Collector/admin**

## <a name="troubleshooting"></a>Problembehandlung

### <a name="troubleshooting-installation-of-the-feature"></a>Problembehandlung bei der Installation des Features

| Fehler | Fehlerbeschreibung | Symptom | Potenzielles Problem |
|--|--|--|--|
| Dism.exe | 87 | Die Option "Feature-Name" wird in diesem Kontext nicht erkannt. |  Dies kann vorkommen, wenn Sie den Funktionsnamen falsch schreiben. Vergewissern Sie sich, dass Sie die richtige Schreibweise haben, und versuchen Sie es Vergewissern Sie sich, dass dieses Feature unter der von Ihnen verwendeten Betriebssystemversion verfügbar ist. Führen Sie in Windows PowerShell `dism /online /get-features &#124; ?{$_ -match boot}`aus. Wenn keine Entsprechung zurückgegeben wird, führen Sie wahrscheinlich eine Version aus, die dieses Feature nicht unterstützt. |
| Dism.exe | 0x800f 080c | Die Funktion `<name>` ist unbekannt. | Wie oben |

### <a name="troubleshooting-the-collector"></a>Problembehandlung beim Collector

**Protokollierung:** Der Collector protokolliert seine eigenen Ereignisse als ETW-Anbieter Microsoft-Windows-bootevent-Collector. Es ist der erste Ort, bei dem Sie nach Problemen mit dem Collector suchen sollten. Sie finden Sie in Ereignisanzeige unter Anwendungs-und Dienst Protokolle > Microsoft > Windows > bootevent-Collector > admin, oder Sie können Sie mit einem der folgenden Befehle in einem Befehlsfenster lesen:

An einer normalen Eingabeaufforderung: **wevtutil QE Microsoft-Windows-bootevent-Collector/admin**

An einer Windows PowerShell-Eingabeaufforderung: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin` (Sie können anfügen `-Oldest` , um die Liste in chronologischer Reihenfolge mit den ältesten Ereignissen zuerst zurückzugeben)

Sie können den Detailgrad in den Protokollen von "Fehler", "Warnung", "Info" (Standard), "Verbose" und "Debug" anpassen. Ausführlichere Ebenen als Informationen sind nützlich für die Diagnose von Problemen mit Ziel Computern, die keine Verbindung herstellen. Sie können jedoch eine große Datenmenge generieren. verwenden Sie Sie daher mit Bedacht.

Sie legen die minimale Protokollebene im- \<collector> Element der Konfigurationsdatei fest. Beispiel: <Collector configversionmajor = 1 minlog \= ausführliche>.

Die ausführliche Ebene protokolliert einen Datensatz für jedes bei der Verarbeitung empfangene Paket. Die Debugebene fügt weitere Verarbeitungsdetails hinzu und sichert auch den Inhalt aller empfangenen etw-Pakete.

Auf Debugebene kann es hilfreich sein, das Protokoll in eine Datei zu schreiben, anstatt zu versuchen, es im üblichen Protokollierungs System anzuzeigen. Fügen Sie zu diesem Zweck ein zusätzliches Element im- \<collector> Element der Konfigurationsdatei hinzu:

<Collector configversionmajor = 1 minlog = Debug Log \=c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt>

 **Eine empfohlene Vorgehensweise bei der Problembehandlung für den Collector:**

1. Vergewissern Sie sich zunächst, dass der Collector die Verbindung vom Ziel erhalten hat (die Datei wird nur erstellt, wenn das Ziel mit dem Senden der Nachrichten beginnt) mit
   ```
   Get-SbecForwarding
   ```
   Wenn zurückgegeben wird, dass eine Verbindung mit diesem Ziel besteht, kann das Problem in den Einstellungen des automatischen Bereitstellungs Modus liegen. Wenn nichts zurückgegeben wird, besteht das Problem darin, dass die KDNet-Verbindung mit gestartet wird. Um KDNet-Verbindungsprobleme zu diagnostizieren, versuchen Sie, die Verbindung von beiden Enden (d. h. vom Collector und vom Ziel) zu überprüfen.

2. Fügen Sie dem- \<collector> Element der Konfigurationsdatei Folgendes hinzu, um die erweiterte Diagnose aus dem Collector anzuzeigen:\<collector ... minlog=verbose>
   Dadurch werden Meldungen zu allen empfangenen Paketen aktiviert.
3. Überprüfen Sie, ob überhaupt Pakete empfangen werden. Optional können Sie das Protokoll im ausführlichen Modus direkt in eine Datei schreiben, anstatt über etw. Fügen Sie hierzu dem- \<collector> Element der Konfigurationsdatei Folgendes hinzu:\<collector ... minlog=verbose log=c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt>

4. Überprüfen Sie die Ereignisprotokolle auf Meldungen zu den empfangenen Paketen. Überprüfen Sie, ob überhaupt Pakete empfangen werden. Wenn die Pakete empfangen werden, aber falsch sind, überprüfen Sie die Ereignismeldungen auf Details.
5. Von der Zielseite schreibt KDNet einige Diagnoseinformationen in die Registrierung. Suchen Sie unter " **hklm\system\currentcontrolset\services\kdnet** " nach Nachrichten.
   Kdinitstatus (DWORD) lautet bei Erfolg = 0 und zeigt einen Fehlercode für den Fehler kdiniterrorstring = Erklärung des Fehlers an (enthält auch Informationsmeldungen, wenn kein Fehler vorliegt).

6. Führen Sie Ipconfig.exe auf dem Ziel aus, und überprüfen Sie den Gerätenamen, den er meldet. Wenn KDNet ordnungsgemäß geladen wurde, sollte der Gerätename in etwa wie folgt lauten: kdnic anstelle des Namens des ursprünglichen Herstellers.
7. Überprüfen Sie, ob DHCP für das Ziel konfiguriert ist. KDNet erfordert unbedingt DHCP.
8. Vergewissern Sie sich, dass sich der Collector im gleichen Netzwerk befindet wie das Ziel. Wenn dies nicht der Wert ist, überprüfen Sie, ob das Routing ordnungsgemäß konfiguriert ist, insbesondere die gatewayeinstellung für DHCP.


**Verbindungsstatus**

Sie können die aktuelle Liste der eingerichteten Verbindungen und Informationen überprüfen, mit denen die Daten weitergeleitet werden `Get-SbecForwarding` .

Sie können auch den aktuellen Verlauf der Statusänderungen in Verbindungen mit erhalten `Get-SbecHistory` .

### <a name="troubleshooting-setting-a-new-configuration"></a>Problembehandlung beim Festlegen einer neuen Konfiguration
Wenn Sie die Konfiguration mit dem Windows PowerShell-Befehl angewendet `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result` haben, enthält die Variable `$result` Informationen zur Bereitstellung. Sie können diese Variable Abfragen, um andere Informationen zu erhalten:

Informationen zu Fehlern mit erhalten `$result.ErrorString` . Wenn hier Fehler gemeldet werden, wird die neue Konfiguration nicht angewendet, und die alte Konfiguration wird unverändert.

Warnungen mit erhalten `$result.WarningString` .

Informationen zu den Details der Konfiguration finden Sie unter `$result.InfoString` .

Sie können das gesamte Ergebnis mit erhalten `$result | fl *` .
Wenn Sie das Ergebnis nicht in einer Variablen speichern möchten, können Sie alternativ verwenden `Get-Content .\newconfig.xml | Set-SbecActiveConfig | fl *` .

### <a name="troubleshooting-target-computers"></a>Problembehandlung bei Ziel Computern

| Fehler | Fehlerbeschreibung | Potenzielles Problem |
|--|--|--|
| Bereitstellungszielcomputer | Das Ziel stellt keine Verbindung mit dem Collector her. | Der Zielcomputer konnte nicht neu gestartet werden, nachdem er konfiguriert wurde. Starten Sie den Zielcomputer neu. Der Zielcomputer weist falsche BCD-Einstellungen auf. Überprüfen Sie die Einstellungen im Abschnitt Zielcomputer Einstellungen überprüfen. Korrigieren Sie die nach Bedarf, und starten Sie den Zielcomputer neu.<p>Der KDNet/Event-NET-Treiber konnte keine Verbindung mit einem Netzwerkadapter herstellen oder eine Verbindung mit dem falschen Netzwerkadapter herstellen. Führen Sie in Windows PowerShell `gwmi Win32_NetworkAdapter` aus, und überprüfen Sie die Ausgabe mit dem Dienstnamen **kdnic**. Wenn der falsche Netzwerkadapter ausgewählt ist, führen Sie die Schritte in erneut aus, um einen Netzwerkadapter anzugeben. Wenn der Netzwerkadapter überhaupt nicht angezeigt wird, kann der Treiber den Netzwerkadapter nicht unterstützen.<p>**Siehe auch:** Eine empfohlene Vorgehensweise für die Problembehandlung des obigen Sammlers, insbesondere die Schritte 5 bis 8. |
| Collector | Nach der Migration des virtuellen Computers, auf dem mein Collector gehostet wird, werden keine Ereignisse mehr angezeigt. | Vergewissern Sie sich, dass die IP-Adresse des Collector-Computers nicht geändert wurde. Wenn dies der Fall ist, überprüfen Sie, um das Senden von ETW-Ereignissen über den Transport Remote zu ermöglichen |
| Collector | Die ETL-Dateien werden nicht erstellt. | `Get-SbecForwarding`zeigt an, dass das Ziel ohne Fehler verbunden ist, aber die ETL-Dateien nicht erstellt werden. | Der Zielcomputer hat wahrscheinlich noch keine Daten gesendet. ETL-Dateien werden nur erstellt, wenn Daten empfangen werden. |
| Collector | Ein Ereignis wird nicht in der ETL-Datei angezeigt. | Der Zielcomputer hat ein Ereignis gesendet, aber wenn die ETL-Datei mit Ereignisanzeige von Message Analyzer gelesen wird, ist das Ereignis nicht vorhanden. Das Ereignis kann sich weiterhin im Puffer befinden. Ereignisse werden erst dann in die ETL-Datei geschrieben, wenn ein vollständiger 64 KB-Puffer oder ein Timeout von ungefähr 10-15 Sekunden ohne neue Ereignisse aufgetreten ist. Warten Sie, bis das Timeout abläuft, oder leeren Sie die Puffer mit `Save-SbecInstance` .<p>Das Ereignis Manifest ist auf dem Collector-Computer oder auf dem Computer, auf dem die Ereignisanzeige oder die Message Analyzer ausgeführt wird, nicht verfügbar.  In diesem Fall kann der Collector das Ereignis möglicherweise nicht verarbeiten (überprüfen Sie das Collector-Protokoll), oder der Viewer kann es möglicherweise nicht anzeigen.  Es empfiehlt sich, alle Manifeste auf dem Collector-Computer zu installieren und vor der Installation auf den Ziel Computern Updates auf dem Collector-Computer zu installieren. |
