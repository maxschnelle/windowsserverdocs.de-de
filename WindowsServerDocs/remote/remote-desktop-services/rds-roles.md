---
title: Remotedesktopdienste – Rollen
description: Beschreibt die Komponenten der Desktop, Dienst hostet.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
author: heidilohr
manager: dougkim
ms.openlocfilehash: 48efbffa4f82b707b63e33e6416da43eb105221f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844721"
---
# <a name="remote-desktop-services-roles"></a>Remotedesktopdienste – Rollen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieser Artikel beschreibt die Rollen in einer Umgebung Remote Desktop Services.

## <a name="remote-desktop-session-host"></a>Remotedesktop-Sitzungshost

Der Remotedesktop-Sitzungshost (RD-Sitzungshost) enthält die Sitzungs-basierten Anwendungen und Desktops, die Sie für Benutzer freigeben. Benutzer können diese Desktops und apps über einen der Remotedesktop-Clients, die unter Windows, MacOS, iOS und Android ausgeführt. Benutzer können auch über einen unterstützten Browser mithilfe des Web-Clients herstellen.

Sie können Desktops und apps in einen oder mehrere RD Session Host-Server, die Namen "Sammlungen". organisieren. Sie können diese Sammlungen für bestimmte Gruppen von Benutzern in jeder Mandant anpassen. Beispielsweise können Sie eine Sammlung erstellen, in denen eine bestimmte Benutzergruppe kann auf bestimmte apps zugreifen, aber Personen außerhalb der gewünschten Gruppe nicht auf diese apps zugreifen können.

Für kleine Bereitstellungen können Sie die Anwendungen direkt auf dem RD-Sitzungshostserver installieren. Für größere Bereitstellungen empfehlen wir eine base-Image Erstellen und Bereitstellen von virtuellen Computern aus diesem Image.

Sie können Sammlungen erweitern, durch das Hinzufügen von RD-Sitzungshost-Server-Computer in einer Auflistung-Farm mit einzelnen virtuellen RDSH-Computers in einer Sammlung, die derselben verfügbarkeitsgruppe zugewiesen. Dies bietet eine höhere Verfügbarkeit der Sammlung und erhöht die Skalierung um Benutzer oder eine Ressource-Anwendungen zu unterstützen.

In den meisten Fällen teilen sich die Benutzer die gleichen Remotedesktop-Sitzungshostserver, die Azure-Ressourcen für eine desktophostinglösungen möglichst effizient verwendet. In dieser Konfiguration müssen die Benutzer in Sammlungen mit einem nicht-Administratorkonten melden. Sie können auch einige Benutzer vollen administrativen Zugriff auf den remote Desktop geben durch das Erstellen von privaten Sitzung desktopsammlungen.

Sie können anpassen, dass Desktops noch erhöhen, indem das Erstellen und Hochladen einer virtuellen Festplatte mit Windows Server-Betriebssystems, die Sie als Vorlage zum Erstellen neuer RD Session Host virtuelle Maschinen verwenden können.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Remotedesktopdienste - sicheren Datenspeicher](rds-plan-secure-data-storage.md)
* [Hochladen einer generalisierten VHD und zum Erstellen neuer virtueller Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Ftoc.json)
* [Aktualisieren Sie die RDSH-Auflistung (ARM-Vorlage)](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/)

## <a name="remote-desktop-connection-broker"></a>Remotedesktop-Verbindungsbroker

Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker) verwaltet eingehende Remotedesktopverbindungen mit RD-Sitzungshost-Serverfarmen. RD Connection Broker verarbeitet Verbindungen mit beiden Auflistungen der vollständigen Desktops und Sammlungen von remote-apps. RD Connection Broker können der Auflistung serverübergreifenden Lastenausgleich beim Herstellen von neuer Verbindungen. Wenn eine Sitzung wird getrennt, Verbindung RD Connection Broker den Benutzer den richtigen RD Session Host-Server und ihre unterbrochenen Sitzung, die in der Farm RD Session Host immer noch vorhanden ist.

Sie müssen übereinstimmende digitale Zertifikate auf dem Remotedesktop-Verbindungsbroker-Server und des Clients zur Unterstützung des einmaligen Anmeldens und Veröffentlichen einer Anwendung zu installieren. Beim Entwickeln oder Testen eines Netzwerks, können Sie ein selbst generiertes und selbstsigniertes Zertifikat verwenden. Veröffentlichte Dienste erfordern jedoch ein digitales Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle. Der Name des Zertifikats muss als der interne vollständig qualifizierte Domäne (FQDN) des virtuellen Computers RD Connection Broker übereinstimmen.

