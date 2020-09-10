---
title: Aggregator der Protokollierung des Softwarebestands
description: Beschreibt das Installieren und Verwalten des Aggregators der Protokollierung des Software Bestands-Software-Inventory-Logging
ms.topic: article
ms.assetid: e4230a75-6bcd-47d9-ba92-a052a90a6abc
author: brentfor
ms.author: brentf
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d533480c18919933d3581901dd8377556c6571c7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628226"
---
# <a name="software-inventory-logging-aggregator"></a>Aggregator der Protokollierung des Softwarebestands

> Gilt für: Windows Server 2012 R2

## <a name="what-is-software-inventory-logging-aggregator"></a>Was ist der Aggregator der Protokollierung des Software Bestands?

Der Aggregator der Protokollierung des Softwarebestands (SILA) empfängt, aggregiert und erzeugt grundlegende Berichte über die Anzahl und Typen installierter Microsoft Enterprise Software auf Windows-Servern in einem Rechenzentrum.

SILA ist Software, die Sie unter Windows Server installieren, aber sie ist nicht in der Windows Server-Installation enthalten. Um die Software zu installieren, laden Sie sie zunächst kostenlos aus dem Windows Download Center herunter: [Aggregator der Protokollierung des Softwarebestands 1.0 für Windows Server](https://www.microsoft.com/download/details.aspx?id=49046)

Das Framework der Protokollierung des Softwarebestands soll die Betriebskosten der Inventarisierung von Microsoft-Software senken, die auf mehreren Servern in einer IT-Umgebung bereitgestellt ist. Dieses Framework besteht aus zwei Komponenten, diesem SIL-Aggregator und der Windows Server-Funktion, die in Windows Server 2012 R2 (Software Inventory Logging, SIL) eingeführt wurde. Dieser Aggregator der Protokollierung des Softwarebestands 1.0 wird auf einem Server installiert und empfängt dann Inventardaten von allen Windows-Servern, die so konfiguriert sind, dass sie Daten an ihn über SIL weiterleiten. Das Design ermöglicht es Administratoren von Rechenzentren, SIL in Windows Server-Masterimages zu aktivieren, die für die breite Verteilung in der jeweiligen Umgebung gedacht sind.  Dieses Softwarepaket ist der Zielpunkt und soll von den Kunden in ihren Standorten installiert werden, um eine einfache Protokollierung von Inventardaten im zeitlichen Verlauf zu ermöglichen. Mit dieser Software können Sie außerdem regelmäßig grundlegende Inventarberichte in Microsoft Excel erstellen. Aggregator der Protokollierung des Softwarebestands 1.0-Berichte enthalten die Anzahl der Installationen von Windows Server, System Center und SQL Server.

> [!IMPORTANT]
> Bei Verwendung dieser Software werden keine Daten an Microsoft gesendet.

### <a name="data-sil-collects-over-time"></a>Von SIL im zeitlichen Verlauf erfasste Daten

Nachdem er ordnungsgemäß bereitgestellt wurde, können die folgenden Daten im SIL-Aggregator angezeigt werden:

-   Eindeutige Windows Server-Installationen in Ihrem Rechenzentrum

-   FQDN

-   Identifikations-GUIDs

-   Anzahl der physischen Prozessoren und Kerne

-   Anzahl der virtuellen Prozessoren (bei virtuellen Computern)

-   Modell und Typ der physischen Prozessoren

-   Ob Hyperthreading auf physischen Prozessoren aktiviert ist oder nicht

-   Seriennummer des Gehäuses

-   Wert der oberen Grenze für die und Identität der gleichzeitig ausgeführten virtuellen Windows Server-Computer (wenn auf einem Host einen Hypervisor ausgeführt wird) auf jedem Host im zeitlichen Verlauf

-   Anzahl der oberen Wasserzeichen und Hostname des gleichzeitig verwalteten \( System Center-Agents, die \) auf jedem Host Windows Server-VMS darstellen, im Zeitverlauf

-   Name der System Center-Agents, die auf virtuellen Computern installiert sind, die in der verwalteten oberen \- Grenze

-   Anzahl und Speicherort der SQL Server Installationen im Lauf der Zeit \( nur SKUs und Editionen, die eine Lizenz erfordern\)

-   Listen der in „Software“ installierten Programme

### <a name="who-will-use-sil"></a>Wer soll SIL verwenden?

-   **IT-Experten oder Administratoren von Rechenzentren**, die eine kostengünstige Methode suchen, wertvolle Softwareinventardaten automatisch und im zeitlichen Verlauf zu sammeln.

-   **CIOs und Finanz Controller**, die die Nutzung von Microsoft Enterprise Software in den IT-bereit Stellungen ihrer Organisationen melden müssen.

## <a name="getting-started"></a>Erste Schritte
**Voraussetzungen**

Aggregator der Protokollierung des Softwarebestands (SIL Aggregator) auf mindestens einem Server für Aggregation und Berichte, entweder auf einem virtuellen Computer oder auf physischer Hardware):

-   **Windows Server 2012 R2** (Standard oder Datacenter Edition)

-   **Die IIS-Serverrolle** ist zusammen mit .NET Framework 4.5, den WCF-Diensten und der HTTP-Aktivierung in derselben Auswahlstruktur im **Assistenten zum Hinzufügen von Rollen und Features** verfügbar.

-   **SQLServer** 2012 SP2 Standard Edition oder SQL Server 2014 Standard Edition

-   **64-Bit-Microsoft Excel** 2013 (optional für die Installation, aber erforderlich zum Erstellen von Berichten)

-   Optional: **VMware PowerCLI 5.5.0.5836** (erforderlich in VMware-Umgebungen)

>[!Note]
>Bei Verwendung von Windows Management Framework gibt es ein bekanntes Kompatibilitätsproblem mit WMF Release 5,1 auf dem SIL-Aggregator.  Es ist nicht erforderlich, WMF Version 4,0 auf Servern mit installiertem SIL-Aggregator zu überschreiten.

Protokollierung des Softwarebestands (SIL) ist in Windows Server-Versionen vorhanden, bei denen die folgenden Updates installiert sind:

-   **Windows Server 2016**oder höher

-   **Windows Server 2012 R2** (Standard oder Datacenter Edition)

    -   Windows Server 2012 R2 Update **KB3000850** (November 2014)

    -   Windows Server 2012 R2-Update **KB3060681** (Juni 2015)(wird ggf. auf Windows Update als optionales Update angezeigt)

### <a name="security-and-account-types"></a>Sicherheit und Kontotypen
**Zertifikat Anforderung**

SIL und SIL-Aggregator verwenden für authentifizierte Kommunikation SSL-Zertifikate. Die gängige Implementierung hiervon besteht in der Installation des SIL-Aggregators mit einem Zertifikat (übereinstimmender Server- und Zertifikatname), um den Webdienst zu hosten, der Inventardaten empfängt. Anschließend verwenden die Windows-Server, die mithilfe der SIL-Funktion inventarisiert werden sollen, ein anderes Clientzertifikat, um Daten per Push an den SIL-Aggregator zu übertragen. Ein PowerShell-Cmdlet ("Set-silaggregator", weitere Details unten) muss verwendet werden, um Zertifikat Fingerabdrücke der Liste der genehmigten Zertifikate des SIL-Aggregators hinzuzufügen, von denen der Aggregator zugeordnete Daten akzeptiert. Der SIL-Aggregator fährt mit der Verarbeitung und dem Einfügen in die Datenbank fort, nachdem die jeweilige Nutzlast von Daten mit einem Zertifikat authentifiziert wurde. Ausführlichere Informationen zur Funktionsweise finden Sie im Abschnitt **Details zu SIL-Aggregator-Cmdlets**.

### <a name="polling-account-setup"></a>Einrichten des Abrufkontos
Wenn Sie dem SIL-Aggregator Anmeldeinformationen hinzufügen, um Abrufvorgänge zu ermöglichen, sollten Sie einen Ansatz mit einem möglichst gering berechtigten Konto verfolgen. Als bewährte Sicherheitsmaßnahme sollten Sie außerdem nicht die gleichen Anmelde Informationen für alle oder viele Hosts in einem Rechenzentrum oder einer anderen IT-Bereitstellung verwenden.

Führen Sie auf einem Windows Server-Host, den Sie für den Abruf durch den SIL-Aggregator einrichten möchten, und um die Verwendung eines Benutzers aus der Administratorengruppe zu vermeiden, diese Schritte aus, um einem Benutzerkonto nur die notwendigen Mindestzugriffsberechtigungen zu erteilen:

