---
title: Planen eines NPS als RADIUS-Proxy
description: Dieses Thema enthält Informationen zur Planung der RADIUS-Proxy Bereitstellung für den Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ca77d64a-065b-4bf2-8252-3e75f71b7734
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9cdc28eae61acb0d8548627e48a882435cd7da81
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952025"
---
# <a name="plan-nps-as-a-radius-proxy"></a>Planen eines NPS als RADIUS-Proxy

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) als Remote Authentication Dial-in User Service RADIUS-Proxy bereitstellen \( \) , empfängt NPS Verbindungsanforderungen von RADIUS-Clients, wie z. b. Netzwerk Zugriffs Server oder andere RADIUS-Proxys, und leitet diese Verbindungsanforderungen an Server weiter, auf denen NPS oder andere RADIUS Sie können diese Planungsrichtlinien verwenden, um die RADIUS-Bereitstellung zu vereinfachen.

Diese Planungsrichtlinien enthalten keine Umstände, in denen Sie NPS als RADIUS-Server bereitstellen möchten. Wenn Sie NPS als RADIUS-Server bereitstellen, führt NPS Authentifizierung, Autorisierung und Kontoführung für Verbindungsanforderungen für die lokale Domäne und Domänen aus, die der lokalen Domäne vertrauen.

Bevor Sie NPS als RADIUS-Proxy in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien, um die Bereitstellung zu planen.

- Planen Sie die NPS-Konfiguration.

- Planen von RADIUS-Clients.

- Planen von RADIUS-Remote Server Gruppen.

- Planen von Attribut Bearbeitungs Regeln für die Nachrichten Weiterleitung.

- Planen von Verbindungs Anforderungs Richtlinien.

- Planen der NPS-Kontoführung.

## <a name="plan-nps-configuration"></a>Planen der NPS-Konfiguration

Wenn Sie NPS als RADIUS-Proxy verwenden, leitet NPS Verbindungsanforderungen zur Verarbeitung an einen NPS-oder einen anderen RADIUS-Server weiter. Aus diesem Grund ist die Domänen Mitgliedschaft des NPS-Proxys irrelevant. Der Proxy muss nicht in Active Directory Domain Services AD DS registriert werden, \( \) da er keinen Zugriff auf die Einwähleigenschaften von Benutzerkonten benötigt. Außerdem müssen Sie keine Netzwerk Richtlinien auf einem NPS-Proxy konfigurieren, da der Proxy keine Autorisierung für Verbindungsanforderungen ausführt. Der NPS-Proxy kann ein Domänen Mitglied sein, oder es kann sich um einen eigenständigen Server ohne Domänen Mitgliedschaft handeln.

NPS muss mit dem RADIUS-Protokoll für die Kommunikation mit RADIUS-Clients konfiguriert werden, die auch als Netzwerk Zugriffs Server bezeichnet werden. Außerdem können Sie die Typen von Ereignissen konfigurieren, die von NPS im Ereignisprotokoll aufgezeichnet werden, und Sie können eine Beschreibung für den Server eingeben.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Proxykonfiguration können Sie die folgenden Schritte ausführen.

- Bestimmen Sie die RADIUS-Ports, die der NPS-Proxy zum Empfangen von RADIUS-Nachrichten von RADIUS-Clients und zum Senden von RADIUS-Nachrichten an Mitglieder von RADIUS-Remote Server Gruppen Die standardmäßigen UDP-Ports (User Datagram Protocol) sind 1812 und 1645 für RADIUS-Authentifizierungs Nachrichten und UDP-Ports 1813 und 1646 für RADIUS-Buchhaltungs Nachrichten.

- Wenn der NPS-Proxy mit mehreren Netzwerkadaptern konfiguriert ist, bestimmen Sie die Adapter, über die der RADIUS-Datenverkehr zugelassen werden soll.

- Bestimmen Sie die Typen von Ereignissen, die von NPS im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnte Verbindungsanforderungen, erfolgreiche Verbindungsanforderungen oder beides protokollieren.

- Stellen Sie fest, ob Sie mehr als einen NPS-Proxy bereitstellen. Verwenden Sie mindestens zwei NPS-Proxys, um Fehlertoleranz bereitzustellen. Ein NPS-Proxy wird als primärer RADIUS-Proxy verwendet, der andere als eine Sicherung. Jeder RADIUS-Client wird dann für beide NPS-Proxys konfiguriert. Wenn der primäre NPS-Proxy nicht mehr verfügbar ist, senden RADIUS-Clients dann Zugriffs Anforderungs Nachrichten an den alternativen NPS-Proxy.

