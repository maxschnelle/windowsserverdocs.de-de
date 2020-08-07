---
title: Einstieg in die Benutzer Zugriffs Protokollierung
desctription: Describes the User Access Logging feature and how to start using it.
ms.topic: article
ms.assetid: 5c395b8b-3b35-4042-b9cc-07e438f86d50
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b5e8ae365fbf8130d134ab2f9fa555e952d012a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895640"
---
# <a name="get-started-with-user-access-logging"></a>Einstieg in die Benutzer Zugriffs Protokollierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Benutzer Zugriffs Protokollierung (User Access Logging, UAL) ist eine Funktion in Windows Server, die Client Verwendungs Daten nach Rolle und Produkten auf einem lokalen Server aggregiert. Dadurch können Windows Server-Administratoren Anforderungen von Client Computern nach Rollen und Diensten auf einem lokalen Server quantifizieren.

Die Benutzer Zugriffs Protokollierung ist standardmäßig installiert und aktiviert und erfasst Daten nahezu in Echtzeit. Es ist keine Konfiguration durch den Administrator erforderlich, wenngleich die Benutzerzugriffsprotokollierung deaktiviert oder aktiviert werden kann. Weitere Informationen finden Sie unter [Verwalten der Benutzerzugriffsprotokollierung](Manage-User-Access-Logging.md). Der Dienst für die Benutzer Zugriffs Protokollierung aggregiert Client Verwendungs Daten nach Rollen und Produkten in lokalen Datenbankdateien.  IT-Administratoren können später Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) oder Windows PowerShell-Cmdlets verwenden, um Mengen und Instanzen nach Serverrolle (oder Softwareprodukt), Benutzer, Gerät, lokalem Server und Datum abzurufen.