#### <a name="to-setup-a-polling-account"></a>So richten Sie ein Abrufkonto ein

1.  Erstellen Sie auf dem Windows Server-Hyper-V-Host, von dem Ihr SIL-Aggregator abrufen soll, ein lokales Benutzerkonto, indem Sie die **Computerverwaltung** in Windows verwenden (achten Sie darauf, dass das Kontrollkästchen deaktiviert ist, das eine Kennwortänderung bei der ersten Anmeldung erzwingt).

2.  Fügen Sie diesen Benutzer der Gruppe **Remoteverwaltungsbenutzer** hinzu.

3.  Fügen Sie diesen Benutzer der Gruppe **Hyper-V-Administratoren** hinzu.

4.  Öffnen Sie **Wmimgmt. msc** mit **Start** -> **Run**.

5.  Klicken Sie im Abschnitt **Aktionen** auf **Weitere Aktionen**, und wählen Sie **Eigenschaften** aus.

6.  Klicken Sie auf **Sicherheit**.

7.  Wählen Sie in der Strukturansicht **Namespace** den Eintrag **cimv2 namespace** aus.

8.  Klicken Sie auf die Schaltfläche **Sicherheit**.

9. Fügen Sie die Gruppe **Remoteverwaltungsbenutzer** im Format **Computername\Gruppenname** hinzu.

10. Klicken Sie auf **OK**.

11. Wenn Sie in das Fenster „Sicherheit“ für **root\cimv2** zurückgekehrt sind, wählen Sie die Gruppe **Remoteverwaltungsbenutzer** aus.

12. Vergewissern Sie sich, dass im Abschnitt "Berechtigungen" am unteren Rand die Option **Remote Aktivierung** aktiviert ist.

13. Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.

14. Klicken Sie im Fenster **Eigenschaften** auf **OK** .

### <a name="installing-sil-aggregator"></a>Installieren des SIL-Aggregators
Es gibt einige Dinge, die Sie vor der Installation des SIL-Aggregators auf einem Windows-Server überprüfen müssen:

-   **Sie verfügen über ein gültiges SSL-Zertifikat** , das Sie zum Hosten des Webdiensts dieser Software verwenden möchten.

    -   Das Zertifikat sollte im **PFX** -Format sein.

    -   Der Name des Windows-Servers und der Zertifikatname müssen übereinstimmen.

-   **SQL Server Standard Edition ist installiert**, oder sie ist auf einem Remoteserver installiert, der mit dieser Software verwendet werden soll.

    -   SIL-Aggregator funktioniert sowohl mit SQL Server 2012 SP2 als auch mit SQL Server 2014. Es ist nichts Ungewöhnliches erforderlich, wenn Sie während der Installation von SQL Server Optionen auswählen.

    -   Das für die Installation des SIL-Aggregators verwendete Konto muss die sysadmin-Rolle in SQL besitzen, damit es die Datenbank während der Installation erstellen kann.

    -   Das für die Installation des SIL-Aggregators verwendete Konto sollte in den SQL Analysis Services als Administrator hinzugefügt werden, bevor der SIL-Aggregator installiert wird.

    -   Sobald der SQL Server-Agent installiert ist, sollte er für die automatische Ausführung konfiguriert werden.

-   **Die IIS-Serverrolle wird** zusammen mit .NET Framework 4.5, den WCF-Diensten und der HTTP-Aktivierung, alle in derselben Auswahlstruktur im **Assistenten zum Hinzufügen von Rollen und Features**, hinzugefügt.

-   Sie sind bei **dem Server mit einem Konto angemeldet, das auf dem Server über Administratorberechtigungen verfügt** .

-   Sie sind bei **dem Server mit einem Konto angemeldet, das auf dem SQL Server über sysadmin-Berechtigungen verfügt**, wenn Windows-Authentifizierung gewünscht ist.

    oder

    Wenn SQL-Authentifizierung gewünscht ist, **haben Sie das Kennwort für ein Konto mit SQL-Administratorrechten**.

#### <a name="to-install-software-inventory-logging-aggregator"></a>So installieren Sie den Aggregator der Protokollierung des Softwarebestands

1.  Doppelklicken Sie auf **Setup.exe**, um die Installation zu starten.

2.  Klicken Sie im Begrüßungsfenster auf **Weiter**.

3.  Wenn Sie den Endbenutzer-Lizenzvertrag akzeptieren, aktivieren Sie das Kontrollkästchen, mit dem die Vereinbarung akzeptiert wird, und klicken Sie dann auf **Weiter**.

4.  Wählen Sie in **Funktionen auswählen** die Option **Aggregator der Protokollierung des Softwarebestands und Berichtmodul installieren**, und klicken Sie dann auf **Weiter**.

    Weitere Informationen zur Installation des Berichtmoduls finden Sie unter `Publish-SilReport` im Abschnitt **Details zu SIL-Aggregator-Cmdlets**.

5.  Nachdem alle erforderlichen Komponenten überprüft wurden, klicken Sie auf **Weiter**.

6.  Wählen Sie in **Kontotyp auswählen**, entweder **Lokaler Benutzer** oder **gMSA**aus, ganz nach Ihren Vorlieben.

    Wenn Sie die Option für das lokale Benutzerkonto auswählen, wird ein lokaler Benutzer mit einem automatisch generierten, sicheren Kennwort erstellt. Dieses Konto wird für alle SIL-Aggregatordienste und -aufgabenvorgänge auf dem lokalen Server verwendet.  Die Verwendung von gruppenverwalteten Dienstkonten (gMSA) wird empfohlen, wenn der Aggregator Teil der Active Directory-Domäne ist (Windows Server 2012 und höher). Weitere Informationen zu gruppenverwalteten Dienstkonten (gMSA) finden Sie unter [Gruppenverwaltete Dienstkonten: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831782(v=ws.11)).

    -   Die gMSA-Kontooption muss verwendet werden, wenn Sie die Ausführung der SQL Server-Datenbank auf einem vom SIL-Aggregator getrennten Server planen.

    -   Vergessen Sie nicht, den Server neu zu starten, nachdem Sie das Computer Konto der GMSA-fähigen Sicherheitsgruppe in Active Directory hinzugefügt haben.

7.  Geben Sie in **SQL Server auswählen** den SQL-Server ein, auf dem Ihre SQL-Instanz installiert ist, oder **localhost**, wenn sie auf dem lokalen Server installiert ist.

    Es wird nur ein SIL-Aggregator pro SQL Server-Instanz unterstützt.

8.  Wählen Sie den Authentifizierungstyp aus, und klicken Sie auf **SQL überprüfen**.

9. Klicken Sie auf **Weiter**, und wählen Sie dann in **Internet Informationen Services-Serverdetails** eine Portnummer aus, oder übernehmen Sie den Standardwert.

10. Wechseln Sie im Dateisystem zum Speicherort der Datei **PFX**-Datei, und klicken Sie dann auf **Weiter**.

11. Im letzten Bildschirm wird der Installationsstatus angezeigt. Nach erfolgreichem Abschluss klicken Sie auf **Fertig stellen**.

### <a name="uninstalling-sil-aggregator"></a>Deinstallieren des SIL-Aggregators

#### <a name="to-uninstall-software-inventory-logging-aggregator"></a>So deinstallieren Sie den Aggregator der Protokollierung des Softwarebestands

1.  Öffnen Sie die **PowerShell** als Administrator, und geben Sie `Stop-SilAggregator`ein. Wenn die Eingabeaufforderung wieder angezeigt wird, wurde der SIL-Aggregator beendet.

    Standardmäßig verarbeitet der SIL-Aggregator Dateien nach 20 Minuten bzw. nachdem 100 Dateien empfangen wurden.  In großen Umgebungen wird dieses Szenario nie eintreten, aber in kleineren Umgebungen können noch zu verarbeitende Dateien zurückbleiben, bevor der Aggregator beendet werden kann. Verwenden Sie den Parameter `–Force`, wenn diese Dateien und Daten nicht aufbewahrt werden müssen.

2.  Wechseln Sie zur **Systemsteuerung**, klicken Sie auf **Programme und Funktionen**, klicken Sie auf **Programme deinstallieren**, klicken Sie auf **Aggregator der Protokollierung des Softwarebestands**, und klicken Sie dann auf **Deinstallieren**.

    Der Aggregator der Protokollierung des Softwarebestands öffnet ein Fenster, in dem Sie aufgefordert werden, zwischen dem Löschen aller Daten in der Datenbank und dem Behalten aller Daten in der Datenbank auszuwählen. Die Standardauswahl ist die Beibehaltung (falls eine Neuinstallation gewünscht ist, können Sie an die vorhandene Datenbank anfügen, um an der Stelle fortzufahren, wo der Aggregator aufgehört hatte).

