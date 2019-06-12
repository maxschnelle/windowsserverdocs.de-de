---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: Cluster-Aware Updating Anforderungen und best practices
ms.prod: windows-server-threshold
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: Anforderungen für die Verwendung des clusterfähigen Aktualisierens, um Updates in Clustern mit Windows Server zu installieren.
ms.openlocfilehash: 32fa77ca2c24d75347d61f9bdeb4c5c93a20d89d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439679"
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>Cluster-Aware Updating Anforderungen und best practices

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Abschnitt wird beschrieben, die Anforderungen und Abhängigkeiten, die erforderlich sind, verwenden [Cluster-Aware Updating](cluster-aware-updating.md) (CAU), um Updates auf einem Failovercluster unter Windows Server anzuwenden.

> [!NOTE]  
> Sie müssen möglicherweise unabhängig überprüfen, ob Ihre Clusterumgebung ist bereit zum Anwenden von Updates, bei der Verwendung einer Plug &\-in anderen als **Microsoft.WindowsUpdatePlugin**. Wenn Sie einen nicht verwenden\-Microsoft Plug\-, wenden Sie sich an den Verleger Informationen. Weitere Informationen zu Plug-Ins\-ins finden Sie unter [wie anschließen\-ins funktionieren](cluster-aware-updating-plug-ins.md).   

