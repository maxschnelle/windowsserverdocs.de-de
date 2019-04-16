---
title: 'Bewährte Methoden: Netzwerk'
description: Dieses Thema enthält bewährte Methoden für die Bereitstellung und Verwaltung von Netzwerkrichtlinienserver in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5a9a68965d0d19504352ad67f7ab268b3d344fb2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-best-practices"></a>Bewährte Methoden: Netzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu bewährten Methoden für die Bereitstellung und Verwaltung von Netzwerkrichtlinienserver \(NPS\).

Die folgenden Abschnitte enthalten bewährte Methoden für verschiedene Aspekte der NPS-Bereitstellung.

## <a name="accounting"></a>Kontoführung

Im folgenden werden die bewährten Methoden für die NPS-Protokollierung.

Es gibt zwei Arten von accounting oder Protokollierung im NPS:

- Ereignisprotokollierung für den NPS. Ereignisprotokollierung NPS-Ereignisse aufzeichnen können in den Ereignisprotokollen System und Sicherheit. Dies wird in erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen verwendet.

- Protokollierung der Benutzerauthentifizierung und kontoführungsanforderungen. Melden Sie Benutzer-Authentifizierung und-Kontoführung Anforderungen in Protokolldateien im Textformat oder Datenbank oder Sie können sich bei einer gespeicherten Prozedur in einer SQL Server 2000-Datenbank. Fordern Sie die Protokollierung wird in erster Linie für Verbindung Analyse und Abrechnung Zwecke verwendet und eignet sich auch als Untersuchung Security-Tool, mit dem Sie eine Methode zum Nachverfolgen der Aktivität eines Angreifers.

Der NPS-Protokollierung am effektivsten nutzen:

- Aktivieren Sie die Protokollierung \(initially\) für die Authentifizierung und-Kontoführung Datensätze. Diese Auswahl zu ändern, nachdem Sie ermittelt haben, was für Ihre Umgebung geeignet ist.

- Sicherstellen Sie, dass die Protokollierung mit einer Kapazität konfiguriert ist, die ausreicht, um Ihre Protokolle zu verwalten.

- Sichern Sie alle Protokolldateien in regelmäßigen Abständen, da sie neu erstellt werden können, wenn sie beschädigt oder gelöscht werden.

- Verwenden Sie die RADIUS-Class-Attribut zum Protokollieren der Verwendung und einfacheren identifizieren, welche Abteilung oder einem Benutzer, die Nutzung in Rechnung stellen. Obwohl die automatisch generierte Class-Attribut für jede Anforderung eindeutig ist, können Duplikate vorhanden sein in Fällen, in dem die Antwort auf einem Server verloren und die Anforderung erneut gesendet wird. Sie müssen möglicherweise doppelte Anforderungen aus den Protokollen zum Nachverfolgen der Verwendung genauer zu löschen.

- Wenn Ihre Netzwerkzugriffsserver und RADIUS-Proxyserver in regelmäßigen Abständen fiktiven Verbindung-Anforderung an den NPS Nachrichten, stellen Sie sicher, dass der NPS-Server online ist, verwenden Sie die **ping Benutzername** Einstellung in der Registrierung. Dieser Einstellung wird konfiguriert, um diese Verbindungsanfragen automatisch ablehnen, ohne den Netzwerkrichtlinienserver. Darüber hinaus zeichnet NPS nicht Transaktionen im Zusammenhang mit dem erfundenen Benutzernamen in Protokolldateien, mit dessen Hilfe das Ereignisprotokoll einfacher zu interpretieren.

- Deaktivieren Sie die Weiterleitung von NAS-Benachrichtigung. Sie können die Weiterleitung von Start deaktivieren und Abbruchfehlern Netzwerkzugriffsservern (NAS) für Mitglieder einer RADIUS-Remoteserver Gruppe, auf dem Netzwerkrichtlinienserver konfiguriert ist. Weitere Informationen finden Sie unter [deaktivieren NAS Benachrichtigung weiterleiten](nps-disable-nas-notifications.md).

Weitere Informationen finden Sie unter [konfigurieren Network Policy Server Accounting](nps-accounting-configure.md).

