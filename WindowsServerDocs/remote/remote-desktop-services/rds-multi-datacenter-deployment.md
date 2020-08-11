---
title: Georedundante RDS-Rechenzentren in Azure
description: Hier erfährst du, wie du eine RDS-Bereitstellung erstellst, die mehrere Rechenzentren nutzt, um Hochverfügbarkeit über mehrere geografische Standorte hinweg zu bieten.
ms.topic: article
ms.assetid: 61c36528-cf47-4af0-83c1-a883f79a73a5
author: haley-rowland
ms.author: elizapo
ms.date: 06/14/2017
manager: dongill
ms.openlocfilehash: cc36a81343b5416d3520a4e3483572d948c6bebc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958018"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>Erstellen einer georedundanten RDS-Bereitstellung mit mehreren Rechenzentren für die Notfallwiederherstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Du kannst eine Notfallwiederherstellung für die Remotedesktopdienste-Bereitstellung (Remote Desktop Services, RDS) einrichten, indem du mehrere Rechenzentren in Azure nutzt. Im Gegensatz zu einer standardmäßigen hoch verfügbaren RDS-Bereitstellung (wie in der [Architektur der Remotedesktopdienste](desktop-hosting-logical-architecture.md) beschrieben), bei der Rechenzentren in einer einzigen Azure-Region (z.B. „Europa, Westen“) genutzt werden, verwendet eine georedundante Bereitstellung mehrere Rechenzentren in mehreren geografischen Regionen. Dadurch wird die Verfügbarkeit der gesamten Bereitstellung erhöht: Es kann passieren, dass ein Azure-Rechenzentrum nicht mehr verfügbar ist, aber dass mehrere Regionen gleichzeitig ausfallen, ist höchst unwahrscheinlich. Durch Bereitstellung einer georedundanten RDS-Architektur kannst du ein Failover aktivieren, falls eine komplette Region vollständig ausfallen sollte.

