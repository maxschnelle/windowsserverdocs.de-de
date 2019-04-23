---
title: Erste Schritte mit User Access Logging
desctription: Describes the User Access Logging feature and how to start using it.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-user-access-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c395b8b-3b35-4042-b9cc-07e438f86d50
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8656bf278519b48f8d26008fd98e46428106e511
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861501"
---
# <a name="get-started-with-user-access-logging"></a>Erste Schritte mit User Access Logging

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Benutzerzugriffsprotokollierung (User Access Logging, UAL) ist die Funktion in Windows Server, der die Client-Verwendungsdaten nach Rolle und Produkten auf einem lokalen Server aggregiert. Sie können Windows Server-Administratoren, die Anforderungen von Clientcomputern nach Rollen und Diensten auf einem lokalen Server messen.  
  
Benutzerzugriffsprotokollierung installiert und standardmäßig aktiviert, und erfasst Daten nahezu in Echtzeit. Es ist keine Konfiguration durch den Administrator erforderlich, wenngleich die Benutzerzugriffsprotokollierung deaktiviert oder aktiviert werden kann. Weitere Informationen finden Sie unter [Manage User Access Logging](Manage-User-Access-Logging.md). Die Benutzerzugriffsprotokollierung-Dienst aggregiert clientverwendungsdaten nach Rollen und Produkten in lokalen Datenbankdateien.  IT-Administratoren können später Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) oder Windows PowerShell-Cmdlets verwenden, um Mengen und Instanzen nach Serverrolle (oder Softwareprodukt), Benutzer, Gerät, lokalem Server und Datum abzurufen.  
  
