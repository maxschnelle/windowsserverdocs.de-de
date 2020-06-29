---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: Anforderungen und Best Practices für clusterfähiges Aktualisieren
ms.prod: windows-server
ms.topic: article
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: Anforderungen für die Verwendung des Cluster fähigen Updates zum Installieren von Updates auf Clustern, auf denen Windows Server ausgeführt wird.
ms.openlocfilehash: 066aca3adb2ceec19663653a7bc2f0f8cd42da16
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473307"
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>Anforderungen und Best Practices für clusterfähiges Aktualisieren

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Abschnitt werden die Anforderungen und Abhängigkeiten beschrieben, die zur Verwendung des [Cluster fähigen Aktualisierens (Cluster-Aware Update](cluster-aware-updating.md) , Cau) zum Anwenden von Updates auf einen Failovercluster unter Windows Server erforderlich sind

> [!NOTE]
> Sie müssen möglicherweise unabhängig überprüfen, ob Ihre Cluster Umgebung für die Anwendung von Updates bereit ist, wenn Sie ein anderes Plug- \- in als **Microsoft. windowsupdateplugin**verwenden. Wenn Sie ein nicht- \- Microsoft-Plug-in verwenden \- , kontaktieren Sie den Herausgeber, um weitere Informationen zu erhalten. Weitere Informationen zu Plug- \- ins finden Sie unter [Funktionsweise von Plug- \- ins](cluster-aware-updating-plug-ins.md).

