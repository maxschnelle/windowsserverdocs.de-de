---
title: 'Bewährte Methoden: Netzwerkrichtlinienserver'
description: Dieses Thema enthält bewährte Methoden für die Bereitstellung und Verwaltung des Netzwerk Richtlinien Servers in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a0bfa96e5fb3b562c23904ebef096d06e0c2d3c8
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546542"
---
# <a name="network-policy-server-best-practices"></a>Bewährte Methoden: Netzwerkrichtlinienserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie mehr über bewährte Methoden für die Bereitstellung und Verwaltung von Netzwerk \(Richtlinien Server\)-NPS.

Die folgenden Abschnitte enthalten bewährte Methoden für verschiedene Aspekte ihrer NPS-Bereitstellung.

## <a name="accounting"></a>Kontoführung

Im folgenden finden Sie die bewährten Methoden für die NPS-Protokollierung.

Es gibt zwei Arten von Buchhaltung oder Protokollierung in NPS:

- Ereignisprotokollierung für NPS. Sie können die Ereignisprotokollierung verwenden, um NPS-Ereignisse in den System-und Sicherheits Ereignisprotokollen aufzuzeichnen. Dies wird hauptsächlich für die Überwachung und Problembehandlung von Verbindungs versuchen verwendet.

- Protokollieren von Benutzer Authentifizierungs-und Buchhaltungs Anforderungen. Sie können Benutzer Authentifizierungs-und Buchhaltungs Anforderungen protokollieren, um Dateien im Textformat oder im Datenbankformat zu protokollieren, oder Sie können sich in einer gespeicherten Prozedur in einer SQL Server 2000-Datenbank anmelden. Die Anforderungs Protokollierung wird hauptsächlich für Verbindungs Analyse und Abrechnungszwecke verwendet und ist auch als Sicherheitsuntersuchung nützlich, sodass Sie die Aktivitäten eines Angreifers nachverfolgen können.

So nutzen Sie die NPS-Protokollierung am effektivsten:

- Aktivieren Sie die \(Protokollierung zunächst\) für die Authentifizierungs-und Buchhaltungsdaten Sätze. Ändern Sie diese Auswahl, nachdem Sie festgelegt haben, was für Ihre Umgebung geeignet ist.

- Stellen Sie sicher, dass die Ereignisprotokollierung mit einer Kapazität konfiguriert ist, die für die Beibehaltung der Protokolle ausreicht.

- Sichern Sie alle Protokolldateien in regelmäßigen Abständen, da Sie nicht neu erstellt werden können, wenn Sie beschädigt oder gelöscht werden.

- Verwenden Sie das RADIUS-Klassen Attribut, um die Nutzung zu verfolgen und die Identifizierung der Abteilung oder des Benutzers zu vereinfachen, die für die Nutzung verantwortlich sind. Obwohl das automatisch generierte Klassen Attribut für jede Anforderung eindeutig ist, sind möglicherweise doppelte Datensätze in Fällen vorhanden, in denen die Antwort an den Zugriffs Server verloren geht und die Anforderung erneut gesendet wird. Sie müssen möglicherweise doppelte Anforderungen aus Ihren Protokollen löschen, um die Nutzung genau zu verfolgen.

- Wenn Ihre Netzwerk Zugriffs Server und RADIUS-Proxy Server in regelmäßigen Abständen fiktive Verbindungs Anforderungs Nachrichten an NPS senden, um zu überprüfen, ob der NPS Online ist, verwenden Sie die Registrierungs Einstellung **Ping User-Name** . Diese Einstellung konfiguriert NPS so, dass diese falschen Verbindungsanforderungen automatisch abgelehnt werden, ohne Sie zu verarbeiten. Außerdem zeichnet NPS keine Transaktionen auf, die den fiktiven Benutzernamen in Protokolldateien einschließen, wodurch das Ereignisprotokoll leichter interpretiert werden kann.

- Deaktivieren der NAS-Benachrichtigungs Weiterleitung Sie können die Weiterleitung von Nachrichten zum Starten und Abbrechen von Netzwerk Zugriffs Servern (nass) an Mitglieder einer Remote-RADIUS-Server Gruppe deaktivieren, die in NPS konfiguriert ist. Weitere Informationen finden Sie unter [Deaktivieren der NAS-Benachrichtigungs Weiterleitung](nps-disable-nas-notifications.md).

Weitere Informationen finden Sie unter [Konfigurieren der Netzwerk Richtlinien Server](nps-accounting-configure.md)-Kontoführung.