> [!NOTE]  
> Die UAL unterstützt das [Microsoft Assessment and Planning Toolkit](https://go.microsoft.com/fwlink/?LinkID=111000).  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Die Benutzerzugriffsprotokollierung aggregiert eindeutige Client-Gerät und benutzeranforderungsereignisse, die in einer lokalen Datenbank protokolliert werden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen.  Darüber hinaus wurde die Benutzerzugriffsprotokollierung erweitert, um nicht-Microsoft-Software-Entwickler von Windows Server aggregiert werden deren Ereignisse der Benutzerzugriffsprotokollierung Instrumentieren zu aktivieren.  
  
Die Benutzerzugriffsprotokollierung kann die folgenden Aufgaben ausführen:  
  
-   Berechnen der Clientbenutzeranforderungen für lokale physische oder virtuelle Server.  
  
-   Berechnen der Clientbenutzeranforderungen für installierte Softwareprodukte auf einem lokalen physischen oder virtuellen Server.  
  
-   Abrufen von Daten auf einem lokalen Server, auf dem Hyper-V ausgeführt wird, um Phasen mit hoher und niedriger Nachfrage auf dem Hyper-V-Computer zu ermitteln.  
  
-   Abrufen von Daten der Benutzerzugriffsprotokollierung von mehreren Remoteservern.  
  
Darüber hinaus können Softwareentwickler Ereignisse der Benutzerzugriffsprotokollierung instrumentieren, die aggregiert und über WMI- und Windows PowerShell-Schnittstellen abgerufen werden können.  
  
Die folgenden Serverrollen und Dienste können von der Benutzerzugriffsprotokollierung unterstützt werden:  
  
-   Active Directory-Zertifikatdienste (AD CS)  
  
-   Active Directory Rights Management Services (AD RMS)  
  
-   BranchCache  
  
-   Domain Name System (DNS)  
  
    > [!NOTE]  
    > Die UAL sammelt DNS-Daten alle 24 Stunden, und es gibt ein separates UAL-Cmdlet für dieses Szenario.  
  
-   Dynamic Host Configuration-Protokoll (DHCP)  
  
-   Faxserver  
  
-   Dateidienste  
  
-   File Transfer Protocol-Server (FTP)  
  
-   Hyper-V  
  
    > [!NOTE]  
    > Die UAL sammelt Hyper-V-Daten alle 24 Stunden, und es gibt ein separates UAL-Cmdlet für dieses Szenario.  
  
-   Webserver (IIS)  
  
    > [!WARNING]  
    > Um die UAL mit IIS zu verwenden, müssen Sie "iisual.exe" verwenden. Weitere Informationen finden Sie unter [Analysieren von Clientverwendungsdaten mit der IIS-Benutzerzugriffsprotokollierung](http://www.iis.net/learn/manage/configuring-security/analyzing-client-usage-data-with-iis-user-access-logging).  
  
-   Microsoft Message Queuing-Dienste (MSMQ)  
  
-   Network Policy and Access Services  
  
-   Druck- und Dokumentdienste  
  
-   Routing- und RAS-Dienst (RRAS)  
  
-   Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)  
  
-   Windows Server Update Services (WSUS)  
  
> [!IMPORTANT]  
> Für direkt mit dem Internet verbundene Server (z. B. Webserver in einem Adressraum, der über das Internet zugänglich ist) oder Szenarien, in denen eine extrem hohe Leistung die primäre Funktion des Servers ist (z. B. in Umgebungen mit High Performance Computing-Auslastung), wird die Verwendung der Benutzerzugriffsprotokollierung nicht empfohlen. Die Benutzerzugriffsprotokollierung ist in erster Linie zur klein, Mittel und Intranet-Unternehmensszenarien, in denen umfangreiche erwartet wird, bestimmt, aber nicht so hoch wie Bereitstellungen, die Internetzugriff Datenverkehrsvolumen in regelmäßigen Abständen zu dienen.  
  
## <a name="BKMK_NEW"></a>Wichtige Funktionen  
In der folgenden Tabelle werden die Hauptfunktionen der Benutzerzugriffsprotokollierung und ihre mögliche Bedeutung beschrieben.  
  
|Funktionalität|Wert|  
|-----------------|---------|  
|Sammeln und Aggregieren von Client-Anforderungsereignisdaten nahezu in Echtzeit.|Es können bis zu drei Jahre an Daten gespeichert werden. **Wichtig:** Administratoren müssen die Konformität der gesammelten Daten und der Datenaufbewahrungsdauer mit den Datenschutzrichtlinien der Organisation und den lokalen Vorschriften erzwingen.|  
|Zum Abrufen von Client-Anforderungsdaten auf einem lokalen Server oder Remoteserver wird UAL über WMI- oder Windows PowerShell-Schnittstellen abgefragt.|UAL ermöglicht eine einzige Ansicht der fortlaufenden Nutzungsdaten. Server- und Unternehmensadministratoren können diese Daten abrufen und zusammen mit Business Administratoren auswerten, um die Nutzung von Volumenlizenzen für Software zu optimieren.|  
|Standardmäßig aktiviert.|Serveradministratoren müssen diese Funktion nicht konfigurieren oder anderweitig festlegen, damit alle wichtigen Funktionen verfügbar und funktionsfähig sind.|  
  
## <a name="data-logged-with-ual"></a>Von der Benutzerzugriffsprotokollierung protokollierte Daten  
Die folgenden benutzerspezifischen Daten werden von der Benutzerzugriffsprotokollierung protokolliert.  
  
|Daten|Beschreibung|  
|--------|---------------|  
|**UserName**|Benutzername des Clients, der die Einträge der Benutzerzugriffsprotokollierung aus installierten Rollen und Produkten ggf. begleitet.|  
|**ActivityCount**|Die Anzahl der Zugriffe auf eine Rolle oder einen Dienst durch einen bestimmten Benutzer.|  
|**FirstSeen**|Datum und Uhrzeit des ersten Zugriffs auf eine Rolle oder einen Dienst durch einen Benutzer.|  
|**LastSeen**|Datum und Uhrzeit des letzten Zugriffs auf eine Rolle oder einen Dienst durch einen Benutzer.|  
|**ProductName**|Name des Softwareprodukts (z. B. Windows), das Daten für die Benutzerzugriffsprotokollierung bereitstellt.|  
|**RoleGUID**|Die von der Benutzerzugriffsprotokollierung zugewiesene oder registrierte GUID, die die Serverrolle bzw. das installierte Produkt darstellt.|  
|**RoleName**|Name der Rolle, der Komponente oder des untergeordneten Produkts, die bzw. das die Daten für die Benutzerzugriffsprotokollierung bereitstellt. Hier besteht außerdem eine Verknüpfung mit %%amp;quot;ProductName%%amp;quot; und %%amp;quot;RoleGUID%%amp;quot;.|  
|**TenantIdentifier**|Eindeutige GUID für den Mandantenclient einer installierten Rolle oder ggf. für ein Produkt, das die Daten der Benutzerzugriffsprotokollierung begleitet.|  
  
Die folgenden gerätespezifischen Daten werden von der Benutzerzugriffsprotokollierung protokolliert.  
  
|Daten|Beschreibung|  
|--------|---------------|  
|**IPAddress**|IP-Adresse eines Clientgeräts, das für den Zugriff auf eine Rolle oder einen Dienst verwendet wird.|  
|**ActivityCount**|Die Anzahl der Zugriffe auf eine Rolle oder einen Dienst durch ein bestimmtes Gerät.|  
|**FirstSeen**|Datum und Uhrzeit der ersten Verwendung einer IP-Adresse für den Zugriff auf eine Rolle oder einen Dienst.|  
|**LastSeen**|Datum und Uhrzeit der letzten Verwendung einer IP-Adresse für den Zugriff auf eine Rolle oder einen Dienst.|  
|**ProductName**|Name des Softwareprodukts (z. B. Windows), das Daten für die Benutzerzugriffsprotokollierung bereitstellt.|  
|**RoleGUID**|Die von der Benutzerzugriffsprotokollierung zugewiesene oder registrierte GUID, die die Serverrolle bzw. das installierte Produkt darstellt.|  
|**RoleName**|Name der Rolle, der Komponente oder des untergeordneten Produkts, die bzw. das die Daten für die Benutzerzugriffsprotokollierung bereitstellt. Hier besteht außerdem eine Verknüpfung mit %%amp;quot;ProductName%%amp;quot; und %%amp;quot;RoleGUID%%amp;quot;.|  
|**TenantIdentifier**|Eindeutige GUID für den Mandantenclient einer installierten Rolle oder ggf. für ein Produkt, das die Daten der Benutzerzugriffsprotokollierung begleitet.|  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Die Benutzerzugriffsprotokollierung kann auf jedem Computer unter Windows Server-Versionen nach Windows Server 2012 verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
[Benutzerzugriffsprotokollierung](https://msdn.microsoft.com/library/windows/desktop/hh437528(v=vs.85).aspx) in MSDN.  
[Verwalten der Benutzer Zugriff auf die Protokollierung](Manage-User-Access-Logging.md)  
  

