---
title: Grundlegendes zu den desktophosting-Umgebung
description: Übersicht über ein RDS-Deployhment mithilfe von Azure IaaS.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 880fc8f9fa2db5ec56d2117e02c069650c61584a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877921"
---
# <a name="understanding-the-desktop-hosting-environment"></a>Grundlegendes zu den desktophosting-Umgebung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Informationen beschreiben die Komponenten des Desktops Hostingdienst.  
  
## <a name="tenant-environment"></a>Umgebung für Mandanten  
Der Anbieter desktophosting-Dienst wird als eine Reihe von Umgebungen isolierten Mandanten implementiert. Jedes Mandanten Umgebung besteht aus einem Speichercontainer, eine Gruppe von virtuellen Computern und eine Kombination von Azure-Dienste, die alle Kommunikation über einem isolierten virtuellen Netzwerk. Jeder virtuelle Computer enthält eine oder mehrere Komponenten, aus denen die Mandanten-desktop-Umgebung gehosteten besteht. In den folgenden Unterabschnitten werden die Komponenten, aus denen jedes Mandanten gehosteten desktop-Umgebung beschrieben.

## <a name="remote-desktop-services"></a>Remotedesktopdienste
In einem desktophosting-Umgebung werden die folgenden Remotedesktopdienste-Rollen von verschiedenen virtuellen Computer installiert:

  - Remotedesktop-Verbindungsbroker
  - Remotedesktopgateway
  - Remotedesktoplizenzierung
  - Remotedesktop-Sitzungshost
  - Web Access für Remotedesktop

Eine vollständige Beschreibung der einzelnen diese Rollen und wie sie miteinander interagieren, finden Sie in der [Grundlegendes zu RDS-Rollen](Understanding-RDS-roles.md) Dokument.
  
##  <a name="azure-active-directory-domain-services"></a>(Azure) Active Directory-Domänendienste  
Es gibt mehrere Möglichkeiten zum Herstellen einer Verbindung mit und Verwalten von Active Directory Domain Services (AD DS) für eine desktophosting-Umgebung in Azure:

1. Erstellen eines virtuellen Computers in der AD DS-Rolle Ausführen des Mandanten-Umgebung
2. Erstellen Sie eine Standort-zu-Standort-VPN-Verbindung mit lokalen Umgebung des Mandanten verwenden Sie ein vorhandenes AD DS
3. Verwenden Sie die Azure AD Domain Services PaaS-Rolle, die eine Domäne auf der virtuellen mandantennetzwerk basierend auf des Mandantenverwaltungs des Azure Active Directory erstellt.

Bei Remote Desktop Services, muss der Mandant ein Active Directory zum Verwalten des Zugriffs in die Umgebung, Speichern von Benutzerprofilen, sein und innerhalb der Bereitstellung überwachen. Wenn Sie die standardmäßige (nicht Azure) AD DS verwenden, erfordert des Mandanten Gesamtstruktur Vertrauensstellung mit der Anbieter Management-Gesamtstruktur keine. Ein Domänenadministratorkonto kann in der Mandanten-Domäne eingerichtet werden, um technische Personal des Anbieters, um administrative Aufgaben in der Mandanten-Umgebung (z. B. das Überwachen des Systemstatus und Anwenden von Softwareupdates) ausführen und zur Unterstützung bei der zulassen Problembehandlung, und klicken Sie mit der Konfiguration.  
    
