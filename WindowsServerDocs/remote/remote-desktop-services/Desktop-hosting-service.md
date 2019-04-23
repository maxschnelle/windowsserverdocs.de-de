---
title: Desktophosting-Dienst
description: Beschreibt die Komponenten der Desktop, Dienst hostet.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: dougkim
ms.openlocfilehash: adbb9fd69bc61d2e877cadb0484a4e42093f262a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840471"
---
# <a name="desktop-hosting-service"></a>Desktophosting-Dienst

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Artikel erfahren Sie mehr über den Desktop, dem des Diensts Komponenten gehostet werden.

## <a name="tenant-environment"></a>Umgebung für Mandanten

Siehe [Remote Desktop Services-Rollen](rds-roles.md), jede Rolle spielt eine distinct in die Mandanten-Umgebung.

Der Anbieter desktophosting-Dienst wird als eine Reihe von Umgebungen isolierten Mandanten implementiert. Jedes Mandanten Umgebung besteht aus einem Speichercontainer, eine Gruppe von virtuellen Computern und eine Kombination von Azure-Dienste, die alle Kommunikation über einem isolierten virtuellen Netzwerk. Jeder virtuelle Computer enthält eine oder mehrere Komponenten, aus denen die Mandanten-desktop-Umgebung gehosteten besteht. In den folgenden Unterabschnitten werden die Komponenten, aus denen jedes Mandanten gehosteten desktop-Umgebung beschrieben.

## <a name="active-directory-domain-services"></a>Active Directory Domain Services

Active Directory-Domänendienste (AD DS) bietet die Domänen- und Gesamtstruktur-Informationen, sodass des Mandanten Benutzer auf die Desktops und Anwendungen, um ihre Workloads durchzuführen anmelden können. Dies können Sie zum Einrichten oder Herstellen einer Verbindung erforderlichen freigegebenen Ordner und Datenbanken, die für Windows-Anwendungen benötigen Sie möglicherweise mit.

Die Mandanten-Gesamtstruktur erfordert kein Vertrauensstellung mit der Anbieter Management-Gesamtstruktur. Ein Domänenadministratorkonto kann in der Mandanten-Domäne eingerichtet werden, um technische Personal des Anbieters, um administrative Aufgaben in der Mandanten-Umgebung (z. B. das Überwachen des Systemstatus und Anwenden von Softwareupdates) ausführen und zur Unterstützung bei der zulassen Problembehandlung, und klicken Sie mit der Konfiguration.

Es gibt mehrere Möglichkeiten zum Bereitstellen von AD DS:

1. Aktivieren Sie Azure Active Directory-Domänendienste im virtuellen Netzwerk des Mandanten-Umgebung. Dadurch wird eine verwaltete AD DS-Instanz erstellt, für den Mandanten, die basierend auf den Benutzer und Gruppen, die in Azure AD vorhanden.
2. Richten Sie einen eigenständigen AD DS-Server im virtuellen Netzwerk des Mandanten-Umgebung. Dies gibt Ihnen vollständige Kontrolle der AD DS-Instanz, die auf virtuellen Computern.
3. Erstellen Sie eine Standort-zu-Standort-VPN-Verbindung mit einem AD DS-Server befindet sich auf dem Firmengelände des Mandanten. Dadurch wird der Mandant ihrer vorhandenen AD DS-Instanz herstellen und diese Duplizierung von Benutzern, Gruppen, Organisationseinheiten und So weiter zu reduzieren.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Azure Active Directory Domain Services-Dokumentation](https://docs.microsoft.com/azure/active-directory-domain-services/)
* [Desktophosting-Referenzarchitekturhandbuch für Windows Server 2012 R2](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Erstellen Sie eine Standort-zu-Standort-Verbindung im Azure-portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL-Datenbank

Eine hoch verfügbare SQL-Datenbank wird von der Remote Desktop Connection Broker zum Speichern von Informationen zur Bereitstellung, z. B. die Zuordnung des aktuellen Benutzers Verbindungen an die Hostserver verwendet.

Es gibt mehrere Möglichkeiten zum Bereitstellen einer SQL­Datenbank:

1. Erstellen Sie eine Azure SQL-Datenbank, in der Mandanten-Umgebung. Dadurch erhalten Sie mit der Funktionalität von eine redundante SQL-Datenbank ohne dass Sie die Server selbst verwalten müssen. Dadurch können Sie bezahlen, was Sie nutzen, anstatt in die Infrastruktur zu investieren.
2. Erstellen eines SQL Server AlwaysOn-Clusters. Dies können Sie vorhandene SQL Server-Infrastruktur einsetzen und bietet Ihnen vollständige Kontrolle über die SQL Server-Instanzen.

Weitere Informationen zum Einrichten einer hoch verfügbaren SQL-Datenbank-Infrastruktur finden Sie unter den folgenden Artikeln:

* [Was ist Azure SQL-Datenbankdienst?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
* [Erstellung und Konfiguration von Verfügbarkeitsgruppen (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017).
* [Die Bereitstellung der Remotedesktop-Verbindungsbrokerserver hinzu, und Konfigurieren von hochverfügbarkeit](rds-connection-broker-cluster.md).

## <a name="file-server"></a>Dateiserver

Der Dateiserver verwendet das Server Message Block (SMB) 3.0-Protokoll zu freigegebenen Ordnern. Diese freigegebenen Ordner werden zum Erstellen und speichern die Datenträger benutzerprofildateien (%% amp;quot;.vhdx%%amp;quot;) zum Sichern von Daten und ermöglicht Benutzern das Freigeben von Daten mit anderen Cloud-Dienst des Mandanten.

Der virtuelle Computer, die den Server bereitstellt, benötigen einen Azure-Datenträger angeschlossen und mit freigegebenen Ordnern konfiguriert. Azure-Datenträger verwenden, Write-through-caching, garantieren, dass Schreibvorgänge auf den Datenträger nicht gelöscht werden, wenn der virtuelle Computer neu gestartet wird.

Kleine Mandanten können Kostensenkung durch die Kombination des Dateiservers und [RD-Lizenzierung Rolle](rds-roles.md#remote-desktop-licensing) auf einem einzelnen virtuellen Computer in der Mandanten-Umgebung.

Weitere Informationen finden Sie in den folgenden Artikeln:

* [Speicher in WindowsServer](../../storage/storage.md)
* [Gewusst wie: Anfügen ein verwalteten Datenträgers an eine Windows-VM im Azure-portal](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json)

### <a name="user-profile-disks"></a>Benutzerprofil-Datenträger

Benutzerprofil-Datenträger können Benutzer Persönliche Einstellungen und Dateien speichern, wenn sie mit einer Sitzung auf einem Remotedesktop-Sitzungshostserver in einer Auflistung angemeldet sind, und klicken Sie dann Zugriff auf den gleichen Einstellungen und Dateien, bei der Anmeldung zu einer anderen [RD-Sitzungshost](rds-roles.md#remote-desktop-session-host) der Server in der Auflistung. Wenn der Benutzer zuerst anmeldet, erstellt des Mandanten Scale-Out File Server einen Benutzerprofil-Datenträger, der auf dem RD-Sitzungshostserver bereitgestellt Ruft ab, die der Benutzer derzeit verbunden ist. Der Benutzerprofil-Datenträger wird für jede nachfolgende-Anmeldung, um den entsprechenden RD-Sitzungshostserver bereitgestellt, und es wird mit jedem aufgehoben abmelden. Nur der Benutzer kann die Benutzerprofil-Datenträger-Inhalt zugreifen.