3.  Wählen Sie entweder **Behalten** oder **Löschen** aus, und klicken Sie dann auf **Weiter**.

4.  Sobald der Statusbalken vollständig ist, klicken Sie auf **Fertig stellen**.

### <a name="start-using-sil-and-the-sil-aggregator"></a>Mit der Verwendung von SIL und dem SIL-Aggregator beginnen

#### <a name="introduction-to-sil-aggregator-powershell-cmdlets"></a>Einführung in die PowerShell-Cmdlets des SIL-Aggregators
Die folgenden Befehle können als Administrator in der Windows PowerShell-Konsole ausgeführt werden:

|Windows PowerShell-Cmdlet|Funktion|
|-----------------------------|------------|
|`Start-SilAggregator`|Startet alle Dienste und Aufgaben des Aggregators der Protokollierung des Softwarebestands. Dies ist erforderlich, damit der Aggregator Daten über HTTPS von Servern mit gestarteter SIL-Protokollierung empfangen kann.|
|`Stop-SilAggregator`|Beendet alle Dienste und Aufgaben des Aggregators der Protokollierung des Softwarebestands. Wenn sich Aufgaben oder Dienste in der Ausführung befinden, kann es zu einer Verzögerung beim Abschluss dieses Befehls kommen.|
|`Set-SilAggregator`|Ermöglicht dem Administrator die Vornahme von Konfigurationsänderungen am Aggregator der Protokollierung des Softwarebestands.|
|`Add-SilVmHost`|Wird verwendet, um bestimmte Hostnamen oder ein Array von Hostnamen hinzuzufügen, die im regelmäßigen Intervall standardmäßig abgerufen werden sollen \( \) .|
|`Remove-SilVmHost`|Wird verwendet, um bestimmte Hostnamen oder ein Array von Hostnamen zu entfernen, die bzw. das in regelmäßigen Abständen abgerufen werden soll.|
|`Get-SilVMHost`|Wird verwendet, um die Liste der physischen Hosts abzurufen, für die der Aggregator der Protokollierung des Softwarebestands zum Abrufen der laufenden Daten der virtuellen Computerzustände konfiguriert ist.|
|`Get-SILAggregatorData`|Wird verwendet, um Daten aus der Datenbank in die PowerShell-Konsole abzurufen.|
|`Publish-SilReport`|Wird verwendet, um Berichte aus der Datenbank der Protokollierungsdaten des Softwarebestands zu erstellen. **Hinweis:** Die Cubeverarbeitung auf dem Aggregator erfolgt einmal täglich. Somit werden vom Aggregator erfasste Daten erst am folgenden Tag in Berichten angezeigt.|

#### <a name="suggested-order-to-start"></a>Empfohlene Reihenfolge für den Start
Nachdem Sie den Aggregator der Protokollierung des Softwarebestands auf Ihrem Server installiert haben, öffnen Sie die PowerShell als Administrator.

-   Auf Ihrem SIL-Aggregator:

    -   Ausführen von `Start-SilAggregator`

        Dies ist erforderlich, damit der Aggregator Daten aktiv empfängt, die von Ihren Servern, die Sie für die Inventarisierung eingerichtet haben (oder einrichten werden), über HTTPS an ihn weitergeleitet werden. Beachten Sie, dass selbst wenn Sie auf Ihren Servern aktiviert haben, dass sie zuerst an diesen Aggregator weiterleiten, dies in Ordnung ist, da sie ihre Datennutzlasten für bis zu 30 Tage lokal zwischenspeichern. Sobald der Aggregator, seine "targetUri", ausgeführt wird, werden alle zwischengespeicherten Daten gleichzeitig an den Aggregator weitergeleitet, und alle Daten werden verarbeitet.

    -   Ausführen von `Add-SilVMHost`

        Beispiel: `add-silvmhost –vmhostname contoso1 –hostcredential get-credential`

        -   In diesem Beispiel ist **contoso1** der Netzwerkname (oder IP-Adresse) des physischen Hostservers, von dem Ihr Aggregator regelmäßige Aktualisierungen dahingehend abrufen soll, welche virtuellen Computer darauf ausgeführt werden, um diese Daten im zeitlichen Verlauf nachzuverfolgen. „Get-Credential“ fordert den angemeldeten Benutzer auf, ein Konto einzugeben, das zum Abrufen dieses Hosts von diesem Zeitpunkt an verwendet werden soll. Wenn Sie denselben Befehl auf demselben Host noch mal ausführen, können Sie jederzeit das verwendete Konto aktualisieren. Passen Sie auf Kontokennwortänderungen und -abläufe im Laufe der Zeit auf. Wenn sich Anmeldeinformationen ändern oder diese ablaufen, schlägt das Abrufen auf dem Host fehl.

        -   Standardmäßig beginnt das Abrufen stündlich, wobei es eine Stunde nach der Ausführung von `Start-SilAggregator` beginnt bzw. eine Stunde nachdem ein Host der Abrufliste neu hinzugefügt wurde.  Das Abrufintervall kann mithilfe des `Set-SilAggregator cmdlet`s geändert werden.

        -   Dieses Cmdlet erkennt automatisch aus einer vordefinierten Liste mit Optionen (siehe Abschnitt **Details zu SIL-Aggregator-Cmdlets**), welcher HostType und HyperVisorType für den Host korrekt ist, den Sie hinzufügen. Wenn es diese nicht erkennen kann, oder wenn die angegebenen Anmeldeinformationen falsch sind, wird eine Eingabeaufforderung angezeigt. Wenn Sie mit der Eingabe von **J** akzeptieren, wird der Host hinzugefügt und als **Unbekannt** aufgeführt, wird aber nicht abgerufen.

    -   Führen `Set-SilAggregator –AddCertificateThumbprint` Sie "Fingerabdruck Ihres Client Zertifikats" aus.

        Dies ist erforderlich, damit Daten über HTTPS von Windows-Servern mit aktivierter SIL-Protokollierung empfangen werden können. Der Fingerabdruck wird der Liste der Fingerabdrücke hinzugefügt, von denen der Aggregator SIL-Daten akzeptiert. Der SIL-Aggregator ist darauf ausgelegt, gültige Enterprise-Clientauthentifizierungszertifikate zu akzeptieren. Das verwendete Zertifikat muss im Speicher ** \\ LocalMachine\MY (lokaler Computer-> persönlich**) auf dem Server installiert sein, der die Daten weiterleitet.

-   Öffnen Sie auf Ihren zu inventarisierenden Windows-Servern die PowerShell als Administrator, und führen Sie diese Befehle aus:

    -   Ausführen von `Set-SilLogging –TargetUri "https://contososilaggregator" –CertificateThumbprint "your client certificate's thumbprint"`

        -   Dies teilt SIL in Windows Server mit, wohin die Inventardaten zu senden sind und welches Zertifikat für die Authentifizierung verwendet werden soll.

            > [!IMPORTANT]
            > Stellen Sie sicher, dass sich "https://" im targetUri-Wert befindet.

        -   Das Enterprise-Clientzertifikat mit diesem Fingerabdruck muss in **\localmachine\MY** installiert werden, oder Sie müssen **certmgr.msc** verwenden, um das Zertifikat im Speicher **Lokaler Computer -> Persönlich** zu installieren.

            > [!IMPORTANT]
            > Wenn diese Werte nicht richtig sind oder das Zertifikat nicht im richtigen Speicher installiert (oder ungültig) ist, schlagen Weiterleitungen an das Ziel fehl, wenn die SIL-Protokollierung gestartet wird. Daten werden für bis zu 30 Tage lang lokal zwischengespeichert.

    -   Ausführen von `Start-SilLogging`

        Dies startet die SIL-Protokollierung. Jede Stunde, in zufälligen Intervallen innerhalb dieser Stunde, leitet SIL seine Inventardaten an den mithilfe des Parameters `–targeturi` angegebenen Aggregator weiter. Die erste Weiterleitung umfasst einen vollständigen Satz von Daten. Jede nachfolgende weiterleiten ist eher ein "Takt", bei dem nur Daten identifiziert werden, die sich nicht geändert haben. Gibt es eine Änderung an dem Dataset, wird ein weiterer vollständiger Satz von Daten weitergeleitet.

    -   Ausführen von `Publish-SilData`

        -   Bei der ersten Aktivierung von SIL für die Protokollierung ist dieser Schritt optional.

        -   Hierbei handelt es sich um eine manuelle, einmalige Weiterleitung eines vollständigen Satzes von Daten.

        -   Wenn die SIL Protokollierung schon seit einiger Zeit gestartet ist und ein neuer SIL-Aggregator mithilfe von `Set-SilLogging` festgelegt wird, ist es erforderlich, dieses Cmdlet einmalig auszuführen, um einen vollständigen Satz von Daten an den neuen Aggregator zu senden.