- Um SQL Server-Protokollierung Failover und Redundanz bereitzustellen, setzen Sie zwei Computer mit SQL Server in verschiedenen Subnetzen. Verwenden Sie den SQL Server **Assistenten zum Erstellen einer Publikation** Datenbankreplikation zwischen den beiden Servern einrichten. Weitere Informationen finden Sie unter [technische Dokumentation zu SQL Server](https://msdn.microsoft.com/library/ms130214.aspx) und [SQL Server-Replikation](https://msdn.microsoft.com/library/ms151198.aspx).

## <a name="authentication"></a>Authentifizierung

Im folgenden werden die bewährten Methoden für die Authentifizierung.

- Verwenden Sie zertifikatbasierte Authentifizierungsmethoden, z. B. Protected Extensible Authentication Protocol \(PEAP\) und Extensible Authentication Protocol \(EAP\) für strenge Authentifizierung. Verwenden Sie nicht nur Kennwort-Authentifizierungsmethoden, da sie eine Vielzahl von Angriffen anfällig sind und sind nicht sicher. Für eine sichere WLAN-Authentifizierung ist mit PEAP\-MS\-CHAP v2 empfohlen, da der NPS-Server bewiesen, seine Identität für drahtlose Clients dass mithilfe eines Serverzertifikats während der Benutzer seine Identität bei ihren Benutzernamen und Ihr Kennwort zu beweisen.  Weitere Informationen zur Verwendung von NPS in der WLAN-Bereitstellung finden Sie unter [Bereitstellung Kennwort-basierte Drahtloszugriff mit 802.1X-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).
- Ihre eigene Zertifizierungsstelle bereitstellen \(CA\) mit Active Directory&reg; Zertifikatdienste \(AD CS\) bei Verwendung der starken zertifikatbasierte Authentifizierungsmethoden, z. B. PEAP und EAP, die ein Serverzertifikat auf dem NPS-Servern erforderlich. Sie können auch die Zertifizierungsstelle verwenden, Zertifikate und Zertifikate zu registrieren. Weitere Informationen zum Bereitstellen von Serverzertifikaten mit NPS und RAS-Servern finden Sie unter [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="client-computer-configuration"></a>Konfiguration für Clientcomputer

Im folgenden werden die bewährten Methoden für die Konfiguration des Client-Computers.

- Konfigurieren Sie alle Ihre Domänenmitglied 802.1 X Clientcomputer automatisch mithilfe von Gruppenrichtlinien. Weitere Informationen finden Sie im Abschnitt "Konfigurieren Wireless Network (IEEE 802.11) Policies" im Thema [Wireless Access Bereitstellung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies).

## <a name="installation-suggestions"></a>Installation Vorschläge

Im folgenden werden die bewährten Methoden für die Installation von NPS.

- Installieren Sie vor der Installation von NPS und Testen Sie alle Ihre Netzwerkzugriffsserver mithilfe lokaler Authentifizierungsmethoden, bevor Sie sie als RADIUS-Clients in NPS konfigurieren.

- Nachdem Sie installieren und Konfigurieren des Netzwerkrichtlinienservers, speichern Sie die Konfiguration mithilfe des Windows PowerShell-Befehls [Export-NpsConfiguration](https://technet.microsoft.com/en-us/library/jj872749.aspx). Speichern Sie die NPS-Konfiguration mit dem folgenden Befehl, der jedes Mal neu konfigurieren Sie den NPS-Server.

>[!CAUTION]
>- Die exportierte Datei des NPS-Konfiguration enthält nicht verschlüsselte gemeinsame geheime Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remoteservergruppen. Stellen Sie daher sicher, dass Sie die Datei an einem sicheren Speicherort speichern.
>- Der Exportvorgang werden in der exportierten Datei keine protokollierungseinstellungen für Microsoft SQL Server. Wenn Sie die exportierte Datei auf einen anderen NPS-Server importieren, müssen Sie manuell SQL Server-Protokollierung auf dem neuen Server konfigurieren.

## <a name="performance-tuning-nps"></a>NPS Optimieren der Leistung

Im folgenden werden die bewährten Methoden für NPS Optimieren der Leistung.

- NPS-Authentifizierung und Autorisierung optimieren und den Netzwerkverkehr zu reduzieren, installieren Sie NPS auf einem Domänencontroller.

- Wenn universelle Benutzerprinzipalnamen \(UPNs\) oder Windows Server 2008 und Windows Server 2003-Domänen verwendet werden, verwendet NPS den globalen Katalog zum Authentifizieren von Benutzern. Um die Zeit zu minimieren, dazu benötigt wird, installieren Sie NPS auf einem globalen Katalogserver oder ein Server, der auf dem gleichen Subnetz wie der globale Katalogserver ist.

- Wenn Sie die RADIUS-Remoteservergruppen konfiguriert haben, und deaktivieren Sie in NPS Verbindungsanforderungsrichtlinien, die **Kontoführungsinformationen auf den Servern in der folgenden RADIUS-Remoteservergruppe aufzeichnen** das Kontrollkästchen Diese Gruppen sind weiterhin Access Server \(NAS\) Netzwerkstart gesendet und Benachrichtigungen zu beenden. Dadurch entsteht unnötigen Netzwerkverkehr. Um diesen Datenverkehr zu vermeiden, deaktivieren Sie Weiterleitung von NAS-Benachrichtigung für einzelne Server an jeden RADIUS-Remoteservergruppe durch Deaktivieren der **weiterleiten Netzwerk starten und Beenden von Benachrichtigungen an diesen Server** Kontrollkästchen.

## <a name="using-nps-in-large-organizations"></a>Mit dem Netzwerkrichtlinienserver in großen Organisationen

Im folgenden werden die bewährten Methoden für die Verwendung von NPS in großen Organisationen.

- Wenn Sie Netzwerkrichtlinien verwenden zum Einschränken des Zugriffs für bestimmte Gruppen, erstellen eine universelle Gruppe für alle Benutzer, denen Sie den Zugriff zulassen möchten, und dann eine Netzwerkrichtlinie, die dieser universellen Gruppe Zugriff gewährt. Stellen Sie nicht alle Benutzer direkt in die universelle Gruppe, insbesondere dann, wenn Sie eine große Anzahl von ihnen in Ihrem Netzwerk verfügen. Erstellen Sie stattdessen separate Gruppen, die Mitglieder der universellen Gruppe sind, und Benutzer zu diesen Gruppen hinzufügen.

- Verwenden Sie einen User principal Name, um für Benutzer möglichst verweisen. Ein Benutzer kann den gleichen User principal Name, ungeachtet der Domänenmitgliedschaft verfügen. Diese Methode bietet Skalierbarkeit, die ggf. in Organisationen mit einer großen Anzahl von Domänen erforderlich sind.

- Wenn Sie Netzwerkrichtlinienserver \(NPS\) auf einem anderen Computer als einen Domänencontroller installiert und der NPS-Server eine große Anzahl von authentifizierungsanforderungen pro Sekunde empfangen wird, können Sie NPS-Leistung verbessern, indem Vergrößern der Anzahl gleichzeitiger Authentifizierungen zwischen dem NPS-Server und dem Domänencontroller zulässig. Weitere Informationen finden Sie unter 

## <a name="security-issues"></a>Sicherheitsprobleme

Im folgenden werden die bewährten Methoden zur Reduzierung von Sicherheitsrisiken.

Senden Sie einen NPS-Server remote verwalten, vertrauliche Daten (z. B. gemeinsame geheime Schlüssel oder Kennwörter) nicht über das Netzwerk in Klartext. Es gibt zwei empfohlenen Methoden für die Remoteverwaltung des NPS-Server:

- Verwenden Sie Remote Desktop Services, auf den NPS-Server zugreifen. Wenn Sie Remote Desktop Services verwenden, werden die Daten nicht zwischen Client und Server gesendet. Nur die Benutzeroberfläche des Servers (z. B. der Desktop des Betriebssystems und NPS-Konsolenabbild) wird gesendet, auf dem Remotedesktopdienste-Client mit dem Namen der Remotedesktopverbindung in Windows&reg; 10. Der Client sendet Tastatur- und Mauseingaben, die lokal vom Server verarbeitet wird, die Remote Desktop Services aktiviert wurde. Wenn Remote Desktop Services-Benutzer anmelden, können sie nur ihre eigenen Clientsitzungen anzeigen, die vom Server verwaltet werden und sind unabhängig voneinander. Darüber hinaus bietet der Remotedesktopverbindung 128-Bit-Verschlüsselung zwischen Client und Server.

- Verwenden Sie Internet Protocol Security (IPsec), um vertrauliche Daten zu verschlüsseln. Sie können IPsec verwenden, zum Verschlüsseln der Kommunikation zwischen dem NPS-Server und dem Remoteclientcomputer, die Sie verwenden, um NPS zu verwalten. Sie können den Server Remote zu verwalten, installieren die [Remote Server Administration Tools für Windows 10](https://www.microsoft.com/download/details.aspx?id=45520) auf dem Clientcomputer. Verwenden Sie nach der Installation der Microsoft Management Console (MMC) das NPS-Server-Snap-in auf der Konsole hinzufügen.

>[!IMPORTANT]
>Sie können nur auf die Vollversion von Windows 10 Professional oder Windows 10 Enterprise Remote Server Administration Tools für Windows 10 installieren.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

