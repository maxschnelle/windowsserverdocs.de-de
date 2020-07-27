---
title: 'Remotedesktopdienste: Rollen'
description: Hier werden die Komponenten eines Desktophostingdiensts beschrieben.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
author: heidilohr
manager: lizross
ms.openlocfilehash: 42116323dce36b071b2af20ff46330a8d39c13ed
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963062"
---
# <a name="remote-desktop-services-roles"></a>Remotedesktopdienste: Rollen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

In diesem Artikel werden die Rollen in einer Remotedesktopdienste-Umgebung beschrieben.

## <a name="remote-desktop-session-host"></a>Remotedesktop-Sitzungshost

Der Remotedesktop-Sitzungshost (RD-Sitzungshost) enthält die sitzungsbasierten Apps und Desktops, die du für Benutzer freigibst. Benutzer können auf diese Desktops und Apps über einen der Remotedesktopclients zugreifen, die unter Windows, macOS, iOS und Android ausgeführt werden. Außerdem können Benutzer eine Verbindung über einen unterstützten Browser herstellen, indem sie den Webclient verwenden.

Du kannst Desktops und Apps zu einzelnen oder mehreren RD-Sitzungshostservern (sogenannten Sammlungen) zusammenfassen. Diese Sammlungen kannst du für bestimmte Gruppen von Benutzern in den einzelnen Mandanten anpassen. So kannst du beispielsweise eine Sammlung erstellen, in der eine bestimmte Benutzergruppe auf bestimmte Apps zugreifen kann, Benutzer außerhalb der Gruppe jedoch keinen Zugriff auf diese Apps haben.

Bei kleinen Bereitstellungen kannst du Anwendungen direkt auf den RD-Sitzungshostservern installieren. Bei größeren Bereitstellungen empfiehlt es sich, ein Basisimage zu erstellen und virtuelle Computer auf der Grundlage dieses Images bereitzustellen.

Du kannst Sammlungen erweitern, indem du virtuelle RD-Sitzungshost-Servercomputer einer Sammlungsfarm hinzufügst, in der jeder virtuelle RDSH-Computer innerhalb einer Sammlung der gleichen Verfügbarkeitsgruppe zugewiesen ist. Dadurch erreichst du eine höhere Verfügbarkeit der Sammlung sowie eine höhere Skalierung und kannst mehr Benutzer oder ressourcenintensive Anwendungen unterstützen.

In den meisten Fällen wird ein RD-Sitzungshostserver von mehreren Benutzern gemeinsam verwendet. Dadurch wird eine möglichst effiziente Nutzung der Azure-Ressourcen für eine Desktophostinglösung erreicht. In dieser Konfiguration müssen sich die Benutzer bei Sammlungen mit einem Konto ohne Administratorrechte anmelden. Du kannst auch persönliche Sitzungsdesktopsammlungen erstellen, um einigen Benutzern uneingeschränkten Administratorzugriff auf ihren Remotedesktop zu gewähren.

Außerdem kannst du zur weiteren Desktopanpassung eine virtuelle Festplatte mit dem Windows Server-Betriebssystem erstellen, hochladen und als Vorlage für die Erstellung neuer virtueller RD-Sitzungshostcomputer verwenden.

Weitere Informationen findest du in den folgenden Artikeln:

* [Remotedesktopdienste: Schützen von Datenspeicher mit Benutzerprofil-Datenträgern](rds-plan-secure-data-storage.md)
* [Hochladen einer generalisierten VHD und Verwendung dieser zum Erstellen neuer VMs in Azure](/azure/virtual-machines/windows/upload-generalized-managed?toc=/azure/virtual-machines/windows/toc.json)
* [Update RDSH collection](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/) (Aktualisieren der RDSH-Sammlung) (ARM-Vorlage)

## <a name="remote-desktop-connection-broker"></a>Remotedesktop-Verbindungsbroker

Der Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker) verwaltet eingehende Remotedesktopverbindungen für RD-Sitzungshost-Serverfarmen. Über den RD-Verbindungsbroker werden sowohl Verbindungen mit Sammlungen vollständiger Desktops als auch Verbindungen mit Sammlungen von Remote-Apps abgewickelt. Der RD-Verbindungsbroker kann bei der Herstellung neuer Verbindungen die Last zwischen den Servern der Sammlung ausgleichen. Sollte die Verbindung mit einer Sitzung unterbrochen werden, verbindet der RD-Verbindungsbroker den Benutzer erneut mit dem korrekten RD-Sitzungshostserver und der unterbrochenen Sitzung, die weiterhin in der RD-Sitzungshostfarm vorhanden ist.

