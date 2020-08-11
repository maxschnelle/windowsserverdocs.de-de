---
title: Grundlegendes zur Desktophostingumgebung
description: Übersicht über eine RDS-Bereitstellung mithilfe von Azure IaaS.
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 7e53bb5a8c7a5497e726526b7e3d371acf3bcc1b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996319"
---
# <a name="understanding-the-desktop-hosting-environment"></a>Grundlegendes zur Desktophostingumgebung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Die folgenden Informationen beschreiben die Komponenten des Desktophostingdiensts.

## <a name="tenant-environment"></a>Mandantenumgebung
Der Desktophostingdienst des Anbieters wird als Gruppe isolierter Mandantenumgebungen implementiert. Jede Mandantenumgebung besteht aus einem Speichercontainer, einer Gruppe von virtuellen Computern und einer Kombination von Azure-Diensten, die alle über ein isoliertes virtuelles Netzwerk miteinander kommunizieren. Jeder virtuelle Computer enthält eine oder mehrere Komponenten, die die gehostete Desktopumgebung des Mandanten bilden. In den folgenden Unterabschnitten werden die Komponenten beschrieben, aus denen sich die gehostete Desktopumgebung des jeweiligen Mandanten zusammensetzt.

## <a name="remote-desktop-services"></a>Remotedesktopdienste
In einer Desktophostingumgebung werden die folgenden RDS-Rollen zwischen verschiedenen VMs installiert:

  - Remotedesktop-Verbindungsbroker
  - Remotedesktopgateway
  - Remotedesktoplizenzierung
  - Remotedesktop-Sitzungshost
  - Remotedesktop-Webzugriff

Eine vollständige Beschreibung jeder dieser Rollen und ihrer Interaktion untereinander findest du im Dokument [Desktophosting-Dienst](./desktop-hosting-service.md).

##  <a name="azure-active-directory-domain-services"></a>(Azure) Active Directory Domain Services
Es gibt mehrere Möglichkeiten zum Herstellen einer Verbindung mit und Verwalten von Active Directory Domain Services (AD DS) für eine Desktophostingumgebung in Azure:

1. Erstellen eines virtuellen Computers in der Mandantenumgebung, die die AD DS-Rolle ausführt
2. Erstellen einer Site-to-Site-VPN-Verbindung mit der lokalen Umgebung des Mandanten, um einen vorhandenen AD DS zu nutzen
3. Verwenden der PaaS-Rolle von Azure AD Domain Services, die basierend auf dem Azure Active Directory des Mandanten eine Domäne im virtuellen Netzwerk des Mandanten erstellt

Bei Remote Desktop Services muss der Mandant über eine Active Directory-Instanz verfügen, um den Zugriff auf die Umgebung, die Benutzerprofilspeicherung und die Überwachung innerhalb der Bereitstellung zu verwalten. Bei Verwendung der standardmäßigen AD DS (nicht in Azure) ist keine Vertrauensstellung der Verwaltungsgesamtstruktur des Anbieters für die Gesamtstruktur des Mandanten erforderlich. In der Domäne des Mandanten kann ein Domänenadministratorkonto eingerichtet werden, damit die Techniker des Anbieters administrative Aufgaben in der Mandantenumgebung wie etwa die Überwachung des Systemstatus und die Anwendung von Softwareupdates ausführen und bei der Problembehandlung und Konfiguration behilflich sein können.