Sie können Remotedesktop-Verbindungsbroker von Windows Server 2016 installieren, auf dem gleichen virtuellen Computer wie AD DS, um Kosten zu senken. Bei Bedarf zu skalieren, dass mehr Benutzer, können Sie auch zusätzliche RD Connection Broker virtuelle Computer in derselben verfügbarkeitsgruppe zum Erstellen eines Remotedesktop-Verbindungsbroker-Clusters hinzufügen.

Bevor Sie einen Remotedesktop-Verbindungsbroker-Cluster erstellen können, müssen Sie Azure SQL-Datenbank in der Mandanten-Umgebung bereitstellen oder erstellen eine SQL Server AlwaysOn-Verfügbarkeitsgruppe.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Die Bereitstellung der Remotedesktop-Verbindungsbrokerserver hinzu, und Konfigurieren von hochverfügbarkeit](rds-connection-broker-cluster.md)
* [SQL-Datenbank](desktop-hosting-service.md#sql-database) in desktophosting-Dienst.

## <a name="remote-desktop-gateway"></a>Remotedesktopgateway

Remotedesktopgateway (RD-Gateway) ermöglicht den Benutzern in öffentlichen Netzwerken auf Windows-Desktops und Anwendungen, die in Microsoft Azure Cloud-Diensten gehostet werden.

Die RD-Gateway-Komponente verwendet Secure Sockets Layer (SSL) zum Verschlüsseln des Kommunikationskanals zwischen Clients und dem Server. Der RD-Gateway-VM muss über eine öffentliche IP-Adresse zugänglich sein, die eingehenden TCP-Verbindungen an Port 443 und eingehende UDP-Verbindungen an Port 3391 ermöglicht. Dadurch können Benutzer über das Internet mithilfe von HTTPS kommunikationstransportprotokoll und das UDP-Protokoll eine Verbindung herstellen.

Digitalen Zertifikate auf dem Server und Client müssen übereinstimmen, damit dies funktioniert. Wenn Sie entwickeln oder testen ein Netzwerks, können Sie ein selbst generiertes und selbstsigniertes Zertifikat verwenden. Allerdings erfordert ein freigegebenen Dienst ein Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle. Der Name des Zertifikats muss übereinstimmen, den FQDN des Remotedesktop-Gateway, den Zugriff auf, ob der FQDN der öffentlichen IP-Adresse extern ausgerichtete DNS-Namen oder den CNAME-DNS-Ressourceneintrag, die auf die öffentliche IP-Adresse ist.

Für Mandanten mit weniger Benutzer können die Rollen Web Access für Remotedesktop und RD-Gateway auf einem einzelnen virtuellen Computer verwenden, um Kosten zu senken kombiniert werden. Sie können auch mehrere RD-Gateway-VMs zu einer Farm RD-Gateway zum Erhöhen der Verfügbarkeit des Diensts und horizontal hochskalieren, dass mehr Benutzer hinzufügen. Virtuelle Computer in größerer RD-Gateway-Farmen sollte in einer Gruppe mit Lastenausgleich konfiguriert werden. -IP-Affinität ist nicht erforderlich, wenn Sie RD-Gateway auf einem virtuellen Windows Server 2016-Computer verwenden, aber es ist, wenn Sie es auf einem virtuellen Windows Server 2012 R2-Computer ausführen.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Hohen Verfügbarkeit auf die Web-Front RD Web- und Gatewaycomputers hinzufügen](rds-rdweb-gateway-ha.md)
* [Remote Desktop Services - Zugriff von überall aus](rds-plan-access-from-anywhere.md)
* [Remote Desktop Services – Multi-Factor authentication](rds-plan-mfa.md)

## <a name="remote-desktop-web-access"></a>Web Access für Remotedesktop

Remote Web Access für Remotedesktop (RD-Webzugriff) können Benutzer Zugriff auf Desktops und Anwendungen über ein Webportal, und sie über das Gerät die native Microsoft-Remotedesktop-Clientanwendung startet. Können Sie das Webportal zum Veröffentlichen von Windows-Desktops und Anwendungen für Windows und nicht-Windows Clientgeräte, und Sie können auch selektiv Desktops oder apps für bestimmte Benutzer oder Gruppen veröffentlichen.