Nachdem Sie diese Schritte ausgeführt haben, um physische Hosts hinzuzufügen, auf denen virtuelle Windows Server-Computer ausgeführt werden UND nachdem Sie die Protokollierung des Softwarebestands (bzw. SIL-Protokollierung) in diesen Windows-Servern aktiviert haben, können Sie jederzeit `Publish-SilReport –OpenReport` auf dem SIL-Aggregator ausführen (erfordert Excel 2013). Beachten Sie jedoch, dass der SQL Server Analysis Services-Cube einmal täglich eine Verarbeitung durchführt, sodass Daten nicht am selben Tag in Berichten verfügbar sind.

## <a name="architectural-overview"></a>Übersicht über die Architektur
SIL arbeitet sowohl im Push- als auch im Pull-Modus und besteht aus zwei Komponenten, die parallel arbeiten: die Funktion „Protokollierung des Softwarebestands (SIL)“ in Windows Server und die herunterladbare MSI-Datei des Aggregators der Protokollierung des Softwarebestands. Die zu inventarisierenden Server senden mithilfe von SIL Inventardaten über HTTPS an den SIL-Aggregator (Push; jede Stunde zu zufälligen Zeitpunkten innerhalb jeder Stunde). Der Aggregator wiederum ruft oder fragt die physischen Hypervisor-Hosts ab (Pull), um stündlich Hardwareinventardaten abzurufen. Beide Funktionen, sowohl Push als auch Pull, müssen ordnungsgemäß konfiguriert sein, um die vollständige Funktionalität von SIL zu ermöglichen. Sie können in beliebiger Reihenfolge konfiguriert werden. Allerdings erfolgt die Cubeverarbeitung auf dem Aggregator einmal täglich, sodass vom Aggregator per Push oder Pull erfasste Daten erst am folgenden Tag in Berichten angezeigt werden.

![Aggregator-Diagramm der Protokollierung des Software Bestands](../media/software-inventory-logging/SILA_Architecture.png)

> [!IMPORTANT]
> Bei Verwendung dieser Software werden keine Daten an Microsoft gesendet.

## <a name="enable-sil-on-multiple-servers"></a>Aktivieren von SIL auf mehrerer Servern
Es gibt mehrere Möglichkeiten, um SIL in einer verteilten Serverinfrastruktur, beispielsweise in einer privaten Cloud aus virtuellen Computern, zu aktivieren.  Im Folgenden finden Sie ein Beispiel für eine Möglichkeit zum Einrichten von Windows Server-Images, damit diese automatisch Inventardaten an einen SIL-Aggregator senden, wenn sie im Netzwerk zum ersten Mal gestartet werden.

Führen Sie auf jeder ausgeführten virtuellen Maschine bzw. physischem Computer/Gerät mit installiertem Windows Server(siehe Abschnitt **Voraussetzungen**) folgende Cmdlets in der PowerShell-Konsole als Administrator aus:

Sie benötigen ein gültiges SSL-Clientzertifikat im PFX-Format, um diese Schritte auszuführen.  Der Fingerabdruck dieses Zertifikats muss mithilfe des Cmdlets `Set-SILAggregator –AddCertificateThumbprint` Ihrem SIL-Aggregator hinzugefügt werden. Dieses Clientzertifikat muss nicht mit dem Namen Ihres SIL-Aggregators übereinstimmen.

-   `$secpasswd = ConvertTo-SecureString "`**<password for the account with permissions to the network location holding your client pfx file>**`" -AsPlainText –Force`

-   `$mycreds = New-Object System.Management.Automation.PSCredential ("`**<user account with permissions to the network location holding your client  pfx file>**`", $secpasswd)`

-   `$driveLetters = ([int][char]'C')..([int][char]'Z') | % {[char]$_}`

-   `$occupiedDriveLetters = Get-Volume | % DriveLetter`

-   `$availableDriveLetters = $driveLetters | ? {$occupiedDriveLetters -notcontains $_}`

-   `$firstAvailableDriveLetter = $availableDriveLetters[0]`

-   `New-PSDrive -Name $firstAvailableDriveLetter -PSProvider filesystem -root`** < \\ server\pfad zur Freigabe, die Ihre PFX-Zertifikat Datei enthält>**`-credential $mycreds`

-   `Copy-Item ${firstAvailableDriveLetter}:\`**<certificename. pfx-Datei im Verzeichnis des neuen Laufwerks> c:\<location of your choice>**

-   `Remove-PSDrive –Name $firstAvailableDriveLetter`

-   `$mypwd = ConvertTo-SecureString -String "`**<password for the certificate pfx file>**`" -Force –AsPlainText`

-   `Import-PfxCertificate -FilePath c:\`**<Location \\ certifiupename. pfx>**`cert:\localMachine\my -Password $mypwd`

-   `Set-sillogging –targeturi "https://`**<machinename of your SIL Aggregator>** `–certificatethumbprint`

> [!NOTE]
> Verwenden Sie den Zertifikat Fingerabdruck aus der PFX-Client Datei, und fügen Sie dem SIL-Aggregator mithilfe des Cmdlets **Set-silaggregator "-addcertifikatethrebprint"** hinzu.

-   `Start-sillogging`

Wann immer ein SIL-Aggregator nicht erreicht werden kann, werden SIL-Inventardaten SIL lokal für bis zu 30 Tage auf Windows-Servern zwischengespeichert. Nachdem ein erfolgreicher Push an den Aggregator erfolgt ist, werden alle zwischengespeicherten Daten weitergeleitet.

Fügen Sie der oben angeführten Liste `Publish-SilData` hinzu, wenn SIL-Daten nach erfolgreichen Pushvorgängen an den alten Aggregator an einen neuen SIL-Aggregator per Push übertragen werden (hierdurch wird ein vollständiger Ergänzungssatz von SIL-Daten gesendet, die der neue Aggregator für diesen Computer benötigt).

## <a name="software-inventory-logging-aggregator-reports"></a>Berichte des Aggregators der Protokollierung des Softwarebestands
![Abbildung des Aggregator-Berichts des Aggregators der Software Inventur](../media/software-inventory-logging/SILA_Report.png)

### <a name="cube-processing"></a>Cubeverarbeitung
Auf einem Aggregator der Protokollierung des Softwarebestands wird der SQL Server Analysis Services-Cube einmal täglich um 3:00:00 Uhr lokale Systemzeit verarbeitet. Berichte enthalten alle bis zu diesem Zeitpunkt erfassten Daten, aber keine Daten, die nach diesem Zeitraum am selben Tag liegen.

### <a name="high-water-mark"></a>Obere Grenze
Ein grundlegender Aspekt der Berichte des Aggregators der Protokollierung des Software Bestands ist die Erfassung, was häufig als "obere Grenze" von gleichzeitig auszulaufenden Windows-Servern bezeichnet wird. Dies gilt für die Anzahl von Windows Server und System Center in diesen Berichten. Bei Windows Server hat jeder einzelne physische Host einen Zeitpunkt (unabhängig vom BS-Typ auf dem Host) im Verlauf eines Monats, wenn die meisten virtuellen Windows Server-Computer gleichzeitig ausgeführt werden. Dies ist die obere Grenze für den Monat. Zusätzlich gibt es für System Center einen Zeitpunkt im Monat, wenn die meisten verwalteten Windows-Server pro physischem Host gleichzeitig ausgeführt werden (ein verwalteter Server wird dadurch gekennzeichnet, dass mindestens ein System Center-Agent vorhanden ist) gleichzeitig ausgeführt werden. Nur die jüngste obere Grenze für jeden physischen Host wird im Bericht angezeigt. Es werden keine Daten angezeigt, die nach der oberen Grenze liegen. Und es ist davon auszugehen, dass die Anzahl virtueller Windows Server-Computer (WS-Registerkarten) oder verwalteter virtueller Windows Server-Computer (SC Registerkarten) nach diesem Punkt unter die obere Grenze gefallen ist. Diese Art der Nachverfolgung und Darstellung der Verwendung soll bei der Kapazitätsplanung sowie bei der Ausrichtung an den Lizenzmodellen für diese Produkte helfen.