Weitere Informationen: [Dokumentation zu Azure Active Directory Domain Services](https://azure.microsoft.com/documentation/services/active-directory-ds/)
[Installieren einer neuen Active Directory-Gesamtstruktur in einem virtuellen Azure-Netzwerk](../../identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md)
[Erstellen eines Ressourcen-Manager-VNet mit einer Site-to-Site-VPN-Verbindung unter Verwendung des Azure-Portals](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="azure-sql-database"></a>Azure SQL-Datenbank
Azure SQL-Datenbank ermöglicht Hostern, ihre RDS-Bereitstellung zu erweitern, ohne einen vollständigen SQL Server Always-On-Cluster bereitstellen und warten zu müssen. Bereitstellungsinformationen wie etwa die Zuordnung der Verbindungen aktueller Benutzer zu Endhostservern werden vom Remotedesktop-Verbindungsbroker in einer Azure SQL-Datenbank-Instanz gespeichert. Wie andere Azure-Dienste verfolgt Azure SQL-Datenbank ein Verbrauchsmodell, das sich ideal für jede Bereitstellungen jeder Größe eignet.

Weitere Informationen: [Worum handelt es sich beim Azure SQL-Datenbank-Dienst?](/azure/azure-sql/database/sql-database-paas-overview)

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory-Anwendungsproxy
Der Azure AD-Anwendungsproxy ist ein Dienst, der in kostenpflichtigen SKUs von Azure Active Directory bereitgestellt wird. Mit diesem Dienst können Benutzer über den Azure-eigenen Reverseproxydienst eine Verbindung mit internen Anwendungen herstellen. Dadurch können die RD-Web- und RD-Gatewayendpunkte innerhalb des virtuellen Netzwerks verborgen werden. Das hat den Vorteil, dass sie nicht mit einer öffentlichen IP-Adresse für das Internet verfügbar gemacht werden müssen. So können Hoster außerdem die Anzahl virtueller Computer in der Mandantenumgebung verringern, ohne die Bereitstellung einzuschränken.

Weitere Informationen: [Tutorial: Hinzufügen einer lokalen Anwendung für den Remotezugriff über den Anwendungsproxy in Azure Active Directory](/azure/active-directory/manage-apps/application-proxy-add-on-premises-application)

## <a name="file-server"></a>Dateiserver
Der Dateiserver verwendet das SMB 3.0-Protokoll (Server Message Block), um freigegebene Ordner bereitzustellen. Diese freigegebenen Ordner dienen zum Erstellen und Speichern von Benutzerprofil-Datenträgerdateien (VHDX-Dateien) für die Datensicherung und um Benutzern zu ermöglichen, Daten im Rahmen des virtuellen Netzwerks des Mandanten an andere Benutzer weiterzugeben.

Die VM, die den Dateiserver bereitstellt, muss über einen angefügten Azure-Datenträger verfügen und mit freigegebenen Ordnern konfiguriert sein. Azure-Datenträger verwenden den Durchschreibcache, was garantiert, dass auf den Datenträger geschriebene Daten auch bei Neustarts der VM erhalten bleiben.

Für kleine Mandanten können die Kosten reduziert werden, indem der Dateiserver mit der VM kombiniert wird, auf der die Rollen RD-Verbindungsbroker und RD-Lizenzierung auf einer einzigen VM in der Umgebung des Mandanten ausgeführt werden.

Zusätzliche Informationen [Übersicht über Datei- und Speicherdienste](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))
[Anfügen eines Datenträgers an einen virtuellen Computer](https://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)

### <a name="user-profile-disks"></a>Benutzerprofil-Datenträger
Benutzerprofil-Datenträger ermöglichen Benutzern, persönliche Einstellungen und Dateien zu speichern, wenn sie bei einer Sitzung auf einem RD-Sitzungshostserver in einer Sammlung angemeldet sind, und später auf die gleichen Einstellungen und Dateien zugreifen können, wenn sie sich bei einem anderen RD-Sitzungshostserver der Sammlung anmelden. Bei der ersten Anmeldung des Benutzers wird auf dem Dateiserver des Mandanten ein Benutzerprofil-Datenträger erstellt. Dieser wird auf dem RD-Sitzungshostserver eingebunden, mit dem der Benutzer verbunden ist. Bei jeder weiteren Anmeldung wird der Benutzerprofil-Datenträger auf dem entsprechenden RD-Sitzungshostserver eingebunden, und bei jeder Abmeldung wird die Einbindung wieder aufgehoben. Auf den Inhalt des Benutzerprofil-Datenträgers kann nur dieser Benutzer zugreifen.