- Zum Bereitstellen von Failover und Redundanz mit SQL Server Protokollierung platzieren Sie zwei Computer, auf denen SQL Server ausgeführt wird, in verschiedenen Subnetzen Mit dem **Assistenten zum Erstellen einer Veröffentlichung** von SQL Server können Sie die Daten Bank Replikation zwischen den beiden Servern einrichten. Weitere Informationen finden Sie unter [SQL Server technische Dokumentation](https://msdn.microsoft.com/library/ms130214.aspx) und [SQL Server-Replikation](https://msdn.microsoft.com/library/ms151198.aspx).

## <a name="authentication"></a>Authentifizierung

Im folgenden finden Sie die bewährten Methoden für die Authentifizierung.

- Verwenden Sie Zertifikat basierte Authentifizierungsmethoden, wie z. b. das \(Protected Extensible Authentication Protocol PEAP \(\) und das\) Extensible Authentication Protocol EAP für eine starke Authentifizierung. Verwenden Sie keine Authentifizierungsmethoden für das Kennwort, da Sie für eine Vielzahl von Angriffen anfällig sind und nicht sicher sind. Zur sicheren drahtlosen Authentifizierung wird die Verwendung\-von\-"Peer-MS CHAP v2" empfohlen, da der NPS seine Identität für drahtlose Clients mithilfe eines Serverzertifikats nach weist, während die Benutzer ihre Identität mit Ihrem Benutzernamen und Kennwort belegen.  Weitere Informationen zur Verwendung von NPS in Ihrer drahtlosen Bereitstellung finden Sie unter Bereitstellen von Kenn [Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).
- Stellen Sie Ihre eigene Zertifizierungs \(stellen\) -Zertifizierungs&reg; Stelle mit \(Active Directory AD\) CS-Zertifikat Diensten bereit, wenn Sie starke Zertifikat basierte Authentifizierungsmethoden wie PEAP und EAP verwenden, die erfordert die Verwendung eines Serverzertifikats auf dem NPSS. Sie können auch die Zertifizierungsstelle zum Registrieren von Computer Zertifikaten und Benutzer Zertifikaten verwenden. Weitere Informationen zum Bereitstellen von Server Zertifikaten für NPS und RAS-Server finden Sie unter Bereitstellen [von Server Zertifikaten für drahtlose und drahtlose 802.1 x](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)-bereit Stellungen.

> [!IMPORTANT]
> Der Netzwerk Richtlinien Server (Network Policy Server, NPS) unterstützt die Verwendung der erweiterten ASCII-Zeichen in Kenn Wörtern nicht.

## <a name="client-computer-configuration"></a>Client Computerkonfiguration

Im folgenden finden Sie die bewährten Methoden für die Konfiguration von Client Computern.

- Konfigurieren Sie alle Domänen Mitglieds-802.1 x-Client Computer mit Gruppenrichtlinie automatisch. Weitere Informationen finden Sie im Abschnitt "Konfigurieren von Drahtlos Netzwerk Richtlinien (IEEE 802,11)" im Thema [drahtlos Zugriffs Bereitstellung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies).

## <a name="installation-suggestions"></a>Installations Vorschläge

Im folgenden finden Sie die bewährten Methoden für die Installation von NPS.

- Vor der Installation von NPS installieren und testen Sie alle Netzwerk Zugriffs Server mithilfe lokaler Authentifizierungsmethoden, bevor Sie Sie als RADIUS-Clients in NPS konfigurieren.

- Nachdem Sie NPS installiert und konfiguriert haben, speichern Sie die Konfiguration, indem Sie den Windows PowerShell-Befehl [Export-npsconfiguration](https://technet.microsoft.com/library/jj872749.aspx)verwenden. Speichern Sie die NPS-Konfiguration bei jeder Neukonfiguration des NPS mit diesem Befehl.

>[!CAUTION]
>- Die exportierte NPS-Konfigurationsdatei enthält unverschlüsselte gemeinsame geheime Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remote Server Gruppen. Stellen Sie daher sicher, dass Sie die Datei an einem sicheren Speicherort speichern.
>- Der Exportprozess umfasst keine Protokollierungs Einstellungen für Microsoft SQL Server in der exportierten Datei. Wenn Sie die exportierte Datei in ein anderes NPS importieren, müssen Sie SQL Server Protokollierung auf dem neuen Server manuell konfigurieren.

## <a name="performance-tuning-nps"></a>Leistungsoptimierung (NPS)

Im folgenden werden die bewährten Methoden für die Leistungsoptimierung von NPS beschrieben.

- Installieren Sie NPS auf einem Domänen Controller, um die Antwortzeiten für die NPS-Authentifizierung und-Autorisierung zu optimieren und den Netzwerkverkehr

- Wenn universelle Prinzipal \(Namen\) -UPNs oder Windows Server 2008-und Windows Server 2003-Domänen verwendet werden, verwendet NPS den globalen Katalog, um Benutzer zu authentifizieren. Um die benötigte Zeit zu minimieren, installieren Sie NPS entweder auf einem globalen Katalogserver oder auf einem Server, der sich im gleichen Subnetz wie der globale Katalogserver befindet.

- Wenn Sie Remote-RADIUS-Server Gruppen konfiguriert haben und Sie in NPS-Verbindungs Anforderungs Richtlinien das Kontrollkästchen **Aufzeichnen von Buchhaltungsinformationen auf den Servern in der folgenden Remote-RADIUS-Server Gruppe** deaktivieren, werden diese Gruppen weiterhin Netzwerk Zugriff gesendet. Server \(-\) NAS startet und beendet Benachrichtigungs Meldungen. Dadurch wird unnötiger Netzwerk Datenverkehr erstellt. Deaktivieren Sie die NAS-Benachrichtigungs Weiterleitung für einzelne Server in jeder RADIUS-Remote Server Gruppe, indem Sie das Kontrollkästchen **Netzwerkstart und-Benachrichtigungen an diesen Server weiterleiten** deaktivieren, um diesen Datenverkehr auszuschließen.

## <a name="using-nps-in-large-organizations"></a>Verwenden von NPS in großen Organisationen

Im folgenden finden Sie die bewährten Methoden für die Verwendung von NPS in großen Organisationen.

- Wenn Sie Netzwerk Richtlinien verwenden, um den Zugriff für alle außer bestimmte Gruppen einzuschränken, erstellen Sie eine universelle Gruppe für alle Benutzer, für die Sie Zugriff gewähren möchten, und erstellen Sie dann eine Netzwerk Richtlinie, die Zugriff für diese universelle Gruppe gewährt. Fügen Sie nicht alle Benutzer direkt in die universelle Gruppe ein, insbesondere, wenn Sie über eine große Anzahl von Benutzern in Ihrem Netzwerk verfügen. Erstellen Sie stattdessen separate Gruppen, die Mitglieder der universellen Gruppe sind, und fügen Sie diesen Gruppen Benutzer hinzu.

- Verwenden Sie einen Benutzer Prinzipal Namen, um nach Möglichkeit auf Benutzer zu verweisen. Ein Benutzer kann unabhängig von der Domänen Mitgliedschaft denselben Benutzer Prinzipal Namen haben. Diese Vorgehensweise bietet Skalierbarkeit, die möglicherweise in Organisationen mit einer großen Anzahl von Domänen erforderlich ist.

- Wenn Sie den Netzwerk Richtlinien Server \(-NPS\) auf einem anderen Computer als einem Domänen Controller installiert haben und der NPS eine große Anzahl von Authentifizierungsanforderungen pro Sekunde empfängt, können Sie die NPS-Leistung verbessern, indem Sie die Anzahl der gleichzeitige Authentifizierungen zwischen dem NPS und dem Domänen Controller sind zulässig. Weitere Informationen finden Sie unter 

## <a name="security-issues"></a>Sicherheitsprobleme

Im folgenden finden Sie die bewährten Methoden zum Reduzieren von Sicherheitsproblemen.

Wenn Sie ein NPS remote verwalten, sollten Sie keine sensiblen oder vertraulichen Daten (z. b. gemeinsame geheime Schlüssel oder Kenn Wörter) über das Netzwerk im Klartext senden. Es gibt zwei empfohlene Methoden für die Remote Verwaltung von NPSS:

- Verwenden Sie Remotedesktopdienste, um auf den NPS zuzugreifen. Wenn Sie Remotedesktopdienste verwenden, werden keine Daten zwischen dem Client und dem Server gesendet. Nur die Benutzeroberfläche des Servers (z. b. das Betriebssystem Desktop-und NPS-Konsolen Image) wird an den Remotedesktopdienste-Client gesendet, der in Windows&reg; 10 Remotedesktopverbindung heißt. Der Client sendet Tastatur-und Maus Eingaben, die lokal von dem Server verarbeitet werden, auf dem Remotedesktopdienste aktiviert ist. Wenn sich Remotedesktopdienste Benutzer anmelden, können Sie nur die einzelnen Client Sitzungen anzeigen, die vom Server verwaltet werden und voneinander unabhängig sind. Außerdem bietet Remotedesktopverbindung eine 128-Bit-Verschlüsselung zwischen Client und Server.

- Verwenden Sie IPSec (Internet Protocol Security), um vertrauliche Daten zu verschlüsseln. Sie können IPSec verwenden, um die Kommunikation zwischen dem NPS und dem Remote Client Computer zu verschlüsseln, den Sie zum Verwalten von NPS verwenden. Wenn Sie den Server remote verwalten möchten, können Sie die [Remoteserver-Verwaltungstools für Windows 10](https://www.microsoft.com/download/details.aspx?id=45520) auf dem Client Computer installieren. Verwenden Sie nach der Installation die Microsoft Management Console (MMC), um der-Konsole das NPS-Snap-in hinzuzufügen.

>[!IMPORTANT]
>Sie können Remoteserver-Verwaltungstools für Windows 10 nur für die Vollversion von Windows 10 Professional oder Windows 10 Enterprise installieren.

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).