Auf SQL-bezogenen Registerkarten im Bericht werden SQL Server Installationen kumulativ gezählt. nicht nach hig-Wasserzeichen. Summen sind eine laufende Zählung der SQL Server-Installationen.

> [!NOTE]
> Die Verwendung der Protokollierung des Softwarebestands ersetzt nicht die Verpflichtung, die Verwendung von Microsoft-Software gemäß den geltenden Lizenzbedingungen genau zu melden.

### <a name="poll-date-time"></a>Datum/Uhrzeit des Abrufs
Bei Verwendung des Aggregators der Protokollierung des Softwarebestands ist es wichtig zu verstehen, dass die Aggregation für die Zählungen der oberen Grenze abrufgesteuert ist. Mit anderen Worten heißt dies, dass eine obere Grenze nur durch einen Abruf des zugrunde liegenden physischen Hosts erfasst werden kann. Daher sind die Anzahl der oberen Grenzwerte direkt mit einem entsprechenden "Abrufdatum/-Zeit" verknüpft. Zwar kann das Abrufintervall angepasst werden, doch die Zuverlässigkeit der erfassten oberen Grenzen wird beeinträchtigt, wenn ein höherer Intervallwert verwendet wird. Je höher das Intervall, desto weniger repräsentativ sind die Daten für die tatsächliche Verwendung.

### <a name="reports-are-month-by-month"></a>Berichte sind „monatlich“ aufgebaut
Alle Berichte, sogar Jahresberichte, werden als monatliche Berichte dargestellt. Obere Grenzen, Summen und Computerdaten werden alle am Anfang jedes Kalendermonats zurückgesetzt.

Berichtsdaten, die u. a. vom Wechsel zu einem neuen Monat betroffen sind:

-   Alle oberen Grenzen für alle Hosts werden zu Beginn eines neuen Monats zurückgesetzt.

-   Wenn der Aggregator mindestens eine vollständige Nutzlast von einem virtuellen Computer (über HTTPS) empfängt, jedoch keine Takte mehr empfängt, setzen alle Abrufe des zugrunde liegenden Hosts innerhalb dieses Monats die Zuordnung zwischen Host, virtuellem Computer und Daten des virtuellen Computers voraus, weil dieser virtuelle Computer im Verlauf des Monats ausgeführt oder beendet wird. Am Anfang des neuen Monats wird diese Zuordnung gelöscht, bis entweder eine vollständige Nutzlast oder ein Takt von diesem virtuellen Computer empfangen wird.

### <a name="additional-notes-on-report-behavior"></a>Zusätzliche Hinweise zum Verhalten von Berichten

-   Zusammenfassungsregisterkarten sollen Kurzübersichtslisten des Inventars sein. Hosts und ihre virtuellen Computer werden in derselben Spalte aufgeführt.

-   Ignoriert alle Werte, die grau oder Dim sind. Dabei handelt es sich um Artefakte der Berichterstellung aus dem SSAS-Cube.

-   Wenn ein virtueller Computer mit "Unbekanntes Betriebssystem" aufgelistet ist, bedeutet dies, dass der Aggregator keine vollständige Daten Nutzlast von diesem virtuellen Computer über SIL über HTTPS erhalten hat.

-   Virtuelle Computer, die unter "Unbekannter Host" aufgeführt sind, sind virtuelle Windows Server-Computer, die erfolgreich Inventur Daten über HTTPS an den Aggregator weiterleiten, der Aggregator aber den zugrunde liegenden Host für diesen virtuellen Computer nicht aktiv oder erfolgreich abfragt Zählungen sind immer null für diese Einträge, da der zugrunde liegenden Host unbekannt ist. Verwenden Sie das Cmdlet `Add-SilVMHost` mit den richtigen Anmeldeinformationen, um den Host (oder alle Hosts) dem SIL-Aggregator für das Abrufen hinzuzufügen. Nach erfolgreichem Abruf werden die Daten der virtuellen Computer und die Hostdaten im weiteren Verlauf in Berichten zugeordnet.

-   Alle Datums- und Zeitangaben sind lokale Systemzeiten und beziehen sich auf das lokale Gebietsschema des SIL-Aggregator. Dies schließt von SIL-aktivierten Systemen über HTTPS empfangene Inventardaten ein. Wenn diese Dateien verarbeitet werden (nicht später als 20 Minuten nach dem Empfang), werden die Daten mit der lokalen Systemzeit in die Datenbank eingefügt.

-   "SIL-Aggregator" wird auf jedem Server Computer angegeben, auf dem der Aggregator der Protokollierung des Software Bestands installiert ist.

-   Wenn sich bei einem physischen Host die Anzahl der Prozessoren oder die Menge des physischen Arbeitsspeichers ändert, wird im Bericht eine neue Zeile zusammen mit der alten Zeile angezeigt. Für die alte Zeile werden keine Aktualisierungen mehr abgerufen, dafür wird aber mit dem Abrufen von Aktualisierungen für die neue Zeile begonnen, als ob es sich um einen neu hinzugefügten Host handelte.

-   Auf den Registerkarten **Zusammenfassung** und **Detail** geben die Summen, die in den Spalten für „Gleichzeitig ausgeführte Windows-Server“ und „Verwaltete Windows-Server“ aufgeführt werden, eine Summe aller oberen Grenzen für alle unten aufgeführten Hosts an. Hierzu gehören Windows-Server, die keine Hypervisor-Hosts sind und auf denen keine virtuellen Computer ausgeführt werden, sowie Server, auf denen virtuelle Computer ausgeführt werden, die aber "unbekannt" sind, da keine Daten aus dem virtuellen Computer von SIL über HTTPS empfangen werden. Diese werden aus Gründen der Bequemlichkeit summiert.

-   Im Abschnitt **SQL Server** der Registerkarte **Dashboard** ist die Summe der SQL Server-Installationen eine Zusammenfassung aller Editionssummen im Dashboard.  Dies kann zu einer Diskrepanz mit der auf der Registerkarte **SQL-Detail** angezeigten Summe führen, wenn mehrere Editionen von SQL auf einem einzelnen Server installiert sind.  Im Dashboard würden diese auf jedem Server getrennt gezählt, was auf der Registerkarte **Detail** nicht der Fall wäre.  Mehrere SQL-Editionen, die auf einem Windows-Server installiert sind, werden gemäß den Lizenzbestimmungen immer als eine gezählt.

-   Im Abschnitt **Windows Server** der Registerkarte **Dashboard** umfassen die Zeilen für **Weitere Hypervisor-Hosts** und **Hypervisor-Hosts gesamt** physische Windows Server-Hosts, auf denen Hyper-V eventuell ausgeführt oder auch NICHT wird.

### <a name="column-descriptions"></a>Spaltenbeschreibungen
Im Folgenden finden Sie Beschreibungen der einzelnen Spalten auf der Registerkarte **Windows Server-Detail** des Excel-basierten Berichts, der vom SIL-Aggregator erstellt wird. Weitere Datenregisterkarten sind entweder mit diesen Spalten identisch oder eine Teilmenge davon. Die einzige Ausnahme wäre die "Installations Anzahl" auf den SQL Server Registerkarten (siehe obere **Grenze** ).

