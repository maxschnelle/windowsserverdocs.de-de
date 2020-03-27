---
title: Netzwerkrichtlinienserver (Network Policy Server, NPS)
description: Dieses Thema enthält eine Übersicht über den Netzwerk Richtlinien Server in Windows Server 2016 und Windows Server 2019 und enthält Links zu weiteren Anleitungen zu NPS.
manager: dougkim
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: lizross
author: eross-msft
ms.date: 06/20/2018
ms.openlocfilehash: b509bb14757fab6ebd32490d0146b2801bc8e9f1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315623"
---
# <a name="network-policy-server-nps"></a>Netzwerkrichtlinienserver (Network Policy Server, NPS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2019

In diesem Thema finden Sie eine Übersicht über den Netzwerk Richtlinien Server unter Windows Server 2016 und Windows Server 2019. NPS wird installiert, wenn Sie das Feature für Netzwerk Richtlinien-und Zugriffs Dienste (Network Policy and Access Services, NPAS) in Windows Server 2016 und Server 2019 installieren.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende NPS-Dokumentation verfügbar.
> - [Bewährte Methoden für den Netzwerk Richtlinien Server](nps-best-practices.md)
> - [Ersten Schritte mit dem Netzwerk Richtlinien Server](nps-getstart-top.md)
> - [Planen des Netzwerk Richtlinien Servers](nps-plan-top.md)
> - [Netzwerk Richtlinien Server bereitstellen](nps-deploy.md)
> - [Netzwerk Richtlinien Server verwalten](nps-manage-top.md)
> - [Cmdlets für Netzwerk Richtlinien Server (Network Policy Server, NPS) in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2016 und Windows 10
> - [Cmdlets für Netzwerk Richtlinien Server (Network Policy Server, NPS) in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2012 R2 und Windows 8.1
> - [NPS-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj872739.aspx) für Windows Server 2012 und Windows 8

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

Sie können NPS auch als RADIUS-Proxy (Remote Authentication Dial-in User Service) konfigurieren, um Verbindungsanforderungen an einen NPS-Remote Server oder einen anderen RADIUS-Server weiterzuleiten, sodass Sie einen Lastenausgleich für Verbindungsanforderungen ausführen und diese zur Authentifizierung an die richtige Domäne weiterleiten können. und Autorisierung.

Mit NPS können Sie die Authentifizierung, Autorisierung und Kontoführung für Netzwerk Zugriffe mithilfe der folgenden Features zentral konfigurieren und verwalten:

- **RADIUS-Server**. NPS führt die zentralisierte Authentifizierung, Autorisierung und Kontoführung für drahtlose, authentifizier Ende Switches, RAS-und VPN-Verbindungen (virtuelles privates Netzwerk) durch. Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerkzugriffsserver, z. B. drahtlose Zugriffspunkte und VPN-Server, als RADIUS-Clients in NPS. Sie können auch Netzwerkrichtlinien konfigurieren, mit denen NPS Verbindungsanforderungen autorisiert, und Sie können die RADIUS-Kontoführung so konfigurieren, dass NPS Kontoführungsinformationen in Protokolldateien auf der lokalen Festplatte oder in einer Microsoft SQL Server-Datenbank protokolliert. Weitere Informationen finden Sie unter [RADIUS-Server](#radius-server).
- **RADIUS-Proxy**. Wenn Sie NPS als RADIUS-Proxy verwenden, konfigurieren Sie Verbindungs Anforderungs Richtlinien, die den NPS mitteilen, welche Verbindungsanforderungen an andere RADIUS-Server weiterleiten sollen und an welche RADIUS-Server Sie Verbindungsanforderungen weiterleiten möchten. Sie können NPS auch so konfigurieren, dass Kontoführungsdaten weitergeleitet und von einem oder mehreren Computern in einer RADIUS-Remoteservergruppe protokolliert werden. Informationen zum Konfigurieren von NPS als RADIUS-Proxy Server finden Sie in den folgenden Themen. Weitere Informationen finden Sie unter [RADIUS-Proxy](#radius-proxy).
    - [Konfigurieren von Verbindungs Anforderungs Richtlinien](nps-crp-configure.md)
- **RADIUS**-Kontoführung. Sie können NPS so konfigurieren, dass Ereignisse in einer lokalen Protokolldatei oder in einer lokalen oder Remote Instanz von Microsoft SQL Server protokolliert werden. Weitere Informationen finden Sie unter [NPS-Protokollierung](#nps-logging).

> [!IMPORTANT]
> Der Netzwerk Zugriffsschutz \(NAP-\), die Integritäts Registrierungsstelle \(HRA\)und das Host Credential Authorization-Protokoll \(HCAP-\) wurden in Windows Server 2012 R2 als veraltet eingestuft und sind in Windows Server 2016 nicht verfügbar. Wenn Sie über eine NAP-Bereitstellung mit älteren Betriebssystemen als Windows Server 2016 verfügen, können Sie die NAP-Bereitstellung nicht zu Windows Server 2016 migrieren.

Sie können NPS mit einer beliebigen Kombination dieser Features konfigurieren. Sie können z. b. einen NPS als RADIUS-Server für VPN-Verbindungen und auch als RADIUS-Proxy für die weiterleiten einiger Verbindungsanforderungen an Mitglieder einer RADIUS-Remote Server Gruppe für die Authentifizierung und Autorisierung in einer anderen Domäne konfigurieren.

## <a name="windows-server-editions-and-nps"></a>Windows Server-Editionen und NPS

NPS bietet unterschiedliche Funktionen, abhängig von der von Ihnen installierten Edition von Windows Server.

### <a name="windows-server-2016-or-windows-server-2019-standarddatacenter-edition"></a>Windows Server 2016 oder Windows Server 2019 Standard/Datacenter Edition

Mit NPS in Windows Server 2016 Standard oder Datacenter können Sie eine unbegrenzte Anzahl von RADIUS-Clients und RADIUS-Remote Server Gruppen konfigurieren. Darüber hinaus können Sie RADIUS-Clients durch Festlegung eines IP-Adressbereichs konfigurieren.

> [!NOTE]
> Die Funktion "Windows-Netzwerk Richtlinien-und-Zugriffs Dienste" ist auf Systemen, die mit einer Server Core-Installation installiert wurden, nicht verfügbar

Die folgenden Abschnitte enthalten ausführlichere Informationen zu NPS als RADIUS-Server und Proxy.

## <a name="radius-server-and-proxy"></a>RADIUS-Server und-Proxy

Sie können NPS als RADIUS-Server, RADIUS-Proxy oder beides verwenden.

### <a name="radius-server"></a>RADIUS-Server

NPS ist die Microsoft-Implementierung des RADIUS-Standards, der durch die Internet Engineering Task Force \(IETF\) in RFCs 2865 und 2866 angegeben wird. Als RADIUS-Server führt NPS eine zentralisierte Verbindungs Authentifizierung, Autorisierung und Kontoführung für viele Arten von Netzwerk Zugriff aus. Hierzu zählen beispielsweise drahtlose, authentifizier Ende Switches, DFÜ-und virtuelle private Netzwerke \(VPN\) Remote Zugriff und Router-zu-Router-Verbindungen.

> [!NOTE]
> Informationen zum Bereitstellen von NPS als RADIUS-Server finden Sie unter Bereitstellen des [Netzwerk Richtlinien Servers](nps-deploy.md).

NPS ermöglicht die Verwendung einer heterogenen Gruppe von drahtlos-, Switch-, Remote-oder VPN-Geräten. Sie können NPS mit dem Remote Zugriffs Dienst verwenden, der in Windows Server 2016 verfügbar ist.

NPS verwendet eine Active Directory Domain Services \(AD DS\) Domäne oder die SAM-Benutzerkonten Datenbank (Local Security Accounts Manager), um Benutzer Anmelde Informationen für Verbindungsversuche zu authentifizieren. Wenn ein Server, auf dem NPS ausgeführt wird, Mitglied einer AD DS Domäne ist, verwendet NPS den Verzeichnisdienst als Benutzerkonten Datenbank und ist Teil einer Single Sign-On Lösung. Der gleiche Satz von Anmelde Informationen wird für die Netzwerk Zugriffs \(Steuerung verwendet, um den Zugriff auf ein Netzwerk\) zu authentifizieren und zu autorialisieren und sich bei einer AD DS Domäne anzumelden.

> [!NOTE]
> NPS verwendet die DFÜ-Eigenschaften des Benutzerkontos und der Netzwerk Richtlinien, um eine Verbindung zu autorisieren.

Internet Dienstanbieter \(ISPs\) und Organisationen, die den Netzwerk Zugriff aufrechterhalten, haben eine größere Herausforderung, alle Arten von Netzwerk Zugriff von einem einzigen Verwaltungspunkt aus zu verwalten, unabhängig davon, welche Art von Netzwerk Zugriffs Geräten verwendet wird. Der RADIUS-Standard unterstützt diese Funktionalität sowohl in homogenen als auch heterogenen Umgebungen. RADIUS ist ein Client/Server-Protokoll, mit dem Netzwerk Zugriffs Ausrüstung (als RADIUS-Clients verwendet) zum Übermitteln von Authentifizierungs-und Buchhaltungs Anforderungen an einen RADIUS-Server aktiviert wird.

Ein RADIUS-Server hat Zugriff auf Benutzerkontoinformationen und kann Anmelde Informationen für die Netzwerk Zugriffs Authentifizierung überprüfen. Wenn Benutzer Anmelde Informationen authentifiziert werden und der Verbindungsversuch autorisiert ist, autorisiert der RADIUS-Server den Benutzer Zugriff auf Grundlage der angegebenen Bedingungen und protokolliert dann die Netzwerk Zugriffs Verbindung in einem Buchhaltungs Protokoll. Durch die Verwendung von RADIUS können Benutzerauthentifizierung, Autorisierung und Kontoführungs Daten für den Netzwerk Zugriff an einem zentralen Ort und nicht auf jedem Zugriffs Server gesammelt und verwaltet werden.

#### <a name="using-nps-as-a-radius-server"></a>Verwenden von NPS als RADIUS-Server

Sie können NPS als RADIUS-Server verwenden, wenn Folgendes der Fall ist:

- Sie verwenden eine AD DS Domäne oder die lokale SAM-Benutzerkonten Datenbank als Benutzerkonto Datenbank für Zugriffs Clients. 
- Sie verwenden den Remote Zugriff auf mehreren DFÜ-Servern, VPN-Servern oder Router für die Bedarfs gesteuerte Verwendung, und Sie möchten die Konfiguration der Netzwerk Richtlinien und der Verbindungs Protokollierung und-Kontoführung zentralisieren. 
- Sie überlagern ihren DFÜ-, VPN-oder drahtlosen Zugriff auf einen Dienstanbieter. Die Zugriffs Server verwenden RADIUS zum Authentifizieren und Autorisieren von Verbindungen, die von Mitgliedern Ihrer Organisation hergestellt werden.
- Sie möchten die Authentifizierung, Autorisierung und Kontoführung für eine heterogene Gruppe von Zugriffs Servern zentralisieren.

Die folgende Abbildung zeigt NPS als RADIUS-Server für eine Vielzahl von Zugriffs Clients. 

![NPS als RADIUS-Server](../../media/Nps-Server/Nps-Server.jpg)

### <a name="radius-proxy"></a>RADIUS-Proxy

Als RADIUS-Proxy leitet NPS Authentifizierungs-und Buchhaltungs Nachrichten an NPS und andere RADIUS-Server weiter. Sie können NPS als RADIUS-Proxy verwenden, um das Routing von RADIUS-Nachrichten zwischen RADIUS-Clients \(auch als Netzwerk Zugriffs Server bezeichnet\) und RADIUS-Servern bereitzustellen, die Benutzerauthentifizierung, Autorisierung und Kontoführung für den Verbindungsversuch durchführen. 

Wenn NPS als RADIUS-Proxy verwendet wird, handelt es sich um einen zentralen Wechsel-bzw. Routing Punkt, über den RADIUS-Zugriffs-und Buchhaltungs Nachrichten fließen. NPS zeichnet Informationen zu den weitergeleiteten Nachrichten in einem Buchhaltungs Protokoll auf.

#### <a name="using-nps-as-a-radius-proxy"></a>Verwenden von NPS als RADIUS-Proxy

Sie können NPS als RADIUS-Proxy verwenden, wenn Folgendes der Fall ist:

- Sie sind ein Dienstanbieter, der für mehrere Kunden ausgelagerte DFÜ-, VPN-oder Drahtlos Netzwerk Zugriffs Dienste anbietet. Ihr nass sendet Verbindungsanforderungen an den NPS-RADIUS-Proxy. Basierend auf dem Bereichs Teil des Benutzernamens in der Verbindungsanforderung leitet der NPS-RADIUS-Proxy die Verbindungsanforderung an einen RADIUS-Server weiter, der vom Kunden verwaltet wird, und kann den Verbindungsversuch authentifizieren und autorisieren.
- Sie möchten Authentifizierung und Autorisierung für Benutzerkonten bereitstellen, die keine Mitglieder der Domäne sind, in der das NPS Mitglied ist, oder eine andere Domäne, die über eine bidirektionale Vertrauensstellung mit der Domäne verfügt, in der das NPS Mitglied ist. Dies schließt Konten in nicht vertrauenswürdigen Domänen, unidirektionale vertrauenswürdige Domänen und andere Gesamtstrukturen ein. Anstatt ihre Zugriffs Server so zu konfigurieren, dass Ihre Verbindungsanforderungen an einen NPS-RADIUS-Server gesendet werden, können Sie Sie so konfigurieren, dass Ihre Verbindungsanforderungen an einen NPS-RADIUS-Proxy gesendet werden. Der NPS-RADIUS-Proxy verwendet den Bereichs Namensteil des Benutzernamens und leitet die Anforderung an einen NPS in der richtigen Domäne oder Gesamtstruktur weiter. Verbindungsversuche für Benutzerkonten in einer Domäne oder Gesamtstruktur können für "nass" in einer anderen Domäne oder Gesamtstruktur authentifiziert werden.
- Sie möchten die Authentifizierung und Autorisierung mithilfe einer Datenbank durchführen, bei der es sich nicht um eine Windows-Konto Datenbank handelt. In diesem Fall werden Verbindungsanforderungen, die einem angegebenen Bereichs Namen entsprechen, an einen RADIUS-Server weitergeleitet, der Zugriff auf eine andere Datenbank mit Benutzerkonten und Autorisierungs Daten hat. Beispiele für andere Benutzer Datenbanken sind Novell Directory Services (NDS) und strukturierte Abfragesprache (SQL)-Datenbanken.
- Sie möchten eine große Anzahl von Verbindungsanforderungen verarbeiten. Anstatt Ihre RADIUS-Clients so zu konfigurieren, dass Sie versuchen, die Verbindungs-und Buchhaltungs Anforderungen über mehrere RADIUS-Server hinweg auszugleichen, können Sie Sie so konfigurieren, dass Ihre Verbindungs-und Buchhaltungs Anforderungen an einen NPS-RADIUS-Proxy gesendet werden. Der NPS-RADIUS-Proxy gleicht die Last der Verbindungs-und Buchhaltungs Anforderungen dynamisch auf mehrere RADIUS-Server aus und erhöht die Verarbeitung einer großen Anzahl von RADIUS-Clients und-Authentifizierungen pro Sekunde.
- Sie möchten RADIUS-Authentifizierung und-Autorisierung für externe Dienstanbieter bereitstellen und die Intranetkonfiguration minimieren. Eine Intranetfirewall befindet sich zwischen Ihrem Umkreis Netzwerk (dem Netzwerk zwischen Ihrem Intranet und dem Internet) und dem Intranet. Durch das Platzieren eines NPS in Ihrem Umkreis Netzwerk muss die Firewall zwischen dem Umkreis Netzwerk und dem Intranet den Datenverkehr zwischen dem NPS und mehreren Domänen Controllern zulassen. Wenn Sie den NPS durch einen NPS-Proxy ersetzen, darf die Firewall nur RADIUS-Datenverkehr zwischen dem NPS-Proxy und einem oder mehreren NPSS innerhalb Ihres Intranets zulassen.

Die folgende Abbildung zeigt NPS als RADIUS-Proxy zwischen RADIUS-Clients und RADIUS-Servern.

![NPS als RADIUS-Proxy](../../media/Nps-Proxy/Nps-Proxy.jpg)

Mit NPS können Organisationen auch die Remote Zugriffs Infrastruktur an einen Dienstanbieter ausgelagert und dabei die Kontrolle über die Benutzerauthentifizierung, Autorisierung und Kontoführung behalten.

NPS-Konfigurationen können für die folgenden Szenarien erstellt werden:

- Drahtloser Zugriff
- DFÜ-oder VPN-Remote Zugriff (Virtual Private Network)
- Ausgelagerter Einwählzugriff oder drahtlos Zugriff
- Internetzugriff
- Authentifizierter Zugriff auf Extranetressourcen für Geschäftspartner

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>Beispiele für die Konfiguration des RADIUS-Servers und RADIUS-Proxy

Die folgenden Konfigurationsbeispiele veranschaulichen, wie Sie NPS als RADIUS-Server und RADIUS-Proxy konfigurieren können.

**NPS als RADIUS-Server**. In diesem Beispiel ist NPS als RADIUS-Server konfiguriert, die standardmäßige Verbindungs Anforderungs Richtlinie ist die einzige konfigurierte Richtlinie, und alle Verbindungsanforderungen werden vom lokalen NPS verarbeitet. Der NPS kann Benutzer authentifizieren und autorisieren, deren Konten sich in der Domäne des NPS und in vertrauenswürdigen Domänen befinden.

**NPS als RADIUS-Proxy**. In diesem Beispiel wird der NPS als RADIUS-Proxy konfiguriert, der Verbindungsanforderungen an Remote-RADIUS-Server Gruppen in zwei nicht vertrauenswürdigen Domänen weiterleitet. Die Standard-Verbindungs Anforderungs Richtlinie wird gelöscht, und es werden zwei neue Verbindungs Anforderungs Richtlinien erstellt, um Anforderungen an die beiden nicht vertrauenswürdigen Domänen weiterzuleiten. In diesem Beispiel verarbeitet NPS keine Verbindungsanforderungen auf dem lokalen Server. 

**NPS als RADIUS-Server und RADIUS-Proxy**. Zusätzlich zu der standardmäßigen Verbindungs Anforderungs Richtlinie, die festlegt, dass Verbindungsanforderungen lokal verarbeitet werden, wird eine neue Verbindungs Anforderungs Richtlinie erstellt, die Verbindungsanforderungen an einen NPS-Server oder einen anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. Diese zweite Richtlinie wird als Proxy Richtlinie bezeichnet. In diesem Beispiel wird die Proxy Richtlinie zuerst in der geordneten Liste der Richtlinien angezeigt. Wenn die Verbindungsanforderung mit der Proxy Richtlinie übereinstimmt, wird die Verbindungsanforderung an den RADIUS-Server in der Remote-RADIUS-Server Gruppe weitergeleitet. Wenn die Verbindungsanforderung nicht mit der Proxy Richtlinie, aber mit der standardmäßigen Verbindungs Anforderungs Richtlinie identisch ist, verarbeitet NPS die Verbindungsanforderung auf dem lokalen Server. Wenn die Verbindungsanforderung keiner Richtlinie entspricht, wird sie verworfen.

**NPS als RADIUS-Server mit Remote Buchhaltungs Servern**. In diesem Beispiel ist der lokale NPS nicht für die Kontoführung konfiguriert, und die standardmäßige Verbindungs Anforderungs Richtlinie wird so überarbeitet, dass RADIUS-Buchhaltungs Nachrichten an einen NPS oder einen anderen RADIUS-Server in einer RADIUS-Remote Server Gruppe weitergeleitet werden. Obwohl Buchhaltungs Nachrichten weitergeleitet werden, werden Authentifizierungs-und Autorisierungs Nachrichten nicht weitergeleitet, und der lokale NPS führt diese Funktionen für die lokale Domäne und alle vertrauenswürdigen Domänen aus.

**NPS mit Remote RADIUS-zu-Windows-Benutzer Zuordnung**. In diesem Beispiel fungiert NPS sowohl als RADIUS-Server als auch als RADIUS-Proxy für jede einzelne Verbindungsanforderung, indem die Authentifizierungsanforderung an einen RADIUS-Remote Server weitergeleitet wird, während ein lokales Windows-Benutzerkonto für die Autorisierung verwendet wird. Diese Konfiguration wird implementiert, indem das Attribut Remote RADIUS für Windows-Benutzer Zuordnung als Bedingung der Verbindungs Anforderungs Richtlinie konfiguriert wird. \(zusätzlich muss ein Benutzerkonto lokal auf dem RADIUS-Server erstellt werden, das den gleichen Namen wie das Remote Benutzerkonto hat, mit dem die Authentifizierung vom RADIUS-Remote Server durchgeführt wird.\)

## <a name="configuration"></a>Konfiguration

Um NPS als RADIUS-Server zu konfigurieren, können Sie entweder die Standardkonfiguration oder die erweiterte Konfiguration in der NPS-Konsole oder in Server-Manager verwenden. Wenn Sie NPS als RADIUS-Proxy konfigurieren möchten, müssen Sie die erweiterte Konfiguration verwenden.

### <a name="standard-configuration"></a>Standard Konfiguration

Mit der Standardkonfiguration werden Assistenten bereitgestellt, die Sie bei der Konfiguration von NPS für die folgenden Szenarien unterstützen:

- RADIUS-Server für DFÜ-oder VPN-Verbindungen
- RADIUS-Server für drahtlose oder verkabelte 802.1X-Verbindungen

Öffnen Sie zum Konfigurieren von NPS mithilfe eines Assistenten die NPS-Konsole, wählen Sie eines der vorangegangenen Szenarien aus, und klicken Sie dann auf den Link zum Öffnen des Assistenten.

### <a name="advanced-configuration"></a>Erweiterte Konfiguration

Wenn Sie die erweiterte Konfiguration verwenden, konfigurieren Sie NPS manuell als RADIUS-Server oder RADIUS-Proxy. 

Wenn Sie NPS mithilfe der erweiterten Konfiguration konfigurieren möchten, öffnen Sie die NPS-Konsole, und klicken Sie dann auf den Pfeil neben **Erweiterte Konfiguration** , um diesen Abschnitt zu erweitern.

Die folgenden erweiterten Konfigurationselemente werden bereitgestellt.

#### <a name="configure-radius-server"></a>Konfigurieren des RADIUS-Servers

Um NPS als RADIUS-Server zu konfigurieren, müssen Sie RADIUS-Clients, die Netzwerk Richtlinie und die RADIUS-Kontoführung konfigurieren.

Anweisungen zum Erstellen dieser Konfigurationen finden Sie in den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von Netzwerkrichtlinien](nps-np-configure.md)
- [Konfigurieren der Netzwerk Richtlinien Server-Kontoführung](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>RADIUS-Proxy konfigurieren

Wenn Sie NPS als RADIUS-Proxy konfigurieren möchten, müssen Sie RADIUS-Clients, RADIUS-Remote Server Gruppen und Verbindungs Anforderungs Richtlinien konfigurieren.

Anweisungen zum Erstellen dieser Konfigurationen finden Sie in den folgenden Themen.

- [Konfigurieren von RADIUS-Clients](nps-radius-clients-configure.md)
- [Konfigurieren von Remote-RADIUS-Server Gruppen](nps-crp-rrsg-configure.md)
- [Konfigurieren von Verbindungs Anforderungs Richtlinien](nps-crp-configure.md)

## <a name="nps-logging"></a>NPS-Protokollierung

NPS-Protokollierung wird auch als RADIUS-Kontoführung bezeichnet. Konfigurieren Sie die NPS-Protokollierung gemäß Ihren Anforderungen, ob NPS als RADIUS-Server, Proxy oder eine beliebige Kombination dieser Konfigurationen verwendet wird.

Zum Konfigurieren der NPS-Protokollierung müssen Sie konfigurieren, welche Ereignisse Ereignisanzeige protokolliert und angezeigt werden sollen, und dann bestimmen, welche anderen Informationen Sie protokollieren möchten. Außerdem müssen Sie entscheiden, ob Sie die Benutzerauthentifizierung und die Buchhaltungsinformationen in Text Protokolldateien protokollieren möchten, die auf dem lokalen Computer oder in einer SQL Server Datenbank auf dem lokalen Computer oder einem Remote Computer gespeichert sind.

Weitere Informationen finden Sie unter [Konfigurieren der Netzwerk Richtlinien Server](nps-accounting-configure.md)-Kontoführung.