Zur Unterstützung von Anwendungsveröffentlichung und einmaligem Anmelden müssen sowohl auf dem RD-Verbindungsbrokerserver als auch auf dem Client übereinstimmende digitale Zertifikate installiert werden. Beim Entwickeln oder Testen eines Netzwerks kannst du ein selbstgeneriertes und selbstsigniertes Zertifikat verwenden. Für veröffentlichte Dienste wird dagegen ein digitales Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle benötigt. Der Name des Zertifikats muss dem internen vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des virtuellen RD-Verbindungsbrokercomputers entsprechen.

Du kannst den Remotedesktop-Verbindungsbroker von Windows Server 2016 auf dem gleichen virtuellen Computer installieren wie AD DS, um Kosten zu sparen. Wenn du horizontal skalieren musst, um mehr Benutzer zu unterstützen, kannst du auch zusätzliche virtuelle RD-Verbindungsbrokercomputer in der gleichen Verfügbarkeitsgruppe hinzufügen, um einen RD-Verbindungsbrokercluster zu erstellen.

Zuvor musst du jedoch entweder eine Azure SQL-Datenbank in der Mandantenumgebung bereitstellen oder eine SQL Server-AlwaysOn-Verfügbarkeitsgruppe erstellen.

Weitere Informationen findest du in den folgenden Artikeln:

* [Add the RD Connection Broker server to the deployment and configure high availability](rds-connection-broker-cluster.md) (Hinzufügen des RD-Verbindungsbrokerservers zur Bereitstellung und Konfigurieren von Hochverfügbarkeit)
* [SQL-Datenbank](desktop-hosting-service.md#sql-database) in „Desktophosting-Dienst“

## <a name="remote-desktop-gateway"></a>Remotedesktopgateway

Über das Remotedesktopgateway (RD-Gateway) können Benutzer in öffentlichen Netzwerken auf Windows-Desktops und Anwendungen zugreifen, die in den Clouddiensten von Microsoft Azure gehostet werden.

Die Remotedesktopgateway-Komponente verwendet Secure Sockets Layer (SSL), um den Kommunikationskanal zwischen den Clients und dem Server zu verschlüsseln. Der virtuelle RD-Gatewaycomputer muss über eine öffentliche IP-Adresse erreichbar sein, die eingehende TCP-Verbindungen am Port 443 sowie eingehende UDP-Verbindungen am Port 3391 zulässt. Dadurch können Benutzer über das Internet eine Verbindung unter Verwendung des HTTPS-Kommunikationstransportprotokolls bzw. des UDP-Protokolls herstellen.

Hierzu müssen auf dem Server und auf dem Client entsprechende digitale Zertifikate installiert sein. Beim Entwickeln oder Testen eines Netzwerks kannst du ein selbstgeneriertes und selbstsigniertes Zertifikat verwenden. Für einen veröffentlichten Dienst wird dagegen ein Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle benötigt. Der Name des Zertifikats muss dem FQDN entsprechen, der für den Zugriff auf das RD-Gateway verwendet wird. Das kann der nach außen gerichtete DNS-Name der öffentlichen IP-Adresse oder der CNAME-DNS-Eintrag sein, der auf die öffentliche IP-Adresse verweist.

Bei Mandanten mit weniger Benutzern können die Rollen „RD-Webzugriff“ und „RD-Gateway“ auf einem einzelnen virtuellen Computer zusammengefasst werden, um Kosten zu sparen. Du kannst aber auch weitere virtuelle RD-Gatewaycomputer zu einer RD-Gatewayfarm hinzufügen, um die Dienstverfügbarkeit zu erhöhen und eine horizontale Skalierung für mehr Benutzer durchzuführen. Virtuelle Computer in größeren RD-Gatewayfarmen sollten in einer Gruppe mit Lastenausgleich konfiguriert werden. Wenn du das RD-Gateway auf einem virtuellen Computer mit Windows Server 2016 verwendest, ist keine IP-Affinität erforderlich. Bei Verwendung eines virtuellen Computers mit Windows Server 2012 R2 dagegen schon.

Weitere Informationen findest du in den folgenden Artikeln:

* [Add high availability to the RD Web and Gateway web front](rds-rdweb-gateway-ha.md) (Hinzufügen von Hochverfügbarkeit zu RD-Web und RD-Gateway (Webfront))
* [Remotedesktopdienste – ortsunabhängiger Zugriff](rds-plan-access-from-anywhere.md)
* [Remote Desktop Services - Multi-Factor Authentication](rds-plan-mfa.md) (Remotedesktopdienste: mehrstufige Authentifizierung)

## <a name="remote-desktop-web-access"></a>Remotedesktop-Webzugriff

Web Access für Remotedesktop (Web Access für RD) ermöglicht Benutzern den Zugriff auf Desktops und Anwendungen über ein Webportal und startet diese über die native Microsoft-Remotedesktop-Clientanwendung des Geräts. Über das Webportal kannst du Windows-Desktops und Anwendungen für Windows-basierte und Windows-fremde Clientgeräte veröffentlichen. Außerdem kannst du Desktops oder Apps wahlweise für bestimmte Benutzer oder Gruppen veröffentlichen.

Web Access für RD benötigt Internetinformationsdienste (Internet Information Services, IIS). Eine HTTPS-Verbindung (Hypertext Transfer Protocol Secure) stellt einen verschlüsselten Kommunikationskanal zwischen den Clients und dem RD-Webserver bereit. Der virtuelle Computer für Web Access für RD muss über eine öffentliche IP-Adresse erreichbar sein, die eingehende TCP-Verbindungen am Port 443 zulässt, damit die Benutzer des Mandanten über das Internet eine Verbindung unter Verwendung des HTTPS-Kommunikationstransportprotokolls herstellen können.

Auf dem Server und den Clients müssen entsprechende digitale Zertifikate installiert sein. Bei der Entwicklung und zu Testzwecken kann ein selbstgeneriertes und selbstsigniertes Zertifikat verwendet werden. Bei einem veröffentlichten Dienst muss das digitale Zertifikat dagegen von einer vertrauenswürdigen Zertifizierungsstelle bezogen werden. Der Name des Zertifikats muss dem vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) entsprechen, der für den Zugriff auf Web Access für RD verwendet wird. Dabei kann es sich um den nach außen gerichteten DNS-Namen für die öffentliche IP-Adresse oder um den CNAME-DNS-Eintrag handeln, der auf die öffentliche IP-Adresse verweist.

