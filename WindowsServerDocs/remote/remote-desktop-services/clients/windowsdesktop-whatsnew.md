---
title: Neuigkeiten im Windows-Desktopclient
description: Hier erfährst du mehr über aktuelle Änderungen am Remotedesktopclient für Windows-Desktop
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6a8e66398bc61a69250b84101a3cb66f2c8f3548
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567069"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Neuigkeiten im Windows-Desktopclient

Ausführlichere Informationen über den Windows-Desktopclient findest du unter [Erste Schritte mit dem Windows-Desktopclient](windowsdesktop.md). Die neuesten Updates für den Client findest du nachstehend.

## <a name="latest-client-versions"></a>Neueste Clientversionen

Der Client kann für verschiedene [Benutzergruppen](windowsdesktop-admin.md#configure-user-groups) konfiguriert werden. In der folgenden Tabelle sind die aktuellen Versionen aufgelistet, die für jede Benutzergruppe verfügbar sind:

|Benutzergruppe |Version  |
|-----------|---------|
|Public     |1.2.247  |
|Insider    |1.2.428  |

## <a name="updates-for-version-12428"></a>Updates für Version 1.2.428

*Veröffentlicht am: 31.10.2019*

- Vorschauversionen der 32-Bit-Version und der ARM64-Version des Clients sind nun verfügbar.
- Der Client speichert jetzt alle an der Verbindungsleiste vorgenommenen Änderungen (z.B. Position, Größe und angehefteter Zustand), und wendet diese Änderungen sitzungsübergreifend an.
- Aktualisierte Dialogfelder für Gatewayinformationen und Verbindungsstatus.
- Es wurde ein Problem behoben, das dazu führte, dass beim Verbindungsversuch nach Ablauf des Azure Active Directory-Token gleichzeitig zwei Mal Anmeldeinformationen angefordert wurden.
- Unter Windows 7 werden die Benutzer nun ordnungsgemäß zur Eingabe von Anmeldeinformationen aufgefordert, wenn sie Anmeldeinformationen gespeichert hatten und der Server dies nicht zulässt.
- Die Azure Active Directory-Eingabeaufforderung wird jetzt beim Wiederherstellen der Verbindung vor dem Verbindungsfenster angezeigt.
- Elemente, die an die Taskleiste angeheftet wurden, werden jetzt während einer Feedaktualisierung aktualisiert.
- Verbessertes Scrollen im Connection Center bei Verwendung der Toucheingabe.
- Die leere Zeile wurde aus dem Dropdownmenü „Auflösung“ entfernt.
- Unnötige Einträge in der Windows-Anmeldeinformationsverwaltung wurden entfernt.
- Beim Beenden des Vollbildmodus erfolgt nun eine ordnungsgemäße Größenanpassung der Desktopsitzungen.
- Das Dialogfeld zum Trennen der RemoteApp wird jetzt im Vordergrund angezeigt, wenn eine Sitzung aus dem Energiesparmodus wieder aufgenommen wird.
- Barrierefreiheitsprobleme, z.B. bei der Tastaturnavigation, wurden behoben.

## <a name="updates-for-version-12247"></a>Updates für Version 1.2.247

*Veröffentlicht am: 17.09.2019*

- Es wurde ein Absturz korrigiert, der vorkam, wenn während einer Verbindung eine Authentifizierung vorgenommen wurde.
- Es wurde ein Absturz korrigiert, der vorkam, wenn der Client geschlossen wurde.

## <a name="updates-for-version-12246"></a>Updates für Version 1.2.246

*Veröffentlicht am: 28.08.2019*

- Verbesserung der Reservesprachen für lokalisierte Versionen. (Beispielsweise wird FR-CA ordnungsgemäß in Französisch anstelle von Englisch angezeigt.)
- Beim Entfernen eines Abonnements entfernt der Client nun die gespeicherten Anmeldeinformationen ordnungsgemäß aus der Anmeldeinformationsverwaltung.
- Der Updatevorgang des Clients erfolgt jetzt nach dem Starten ohne Benutzereingriff, und der Client wird nach Abschluss neu gestartet.
- Der Client kann jetzt unter Windows 10 im S-Modus verwendet werden.
- Es wurde ein Problem behoben, das für Benutzer mit einem Leerzeichen im Benutzernamen zu einem Fehler beim Update führte.
