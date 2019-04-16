---
title: Der Netzwerkrichtlinienserver (NPS)
description: Dieses Thema enthält eine Übersicht des Netzwerkrichtlinienservers in Windows Server2016 und enthält Links zu weiteren Anleitungen zum NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f48cbdaec82e9e60f734a4a8949082187b13166
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-nps"></a>Der Netzwerkrichtlinienserver (NPS)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können eine Übersicht über Netzwerkrichtlinienserver in Windows Server2016.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende NPS-Dokumentation verfügbar.
> - [Bewährte Methoden: Netzwerk](nps-best-practices.md)
> - [Erste Schrittemit dem Netzwerkrichtlinienserver](nps-getstart-top.md)
> - [Planen eines Netzwerkrichtlinienservers](nps-plan-top.md)
> - [Bereitstellen eines Netzwerkrichtlinienservers](nps-deploy.md)
> - [Verwalten eines Netzwerkrichtlinienservers](nps-manage-top.md)
> - [Network Policy Server (NPS)-Cmdlets](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2016 und Windows10
> - [Network Policy Server (NPS)-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server2012 R2 und Windows8.1
> - [NPS-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2012 und Windows8

Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie zum Erstellen und erzwingen für die gesamte Organisation Netzwerkzugriffsrichtlinien für die Anforderung Verbindungsauthentifizierung und Autorisierung.

Sie können NPS auch konfigurieren, als Proxy Remote Authentication Dial-in User Service (RADIUS) Verbindungsanforderungen an einen Remoteserver NPS oder anderen RADIUS-Server weitergeleitet, damit Sie für Verbindungsanforderungen zu laden und diese an der richtigen Domäne für die Authentifizierung und Autorisierung weiterleiten können.

Sie können zentral konfigurieren und Verwalten von Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführung mit den folgenden Features:

- **RADIUS-Server**. NPS führt die zentralisierte Authentifizierung, Autorisierung und Kontoführung für drahtlose, Authentifizierung, Remotezugriff-DFÜ-Netzwerk und virtuelles privates Netzwerk (VPN). Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerkzugriffsserver, z.B. drahtlose Zugriffspunkte und VPN-Server als RADIUS-Clients in NPS. Sie auch Netzwerkrichtlinien konfigurieren, die NPS verwendet, um Verbindungsanforderungen zu autorisieren, und Sie können die RADIUS-Kontoführung konfigurieren, sodass NPS Kontoführungsinformationen in Protokolldateien auf der lokalen Festplatte oder in einer Microsoft SQL Server-Datenbank protokolliert. Weitere Informationen finden Sie unter [RADIUS-Server](#bkmk_server).
- **RADIUS-Proxy**. Wenn Sie NPS als RADIUS-Proxy verwenden, konfigurieren Sie Verbindungsanforderungsrichtlinien, die dem Netzwerkrichtlinienserver mitgeteilt, welche Verbindungsanforderungen weitergeleitet zu anderen RADIUS-Servern und an welche RADIUS-Server Verbindungsanforderungen weitergeleitet werden sollen. Sie können NPS auch konfigurieren, um Kontoführungsdaten weitergeleitet und von einem oder mehreren Computern in einer RADIUS-Remoteservergruppe protokolliert werden. Wenn Sie NPS als RADIUS-Proxy-Server konfigurieren, finden Sie unter den folgenden Themen. Weitere Informationen finden Sie unter [RADIUS-Proxy](#bkmk_proxy).
    - [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)
- **RADIUS-Kontoführung**. Sie können NPS Protokollieren von Ereignissen in einer lokalen Protokolldatei oder einer lokalen oder Remotecomputer Instanz von Microsoft SQL Server konfigurieren. Weitere Informationen finden Sie unter [NPS-Protokollierung](#bkmk_logging).

>[!IMPORTANT]
>Network Access Protection \(NAP\), der Integritätsregistrierungsstelle \(HRA\) und Host Credential Authorization-Protokoll \(HCAP\) wurden in Windows Server2012 R2 veraltet und sind in Windows Server2016 nicht verfügbar. Wenn Sie eine NAP-Bereitstellung mit Betriebssystemen vor Windows Server2016 haben, kann nicht NAP-Bereitstellung zu Windows Server2016 migriert werden.

Sie können NPS mit einer beliebigen Kombination dieser Features konfigurieren. Beispielsweise können Sie einen Netzwerkrichtlinienserver als RADIUS-Server für VPN-Verbindungen und auch als RADIUS-Proxy einige Verbindungsanforderungen weitergeleitet, auf Mitglieder einer RADIUS-Remoteservergruppe für die Authentifizierung und Autorisierung in einer anderen Domäne konfigurieren.

## <a name="windows-server-editions-and-nps"></a>Windows Server-Editionen und NPS

NPS enthält verschiedene Funktionen abhängig von der Edition von Windows Server, die Sie installieren.

### <a name="windows-server-2016-datacenter-edition"></a>Windows Server2016 Datacenter Edition

Mit NPS in Windows Server2016 Datacenter können Sie eine unbegrenzte Anzahl von RADIUS-Clients und RADIUS-Remoteservergruppen konfigurieren. Darüber hinaus können Sie RADIUS-Clients konfigurieren, indem Sie einen IP-Adressbereich angeben.

### <a name="windows-server-2016-standard-edition"></a>Windows Server2016 Standard Edition

Mit NPS in Windows Server2016 Standard können Sie maximal 50 RADIUS-Clients und maximal 2 RADIUS-Remoteservergruppen konfigurieren. Sie können einen RADIUS-Client mit einem vollständig qualifizierten Domänennamen oder eine IP-Adresse definieren, aber Sie können keine Gruppen von RADIUS-Clients durch Angabe eines IP-Adressbereichs definieren. Wenn Sie der vollständig qualifizierten Domänennamen eines RADIUS-Clients in mehrere IP-Adressen aufgelöst wird, verwendet der NPS-Server die erste IP-Adresse, die in der Abfrage Domain Name System (DNS) zurückgegeben.

Die folgenden Abschnitte enthalten ausführlichere Informationen zu NPS als RADIUS-Server und Proxy.

## <a name="radius-server-and-proxy"></a>RADIUS-Server und proxy

Sie können NPS als RADIUS-Server, RADIUS-Proxy oder beides verwenden.

### <a name="bkmk_server"></a>RADIUS-Server

NPS ist die Microsoft-Implementierung von RADIUS-Standards von der Internet Engineering Task Force \(IETF\) in RFC 2865 und 2866 angegeben. Als RADIUS-Server führt NPS die zentralisierte Verbindungsauthentifizierung, Autorisierung und Kontoführung für viele Arten des Netzwerkzugriffs, einschließlich drahtlos, Switch, DFÜ-Authentifizierung, virtuelles privates Netzwerk \(VPN\) Remotezugriff und Router-zu-Router-Verbindungen.

>[!NOTE]
>Informationen zum Bereitstellen von NPS als RADIUS-Server finden Sie unter [Netzwerkrichtlinienserver bereitstellen](nps-deploy.md).

NPS ermöglicht die Verwendung von einem heterogenen Satzes von Drahtlos-, Switch, RAS- oder VPN-Geräten. Sie können NPS mit dem RAS-Dienst in Windows Server2016 verfügbar ist.

NPS mithilfe einer Active Directory-Domänendienste-Domäne \(AD DS\) oder die lokalen Sicherheitskontenverwaltung (Security Accounts Manager, SAM) Benutzerkontendatenbank zum Authentifizieren der Benutzeranmeldeinformationen für die Verbindung versucht. Wenn Sie ein Server mit NPS ein Mitglied einer AD DS-Domäne ist, wird NPS verwendet den Verzeichnisdienst als seine Datenbank für Benutzerkonten und ist Teil einer Lösung für einmaliges Anmelden. Der gleiche Satz von Anmeldeinformationen wird verwendet, für die Netzwerkzugriffsteuerung \ (Authentifizierung und Autorisierung des Zugriffs auf eine vom Netzwerk) und melden Sie sich bei einer AD DS-Domäne.

>[!NOTE]
>NPS verwendet die DFÜ-Eigenschaften des Benutzerkontos und Netzwerkrichtlinien, um eine Verbindung zu autorisieren.

Haben zunehmend vor der Herausforderung Verwalten von allen Arten von Netzwerkzugriff über eine zentrale Verwaltung, unabhängig von der Art der verwendeten Netzwerkzugriffsgeräte Internet Service Provider \(ISPs\) und Organisationen, die Zugriff auf das Netzwerk zu verwalten. Der RADIUS-Standard unterstützt diese Funktion in einer einheitlichen und gemischten Umgebung. RADIUS ist ein Client / Server-Protokoll, die Geräte für den Netzwerkzugriff (als RADIUS-Clients verwendet) ermöglicht, um Authentifizierung und kontoführungsanforderungen an einen RADIUS-Server zu senden.

RADIUS-Server hat Zugriff auf Informationen zum Benutzerkonto und Authentifizierungsinformationen Netzwerk überprüfen kann. Wenn Anmeldeinformationen authentifiziert werden und der Verbindungsversuch autorisiert ist, der RADIUS-Server autorisiert Benutzerzugriff auf der Grundlage der angegebenen Bedingungen und die Netzwerkschnittstelle für den Zugriff in einem Kontoführungsprotokoll protokolliert. Die Verwendung von RADIUS ermöglicht dem Benutzer für die Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführungsdaten weitergeleitet und gesammelt und an einem zentralen Ort, anstatt auf jedem Server gewartet werden.

#### <a name="using-nps-as-a-radius-server"></a>Mit dem Netzwerkrichtlinienserver als RADIUS-Server

Sie können NPS als RADIUS-Server bei:

- Sie verwenden AD DS-Domäne oder der lokalen SAM-Benutzerkontendatenbank als Benutzerkontendatenbank für RAS-Clients. 
- Verwenden Sie Remotezugriff auf mehrere DFÜ-Server, VPN-Server, oder bei Bedarf Router und sowohl die Konfiguration von Netzwerkrichtlinien und Verbindung Protokollierung und Kontoführung zentralisieren möchten. 
- Sie werden Ihre DFÜ, VPN oder drahtlosen Zugriff auf einen Dienstanbieter outsourcing. Die Access-Server verwenden RADIUS zur Authentifizierung und Autorisierung von Verbindungen, die von Mitgliedern Ihrer Organisation vorgenommen werden.
- Sie möchten die Authentifizierung, Autorisierung und Kontoführung für eine heterogene Gruppe von Server zu zentralisieren.

Die folgende Abbildungzeigt NPS als RADIUS-Server für eine Vielzahl von RAS-Clients. 

![NPS als RADIUS-Server](../../media/Nps-Server/Nps-Server.jpg)

### <a name="bkmk_proxy"></a>RADIUS-proxy

Als RADIUS-Proxy leitet NPS-Authentifizierung und -Kontoführung Nachrichten an NPS und andere RADIUS-Server weiter. Sie können NPS als RADIUS-Proxy für das Routing von RADIUS-zwischen RADIUS-Clients Nachrichten \ (auch als "Network Access Server\" bezeichnet) und RADIUS-Servern, die Benutzerauthentifizierung, Autorisierung und Kontoführung für die Verbindung ausführen. 

Als RADIUS-Proxy verwendet, ist NPS an einem zentralen wechseln oder Routing Point über den RADIUS-Zugriff und Kontoführung weitergeleitet. NPS in einem Kontoführungsprotokoll zeichnet Informationen zu den Nachrichten, die weitergeleitet werden.

#### <a name="using-nps-as-a-radius-proxy"></a>Mit dem Netzwerkrichtlinienserver als RADIUS-proxy

Sie können NPS als RADIUS-Proxy verwenden bei:

- Sie können ein externes DFÜ, VPN oder Drahtlosnetzwerk-Dienste für mehrere Kunden bietet Dienstanbieter. Ihre Netzwerkzugriffsserver senden Verbindungsanforderungen an den NPS-RADIUS-Proxy. Basierend auf den Bereich Teil des Benutzernamens in der Anfrage, kann NPS RADIUS-Proxy leitet die Anforderung der Verbindung an einen RADIUS-Server, der vom Kunden verwaltet wird und authentifizieren und autorisieren den Verbindungsversuch.
- Sie möchten die Authentifizierung und Autorisierung für Benutzerkonten, die nicht Mitglieder der Domäne, in der der NPS-Server angehört, oder einer anderen Domäne, die über eine bidirektionale Vertrauensstellung mit der Domäne verfügt, in dem der NPS-Server angehört. Dazu zählen Konten in nicht vertrauenswürdigen Domänen, unidirektionale vertrauenswürdigen Domänen und anderen Gesamtstrukturen. Anstatt Ihre Access Server so konfigurieren, ihre Verbindungsanforderungen an einen NPS RADIUS-Server senden, können Sie sie zum Senden von Verbindungsanfragen an einen NPS RADIUS-Proxy konfigurieren. Der NPS RADIUS-Proxy verwendet der Bereich Teil des Benutzernamens und leitet die Anforderung an einen NPS-Server in der richtigen Domäne oder Gesamtstruktur. Verbindungsversuche für Benutzer, die Konten in einer Domäne oder Gesamtstruktur für Netzwerkzugriffsserver in einer anderen Domäne oder Gesamtstruktur authentifiziert werden können.
- Authentifizierung und Autorisierung mithilfe einer Datenbank, die keine Windows-Konto-Datenbank ist durchführen möchten. In diesem Fall sind Verbindungsanforderungen, die einen angegebenen Bereichsnamen entsprechen an einen RADIUS-Server weitergeleitet, die Zugriff auf eine andere Datenbank mit Benutzerkonten und Autorisierungsdaten hat. Beispiele für andere Benutzerdatenbanken sind Datenbanken (Novell Directory Services, NDS) und Structured Query Language (SQL).
- Sie möchten eine große Anzahl von Verbindungsanforderungen zu verarbeiten. In diesem Fall können anstatt Ihre RADIUS-Clients so konfigurieren, versuchen Sie, ihre Verbindung und die Kontoführung auf mehrere RADIUS-Server zu verteilen, Sie sie zum Senden von ihrer Verbindung und kontoführungsanforderungen an einen NPS RADIUS-Proxy konfigurieren. Der NPS RADIUS-Proxy dynamisch verteilt die Last der Verbindung und Kontoführung auf mehrere RADIUS-Server angefordert und erhöht die Verarbeitung einer großen Anzahl von RADIUS-Clients und -Authentifizierungen pro Sekunde.
- Konfiguration des Intranetfirewalls zum Minimieren und RADIUS-Authentifizierung und Autorisierung für externe Dienstanbieter bereitstellen möchten. Eine Intranetfirewall ist zwischen dem Umkreisnetzwerk (das Netzwerk zwischen dem Intranet und Internet) und dem Intranet. Platzieren Sie einen NPS-Server im Umkreisnetzwerk, muss die Firewall zwischen dem Umkreisnetzwerk und dem Intranet Datenverkehr zwischen dem NPS-Server und mehreren Domänencontrollern zulassen. Durch Ersetzen des NPS-Servers mit NPS-Proxy, muss die Firewall nur RADIUS-Datenverkehr zwischen dem NPS-Proxy und einen oder mehrere NPS-Server in Ihrem Intranet zulassen.

Die folgende Abbildungzeigt NPS als RADIUS-Proxy zwischen RADIUS-Clients und RADIUS-Server.

![NPS als RADIUS-Proxy](../../media/Nps-Proxy/Nps-Proxy.jpg)


Mit NPS können Organisationen außerdem RAS-Infrastruktur an einen Dienstanbieter auslagern, und behalten die Kontrolle über die Benutzerauthentifizierung, Autorisierung und Kontoführung.

NPS-Konfigurationen können für die folgenden Szenarien erstellt werden:

- Drahtlosen Zugriff
- Remotezugriff der Organisation DFÜ- oder virtuelles privates Netzwerk (VPN)
- Externes DFÜ-Verbindung oder drahtlosen Zugriff
- Zugriff auf das Internet
- Authentifizierten Zugriff auf Extranet-Ressourcen für Geschäftspartner

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>RADIUS-Server und RADIUS-Proxy Configuration Beispiele

Die folgende Konfigurationsbeispiele veranschaulichen, wie Sie NPS als RADIUS-Server und RADIUS-Proxy konfigurieren können.

**NPS als RADIUS-Server**. In diesem Beispiel NPS als RADIUS-Server konfiguriert ist, die standardmäßige Verbindungsanforderungsrichtlinie ist die einzige konfigurierte Richtlinie und alle Verbindungsanforderungen von den lokalen Netzwerkrichtlinienserver verarbeitet werden. Der NPS-Server kann authentifizieren und Autorisieren von Benutzern, deren Konten in der Domäne des Netzwerkrichtlinienservers und in vertrauenswürdigen Domänen befinden.

**NPS als RADIUS-Proxy**. In diesem Beispiel wird der NPS-Server als RADIUS-Proxy konfiguriert, der Verbindungsanforderungen an RADIUS-Remoteservergruppen in zwei nicht vertrauenswürdige Domänen weiterleitet. Die standardmäßige Verbindungsanforderungsrichtlinie wird gelöscht, und zwei neue Verbindungsanforderungsrichtlinien werden erstellt, um Anfragen an jedem der beiden nicht vertrauenswürdigen Domänen weiterleiten. In diesem Beispiel wird NPS keine Verbindungsanfragen auf dem lokalen Server verarbeitet. 

**NPS als RADIUS-Server und RADIUS-Proxy**. Zusätzlich zu den standardmäßigen Verbindungsanforderungsrichtlinie, ausweist Verbindungsanfragen lokal verarbeitet werden, wird eine neue Verbindungsanforderungsrichtlinie erstellt, die Verbindungsanforderungen an einen Netzwerkrichtlinienserver oder einen anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. Diese zweite Richtlinie heißt die Proxy-Richtlinie. In diesem Beispiel wird die Proxy-Richtlinie in der sortierte Liste der Richtlinien zuerst angezeigt. Wenn die Verbindungsanforderung die Proxy-Richtlinie übereinstimmt, wird die Verbindungsanforderung an den Radius-Server die RADIUS-Remoteservergruppe weitergeleitet. Wenn die Verbindungsanforderung nicht die Proxy-Richtlinie entspricht aber der standardmäßige Verbindungsanforderungsrichtlinie entspricht, verarbeitet NPS die Verbindungsanforderung auf dem lokalen Server. Wenn die verbindungsanforderung entweder Richtlinie nicht übereinstimmt, wird sie verworfen.

**NPS als RADIUS-Server mit Remoteservern Kontoführung**. In diesem Beispiel der lokale NPS-Server ist nicht für die Kontoführung ausführen konfiguriert, und die standardmäßige Verbindungsanforderungsrichtlinie wird überarbeitet, sodass RADIUS-Kontoführungsnachrichten an einem NPS-Server oder anderen RADIUS-Server in einer RADIUS-Remoteservergruppe weitergeleitet werden. Zwar Kontoführungsnachrichten weitergeleitet werden, Authentifizierung und Autorisierung Nachrichten nicht weitergeleitet werden, und der lokale NPS-Server führt diese Funktionen für die lokale Domäne, und alle vertrauenswürdigen Domänen.

**NPS mit RADIUS für die Zuordnung der Windows-Benutzer**. In diesem Beispiel fungiert NPS als einen RADIUS-Server und RADIUS-Proxy für jede einzelne verbindungsanforderung durch die Authentifizierungsanforderung an einen RADIUS-Remoteserver bei der Verwendung von einem lokalen Windows-Benutzerkonto für die Autorisierung weiterleiten. Diese Konfiguration wird durch die Konfiguration der Remote-RADIUS-Attribut Windows Benutzerzuordnung als Bedingung für die Verbindungsanforderungsrichtlinie implementiert. \ (Darüber hinaus ein Benutzerkonto muss erstellt werden lokal auf dem RADIUS-Server, die den gleichen Namen wie das Remotebenutzerkonto hat für die Authentifizierung vom RADIUS-Remoteserver ausgeführt wird. \)

## <a name="configuration"></a>Konfiguration

Um NPS als RADIUS-Server konfigurieren, können Sie Standardkonfiguration oder die erweiterte Konfiguration in der NPS-Konsole oder im Server-Manager verwenden. Wenn Sie um NPS als RADIUS-Proxy zu konfigurieren, müssen Sie die erweiterte Konfiguration verwenden.

### <a name="standard-configuration"></a>Standardkonfiguration

Mit der Standardkonfiguration werden Assistenten bereitgestellt, können Sie NPS für die folgenden Szenarien konfigurieren:

- RADIUS-Server für DFÜ- oder VPN-Verbindungen
- RADIUS-Server für 802.1X-Drahtlosverbindungen oder -Kabelverbindungen

Konfigurieren von NPS mithilfe eines Assistenten, die NPS-Konsole zu öffnen, wählen Sie eine der oben beschriebenen Szenarien, und klicken Sie dann auf den Link, der der Assistent wird geöffnet.

### <a name="advanced-configuration"></a>Erweiterte Konfiguration

Wenn Sie erweiterte Konfiguration verwenden, konfigurieren Sie manuell von NPS als RADIUS-Server oder RADIUS-Proxy. 

Zum Konfigurieren von NPS mithilfe der erweiterten Konfiguration, öffnen Sie die NPS-Konsole, und klicken Sie dann auf den Pfeil neben **erweiterte Konfiguration** auf diesen Abschnittzu erweitern.

Die folgenden erweiterten Konfigurationselemente werden bereitgestellt.

#### <a name="configure-radius-server"></a>Konfigurieren von RADIUS-Server

Wenn Sie NPS als RADIUS-Server konfigurieren, müssen Sie RADIUS-Clients, eine Netzwerkrichtlinie und RADIUS-Kontoführung konfigurieren.

Eine Anleitung zum Bereitstellen dieser Konfigurationen finden Sie unter den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von Netzwerkrichtlinien](nps-np-configure.md)
- [Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver Netzwerk](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>Konfigurieren von RADIUS-proxy

Wenn Sie um NPS als RADIUS-Proxy zu konfigurieren, müssen Sie RADIUS-Clients, RADIUS-Remoteservergruppen und Verbindungsanforderungsrichtlinien konfigurieren.

Eine Anleitung zum Bereitstellen dieser Konfigurationen finden Sie unter den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von RADIUS-Remoteservergruppen](nps-crp-rrsg-configure.md)
- [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)

## <a name="bkmk_logging"></a>NPS-Protokollierung

NPS-Protokollierung wird auch als RADIUS-Kontoführung bezeichnet. Konfigurieren Sie die NPS-Protokollierung an Ihre Bedürfnisse, ob NPS als RADIUS-Server, Proxy oder eine beliebige Kombination dieser Konfigurationen verwendet wird.

Um die NPS-Protokollierung konfigurieren möchten, müssen Sie konfigurieren, welche Ereignisse protokolliert und mit der Ereignisanzeige angezeigt werden soll, und klicken Sie dann bestimmt, welche anderen Informationen, die Sie sich anmelden möchten. Darüber hinaus müssen Sie entscheiden, ob der Benutzerauthentifizierung und Kontoführungsinformationen auf Text-Protokolldateien, die auf dem lokalen Computer gespeichert oder in SQL Server-Datenbank auf dem lokalen Computer oder einem Remotecomputer protokolliert werden sollen.

Weitere Informationen finden Sie unter [konfigurieren Network Policy Server Accounting](nps-accounting-configure.md).