Weitere Informationen:  
[Dokumentation zu Azure Active Directory Domain Services](https://azure.microsoft.com/documentation/services/active-directory-ds/)  
[Installieren einer neuen Active Directory-Gesamtstruktur in einem Azure virtual network](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/)  
[Erstellen Sie eine Resource Manager-VNet mit einer Standort-zu-Standort-VPN-Verbindung über das Azure-Portal](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  
  
## <a name="azure-sql-database"></a>Azure SQL-Datenbank  
Azure SQL-Datenbank ermöglicht Hostinganbietern, zu ihren Remote Desktop Services-Bereitstellung zu erweitern, ohne die Bereitstellung und Verwaltung eines vollständigen SQL Server Always On-Clusters. Azure SQL-Datenbank wird von der Remote Desktop Connection Broker zum Speichern von Informationen zur Bereitstellung, z. B. die Zuordnung des aktuellen Benutzers Verbindungen mit End-Host-Servern verwendet. Wie andere Azure-Dienste folgt Azure SQL-Datenbank ein verbrauchsmodell, das sich ideal für jede Größe-Bereitstellung.   
  
Weitere Informationen:  
[Was ist SQL-Datenbank?](https://azure.microsoft.com/documentation/articles/sql-database-technical-overview/)  
  
## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory-Anwendungsproxy  
Azure Active Directory-Anwendungsproxy ist ein Dienst in kostenpflichtige-SKUs von Azure Active Directory, mit die Benutzer eine Verbindung mit internen Anwendungen über Azure eigenen Reverse-Proxy-Dienst herstellen können. Dadurch können die RD-Web und RD-Gateway-Endpunkte innerhalb des virtuellen Netzwerks, und Sie müssen für das Internet über eine öffentliche IP-Adresse verfügbar gemacht werden ausgeblendet werden soll. Dadurch können weitere Hoster die Anzahl der virtuellen Computer des Mandanten Umgebung zusammengefasst, während gleichzeitig eine vollständige Bereitstellung.
  
Weitere Informationen:  
[Aktivieren von Azure AD-Anwendungsproxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-enable/)  
    
## <a name="file-server"></a>Dateiserver  
Der Dateiserver bietet freigegebenen Ordner mithilfe des Server Message Block (SMB) 3.0-Protokolls. Zum Erstellen und speichern Datenträger benutzerprofildateien (%% amp;quot;.vhdx%%amp;quot;) zum Sichern von Daten, und Benutzer auf einen Ort zum Freigeben von Daten für andere Benutzer im virtuellen Netzwerk des Mandanten können, werden die freigegebenen Ordner verwendet.
  
Der virtuelle Computer zum Bereitstellen des Dateiservers muss einen Azure-Datenträger angeschlossen und mit freigegebenen Ordnern konfiguriert haben. Azure-Datenträger verwenden, Write-through-caching die Garantien, die auf den Datenträger schreibt über Neustarts des virtuellen Computers beibehalten werden.  
  
Für kleine Mandanten kann die Kosten reduziert werden, durch die Kombination des Dateiservers mit dem virtuellen Computer, die die Rollen des Remotedesktop-Verbindungsbroker und RD-Lizenzierung auf einen einzelnen virtuellen Computer in der Mandanten-Umgebung ausgeführt.  
  
Weitere Informationen  
[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)  
[Gewusst wie: Anfügen eines Datenträgers an einen virtuellen Computer](http://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)  
  
### <a name="user-profile-disks"></a>Benutzerprofil-Datenträger  
Benutzerprofil-Datenträger können Benutzer Persönliche Einstellungen und Dateien speichern, wenn sie mit einer Sitzung auf einem Remotedesktop-Sitzungshostserver in einer Auflistung angemeldet sind, und klicken Sie dann den Zugriff auf den gleichen Einstellungen und Dateien verfügen, bei der Anmeldung auf einen anderen RD Session Host-Server in der Auflistung. Beim ersten des Benutzers in Anmelden ein Benutzerprofil-Datenträger wird auf Dateiserver des Mandanten erstellt, und dieser Datenträger wird bereitgestellt, mit dem Remotedesktop-Sitzungshost-Server mit dem der Benutzer verbunden ist. Für jede nachfolgende-Anmeldung der Benutzerprofil-Datenträger auf den entsprechenden RD-Sitzungshostserver bereitgestellt wird, und mit jedem Abmeldung kann nicht eingebunden. Der Inhalt des Benutzerprofil-Datenträger können nur von diesem Benutzer zugegriffen werden.  
  