- Planen Sie das Skript, mit dem eine NPS-Proxykonfiguration in andere NPS-Proxys kopiert wird, um den Verwaltungsaufwand zu sparen und die falsche Konfiguration eines Servers zu verhindern. NPS bietet die Netsh-Befehle, mit denen Sie den gesamten oder einen Teil der NPS-Proxykonfiguration für den Import auf einen anderen NPS-Proxy kopieren können. Sie können die Befehle manuell an der netsh-Eingabeaufforderung ausführen. Wenn Sie jedoch die Befehlssequenz als Skript speichern, können Sie das Skript zu einem späteren Zeitpunkt ausführen, wenn Sie sich entscheiden, die Proxy Konfigurationen zu ändern.

## <a name="plan-radius-clients"></a>Planen von RADIUS-Clients

RADIUS-Clients sind Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, VPN-Server für virtuelle private Netzwerke \( \) , 802.1 x-fähige Switches und DFÜ-Server. RADIUS-Proxys, die Verbindungs Anforderungs Nachrichten an RADIUS-Server weiterleiten, sind ebenfalls RADIUS-Clients. NPS unterstützt alle Netzwerk Zugriffs Server und RADIUS-Proxys, die dem RADIUS-Protokoll entsprechen, wie in RFC 2865, "Remote Authentication Dial-in User Service \( RADIUS \) " und RFC 2866, "RADIUS Accounting" beschrieben.

Außerdem müssen sowohl drahtlos Zugriffspunkte als auch Switches in der 802.1 x-Authentifizierung aktiviert sein. Wenn Sie das Extensible Authentication Protocol (EAP) oder das Protected Extensible Authentication Protocol (PEAP) bereitstellen möchten, müssen Zugriffspunkte und Switches die Verwendung von EAP unterstützen.

Zum Testen der grundlegenden Interoperabilität für PPP-Verbindungen für drahtlos Zugriffspunkte konfigurieren Sie den Zugriffspunkt und den Zugriffs Client für die Verwendung des Kennwort-Authentifizierungs Protokolls (PAP). Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle, wie z. b. "Peer-AP", bis Sie die Tests getestet haben, die Sie für den Netzwerk Zugriff verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients können Sie die folgenden Schritte ausführen.

- Dokumentieren Sie die herstellerspezifischen Attribute (VSAs), die Sie in NPS konfigurieren müssen. Wenn Ihr nass VSAs erfordert, protokollieren Sie die VSA-Informationen zur späteren Verwendung, wenn Sie Ihre Netzwerk Richtlinien in NPS konfigurieren.

- Dokumentieren Sie die IP-Adressen der RADIUS-Clients und des NPS-Proxys, um die Konfiguration aller Geräte zu vereinfachen. Beim Bereitstellen der RADIUS-Clients müssen Sie diese so konfigurieren, dass das RADIUS-Protokoll verwendet wird, wobei die IP-Adresse des NPS-Proxys als authentifizierende Server eingegeben wird. Wenn Sie NPS für die Kommunikation mit ihren RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen in das NPS-Snap-in eingeben.

- Erstellen Sie freigegebene geheime Schlüssel für die Konfiguration auf den RADIUS-Clients und im NPS-Snap-in. Sie müssen RADIUS-Clients mit einem gemeinsamen geheimen Schlüssel oder Kennwort konfigurieren, das Sie auch beim Konfigurieren von RADIUS-Clients in NPS in das NPS-Snap-in eingeben.

## <a name="plan-remote-radius-server-groups"></a>Planen von RADIUS-Remote Server Gruppen

Wenn Sie eine Remote-RADIUS-Server Gruppe auf einem NPS-Proxy konfigurieren, weisen Sie den NPS-Proxy an, wohin einige oder alle Verbindungs Anforderungs Nachrichten gesendet werden sollen, die von Netzwerk Zugriffs Servern und NPS-Proxys oder anderen RADIUS-Proxys empfangen werden.

Sie können NPS als RADIUS-Proxy verwenden, um Verbindungsanforderungen an eine oder mehrere RADIUS-Remote Server Gruppen weiterzuleiten, und jede Gruppe kann einen oder mehrere RADIUS-Server enthalten. Wenn Sie möchten, dass der NPS-Proxy Nachrichten an mehrere Gruppen weiterleiten soll, konfigurieren Sie eine Verbindungs Anforderungs Richtlinie pro Gruppe. Die Verbindungs Anforderungs Richtlinie enthält zusätzliche Informationen, wie z. b. Regeln zur Attribut Bearbeitung, die dem NPS-Proxy mitteilen, welche Nachrichten an die in der Richtlinie angegebene Remote-RADIUS-Server Gruppe gesendet werden sollen.