Web Access für Remotedesktop muss IIS (Internetinformationsdienste) ordnungsgemäß funktioniert. Eine Hypertext Transfer Protocol Secure (HTTPS)-Verbindung stellt einen Kanal verschlüsselte Kommunikation zwischen Clients und dem RD-Web-Server bereit. Der virtuelle Computer von Web Access für Remotedesktop muss über eine öffentliche IP-Adresse zugegriffen werden, die eingehende TCP-Verbindungen an Port 443, um die Benutzer des Mandanten über das Internet herstellen können ermöglicht die Verwendung von Transport des HTTPS-Kommunikationsprotokoll.

Abgleich von digitalen Zertifikaten muss auf dem Server und Clients installiert sein. Für Entwicklungs- und Testzwecke verwenden kann dies ein selbst generiertes und selbstsigniertes Zertifikat sein. Für einen veröffentlichten Dienst muss das digitale Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle abgerufen werden. Der Name des Zertifikats muss den vollständig qualifizierten Domänennamen (FQDN) für den Zugriff auf Web Access für Remotedesktop übereinstimmen. Mögliche FQDNs enthalten den extern zugänglichen DNS-Namen für die öffentliche IP-Adresse und den CNAME-DNS-Ressourceneintrag, die auf die öffentliche IP-Adresse verweist.

Bei Mandanten mit weniger Benutzern können Sie Kosten senken, durch die Kombination der Web Access für Remotedesktop und Remotedesktopgateway-Workloads in einem einzelnen virtuellen Computer. Sie können auch zusätzliche RD-Web-virtuelle Computer zu einer Farm Web Access für RD-Erhöhen der Verfügbarkeit des Diensts und horizontal hochskalieren, dass mehr Benutzer hinzufügen. In einer Web Access für Remotedesktop-Serverfarm mit mehreren virtuellen Computern müssen Sie die virtuellen Computer in einer Gruppe mit Lastenausgleich konfigurieren.

Weitere Informationen zum Konfigurieren von Web Access für Remotedesktop finden Sie unter den folgenden Artikeln:

* [Richten Sie den Remotedesktop-Web-Client für Ihre Benutzer](clients/remote-desktop-web-client-admin.md)
* [Erstellen und Bereitstellen einer Sammlung von Remote Desktop Services](rds-create-collection.md)
* [Erstellen einer Remote Desktop Services-Sammlung für Desktops und apps ausführen](rds-create-collection.md)

## <a name="remote-desktop-licensing"></a>Remotedesktoplizenzierung

Aktiviert die Remotedesktoplizenzierung (RD-Lizenzierung) Server ermöglichen Benutzern die Verbindung mit dem Remotedesktop-Sitzungshostserver Hosten von Desktops und apps des Mandantenverwaltungs. Mandantenumgebungen kommen in der Regel mit dem RD-Lizenzierungsserver bereits installiert, aber für gehostete Umgebungen müssen Sie den Server im Modus "pro Benutzer" konfigurieren.

Der Dienstanbieter benötigt genügend RDS Subscriber Access Licenses, (SALs), um alle autorisierten eindeutig (nicht gleichzeitigen) Benutzer abzudecken, die an den Dienst pro Monat, melden Sie sich. Dienstanbieter können Microsoft Azure Infrastructure Services direkt erwerben und können SALs über das Microsoft Service Provider Licensing Agreement (SPLA)-Programm erwerben. Kunden, die für eine desktop gehostete Lösung müssen vollständige gehostete Lösung (Azure und RDS) vom Dienstanbieter erwerben.

Kleine Mandanten können Kosten senken, durch die Kombination des Dateiservers und RD-Lizenzierung Komponenten auf einem einzelnen virtuellen Computer. Um höhere Verfügbarkeit zu gewährleisten, können Mandanten zwei RD-Lizenz-Server-Computer in derselben verfügbarkeitsgruppe bereitstellen. Alle Remotedesktop-Server in der Mandanten-Umgebung fallen beide Remotedesktop-Lizenzserver zu Benutzern, die für neue Sitzungen herstellen, selbst wenn einer der Server ausfällt.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Lizenzieren Sie Ihre RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)](rds-client-access-license.md)
* [Aktivieren des Lizenzservers Remote Desktop Services](rds-activate-license-server.md)
* [Verfolgen Sie Ihre Remote Desktop Services-Clientzugriffslizenzen (TS CALs)](rds-track-cals.md)
* [Microsoft Volume Licensing: Lizenzierungsoptionen für Dienstanbieter](https://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx)