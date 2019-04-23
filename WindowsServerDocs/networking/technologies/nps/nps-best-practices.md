---
title: 'Bewährte Methoden: Netzwerkrichtlinienserver'
description: Dieses Thema enthält bewährte Methoden für die Bereitstellung und Verwaltung von Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6cbd606edec06a80767ee997ef6a1397b66b7843
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834231"
---
# <a name="network-policy-server-best-practices"></a>Bewährte Methoden: Netzwerkrichtlinienserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mithilfe dieses Themas können Sie Informationen zu bewährten Methoden zum Bereitstellen und Verwalten des Netzwerkrichtlinienservers \(NPS\).

Die folgenden Abschnitte enthalten bewährte Methoden für verschiedene Aspekte der NPS-Bereitstellung.

## <a name="accounting"></a>Kontoführung

Im folgenden werden die bewährten Methoden für NPS-Protokollierung.

Es gibt zwei Arten von accounting oder Protokollierung im NPS aus:

- Ereignisprotokollierung für den NPS. Sie können die ereignisprotokollierung NPS Ereignisse in die Ereignisprotokolle System und Sicherheit. Hiermit wird in erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen.

- Protokollieren der Benutzerauthentifizierung und kontoführungsanforderungen. Melden Sie Authentifizierung und-Kontoführung benutzeranforderungen in Protokolldateien im Textformat oder Datenbankformat oder Sie können an eine gespeicherte Prozedur in einer SQL Server 2000-Datenbank anmelden. Fordern Sie die Protokollierung wird in erster Linie für verbindungszwecke für Analyse und die Abrechnung verwendet und kann auch eine Untersuchung Sicherheitstool, bietet Ihnen eine Methode zum Aufspüren der Aktivitäts von eines Angreifers.

So erstellen Sie möglichst effiziente Nutzung der NPS-Protokollierung

- Aktivieren der Protokollierung \(anfänglich\) für Authentifizierung und Kontoführung Datensätze. Ändern Sie die Auswahl, nachdem Sie ermittelt haben, was für Ihre Umgebung geeignet ist.

- Stellen Sie sicher, dass die ereignisprotokollierung mit einer Kapazität konfiguriert ist, die ausreicht, um Ihre Protokolle zu verwalten.

- Sichern Sie alle Protokolldateien in regelmäßigen Abständen, da sie neu erstellt werden können, wenn sie beschädigt oder gelöscht werden.

- Verwenden Sie das Attribut der RADIUS-Klasse, um sowohl Nachverfolgen der Nutzung und vereinfachen die Identifikation von der Abteilung oder einem Benutzer, für die Nutzung zu berechnen. Zwar das automatisch generierte Klasse-Attribut für jede Anforderung eindeutig ist, können doppelte Datensätze vorhanden sein in Fällen, in dem die Antwort an den Zugriffsserver verloren gegangen ist, und die Anforderung erneut gesendet wird. Sie müssen möglicherweise doppelte Anforderungen Ihre Protokolle genau Nachverfolgen der Nutzung zu löschen.

- Wenn Ihre Netzwerkzugriffsserver und RADIUS-Proxy-Server senden in regelmäßigen Abständen fiktive Verbindung Anforderungsnachrichten an NPS, stellen Sie sicher, dass der NPS online ist, verwenden Sie die **Pingen Benutzername** registrierungseinstellung. Diese Einstellung konfiguriert NPS, um diese "false" verbindungsanforderungen automatisch ablehnen, ohne sie zu verarbeiten. Darüber hinaus zeichnet NPS nicht Transaktionen im Zusammenhang mit der fiktive Benutzername in der alle Protokolldateien im Ereignisprotokoll leichter interpretiert werden.

- Deaktivieren Sie die Weiterleitung von NAS-Benachrichtigung. Sie können die Weiterleitung von Start deaktivieren aus, und Stop-Nachrichten von Netzwerkzugriffsservern (NAS) für Mitglieder von einem RADIUS-Remoteserver gruppieren, auf dem Netzwerkrichtlinienserver so konfiguriert ist. Weitere Informationen finden Sie unter [deaktivieren NAS Benachrichtigung Weiterleitung](nps-disable-nas-notifications.md).

Weitere Informationen finden Sie unter [konfigurieren Network Policy Server Accounting](nps-accounting-configure.md).