|Spaltenüberschrift|BESCHREIBUNG|
|-----------------|---------------|
|Kalendermonat|Daten in Berichten werden nach Monat gruppiert, der jüngste zuerst. Daten innerhalb des Monats werden in keiner bestimmten Reihenfolge aufgeführt.|
|Hostname|Netzwerkname oder FQDN des physischen Hosts, der vom SIL-Aggregator erfolgreich abgerufen wird.<p>Verwenden Sie das Cmdlet „Get-SilVMHost“, um Hosts zu suchen, die hinzugefügt wurden, aber nicht oder nicht mehr erfolgreich abgerufen werden. Der letzte erfolgreiche Abruf wird angezeigt.|
|Hosttyp|Betriebssystemhersteller auf dem physischen Host.|
|Hypervisor Type (Hypervisor-Typ)|Hypervisor-Hersteller auf dem physischen Host.|
|Processor Manufacturer (Prozessorhersteller)|Hersteller der Prozessoren auf dem physischen Host.|
|Processor Model (Prozessormodell)|Modell der Prozessoren auf dem physischen Host.|
|Is Hyper Threading Enabled? (Ist Hyperthreading aktiviert?)|Wird entweder als „True“ oder „False“ angezeigt, abhängig davon, ob Hyperthreading auf den Prozessoren des physischen Hosts aktiviert ist.|
|VM-Name|Der Netzwerkname oder FQDN des virtuellen Windows Server-Computers. Wenn der Aggregator keine Daten von diesem Computer über HTTPS erhalten hat, wird der Anzeigename des virtuellen Computers im Hypervisor aufgeführt.|
|Simultaneously Running Windows Server VMs by host (Gleichzeitig ausgeführte virtuelle Windows Server-Computer nach Host)|Anzahl der gleichzeitig ausgeführten virtuellen Windows Server-Computer auf dem Host. Die höchste Zahl im Monat für diesen Host ist die obere Grenze, die zu diesem Zeitpunkt erfasst und aufgeführt wird.<p>Siehe im Abschnitt **Obere Grenze** in dieser Dokumentation.<p>Physische Hosts mit installiertem Windows Server oder mit installiertem Windows Server und ohne bekannte, ausgeführte virtuelle Windows Server-Computer werden immer als eins gezählt. Wenn mindestens ein bekannter, virtueller Windows Server-Computer auf dem Host und Windows Server auf dem Host selbst ausgeführt wird, ist das Hostbetriebssystem in der Zählung nicht enthalten.|
|Physical Processor Count (Anzahl physische Prozessoren)|Die Anzahl der physischen Prozessoren, die auf dem physischen Host installiert sind.|
|Physical Core Count (Anzahl physische Kerne)|Die Anzahl der physischen Prozessorkerne, die auf dem physischen Host installiert sind.|
|Virtual Processor Count (Anzahl virtuelle Prozessoren)|Die Anzahl virtueller Prozessoren, die Windows innerhalb des virtuellen Computers erkennt. Dieser Wert stammt nur aus Daten, die über HTTPS mithilfe von SIL in einem Windows Server weitergeleitet wurden.|
|Datum/Uhrzeit des Abrufs|Datum und Uhrzeit des letzten oberen Grenzwertpunkts der virtuellen Windows Server-Computer, die gleichzeitig auf diesem physischen Host ausgeführt werden.<p>Siehe im Abschnitt **Datum/Uhrzeit des Abrufs** in dieser Dokumentation.|
|VM Last Seen Date Time (Datum/Uhrzeit der letzten Anzeige des virtuellen Computers)|Datum und Uhrzeit, zu dem der Aggregator zuletzt Inventardaten über HTTPS von diesem virtuellen Windows Server-Computer erhalten hat.|
|Host Last Seen Date Time (Datum/Uhrzeit der letzten Anzeige des Hosts)|Datum und Uhrzeit, zu dem der Aggregator zuletzt Inventardaten über HTTPS von diesem physischen Windows Server-Host erhalten hat.<p>Hierbei wird das Vorhandensein physischer Hosts, auf denen Windows Server und Hyper-V ausgeführt wird, unterstützt, um SIL zu aktivieren und Inventardaten über HTTPS an einen SIL-Aggregator weiterzuleiten.|

## <a name="sil-aggregator-cmdlets-detail"></a>Details zu SIL-Aggregator-Cmdlets
Im Folgenden finden Sie Detailinformationen zu den Cmdlets des SIL-Aggregators. Die vollständigen Cmdlet-Dokumentation finden Sie unter: [PowerShell-Cmdlets des SIL-Aggregators](/previous-versions/windows/powershell-scripting/mt548455(v=wps.640))

### <a name="publish-silreport"></a>Publish-SilReport

-   Mit diesem Cmdlet, das unverändert verwendet wird, wird ein Bericht zur Protokollierung des Software Bestands erstellt und im Verzeichnis "Dokumente" des angemeldeten Benutzers abgelegt (auf dem Computer, auf dem das Cmdlet ausgeführt wird, ist Excel 2013 erforderlich).

-   Bei Verwendung mit dem `–OpenReport`-Parameter erstellt es den Bericht und öffnet ihn zur Anzeige in Excel.

-   Beachten Sie bei der Installation des SIL-Aggregators, dass es eine Option gibt, um nur das Berichtmodul zu installieren. Es ist möglich, das Berichtmodul auf einem Windows-Clientbetriebssystem wie Windows 8.1 oder Windows 10 zu installieren. Dies ermöglicht einem Thin Client, z. B. einem Laptop oder Tablet, das Herstellen einer Verbindung mit einem SIL-Aggregator-Datenbankserver, um SIL-Berichte direkt zu veröffentlichen.

    -   Im folgenden Beispiel wird zur Eingabe der zu verwendenden Anmeldeinformationen aufgefordert, eine Verbindung mit einem SIL-Aggregator-Datenbankserver namens „SILContoso“ hergestellt und ein SIL-Bericht auf dem lokalen Computer erstellt und geöffnet.

        `Publish-SilReport -DBServerName "SILContoso" -DBServerCredential Get-Credential –OpenReport`

    -   Vor dem ersten Herstellen einer Verbindung müssen Sie in den meisten Fällen einen Port in der Firewall auf dem SIL-Aggregator-Datenbankserver öffnen, um Verbindungen zuzulassen. IT-Experten können dies im Voraus einrichten, um Ihren Finanz-Controllern oder anderen Inventar-Managern den Zugriff zu gewähren, damit sie eigene Berichte erstellen können. Die hierfür notwendigen Schritte finden Sie unter dem unten stehenden Link. Ein typischer Standardport für SQL Server Analysis Services ist 2383.

### <a name="add-silvmhost"></a>Add-SilVMHost
Die folgenden Hosttypen und Hypervisor-Versionen werden unterstützt, wenn das `Add-SilVMHost` -Cmdlet verwendet wird. Beachten Sie, dass es nicht erforderlich ist, diese anzugeben. Das `Add-SilVMHost`-Cmdlet erkennt eine unterstützte Kombination automatisch. Wenn es eine solche nicht erkennen kann, oder wenn die angegebenen Anmeldeinformationen falsch sind, wird eine Eingabeaufforderung angezeigt. Wenn der Benutzer mit einem "Y"-Eintrag akzeptiert, wird der Host hinzugefügt, aber nicht abgerufen. Er wird als "unbekannt" hinzugefügt.

|Hypervisor-Version|SIL-Aggregator         HostType-Wert|SIL-Aggregator HypervisorType-Wert|
|----------------------|-----------------------------------------|---------------------------------------|
|Windows Server 2012 R2|Windows|HyperV|
|VMware 5.5|VMware|Esxi|
|Xen 4.x|Ubuntu, OpenSuse oder CentOS|Xen|
|XenServer 6.2|Citrix|XenServer|
|KVM|Ubuntu, OpenSuse oder CentOS|KVM|

Andere Versionen und Typen dieser Hypervisor-Plattformen können möglicherweise ebenfalls funktionieren.  Im Lieferumfang des SIL-Aggregators ist die unten aufgeführte sshnet-Version enthalten.  Diese wird für die Kommunikation mit Linux-basierten Virtualisierungsplattformen verwendet.

<pre>sshnet 2014.4.6-beta1
https://sshnet.codeplex.com/releases/view/120504
Copyright (c) 2010, RENCI</pre>

### <a name="get-silaggregator"></a>Get-SilAggregator
`Get-SilAggregator` stellt Konfigurationsinformationen für Ihre Aggregatoranwendung der Protokollierung des Softwarebestands bereit. Die folgende Beispielausgabe zeigt an:

-   Anwendung wird ausgeführt.

-   Abrufintervall ist stündlich (kann in Stundeninkrementen geändert werden).

-   Startzeit des Abrufs

-   Ziel-URI, den andere Computer für das Weiterleiten von Daten an diesen Aggregator festlegen sollten.

-   Zertifikatfingerabdrücke, von denen dieser Aggregator SIL-Daten akzeptiert.

-   Bei der Installation angegebener Kontotyp

    `PS C:\Windows\system32> Get-SilAggregator`

    ``

    `State          : Running HostPollIntervalInHours : Every 1 Hour(s)`

    `PollStartTime      : 8/24/2015 5:07:33 AM`

    `TargetURI        : https://SilContoso`

    `CertificateThumbprint  : 3efc6b8ce7d5eefba5107ede9d1caca550417452, 2dc4ea8bfb64b1246a8c1ffa1b701cd1042a3412`

    `UserProfile       : Local`

