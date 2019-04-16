---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: Cluster-Aware Updating Anforderungen und best practices
ms.prod: windows-server-threshold
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 4/28/2017
description: "Anforderungen für die Verwendung des clusterfähigen Aktualisierens, Updates auf Clustern unter Windows Server installieren."
ms.openlocfilehash: 8517466d58345077af446c1b2c1e2aeb3b17aaa1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>Cluster-Aware Updating Anforderungen und best practices

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieser Abschnittbeschreibt die Anforderungen und Abhängigkeiten, die erforderlich sind, verwenden [Cluster-Aware Updating](cluster-aware-updating.md) (CAU) zum Anwenden von Updates zu einem Failovercluster unter Windows Server ausgeführt wird.
  
> [!NOTE]  
> Möglicherweise müssen Sie unabhängig voneinander überprüfen, ob Ihre Clusterumgebung bereit zum Anwenden von Updates, wenn Sie ein Remoteverwaltungssoftware-in, als verwenden **Microsoft.WindowsUpdatePlugin**. Wenn Sie eine-Microsoft Remoteverwaltungssoftware-in verwenden, erhalten Sie der Herausgeber den Weitere Informationen. Weitere Informationen zu Remoteverwaltungssoftware-ins finden Sie unter [Funktionsweise Remoteverwaltungssoftware ins](cluster-aware-updating-plug-ins.md).   
  