Mit der unten stehenden Anleitung kannst du die Microsoft Azure-Infrastrukturdienste und die Remotedesktopdienste nutzen, um über das [Microsoft SPLA-Programm](https://www.microsoft.com/hosting/licensing/splabenefits.aspx) (Service Provider License Agreement) georedundante Desktophostingdienste und Abonnentenzugriffslizenzen (Subscriber Access Licenses, SALs) auf mehreren Mandanten bereitzustellen. Du kannst die Schritte auch nutzen, um über [erweiterte Rechte für RDS-Benutzer-CALs durch Software Assurance](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf) einen georedundanten Hostingdienst für deine eigenen Mitarbeiter zu erstellen.

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>Logische Architektur für Hochverfügbarkeit – in einzelnen oder mehreren Regionen
Die folgende Abbildung zeigt die Architektur für eine hoch verfügbare Bereitstellung in einer einzelnen Azure-Region:

![Hoch verfügbare Bereitstellung in einer einzelnen Azure-Region](media/rds-ha-single-region.png)

Die Bereitstellung besteht aus drei Ebenen:

- Azure-Dienste: die Azure-Verwaltungsschnittstellen, einschließlich Azure-Portal und APIs, sowie öffentliche Netzwerkdienste wie DNS und öffentliche IP-Adressen.
- Desktophostingdienste: virtuelle Computer, Netzwerke, Speicher, Azure-Dienste und Windows Server-Rollendienste.
- Azure Fabric: Windows Server-Betriebssysteme mit Hyper-V-Rolle, die zum Virtualisieren von physischen Servern, Speichereinheiten, Netzwerkswitches und Routern verwendet werden. Mit Azure Fabric kannst du VMs, Netzwerke, Speicher und Anwendungen unabhängig von der zugrunde liegenden Hardware erstellen.


Im Vergleich dazu zeigt die folgende Abbildung die Architektur für eine Bereitstellung mit mehreren Azure-Rechenzentren:

![RDS-Bereitstellung mit mehreren Azure-Regionen](media/rds-ha-multi-region.png)

Die gesamte RDS-Bereitstellung wird in einer zweiten Azure-Region repliziert, sodass eine georedundante Bereitstellung entsteht. Diese Architektur verwendet ein Aktiv-Passiv-Modell, bei dem nur jeweils eine RDS-Bereitstellung ausgeführt wird. Eine VNET-to-VNET-Verbindung ermöglicht die Kommunikation zwischen den beiden Umgebungen. Die RDS-Bereitstellungen basieren auf einer einzelnen Active Directory-Gesamtstruktur bzw. -Domäne, und die AD-Server führen die Replikation zwischen den beiden Bereitstellungen aus. Das bedeutet, dass Benutzer sich mit den gleichen Anmeldeinformationen bei beiden Bereitstellungen anmelden können. Benutzereinstellungen und Daten auf Benutzerprofil-Datenträgern (User Profile Disks, UPDs) werden auf einem aus zwei Knoten bestehenden Scale-Out-Dateiclusterserver (Scale-Out File Server, SOFS) mit direkten Speicherplätzen gespeichert. In der zweiten (passiven) Region wird ein zweiter, identischer Cluster mit direkten Speicherplätzen bereitgestellt, und die Benutzerprofile werden mithilfe von Speicherreplikaten von der aktiven in die passive Bereitstellung repliziert. Endbenutzer werden mithilfe von Azure Traffic Manager an diejenige Bereitstellung weitergeleitet, die gerade aktiv ist. Aus Perspektive der Endbenutzer greifen diese über eine einzelne URL auf die Bereitstellung zu und erfahren nicht, welche Region sie letztendlich nutzen.


Du *könntest* in jeder Region eine RDS-Bereitstellung ohne Hochverfügbarkeit erstellen, aber schon das Neustarten einer einzigen VM in einer Region würde zu einem Failover führen. Damit würde die Wahrscheinlichkeit eines Failovers mit den damit zusammenhängenden Leistungsbeeinträchtigungen steigen.

## <a name="deployment-steps"></a>Bereitstellungsschritte
Erstelle die folgenden Ressourcen in Azure, um eine georedundante RDS-Bereitstellung mit mehreren Rechenzentren aufzubauen:

1. Zwei Ressourcengruppen in zwei separaten Azure-Regionen. Beispielsweise RG A (die aktive Bereitstellung, RG bedeutet „Ressourcengruppe“) und RG B (die passive Bereitstellung).
2. Eine hoch verfügbare Active Directory-Bereitstellung in RG A. Du kannst die Vorlage [Create an new AD Domain with 2 Domain Controllers](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/) (Neue AD-Domäne mit zwei Domänencontrollern erstellen) verwenden, um die Bereitstellung zu erstellen.
3. Eine hoch verfügbare RDS-Bereitstellung in RG A. Verwende die Vorlage [RDS farm deployment using existing active directory](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) (Bereitstellung einer RDS-Farm über eine vorhandene Active Directory-Instanz), um die grundlegende RDS-Bereitstellung zu erstellen. Befolge dann die Anweisungen in [Remote Desktop Services – hohe Verfügbarkeit](rds-plan-high-availability.md), um die anderen RDS-Komponenten im Hinblick auf Hochverfügbarkeit zu konfigurieren.
4. Ein VNET in RG B: Stelle sicher, dass du einen Adressraum verwendest, der sich nicht mit der Bereitstellung in RG A überschneidet.
5. Eine [VNET-to-VNET-Verbindung](/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps) zwischen den beiden Ressourcengruppen.
6. Zwei virtuelle AD-Computer in einer Verfügbarkeitsgruppe in RG B: Stelle sicher, dass die VM-Namen sich von den AD-VMs in RG A unterscheiden. Stelle zwei Windows Server 2016-VMs in einer einzelnen Verfügbarkeitsgruppe bereit, installiere die Active Directory Domain Services-Rolle, und stufe die VMs dann zum Domänencontroller in der in Schritt 1 erstellten Domäne hoch.
7. Eine zweite hoch verfügbare RDS-Bereitstellung in RG B.
   1. Verwende erneut die Vorlage [RDS farm deployment using existing active directory](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) (Bereitstellung einer RDS-Farm über eine vorhandene Active Directory-Instanz), nimm aber diesmal die folgenden Änderungen vor. (Um die Vorlage anzupassen, wähle sie im Katalog aus, und klicke auf **In Azure bereitstellen** und dann auf **Vorlage bearbeiten**.)
      1. Ändere den Adressraum der privaten IP-Adresse des DNS-Servers so, dass er dem VNET in RG B entspricht.

         Suche in Variablen nach „dnsServerPrivateIp“. Bearbeite die Standardadresse (10.0.0.4) so, dass sie dem im VNET in RG B definierten Adressraum entspricht.

      2. Bearbeite die Computernamen, sodass keine Konflikte mit den Namen in der Bereitstellung in RG A entstehen.

         Suche im Abschnitt **Resources** der Vorlage nach den VMs. Ändere das Feld **computerName** unter **osProfile**. „gateway“ kann beispielsweise zu „gateway **-b**“ werden, „[concat('rdsh-', copyIndex())]“ zu „[concat('rdsh-b-', copyIndex())]“ und „broker“ zu „broker **-b**“.

         (Du kannst die Namen der VMs auch nach dem Ausführen der Vorlage manuell ändern.)
   2. Verwende wie in Schritt 3 oben die Informationen in [Remote Desktop Services – hohe Verfügbarkeit](rds-plan-high-availability.md), um die anderen RDS-Komponenten im Hinblick auf Hochverfügbarkeit zu konfigurieren.
8. Ein Scale-Out-Dateiserver mit direkten Speicherplätzen und Speicherreplikaten über die beiden Bereitstellungen hinweg. Verwende das [PowerShell-Skript](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts), um die [Vorlage](https://github.com/robotechredmond/301-s2d-sr-dr-md) für alle Ressourcengruppen bereitzustellen.

   > [!NOTE]
   > Du kannst den Speicher auch manuell bereitstellen (anstatt das PowerShell-Skript und eine Vorlage zu verwenden):
   >1. Stelle einen [Scale-Out-Dateiserver mit direkten Speicherplätzen und zwei Knoten](rds-storage-spaces-direct-deployment.md) in RG A bereit, um die Benutzerprofil-Datenträger (User Profile Disks, UPDs) zu speichern.
   >2. Stelle einen zweiten, identischen Scale-Out-Dateiserver mit direkten Speicherplätzen in RG B bereit, und stelle sicher, dass in jedem Cluster die gleiche Menge an Speicherplatz verwendet wird.
   >3. Richte ein [Speicherreplikat mit asynchroner Replikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md) zwischen beiden ein.

### <a name="enable-upds"></a>Aktivieren von UPDs
Das Speicherreplikat repliziert Daten aus einem Quellvolume (das der primären bzw. aktiven Bereitstellung zugeordnet ist) in ein Zielvolume (das der sekundären bzw. passiven Bereitstellung zugeordnet ist). Programmbedingt wird der Zielcluster als **online (kein Zugriff)** angezeigt. Das Speicherreplikat hebt die Bereitstellung der Zielvolumes und der zugehörigen Laufwerkbuchstaben oder Bereitstellungspunkte auf. Das bedeutet, dass die Aktivierung von UPDs für die sekundäre Bereitstellung durch Angabe des Dateifreigabepfad nicht funktioniert, weil das Volume nicht eingebunden ist.

Möchtest du mehr über das Verwalten der Replikation erfahren? Dann lies den Artikel [Cluster-zu-Cluster-Speicherreplikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md).

Führe zum Aktivieren von UPDs in beiden Bereitstellungen folgende Schritte aus:

1. Führe das Cmdlet [Set-RDSessionCollectionConfiguration](/powershell/module/remotedesktop/set-rdsessioncollectionconfiguration) aus, um die Benutzerprofil-Datenträger für die primäre (aktive) Bereitstellung zu aktivieren. Gib einen Pfad zu der Dateifreigabe auf dem Quellvolume an (das du in Bereitstellungsschritt 7 erstellt hast).
2. Kehre die Richtung des Speicherreplikats um, sodass das Zielvolume zum Quellvolume wird (dadurch wird das Volume eingebunden, und die sekundäre Bereitstellung kann darauf zugreifen). Zu diesem Zweck kannst du das Cmdlet **Set-SRPartnership** ausführen. Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. Aktiviere die Benutzerprofil-Datenträger in der sekundären (passiven) Bereitstellung. Führe die gleichen Aktionen aus wie für die primäre Bereitstellung in Schritt 1.
4. Kehre die Richtung des Speicherreplikats erneut um, sodass das ursprüngliche Quellvolume wieder zum Quellvolume in der Speicherreplikat-Partnerschaft wird. Nun kann die primäre Bereitstellung auf die Dateifreigabe zugreifen. Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager

Erstelle ein [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview)-Profil, und wähle die Routingmethode **Priorität** aus. Lege die beiden Endpunkte auf die öffentlichen IP-Adressen jeder Bereitstellung fest. Ändere unter **Konfiguration** das Protokoll zu HTTPS (statt HTTP) und den Port zu 443 (statt 80). Lege die **DNS-Gültigkeitsdauer** auf einen für deine Failoveranforderungen geeigneten Wert fest.

Beachte, dass Endpunkte bei GET-Anforderungen „200 OK“ zurückgeben müssen, um von Traffic Manager als „fehlerfrei“ markiert zu werden. Das aus den RDS-Vorlagen erstellte publicIP-Objekt funktioniert. Füge jedoch keinen Pfadzusatz hinzu. Stattdessen kannst du Endbenutzern die Traffic Manager-URL mit angefügtem „/RDWeb“ zur Verfügung stellen, z. B.: ```http://deployment.trafficmanager.net/RDWeb```.

Durch Bereitstellung von Azure Traffic Manager mit der prioritätsbasierten Routingmethode verhinderst du, dass Endbenutzer auf die passive Bereitstellung zugreifen, während die aktive Bereitstellung funktionsfähig ist. Wenn Endbenutzer auf die passive Bereitstellung zugreifen und die Richtung des Speicherreplikats nicht zum Failover geändert wurde, reagiert die Benutzeranmeldung nicht, weil die Bereitstellung erfolglos versucht, auf dem passiven Cluster mit direkten Speicherplätzen auf die Dateifreigabe zuzugreifen. Letztendlich erhält der Benutzer ein temporäres Profil.

### <a name="deallocate-vms-to-save-resources"></a>Aufheben der Zuordnung von VMs zum Einsparen von Ressourcen
Nachdem du beide Bereitstellungen konfiguriert hast, kannst du optional die sekundäre RDS-Infrastruktur und die sekundären RDSH-VMs herunterfahren und die Zuordnung aufheben, um die Kosten für diese VMs zu sparen. Die Scale-Out-Dateiserver mit direkten Speicherplätzen und die AD-Server-VMs müssen in der sekundären bzw. passiven Bereitstellung immer ausgeführt werden, um die Synchronisierung von Benutzerkonto und Benutzerprofil zu ermöglichen.

Wenn ein Failover auftritt, musst du die VMs, deren Zuordnung aufgehoben wurde, starten. Diese Bereitstellungskonfiguration ist kostengünstiger, benötigt aber mehr Zeit für ein Failover. Bei einem schwerwiegenden Ausfall der aktiven Umgebung musst du die passive Bereitstellung manuell starten oder benötigst ein Automatisierungsskript, das den Ausfall erkennt und die passive Bereitstellung automatisch startet. In beiden Fällen kann es mehrere Minuten dauern, bis die passive Bereitstellung ausgeführt wird und Benutzern für die Anmeldung zur Verfügung steht. Dadurch können Ausfallzeiten für den Dienst entstehen. Die Länge dieser Ausfallzeit hängt davon ab, wie lange es dauert, die RDS-Infrastruktur und die RDSH-VMs neu zu starten (in der Regel zwei bis vier Minuten, wenn die VMs nicht seriell, sondern parallel gestartet werden) und den passiven Cluster online zu schalten (dies wiederum hängt von der Größe des Clusters ab – in der Regel sind bei einem Cluster mit zwei Knoten und zwei Datenträgern pro Knoten zwei bis vier Minuten zu veranschlagen).

### <a name="active-directory"></a>Active Directory
Die Active Directory-Server in den Bereitstellungen sind Replikate innerhalb der gleichen Gesamtstruktur bzw. Domäne. Active Directory verfügt über ein integriertes Synchronisierungsprotokoll, um die vier Domänencontroller zu synchronisieren. Es können jedoch Verzögerungen auftreten. Wenn also ein neuer Benutzer zu einem AD-Server hinzugefügt wird, kann es eine Weile dauern, bis dieser auf allen AD-Servern in beiden Bereitstellungen repliziert ist. Benutzer sollten daher nicht sofort versuchen, sich anzumelden, nachdem sie der Domäne hinzugefügt wurden.

### <a name="rd-license-server"></a>RD-Lizenzserver
Stelle eine [RD-Lizenz pro Benutzer](rds-client-access-license.md) für jeden benannten Benutzer bereit, der für den Zugriff auf die georedundante Bereitstellung autorisiert ist. Verteile die CALs pro Benutzer gleichmäßig auf die beiden RD-Lizenzserver in der aktiven Bereitstellung. Dupliziere diese CALs dann auf die beiden RD-Lizenzserver in der passiven Bereitstellung. Da die CALs zwischen der aktiven und der passiven Bereitstellung dupliziert sind, kann zu jedem Zeitpunkt nur eine Bereitstellung aktiv sein, mit der Benutzer eine Verbindung herstellen. Andernfalls besteht ein Verstoß gegen die Lizenzvereinbarung.

### <a name="image-management"></a>Imageverwaltung
Beim Aktualisieren von RDSH-Images zum Bereitstellen von Softwareupdates oder neuen Anwendungen musst du die RDSH-Sammlungen in jeder Bereitstellung separat aktualisieren, um ein einheitliches Benutzererlebnis in beiden Bereitstellungen beizubehalten. Du kannst die Vorlage [Update RDSH collection](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/) (RDSH-Sammlung aktualisieren) verwenden, beachte aber, dass die RDS-Infrastruktur-VMs und RDSH-VMs der passiven Bereitstellung ausgeführt werden müssen, damit die Vorlage ausgeführt werden kann.

## <a name="failover"></a>Failover

Im Fall der Aktiv-Passiv-Bereitstellung ist es für ein Failover erforderlich, die VMs der sekundären Bereitstellung zu starten. Du kannst dies manuell oder mit einem Automatisierungsskript durchführen. Sollte ein schwerwiegender Ausfall des Scale-Out-Dateiservers mit direkten Speicherplätzen eintreten, ändere die Richtung der Speicherreplikat-Partnerschaft, sodass das Zielvolume zum Quellvolume wird. Beispiel:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

Mehr dazu erfährst du im Artikel [Cluster-zu-Cluster-Speicherreplikation](../../storage/storage-replica/cluster-to-cluster-storage-replication.md).

Azure Traffic Manager erkennt automatisch, dass die primäre Bereitstellung ausgefallen und die sekundäre Bereitstellung fehlerfrei ist (wenn die RD-Gateway-VMs in RG B gestartet wurden), und leitet den Benutzerdatenverkehr an die sekundäre Bereitstellung weiter. Benutzer können die gleiche Traffic Manager-URL verwenden, um weiter an ihren Remoteressourcen zu arbeiten, und profitieren von einem konsistenten Benutzererlebnis. Beachte, dass der DNS-Clientcache den Datensatz während der in der Azure Traffic Manager-Konfiguration festgelegten Gültigkeitsdauer nicht aktualisiert.

### <a name="test-failover"></a>Testen des Failovers
In einer Speicherreplikat-Partnerschaft kann immer nur ein Volume (die Quelle) aktiv sein. Das bedeutet Folgendes: Wenn du die Richtung der Speicherreplikat-Partnerschaft änderst, wird das Volume in der primären Bereitstellung (RG A) zum Ziel der Replikation und wird daher ausgeblendet. Daher haben Benutzer, die eine Verbindung mit RG A herstellen, keinen Zugriff mehr auf ihre Benutzerprofil-Datenträger, die auf dem Scale-Out-Dateiserver in RG A gespeichert sind.

So testest du das Failover und ermöglichst Benutzern weiterhin die Anmeldung:
1. Starte die Infrastruktur-VMs und die RDSH-VMs in RG B.
2. Ändere die Richtung der Speicherreplikat-Partnerschaft („cluster-b-s2d-c“ wird zum Quellvolume).
3. [Deaktiviere den Endpunkt](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint) von RG A im Azure Traffic Manager-Profil, um Azure Traffic Manager zu zwingen, Datenverkehr an RG B weiterzuleiten. Alternativ dazu kannst du auch ein PowerShell-Skript verwenden:

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

RG B ist jetzt die aktive primäre Bereitstellung. So wechselst du wieder zu RG A als primäre Bereitstellung:

1. Ändere die Richtung der Speicherreplikat-Partnerschaft („cluster-a-s2d-c“ wird zum Quellvolume):

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Aktiviere den Endpunkt von RG A erneut im Azure Traffic Manager-Profil:

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA
   ```

## <a name="considerations-for-on-premises-deployments"></a>Überlegungen zu lokalen Bereitstellungen

Zwar kannst du bei einer lokalen Bereitstellung nicht die in diesem Artikel erwähnten Azure-Schnellstartvorlagen verwenden, aber du kannst alle Infrastrukturrollen manuell implementieren. In einer lokalen Bereitstellung, bei der die Kosten nicht durch die Azure-Nutzung bestimmt werden, solltest du ein Aktiv-Aktiv-Modell in Betracht ziehen, um ein schnelleres Failover zu erreichen.

Du kannst Azure Traffic Manager mit lokalen Endpunkten verwenden, aber dafür ist ein Azure-Abonnement erforderlich. Alternativ dazu kannst du für das Domain Name System, das für Endbenutzer bereitgestellt wird, auch einen CNAME-Eintrag zur Verfügung stellen, der Benutzer einfach an die primäre Bereitstellung weiterleitet. Ändere bei einem Failover den DNS-CNAME-Eintrag so, dass die Weiterleitung an die sekundäre Bereitstellung erfolgt. Auf diese Weise benötigen Endbenutzer nur eine einzige URL – genau wie bei Azure Traffic Manager –, die sie an die geeignete Bereitstellung weiterleitet.

Wenn du ein Modell mit Weiterleitung zwischen lokaler Umgebung und Azure-Standort erstellen möchtest, ziehe die Verwendung von [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) in Betracht.
