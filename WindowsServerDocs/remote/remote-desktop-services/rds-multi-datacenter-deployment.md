---
title: Geo-redundant RDS-Rechenzentren in Azure
description: Erfahren Sie, wie eine RDS-Bereitstellung zu erstellen, die mehrere Rechenzentren verwendet werden, um hochverfügbarkeit über geografische Standorte hinweg bereitzustellen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61c36528-cf47-4af0-83c1-a883f79a73a5
author: haley-rowland
ms.author: elizapo
ms.date: 06/14/2017
manager: dongill
ms.openlocfilehash: 2d12062f302c28a8124e0aa49af7f441e77ffe33
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222793"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>Erstellen einer Geo-redundant, mit mehreren Daten Center RDS-Bereitstellung für die notfallwiederherstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Sie können die Wiederherstellung im Notfall für Ihre Remote Desktop Services-Bereitstellung aktivieren, durch die Nutzung von mehreren Rechenzentren in Azure. Im Gegensatz zu einer standard hoch verfügbaren RDS-Bereitstellung (wie in der [Remote Desktop Services-Architektur](desktop-hosting-logical-architecture.md)), die Rechenzentren in einer einzelnen Azure-Region (z.B. Europa, Westen) verwendet, eine Bereitstellung mit mehreren Data Center verwendet die Daten Rechenzentren an mehreren geografischen Standorten befinden, erhöhen die Verfügbarkeit Ihrer Bereitstellung – eine Azure-Rechenzentrum ist möglicherweise nicht verfügbar, aber es ist unwahrscheinlich, dass mehrere Regionen zur gleichen Zeit ausfallen würde. Durch die Bereitstellung eines geografisch redundanten RDS-Architektur, können Sie Failover im Fall von schwerwiegenden Fehler einer gesamten Region aktivieren.