Bei Mandanten mit weniger Benutzern können die Workloads „RD-Webzugriff“ und „Remotedesktopgateway“ zu einem einzelnen virtuellen Computer zusammengefasst werden, um Kosten zu sparen. Du kannst aber auch zusätzliche virtuelle RD-Webcomputer zu einer Farm für Web Access für RD hinzufügen, um die Dienstverfügbarkeit zu erhöhen und eine horizontale Skalierung für mehr Benutzer durchzuführen. In einer Farm für Web Access für RD mit mehreren virtuellen Computern müssen die virtuellen Computer in einer Gruppe mit Lastenausgleich konfiguriert werden.

Weitere Informationen zum Konfigurieren von Web Access für RD findest du in den folgenden Artikeln:

* [Einrichten des Remotedesktop-Webclients für Ihre Benutzer](clients/remote-desktop-web-client-admin.md)
* [Erstellen und Bereitstellen einer Remotedesktopdienste-Sammlung](rds-create-collection.md)
* [Create a Remote Desktop Services collection for desktops and apps to run](rds-create-collection.md) (Erstellen einer Remotedesktopdienste-Sammlung zum Ausführen von Desktops und Apps)

## <a name="remote-desktop-licensing"></a>Remotedesktoplizenzierung

Aktivierte Server für die Remotedesktoplizenzierung (RD-Lizenzierung) ermöglichen es Benutzern, eine Verbindung mit den RD-Sitzungshostservern herzustellen, auf denen die Desktops und Apps des Mandanten gehostet werden. In Mandantenumgebungen ist der RD-Lizenzierungsserver in der Regel bereits installiert. Für gehostete Umgebungen muss der Server jedoch im Modus „Pro Benutzer“ konfiguriert werden.

Der Dienstanbieter muss über genügend RDS-Abonnentenzugriffslizenzen (Subscriber Access Licenses, SALs) für alle autorisierten individuellen (nicht gleichzeitigen) Benutzer verfügen, die sich jeden Monat bei dem Dienst anmelden. Dienstanbieter können Microsoft Azure-Infrastrukturdienste direkt und SALs über das SPLA-Programm (Service Provider Licensing Agreement) von Microsoft erwerben. Kunden, die eine gehostete Desktoplösung benötigen, müssen die vollständige gehostete Lösung (Azure und RDS) vom Dienstanbieter erwerben.

Bei kleinen Mandanten können die Dateiserver- und die RD-Lizenzierungskomponente auf einem einzelnen virtuellen Computer zusammengefasst werden, um Kosten zu sparen. Um eine höhere Dienstverfügbarkeit zu erzielen, können Mandanten zwei virtuelle RD-Lizenzservercomputer in der gleichen Verfügbarkeitsgruppe bereitstellen. Alle RD-Server in der Mandantenumgebung werden mit beiden RD-Lizenzservern verknüpft, damit Benutzer auch dann eine Verbindung mit neuen Sitzungen herstellen können, wenn einer der Server ausfällt.

Weitere Informationen findest du in den folgenden Artikeln:

* [License your RDS deployment with client access licenses (CALs)](rds-client-access-license.md) (Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs))
* [Aktivieren des Remotedesktopdienste-Lizenzservers](rds-activate-license-server.md)
* [Track your Remote Desktop Services client access licenses (RDS CALs)](rds-track-cals.md) (Nachverfolgen deiner Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs))
* [Lizenzoptionen für Service Provider](https://www.microsoft.com/Licensing/licensing-programs/spla-program.aspx)
