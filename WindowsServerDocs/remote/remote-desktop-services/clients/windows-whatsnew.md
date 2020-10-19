---
title: Neuerungen im Microsoft Store-Client
description: Hier erfährst du mehr über aktuelle Änderungen am Remotedesktopclient für Windows Store.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 10/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 63f3ccb3b105bf59033214d426650dd727509095
ms.sourcegitcommit: 45099dfe3682df1e2bc0bd5998594a79cfff16fe
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2020
ms.locfileid: "92079829"
---
# <a name="whats-new-in-the-microsoft-store-client"></a>Neuerungen im Microsoft Store-Client

Der [Microsoft Store-Client](windows.md) wird regelmäßig mit neuen Features und Problembehebungen aktualisiert. Hier findest du die neuesten Updates.

## <a name="updates-for-version-1021534"></a>Updates für Version 10.2.1534

*Veröffentlicht am: 26.08.2020*

- Client wurde neu geschrieben, um dasselbe zugrunde liegende RDP-Kernmodul wie die iOS-, macOS- und Android-Clients zu verwenden.
- Unterstützung für die in Azure Resource Manager integrierte Version von Windows Virtual Desktop wurde hinzugefügt.
- Unterstützung für x64 und ARM64 wurde hinzugefügt.
- Das Seitenbereich-Design wurde auf den Vollbildschirm aktualisiert.
- Unterstützung für den hellen und dunklen Modus wurde hinzugefügt.
- Funktionen zum Abonnieren und Verbinden mit Sovereign Cloudbereitstellungen wurden hinzugefügt.
- Funktionen zum Aktivieren der Sicherung und Wiederherstellung von Arbeitsbereichen (Lesezeichen) in Release to Manufacturing (RTM) wurden hinzugefügt.
- Funktionen zur Verwendung vorhandener Azure Active Directory (Azure AD)-Token während des Abonnementprozesses wurden aktualisiert, damit sich Benutzer nicht mehr so oft anmelden müssen.
- Ein aktualisiertes Abonnement kann jetzt erkennen, ob Sie Windows Virtual Desktop oder Windows Virtual Desktop (klassisch) verwenden.
- Problem beim Kopieren von Dateien auf Remote-PCs wurde behoben.
- Häufig gemeldete Barrierefreiheitsprobleme mit Schaltflächen wurde behoben.
- Eine Begrenzung auf bis zu 20 Sätze von Anmeldeinformationen pro App ist zulässig.

## <a name="updates-for-version-1011215"></a>Updates für Version 10.1.1215

*Veröffentlicht am: 20.04.2020*

- Die Zeichenfolge des Benutzer-Agents für Windows Virtual Desktop wurde aktualisiert.

## <a name="updates-for-version-1011195"></a>Updates für Version 10.1.1195

*Veröffentlicht am: 06.03.2020*

- Die Audioausgabe der Sitzung wird nun auch dann wiedergegeben, wenn die App minimiert oder im Hintergrund angezeigt wird.
- Es wurde ein Problem behoben, durch das die Umschalttasten (FESTSTELLTASTE, NUM-TASTE usw.) des lokalen Computer und des Remote-PCs nicht synchron waren.
- Leistungsverbesserungen auf 64-Bit-Geräten.
- Die Ursache für einen Absturz wurde beseitigt, der auftrat, wenn die App angehalten wurde.

## <a name="updates-for-version-1011107"></a>Updates für Version 10.1.1107

*Veröffentlicht am: 04.09.2019*

- Du kannst nun Dateien zwischen lokalen und entfernten PCs kopieren.
- Du kannst nun deine E-Mail-Adresse verwenden, um auf Remoteressourcen zuzugreifen (falls von deinem Administrator aktiviert).
- Du kannst nun die Benutzerkontozuweisungen für Remoteressourcenfeeds ändern.
- Die App zeigt nun anstelle eines leeren Standardsymbols das richtige Symbol für RDP-Dateien an, die dieser App im Datei-Explorer zugeordnet sind.

## <a name="updates-for-version-1011098"></a>Updates für Version 10.1.1098

*Veröffentlicht am: 15.03.2019*

- Du kannst nun einen Anzeigenamen für Benutzerkonten festlegen und dadurch den gleichen Benutzernamen mit verschiedenen Kennwörtern speichern.
- Beim Hinzufügen von Remoteressourcen kann nun ein vorhandenes Benutzerkonto ausgewählt werden.
- Ein Problem wurde behoben, aufgrund dessen der Client nicht ordnungsgemäß beendet wurde.
- Der Client behandelt sein Aussetzen nun ordnungsgemäß, wenn sekundäre Fenster geöffnet sind.
- Zusätzliche Fehlerbehebungen

## <a name="updates-for-version-1011088"></a>Updates für Version 10.1.1088

*Veröffentlicht am: 06.11.2018*

- Der Anzeigename der Verbindung ist jetzt leichter auffindbar.
- Ein Absturz wurde behoben, der auftrat, wenn während einer aktiven Verbindung das Clientfenster geschlossen wurde.
- Die ausbleibende Reaktion beim Wiederherstellen der Verbindung nach dem Minimieren des Clients wurde korrigiert.
- Desktops können an eine beliebige Position in einer Gruppe gezogen werden.
- Es wird sichergestellt, dass beim Starten einer Verbindung über die Sprungliste bei Bedarf ein separates Fenster geöffnet wird.
- Zusätzliche Fehlerbehebungen

## <a name="updates-for-version-1011060"></a>Updates für Version 10.1.1060

*Veröffentlicht am: 14.09.2018*

- Ein Problem wurde behoben, das dazu führte, dass beim Doppelklicken auf eine Desktopverbindung zwei Sitzungen gestartet wurden.
- Ein Absturz wurde behoben, der beim lokalen Wechseln zwischen virtuellen Desktops auftrat.
- Beim Verschieben einer Sitzung auf einen anderen Monitor wird nun auch der Skalierungsfaktor der Sitzung aktualisiert.
- Behandlung zusätzlicher Systemtasten wie ALT GR.
- Zusätzliche Fehlerbehebungen

## <a name="updates-for-version-1011046"></a>Updates für Version 10.1.1046

*Veröffentlicht am: 20.6.2018*

- Fehlerbehebungen

## <a name="updates-for-version-1011042"></a>Updates für Version 10.1.1042

*Veröffentlicht am: 02.04.2018*

- Updates für die in CVE-2018-0886 beschriebene CredSSP-Encryption Oracle-Abwehr.
- Zusätzliche Fehlerbehebungen