> [!NOTE]
> Die UAL unterstützt das [Microsoft Assessment and Planning Toolkit](https://go.microsoft.com/fwlink/?LinkID=111000).

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Die Benutzer Zugriffs Protokollierung aggregiert eindeutige Client Geräte-und Benutzer Anforderungs Ereignisse, die in einer lokalen Datenbank protokolliert werden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen.  Außerdem wurde die Benutzer Zugriffs Protokollierung erweitert, damit nicht-Microsoft-Softwareentwickler ihre UAL-Ereignisse so instrumentieren, dass Sie von Windows Server aggregiert werden.

Die Benutzer Zugriffs Protokollierung kann die folgenden Aufgaben ausführen:

-   Berechnen der Clientbenutzeranforderungen für lokale physische oder virtuelle Server.

-   Berechnen der Clientbenutzeranforderungen für installierte Softwareprodukte auf einem lokalen physischen oder virtuellen Server.

-   Abrufen von Daten auf einem lokalen Server, auf dem Hyper-V ausgeführt wird, um Phasen mit hoher und niedriger Nachfrage auf dem Hyper-V-Computer zu ermitteln.

-   Abrufen von Daten der Benutzerzugriffsprotokollierung von mehreren Remoteservern.

Außerdem können Softwareentwickler Ereignisse der Benutzer Zugriffs Protokollierung instrumentieren, die dann mithilfe von WMI-und Windows PowerShell-Schnittstellen aggregiert und abgerufen werden können.

Die folgenden Serverrollen und Dienste können von der Benutzerzugriffsprotokollierung unterstützt werden:

-   Active Directory-Zertifikatdienste (AD CS)

-   Active Directory Rights Management Services (AD RMS)

-   BranchCache

-   Domänennamenserver (DNS)

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
    > Um die UAL mit IIS zu verwenden, müssen Sie "iisual.exe" verwenden. Weitere Informationen finden Sie unter [Analysieren von Clientverwendungsdaten mit der IIS-Benutzerzugriffsprotokollierung](https://www.iis.net/learn/manage/configuring-security/analyzing-client-usage-data-with-iis-user-access-logging).

-   Microsoft Message Queuing-Dienste (MSMQ)

-   Network Policy and Access Services

-   Druck- und Dokumentdienste

-   Routing- und RAS-Dienst (RRAS)

-   Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)

-   Windows Server Update Services (WSUS)

> [!IMPORTANT]
> Für direkt mit dem Internet verbundene Server (z. B. Webserver in einem Adressraum, der über das Internet zugänglich ist) oder Szenarien, in denen eine extrem hohe Leistung die primäre Funktion des Servers ist (z. B. in Umgebungen mit High Performance Computing-Auslastung), wird die Verwendung der Benutzerzugriffsprotokollierung nicht empfohlen. Die Benutzer Zugriffs Protokollierung ist in erster Linie für Intranetszenarios in kleinen, mittelgroßen und großen Unternehmen gedacht, bei denen ein hohes Volumen erwartet wird, aber nicht so hoch wie bereit Stellungen, die regelmäßig Internet Datenverkehr verarbeiten.

## <a name="important-functionality"></a><a name="BKMK_NEW"></a>Wichtige Funktionalität
In der folgenden Tabelle werden die Hauptfunktionen der Benutzerzugriffsprotokollierung und ihre mögliche Bedeutung beschrieben.

|Funktionalität|Wert|
|-----------------|---------|
|Sammeln und Aggregieren von Client-Anforderungsereignisdaten nahezu in Echtzeit.|Es können bis zu drei Jahre an Daten gespeichert werden. **Wichtig:** Administratoren müssen die Konformität der gesammelten Daten und der Beibehaltungs Dauer der Daten mit den Datenschutzbestimmungen der Organisation und den lokalen Vorschriften erzwingen.|
|Zum Abrufen von Client-Anforderungsdaten auf einem lokalen Server oder Remoteserver wird UAL über WMI- oder Windows PowerShell-Schnittstellen abgefragt.|UAL ermöglicht eine einzige Ansicht der fortlaufenden Nutzungsdaten. Server- und Unternehmensadministratoren können diese Daten abrufen und zusammen mit Business Administratoren auswerten, um die Nutzung von Volumenlizenzen für Software zu optimieren.|
|Standardmäßig aktiviert.|Serveradministratoren müssen diese Funktion nicht konfigurieren oder anderweitig festlegen, damit alle wichtigen Funktionen verfügbar und funktionsfähig sind.|

## <a name="data-logged-with-ual"></a>Von der Benutzerzugriffsprotokollierung protokollierte Daten
Die folgenden benutzerspezifischen Daten werden von der Benutzerzugriffsprotokollierung protokolliert.

|Daten|BESCHREIBUNG|
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

|Daten|BESCHREIBUNG|
|--------|---------------|
|**IPAddress**|IP-Adresse eines Clientgeräts, das für den Zugriff auf eine Rolle oder einen Dienst verwendet wird.|
|**ActivityCount**|Die Anzahl der Zugriffe auf eine Rolle oder einen Dienst durch ein bestimmtes Gerät.|
|**FirstSeen**|Datum und Uhrzeit der ersten Verwendung einer IP-Adresse für den Zugriff auf eine Rolle oder einen Dienst.|
|**LastSeen**|Datum und Uhrzeit der letzten Verwendung einer IP-Adresse für den Zugriff auf eine Rolle oder einen Dienst.|
|**ProductName**|Name des Softwareprodukts (z. B. Windows), das Daten für die Benutzerzugriffsprotokollierung bereitstellt.|
|**RoleGUID**|Die von der Benutzerzugriffsprotokollierung zugewiesene oder registrierte GUID, die die Serverrolle bzw. das installierte Produkt darstellt.|
|**RoleName**|Name der Rolle, der Komponente oder des untergeordneten Produkts, die bzw. das die Daten für die Benutzerzugriffsprotokollierung bereitstellt. Hier besteht außerdem eine Verknüpfung mit %%amp;quot;ProductName%%amp;quot; und %%amp;quot;RoleGUID%%amp;quot;.|
|**TenantIdentifier**|Eindeutige GUID für den Mandantenclient einer installierten Rolle oder ggf. für ein Produkt, das die Daten der Benutzerzugriffsprotokollierung begleitet.|

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
Die Benutzer Zugriffs Protokollierung kann auf jedem Computer verwendet werden, auf dem Windows Server-Versionen nach Windows Server 2012 ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise
[Benutzerzugriffsprotokollierung](https://msdn.microsoft.com/library/windows/desktop/hh437528(v=vs.85).aspx) in MSDN.
[Verwalten der Benutzerzugriffsprotokollierung](Manage-User-Access-Logging.md)


