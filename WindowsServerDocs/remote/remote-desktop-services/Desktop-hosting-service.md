---
title: Desktophosting-Dienst
description: Hier werden die Komponenten eines Desktophostingdiensts beschrieben.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
author: heidilohr
manager: lizross
ms.openlocfilehash: 64e433ed379ca322996bcfe2d0ddd513e074b85e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854713"
---
# <a name="desktop-hosting-service"></a>Desktophosting-Dienst

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

In diesem Artikel erfährst du mehr über die Komponenten des Desktophostingdiensts.

## <a name="tenant-environment"></a>Mandantenumgebung

Jede Rolle erfüllt in der Mandantenumgebung einen bestimmten Zweck, wie unter [Remotedesktopdienste – Rollen](rds-roles.md) beschrieben.

Der Desktophostingdienst des Anbieters wird als Gruppe isolierter Mandantenumgebungen implementiert. Jede Mandantenumgebung besteht aus einem Speichercontainer, einer Gruppe von virtuellen Computern und einer Kombination von Azure-Diensten, die alle über ein isoliertes virtuelles Netzwerk miteinander kommunizieren. Jeder virtuelle Computer enthält eine oder mehrere Komponenten, die die gehostete Desktopumgebung des Mandanten bilden. In den folgenden Unterabschnitten werden die Komponenten beschrieben, aus denen sich die gehostete Desktopumgebung des jeweiligen Mandanten zusammensetzt.

## <a name="active-directory-domain-services"></a>Active Directory-Domänendienste (AD DS)

Active Directory Domain Services (AD DS) stellt die Domänen- und Gesamtstrukturinformationen bereit, damit sich die Benutzer des Mandanten bei den Desktops und Anwendungen anmelden und ihre Workloads ausführen können. Dadurch kannst du auch Dateifreigaben und Datenbanken einrichten, die ggf. für Windows-Anwendungen erforderlich sind, und eine Verbindung mit ihnen herstellen.

Für Gesamtstruktur des Mandanten ist keine Vertrauensstellung für die Verwaltungsgesamtstruktur des Anbieters erforderlich. In der Domäne des Mandanten kann ein Domänenadministratorkonto eingerichtet werden, damit die Techniker des Anbieters administrative Aufgaben in der Mandantenumgebung wie etwa die Überwachung des Systemstatus und die Anwendung von Softwareupdates ausführen und bei der Problembehandlung und Konfiguration behilflich sein können.

AD DS kann auf unterschiedliche Weise bereitgestellt werden:

1. Du kannst Azure Active Directory Domain Services in der virtuellen Netzwerkumgebung des Mandanten aktivieren. Dadurch wird auf der Grundlage der in Azure AD vorhandenen Benutzer und Gruppen eine verwaltete AD DS-Instanz für den Mandanten erstellt.
2. Du kannst einen eigenständigen AD DS-Server in der virtuellen Netzwerkumgebung des Mandanten einrichten. Dadurch erhältst du die vollständige Kontrolle über die auf virtuellen Computern ausgeführte AD DS-Instanz.
3. Du kannst eine Site-to-Site-VPN-Verbindung mit einem lokalen AD DS-Server des Mandanten herstellen. Dadurch kann der Mandant eine Verbindung mit seiner vorhandenen AD DS-Instanz herstellen und die Duplizierung von Benutzern, Gruppen, Organisationseinheiten und Ähnlichem reduzieren.

Weitere Informationen findest du in den folgenden Artikeln:

* [Dokumentation zu Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/)
* [Handbuch zur Referenzarchitektur für das Desktophosting für Windows Server 2012 R2](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Erstellen einer Site-to-Site-Verbindung im Azure-Portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL-Datenbank

Bereitstellungsinformationen wie etwa die Zuordnung der Verbindungen aktueller Benutzer zu Hostservern werden vom Remotedesktop-Verbindungsbroker in einer hoch verfügbaren SQL-Datenbank gespeichert.

Eine SQL-Datenbank kann auf unterschiedliche Weise bereitgestellt werden:

1. Du kannst eine Azure SQL-Datenbank in der Mandantenumgebung erstellen. Dadurch erhältst du die Funktionen einer redundanten SQL-Datenbank, ohne die Server selbst verwalten müssen. Außerdem musst du bei dieser Lösung nicht in die Infrastruktur investieren, sondern nur für das bezahlen, was du tatsächlich nutzt.
2. Du kannst einen SQL Server-AlwaysOn-Cluster erstellen. Dadurch kannst du die vorhandene SQL Server-Infrastruktur nutzen und erhältst die vollständige Kontrolle über die SQL Server-Instanzen.

Weitere Informationen zum Einrichten einer hoch verfügbaren SQL-Datenbankinfrastruktur findest du in den folgenden Artikeln:

* [Worum handelt es sich beim Azure SQL-Datenbank-Dienst?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
* [Referenz für die Erstellung und Konfiguration von Always On-Verfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017)
* [Hinzufügen des Remotedesktop-Verbindungsbrokerservers zur Bereitstellung und Konfigurieren von hoher Verfügbarkeit](rds-connection-broker-cluster.md)

## <a name="file-server"></a>Dateiserver

Der Dateiserver verwendet das SMB 3.0-Protokoll (Server Message Block), um freigegebene Ordner bereitzustellen. Diese freigegebenen Ordner dienen zum Erstellen und Speichern von Benutzerprofil-Datenträgerdateien (VHDX-Dateien) für die Datensicherung und ermöglichen es Benutzern, Daten im Rahmen des Clouddiensts des Mandanten an andere Benutzer weiterzugeben.

Der virtuelle Computer, der den Dateiserver bereitstellt, muss über einen angefügten Azure-Datenträger verfügen und mit freigegebenen Ordnern konfiguriert sein. Azure-Datenträger verwenden Durchschreibcache, um zu gewährleisten, dass Schreibvorgänge auf dem Datenträger bei einem Neustart des virtuellen Computers nicht gelöscht werden.

Bei kleinen Mandanten können der Dateiserver und die [RD-Lizenzierungsrolle](rds-roles.md#remote-desktop-licensing) auf einem einzelnen virtuellen Computer in der Mandantenumgebung zusammengefasst werden, um Kosten zu sparen.

Weitere Informationen findest du in den folgenden Artikeln:

* [Speicher](../../storage/storage.md)
* [Anfügen eines verwalteten Datenträgers an einen virtuellen Windows-Computer im Azure-Portal](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json)

### <a name="user-profile-disks"></a>Benutzerprofil-Datenträger

Benutzerprofil-Datenträger ermöglichen es Benutzern, persönliche Einstellungen und Dateien zu speichern, wenn sie bei einer Sitzung auf einem RD-Sitzungshostserver in einer Sammlung angemeldet sind, und später auf die gleichen Einstellungen und Dateien zuzugreifen, wenn sie sich bei einem anderen [RD-Sitzungshostserver](rds-roles.md#remote-desktop-session-host) der Sammlung anmelden. Bei der ersten Anmeldung des Benutzers erstellt der Dateiserver des Mandanten einen Benutzerprofil-Datenträger. Dieser wird auf dem RD-Sitzungshostserver eingebunden, mit dem der Benutzer gerade verbunden ist. Bei jeder weiteren Anmeldung wird der Benutzerprofil-Datenträger auf dem entsprechenden RD-Sitzungshostserver eingebunden, und bei jeder Abmeldung wird die Einbindung wieder aufgehoben. Nur der Benutzer kann auf den Inhalt des Benutzerprofil-Datenträgers zugreifen.