Können Sie die nachstehenden Anweisungen für die Nutzung von Microsoft Azure-Infrastrukturdiensten und RDS zum Bereitstellen von geografisch redundanten Desktop hostende Dienste und Subscriber Access Licenses, (SALs) mit mehreren Mandanten über das [Microsoft Service Provider License Agreement (SPLA)-Programm](https://www.microsoft.com/hosting/licensing/splabenefits.aspx). Sie können auch die folgenden Schritte verwenden, erstellen Sie ein Geo-redundant-Hostingdienst für Ihre eigenen Mitarbeiter mit [RDS-Benutzer-CALs erweiterten Rechte durch Software Assurance](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf).

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>Logische Architektur für hohe Verfügbarkeit – einzelne und mehrere Regionen
Die folgende Abbildung zeigt die Architektur für eine hoch verfügbare Bereitstellung in einer Azure-Region an:

![Eine hoch verfügbare Bereitstellung in einer Azure-region](media/rds-ha-single-region.png)

Die Bereitstellung besteht aus drei Schichten:

- Azure-Dienste – die Azure-Verwaltungsschnittstellen, einschließlich der Azure-Portal und APIs sowie öffentliche Netzwerkdienste wie DNS und die öffentliche IP-Adressen.
- Desktophosting-Dienst – virtuelle Computer, Netzwerke, Speicher, Azure-Dienste und Windows Server-Rollendienste
- Azure-Fabric - Windows Server-Betriebssystemen die Hyper-V-Rolle, die zum Virtualisieren von physischen Servern, Speichereinheiten, Netzwerk-Switches und Router verwendet werden. Mithilfe der Azure-Fabric können Sie die virtuellen Computer, Netzwerke, Speicher und Anwendungen unabhängig von der zugrunde liegenden Hardware zu erstellen.


Im Gegensatz dazu ist hier die Architektur für eine Bereitstellung mit mehreren Azure-Datencentern ein:

![Einer RDS-Bereitstellung, die mehrere Azure-Regionen verwendet.](media/rds-ha-multi-region.png)

Die gesamte RDS-Bereitstellung wird in einer zweiten Azure-Region zum Erstellen einer geografisch redundanten Bereitstellung repliziert. Diese Architektur verwendet ein Aktiv / Passiv-Modell, dem nur eine RDS-Bereitstellung zu einem Zeitpunkt ausgeführt wird. Eine VNet-zu-VNet-Verbindung können die beiden Umgebungen, die miteinander kommunizieren. Die RDS-Bereitstellungen basieren auf einer einzelnen Active Directory-Gesamtstruktur/Domäne, und die AD-Server in die beiden Bereitstellungen replizieren, Bedeutung-Benutzer können sich anmelden, in keiner der Bereitstellungen mit denselben Anmeldeinformationen an. Benutzereinstellungen und im Benutzer-Benutzerprofil-Datenträger (UPD) gespeicherten Daten werden auf einem Cluster "direkte Speicherplätze" Horizontales Skalieren mit zwei Knoten-Dateiserver (SOFS) gespeichert. Ein zweiter Cluster auf identischer "direkte Speicherplätze" in der zweiten (passiven) Region bereitgestellt wird, und die Funktion "Speicherreplikat" wird verwendet, um die Benutzerprofile aus dem aktiven replizieren, passiven Bereitstellung. Azure Traffic Manager wird verwendet, um automatisch weiterzuleiten, welche Bereitstellung Benutzer ist zurzeit eine aktive - aus der Perspektive des Endbenutzers, die sie Zugriff auf die Bereitstellung mithilfe einer einzelnen URL und nicht bewusst, welche Region sie enden mit.


Sie *konnte* erstellen Sie eine nicht hoch verfügbare RDS-Bereitstellung in jeder Region, aber auch ein einzelnen virtuellen Computer in einer Region gestartet wird, wird ein Failover auftreten, erhöhen die Wahrscheinlichkeit, dass bei Failovern Auswirkungen auf die Leistung verknüpft.

## <a name="deployment-steps"></a>Bereitstellungsschritte
Erstellen Sie die folgenden Ressourcen in Azure zum Erstellen einer geografisch redundanten mehreren Rechenzentren RDS-Bereitstellung:

1. Zwei Ressourcengruppen in zwei separate Azure-Regionen. Z. B. RG A (die aktive Bereitstellung, RG steht für "Ressourcengruppe") und RG B (die passive Bereitstellung).
2. Eine hoch verfügbare Active Directory-Bereitstellung in der RG A. Sie können die [neue AD-Domäne mit einer Vorlage für 2 Domänencontroller](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/) zum Erstellen der Bereitstellung.
3. Einer hoch verfügbaren RDS-Bereitstellung RG A. Use der [RDS-Bereitstellung mithilfe von vorhandenen active Directory farm](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) Vorlage zum Erstellen der grundlegenden RDS-Bereitstellung, und befolgen dann die Informationen in [Remote Desktop Services – hoch Verfügbarkeit](rds-plan-high-availability.md) so konfigurieren Sie die anderen RDS-Komponenten für hohe Verfügbarkeit.
4. Ein VNet in der RG B – Achten Sie darauf, einen Adressraum verwenden, der die Bereitstellung in der RG A. nicht überlappt
5. Ein [VNet-zu-VNet-Verbindung](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps) zwischen den zwei Ressourcengruppen.
6. Zwei AD virtuelle Computer in einer verfügbarkeitsgruppe, die in der RG-B - stellen Sie sicher, dass die VM-Namen unterscheiden sich von den AD-VMs in RG A. Deploy zwei Windows Server 2016-VMs in einer einzelnen verfügbarkeitsgruppe festlegen, installieren Sie die Active Directory-Domänendienste-Rolle und dann zu der Domäne bietet höher stufen farbrollen in der Domäne, die Sie in Schritt 1 erstellt haben.
7. Eine zweite hoch verfügbaren RDS-Bereitstellung in der RG B. 
   1. Verwenden der [RDS-Bereitstellung mithilfe von vorhandenen active Directory farm](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) Vorlage erneut, dieses Mal jedoch die folgenden Änderungen vornehmen. (Zum Anpassen der Vorlage, wählen sie im Katalog aus, klicken Sie auf **in Azure bereitstellen** und dann **Bearbeitungsvorlage**.)
      1. Passen Sie den Adressraum des der DNS-Server private IP-Adresse in das VNet in der RG B. entsprechen. 
      
         Suchen Sie nach "DnsServerPrivateIp" in der Variablen. Bearbeiten Sie die Standard-IP (10.0.0.4) um den Adressraum zu entsprechen, die Sie in das VNet in der RG B. definiert
   
      2. Bearbeiten Sie die Computernamen, damit sie mit den Angaben in der Bereitstellung in der RG A. in Konflikt stehen keine
      
         Suchen Sie die virtuellen Computer in der **Ressourcen** -Abschnitt der Vorlage. Ändern der **ComputerName** Feld **"osprofile"** . Beispielsweise kann "Gateway" werden "Gateway **-b**"; "[Concat ('Rdsh-", copyIndex())] "kann"[Concat ("Rdsh - b-", copyIndex())]"werden, und"Broker"Annehmen" Broker **-b**".
      
         (Sie können auch die Namen der virtuellen Computer manuell ändern, nachdem Sie die Vorlage ausführen.)
   2. Wie in Schritt 3 oben, verwenden Sie die Informationen im [Remote Desktop Services - hochverfügbarkeit](rds-plan-high-availability.md) so konfigurieren Sie die anderen RDS-Komponenten für hohe Verfügbarkeit.