Sie können RADIUS-Remote Server Gruppen mithilfe der Netsh-Befehle für NPS konfigurieren, indem Sie Gruppen direkt im NPS-Snap-in unter RADIUS-Remote Server Gruppen konfigurieren oder indem Sie den Assistenten für neue Verbindungs Anforderungs Richtlinien ausführen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung von RADIUS-Remote Server Gruppen können Sie die folgenden Schritte ausführen.

- Bestimmen Sie die Domänen, die die RADIUS-Server enthalten, an die der NPS-Proxy Verbindungsanforderungen weiterleiten soll. Diese Domänen enthalten die Benutzerkonten für Benutzer, die über die von Ihnen bereitgestellten RADIUS-Clients eine Verbindung mit dem Netzwerk herstellen.

- Bestimmen Sie, ob Sie neue RADIUS-Server in Domänen hinzufügen müssen, in denen der RADIUS noch nicht bereitgestellt wurde

- Dokumentieren Sie die IP-Adressen von RADIUS-Servern, die Sie Remote-RADIUS-Server Gruppen hinzufügen möchten.

- Bestimmen Sie, wie viele RADIUS-Remote Server Gruppen Sie erstellen müssen. In einigen Fällen empfiehlt es sich, eine Remote-RADIUS-Server Gruppe pro Domäne zu erstellen und die RADIUS-Server für die Domäne der Gruppe hinzuzufügen. Allerdings gibt es möglicherweise Fälle, in denen Sie über eine große Menge von Ressourcen in einer Domäne verfügen, darunter eine große Anzahl von Benutzern mit Benutzerkonten in der Domäne, eine große Anzahl von Domänen Controllern und eine große Anzahl von RADIUS-Servern. Oder Ihre Domäne deckt einen großen geografischen Raum ab, sodass Sie Netzwerk Zugriffs Server und RADIUS-Server an Standorten haben, die sich nicht voneinander unterliegen. In diesen und möglicherweise anderen Fällen können Sie mehrere RADIUS-Remote Server Gruppen pro Domäne erstellen.

- Erstellen Sie freigegebene geheime Schlüssel für die Konfiguration auf dem NPS-Proxy und auf den Remote-RADIUS-Servern.

## <a name="plan-attribute-manipulation-rules-for-message-forwarding"></a>Planen von Attribut Bearbeitungs Regeln für die Nachrichten Weiterleitung

Mit den Regeln für die Attribut Bearbeitung, die in Verbindungs Anforderungs Richtlinien konfiguriert sind, können Sie die Zugriffs Anforderungs Nachrichten ermitteln, die Sie an eine bestimmte Remote-RADIUS-Server Gruppe weiterleiten möchten.

Sie können NPS so konfigurieren, dass alle Verbindungsanforderungen an eine Remote-RADIUS-Server Gruppe weiterleiten werden, ohne dass Regeln für die Attribut Bearbeitung

Wenn Sie mehr als einen Speicherort haben, an den Sie Verbindungsanforderungen weiterleiten möchten, müssen Sie für jeden Standort eine Verbindungs Anforderungs Richtlinie erstellen und dann die Richtlinie mit der Remote-RADIUS-Server Gruppe konfigurieren, an die Sie Nachrichten weiterleiten möchten, sowie mit den Regeln für die Attribut Bearbeitung, die NPS darüber informieren, welche Nachrichten weiterleiten sollen.

Sie können Regeln für die folgenden Attribute erstellen.

- Aufgerufene Stations-ID. Die Telefonnummer des Netzwerk Zugriffs Servers (NAS). Der Wert dieses Attributs ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax zum Angeben von Bereichs Codes verwenden.

- "Call-Station-ID". Die vom Aufrufer verwendete Telefonnummer. Der Wert dieses Attributs ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax zum Angeben von Bereichs Codes verwenden.

- Benutzer Name. Der Benutzername, der vom Zugriffs Client bereitgestellt wird und der vom NAS in der RADIUS-Access-Request-Nachricht eingeschlossen wird. Der Wert dieses Attributs ist eine Zeichenfolge, die in der Regel einen Bereichs Namen und einen Benutzerkonto Namen enthält.

Um Bereichs Namen im Benutzernamen einer Verbindungsanforderung ordnungsgemäß zu ersetzen oder zu konvertieren, müssen Sie die Regeln für die Attribut Bearbeitung für das Benutzernamen Attribut in der entsprechenden Verbindungs Anforderungs Richtlinie konfigurieren.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung von Regeln für die Attribut Bearbeitung können Sie die folgenden Schritte ausführen.