## <a name="install-the-failover-clustering-feature-and-the-failover-clustering-tools"></a><a name="BKMK_REQ_CLUS"></a>Installieren des Failoverclustering-Features und der Failoverclusteringtools
Für das clusterfähige Aktualisieren ist die Installation des Failoverclustering-Features und der Failoverclusteringtools erforderlich. Die failoverclusteringtools umfassen die Cau \( -Toolsclusterawareupdating.dll\) , die Failoverclustering-Cmdlets und andere Komponenten, die für Cau-Vorgänge erforderlich sind. Schritte zum Installieren des Failoverclustering-Features finden Sie unter [Installieren des Failoverclustering-Features und der Failoverclusteringtools](create-failover-cluster.md#install-the-failover-clustering-feature).

Die genauen Installationsanforderungen für die failoverclusteringtools hängen davon ab, ob Updates von Cau als Cluster Rolle auf dem Failovercluster \( mithilfe des selbst \- Aktualisierungs Modus \) oder eines Remote Computers koordiniert werden. Der selbst \- Aktualisierungs Modus von Cau erfordert zusätzlich die Installation der Cluster Rolle für Cluster fähiges aktualisieren auf dem Failovercluster mithilfe der Cau-Tools.

In der folgenden Tabelle werden die Installationsanforderungen des Features für clusterfähiges Aktualisieren für die beiden Aktualisierungsmodi für clusterfähiges Aktualisieren zusammengefasst.

|Installierte Komponente|Selbst \- Aktualisierungs Modus|Remote \- Aktualisierungs Modus|
|-----------------------|-----------------------|-------------------------|
|Failoverclustering-Feature|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|
|Failoverclusteringtools|Auf allen Clusterknoten erforderlich|-Erforderlich auf Remote \- aktualisierbaren Computern<br />-Erforderlich auf allen Cluster Knoten zum Ausführen des Cmdlets " [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) "|
|Clusterrolle für clusterfähiges Aktualisieren|Erforderlich|Nicht erforderlich|

## <a name="obtain-an-administrator-account"></a>Anfordern eines Administratorkontos
Die folgenden Administratoranforderungen sind zur Verwendung der Features für clusterfähiges Aktualisieren erforderlich.

-   \( \) Sie müssen ein Domänen Konto verwenden, das über lokale Administratorrechte und Berechtigungen für alle Cluster Knoten verfügt, um eine Vorschau oder Anwendung von Update Aktionen mithilfe der Benutzeroberfläche für die Benutzeroberfläche für Cluster fähiges aktualisieren oder der Cmdlets für das Cluster fähige aktualisieren zu verwenden. Wenn das Konto nicht auf jedem Knoten über ausreichende Berechtigungen verfügt, werden Sie im Fenster Cluster fähiges Aktualisieren aufgefordert, die erforderlichen Anmelde Informationen anzugeben, wenn Sie diese Aktionen ausführen. Wenn Sie die Cmdlets für das [Cluster fähige aktualisieren](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps) verwenden möchten, können Sie die erforderlichen Anmelde Informationen als Cmdlet-Parameter angeben.

-   Wenn Sie \- das Cluster fähige aktualisieren im Remote Aktualisierungs Modus verwenden, wenn Sie mit einem Konto angemeldet sind, das nicht über lokale Administratorrechte und Berechtigungen auf den Cluster Knoten verfügt, müssen Sie die Tools für Cluster fähiges aktualisieren als Administrator ausführen, indem Sie ein lokales Administrator Konto auf dem Computer mit dem Update Koordinator oder ein Konto verwenden, das über das Benutzerrecht Identität **eines Clients annehmen nach der Authentifizierung** verfügt.

-   Zum Ausführen des Best Practices Analyzer für Cluster fähiges aktualisieren müssen Sie ein Konto verwenden, das auf den Cluster Knoten über Administratorrechte und lokale Administratorrechte auf dem Computer, der zum Ausführen des [Test-causetup-](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Cmdlets verwendet wird, oder zum Analysieren der Update Bereitschaft des Clusters mithilfe des Cluster fähigen Aktualisierungs Fensters verwendet wird. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft des Clusters](#BKMK_BPA).

## <a name="verify-the-cluster-configuration"></a>Überprüfen der Clusterkonfiguration
Nachfolgend sind allgemeine Anforderungen an einen Failovercluster zum Unterstützen von Updates mithilfe des clusterfähigen Aktualisierens aufgeführt. Weitere Konfigurationsanforderungen für die Remoteverwaltung auf den Knoten finden Sie weiter unten in diesem Thema unter [Konfigurieren von Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).

-   Es müssen ausreichend Clusterknoten online sein, damit der Cluster das Quorum besitzt.

-   Alle Clusterknoten müssen sich in derselben Active Directory-Domäne befinden.

-   Der Clustername muss im Netzwerk mithilfe von DNS aufgelöst werden.

-   Wenn das Cluster fähige aktualisieren im Remote \- Aktualisierungs Modus verwendet wird, muss der Computer des Update Koordinators über eine Netzwerkverbindung mit den Failoverclusterknoten verfügen, und er muss sich in derselben Active Directory Domäne wie der Failovercluster befinden.

-   Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden. Dieser Dienst wird standardmäßig auf allen Clusterknoten installiert und für den automatischen Start konfiguriert.

-   \- \- Stellen Sie sicher, dass die Skripts auf allen Cluster Knoten installiert sind oder dass Sie für alle Knoten verfügbar sind, z. b. auf einer hoch verfügbaren Netzwerkdatei Freigabe, um PowerShell-Skripts vor Update oder nach Update Skripts während einer Update-Update-Aktualisierung zu verwenden. Wenn Skripts auf einer Netzwerkdateifreigabe gespeichert werden, konfigurieren Sie den Ordner für die Gruppe "Alle" für die Berechtigung "Lesen".

## <a name="configure-the-nodes-for-remote-management"></a><a name="BKMK_NODE_CONFIG"></a>Konfigurieren der Knoten für die Remoteverwaltung
Zum Verwenden des Cluster fähigen Aktualisierens müssen alle Knoten des Clusters für die Remote Verwaltung konfiguriert sein. Standardmäßig müssen Sie zum Konfigurieren der Knoten für die Remote Verwaltung nur [eine Firewallregel aktivieren, um automatische Neustarts zuzulassen](#BKMK_FW).

In der folgenden Tabelle sind die Anforderungen an die gesamte Remote Verwaltung aufgeführt, wenn die Umgebung von den Standardeinstellungen abweicht.

Diese Anforderungen treten zusätzlich zu den Installationsanforderungen für [Installieren des Failoverclustering-Features und der Failoverclusteringtools](#BKMK_REQ_CLUS) und zu den allgemeinen Anforderungen auf, die in vorherigen Abschnitten dieses Themas beschrieben werden.

|Anforderung|Standardstatus|Selbst \- Aktualisierungs Modus|Remote \- Aktualisierungs Modus|
|---------------|---|-----------------------|-------------------------|
|[Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW)|Disabled|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|
|[Aktivieren der Windows-Verwaltungsinstrumentation](#BKMK_WMI)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|
|[Aktivieren von Windows PowerShell 3.0 oder 4.0 und Windows PowerShell-Remoting](#BKMK_PS)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten muss Folgendes ausgeführt werden:<p>-Das [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) -Cmdlet<br />-PowerShell- \- Skripts vor und nach \- dem Update während einer Update Lauf Zeit Aktualisierung<br />-Tests der Update Bereitschaft des Clusters mithilfe des Cluster fähigen Aktualisierungs Fensters oder des Windows PowerShell-Cmdlets " [Test \- causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) "|
|[Installieren von .NET Framework 4,6 oder 4,5](#BKMK_NET)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten muss Folgendes ausgeführt werden:<p>-Das [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) -Cmdlet<br />-PowerShell- \- Skripts vor und nach \- dem Update während einer Update Lauf Zeit Aktualisierung<br />-Tests der Update Bereitschaft des Clusters mithilfe des Cluster fähigen Aktualisierungs Fensters oder des Windows PowerShell-Cmdlets " [Test \- causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) "|

### <a name="enable-a-firewall-rule-to-allow-automatic-restarts"></a><a name="BKMK_FW"></a>Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts
Um automatische Neustarts nach dem Anwenden von Updates zuzulassen \( , wenn für die Installation eines Updates ein Neustart erforderlich ist \) , \- muss auf jedem Knoten, der folgenden Datenverkehr zulässt, eine Firewallregel aktiviert werden, wenn die Windows-Firewall oder eine nicht-Microsoft-Firewall auf den Cluster Knoten verwendet wird:

-   Protokoll: TCP

-   Richtung: Eingehend

-   Programm: wininit.exe

-   Ports: Dynamische RPC-Ports

-   Profil: Domäne

Wenn die Windows-Firewall auf den Clusterknoten verwendet wird, können Sie dazu die Regelgruppe **Remotecomputer herunterfahren** der Windows-Firewall auf den einzelnen Clusterknoten aktivieren. Wenn Sie das Fenster Cluster fähiges aktualisieren verwenden, um Updates anzuwenden und selbst \- Aktualisierungs Optionen zu konfigurieren, wird die Regelgruppe **Remote herunter** fahren der Windows-Firewall auf jedem Cluster Knoten automatisch aktiviert.

> [!NOTE]
> Die Regelgruppe **Remote Shutdown** der Windows-Firewall kann nicht aktiviert werden, wenn sie mit Gruppenrichtlinieneinstellungen in Konflikt steht, die für die Windows-Firewall konfiguriert sind.

Die Firewallregelgruppe **Remote Shutdown** wird auch durch Angeben des **– enablefirewallrules** -Parameters aktiviert, wenn die folgenden Cmdlets für Cluster fähiges aktualisieren ausgeführt werden: [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps), [Aufruf-caurun](https://docs.microsoft.com/powershell/module/clusterawareupdating/Invoke-CauRun?view=win10-ps)und [setcauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole?view=win10-ps).

Das folgende PowerShell-Beispiel zeigt eine zusätzliche Methode zum Aktivieren automatischer Neustarts auf einem Cluster Knoten.

```PowerShell
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true
```

### <a name="enable-windows-management-instrumentation-wmi"></a><a name="BKMK_WMI"></a>Windows-Verwaltungsinstrumentation aktivieren (WMI)
Alle Cluster Knoten müssen mit Windows-Verwaltungsinstrumentation WMI für die Remote Verwaltung konfiguriert werden \( \) . Diese Einstellung ist standardmäßig aktiviert.

Gehen Sie wie folgt vor, um die Remoteverwaltung manuell zu aktivieren:

1.  Starten Sie in der Konsole "Dienste" den Dienst **Windows-Remoteverwaltung**, und legen Sie für den Starttyp **Automatisch** fest.

2.  Führen Sie das [-Cmdlet](https://docs.microsoft.com/powershell/module/Microsoft.WsMan.Management/Set-WSManQuickConfig?view=powershell-6) oder den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten aus:

    ```PowerShell
    winrm quickconfig -q
    ```

Zur Unterstützung von WMI-Remoting muss die eingehende Firewallregel für **Windows-Remoteverwaltung \( http \- in \) ** auf jedem Knoten aktiviert sein, wenn die Windows-Firewall auf den Cluster Knoten verwendet wird.  Diese Regel ist standardmäßig aktiviert.

### <a name="enable-windows-powershell-and-windows-powershell-remoting"></a><a name="BKMK_PS"></a>Aktivieren von Windows PowerShell und Windows PowerShell-Remoting
\- \- PowerShell muss installiert und aktiviert sein, damit Remote Befehle auf allen Cluster Knoten ausgeführt werden können, um den selbst Aktualisierungs Modus und bestimmte Cau-Features im Remote Aktualisierungs Modus zu aktivieren. PowerShell ist standardmäßig installiert und für Remoting aktiviert.

Verwenden Sie eine der folgenden Methoden, um PowerShell-Remoting zu aktivieren:

-   Führen Sie das [-Cmdlet](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enable-PSRemoting) aus.

-   Konfigurieren Sie eine \- Gruppenrichtlinie Einstellung auf Domänen Ebene für Windows-Remoteverwaltung \( WinRM \) .

Weitere Informationen zum Aktivieren von PowerShell-Remoting finden Sie unter [Informationen zu Remote Anforderungen](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements?view=powershell-6).

### <a name="install-net-framework-46-or-45"></a><a name="BKMK_NET"></a>Installieren von .NET Framework 4,6 oder 4,5
Um den selbst \- Aktualisierungs Modus und bestimmte Features für Cluster fähiges aktualisieren im Remote \- Aktualisierungs Modus zu aktivieren, muss .NET Framework 4,6 oder .NET Framework 4,5 (auf Windows Server 2012 R2) auf allen Cluster Knoten installiert sein. Standardmäßig ist .NET Framework installiert.

Verwenden Sie den folgenden Befehl, um .NET Framework 4,6 (oder 4,5) mithilfe von PowerShell zu installieren, wenn er nicht bereits installiert ist:

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="best-practices-recommendations-for-using-cluster-aware-updating"></a><a name="BKMK_BEST_PRAC"></a>Empfehlungen zu bewährten Methoden für die Verwendung des Cluster fähigen Updates

### <a name="recommendations-for-applying-microsoft-updates"></a><a name="BKMK_BP_WUA"></a>Empfehlungen zum Anwenden von Microsoft-Updates

Wenn Sie mit der Verwendung von Cau zum Anwenden von Updates mit dem Standard-Plug-in für **Microsoft. windowsupdateplugin** in \- einem Cluster beginnen, sollten Sie keine anderen Methoden zum Installieren von Software Updates von Microsoft auf den Cluster Knoten mehr verwenden.

> [!CAUTION]
> Das Kombinieren von Cau mit Methoden, die einzelne Knoten automatisch \( nach einem festgelegten Zeitplan aktualisieren \) , kann zu unvorhersehbaren Ergebnissen führen, einschließlich Dienstunterbrechungen und ungeplanter Ausfallzeiten.

Empfohlene Richtlinien:

-   Um die besten Ergebnisse zu erzielen, empfiehlt es sich, dass Sie Einstellungen auf dem Clusterknoten für die automatische Aktualisierung deaktivieren, z. B. über die Einstellungen für automatische Updates in der Systemsteuerung oder über die Einstellungen, die mithilfe der Gruppenrichtlinie konfiguriert werden.

    > [!CAUTION]
    > Die automatische Installation von Updates auf den Clusterknoten kann die Installation von Updates durch clusterfähiges Aktualisieren beeinträchtigen und somit beim clusterfähigen Aktualisieren zu Fehlern führen.

    Die folgenden Einstellungen für automatische Updates sind (sofern erforderlich) mit dem clusterfähigen Aktualisieren kompatibel, da der Administrator die zeitliche Abfolge der Updateinstallation steuern kann.

    -   Einstellungen zur Benachrichtigung vor dem Herunterladen von Updates und zur Benachrichtigung vor der Installation

    -   Einstellungen zum automatischen Herunterladen von Updates und zur Benachrichtigung vor der Installation

    Wenn die Option "Automatische Updates" Updates jedoch zur selben Zeit wie eine Updateausführung für clusterfähiges Aktualisieren herunterlädt, kann die Updateausführung möglicherweise länger dauern.

-   Konfigurieren Sie kein Update System wie z. b \( . Windows Server Update Services WSUS \) , um Updates automatisch nach \( einem festgelegten Zeitplan auf \) Cluster Knoten anzuwenden.

-   Alle Clusterknoten müssen einheitlich für die Verwendung derselben Updatequelle konfiguriert sein, z. B. WSUS-Server, Windows-Update oder Microsoft Update.

-   Schließen Sie Clusterknoten von allen erforderlichen oder automatischen Updates aus, wenn Sie Softwareupdates mithilfe eines Konfigurationsverwaltungssystems auf Computer im Netzwerk anwenden. Beispiele für Konfigurations Verwaltungssysteme sind Microsoft Endpoint Configuration Manager und Microsoft System Center Virtual Machine Manager 2008.

-   Wenn z. b. \( von den WSUS-Servern interne Software Verteilungs Server zum Speichern \) und Bereitstellen der Updates verwendet werden, stellen Sie sicher, dass die genehmigten Updates für die Cluster Knoten von diesen Servern korrekt identifiziert werden.

#### <a name="apply-microsoft-updates-in-branch-office-scenarios"></a><a name="BKMK_PROXY"></a>Anwenden von Microsoft-Updates in Filialszenarien
Wenn Sie in bestimmten Filialszenarien Microsoft-Updates über Microsoft Update oder Windows Update auf Clusterknoten herunterladen möchten, müssen Sie möglicherweise auf jedem Knoten Proxyeinstellungen für das lokale Systemkonto konfigurieren. Dies kann z. B. erforderlich sein, wenn die Filialcluster auf Microsoft Update oder Windows Update zugreifen, um Updates mithilfe eines lokalen Proxyservers herunterzuladen.

Konfigurieren Sie bei Bedarf die WinHTTP-Proxy Einstellungen auf den einzelnen Knoten, um einen lokalen Proxy Server anzugeben und lokale Adress Ausnahmen ( \( eine Umgehungs Liste für lokale Adressen) zu konfigurieren \) . Dazu können Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten auf den einzelnen Clusterknoten ausführen:

```
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"
```

Dabei ist <*proxyserverfqdn*> der voll qualifizierte Domänen Name für den Proxy Server und <*Port*> ist der Port, über den die Kommunikation stattfinden soll (normalerweise Port 443).

Geben Sie beispielsweise den folgenden Befehl ein, um die WinHTTP-Proxy Einstellungen für das lokale System Konto anzugeben, in dem der Proxy Server *MyProxy.contoso.com*mit Port 443 und lokale Adress Ausnahmen angegeben ist:

```
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"
```

### <a name="recommendations-for-using-the-microsofthotfixplugin"></a><a name="BKMK_BP_HF"></a>Empfehlungen zur Verwendung von Microsoft.HotfixPlugin

-   Es wird empfohlen, dass Sie Berechtigungen im Hotfixstammordner und in der Hotfixkonfigurationsdatei konfigurieren, um den Schreibzugriff nur auf lokale Administratoren auf den Computer zu beschränken, die zum Speichern dieser Dateien verwendet werden. Dadurch können Manipulationen an diesen Dateien durch nicht berechtigte Benutzer verhindert werden, die die Funktionalität des Failoverclusters beeinträchtigen könnten, wenn Hotfixes angewendet werden.

-   Um die Datenintegrität für die Server Message Block-SMB-Verbindungen sicherzustellen, \( \) die für den Zugriff auf den hotfixstamm Ordner verwendet werden, sollten Sie die SMB-Verschlüsselung im freigegebenen SMB-Ordner konfigurieren, sofern dies möglich ist. **Microsoft.HotfixPlugin** erfordert, dass die SMB-Signatur oder SMB-Verschlüsselung konfiguriert ist, um die Datenintegrität für SMB-Verbindungen sicherzustellen.

    Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den hotfixstamm Ordner und die hotfixkonfigurationsdatei](cluster-aware-updating-plug-ins.md#BKMK_ACL).

### <a name="additional-recommendations"></a>Weitere Empfehlungen

-   Um Konflikte mit einer Updateausführung für clusterfähiges Aktualisieren zu vermeiden, die möglicherweise für den gleichen Zeitpunkt vorgesehen sind, planen Sie während der geplanten Wartungszeitfenster keine Kennwortänderungen für Clusternamenobjekte und virtuelle Computerobjekte.

-   Sie sollten die entsprechenden Berechtigungen für \- Skripts vor und nach \- dem Update festlegen, die in freigegebenen Netzwerk Ordnern gespeichert werden, um mögliche Manipulationen an diesen Dateien durch nicht autorisierte Benutzer zu verhindern.

-   Zum Konfigurieren von Cau im selbst \- Aktualisierungs Modus muss ein virtuelles Computer Objekt \( VCO \) für die Cluster Rolle für Cluster fähiges aktualisieren in Active Directory erstellt werden. Dieses Objekt kann durch das clusterfähige Aktualisieren automatisch zu dem Zeitpunkt erstellt werden, zu dem die Clusterrolle für clusterfähiges Aktualisieren hinzugefügt wird, wenn der Failovercluster über die entsprechenden Berechtigungen verfügt. Aufgrund der Sicherheitsrichtlinien in einigen Organisationen ist es möglicherweise erforderlich, das Objekt in Active Directory vorab bereitzustellen. Das entsprechende Verfahren hierfür finden Sie unter [Schritte für die Vorabbereitstellung eines Kontos für eine Clusterrolle](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002\(v=ws.10\)#steps-for-prestaging-the-cluster-name-account).

-   Sie können Profile für die Updateausführung erstellen, um Updateausführungseinstellungen für verschiedene Failovercluster mit ähnlichen Aktualisierungsanforderungen in der IT-Organisation zu speichern und wiederzuverwenden. In Abhängigkeit vom Aktualisierungsmodus können Sie die Updateausführungsprofile zusätzlich auf einer Dateifreigabe speichern und verwalten, auf die alle Remotecomputer für den Updatekoordinator oder die Failovercluster zugreifen können. Weitere Informationen finden Sie unter [Erweiterte Optionen und Update Lauf Profile für Cau](cluster-aware-updating-options.md).

## <a name="test-cluster-updating-readiness"></a><a name="BKMK_BPA"></a>Testen der Updatebereitschaft des Clusters
Sie können Best Practices Analyzer das BPA-Modell für Cluster fähiges aktualisieren ausführen \( \) , um zu testen, ob ein Failovercluster und die Netzwerkumgebung vielen der Anforderungen entsprechen, damit Software Updates von Cau angewendet werden. Viele der Tests prüfen die Umgebung auf die Bereitschaft zur Anwendung von Microsoft-Updates mithilfe des Standard-Plug- \- ins, **Microsoft. windowsupdateplugin**.

> [!NOTE]
> Möglicherweise müssen Sie unabhängig prüfen, ob Ihre Cluster Umgebung für die Anwendung von Software Updates bereit ist, indem Sie ein anderes Plug- \- in als **Microsoft. windowsupdateplugin**verwenden. Wenn Sie ein nicht- \- Microsoft-Plug-in verwenden \- , z. b. ein von Ihrem Hardwarehersteller bereitgestelltes Plug-in, wenden Sie sich an den Herausgeber

Zum Ausführen des Best Practices Analyzer (BPA) haben Sie die folgenden beiden Möglichkeiten:

1.  Wählen Sie in der Konsole für clusterfähiges Aktualisieren die Option **Vorbereitung auf das Clusterupdate analysieren** aus. Nachdem der BPA die Bereitschafts Tests abgeschlossen hat, wird ein Testbericht angezeigt. Wenn auf den Clusterknoten Probleme aufgetreten sind, werden die bestimmten Probleme und die betroffenen Knoten identifiziert, damit Sie entsprechende Korrekturmaßnahmen ergreifen können. Diese Tests können einige Minuten dauern.

2.  Führen Sie das [Test-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup) aus. Sie können das Cmdlet auf einem lokalen Computer oder einem Remote Computer ausführen, auf dem das Failoverclustering-Modul für Windows PowerShell (Teil der Failoverclustering-Tools) installiert ist. Sie können das Cmdlet auch auf einem Knoten des Failoverclusters ausführen.

> [!NOTE]
> -   Sie müssen ein Konto verwenden, das auf den Cluster Knoten über Administratorrechte und lokale Administratorrechte auf dem Computer, der zum Ausführen des **Test- \- causetup** -Cmdlets verwendet wird, oder zum Analysieren der Update Bereitschaft des Clusters mithilfe des Cluster fähigen Aktualisierungs Fensters verwendet wird. Zum Ausführen der Tests mithilfe des Cluster fähigen Aktualisierungs Fensters müssen Sie auf dem Computer mit den erforderlichen Anmelde Informationen angemeldet sein.
> -   Bei den Tests wird angenommen, dass die Tools für clusterfähiges Aktualisieren, die zum Anzeigen einer Updatevorschau oder zum Anwenden von Updates verwendet werden, auf demselben Computer und mit denselben Anmeldeinformationen ausgeführt werden, die zum Testen der Updatebereitschaft des Clusters verwendet werden.

> [!IMPORTANT]
> Es wird dringend empfohlen, dass Sie die Cluster in den folgenden Situationen auf die Updatebereitschaft testen:
>
> -   Bevor Sie das clusterfähige Aktualisieren zum ersten Mal zum Anwenden von Softwareupdates verwenden können.
> -   Nachdem Sie einen Knoten zum Cluster hinzugefügt oder andere Hardwareänderungen am Cluster vorgenommen haben, die die Ausführung des Assistenten zum Überprüfen von Clustern erfordern.
> -   Nachdem Sie eine Update Quelle geändert haben, oder ändern Sie die Update Einstellungen oder-Konfigurationen, die \( \) sich auf die Anwendung von Updates auf den Knoten auswirken können.

### <a name="tests-for-cluster-updating-readiness"></a>Tests für die Updatebereitschaft des Clusters
In der folgenden Tabelle sind die Tests für die Updatebereitschaft des Clusters, einige allgemeine Probleme sowie Schritte zur Behebung dieser Probleme aufgeführt.


|                                                      Test                                                      |                                                                                                                                               Mögliche Probleme und Auswirkungen                                                                                                                                               |                                                                                                                                                                                         Lösungsschritte                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                     Der Failovercluster muss verfügbar sein.                                     |                                                                                       Der Failoverclustername kann nicht aufgelöst werden oder der Zugriff ist auf mindestens einen Clusterknoten nicht möglich. Der BPA kann die Clusterbereitschaftstests nicht ausführen.                                                                                        |                                                                   -Überprüfen Sie die Schreibweise des Namens des Clusters, der während der BPA-Laufzeit angegeben wurde.<br />-Stellen Sie sicher, dass alle Knoten des Clusters online sind und ausgeführt werden.<br />-Überprüfen Sie, ob der Konfigurationsüberprüfungs-Assistent erfolgreich auf dem Failovercluster ausgeführt werden kann.                                                                    |
|                    Die Failoverclusterknoten müssen über die Windows-Verwaltungsinstrumentation (WMI) für die Remoteverwaltung aktiviert sein.                    |                                                Mindestens ein Failoverclusterknoten ist nicht mit Windows-Verwaltungsinstrumentation WMI für die Remote Verwaltung aktiviert \( \) . Die Clusterknoten können nicht über das clusterfähige Aktualisieren aktualisiert werden, wenn die Knoten nicht für die Remoteverwaltung konfiguriert sind.                                                 |                                                                                                  Stellen Sie sicher, dass alle Failoverclusterknoten über die WMI für die Remoteverwaltung aktiviert wurden. Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                                                   |
|                      PowerShell-Remoting muss auf jedem Failoverclusterknoten aktiviert werden.                       |                                                           PowerShell ist nicht installiert oder nicht für das Remoting auf mindestens einem Failoverclusterknoten aktiviert. Cau kann nicht für den selbst \- Aktualisierungs Modus konfiguriert werden oder bestimmte Features im Remote \- Aktualisierungs Modus verwenden.                                                            |                                                                                             Stellen Sie sicher, dass PowerShell auf allen Cluster Knoten installiert und für das Remoting aktiviert ist.<p>Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                                             |
|                                            Failoverclusterversion                                            |                                                                            Mindestens ein Knoten im Failovercluster wird nicht unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt. Der Failovercluster kann nicht mithilfe des clusterfähigen Aktualisierens aktualisiert werden.                                                                             |                                                                   Vergewissern Sie sich, dass der während der BPA-Ausführung angegebene Failovercluster unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.<p>Weitere Informationen finden Sie in diesem Thema unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS).                                                                   |
| Die erforderlichen Versionen von .NET Framework und Windows PowerShell müssen auf allen Failoverclusterknoten installiert werden. |                                                                                              .NET Framework 4,6, 4,5 oder Windows PowerShell ist auf mindestens einem Cluster Knoten nicht installiert. Möglicherweise funktionieren einige Features für das clusterfähige Aktualisieren nicht.                                                                                              |                                                                            Stellen Sie sicher, dass .NET Framework 4,6 oder 4,5 und Windows PowerShell auf allen Cluster Knoten installiert sind, sofern diese erforderlich sind.<p>Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                             |
|                           Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden.                           |                                                                                                            Der Clusterdienst wird auf mindestens einem Knoten nicht ausgeführt. Der Failovercluster kann nicht mithilfe des clusterfähigen Aktualisierens aktualisiert werden.                                                                                                             |                        -Stellen Sie sicher, dass die Clusterdienst \( ClusSvc \) auf allen Knoten im Cluster gestartet wird und für den automatischen Start konfiguriert ist.<br />-Überprüfen Sie, ob der Konfigurationsüberprüfungs-Assistent erfolgreich auf dem Failovercluster ausgeführt werden kann.<p>Weitere Informationen finden Sie in diesem Thema unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS).                         |
|     Automatische Updates dürfen nicht für die automatische Installation von Updates auf beliebigen Failoverclusterknoten konfiguriert werden.     |                                           Auf mindestens einem Failoverclusterknoten sind automatische Updates für die automatische Installation von Microsoft-Updates auf diesem Knoten konfiguriert. Die Kombination des clusterfähigen Aktualisierens mit anderen Aktualisierungsmethoden kann zu ungeplanter Downtime oder zu unvorhergesehenen Ergebnissen führen.                                            |                                                     Wenn die Windows Update-Funktionalität auf mindestens einem Clusterknoten für automatische Updates konfiguriert ist, stellen Sie sicher, dass automatische Updates nicht für die automatische Installation von Updates konfiguriert sind.<p>Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).                                                     |
|                          Die Failoverclusterknoten müssen dieselbe Updatequelle verwenden.                          |                                                    Mindestens ein Failoverclusterknoten ist für die Verwendung einer Updatequelle für Microsoft-Updates konfiguriert, die sich von den restlichen Knoten unterscheidet. Die Updates werden möglicherweise nicht einheitlich über das clusterfähige Aktualisieren auf die Clusterknoten angewendet.                                                    |                                                                        Stellen Sie sicher, dass alle Clusterknoten für die Verwendung derselben Updatequelle konfiguriert sind, z. B. WSUS-Server, Windows-Update oder Microsoft Update.<p>Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).                                                                         |
|       Eine Firewallregel, die das Remoteherunterfahren gestattet, muss auf jedem Knoten im Failovercluster aktiviert werden.       |                 Mindestens ein Failoverclusterknoten verfügt nicht über eine aktivierte Firewallregel, die das Remoteherunterfahren gestattet, oder eine Gruppenrichtlinieneinstellung verhindert, dass diese Regel aktiviert wird. Eine Updateausführung, die Updates anwendet, die einen automatischen Neustart der Knoten erfordern, wurde möglicherweise nicht ordnungsgemäß beendet.                  |                                                                    Wenn auf den Cluster Knoten die Windows-Firewall oder eine nicht- \- Microsoft-Firewall verwendet wird, konfigurieren Sie eine Firewallregel, die das Remote Herunterfahren zulässt.<p>Weitere Informationen finden Sie in diesem Thema unter [Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW).                                                                    |
|          Die Proxyservereinstellung muss auf jedem Failoverclusterknoten auf einen lokalen Proxyserver festgelegt werden.          |                             Mindestens ein Failoverclusterknoten weist eine fehlerhafte Proxyserverkonfiguration auf.<p>Wenn ein lokaler Proxyserver verwendet wird, muss die Proxyservereinstellung auf den einzelnen Knoten ordnungsgemäß konfiguriert werden, damit der Cluster auf Microsoft Update oder Windows Update zugreifen kann.                              |                                            Stellen Sie sicher, dass die WinHTTP-Proxyeinstellungen auf allen Clusterknoten auf einem lokalen Proxyserver eingestellt sind, wenn dies erforderlich ist. Wenn in Ihrer Umgebung kein Proxyserver verwendet wird, kann diese Warnung ignoriert werden.<p>Weitere Informationen finden Sie in diesem Thema unter [Anwenden von Updates in Filialszenarien](#BKMK_PROXY).                                            |
|        Die Cluster Rolle für Cluster fähiges aktualisieren muss auf dem Failovercluster installiert werden, um den selbst \- Aktualisierungs Modus zu aktivieren.        |                                                                                                   Die Clusterrolle für clusterfähiges Aktualisieren ist auf diesem Failovercluster nicht installiert. Diese Rolle ist für die selbst Aktualisierung des Clusters erforderlich \- .                                                                                                   |      Wenn Sie Cau im selbst \- Aktualisierungs Modus verwenden möchten, fügen Sie die Cluster Rolle für Cluster fähiges aktualisieren auf dem Failovercluster mit einer der folgenden Methoden hinzu:<p>-Führen Sie das PowerShell-Cmdlet [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole) aus.<br />-Wählen Sie im Fenster "Cluster fähiges aktualisieren" die Aktion " **selbst \- Aktualisierungs Optionen für Cluster konfigurieren** " aus.      |
|         Die Cluster Rolle für Cluster fähiges aktualisieren muss auf dem Failovercluster aktiviert werden, um den selbst \- Aktualisierungs Modus zu aktivieren.         | Die Clusterrolle für clusterfähiges Aktualisieren ist deaktiviert. Die Cluster Rolle für Cluster fähiges aktualisieren ist z. b. nicht installiert oder wurde mithilfe des PowerShell-Cmdlets " [ \- cauclusterrole deaktivieren](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole) " deaktiviert. Diese Rolle ist für die selbst Aktualisierung des Clusters erforderlich \- . | Wenn Sie Cau im selbst \- Aktualisierungs Modus verwenden möchten, aktivieren Sie die Cluster Rolle für Cluster fähiges aktualisieren auf diesem Failovercluster mit einer der folgenden Methoden:<p>-Führen Sie das PowerShell-Cmdlet [enable-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole) aus.<br />-Wählen Sie im Fenster "Cluster fähiges aktualisieren" die Aktion " **selbst \- Aktualisierungs Optionen für Cluster konfigurieren** " aus. |
|      Das konfigurierte Cau-Plug- \- in für den selbst \- Aktualisierungs Modus muss auf allen Failoverclusterknoten registriert werden.      |                                                              Die Cluster Rolle für Cluster fähiges aktualisieren auf einem oder mehreren Knoten dieses Failoverclusters kann nicht auf das Plug-in-Modul für Cluster fähiges \- Aktualisieren zugreifen, das in den selbst \- Aktualisierungs Optionen konfiguriert ist. Eine selbst \- Aktualisierungs Ausführung kann fehlschlagen.                                                              |           -Stellen Sie sicher, dass das konfigurierte Plug- \- in für Cluster fähiges aktualisieren auf allen Cluster Knoten installiert ist, indem Sie das Installationsverfahren für das Produkt befolgen, das das Plug-in für Cluster fähiges \-<br />-Führen Sie das PowerShell-Cmdlet " [Register \- cauplugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) " aus, um das Plug- \- in auf den erforderlichen Cluster Knoten zu registrieren.           |
|                Alle Failoverclusterknoten müssen denselben Satz von registrierten Plug-Ins für Cluster fähiges aktualisieren aufweisen. \-                 |                                                                             Eine selbst \- Aktualisierungs Ausführung kann fehlschlagen, wenn das Plug- \- in, das für die Verwendung in einer Update Ausführung konfiguriert ist, in ein solches geändert wird, das nicht auf allen Cluster Knoten verfügbar ist.                                                                              |           -Stellen Sie sicher, dass das konfigurierte Plug- \- in für Cluster fähiges aktualisieren auf allen Cluster Knoten installiert ist, indem Sie das Installationsverfahren für das Produkt befolgen, das das Plug-in für Cluster fähiges \-<br />-Führen Sie das PowerShell-Cmdlet " [Register \- cauplugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) " aus, um das Plug- \- in auf den erforderlichen Cluster Knoten zu registrieren.           |
|                               Die konfigurierten Optionen für die Updateausführung müssen gültig sein.                                |                                                                          Der selbst \- Aktualisierungs Zeitplan und die Update Lauf Optionen, die für diesen Failovercluster konfiguriert sind, sind unvollständig oder ungültig. Eine selbst \- Aktualisierungs Ausführung kann fehlschlagen.                                                                           |                                                            Konfigurieren Sie einen gültigen \- Zeitplan für die selbst Aktualisierung und einen Satz von Optionen für die Update Ausführung. Beispielsweise können Sie das PowerShell-Cmdlet " [Set \- cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole) " verwenden, um die Cluster Rolle für Cluster fähiges aktualisieren zu konfigurieren.                                                            |
|                  Mindestens zwei Failoverclusterknoten müssen Besitzer der Clusterrolle für clusterfähiges Aktualisieren sein.                  |                                                                                        Eine im selbst \- Aktualisierungs Modus gestartete Update Ausführung schlägt fehl, da die Cluster Rolle für Cluster fähiges aktualisieren keinen möglichen Besitzer Knoten besitzt, zu dem gewechselt werden kann.                                                                                         |                                                                                                                Stellen Sie mithilfe der Failoverclustering-Tools sicher, dass alle Clusterknoten als mögliche Besitzer der Clusterrolle für clusterfähiges Aktualisieren konfiguriert sind. Dies ist die Standardkonfiguration.                                                                                                                |
|                  Alle Failoverclusterknoten müssen auf die Windows PowerShell-Skripts zugreifen können.                  |                                                                        Nicht alle möglichen Besitzer Knoten der Cluster Rolle für Cluster fähiges aktualisieren können auf die konfigurierten Windows PowerShell \- -Skripts vor und nach dem Update zugreifen \- . Eine selbst \- Aktualisierungs Ausführung schlägt fehl.                                                                        |                                                                                                                    Stellen Sie sicher, dass alle möglichen Besitzer Knoten der Cluster Rolle für Cluster fähiges Aktualisieren über Berechtigungen für den Zugriff auf die konfigurierten PowerShell \- -Skripts vor und nach dem Update verfügen \- .                                                                                                                     |
|                   Alle Failoverclusterknoten müssen dieselben Windows PowerShell-Skripts verwenden.                   |                                                     Nicht alle möglichen Besitzer Knoten der Cluster Rolle für Cluster fähiges aktualisieren verwenden dieselbe Kopie der angegebenen Windows PowerShell \- -Skripts vor und nach dem Update \- . Eine selbst \- Aktualisierungs Ausführung kann fehlschlagen oder ein unerwartetes Verhalten anzeigen.                                                     |                                                                                                                                   Stellen Sie sicher, dass alle möglichen Besitzer Knoten der Cluster Rolle für Cluster fähiges aktualisieren dieselben PowerShell \- -Skripts vor und nach dem Update verwenden \- .                                                                                                                                   |
|         Die Einstellung "WarnAfter", die für die Updateausführung angegeben wurde, muss niedriger sein als die Einstellung "StopAfter".         |                                                                           Die angegebenen Timeoutwerte der Updateausführung für clusterfähiges Aktualisieren sorgen dafür, dass der Warnungstimeout wirkungslos ist. Eine Updateausführung kann möglicherweise abgebrochen werden, bevor ein Warnereignisprotokoll generiert werden kann.                                                                            |                                                                                                                                      Konfigurieren Sie in den Optionen der Updateausführung einen Optionswert für **WarnAfter**, der niedriger als der Optionswert für **StopAfter** ist.                                                                                                                                       |

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Übersicht über die clusterfähige Aktualisierung.](cluster-aware-updating.md)