8. Ein "direkte Speicherplätze" Dateiserver mit horizontaler Skalierung Server mit der Funktion "Speicherreplikat" in die beiden Bereitstellungen. Verwenden der [PowerShell-Skript](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts) zum Bereitstellen der [Vorlage](https://github.com/robotechredmond/301-s2d-sr-dr-md) über Ressourcengruppen hinweg.

   > [!NOTE]
   > Sie können den Speicher manuell (anstatt die PowerShell-Skript und die Vorlage) bereitstellen: 
   >1. Bereitstellen einer [zwei Knoten Storage Spaces Direct SOFS](rds-storage-spaces-direct-deployment.md) RG A zum Speichern der Benutzerprofil-Datenträgern (UPDs).
   >2. Bereitstellen eines zweiten, identische Speicher Leerzeichen direkte SOFS in RG B – stellen Sie sicher, dass die gleiche Menge an Speicher in jedem Cluster verwenden.
   >3. Richten Sie [Funktion "Speicherreplikat" bei der asynchronen Replikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md) zwischen den beiden.

### <a name="enable-upds"></a>Aktivieren von Benutzerprofil-Datenträger
Funktion "Speicherreplikat" repliziert Daten über ein Quellvolume (primär/aktiv-Bereitstellung zugeordnet) auf ein Zielvolume (sekundär/Passiv-Bereitstellung zugeordnet). Programmbedingt wird der Zielcluster als **Online (kein Zugriff)** -Funktion "Speicherreplikat" hebt die Bereitstellung der Zielvolumes sowie deren Laufwerk Laufwerkbuchstaben oder Bereitstellungspunkte Punkte. Dies bedeutet, dass es sich bei Aktivierung von Benutzerprofil-Datenträger für die sekundäre Bereitstellung durch die Bereitstellung des Dateifreigabepfad misslingt, da das Volume nicht bereitgestellt wird. 

Möchten Sie weitere Informationen zum Verwalten der Replikation? Sehen Sie sich [-Cluster zu Cluster-Speicherreplikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md).

Um die Benutzerprofil-Datenträger für beide Bereitstellungen zu aktivieren, führen Sie folgende Schritte aus:

1. Führen Sie die [Cmdlet "Set-RDSessionCollectionConfiguration"](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdsessioncollectionconfiguration) So aktivieren Sie die Benutzerprofil-Datenträger für die Bereitstellung die primäre (aktive) – Geben Sie einen Pfad für die Dateifreigabe, auf dem Quellvolume (das Sie in Schritt 7 in den Schritten zur Bereitstellung erstellt haben).
2. Kehren Sie die Funktion "Speicherreplikat", damit das Zielvolume wird dem Quellvolume (dies einbinden des Volumes und ermöglicht es den von der sekundären Bereitstellung Zugriff auf). Sie können ausführen **Set-SRPartnership** Cmdlet, um diese auszuführen. Zum Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. Die Benutzerprofil-Datenträger in der sekundären (passiven) Bereitstellung zu aktivieren. Verwenden Sie die gleichen Schritte wie für die primäre Bereitstellung, in Schritt 1.
4. Kehren Sie die Funktion "Speicherreplikat" in diesem Fall also das ursprüngliche Volume mit Datenquelle erneut dem Quellvolume in der SR-Partnerschaft, und die primäre Bereitstellung Zugriff auf die Dateifreigabe. Zum Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager 

Erstellen einer [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) Profil, und wählen Sie die **Priorität** Methode für das datenverkehrsrouting. Legen Sie die beiden Endpunkte, auf die öffentliche IP-Adressen jeder Bereitstellung. Klicken Sie unter **Konfiguration**, ändern Sie das Protokoll auf HTTPS (anstelle von HTTP) und den Port 443 (anstelle von 80). Notieren Sie sich die **DNS-Gültigkeitsdauer Standardnachricht**, und legen Sie ihn entsprechend dem Failover muss. 

Beachten Sie, dass Traffic Manager Endpunkte zurückzugebenden 200 OK als Reaktion auf eine GET-Anforderung, um als "fehlerfrei" markiert werden. Die öffentliche IP-Objekt, das aus den RDS-Vorlagen erstellten funktionieren, aber fügen Sie einen Nachtrag Pfad nicht. Stattdessen, Sie erhalten Benutzer die URL des Traffic Manager mit "/ RDWeb" angefügt, beispielsweise: ```http://deployment.trafficmanager.net/RDWeb```

Durch die Bereitstellung von Azure Traffic Manager mit der prioritätsbasierten Routingmethode verhindern, dass Sie Endbenutzern den Zugriff auf die passiven Bereitstellung, während die aktive Bereitstellung funktionsfähig ist. Wenn Endbenutzer greifen auf den passiven Bereitstellung und die Richtung für die Funktion "Speicherreplikat" noch nicht für das Failover gewechselt wurde, hängt die Benutzeranmeldung, wie die Bereitstellung versucht und Zugriff auf die Dateifreigabe auf dem passiven Cluster "direkte Speicherplätze" - schließlich die Bereitstellung schlägt fehl wird aufgeben und weisen Sie dem Benutzer ein temporäres Profil.  

### <a name="deallocate-vms-to-save-resources"></a>Zuordnung VMs zum Einsparen von Ressourcen 
Nach der Konfiguration beider Bereitstellungen können Sie optional Herunterfahren und Aufheben der Zuordnung der sekundären RDS-Infrastruktur und RDSH-VMs, um Kosten einzusparen, auf diesen VMs. Der Storage Spaces Direct SOFS und AD-Server VMs muss immer in der sekundären/Passiv-Bereitstellung zum Aktivieren der Synchronisierung für Benutzer Konto- und Profilinformationen ausgeführt wird.  

Wenn ein Failover auftritt, müssen Sie die Aufhebung der Zuordnung virtuellen Computer gestartet. Diese Konfiguration hat es sich um den Vorteil, geringeren Kosten, aber auf Kosten der Failover-Zeit. Im Falle ein schwerwiegenden Fehlers in der aktiven Bereitstellung müssen Sie die passive Bereitstellung manuell starten, oder Sie benötigen ein Automatisierungsskript erkennt den Ausfall, und starten Sie die passive Bereitstellung automatisch. In beiden Fällen dauert mehrere Minuten in der passiven Bereitstellung ausgeführt wird und für Benutzer zur Anmeldung erhalten es einige Ausfallzeiten für den Dienst. Diese Ausfallzeit hängt die Zeitspanne, während es verwendet, um die RDS-Infrastruktur und RDSH-VMs (in der Regel 2 bis 4 Minuten, wenn der virtuelle Computer nacheinander, sondern parallel gestartet werden) und die Uhrzeit auf den passiven Cluster online schalten (das hängt von der Größe des Clusters zu starten in der Regel 2 bis 4 Minuten für einen 2-Knoten-Cluster mit 2 Datenträger pro Knoten). 

### <a name="active-directory"></a>Active Directory 
Die Active Directory-Server in jeder Bereitstellung sind Replikate in der gleichen Gesamtstruktur oder Domäne an. Active Directory verfügt über eine integrierte Synchronisierungsprotokoll, um die vier Domänencontroller zu synchronisieren. Allerdings gibt es möglicherweise gewisse Verzögerung, wenn ein AD-Server ein neuer Benutzer hinzugefügt wird, kann es einige Zeit über alle AD-Server in die beiden Bereitstellungen repliziert dauern. Achten Sie daher darauf, warnen der Benutzer nicht versuchen, melden Sie sich unmittelbar mit der Domäne hinzugefügt wird. 

### <a name="rd-license-server"></a>Remotedesktop-Lizenzserver 
Geben Sie einen [RD-pro-Benutzer-CAL](rds-client-access-license.md) für jeden benannten Benutzer, die autorisiert ist, auf den geografisch redundanten Bereitstellung zugreifen. Verteilen der pro Benutzer-Clientzugriffslizenzen gleichmäßig auf die beiden Remotedesktop-Lizenzserver in der aktiven Bereitstellung. Klicken Sie dann doppelte diese Lizenzen, die zwei Remotedesktop-Lizenzserver in der passiven Bereitstellung. Da die CALs zwischen aktivem und passivem Bereitstellung dupliziert werden, kann zu jedem Zeitpunkt nur eine Bereitstellung mit Benutzern verbinden aktiv; andernfalls verstoßen Sie den Lizenzvertrag.  

### <a name="image-management"></a>Abbildverwaltung 
Wenn Sie Ihre RDSH-Images zum Bereitstellen von Softwareupdates oder neue Anwendungen aktualisieren, müssen Sie separat aktualisieren Sie die RDSH-Sammlungen in jeder Bereitstellung, die eine übergreifende benutzerfreundlichkeit innerhalb beider Bereitstellungen beibehalten. Können Sie die [Update RDSH Auflistung Vorlage](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/), aber beachten Sie, dass der passive Bereitstellung RDS-Infrastruktur und RDSH-VMs ausgeführt werden muss, um die Vorlage auszuführen. 

## <a name="failover"></a>Failover

Bei der Aktiv / Passiv-Bereitstellung erfordert das Failover die virtuellen Computer eines der sekundären Bereitstellung zu starten. Sie können manuell oder mit einem Automatisierungsskript dazu. Im Fall eines schwerwiegenden Failovers des Storage Spaces Direct SOFS ändern Sie die Funktion "Speicherreplikat" Partnerschaft Richtung, sodass das Zielvolume auf dem Quellvolume wird. Zum Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

Weitere Informationen finden Sie in [-Cluster zu Cluster-Speicherreplikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md).

Azure Traffic Manager erkennt automatisch, dass die primäre Bereitstellung fehlgeschlagen ist und die sekundäre Bereitstellung fehlerfrei ist (in den RD-Gateway-VMs gestartet wurden in der RG B) und leitet den Datenverkehr auf die sekundäre Bereitstellung. Benutzer können die gleichen Traffic Manager-URL verwenden, zum Fortsetzen der Arbeit auf die Remoteressourcen an, ein konsistentes Verhalten profitieren zu können. Beachten Sie, dass der Client DNS-Cache den Datensatz nicht für die Dauer der Gültigkeitsdauer (TTL), legen Sie in Azure Traffic Manager-Konfiguration aktualisiert wird.

### <a name="test-failover"></a>Testen des Failovers
In einer Partnerschaft für Funktion "Speicherreplikat" kann nur ein Volume (Quelle) zu einem Zeitpunkt aktiv sein. Dies bedeutet, wenn Sie die Richtung SR-Partnerschaft wechseln, das Volume in der primären Bereitstellung (RG A) wird das Ziel der Replikation und daher ausgeblendet ist. Daher haben alle Benutzer RG A mit mehr Zugriff auf ihren Benutzerprofil-Datenträger gespeichert, auf dem SOFS in RG A. 

So testen Sie das Failover, während Benutzer weiterhin anmelden:
1. Starten Sie die Infrastruktur-VMs und die RDSH-Computer in der RG B.
2. Die SR-Partnerschaft Richtung wechseln (Cluster-b-s2d-c wird das Quellvolume).
3. [Deaktivieren Sie den Endpunkt](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint) RG A in Azure Traffic Manager-Profils zu einem Geldautomaten zum Leiten des Datenverkehrs auf RG B. Sie können auch erzwingen, verwenden Sie ein PowerShell-Skript:

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

RG B ist jetzt der aktiven primären Bereitstellung. Wechseln Sie zurück zur RG A als die primäre Bereitstellung:

1. Die SR-Partnerschaft Richtung wechseln (Cluster-a-s2d-c wird das Quellvolume):

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Aktivieren Sie erneut den Endpunkt der RG A in Azure Traffic Manager-Profil:

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA 
   ```

## <a name="considerations-for-on-premises-deployments"></a>Überlegungen für lokale Bereitstellungen

Während eine lokalen Bereitstellung der Azure-Schnellstartvorlagen, die in diesem Artikel erwähnten verwenden konnte nicht, können Sie die Infrastrukturrollen manuell implementieren. In einer lokalen-Bereitstellung, in dem Kosten nicht von Azure-Nutzung gesteuert wird, sollten Sie in Betracht ziehen, ein aktiv / aktiv-Modell für schnellere Failover zu verwenden.

Können Sie Azure Traffic Manager mit lokalen Endpunkten, aber es ist ein Azure-Abonnement erforderlich. Alternativ dazu für das DNS-Endbenutzer die Möglichkeit bereitgestellt, geben sie einen CNAME-Eintrag, der die Benutzer auf die primäre Bereitstellung einfach weiterleitet. Im Fall eines Failovers ändern Sie den DNS CNAME-Eintrag an die sekundäre Bereitstellung umleiten. Auf diese Weise verwendet der Endbenutzer eine einzelne URL, wie mit Azure Traffic Manager, die den Benutzer die entsprechende Bereitstellung weiterleitet. 

Wenn Sie ein Modell auf-lokal-zu-Azure-Standort erstellen möchten, erwägen Sie [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).