### <a name="set-silaggregator"></a>Set-SilAggregator
Mit dem `Set-SilAggregator`-Cmdlet können Sie Folgendes:

-   Ändern des stündlichen Intervalls, in dem der Abruf erfolgt.

-   Ändern von Startdatum und Startzeit für den Beginn des Abrufs zum angegebenen Intervall.

-   Hinzufügen oder Entfernen von Zertifikatfingerabdrücken, von denen der SIL-Aggregator Daten akzeptiert bzw. denen er Daten zuordnet.

### <a name="get-aggregatordata"></a>Get-AggregatorData

-   Bei Verwendung ohne Parameter zeigt dieses Cmdlet den Inhalt der Registerkarte „Windows Server-Detail“ eines SIL-Aggregator-Excel-Berichts an.

-   Wenn dieses Cmdlet mit Parametern verwendet wird, ruft es Daten direkt aus der Datenbank ab, die der Unterstützung bei benutzerdefinierten Verwendungen der SIL-Gesamtlösung dienen sollen.

-   Beachten Sie, dass die Parameter `–StartTime` und `–Endtime` Berichtdaten aus dem ersten des Monats des Startdatums und dem letzten des Monats des Enddatums anzeigen.

![Bild des abgeschlossenen Cmdlets "Get-aggregatordata"](../media/software-inventory-logging/SILA_Get-SILAggregator.png)

### <a name="get-silvmhost"></a>Get-SilVMHost

-   Dieses Cmdlet gibt die Liste der physischen Hosts aus, für deren Abruf der SIL.-Aggregator konfiguriert ist, Datum und Uhrzeit des jüngsten erfolgreichen Abrufs sowie den „HostType“ (oder BS-Hersteller) und den „HypervisorType“ (Hypervisor-Hersteller). Weitere Informationen zu „HostType“ und „HypervisorType“ finden Sie in den Details zu „Add-SilVMHost“.

    Wenn ein Host weder Abfragedatum noch -uhrzeit, aber einen unterstützten „HostType“ und „HypervisorType“ besitzt, bedeutet dies, dass der Abruf noch nicht begonnen hat oder noch nicht erfolgreich war.

-   Dieses Cmdlet listet außerdem alle Hostnamen auf, die mittels der Daten, die von virtuellen Computern selbst stammen (falls sie von dem virtuellen Computer verfügbar waren), hinzugefügt wurden Diese werden zwar in der Liste angezeigt, besitzen aber weder „HostType“ noch „HypervisorType“. Diese Daten können bei der Zuordnung von virtuellen Computern und Hosts helfen, die möglicherweise nicht für den Abruf eingerichtet sind.

-   Mithilfe der Parameter `–StartTime` und`–EndTime` können Ihnen dabei helfen zu verstehen, wann Hosts zum ersten Mal hinzugefügt oder zuletzt abgerufen wurden.

### <a name="remove-silvmhost"></a>Remove-SilVMHost

-   Dieses Cmdlet entfernt jeden Host aus der Liste der abzufragenden Hosts. Wenn ein Host entfernt wird, ist es möglich, dass ein virtueller Computer auf dem Host den Host der Liste erneut hinzufügt, wobei der Host aber nicht mit den richtigen Anmeldeinformationen abgerufen wird, die mithilfe des `Add-SilVMHost`-Cmdlets angegeben werden.

-   Wenn ein Host entfernt wird, wird er nicht mehr abgefragt, aber nicht aus Berichten entfernt. Da das Abrufen eingestellt wird, ist der Host in Berichten der folgenden Monate nicht mehr vorhanden.

-   Verwenden Sie die Parameter `–StartTime` und`–EndTime` einzeln, um beim Entfernen von Gruppen von Hosts zu helfen, die bis zu einem oder ab einem bestimmten Datum erfolgreich abgerufen wurden.

## <a name="avoid-these-errors-and-issues-with-sil-and-sil-aggregator-troubleshooting-guide"></a>Vermeiden dieser Fehler und Probleme mit SIL und SIL Aggregator (Handbuch zur Problembehandlung)

-   Zu überprüfende Dinge, wenn eins der Cmdlets `SilLogging` und `Publish-Sildata` fehlschlägt:

    -   Stellen Sie sicher, dass der **targetUri** den Wert **https://** im Eintrag enthält.

    -   Stellen Sie sicher, dass alle erforderlichen Updates für Windows Server installiert sind (siehe „Voraussetzungen für SIL“).  Eine schnelle Möglichkeit zum Überprüfen besteht darin, diese mithilfe des folgenden Cmdlets zu suchen:   `Get-SilWindowsUpdate *3060*, *3000*`

    -   Stellen Sie sicher, dass das zur Authentifizierung bei dem Aggregator verwendete Zertifikat im richtigen Speicher auf dem lokalen Server installiert ist, der mithilfe von „SilLogging“ inventarisiert werden soll (siehe im Abschnitt „Erste Schritte“).

    -   Stellen Sie auf dem SIL-Aggregator sicher, dass der Zertifikatfingerabdruck des für die Authentifizierung bei dem Aggregator verwendeten Zertifikats der Liste mithilfe des Cmdlets `Set-SilAggregator –AddCertificateThumbprint` hinzugefügt wurde (siehe im Abschnitt „Erste Schritte“).

    -   Bei Verwendung von Enterprise-Zertifikaten überprüfen Sie, ob der Server mit aktivierter SIL der Domäne beigetreten ist, für die das Zertifikat erstellt wurde, bzw. anderweitig bei einer Stammzertifizierungsstelle überprüfbar ist. Wenn ein Zertifikat auf dem lokalen Computer, der versucht, Daten an den Aggregator weiterzuleiten oder per Push zu übertragen, nicht vertrauenswürdig ist, schlägt diese Aktion mit einem Fehler fehl.

    -   Wenn alle oben genannten Punkte überprüft wurden, können Sie überprüfen, ob das zur Installation des SIL-Aggregators verwendete Zertifikat fehlerfrei ist und mit dem Namen des SIL-Aggregatorservers selbst übereinstimmt (dieser Schritt ist nicht erforderlich, wenn andere Computer erfolgreich an denselben SIL-Aggregator weiterleiten).

    -   Sie können den folgenden Speicherort auf zwischengespeicherte SIL-Dateien auf dem Server überprüfen, der den Forward/Push-Vorgang versucht, \Windows\System32 \\ Logfiles \\ SIL. Wenn `SilLogging` gestartet wurde und schon länger als eine Stunde ausgeführt wird, oder wenn `Publish-SilData` vor Kurzem ausgeführt wurde und keine Dateien in diesem Verzeichnis vorhanden sind, dann war die Protokollierung auf dem Aggregator erfolgreich.

-   Vergewissern Sie sich, dass der angemeldete Benutzer über Zugriff auf die SQL-Datenbank und die Analysis Services verfügt.

    -   Dies ist erforderlich für die Installation des SIL-Aggregators.

    -   Dies ist erforderlich, wenn Sie PowerShell Remote zum Verwalten des SIL-Aggregators verwenden.

-   Beim Veröffentlichen von SIL-Aggregatorberichten von einem Clientdesktop-Betriebssystem aus:

    -   Verwenden Sie die Option, mit der nur das Berichtmodul installiert wird, auf Ihrem Windows-Client (8.1/10).

    -   Wenn bei dem Versuch, einen Bericht mithilfe von PowerShell remote zu erstellen, Probleme auftreten, müssen Sie wahrscheinlich einen Firewallport auf dem SIL-Aggregator öffnen lassen, mit dem Sie eine Verbindung herstellen möchten (siehe im Abschnitt „Details zu SIL-Aggregator-Cmdlets“ unter dem Cmdlet `Publish-SilReport` ).

-   Bei Verwendung der gMSA-Option:

    -   Vergessen Sie nicht, den Server neu zu starten, nachdem Sie ihn mit der GMSA-fähigen Computergruppe in Active Directory hinzufügen.

    -   Verwenden Sie bei der Installation bei der Eingabe von Domäne \ Benutzer nicht die voll qualifizierte Domäne. Verwenden Sie z. b. **meineDomäne \ gmsaaccount**. Geben Sie **mydomain nicht ein. <i></i> com\gmsaaccount**.

-   Bei Verwendung von Windows Management Framework in Ihrer Umgebung:

    -   Stellen Sie sicher, dass auf den Servern, auf denen Sila installiert ist, WMF 5,1 nicht installiert ist.  Es ist möglich, im Ereignisprotokoll einen Fehler im Zusammenhang mit der DLL **"mpunits.dll"** zu finden.  Dadurch wird der ordnungsgemäße Betrieb verhindert.  Sila erfordert nur WMF 4,0.

