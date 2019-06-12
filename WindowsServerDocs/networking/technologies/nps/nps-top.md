---
title: Netzwerkrichtlinienserver (Network Policy Server, NPS)
description: Dieses Thema bietet einen Überblick über die Network Policy Server in Windows Server 2016 und Windows Server-2019, und enthält Links zu weiteren Anleitungen zum NPS.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: pashort
author: shortpatti
ms.date: 06/20/2018
ms.openlocfilehash: 515012a21ba6e90abe2c4db2150fd1feaad06677
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812368"
---
# <a name="network-policy-server-nps"></a>Netzwerkrichtlinienserver (Network Policy Server, NPS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, WindowsServer 2019

In diesem Thema können einen Überblick über die Network Policy Server in Windows Server 2016 und Windows Server-2019. NPS ist installiert, bei der Installation von dem die Netzwerkrichtlinien- und Zugriffsdienste (NPAS)-Feature in Windows Server 2016 und Server 2019.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende NPS-Dokumentation verfügbar.
> - [Network Policy Server-Best Practices](nps-best-practices.md)
> - [Erste Schritte mit der Netzwerkrichtlinienserver](nps-getstart-top.md)
> - [Planen des Netzwerkrichtlinienservers](nps-plan-top.md)
> - [Bereitstellen des Netzwerkrichtlinienservers](nps-deploy.md)
> - [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md)
> - [Network Policy Server (NPS)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für WindowsServer 2016 und Windows 10
> - [Network Policy Server (NPS)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2012 R2 und Windows 8.1
> - [NPS-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für WindowsServer 2012 und Windows 8

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

Sie können NPS auch konfigurieren, als Proxy Remote Authentication Dial-in User Service (RADIUS) zum Weiterleiten von verbindungsanforderungen an einen Remoteserver NPS oder anderen RADIUS-Server, damit Sie für Anforderungen, die Verbindung zu laden und an die richtige Domäne zur Authentifizierung werden weitergeleitet können und die Autorisierung.

NPS können Sie zentral konfigurieren und Verwalten von Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführung mit den folgenden Features:

- **RADIUS-Server**. NPS führt zentralisierte Authentifizierung, Autorisierung und Kontoführung für drahtlose, authentifizierenden Switches, DFÜ-RAS und Verbindungen virtuelles privates Netzwerk (VPN). Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerkzugriffsserver, z. B. drahtlose Zugriffspunkte und VPN-Server, als RADIUS-Clients in NPS. Sie können auch Netzwerkrichtlinien konfigurieren, mit denen NPS Verbindungsanforderungen autorisiert, und Sie können die RADIUS-Kontoführung so konfigurieren, dass NPS Kontoführungsinformationen in Protokolldateien auf der lokalen Festplatte oder in einer Microsoft SQL Server-Datenbank protokolliert. Weitere Informationen finden Sie unter [RADIUS-Server](#radius-server).
- **RADIUS-Proxy**. Wenn Sie NPS als RADIUS-Proxy verwenden, konfigurieren Sie Verbindungsanforderungsrichtlinien, die den NPS mitteilen, welche verbindungsanforderungen an das Weiterleiten an andere RADIUS-Server und an welche RADIUS-Server, die verbindungsanforderungen weitergeleitet werden sollen. Sie können NPS auch so konfigurieren, dass Kontoführungsdaten weitergeleitet und von einem oder mehreren Computern in einer RADIUS-Remoteservergruppe protokolliert werden. Zum Konfigurieren von NPS als RADIUS-Proxy-Server finden Sie unter den folgenden Themen. Weitere Informationen finden Sie unter [RADIUS-Proxy](#radius-proxy).
    - [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)
- **RADIUS-Kontoführung**. Sie können NPS, um Ereignisse zu protokollieren, in einer lokalen Protokolldatei oder eine lokale oder remote-Instanz von Microsoft SQL Server konfigurieren. Weitere Informationen finden Sie unter [NPS-Protokollierung](#nps-logging).

> [!IMPORTANT]
> Netzwerkzugriffsschutz \(NAP\), der Integritätsregistrierungsstelle \(HRA\), und der Host Credential Authorization-Protokoll \(HCAP\) wurden in Windows Server 2012 R2 als veraltet markiert und in Windows Server 2016 nicht verfügbar sind. Wenn Sie eine NAP-Bereitstellung mit Betriebssystemen vor Windows Server 2016 verfügen, können nicht Sie NAP-Bereitstellung auf Windows Server 2016 migrieren.

Sie können NPS mit einer beliebigen Kombination dieser Features konfigurieren. Beispielsweise können Sie einen Netzwerkrichtlinienserver als RADIUS-Server für VPN-Verbindungen und auch als RADIUS-Proxy zum Weiterleiten von einigen verbindungsanforderungen an Mitglieder einer remote-RADIUS-Servergruppe für die Authentifizierung und Autorisierung in einer anderen Domäne konfigurieren.

## <a name="windows-server-editions-and-nps"></a>Windows Server-Editionen und NPS

NPS enthält andere Funktionalität abhängig von der Edition von Windows Server, die Sie installieren.

### <a name="windows-server-2016-or-windows-server-2019-standarddatacenter-edition"></a>WindowsServer 2016 oder Windows Server 2019 Standard/Datacenter Edition

Mit der NPS in Windows Server 2016 Standard oder Datacenter können Sie eine unbegrenzte Anzahl von RADIUS-Clients und RADIUS-Remoteservergruppen konfigurieren. Außerdem können Sie RADIUS-Clients konfigurieren, indem Sie einen IP-Adressbereich angeben.

> [!NOTE]
> Die WIndows-Netzwerkrichtlinien- und Zugriffsdienste-Funktion ist nicht verfügbar, auf Systemen, die mit einer Server Core-Installationsoption installiert.

Die folgenden Abschnitte enthalten ausführliche Informationen zu NPS als RADIUS-Server und -Proxy.

## <a name="radius-server-and-proxy"></a>RADIUS-Server und -proxy

Sie können NPS als RADIUS-Server, RADIUS-Proxy oder beides verwenden.

### <a name="radius-server"></a>RADIUS-Server

NPS ist die Microsoft-Implementierung eines RADIUS-Standards, die von der Internet Engineering Task Force angegeben \(IETF\) in den RFCs 2865 und 2866. NPS als RADIUS-Server, führt die zentralisierte Verbindungsauthentifizierung, Autorisierung und Kontoführung für viele Arten von Netzwerkzugriffen, einschließlich von Drahtlosverbindungen, authentifizierenden Switches, Einwähl- und virtuelles privates Netzwerk \(VPN\) remote Zugriff und Router-zu-Router-Verbindungen.

> [!NOTE]
> Informationen zum Bereitstellen von NPS als RADIUS-Server finden Sie unter [Netzwerkrichtlinienserver bereitstellen](nps-deploy.md).

NPS ermöglicht die Verwendung von eine heterogene Gruppe von Drahtlos, Switch, Remotezugriff oder VPN-Geräten. Sie können NPS mit dem RAS-Dienst verwenden, die in Windows Server 2016 verfügbar ist.

NPS verwendet eine Active Directory-Domänendienste \(AD DS\) Domänen- oder der lokalen Sicherheitskontenverwaltung (Security Accounts Manager, SAM) Benutzerkonten-Datenbank verwendet, um die Benutzeranmeldeinformationen für die versucht, eine Verbindung zu authentifizieren. Wenn ein Server mit NPS ein Mitglied einer AD DS-Domäne ist, wird NPS den Verzeichnisdienst als Benutzerkontendatenbank verwendet und ist Teil einer Lösung für einmaliges Anmelden. Der gleiche Satz von Anmeldeinformationen wird verwendet, für die Netzwerk-Zugriffssteuerung \(authentifizieren und Autorisieren von Zugriff auf ein Netzwerk\) und melden Sie sich bei einer AD DS-Domäne.

> [!NOTE]
> NPS verwendet die Einwähleigenschaften des Benutzerkontos und Netzwerkrichtlinien, um eine Verbindung zu autorisieren.

Internetdienstanbieter \(ISPs\) und Organisationen, die den Zugriff auf das Netzwerk verwalten können, zunehmend vor der Herausforderung der Verwaltung von allen Arten von Netzwerkzugriffen von einem einzelnen Punkt der Verwaltung auf, unabhängig von der Art des Netzwerkzugriffs Geräte, die verwendet werden. Der RADIUS-Standard unterstützt diese Funktion in homogene und heterogene Umgebungen. RADIUS ist ein Client / Server-Protokoll, die Geräte für den Netzwerkzugriff (als RADIUS-Clients verwendete) ermöglicht, um Authentifizierung und kontoführungsanforderungen an einen RADIUS-Server zu senden.

RADIUS-Server verfügt über Zugriff auf die Benutzerkontoinformationen und kann die Netzwerk-Anmeldeinformationen für Authentifizierung überprüfen. Wenn Anmeldeinformationen des Benutzers authentifiziert werden, und der Verbindungsversuch ist autorisiert, der RADIUS-Server autorisiert den Benutzerzugriff auf Grundlage der angegebenen Bedingungen und protokolliert dann die Netzwerk-Access-Verbindung in einem Kontoführungsprotokoll. Die Verwendung von RADIUS ermöglicht dem Benutzer für die Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführungsdaten weitergeleitet und erfasst und verwaltet und auf jedem Zugriffsserver, nicht an einem zentralen Ort.

#### <a name="using-nps-as-a-radius-server"></a>Verwenden NPS als RADIUS-server

Sie können NPS als RADIUS-Server beim:

- Sie sind einer AD DS-Domäne oder der lokalen SAM-Benutzerkontendatenbank als Benutzerkontendatenbank für Zugriffsclients verwenden. 
- Verwenden Sie den Remotezugriff auf mehreren Einwählservern, VPN-Server, oder Router für Wählen bei Bedarf und sowohl die Konfiguration von Richtlinien und die Verbindungszeichenfolge, die Protokollierung und Kontoführung zentralisieren möchten. 
- Sie werden Ihre DFÜ, VPN oder drahtlosen Zugriff an einen Service Provider outsourcing. Die Zugriffsserver verwenden RADIUS zum Authentifizieren und Autorisieren von Verbindungen, die von einem Mitglied Ihrer Organisation vorgenommen werden.
- Möchten Sie die Authentifizierung, Autorisierung und Kontoführung für eine heterogene Gruppe von Zugriffsservern zentralisieren.

Die folgende Abbildung zeigt die NPS als RADIUS-Server für eine Vielzahl von Zugriffsclients. 

![NPS als RADIUS-Server](../../media/Nps-Server/Nps-Server.jpg)

### <a name="radius-proxy"></a>RADIUS-Proxy

Als RADIUS-Proxy leitet die NPS-Authentifizierung und Kontoführungsnachrichten an NPS- und andere RADIUS-Server ein. Können Sie NPS als RADIUS-Proxy auf das Routing von RADIUS-zwischen RADIUS-Clients Nachrichten \(Netzwerkzugriffsserver so genannte\) und RADIUS-Servern, die Benutzerauthentifizierung, Autorisierung und Kontoführung für Ausführen der Verbindungsversuch. 

Bei Verwendung als RADIUS-Proxy ist NPS als zentraler Switch- bzw. Routingpunkt, über den RADIUS-Zugriffs- und Kontoführungsnachrichten weitergeleitet. NPS in einem Kontoführungsprotokoll zeichnet Informationen zu den Nachrichten, die weitergeleitet werden.

#### <a name="using-nps-as-a-radius-proxy"></a>Verwenden NPS als RADIUS-proxy

Sie können NPS als RADIUS-Proxy bei:

- Sie können ein Dienstanbieter, der externes DFÜ-, VPN- oder drahtlosen Netzwerkzugriffen für mehrere Kunden bietet. Ihre Netzwerkzugriffsserver senden verbindungsanforderungen an den NPS RADIUS-Proxy. Basierend auf der Realm-Abschnitt des Benutzernamens in der verbindungsanforderung, kann der NPS RADIUS-Proxy leitet die verbindungsanforderung an einen RADIUS-Server, der vom Kunden verwaltet wird und authentifizieren und den Verbindungsversuch zu autorisieren.
- Sie möchten Authentifizierung und Autorisierung für Benutzerkonten, die nicht Mitglieder der Domäne, in der der NPS ein Element ist, oder eine andere Domäne, die über eine bidirektionale Vertrauensstellung mit der Domäne verfügt, in dem der NPS Mitglied ist. Dazu gehören Konten, in anderen Gesamtstrukturen, Domänen mit unidirektionaler Vertrauensstellung und nicht vertrauenswürdigen Domänen. Anstatt Ihre Access-Server zum Senden von eigenen verbindungsanforderungen an einen NPS RADIUS-Server zu konfigurieren, können Sie sie zum Senden von eigenen verbindungsanforderungen an einen NPS RADIUS-Proxy konfigurieren. Der NPS RADIUS-Proxy des Teil mit dem Bereich des Benutzernamens verwendet, und leitet die Anforderung an einen NPS in der richtigen Domäne oder Gesamtstruktur. Verbindungsversuche für Benutzer, die Konten in einer Domäne oder Gesamtstruktur für NAS-Servern in einer anderen Domäne oder Gesamtstruktur authentifiziert werden können.
- Authentifizierung und Autorisierung über eine Datenbank, die keinem Windows-Datenbank durchführen möchten. Verbindungsanforderungen, die mit einem angegebenen Bereich übereinstimmen werden in diesem Fall ein RADIUS-Server weitergeleitet, die Zugriff auf eine andere Datenbank von Benutzerkonten und Autorisierungsdaten hat. Beispiele für andere Benutzerdatenbanken sind (Novell Directory Services, NDS) und (SQL = Structured Query Language)-Datenbanken.
- Möchten Sie eine große Anzahl von verbindungsanforderungen zu verarbeiten. In diesem Fall können anstatt zu konfigurieren, Ihre RADIUS-Clients, um zu versuchen, die Verbindungs- und kontoführungsanforderungen gleichmäßig auf mehrere RADIUS-Server zu verteilen, Sie werden zum Senden ihre Verbindungs- und kontoführungsanforderungen an einen NPS RADIUS-Proxy konfigurieren. Der NPS RADIUS-Proxy dynamisch verteilt die Last der Verbindung und Kontoführung, Anfragen über mehrere RADIUS-Server und erhöht die Verarbeitung einer großen Anzahl von RADIUS-Clients und Authentifizierungen pro Sekunde.
- Sie möchten RADIUS-Authentifizierung und-Autorisierung für Provider ausgelagerter Dienste bereitstellen, und Minimieren der Intranet-Firewall-Konfiguration. Eine Intranetfirewall liegt zwischen dem Umkreisnetzwerk (das Netzwerk zwischen Ihrem Intranet und Internet) und dem Intranet. Durch eine NPS auf Ihrem Umkreisnetzwerk platzieren, muss die Firewall zwischen dem Umkreisnetzwerk und Intranet-Datenverkehr zwischen den NPS- und mehreren Domänencontrollern ermöglichen. Ersetzen Sie den NPS mit einem NPS-Proxy, muss die Firewall nur RADIUS-Datenverkehr zwischen dem NPS-Proxy und eine oder mehrere NPSs in Ihrem Intranet zulassen.

Die folgende Abbildung zeigt die NPS als RADIUS-Proxy zwischen RADIUS-Clients und RADIUS-Servern.

![NPS als RADIUS-Proxy](../../media/Nps-Proxy/Nps-Proxy.jpg)

Mit NPS können Organisationen auch RAS-Infrastruktur zu einem Dienstanbieter auslagern, und behalten die Kontrolle über die Benutzerauthentifizierung, Autorisierung und Kontoführung.

NPS-Konfigurationen können für die folgenden Szenarien erstellt werden:

- Drahtloser Zugriff
- Remotezugriff für Unternehmen-DFÜ-Verbindung oder virtuelle private Netzwerk (VPN)
- Ausgelagerter drahtloser oder Einwählzugriff
- Internetzugriff
- Authentifizierter Zugriff auf extranet-Ressourcen für Geschäftspartner

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>RADIUS-Server und Beispiele für RADIUS-proxy

Die folgende Konfigurationsbeispiele veranschaulichen, wie Sie NPS als RADIUS-Server und RADIUS-Proxy konfigurieren können.

**NPS als RADIUS-Server**. In diesem Beispiel NPS als RADIUS-Server konfiguriert ist, die Standard-Verbindungsanforderungsrichtlinie ist die einzige konfigurierte Richtlinie und alle verbindungsanforderungen werden von den lokalen NPS verarbeitet. Der NPS kann authentifizieren und Autorisieren von Benutzern, deren Konten in der Domäne des NPS und in vertrauenswürdigen Domänen befinden.

**NPS als RADIUS-Proxy**. In diesem Beispiel wird die NPS als RADIUS-Proxy konfiguriert, die Weiterleitung von verbindungsanforderungen an remote-RADIUS-Servergruppen in nicht vertrauenswürdigen Domänen weiterleitet. Die Standard-Verbindungsanforderungsrichtlinie wird gelöscht, und zwei neue Verbindungsanforderungsrichtlinien zum Weiterleiten von Anforderungen an jeden der zwei nicht vertrauenswürdigen Domänen erstellt werden. In diesem Beispiel verarbeitet NPS keine Verbindungsanfragen auf dem lokalen Server. 

**NPS als RADIUS-Server und RADIUS-Proxy**. Zusätzlich zu der Standard-Verbindungsanforderungsrichtlinie, der gibt an, dass die Weiterleitung von verbindungsanforderungen lokal verarbeitet werden, wird eine neue Verbindungsanforderungsrichtlinie erstellt, die Weiterleitung von verbindungsanforderungen an ein NPS oder anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. Diese zweite Richtlinie heißt die Proxy-Richtlinie. In diesem Beispiel wird die Proxy-Richtlinie in der sortierten Liste der Richtlinien zuerst angezeigt. Wenn die verbindungsanforderung die Proxy-Richtlinie übereinstimmt, wird die verbindungsanforderung an den Radius-Server in der remote-RADIUS-Servergruppe weitergeleitet. Wenn die verbindungsanforderung der Proxyrichtlinie stimmt nicht überein, aber es die Standard-Verbindungsanforderungsrichtlinie entspricht, verarbeitet der NPS die verbindungsanforderung auf dem lokalen Server. Wenn die verbindungsanforderung nicht mit beiden Richtlinien übereinstimmt, wird sie verworfen.

**NPS als RADIUS-Server mit Remoteservern Buchhaltung**. In diesem Beispiel den lokalen NPS ist nicht für die Kontoführung konfiguriert, und die Standard-Verbindungsanforderungsrichtlinie wird so überarbeitet, dass eine NPS oder anderen RADIUS-Server in einer remote-RADIUS-Servergruppe RADIUS-Kontoführungsnachrichten weitergeleitet werden. Obwohl Kontoführungsnachrichten weitergeleitet werden, Authentifizierung und Autorisierung Nachrichten werden nicht weitergeleitet, und den lokalen NPS führt diese Funktionen für die lokale Domäne, und alle vertrauenswürdigen Domänen.

**NPS mit remote-RADIUS-Windows-benutzerzuordnung**. In diesem Beispiel fungiert NPS als ein RADIUS-Server und RADIUS-Proxy für jede einzelne verbindungsanforderung durch Weiterleiten der Authentifizierungsanforderung an einen RADIUS-Remoteserver bei der Verwendung von eines lokalen Windows-Benutzerkontos für die Autorisierung an. Diese Konfiguration wird durch Konfigurieren der Remote-RADIUS-Attribut Windows Benutzerzuordnung als Bedingung für die Verbindungsanforderungsrichtlinie implementiert. \(Darüber hinaus muss ein Benutzerkonto lokal auf dem RADIUS-Server erstellt werden, die den gleichen Namen wie das Remotebenutzerkonto verfügt für die Authentifizierung vom RADIUS-Remoteserver ausgeführt wird.\)

## <a name="configuration"></a>Konfiguration

Zum Konfigurieren von NPS als RADIUS-Server können Sie in der NPS-Konsole oder im Server-Manager entweder standard oder erweiterte Konfiguration verwenden. Um NPS als RADIUS-Proxy konfigurieren zu können, müssen Sie die erweiterten Konfiguration verwenden.

### <a name="standard-configuration"></a>Standardkonfiguration

Mit der Standardkonfiguration werden Assistenten bereitgestellt, können Sie das Konfigurieren von NPS für die folgenden Szenarien:

- RADIUS-Server für DFÜ- oder VPN-Verbindungen
- RADIUS-Server für drahtlose oder verkabelte 802.1X-Verbindungen

Zum Konfigurieren von NPS mithilfe eines Assistenten öffnen Sie die NPS-Konsole, wählen Sie einen der vorangehenden Szenarios, und klicken Sie dann auf den Link, der der Assistent wird geöffnet.

### <a name="advanced-configuration"></a>Erweiterte Konfiguration

Wenn Sie erweiterten Konfiguration verwenden, konfigurieren Sie NPS als RADIUS-Server oder RADIUS-Proxy manuell. 

Klicken Sie zum Konfigurieren von NPS mithilfe von erweiterten Konfiguration die NPS-Konsole öffnen, und klicken Sie dann auf den Pfeil neben **erweiterte Konfiguration** auf diesen Abschnitt zu erweitern.

Die folgenden erweiterten Konfigurationselemente werden bereitgestellt.

#### <a name="configure-radius-server"></a>Konfigurieren Sie RADIUS-server

Zum Konfigurieren von NPS als RADIUS-Server müssen Sie die RADIUS-Clients, die Netzwerkrichtlinien- und RADIUS-Kontoführung konfigurieren.

Anweisungen dazu, wie diese Konfigurationen finden Sie unter den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von Netzwerkrichtlinien](nps-np-configure.md)
- [Network Policy Server Kontoführung konfigurieren](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>Konfigurieren Sie RADIUS-proxy

Um NPS als RADIUS-Proxy konfigurieren zu können, müssen Sie die RADIUS-Clients, RADIUS-Remoteservergruppen und Verbindungsanforderungsrichtlinien konfigurieren.

Anweisungen dazu, wie diese Konfigurationen finden Sie unter den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von Remote-RADIUS-Servergruppen](nps-crp-rrsg-configure.md)
- [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)

## <a name="nps-logging"></a>NPS-Protokollierung

Protokollierung von NPS wird RADIUS-Kontoführung auch aufgerufen werden. Konfigurieren Sie die NPS-Protokollierung an Ihre Anforderungen an, ob NPS als RADIUS-Server, Proxy oder eine beliebige Kombination aus diesen Konfigurationen verwendet wird.

Zum Konfigurieren der NPS-Protokollierung müssen Sie konfigurieren, welche Ereignisse protokolliert und mit der Ereignisanzeige angezeigt werden soll, und dann bestimmen, welche anderen Informationen, die Sie protokollieren möchten. Darüber hinaus müssen Sie entscheiden, ob Sie die Benutzerauthentifizierung und Informationen zur Kontoführung Textprotokolldateien, die auf dem lokalen Computer gespeichert oder in eine SQL Server-Datenbank auf entweder dem lokalen Computer oder einem Remotecomputer anmelden möchten.

Weitere Informationen finden Sie unter [konfigurieren Network Policy Server Accounting](nps-accounting-configure.md).