## <a name="BKMK_REQ_CLUS"></a>Installieren Sie das Feature Failoverclustering und der Failoverclustering-Tools  
CAU ist eine Installation des Failoverclustering-Feature und der Failoverclustering-Tools erforderlich. Die Failoverclusteringtools umfassen die CAU-Tools \(clusterawareupdating.dll\), die Failoverclustering-Cmdlets und anderen Komponenten, die für Clusterfähige Aktualisierungsvorgänge erforderlich sind. Schrittezum Installieren des Failoverclustering-Features finden Sie unter [Installieren des Failoverclustering-Features und Tools](http://go.microsoft.com/fwlink/p/?LinkId=253342).  
  
Die genauen Installationsanforderungen für die Failoverclustering-Tools, hängt davon ab, ob Sie das Koordinieren von Updates durch CAU als Clusterrolle auf dem Failovercluster \ (mithilfe von deren Hilfe aktualisieren Arbeitsplatz\) oder von einem Remotecomputer. Der Modus Aktualisieren von deren Hilfe von CAU erfordert zusätzlich die Installation der Clusterrolle für clusterfähiges aktualisieren auf dem Failovercluster mithilfe der CAU-Tools.    
  
In der folgende Tabelle werden die CAU-Feature-Installationsanforderungen für die beiden aktualisierungsmodi für clusterfähiges aktualisieren zusammengefasst.  
  
|Installierte Komponente|Aktualisieren von deren Hilfe-Modus|Remote\ Remoteaktualisierungsmodus|  
|-----------------------|-----------------------|-------------------------|  
|Failover-Clusterunterstützung|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|  
|Failoverclustering-Tools|Auf allen Clusterknoten erforderlich|-Auf Remote\ Remoteaktualisierungscomputer erforderlich<br />– erforderliche auf alle Knoten des Clusters zum Ausführen der [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) Cmdlet|  
|Clusterrolle für clusterfähiges aktualisieren|Erforderlich|Nicht erforderlich.|  
  
## <a name="obtain-an-administrator-account"></a>Anfordern eines Administratorkontos  
Die folgenden administratoranforderungen sind erforderlich, um die Features für clusterfähiges aktualisieren verwenden.  
  
-   Für die Vorschau oder Anwenden von Updates mithilfe der CAU-Benutzeroberfläche müssen \(UI\) oder die Cmdlets des clusterfähigen Aktualisierens Sie ein Domänenkonto verwenden, das über lokale Administratorrechte und Berechtigungen auf allen Clusterknoten verfügt. Wenn das Konto auf jedem Knoten über ausreichende Berechtigungen besitzt, werden Sie im Fenster des clusterfähigen Aktualisierens aufgefordert, die erforderlichen Anmeldeinformationen angeben, wenn Sie diese Aktionen ausführen. Verwenden der [Cluster-Aware Updating](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating) -Cmdlets können Sie die erforderlichen Anmeldeinformationen als Cmdlet-Parameter angeben.  
  
-   Wenn Sie CAU in Remote\ Remoteaktualisierungsmodus verwenden, wenn Sie sich mit einem Konto angemeldet sind, die lokale Administratorrechte und Berechtigungen auf den Clusterknoten besitzt, müssen Sie die CAU-Tools als Administrator ausführen, mithilfe eines lokalen Administratorkontos auf dem Computer des Updatekoordinators oder mit einem Konto mit den **annehmen der Clientidentität nach Authentifizierung** Benutzerrecht. 
  
-   Zum Ausführen des Best Practices Analyzer von CAU verwenden Sie ein Konto, dessen über Administratorrechte auf den Clusterknoten und lokale Administratorrechte auf dem Computer, mit dem Ausführen, der [Test-CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) Cmdlet oder zum Analysieren der updatebereitschaft des Cluster-Aware Updating Fenster. Weitere Informationen finden Sie unter [Testen der updatebereitschaft des Clusters](#BKMK_BPA).  
  
## <a name="verify-the-cluster-configuration"></a>Überprüfen der Clusterkonfiguration  
Im folgenden sind allgemeine Anforderungen für einen Failovercluster zum Unterstützen von der Verwendung von CAU Updates. Weitere konfigurationsanforderungen für die Remoteverwaltung auf den Knoten finden Sie unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG) weiter unten in diesem Thema.  
  
-   Ausreichend Clusterknoten müssen online sein, damit der Cluster das Quorum besitzt.  
  
-   Alle Clusterknoten müssen in der gleichen Active Directory-Domäne sein.  
  
-   Der Clustername muss im Netzwerk mithilfe von DNS aufgelöst werden.  
  
-   Wenn das clusterfähige aktualisieren im Remoteaktualisierungsmodus Remote\ verwendet wird, benötigen Sie die Computer des Updatekoordinators über Netzwerkkonnektivität zum Knoten Failoverclusters, und es muss sich in derselben Active Directory-Domäne als Failovercluster.  
  
-   Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden. Standardmäßig wird dieser Dienst wird auf allen Clusterknoten installiert und für den automatischen Start konfiguriert ist.  
  
-   Um PowerShell-Skripts für registrierungseintragswert- oder Post\-Update während einer Updateausführung für Clusterfähiges aktualisieren verwenden, stellen Sie sicher, dass die Skripts auf allen Clusterknoten installiert oder für alle Knoten, z.B. auf einer Netzwerkdateifreigabe mit hoher Verfügbarkeit zugänglich sind. Wenn Skripts in einem freigegebenen Netzwerkordner gespeichert werden, konfigurieren Sie den Ordner für die Berechtigung "Lesen" für die jeder Gruppe.  
  
## <a name="BKMK_NODE_CONFIG"></a>Konfigurieren der Knoten für die Remoteverwaltung  
Um Cluster-Aware Updating zu verwenden, müssen alle Knoten des Clusters für die Remoteverwaltung konfiguriert werden. Standardmäßig die einzige Aufgabe erforderlich um die Knoten zu konfigurieren, für die Remoteverwaltung ist [Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW). 

Die folgende Tabelle enthält die vollständige remote Management-Anforderungen für den Fall, dass Ihre Umgebung in den Standardwerten gewissen Grad.

Diese Anforderungen treten zusätzlich zu den Installationsanforderungen für die [installieren Sie das Feature Failoverclustering und der Failoverclustering-Tools](#BKMK_REQ_CLUS) und den allgemeinen Anforderungen, die in den vorherigen Abschnitten in diesem Thema beschrieben werden.  
  
|Anforderung|Standardzustand|Aktualisieren von deren Hilfe-Modus|Remote\ Remoteaktualisierungsmodus|  
|---------------|---|-----------------------|-------------------------|  
|[Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW)|Deaktiviert|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|Auf allen Clusterknoten erforderlich, wenn eine Firewall verwendet wird|  
|[Aktivieren von Windows-Verwaltungsinstrumentation](#BKMK_WMI)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich|  
|[Aktivieren Sie Windows PowerShell 3.0 oder 4.0 und Windows PowerShell-remoting](#BKMK_PS)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich, auf den folgenden Befehl ausführen:<br /><br />-Das [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) Cmdlet<br />-PowerShell Skripts registrierungseintragswert- und Post\-Update haben während einer Updateausführung<br />-Tests mit dem Fenster des clusterfähigen Aktualisierens updatebereitschaft des Clusters oder den [Test-CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) Windows PowerShell-Cmdlet|  
|[Installieren Sie .NET Framework 4.6 oder 4.5](#BKMK_NET)|Aktiviert|Auf allen Clusterknoten erforderlich|Auf allen Clusterknoten erforderlich, auf den folgenden Befehl ausführen:<br /><br />-Das [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) Cmdlet<br />-PowerShell Skripts registrierungseintragswert- und Post\-Update haben während einer Updateausführung<br />-Tests mit dem Fenster des clusterfähigen Aktualisierens updatebereitschaft des Clusters oder den [Test-CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) Windows PowerShell-Cmdlet|  

### <a name="BKMK_FW"></a>Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts  
Zum Zulassen automatischer Neustarts nach Updates der Anwendung \ (wenn die Installation eines Updates eine Restart erforderlich ist), wenn Windows-Firewall oder eine von Microsoft stammende Firewall auf den Clusterknoten verwendet wird, muss eine Firewallregel aktiviert werden, auf jedem Knoten, die der folgenden Datenverkehr zulässt:  
  
-   Protokoll: TCP  
  
-   Richtung: eingehende  
  
-   Programm: wininit.exe  
  
-   Ports: Dynamische RPC-Ports  
  
-   Profil: Domäne  
  
Wenn Windows-Firewall auf den Clusterknoten verwendet wird, können Sie dies tun, indem Sie aktivieren die **Remoteherunterfahren** Regelgruppe für Windows-Firewall auf den einzelnen Knoten. Bei Verwendung der das Fenster des clusterfähigen Aktualisierens zum Anwenden von Updates und deren Hilfe aktualisieren Optionen Konfigurieren der **Remoteherunterfahren** Regelgruppe für Windows-Firewall automatisch auf allen Clusterknoten aktiviert ist.  
  
> [!NOTE]  
> Die **Remoteherunterfahren** Regelgruppe für Windows-Firewall kann nicht aktiviert werden, wenn es mit Gruppenrichtlinien in Konflikt Gerät, die für Windows-Firewall konfiguriert sind.    
  
Die **Remotecomputer herunterfahren** Firewallregelgruppe aktiviert durch Angabe der **– EnableFirewallRules** Parameter beim Ausführen der folgenden Cmdlets für clusterfähiges aktualisieren: [Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole), [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan), und [SetCauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole).  
  
Das folgende PowerShell-Beispiel zeigt eine weitere Methode, um automatische Neustarts auf einem Clusterknoten aktivieren.  
  
```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>Aktivieren von Windows-Verwaltungsinstrumentation (WMI) 
Alle Clusterknoten müssen für die Remoteverwaltung mithilfe von Windows-Verwaltungsinstrumentation \(WMI\) konfiguriert werden. Dies ist standardmäßig aktiviert.  
  
Führen Sie folgende Schritteaus, um die Remoteverwaltung manuell zu aktivieren:  
  
1.  Starten Sie in der Konsole Dienste die **Windows Remote Management** Service und legen Sie den Starttyp auf **automatische**.  
  
2.  Führen Sie die [Set-WSManQuickConfig](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.wsman.management/set-wsmanquickconfig) Cmdlets oder führen Sie folgenden Befehl an einer mit erhöhten Rechten aufgefordert:  
  
    ```PowerShell  
    winrm quickconfig -q  
    ```  
  
Um WMI-Remoting zu unterstützen, wenn Windows-Firewall auf den Clusterknoten verwendet wird, die eingehende Firewallregel für **Windows Remote Management \(HTTP\-In\)** muss auf jedem Knoten aktiviert sein.  Standardmäßig wird diese Regel aktiviert.  
  
### <a name="BKMK_PS"></a>Aktivieren Sie Windows PowerShell und Windows PowerShell-remoting  
PowerShell muss installiert und zum Ausführen von Remotebefehlen auf allen Clusterknoten aktiviert werden, um deren Hilfe Remoteaktualisierungsmodus und bestimmte Features für clusterfähiges aktualisieren im Remoteaktualisierungsmodus Remote\ zu aktivieren. Standardmäßig ist PowerShell installiert und für das Remoting aktiviert.  
  
Um PowerShell-Remoting zu aktivieren, verwenden Sie eine der folgenden Methoden:  
  
-   Führen Sie die [Enable-PSRemoting](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) Cmdlet.  
  
-   Konfigurieren Sie eine Domäne\-Level-Gruppenrichtlinie für Windows-Remoteverwaltung \(WinRM\).  
  
Weitere Informationen zum Aktivieren der PowerShell-Remoting finden Sie unter [About\_Remote\_Requirements](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_remote_requirements).  
  
### <a name="BKMK_NET"></a>Installieren Sie .NET Framework 4.6 oder 4.5  
Zum Aktivieren von deren Hilfe Remoteaktualisierungsmodus und bestimmte Features für clusterfähiges aktualisieren im Remoteaktualisierungsmodus Remote\, .NET Framework 4.6 oder .NET Framework 4.5 (unter Windows Server2012 R2) müssen auf allen Clusterknoten installiert werden. Standardmäßig ist .NET Framework installiert.  

So installieren .NET Framework 4.6 (oder 4.5) mithilfe von PowerShell, wenn es nicht bereits installiert ist, verwenden Sie den folgenden Befehl ein:

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>Empfehlung für die Verwendung des clusterfähigen Aktualisierens von Best practices 
  
### <a name="BKMK_BP_WUA"></a>Empfehlungen zum Anwenden von Microsoft-Updates

Es wird empfohlen, die beim CAU verwenden, um das Anwenden von Updates mit der standardmäßigen **Microsoft.WindowsUpdatePlugin** Remoteverwaltungssoftware-in in einem Cluster, das Sie beenden mit anderen Methoden zum Installieren von Softwareupdates von Microsoft auf den Clusterknoten.  
  
> [!CAUTION]  
> Kombinieren von CAU mit Methoden, die einzelne Knoten automatisch aktualisieren \ (auf einem festen Schedule\) können zu unvorhersehbaren Ergebnissen wie dienstunterbrechungen oder ungeplanter Downtime führen.  
  
Es wird empfohlen, dass Sie die folgenden Richtlinien:  
  
-   Um optimale Ergebnisse zu erzielen empfehlen wir, dass Sie Einstellungen auf den Clusterknoten für automatische Updates, z.B. deaktivieren, über die Einstellungen für automatische Updates in der Systemsteuerung oder in den Einstellungen, die mithilfe einer Gruppenrichtlinie konfiguriert werden.  
  
    > [!CAUTION]  
    > Automatische Installation von Updates auf den Clusterknoten kann die Installation von Updates durch clusterfähiges aktualisieren beeinträchtigen und CAU Fehler verursachen kann.  
  
    Wenn sie benötigt werden, sind die folgenden Einstellungen für automatische Updates mit dem clusterfähigen aktualisieren, kompatibel, da der Administrator die zeitliche Abfolge der Updateinstallation steuern kann:  
  
    -   Einstellungen zur Benachrichtigung vor dem Herunterladen von Updates und zur Benachrichtigung vor der Installation  
  
    -   Einstellungen zum automatischen Herunterladen von Updates und zur Benachrichtigung vor der Installation  
  
    Jedoch, wenn automatische Updates Updates zur gleichen Zeit wie eine Updateausführung für Clusterfähiges aktualisieren herunterlädt, kann die Updateausführung länger dauern.  
  
-   Ein UpdateSystem nicht konfigurieren, wie z.B. Windows Server Update Services \(WSUS\) anwenden automatisch aktualisiert \ (auf einem festen Schedule\) für alle Clusterknoten.  
  
-   Alle Knoten des Clusters sollten einheitlich für die Verwendung derselben Updatequelle, z.B. ein WSUS-Server, Windows Update oder Microsoft Update konfiguriert werden.  
  
-   Wenn Sie ein Verwaltungssystem zum Anwenden von Softwareupdates auf Computern im Netzwerk verwenden, schließen Sie Clusterknoten von allen erforderlichen oder automatischen Updates. Beispiele für konfigurationsverwaltungssysteme sind Microsoft System Center Configuration Manager 2007 und Microsoft System Center Virtual Machine Manager 2008.  
  
-   Wenn Software zum internen Verteilungsserver \ (z.B. WSUS Server\) werden verwendet, um enthalten und die Updates bereitstellen, stellen Sie sicher, dass die Server ordnungsgemäß für die Clusterknoten die genehmigten Updates identifizieren.  
  
#### <a name="BKMK_PROXY"></a>Anwenden von Microsoft-Updates in filialszenarien  
Zum Herunterladen von Microsoft-Updates über Microsoft Update oder Windows Update auf Clusterknoten in bestimmten filialszenarien müssen Sie möglicherweise Proxyeinstellungen für das lokale Systemkonto auf jedem Knoten konfigurieren. Beispielsweise müssen Sie dies tun, wenn die filialcluster auf Microsoft Update oder Windows Update zum Herunterladen von Updates mithilfe eines lokalen Proxyservers zugreifen.  
  
Konfigurieren Sie bei Bedarf die WinHTTP-Proxyeinstellungen auf jedem Knoten einen lokalen Proxyserver angeben und Konfigurieren von lokalen adressausnahmen \ (d.h. eine Umgehungsliste für lokale Addresses\). Zu diesem Zweck können Sie eine Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl auf jedem Clusterknoten ausführen:  
  
```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  
  
Wo <*ProxyServerFQDN*> ist für den Proxyserver den vollqualifizierten Domänennamen und <*Port*> ist der Port, über die für die Kommunikation (normalerweise Port 443).  
  
Beispielsweise, um WinHTTP-Proxyeinstellungen für das lokale Systemkonto, das den Proxyserver konfigurieren *MyProxy.CONTOSO.com*mit Port 443 und lokale adressausnahmen, geben Sie folgenden Befehl:  
  
```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  
  
### <a name="BKMK_BP_HF"></a>Empfehlungen zur Verwendung von Microsoft.HotfixPlugin  
  
-   Es wird empfohlen, dass Sie Berechtigungen konfigurieren, in den hotfixstammordner und hotfixkonfigurationsdatei Schreibzugriff auf die nur lokale Administratoren auf dem Computer zu beschränken, die zum Speichern dieser Dateien verwendet werden. Dies verhindert, dass Manipulationen an diesen Dateien durch nicht autorisierte Benutzer, die die Funktionalität des Failoverclusters gefährden könnten, wenn Hotfixes angewendet werden.  
  
-   Um die Integrität der Daten für die Server Message Block \(SMB\) Verbindungen zu gewährleisten, die auf den hotfixstammordner verwendet werden, sollten Sie SMB-Verschlüsselung in den freigegebenen SMB-Ordner konfigurieren, wenn es möglich ist. Die **Microsoft.HotfixPlugin** erfordert, dass die SMB-Signatur oder SMB-Verschlüsselung konfiguriert ist, um die Datenintegrität für SMB-Verbindungen zu gewährleisten. 
  
    Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den hotfixstammordner und die hotfixkonfigurationsdatei](cluster-aware-updating-plug-ins.md#BKMK_ACL).
  
### <a name="additional-recommendations"></a>Zusätzliche Informationen  
  
-   Um zu vermeiden, bei einer Updateausführung für Clusterfähiges aktualisieren, die zur gleichen Zeit geplant werden kann, Planen Sie Kennwortänderungen für Clusterobjekte Namen und virtuelle Computerobjekte nicht während der geplanten Wartungszeitfenster.  
  
-   Sie sollten die entsprechende Berechtigungen auf Skripts registrierungseintragswert- und Post\-Update festlegen, die in freigegebenen Netzwerkordnern zu verhindern, dass mögliche Manipulationen an diesen Dateien durch nicht autorisierte Benutzer gespeichert werden.  
  
-   Zum Konfigurieren von CAU in deren Hilfe Remoteaktualisierungsmodus, ein virtuelles Computerobjekt muss \(VCO\) für die Clusterrolle für clusterfähiges aktualisieren in Active Directory erstellt werden. CAU kann dieses Objekt automatisch zum Zeitpunkt die Clusterrolle für clusterfähiges aktualisieren hinzugefügt wird, bei Erstellen des Failoverclusters über ausreichende Berechtigungen verfügt. Aufgrund der Sicherheitsrichtlinien in einigen Organisationen, kann es jedoch erforderlich, um das Objekt in Active Directory vorab bereitgestellt sein. Eine Anleitung hierzu finden Sie unter [Schrittefür die Vorabbereitstellung eines Kontos für eine Clusterrolle](http://go.microsoft.com/fwlink/p/?LinkId=237624).  
  
-   Zum Speichern und Wiederverwenden von updateausführungseinstellungen für Failovercluster mit ähnlichen aktualisierungsanforderungen in der IT-Organisation Updateausführungsprofile schaffen Sie. Darüber hinaus können Sie Abhängigkeit vom Aktualisierungsmodus, speichern und verwalten die Updateausführungsprofile auf einer Dateifreigabe, die alle Remotecomputer des Updatekoordinators oder Failovercluster zugegriffen werden kann. Weitere Informationen finden Sie unter [erweiterte Optionen und Updateausführungsprofile für CAU](cluster-aware-updating-options.md).  
  
## <a name="BKMK_BPA"></a>Testen der updatebereitschaft des Clusters  
Sie können das Best Practices Analyzer für CAU \(BPA\) Modell zu testen, ob ein Failovercluster ausführen und die Netzwerkumgebung erfüllen zahlreiche Anforderungen für die Softwareupdates von CAU angewendet werden. Viele dieser Tests prüfen die Umgebung für die Bereitschaft für Microsoft-Updates anwenden, indem Sie mithilfe des Remoteverwaltungssoftware-in, **Microsoft.WindowsUpdatePlugin**.  
  
> [!NOTE]  
> Möglicherweise müssen Sie unabhängig voneinander überprüfen, ob Ihre Clusterumgebung bereit zum Anwenden der Softwareupdates mit einem Remoteverwaltungssoftware-in nicht **Microsoft.WindowsUpdatePlugin**. Bei Verwendung eine-Microsoft Remoteverwaltungssoftware-in, z.B. ein vom Hardwarehersteller bereitgestellt, wenden Sie sich an den Herausgeber der Weitere Informationen.  
  
Sie können die BPA in die folgenden beiden Arten ausführen:  
  
1.  Wählen Sie **clusterupdate analysieren** in der Konsole für clusterfähiges aktualisieren. Nachdem der BPA die Bereitschaftstests abgeschlossen hat, wird ein Testbericht angezeigt. Wenn Probleme auf Clusterknoten erkannt werden, sind die spezifischen Probleme und die Knoten, die Probleme angezeigt werden, identifiziert, damit Sie Korrekturmaßnahmen ergreifen können. Die Tests können mehrere Minuten dauern.  
  
2.  Führen Sie die [Test-CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) Cmdlet. Sie können das Cmdlet auf einem lokalen Computer oder Remotecomputer ausführen, auf denen das Failover Clustering-Modul für Windows PowerShell (Teil der Failoverclustering-Tools) installiert ist. Sie können auch das Cmdlet auf einem Knoten des Failoverclusters ausführen.  
  
> [!NOTE]  
> -   Verwenden Sie ein Konto, dessen über Administratorrechte auf den Clusterknoten und lokale Administratorrechte auf dem Computer, mit dem Ausführen, der **Test-CauSetup** Cmdlet oder zum Analysieren der updatebereitschaft des Cluster-Aware Updating Fenster. Führen Sie Tests über das Fenster des clusterfähigen Aktualisierens müssen Sie auf dem Computer mit den erforderlichen Anmeldeinformationen angemeldet sein.  
> -   Die Tests wird davon ausgegangen, dass die CAU-Tools, die Vorschau und das Anwenden von Softwareupdates verwendet werden vom selben Computer und mit den gleichen Anmeldeinformationen ausführen, wie zum Testen der updatebereitschaft des Clusters verwendet werden.  
  
> [!IMPORTANT]  
> Es wird dringend empfohlen, dass Sie den Cluster in den folgenden Situationen die updatebereitschaft testen:  
>   
> -   Bevor Sie clusterfähige aktualisieren zum ersten Mal verwenden, um Softwareupdates anwenden.  
> -   Nachdem Sie einen Knoten zum Cluster hinzufügen oder andere hardwareänderungen im Cluster, die erfordern, Ausführen des Konfigurationsüberprüfungs-Assistenten ausführen.  
> -   Nachdem Sie eine Updatequelle oder ändern, Aktualisieren von Einstellungen oder Konfigurationen \(other than CAU\), die die Anwendung von Updates auf den Knoten auswirken können.  
  
### <a name="tests-for-cluster-updating-readiness"></a>Tests für die updatebereitschaft des Clusters  
Die folgende Tabelle enthält die Clusteraktualisierung Bereitschaftstests, einige allgemeine Probleme sowie Schrittezur Behebung.  
  
|Test|Mögliche Probleme und Auswirkungen|Lösungsschritte|  
|--------|-------------------------------|--------------------|  
|Der Failovercluster muss verfügbar sein.|Kann nicht aufgelöst werden, dass der Failover Cluster-Name oder eine oder mehrere Knoten im Cluster zugegriffen werden können. Der BPA kann nicht die clusterbereitschaftstests nicht ausführen.|– Überprüfen Sie die Schreibweise des Namens des Clusters während der BPA-Ausführung angegeben.<br />– Stellen Sie sicher, dass alle Knoten des Clusters online sind und ausgeführt werden.<br />-Überprüfen Sie, dass die Validate ein Konfigurations-Assistent erfolgreich auf dem Failovercluster ausgeführt werden können.|  
|Die Failoverclusterknoten müssen für die Remoteverwaltung über WMI aktiviert werden|Mindestens ein Failoverclusterknoten sind nicht für die Remoteverwaltung mithilfe von Windows-Verwaltungsinstrumentation \(WMI\) aktiviert. CAU kann Clusterknoten nicht aktualisieren, wenn die Knoten nicht für die Remoteverwaltung konfiguriert sind.|Stellen Sie sicher, dass alle Knoten des Failoverclusters für die Remoteverwaltung über WMI aktiviert sind. Weitere Informationen finden Sie unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG) in diesem Thema.|  
|PowerShell-Remoting muss auf jedem Failoverclusterknoten aktiviert werden|PowerShell ist nicht installiert oder nicht für das Remoting auf mindestens ein Failoverclusterknoten aktiviert ist. CAU kann nicht konfiguriert werden, für deren Hilfe Remoteaktualisierungsmodus oder bestimmte Funktionen in Remote\ Remoteaktualisierungsmodus verwenden.|Stellen Sie sicher, dass PowerShell auf allen Clusterknoten installiert ist und für das Remoting aktiviert ist.<br /><br />Weitere Informationen finden Sie unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG) in diesem Thema.|  
|Failover Cluster-Version|Eine oder mehrere Knoten im Failovercluster ausführen nicht Windows Server2016, Windows Server2012 R2 oder Windows Server2012. CAU kann nicht den Failovercluster aktualisiert werden.|Stellen Sie sicher, dass der Failovercluster, der während der BPA-Ausführung angegeben wird Windows Server2016, Windows Server2012 R2 oder Windows Server2012 ausgeführt wird.<br /><br />Weitere Informationen finden Sie unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS) in diesem Thema.|  
|Die erforderlichen Versionen von .NET Framework und Windows PowerShell müssen auf allen Failoverclusterknoten installiert werden|.NET Framework 4.6 4.5 oder Windows PowerShell ist nicht auf einen oder mehrere Knoten im Cluster installiert. Einige Features für clusterfähiges aktualisieren, funktionieren möglicherweise nicht.|Stellen Sie sicher, dass .NET Framework 4.6 oder 4.5 und Windows PowerShell auf allen Clusterknoten installiert werden, wenn sie erforderlich sind.<br /><br />Weitere Informationen finden Sie unter [Konfigurieren der Knoten für die Remoteverwaltung](#BKMK_NODE_CONFIG) in diesem Thema.|  
|Der Clusterdienst muss auf allen Clusterknoten ausgeführt werden|Der Clusterdienst wird nicht auf einem oder mehreren Knoten ausgeführt. CAU kann nicht den Failovercluster aktualisiert werden.|– Stellen Sie sicher, dass die Cluster-Dienst \(clussvc\) auf allen Knoten im Cluster gestartet wird, für den automatischen Start konfiguriert ist.<br />-Überprüfen Sie, dass die Validate ein Konfigurations-Assistent erfolgreich auf dem Failovercluster ausgeführt werden können.<br /><br />Weitere Informationen finden Sie unter [Überprüfen der Clusterkonfiguration](#BKMK_REQ_CLUS) in diesem Thema.|  
|Automatische Updates müssen nicht konfiguriert werden, um Updates automatisch auf allen Knoten des Failoverclusters zu installieren|Auf mindestens einem Knoten des Failoverclusters ist automatische Updates konfiguriert, um Microsoft-Updates auf diesem Knoten automatisch zu installieren. Kombination des clusterfähigen Aktualisierens mit anderen Aktualisierungsmethoden kann zu ungeplanter Downtime oder zu unvorhersehbaren Ergebnissen führen.|Wenn Windows Update-Funktionalität auf mindestens einem Clusterknoten für automatische Updates konfiguriert ist, stellen Sie sicher, dass automatische Updates nicht für die automatische Installation von Updates konfiguriert ist.<br /><br />Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).|  
|Die Knoten des Failoverclusters sollten derselben Updatequelle verwenden.|Mindestens ein Failoverclusterknoten werden konfiguriert, um die Verwendung einer Updatequelle für Microsoft-Updates, die von den restlichen Knoten unterscheidet. Updates möglicherweise nicht einheitlich auf den Clusterknoten von CAU angewendet.|Stellen Sie sicher, dass alle Clusterknoten für die Verwendung derselben Updatequelle, z.B. ein WSUS-Server, Windows Update oder Microsoft Update konfiguriert ist.<br /><br />Weitere Informationen finden Sie unter [Empfehlungen zum Anwenden von Microsoft-Updates](#BKMK_BP_WUA).|  
|Eine Firewallregel, die Remoteherunterfahren gestattet, sollte auf jedem Knoten im Failovercluster aktiviert werden|Mindestens ein Failoverclusterknoten müssen sich nicht auf eine aktivierte Firewallregel, die Remoteherunterfahren gestattet, oder eine Gruppenrichtlinieneinstellung verhindert, dass diese Regel aktiviert wird. Eine Updateausführung, die Updates angewendet wird, die durch einen Neustart der Knoten automatisch erfordern möglicherweise nicht ordnungsgemäß beendet.|Wenn Windows-Firewall oder eine von Microsoft stammende Firewall auf den Clusterknoten verwendet wird, konfigurieren Sie eine Firewallregel, die Remoteherunterfahren gestattet.<br /><br />Weitere Informationen finden Sie unter [Aktivieren einer Firewallregel zum Zulassen automatischer Neustarts](#BKMK_FW) in diesem Thema.|  
|Die proxyservereinstellung auf jedem Knoten des Failoverclusters sollte auf einen lokalen Proxyserver festgelegt werden|Mindestens ein Failoverclusterknoten haben eine fehlerhafte Proxyserverkonfiguration.<br /><br />Wenn ein lokaler Proxyserver verwendet wird, muss die proxyservereinstellung auf den einzelnen Knoten ordnungsgemäß für den Zugriff auf Microsoft Update oder Windows Update-Cluster konfiguriert werden.|Stellen Sie sicher, dass die WinHTTP-Proxyeinstellungen auf den einzelnen Knoten zu einem lokalen Proxyserver festgelegt werden, wenn dies erforderlich ist. Wenn Sie ein Proxyserver nicht in Ihrer Umgebung verwendet wird, kann diese Warnung ignoriert werden.<br /><br />Weitere Informationen finden Sie unter [Anwenden von Updates in filialszenarien](#BKMK_PROXY) in diesem Thema.|  
|Auf dem Failovercluster Aktivieren des Modus Aktualisieren von deren Hilfe sollte die Clusterrolle für clusterfähiges aktualisieren installiert werden|Die Clusterrolle für clusterfähiges aktualisieren ist auf diesem Failovercluster nicht installiert. Diese Rolle ist für Cluster mit deren Hilfe-Aktualisierung erforderlich.|Um das clusterfähige aktualisieren im Remoteaktualisierungsmodus deren Hilfe verwenden, fügen Sie die Clusterrolle für clusterfähiges aktualisieren auf dem Failovercluster in eine der folgenden Methoden:<br /><br />-Führen Sie die [Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole) PowerShell-Cmdlet.<br />-Wählen Sie die **konfigurieren Sie Cluster Aktualisieren von deren Hilfe Optionen** Aktion im Fenster des clusterfähigen Aktualisierens.|  
|Die CAU-Clusterrolle sollte auf dem Failovercluster aktiviert werden, um deren Hilfe Remoteaktualisierungsmodus zu aktivieren|Die Clusterrolle für clusterfähiges aktualisieren ist deaktiviert. Z.B. die Clusterrolle für clusterfähiges aktualisieren ist nicht installiert oder wurde mithilfe der [Disable-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/disable-cauclusterrole) PowerShell-Cmdlet. Diese Rolle ist für Cluster mit deren Hilfe-Aktualisierung erforderlich.|Um das clusterfähige aktualisieren im Remoteaktualisierungsmodus deren Hilfe verwenden, aktivieren Sie die CAU-Clusterrolle auf diesem Failovercluster in eine der folgenden Methoden:<br /><br />-Führen Sie die [Enable-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/enable-cauclusterrole) PowerShell-Cmdlet.<br />-Wählen Sie die **konfigurieren Sie Cluster Aktualisieren von deren Hilfe Optionen** Aktion im Fenster des clusterfähigen Aktualisierens.|  
|Die konfigurierten CAU Remoteverwaltungssoftware-in für den Modus mit deren Hilfe aktualisieren muss auf allen Failoverclusterknoten registriert werden|Die Clusterrolle für clusterfähiges aktualisieren auf mindestens einem Knoten dieses Failoverclusters haben keinen Zugriff auf die CAU-Remoteverwaltungssoftware-in-Modul, das in den Optionen mit deren Hilfe aktualisieren konfiguriert ist. Eine deren Hilfe-Aktualisierung ausführen schlägt möglicherweise fehl.|– Stellen Sie sicher, dass die konfigurierten CAU Remoteverwaltungssoftware in auf allen Clusterknoten installiert ist, indem Sie dem Installationsverfahren für das Produkt, das Remoteverwaltungssoftware-in für clusterfähiges aktualisieren bereitstellt.<br />-Führen Sie die [Register-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) PowerShell-Cmdlet, um das Remoteverwaltungssoftware-in auf den erforderlichen Clusterknoten zu registrieren.|  
|Alle Failoverclusterknoten müssen denselben Satz von registrierten Remoteverwaltungssoftware clusterfähiges|Eine deren Hilfe-Aktualisierung ausführen kann fehlschlagen, wenn das Remoteverwaltungssoftware-in konfiguriert ist, dass in einer Updateausführung verwendet werden, das geändert wurde, die nicht auf allen Clusterknoten verfügbar ist.|– Stellen Sie sicher, dass die konfigurierten CAU Remoteverwaltungssoftware in auf allen Clusterknoten installiert ist, indem Sie dem Installationsverfahren für das Produkt, das Remoteverwaltungssoftware-in für clusterfähiges aktualisieren bereitstellt.<br />-Führen Sie die [Register-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) PowerShell-Cmdlet, um das Remoteverwaltungssoftware-in auf den erforderlichen Clusterknoten zu registrieren.|  
|Die konfigurierten Optionen für die Updateausführung müssen gültig sein.|Aktualisieren von deren Hilfe Zeitplan und updateausführungsoptionen, die für diesen Failovercluster konfiguriert sind sind unvollständig oder ungültig. Eine deren Hilfe-Aktualisierung ausführen schlägt möglicherweise fehl.|Konfigurieren Sie eine gültige Zeitplan mit deren Hilfe aktualisieren und updateausführungsoptionen. Sie können z.B. Verwenden der [Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole) PowerShell-Cmdlet zum Konfigurieren der CAU-Clusterrolle.|  
|Mindestens zwei Failoverclusterknoten müssen Besitzer der Clusterrolle für clusterfähiges aktualisieren sein.|Eine Updateausführung starten im Modus mit deren Hilfe aktualisieren fehl, da die Clusterrolle für clusterfähiges aktualisieren keinen möglichen Besitzerknoten zu verschieben.|Verwenden Sie die Failoverclustering-Tools, um sicherzustellen, dass alle Clusterknoten als mögliche Besitzer für die CAU-Clusterrolle konfiguriert sind. Dies ist die Standardkonfiguration.||  
|Alle Failoverclusterknoten müssen auf Windows PowerShell-Skripts zugreifen können.|Nicht alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren können die konfigurierten Windows PowerShell-Skripts registrierungseintragswert- und Post\-Update zugreifen. Eine deren Hilfe-Aktualisierung ausführen, schlägt fehl.|Stellen Sie sicher, dass alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren Zugriffsberechtigungen für die konfigurierte PowerShell-Skripts registrierungseintragswert- und Post\-Update verfügen.|  
|Alle Failoverclusterknoten sollten identische Windows PowerShell-Skripts verwenden.|Nicht alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren verwenden dieselbe Kopie von der angegebenen Windows PowerShell-Skripts registrierungseintragswert- und Post\-Update. Eine Ausführung mit deren Hilfe aktualisieren möglicherweise fehl oder unerwartetes Verhalten.|Stellen Sie sicher, dass alle möglichen Besitzerknoten der Clusterrolle für clusterfähiges aktualisieren die gleichen PowerShell-Skripts registrierungseintragswert- und Post\-Update verwenden.|  
|Die Einstellung "WarnAfter" für die Updateausführung angegeben muss kleiner als die Einstellung "StopAfter" sein.|Die angegebenen Updateausführung für Clusterfähiges aktualisieren sorgen dafür, dass der warnungstimeout wirkungslos. Eine Updateausführung möglicherweise abgebrochen werden, bevor ein warnereignisprotokoll generiert werden kann.|Konfigurieren der Optionen der Updateausführung ein **WarnAfter** Option Wert, der kleiner als der **StopAfter** Optionswert.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Cluster-Aware Updating (Übersicht)](cluster-aware-updating.md)
  