- Um Failover- und redundanzmodelle mit SQL Server-Protokollierung bereitzustellen, platzieren Sie zwei Computer mit SQL Server in unterschiedlichen Subnetzen. Verwenden Sie den SQL Server **Veröffentlichungserstellungs-Assistenten die** Datenbankreplikation zwischen den beiden Servern einrichten. Weitere Informationen finden Sie unter [technische Dokumentation zu SQL Server](https://msdn.microsoft.com/library/ms130214.aspx) und [SQL Server-Replikation](https://msdn.microsoft.com/library/ms151198.aspx).

## <a name="authentication"></a>Authentifizierung

Im folgenden werden die bewährten Methoden für die Authentifizierung.

- Verwenden Sie die zertifikatbasierte Authentifizierungsmethoden, z. B. Protected Extensible Authentication Protocol \(PEAP\) und Extensible Authentication Protocol \(EAP\) für eine sichere Authentifizierung. Verwenden Sie nicht nur das Kennwort-Authentifizierungsmethoden aus, da sie eine Vielzahl von Angriffe anfällig und sind nicht sicher. Für sichere drahtlose Authentifizierung mithilfe von PEAP\-MS\-CHAP-v2 wird empfohlen, da der NPS erweist sich seine Identität für drahtlose Clients als verwenden Benutzer ihre Identität mit ihren Benutzernamen und Kennwort bestätigen ein Serverzertifikat.  Weitere Informationen zur Verwendung von NPS in der drahtlosen Bereitstellung finden Sie unter [Bereitstellung Kennwort-basierten Drahtloszugriff mit 802.1X-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).
- Bereitstellen Ihrer eigenen Zertifizierungsstelle \(Zertifizierungsstelle\) in Active Directory&reg; Zertifikatdienste \(AD CS\) bei Verwendung der starken zertifikatbasierte Authentifizierungsmethoden, z. B. PEAP und EAP, erfordern Sie die Verwendung eines Serverzertifikats auf NPSs. Sie können auch die Zertifizierungsstelle verwenden, zum Registrieren von Computerzertifikaten und Benutzerzertifikate. Weitere Informationen zum Bereitstellen von Serverzertifikaten für NPS- und RAS-Server finden Sie unter [Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="client-computer-configuration"></a>Konfiguration von Clientcomputern

Im folgenden werden die bewährten Methoden für die Konfiguration von Clientcomputern.

- Konfigurieren Sie alle Ihre Domänenmitglieds 802.1 X-Client-Computer automatisch mithilfe der Gruppenrichtlinie. Weitere Informationen finden Sie im Abschnitt "Konfigurieren Wireless Network (IEEE 802.11) Policies" im Thema [drahtlosen Zugriff Bereitstellung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies).

## <a name="installation-suggestions"></a>Empfehlungen für Installation

Im folgenden werden die bewährten Methoden für die Installation von NPS.

- Klicken Sie vor der Installation von NPS ein, installieren Sie und Testen Sie alle Ihre Netzwerkzugriffsserver, die mit lokalen Authentifizierungsmethoden aus, bevor Sie sie als RADIUS-Clients in NPS konfigurieren.

- Nachdem Sie installieren und Konfigurieren von NPS, speichern Sie die Konfiguration mithilfe des Windows PowerShell-Befehls [Export-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx). Speichern Sie die NPS-Konfiguration mit dem folgenden Befehl, der jedes Mal neu konfigurieren Sie den NPS.

>[!CAUTION]
>- Die exportierte NPS-Konfigurationsdatei enthält die unverschlüsselte gemeinsamen geheimen Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remoteservergruppen. Aus diesem Grund sicher, dass Sie die Datei an einem sicheren Ort speichern.
>- Der Exportvorgang umfasst keine protokollierungseinstellungen für Microsoft SQL Server in der exportierten Datei. Wenn Sie die exportierte Datei an einem anderen NPS importieren, müssen Sie manuell SQL Server-Protokollierung auf dem neuen Server konfigurieren.

## <a name="performance-tuning-nps"></a>NPS die Optimierung der Leistung

Im folgenden werden die bewährten Methoden für NPS die Optimierung der Leistung.

- Um NPS-Authentifizierung und Autorisierung Antwortzeiten zu optimieren und den Netzwerkverkehr zu reduzieren, installieren Sie NPS auf einem Domänencontroller aus.

- Wenn universal principal Name \(UPNs\) oder Windows Server 2008 und Windows Server 2003-Domänen werden verwendet, NPS mithilfe des globalen Katalogs zum Authentifizieren von Benutzern. Um die Zeit zu minimieren, dauert es dies vornehmen können, installieren Sie NPS auf einem globalen Katalogserver oder ein Server, der auf dem gleichen Subnetz wie der globale Katalogserver ist.

- Wenn Sie die RADIUS-Remoteservergruppen konfiguriert haben, und NPS Verbindungsanforderungsrichtlinien, deaktivieren Sie die **Aufzeichnen von Informationen zur Kontoführung auf den Servern in der folgenden RADIUS-Remoteservergruppe** Kontrollkästchen Diese Gruppen sind immer noch gesendet von Netzwerkzugriffsserver \(NAS\) starten und Beenden von benachrichtigungsmeldungen. Dadurch wird die unnötigen Netzwerkdatenverkehr erstellt. Um diesen Datenverkehr zu vermeiden, deaktivieren Sie NAS-Notification-Weiterleitung für einzelne Server an jeden remote-RADIUS-Servergruppe durch Deaktivieren der **weiterleiten Netzwerk starten und Beenden von Benachrichtigungen an diesen Server** Kontrollkästchen.

## <a name="using-nps-in-large-organizations"></a>Mit dem Netzwerkrichtlinienserver in großen Organisationen

Im folgenden werden die bewährten Methoden für die Verwendung von NPS in großen Organisationen.

- Bei Netzwerkrichtlinien Verwendung zum Einschränken des Zugriffs für bestimmte Gruppen, erstellen eine universelle Gruppe für alle Benutzer für den Sie den Zugriff zulassen möchten, und klicken Sie dann erstellen Sie eine Netzwerkrichtlinie, die Zugriff für diese universelle Gruppe. Fügen Sie alle Ihre Benutzer nicht direkt in der Gruppe "universelle" fest, insbesondere dann, wenn Sie eine große Anzahl von ihnen in Ihrem Netzwerk haben. Erstellen Sie stattdessen separate Gruppen, die die universelle Gruppe angehören, und diesen Gruppen Benutzer hinzufügen.

- Verwenden Sie zum Verweisen auf Benutzer, die nach Möglichkeit einen Benutzerprinzipalnamen. Ein Benutzer kann den gleichen Benutzerprinzipalnamen ungeachtet der Domänenmitgliedschaft verfügen. Diese Vorgehensweise bietet Skalierbarkeit, die in Organisationen mit einer großen Anzahl von Domänen erforderlich sein könnten.

- Bei der Installation des Netzwerkrichtlinienservers \(NPS\) auf einem anderen Computer als eine Domäne einer Controller und dem NPS ist eine große Anzahl von authentifizierungsanforderungen pro Sekunde empfangen, können Sie NPS-Leistung durch Erhöhen der Anzahl der verbessern gleichzeitiger Authentifizierungen, die zwischen den NPS- und dem Domänencontroller zulässig. Weitere Informationen finden Sie unter 

## <a name="security-issues"></a>Sicherheitsprobleme

Im folgenden werden die bewährten Methoden zum Reduzieren von Sicherheitsproblemen.

Senden Sie einen NPS remote verwalten, sensible oder vertrauliche Daten (z. B. gemeinsame geheime Schlüssel oder Kennwörter) nicht über das Netzwerk als nur-Text. Es gibt zwei empfohlene Methoden für die Remoteverwaltung von NPSs:

- Verwenden Sie Remote Desktop Services, um den NPS zuzugreifen. Wenn Sie Remote Desktop Services verwenden, werden die Daten nicht zwischen Client und Server gesendet. Nur die Benutzeroberfläche des Servers (z. B. der Desktop des Betriebssystems und eine Abbildung der NPS-Konsole) wird an den Client Remote Desktop Services, mit dem Namen des Remotedesktop-Verbindung in Windows gesendet&reg; 10. Der Client sendet Tastatur- und Mauseingaben, die lokal vom Server verarbeitet wird, die Remote Desktop Services aktiviert ist. Wenn Remote Desktop Services-Benutzer anmelden, können sie nur ihre eigenen Clientsitzungen, anzeigen, die vom Server verwaltet werden und unabhängig voneinander sind. Darüber hinaus bietet die Remotedesktopverbindung 128-Bit-Verschlüsselung zwischen Client und Server.

- Verwenden Sie Internet Protocol Security (IPsec), um vertrauliche Daten zu verschlüsseln. Sie können IPsec verwenden, zum Verschlüsseln der Kommunikation zwischen den NPS- und dem remote-Client-Computer, den Sie verwenden, um NPS zu verwalten. Sie können den Server Remote zu verwalten, installieren die [Remote Server Administration Tools für Windows 10](https://www.microsoft.com/download/details.aspx?id=45520) auf dem Clientcomputer. Verwenden Sie nach der Installation der Microsoft Management Console (MMC), um die NPS-Snap-in zur Konsole hinzufügen.

>[!IMPORTANT]
>Sie können Remote Server Administration Tools für Windows 10 nur auf die Vollversion von Windows 10 Professional oder Windows 10 Enterprise installieren.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