- Planen Sie das Nachrichten Routing vom NAS über den Proxy zu den Remote-RADIUS-Servern, um sicherzustellen, dass Sie über einen logischen Pfad verfügen, mit dem Nachrichten an die RADIUS-Server weiterleiten werden.

- Bestimmen Sie ein oder mehrere Attribute, die Sie für die einzelnen Verbindungs Anforderungs Richtlinien verwenden möchten.

- Dokumentieren Sie die Regeln für die Attribut Bearbeitung, die Sie für die einzelnen Verbindungs Anforderungs Richtlinien verwenden möchten, und passen Sie die Regeln mit der Remote-RADIUS-Server Gruppe an, an die Nachrichten weitergeleitet werden.

## <a name="plan-connection-request-policies"></a>Planen von Verbindungs Anforderungs Richtlinien

Die Standard-Verbindungs Anforderungs Richtlinie ist für NPS konfiguriert, wenn Sie als RADIUS-Server verwendet wird. Zusätzliche Verbindungs Anforderungs Richtlinien können verwendet werden, um spezifischere Bedingungen zu definieren, Regeln zur Attribut Manipulation zu erstellen, die NPS mitteilen, welche Nachrichten an Remote-RADIUS-Server Gruppen weiterzuleiten sind, und erweiterte Attribute anzugeben. Verwenden Sie den Assistenten für neue Verbindungs Anforderungs Richtlinien, um entweder allgemeine oder benutzerdefinierte Verbindungs Anforderungs Richtlinien zu erstellen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung von Verbindungs Anforderungs Richtlinien können Sie die folgenden Schritte ausführen.

- Löschen Sie die Standard-Verbindungs Anforderungs Richtlinie auf jedem Server, auf dem NPS ausgeführt wird und der ausschließlich als RADIUS-Proxy fungiert.

- Planen Sie zusätzliche Bedingungen und Einstellungen, die für jede Richtlinie erforderlich sind, und kombinieren Sie diese Informationen mit der RADIUS-Remote Server Gruppe und den für die Richtlinie vorgesehenen Regeln zur Attribut Bearbeitung.

- Entwerfen Sie den Plan, um allgemeine Verbindungs Anforderungs Richtlinien an alle NPS-Proxys zu verteilen. Erstellen Sie Richtlinien, die für mehrere NPS-Proxys auf einem NPS gemeinsam sind, und verwenden Sie dann die Netsh-Befehle für NPS, um die Verbindungs Anforderungs Richtlinien und die Serverkonfiguration für alle anderen Proxys

## <a name="plan-nps-accounting"></a>Planen der NPS-Kontoführung

Wenn Sie NPS als RADIUS-Proxy konfigurieren, können Sie ihn so konfigurieren, dass die RADIUS-Kontoführung mithilfe von NPS-Format Protokolldateien, Daten Bank kompatiblen Format Protokolldateien oder NPS-SQL Server Protokollierung durchgeführt wird.

Sie können Buchhaltungs Nachrichten auch an eine Remote-RADIUS-Server Gruppe weiterleiten, die die Kontoführung mithilfe eines dieser Protokollierungs Formate ausführt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Buchhaltung können Sie die folgenden Schritte ausführen.

- Legen Sie fest, ob der NPS-Proxy Buchhaltungs Dienste ausführen oder Buchhaltungs Nachrichten an eine Remote-RADIUS-Server Gruppe für die Kontoführung weiterleiten soll.

- Planen Sie die Deaktivierung der lokalen NPS-Proxy Kontoführung, wenn Sie Buchhaltungs Nachrichten an andere Server weiterleiten möchten.

- Planen von Konfigurationsschritten für die Verbindungs Anforderungs Richtlinie, wenn Sie Buchhaltungs Nachrichten an andere Server weiterleiten möchten. Wenn Sie die lokale Kontoführung für den NPS-Proxy deaktivieren, muss jede Verbindungs Anforderungs Richtlinie, die Sie auf diesem Proxy konfigurieren, die Überführung der Nachrichten Weiterleitung aktiviert und ordnungsgemäß konfiguriert haben.

- Bestimmen Sie das zu verwendende Protokollierungs Format: die IAS-Format Protokolldateien, Daten Bank kompatible Format Protokolldateien oder die NPS-SQL Server Protokollierung.

Informationen zum Konfigurieren des Lasten Ausgleichs für NPS als RADIUS-Proxy finden Sie unter [NPS-Proxy Server-Lastenausgleich](nps-manage-proxy-lb.md).