## <a name="BKMK_REQ_CLUS"></a>Installieren Sie das Feature "Failoverclustering" und der Failoverclustering-Tools  
Für das clusterfähige Aktualisieren ist die Installation des Failoverclustering-Features und der Failoverclusteringtools erforderlich. Die Failoverclusteringtools umfassen die CAU-Tools \(clusterawareupdating.dll\), das Cmdlets für Failoverclustering und andere Komponenten, die für Clusterfähige Aktualisierungsvorgänge erforderlich sind. Schritte zum Installieren des Failoverclustering-Features finden Sie unter [Installieren des Failoverclustering-Features und der Failoverclusteringtools](create-failover-cluster.md#install-the-failover-clustering-feature).  

Hängen Sie, dass die genauen Installationsanforderungen für die Failoverclustering-Tools gibt an, ob Sie das Koordinieren von Updates durch clusterfähiges aktualisieren als Clusterrolle auf dem Failovercluster \(mithilfe von Self-Service\-Updatemodus\) oder von einem Remotecomputer aus. Die Self\-Updatemodus von CAU darüber hinaus erfordert die Installation der Clusterrolle für clusterfähiges aktualisieren für den Failovercluster mithilfe der CAU-Tools.    

In der folgenden Tabelle werden die Installationsanforderungen des Features für clusterfähiges Aktualisieren für die beiden Aktualisierungsmodi für clusterfähiges Aktualisieren zusammengefasst.  

|Installierte Komponente|Self\-Updatemodus|Remote\-Updatemodus|  
|-----------------------|-----------------------|-------------------------|  
|Failoverclustering-Feature|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|  
|Failoverclusteringtools|Auf allen Clusterknoten erforderlich|-Required auf\-Computer aktualisieren<br />– Erforderlich für alle Knoten des Clusters zum Ausführen der [Save-CauDebugTrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) Cmdlet|  
|Clusterrolle für clusterfähiges Aktualisieren|Erforderlich|Nicht erforderlich|  

## <a name="obtain-an-administrator-account"></a>Anfordern eines Administratorkontos  
Die folgenden Administratoranforderungen sind zur Verwendung der Features für clusterfähiges Aktualisieren erforderlich.  

-   Um eine Vorschau oder Anwenden von Updates mithilfe der Benutzeroberfläche für clusterfähiges aktualisieren \(UI\) , oder der Cluster-Aware Updating-Cmdlets verwenden Sie ein Domänenkonto, das über lokale Administratorrechte und Berechtigungen auf allen Clusterknoten verfügt. Wenn das Konto auf jedem Knoten über ausreichende Berechtigungen besitzt, werden Sie im Fenster des clusterfähigen Aktualisierens aufgefordert, die erforderlichen Anmeldeinformationen angeben, wenn Sie diese Aktionen ausführen. Verwenden der [Cluster-Aware Updating](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps) -Cmdlets können Sie die erforderlichen Anmeldeinformationen als Cmdlet-Parameter angeben.  

-   Bei Verwendung von CAU in Remotebüros\-Modus aktualisieren, wenn Sie sich mit einem Konto angemeldet sind, das lokale Administratorrechte und Berechtigungen auf den Clusterknoten keine, müssen Sie die CAU-Tools als Administrator ausführen, mithilfe eines lokalen Administratorkontos auf den Koordinator Computer aktualisieren oder mithilfe ein Kontos mit der **annehmen der Clientidentität nach Authentifizierung** verfügen. 

-   Führen Sie Best Practices Analyzer für CAU müssen Sie ein Konto mit Administratorberechtigungen auf den Clusterknoten und lokale Administratorrechte auf dem Computer, die verwendet wird, zum Ausführen mit der [Test-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Cmdlets oder zum Analysieren der Verwenden des Fensters des clusterfähigen Aktualisierens updatebereitschaft des Clusters. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft des Clusters](#BKMK_BPA).  

## <a name="verify-the-cluster-configuration"></a>Überprüfen der Clusterkonfiguration  
Nachfolgend sind allgemeine Anforderungen an einen Failovercluster zum Unterstützen von Updates mithilfe des clusterfähigen Aktualisierens aufgeführt. Weitere Konfigurationsanforderungen für die Remoteverwaltung auf den Knoten finden Sie weiter unten in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG) .  

-   Es müssen ausreichend Clusterknoten online sein, damit der Cluster das Quorum besitzt.  

-   Alle Clusterknoten müssen sich in derselben Active Directory-Domäne befinden.  

-   Der Clustername muss im Netzwerk mithilfe von DNS aufgelöst werden.  

-   Wenn für clusterfähiges aktualisieren, in Remotebüros verwendet wird\-Updatemodus an, die Computer des Updatekoordinators müssen über eine Netzwerkverbindung mit den Failover-Clusterknoten, und es muss sich in derselben Active Directory-Domäne wie der Failovercluster.  

-   Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden. Dieser Dienst wird standardmäßig auf allen Clusterknoten installiert und für den automatischen Start konfiguriert.  

-   Verwenden von PowerShell vor\-aktualisieren oder nach\-aktualisieren Sie Skripts während einer Updateausführung für Clusterfähiges aktualisieren, stellen Sie sicher, dass die Skripts auf allen Clusterknoten installiert oder für alle Knoten, z. B. über eine Netzwerkdateifreigabe mit hoher Verfügbarkeit zugänglich sind. Wenn Skripts auf einer Netzwerkdateifreigabe gespeichert werden, konfigurieren Sie den Ordner für die Gruppe "Alle" für die Berechtigung "Lesen".  

## <a name="BKMK_NODE_CONFIG"></a>Konfigurieren Sie die Knoten für die Remoteverwaltung  
Um Cluster-Aware Updating verwenden zu können, müssen alle Knoten des Clusters für die Remoteverwaltung konfiguriert werden. In der Standardeinstellung die einzige Aufgabe Sie müssen ausführen, um die Knoten zu konfigurieren, für die Remoteverwaltung ist [Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW). 

Die folgende Tabelle enthält die vollständige remote Management-Anforderungen, für den Fall, dass Ihre Umgebung von den Standardwerten abweicht.

Diese Anforderungen treten zusätzlich zu den Installationsanforderungen für [Installieren des Failoverclustering-Features und der Failoverclusteringtools](#BKMK_REQ_CLUS) und zu den allgemeinen Anforderungen auf, die in vorherigen Abschnitten dieses Themas beschrieben werden.  

|Anforderung|Standardstatus|Self\-Updatemodus|Remote\-Updatemodus|  
|---------------|---|-----------------------|-------------------------|  
|[Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW)|Disabled|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|  
|[Aktivieren der Windows-Verwaltungsinstrumentation](#BKMK_WMI)|Enabled|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|  
|[Aktivieren Sie Windows PowerShell 3.0 oder 4.0 und Windows PowerShell-remoting](#BKMK_PS)|Enabled|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten muss Folgendes ausgeführt werden:<br /><br />– Die [Save-CauDebugTrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) Cmdlet<br />-PowerShell vor\-aktualisieren und buchen\-aktualisieren Sie Skripts während einer Updateausführung<br />-Tests mithilfe des Fensters des clusterfähigen Aktualisierens updatebereitschaft des Clusters oder [Test\-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell-Cmdlet|  
|[Installieren Sie .NET Framework 4.6 oder 4.5](#BKMK_NET)|Enabled|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten muss Folgendes ausgeführt werden:<br /><br />– Die [Save-CauDebugTrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) Cmdlet<br />-PowerShell vor\-aktualisieren und buchen\-aktualisieren Sie Skripts während einer Updateausführung<br />-Tests mithilfe des Fensters des clusterfähigen Aktualisierens updatebereitschaft des Clusters oder [Test\-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell-Cmdlet|  

### <a name="BKMK_FW"></a>Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts  
Zum Zulassen automatischer Neustarts, nachdem die Updates angewendet werden \(, wenn die Installation eines Updates einen Neustart erfordert\), wenn Windows-Firewall oder einen nicht\-Microsoft-Firewall auf den Clusterknoten verwendet wird, eine Firewallregel muss aktiviert sein, auf Jeder Knoten, die der folgenden Datenverkehr zulässt:  

-   Protokoll: TCP  

-   Richtung: Eingehend  

-   Programm: wininit.exe  

-   Ports: Dynamische RPC-Ports  

-   Profil: Domäne  

Wenn die Windows-Firewall auf den Clusterknoten verwendet wird, können Sie dazu die Regelgruppe **Remotecomputer herunterfahren** der Windows-Firewall auf den einzelnen Clusterknoten aktivieren. Bei Verwendung des Fensters des clusterfähigen Aktualisierens zum Anwenden der Updates und das Self-Service konfigurieren\-aktualisieren die Optionen, die **Remoteherunterfahren** Windows-Firewall-Regelgruppe wird automatisch auf allen Clusterknoten aktiviert.  

> [!NOTE]  
> Die Regelgruppe **Remote Shutdown** der Windows-Firewall kann nicht aktiviert werden, wenn sie mit Gruppenrichtlinieneinstellungen in Konflikt steht, die für die Windows-Firewall konfiguriert sind.    

Die **Remotecomputer herunterfahren** firewallregelgruppe ist ebenfalls aktiviert, durch Angabe der **– EnableFirewallRules** Parameter beim Ausführen der folgenden Cmdlets für clusterfähiges aktualisieren: [Hinzufügen-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps), [Invoke-CauRun](https://docs.microsoft.com/powershell/module/clusterawareupdating/Invoke-CauRun?view=win10-ps), und [SetCauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole?view=win10-ps).  

Das folgende PowerShell-Beispiel zeigt eine weitere Methode zum Aktivieren automatischer Neustarts auf einem Clusterknoten.  

```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>Aktivieren der Windows-Verwaltungsinstrumentation (WMI) 
Alle Knoten des Clusters müssen konfiguriert werden, für die Remoteverwaltung mit der Windows-Verwaltungsinstrumentation \(WMI\). Diese Option ist standardmäßig aktiviert.  

Gehen Sie wie folgt vor, um die Remoteverwaltung manuell zu aktivieren:  

1.  Starten Sie in der Konsole "Dienste" den Dienst **Windows-Remoteverwaltung** , und legen Sie für den Starttyp **Automatisch**fest.  

2.  Führen Sie die [Set-WSManQuickConfig](https://docs.microsoft.com/powershell/module/Microsoft.WsMan.Management/Set-WSManQuickConfig?view=powershell-6) Cmdlet oder führen Sie den folgenden Befehl an einer erhöhten Eingabeaufforderung:  

    ```PowerShell  
    winrm quickconfig -q  
    ```  

Um WMI-Remoting unterstützen, wenn es sich bei Windows-Firewall auf den Clusterknoten verwendet wird, die eingehende Firewallregel für **Windows Remote Management \(HTTP\-In\)**  muss auf jedem Knoten aktiviert sein.  Diese Regel ist standardmäßig aktiviert.  

### <a name="BKMK_PS"></a>Aktivieren Sie Windows PowerShell und Windows PowerShell-remoting  
So aktivieren Sie Self-Service\-aktualisieren-Modus und bestimmte Features für clusterfähiges aktualisieren in Remotebüros\-Updatemodus, PowerShell muss installiert und zum Ausführen von Remotebefehlen auf allen Clusterknoten aktiviert. Standardmäßig ist PowerShell installiert und für das Remoting aktiviert.  

Um PowerShell-Remoting zu aktivieren, verwenden Sie eine der folgenden Methoden:  

-   Führen Sie die [Enable-PSRemoting](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enable-PSRemoting) Cmdlet.  

-   Konfigurieren Sie eine Domäne\-Ebene der Einstellung der Gruppenrichtlinie für die Windows-Remoteverwaltung \(WinRM\).  

Weitere Informationen zum Aktivieren der PowerShell-Remoting finden Sie unter [Informationen zu Remoteanforderungen](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements?view=powershell-6).  

### <a name="BKMK_NET"></a>Installieren Sie .NET Framework 4.6 oder 4.5  
So aktivieren Sie Self-Service\-aktualisieren-Modus und bestimmte Features für clusterfähiges aktualisieren in Remotebüros\-Aktualisierung Modus, den .NET Framework 4.6 oder .NET Framework 4.5 (auf Windows Server 2012 R2) muss auf allen Clusterknoten installiert sein. Standardmäßig ist .NET Framework installiert.  

Zum Installieren von .NET Framework 4.6 (oder 4.5) mithilfe von PowerShell, wenn sie noch nicht installiert ist, verwenden Sie den folgenden Befehl aus:

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>Best practices-Empfehlungen für die Verwendung des clusterfähigen Aktualisierens 

### <a name="BKMK_BP_WUA"></a>Empfehlungen zum Anwenden von Microsoft-updates

Wird empfohlen, bei der Sie beginnen, Anwenden von Updates mit der standardmäßigen Verwendung von CAU **Microsoft.WindowsUpdatePlugin** anschließen\-im in einem Cluster, beenden Sie mit anderen Methoden zum Installieren von Softwareupdates von Microsoft auf dem Cluster Knoten.  

> [!CAUTION]  
> CAU mit Methoden, mit denen einzelne Knoten automatisch aktualisiert kombiniert \(auf einem festen Zeitplan\) kann zu unvorhersehbaren Ergebnissen wie dienstunterbrechungen oder ungeplanter Downtime führen.  

Empfohlene Richtlinien:  

-   Um die besten Ergebnisse zu erzielen, empfiehlt es sich, dass Sie Einstellungen auf dem Clusterknoten für die automatische Aktualisierung deaktivieren, z. B. über die Einstellungen für automatische Updates in der Systemsteuerung oder über die Einstellungen, die mithilfe der Gruppenrichtlinie konfiguriert werden.  

    > [!CAUTION]  
    > Die automatische Installation von Updates auf den Clusterknoten kann die Installation von Updates durch clusterfähiges Aktualisieren beeinträchtigen und somit beim clusterfähigen Aktualisieren zu Fehlern führen.  

    Die folgenden Einstellungen für automatische Updates sind (sofern erforderlich) mit dem clusterfähigen Aktualisieren kompatibel, da der Administrator die zeitliche Abfolge der Updateinstallation steuern kann.  

    -   Einstellungen zur Benachrichtigung vor dem Herunterladen von Updates und zur Benachrichtigung vor der Installation  

    -   Einstellungen zum automatischen Herunterladen von Updates und zur Benachrichtigung vor der Installation  

    Wenn die Option "Automatische Updates" Updates jedoch zur selben Zeit wie eine Updateausführung für clusterfähiges Aktualisieren herunterlädt, kann die Updateausführung möglicherweise länger dauern.  

-   Konfigurieren ein aktualisierungssystems, wie z. B. Windows Server Update Services nicht \(WSUS\) das automatische Anwenden von Updates \(auf einem festen Zeitplan\) Clusterknoten.  

-   Alle Clusterknoten müssen einheitlich für die Verwendung derselben Updatequelle konfiguriert sein, z. B. WSUS-Server, Windows-Update oder Microsoft Update.  

-   Schließen Sie Clusterknoten von allen erforderlichen oder automatischen Updates aus, wenn Sie Softwareupdates mithilfe eines Konfigurationsverwaltungssystems auf Computer im Netzwerk anwenden. Beispiele für Konfigurationsverwaltungssysteme sind Microsoft System Center Configuration Manager 2007 und Microsoft System Center Virtual Machine Manager 2008.  

-   Wenn internen softwareverteilungsservern \(z. B. WSUS-Server\) werden verwendet, um enthalten und die Updates bereitstellen, stellen Sie sicher, dass die genehmigten Updates für die Clusterknoten in diesen Servern ordnungsgemäß identifizieren.  

#### <a name="BKMK_PROXY"></a>Anwenden von Microsoft-Updates in filialszenarien  
Wenn Sie in bestimmten Filialszenarien Microsoft-Updates über Microsoft Update oder Windows Update auf Clusterknoten herunterladen möchten, müssen Sie möglicherweise auf jedem Knoten Proxyeinstellungen für das lokale Systemkonto konfigurieren. Dies kann z. B. erforderlich sein, wenn die Filialcluster auf Microsoft Update oder Windows Update zugreifen, um Updates mithilfe eines lokalen Proxyservers herunterzuladen.  

Konfigurieren Sie bei Bedarf die WinHTTP-Proxyeinstellungen auf jedem Knoten aus, geben einen lokalen Proxyserver und Konfigurieren von lokalen adressausnahmen \(d. h. eine Umgehungsliste für lokale Adressen\). Dazu können Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten auf den einzelnen Clusterknoten ausführen:  

```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  

wobei <*ProxyServerFQDN*> wird von der vollständig qualifizierten Domänennamen für den Proxyserver und <*Port*> ist der Port für die Kommunikation (üblicherweise port 443).  

Beispielsweise, um WinHTTP-Proxyeinstellungen für das lokale Systemkonto, das den Proxyserver konfigurieren *MyProxy.CONTOSO.com*mit Port 443 und lokale adressausnahmen, geben Sie den folgenden Befehl aus:  

```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  

### <a name="BKMK_BP_HF"></a>Empfehlungen zur Verwendung von Microsoft.HotfixPlugin  

-   Es wird empfohlen, dass Sie Berechtigungen im Hotfixstammordner und in der Hotfixkonfigurationsdatei konfigurieren, um den Schreibzugriff nur auf lokale Administratoren auf den Computer zu beschränken, die zum Speichern dieser Dateien verwendet werden. Dadurch können Manipulationen an diesen Dateien durch nicht berechtigte Benutzer verhindert werden, die die Funktionalität des Failoverclusters beeinträchtigen könnten, wenn Hotfixes angewendet werden.  

-   Um sicherzustellen, dass die Integrität der Daten für Server Message Block \(SMB\) Verbindungen, die für den Zugriff auf den hotfixstammordner, sollten Sie SMB-Verschlüsselung in konfigurieren den freigegebenen SMB-Ordner, wenn es möglich ist. **Microsoft.HotfixPlugin** erfordert, dass die SMB-Signatur oder SMB-Verschlüsselung konfiguriert ist, um die Datenintegrität für SMB-Verbindungen sicherzustellen. 

    Weitere Informationen finden Sie unter [Beschränken des Zugriffs auf den hotfixstammordner und die hotfixkonfigurationsdatei](cluster-aware-updating-plug-ins.md#BKMK_ACL).

### <a name="additional-recommendations"></a>Weitere Empfehlungen  

-   Um Konflikte mit einer Updateausführung für clusterfähiges Aktualisieren zu vermeiden, die möglicherweise für den gleichen Zeitpunkt vorgesehen sind, planen Sie während der geplanten Wartungszeitfenster keine Kennwortänderungen für Clusternamenobjekte und virtuelle Computerobjekte.  

-   Sie sollten die entsprechende Berechtigungen festlegen, auf Pre\-aktualisieren und buchen\-Aktualisierung von Skripts, die im Netzwerk gespeichert werden freigegebene Ordner, um zu verhindern, mögliche Manipulationen an diesen Dateien durch nicht autorisierte Benutzer.  

-   So konfigurieren Sie für clusterfähiges aktualisieren im selbst\-Updatemodus an, ein virtuelles Computerobjekt \(VCO\) für die CAU-Clusterrolle muss in Active Directory erstellt werden. Dieses Objekt kann durch das clusterfähige Aktualisieren automatisch zu dem Zeitpunkt erstellt werden, zu dem die Clusterrolle für clusterfähiges Aktualisieren hinzugefügt wird, wenn der Failovercluster über die entsprechenden Berechtigungen verfügt. Aufgrund der Sicherheitsrichtlinien in einigen Organisationen ist es möglicherweise erforderlich, das Objekt in Active Directory vorab bereitzustellen. Das entsprechende Verfahren hierfür finden Sie unter [Schritte für die Vorabbereitstellung eines Kontos für eine Clusterrolle](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002\(v=ws.10\)#steps-for-prestaging-the-cluster-name-account).  

-   Sie können Profile für die Updateausführung erstellen, um Updateausführungseinstellungen für verschiedene Failovercluster mit ähnlichen Aktualisierungsanforderungen in der IT-Organisation zu speichern und wiederzuverwenden. In Abhängigkeit vom Aktualisierungsmodus können Sie die Updateausführungsprofile zusätzlich auf einer Dateifreigabe speichern und verwalten, auf die alle Remotecomputer für den Updatekoordinator oder die Failovercluster zugreifen können. Weitere Informationen finden Sie unter [erweiterte Optionen und Updateausführungsprofile für CAU](cluster-aware-updating-options.md).  

## <a name="BKMK_BPA"></a>Testen der updatebereitschaft des Clusters  
Sie können den Best Practices Analyzer für CAU ausführen \(BPA\) Modell zu prüfen, ob es sich bei einem Failovercluster und die Netzwerkumgebung erfüllen viele Anforderungen von Softwareupdates über clusterfähiges aktualisieren angewendet haben. Viele dieser Tests prüfen die Umgebung auf die Bereitschaft zur Anwendung von Microsoft-Updates mithilfe des Standard-Steckers\-in **Microsoft.WindowsUpdatePlugin**.  

> [!NOTE]  
> Möglicherweise müssen Sie unabhängig voneinander überprüfen, ob Ihre Clusterumgebung bereit zum Anwenden von Softwareupdates mithilfe einer Plug\-in anderen als **Microsoft.WindowsUpdatePlugin**. Wenn Sie einen nicht verwenden\-Microsoft Plug\-, z. B. ein von Ihrem Hardwarehersteller bereitgestellten wenden Sie sich an den Verleger Weitere Informationen.  

Zum Ausführen des Best Practices Analyzer (BPA) haben Sie die folgenden beiden Möglichkeiten:  

1.  Wählen Sie in der Konsole für clusterfähiges Aktualisieren die Option **Vorbereitung auf das Clusterupdate analysieren** aus. Nachdem der BPA die Bereitschaftstests abgeschlossen hat, wird ein Testbericht angezeigt. Wenn auf den Clusterknoten Probleme aufgetreten sind, werden die bestimmten Probleme und die betroffenen Knoten identifiziert, damit Sie entsprechende Korrekturmaßnahmen ergreifen können. Diese Tests können einige Minuten dauern.  

2.  Führen Sie die [Test-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup) Cmdlet. Sie können das Cmdlet auf einem Computer lokal oder remote ausführen, auf denen die Failover-Clustering-Modul für Windows PowerShell (Teil der Failoverclustering-Tools) installiert ist. Sie können das Cmdlet auch auf einem Knoten des Failoverclusters ausführen.  

> [!NOTE]  
> -   Verwenden Sie das Konto, die über Administratorrechte auf den Clusterknoten und lokale Administratorrechte auf dem Computer, die verwendet wird, zum Ausführen der **Test\-CauSetup** Cmdlets oder zum Analysieren der updatebereitschaft des Clusters Verwenden des Cluster-Aware Updating-Fensters. Zum Ausführen der Tests, die mithilfe des Cluster-Aware Updating-Fensters müssen Sie auf dem Computer mit den erforderlichen Anmeldeinformationen angemeldet sein.  
> -   Bei den Tests wird angenommen, dass die Tools für clusterfähiges Aktualisieren, die zum Anzeigen einer Updatevorschau oder zum Anwenden von Updates verwendet werden, auf demselben Computer und mit denselben Anmeldeinformationen ausgeführt werden, die zum Testen der Updatebereitschaft des Clusters verwendet werden.  

> [!IMPORTANT]  
> Es wird dringend empfohlen, dass Sie die Cluster in den folgenden Situationen auf die Updatebereitschaft testen:  
>   
> -   Bevor Sie das clusterfähige Aktualisieren zum ersten Mal zum Anwenden von Softwareupdates verwenden können.  
> -   Nachdem Sie einen Knoten zum Cluster hinzugefügt oder andere Hardwareänderungen am Cluster vorgenommen haben, die die Ausführung des Assistenten zum Überprüfen von Clustern erfordern.  
> -   Nachdem Sie eine Updatequelle oder updateeinstellungen Konfigurationen oder \(als CAU\) , die Auswirkungen auf die Anwendung von Updates auf den Knoten.  

### <a name="tests-for-cluster-updating-readiness"></a>Tests für die Updatebereitschaft des Clusters  
In der folgenden Tabelle sind die Tests für die Updatebereitschaft des Clusters, einige allgemeine Probleme sowie Schritte zur Behebung dieser Probleme aufgeführt.  


|                                                      Test                                                      |                                                                                                                                               Mögliche Probleme und Auswirkungen                                                                                                                                               |                                                                                                                                                                                         Lösungsschritte                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                     Der Failovercluster muss verfügbar sein.                                     |                                                                                       Der Failoverclustername kann nicht aufgelöst werden oder der Zugriff ist auf mindestens einen Clusterknoten nicht möglich. Der BPA kann die Clusterbereitschaftstests nicht ausführen.                                                                                        |                                                                   -Überprüfen Sie die Schreibweise des Namens des Clusters während der BPA-Ausführung angegeben wurde.<br />-Stellen Sie sicher, dass alle Knoten des Clusters online und aktiv sind.<br />-Überprüfen Sie, dass es sich bei den Konfigurationsüberprüfungs-Assistenten erfolgreich auf dem Failovercluster ausführen können.                                                                    |
|                    Die Failoverclusterknoten müssen über die Windows-Verwaltungsinstrumentation (WMI) für die Remoteverwaltung aktiviert sein.                    |                                                Mindestens ein Failoverclusterknoten sind nicht für die Remoteverwaltung mithilfe von Windows-Verwaltungsinstrumentation aktiviert \(WMI\). Die Clusterknoten können nicht über das clusterfähige Aktualisieren aktualisiert werden, wenn die Knoten nicht für die Remoteverwaltung konfiguriert sind.                                                 |                                                                                                  Stellen Sie sicher, dass alle Failoverclusterknoten über die WMI für die Remoteverwaltung aktiviert wurden. Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                                                   |
|                      PowerShell-Remoting muss auf jedem Failoverclusterknoten aktiviert sein                       |                                                           PowerShell ist nicht installiert oder ist nicht für das Remoting auf mindestens ein Failoverclusterknoten aktiviert. CAU kann nicht konfiguriert werden, für sich selbst\-Updatemodus an, oder verwenden Sie bestimmte Features in Remotebüros\-Updatemodus.                                                            |                                                                                             Stellen Sie sicher, dass PowerShell auf allen Clusterknoten installiert ist und für das Remoting aktiviert ist.<br /><br />Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                                             |
|                                            Failoverclusterversion                                            |                                                                            Einen oder mehrere Knoten im Failovercluster nicht Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden. Der Failovercluster kann nicht mithilfe des clusterfähigen Aktualisierens aktualisiert werden.                                                                             |                                                                   Stellen Sie sicher, dass der Failovercluster, der während der BPA-Ausführung angegeben wird, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.<br /><br />Weitere Informationen finden Sie unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS) in diesem Thema.                                                                   |
| Die erforderlichen Versionen von .NET Framework und Windows PowerShell müssen auf allen Failoverclusterknoten installiert werden. |                                                                                              .NET Framework 4.6 4.5 oder Windows PowerShell ist nicht auf eine oder mehrere Clusterknoten installiert. Möglicherweise funktionieren einige Features für das clusterfähige Aktualisieren nicht.                                                                                              |                                                                            Stellen Sie sicher, dass .NET Framework 4.6 oder 4.5 und Windows PowerShell auf allen Clusterknoten installiert werden, wenn sie erforderlich sind.<br /><br />Weitere Informationen finden Sie in diesem Thema unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG).                                                                             |
|                           Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden.                           |                                                                                                            Der Clusterdienst wird auf mindestens einem Knoten nicht ausgeführt. Der Failovercluster kann nicht mithilfe des clusterfähigen Aktualisierens aktualisiert werden.                                                                                                             |                        -Sicherstellen, dass den Clusterdienst \(Clussvc\) auf allen Knoten im Cluster gestartet wird und für den automatischen start konfiguriert ist.<br />-Überprüfen Sie, dass es sich bei den Konfigurationsüberprüfungs-Assistenten erfolgreich auf dem Failovercluster ausführen können.<br /><br />Weitere Informationen finden Sie unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS) in diesem Thema.                         |
|     Automatische Updates dürfen nicht für die automatische Installation von Updates auf beliebigen Failoverclusterknoten konfiguriert werden.     |                                           Auf mindestens einem Failoverclusterknoten sind automatische Updates für die automatische Installation von Microsoft-Updates auf diesem Knoten konfiguriert. Die Kombination des clusterfähigen Aktualisierens mit anderen Aktualisierungsmethoden kann zu ungeplanter Downtime oder zu unvorhergesehenen Ergebnissen führen.                                            |                                                     Wenn die Windows Update-Funktionalität auf mindestens einem Clusterknoten für automatische Updates konfiguriert ist, stellen Sie sicher, dass automatische Updates nicht für die automatische Installation von Updates konfiguriert sind.<br /><br />Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).                                                     |
|                          Die Failoverclusterknoten müssen dieselbe Updatequelle verwenden.                          |                                                    Mindestens ein Failoverclusterknoten ist für die Verwendung einer Updatequelle für Microsoft-Updates konfiguriert, die sich von den restlichen Knoten unterscheidet. Die Updates werden möglicherweise nicht einheitlich über das clusterfähige Aktualisieren auf die Clusterknoten angewendet.                                                    |                                                                        Stellen Sie sicher, dass alle Clusterknoten für die Verwendung derselben Updatequelle konfiguriert sind, z. B. WSUS-Server, Windows-Update oder Microsoft Update.<br /><br />Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).                                                                         |
|       Eine Firewallregel, die das Remoteherunterfahren gestattet, muss auf jedem Knoten im Failovercluster aktiviert werden.       |                 Mindestens ein Failoverclusterknoten verfügt nicht über eine aktivierte Firewallregel, die das Remoteherunterfahren gestattet, oder eine Gruppenrichtlinieneinstellung verhindert, dass diese Regel aktiviert wird. Eine Updateausführung, die Updates anwendet, die einen automatischen Neustart der Knoten erfordern, wurde möglicherweise nicht ordnungsgemäß beendet.                  |                                                                    Wenn Windows-Firewall oder einen nicht\-Microsoft-Firewall wird auf den Clusterknoten, konfigurieren Sie eine Firewallregel, die Remoteherunterfahren gestattet.<br /><br />Weitere Informationen finden Sie unter [Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW) in diesem Thema.                                                                    |
|          Die Proxyservereinstellung muss auf jedem Failoverclusterknoten auf einen lokalen Proxyserver festgelegt werden.          |                             Mindestens ein Failoverclusterknoten weist eine fehlerhafte Proxyserverkonfiguration auf.<br /><br />Wenn ein lokaler Proxyserver verwendet wird, muss die Proxyservereinstellung auf den einzelnen Knoten ordnungsgemäß konfiguriert werden, damit der Cluster auf Microsoft Update oder Windows Update zugreifen kann.                              |                                            Stellen Sie sicher, dass die WinHTTP-Proxyeinstellungen auf allen Clusterknoten auf einem lokalen Proxyserver eingestellt sind, wenn dies erforderlich ist. Wenn in Ihrer Umgebung kein Proxyserver verwendet wird, kann diese Warnung ignoriert werden.<br /><br />Weitere Informationen finden Sie in diesem Thema unter [Anwenden von Updates in Filialszenarien](#BKMK_PROXY).                                            |
|        Die Clusterrolle für clusterfähiges aktualisieren sollten installiert werden, auf dem Failovercluster Self-Service aktivieren\-Updatemodus        |                                                                                                   Die Clusterrolle für clusterfähiges Aktualisieren ist auf diesem Failovercluster nicht installiert. Diese Rolle ist erforderlich, für die Self-Service-cluster\-aktualisieren.                                                                                                   |      Verwendung von CAU in Self-Service\-Updatemodus an, fügen Sie die Clusterrolle für clusterfähiges aktualisieren für den Failovercluster, in einem der folgenden Methoden:<br /><br />– Führen Sie die [Add-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole) PowerShell-Cmdlet.<br />– Aktivieren der **konfigurieren Self-Service-cluster\-Optionen aktualisieren** Aktion im Cluster-Aware Updating-Fenster.      |
|         Die Clusterrolle für clusterfähiges aktualisieren muss auf dem Failovercluster aktiviert werden, um Self-Service zu aktivieren\-Updatemodus         | Die Clusterrolle für clusterfähiges Aktualisieren ist deaktiviert. Z. B. die Clusterrolle für clusterfähiges aktualisieren ist nicht installiert oder diese Funktion wurde mit deaktiviert die [deaktivieren\-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole) PowerShell-Cmdlet. Diese Rolle ist erforderlich, für die Self-Service-cluster\-aktualisieren. | Verwendung von CAU in Self-Service\-Updatemodus an, die Clusterrolle für clusterfähiges aktualisieren auf diesem Failovercluster in einem der folgenden Methoden aktivieren:<br /><br />– Führen Sie die [Enable-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole) PowerShell-Cmdlet.<br />– Aktivieren der **konfigurieren Self-Service-cluster\-Optionen aktualisieren** Aktion im Cluster-Aware Updating-Fenster. |
|      Der konfigurierten CAU-Stecker\-in für sich selbst\-Updatemodus muss auf allen Failoverclusterknoten registriert werden      |                                                              Die Clusterrolle für clusterfähiges aktualisieren auf eine oder mehrere Knoten dieses Failoverclusters kann nicht zugegriffen werden die Plug-Ins für clusterfähiges aktualisieren\-im Modul, das in der eigenen konfiguriert ist\-Optionen aktualisieren. Ein selbstsigniertes\-aktualisieren, führen Sie fehlschlagen.                                                              |           -Stellen Sie sicher, die den konfigurierten CAU-Stecker\-in wird installiert auf allen Clusterknoten anhand der Installationsverfahren für das Produkt, das das Plug-In für clusterfähiges aktualisieren bereitstellt\-in.<br />– Führen Sie die [registrieren\-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell-Cmdlet zum Registrieren des Steckers\-in auf den erforderlichen Clusterknoten.           |
|                Alle Failoverclusterknoten müssen den gleichen Satz von registrierten CAU-Plug &\-ins                 |                                                                             Ein selbstsigniertes\-aktualisieren, führen Sie fehlschlagen, wenn der Stecker\-in, das ist so konfiguriert wird geändert, die in einer Updateausführung verwendet werden, die nicht auf allen Clusterknoten verfügbar ist.                                                                              |           -Stellen Sie sicher, die den konfigurierten CAU-Stecker\-in wird installiert auf allen Clusterknoten anhand der Installationsverfahren für das Produkt, das das Plug-In für clusterfähiges aktualisieren bereitstellt\-in.<br />– Führen Sie die [registrieren\-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell-Cmdlet zum Registrieren des Steckers\-in auf den erforderlichen Clusterknoten.           |
|                               Die konfigurierten Optionen für die Updateausführung müssen gültig sein.                                |                                                                          Die Self\-Aktualisieren von Zeitplan und die Updateausführung Optionen, die für diesen Failovercluster konfiguriert sind sind unvollständig oder sind ungültig. Ein selbstsigniertes\-aktualisieren, führen Sie fehlschlagen.                                                                           |                                                            Konfigurieren eines gültigen\-Zeitplan und die verschiedenen Optionen der Updateausführung wird aktualisiert. Beispielsweise können Sie die [festgelegt\-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole) PowerShell-Cmdlet zum Konfigurieren der CAU-Clusterrolle.                                                            |
|                  Mindestens zwei Failoverclusterknoten müssen Besitzer der Clusterrolle für clusterfähiges Aktualisieren sein.                  |                                                                                        Eine Updateausführung im Self-Service gestartet\-Updatemodus schlägt fehl, da die Clusterrolle für clusterfähiges aktualisieren keinen möglichen Besitzerknoten zu verschieben.                                                                                         |                                                                                                                Stellen Sie mithilfe der Failoverclustering-Tools sicher, dass alle Clusterknoten als mögliche Besitzer der Clusterrolle für clusterfähiges Aktualisieren konfiguriert sind. Hierbei handelt es sich um die Standardkonfiguration.                                                                                                                |
|                  Alle Failoverclusterknoten müssen auf die Windows PowerShell-Skripts zugreifen können.                  |                                                                        Nicht alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren, stehen die konfigurierten Windows PowerShell vor\-aktualisieren und buchen\-Skripts zu aktualisieren. Ein selbstsigniertes\-führen Sie die Aktualisierung schlägt fehl.                                                                        |                                                                                                                    Stellen Sie sicher, dass alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges Aktualisieren über Zugriffsberechtigungen für die konfigurierte PowerShell vor verfügt\-aktualisieren und buchen\-Skripts zu aktualisieren.                                                                                                                     |
|                   Alle Failoverclusterknoten müssen dieselben Windows PowerShell-Skripts verwenden.                   |                                                     Nicht alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren verwenden dieselbe Kopie der angegebenen Windows PowerShell vor\-aktualisieren und buchen\-Skripts zu aktualisieren. Ein selbstsigniertes\-aktualisieren, führen Sie möglicherweise Fehler oder unerwartetes Verhalten.                                                     |                                                                                                                                   Stellen Sie sicher, dass alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren verwenden, die gleiche PowerShell vor\-aktualisieren und buchen\-Skripts zu aktualisieren.                                                                                                                                   |
|         Die Einstellung "WarnAfter", die für die Updateausführung angegeben wurde, muss niedriger sein als die Einstellung "StopAfter".         |                                                                           Die angegebenen Timeoutwerte der Updateausführung für clusterfähiges Aktualisieren sorgen dafür, dass der Warnungstimeout wirkungslos ist. Eine Updateausführung kann möglicherweise abgebrochen werden, bevor ein Warnereignisprotokoll generiert werden kann.                                                                            |                                                                                                                                      Konfigurieren Sie in den Optionen der Updateausführung einen Optionswert für **WarnAfter** , der niedriger als der Optionswert für **StopAfter** ist.                                                                                                                                       |

## <a name="see-also"></a>Siehe auch  

-   [Übersicht über die clusterfähige Aktualisierung](cluster-aware-updating.md)