## <a name="managing-sil-over-time"></a>Verwalten von SIL im zeitlichen Verlauf

### <a name="uninstallreinstall-sil-aggregator"></a>Deinstallieren/Neuinstallieren des SIL-Aggregators
Falls es erforderlich werden sollte, den SIL-Aggregator zu deinstallieren und neu zu installieren, können Sie dies durchführen, ohne dabei vorhandene oder historische Inventardaten zu verlieren. Führen Sie einfach eine Deinstallation durch (befolgen Sie die Schritte in dieser Dokumentation), und aktivieren Sie die Option zum Beibehalten der Datenbank der Protokollierung des Softwarebestands. Installieren Sie dann den SIL-Aggregator neu (befolgen Sie die Schritte in dieser Dokumentation), und aktivieren Sie die Option zum Anfügen an eine vorhandene Datenbank.

Nach dem Ausführen dieses Vorgangs ist es notwendig, die Anmeldeinformationen mithilfe des Cmdlets `Add-SilVMHost` auf allen Hosts zu aktualisieren, die zuvor vom SIL-Aggregator abgerufen wurden (vorausgesetzt, dass es gewünscht ist, das Sammeln von Daten von diesen Hosts fortzusetzen). Darüber hinaus ist es zur Vermeidung doppelter Einträge für denselben Host in Berichten notwendig, Hosts für den Abruf unter Verwendung derselben Netzwerkadresse, mit der sie ursprünglich hinzugefügt wurden, erneut hinzuzufügen. Im Folgenden finden Sie die drei unterstützten „vmhostname“-Typen, die zum Hinzufügen eines Hosts mithilfe des Cmdlets `Add-SilVMHost` verwendet werden können:

-   IP-Adresse

-   Vollqualifizierter Domänennamen (FQDN)

-   NetBIOS-Name

### <a name="changing-sil-aggregators"></a>Ändern des SIL-Aggregators
Wenn Sie die Inventarisierung von Servern in Ihrer Umgebung mit einem anderen SIL-Aggregator starten möchten, verwenden Sie einfach das SIL-Cmdlet auf diesen Servern, um den „targeturi“ (und ggf. den Zertifikatfingerabdruck) zu ändern, `Set-SilLogging –TargetUri`. Beachten Sie, dass es nach der Durchführung dieses Vorgangs notwendig ist, das Cmdlet `Publish-SilData` mindestens einmal zu verwenden, um ein vollständiges Inventar an den neu angegebenen SIL-Aggregator weiterzuleiten.

### <a name="changing-or-updating-certificates"></a>Ändern oder Aktualisieren von Zertifikaten
**WICHTIGE SCHRITTE ZUR VERMEIDUNG VON DATENVERLUSTEN:** Wenn es erforderlich ist, das Zertifikat zu ändern, das Server zum Weiterleiten von Daten an einen SIL-Aggregator verwenden, der Zielaggregator bleibt aber derselbe, gehen Sie folgendermaßen vor, um während des Übergangs zu dem Aggregator potenzielle Datenverluste zu vermeiden:

-   Verwenden Sie auf dem SIL-Aggregator das Cmdlet `Set-SilAggregator –AddCertificateThumbprint`, um dem SIL-Aggregator die neuen Fingerabdrücke hinzuzufügen.

-   Installieren Sie auf ALLEN Servern, die Daten weiterleiten, das neue, zu verwendende Zertifikat mit Ihrer bevorzugten Methode in **\LOCALMACHINE\MY**.

-   Verwenden Sie auf allen Servern, die Daten weiterleiten, das Cmdlet `Set-SilLogging –CertificateThumbprint` , um auf den Fingerabdruck des neuen Zertifikats zu aktualisieren.

-   **KRITISCH: Erst nachdem alle Server, die Daten weiterleiten, aktualisiert wurden, entfernen Sie den alten Fingerabdruck** von dem SIL-Aggregator mithilfe des Cmdlets `Set-SilAggregator –RemoveCertificateThumbprint`. Wenn ein Server, der Daten weiterleitet, die Weiterleitung unter Verwendung eines alten Zertifikats fortsetzt, das vom SIL-Aggregator entfernt wurde, **gehen Daten verloren** und werden nicht in die Datenbank auf dem Aggregator eingefügt. Dies wirkt sich nur auf Szenarien aus, in denen ein Server zuvor Daten erfolgreich an einen SIL-Aggregator weitergeleitet hat und das Zertifikat dann aus der Liste der Fingerabdrücke des SIL-Aggregators entfernt wird, um Daten von zu akzeptieren.

## <a name="release-notes"></a>Versionsinformationen

-   Es gibt das bekannte Problem, dass der SIL-Aggregator bei Vorhandensein von Installationen der SQL Server Standard Edition keine Verarbeitungen durchführt oder Berichte erstellt.  Dieser Fehler lässt sich mit folgenden Schritten beheben:

    1.  Öffnen Sie SQL Server Management Studio auf Ihrem SIL-Aggregator.

    2.  Stellen Sie eine Verbindung mit der Datenbank-Engine her.

    3.  Erweitern Sie in der Auswahlstruktur die Datenbank „SoftwareInventoryLogging“ und dann „Tabellen“.

    4.  Rechts klicken Sie auf **dbo. Sqlserveredition**, und wählen Sie dann "**Top 200 Rows bearbeiten**" aus.

    5.  Ändern Sie den PropertyNumValue-Wert neben "Standard Edition" in **2760240536** (von-1534726760).

    6.  Schließen Sie die Abfrage, um die Änderung zu speichern.

    7.  Für Server mit SIL, die bereits Daten in diesem Aggregator protokolliert haben, muss möglicherweise das Cmdlet `Publish-SilData` einmal ausgeführt werden, damit der Aggregator das Vorhandensein der SQL Server Standard Edition ordnungsgemäß verarbeitet.

-   In SIL-generierten Berichten umfasst jede Prozessorkernanzahle die Anzahl der Threads, wenn Hyperthreading auf dem physischen Server aktiviert ist.  Um die tatsächliche Anzahl der physischen Kerne auf Servern mit aktiviertem Hyperthreading zu erhalten, ist es notwendig, diese Zähler um die Hälfte zu verringern.

-   Gesamtwerte in den Zeilen (auf der Registerkarte **Dashboard** ) und Spalten (auf der Registerkarte **Zusammenfassung und Detail** ) mit der Bezeichnung "**gleichzeitig ausgeführt**..." für Windows Server und System Center Stimmen zwischen den beiden Standorten nicht genau überein. Auf der Registerkarte **Dashboard** ist es erforderlich, den Wert "**Windows Server-Geräte (ohne bekannte VMS**)" dem Wert "**gleichzeitig ausgeführt**..." hinzuzufügen. Wert, der dieser Zahl auf den Registerkarten **Zusammenfassung und Detail** entspricht.

-   Siehe **WICHTIGE SCHRITTE ZUR VERMEIDUNG VON DATENVERLUSTEN**, wenn Sie Zertifikate unter dem Abschnitt **Verwalten von SIL im zeitlichen Verlauf** dieser Dokumentation ändern oder aktualisieren.

-   Es ist zwar möglich, Windows Server 2008 R2- und Windows Server 2012-Hosts der Liste der abzurufenden Hosts hinzuzufügen, doch diese Version (1.0) von SIL-Aggregator unterstützt nur den Abruf von Windows Server 2012 R2-Hosts für Windows-/Hyper-V-basierte Hosts, damit alle Features und Funktionen erfolgreich ausgeführt werden.  Insbesondere ist bekannt, dass virtuelle Computer und Hosts beim Abrufen von Windows Server 2008 R2-Hosts in den Berichten des SIL-Aggregators möglicherweise nicht zugeordnet werden können.

## <a name="see-also"></a>Weitere Informationen
[Aggregator der Protokollierung des Softwarebestands 1.0 für Windows Server](https://www.microsoft.com/download/details.aspx?id=49046)<br>
[PowerShell-Cmdlets des SIL-Aggregators](/previous-versions/windows/powershell-scripting/mt548455(v=wps.640))<br>
[SIL PowerShell-Cmdlets](/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)<br>
[Eine Übersicht über SIL](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn268301(v=ws.11))<br>
[Verwalten von SIL](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383584(v=ws.11))