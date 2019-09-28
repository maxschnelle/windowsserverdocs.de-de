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
ms.date: 09/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4325bd7b33c16d972cac980e17c10bacbfeffd8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387590"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Neuigkeiten im Windows-Desktopclient

Ausführlichere Informationen über den Windows-Desktopclient findest du unter [Erste Schritte mit dem Windows-Desktopclient](windowsdesktop.md). Die neuesten Updates für den Client findest du nachstehend.

## <a name="latest-client-versions"></a>Neueste Clientversionen

Der Client kann für verschiedene [Benutzergruppen](windowsdesktop-admin.md#configure-user-groups) konfiguriert werden. In der folgenden Tabelle sind die aktuellen Versionen aufgelistet, die für jede Benutzergruppe verfügbar sind:

|Benutzergruppe |Version  |
|-----------|---------|
|Public     |1.2.247  |
|Insider    |1.2.247  |

## <a name="updates-for-version-12247"></a>Updates für Version 1.2.247

*Veröffentlicht am: 17.09.2019*

- Es wurde ein Absturz korrigiert, der vorkam, wenn während einer Verbindung eine Authentifizierung vorgenommen wurde.
- Es wurde ein Absturz korrigiert, der vorkam, wenn der Client geschlossen wurde.

## <a name="updates-for-version-12246"></a>Updates für Version 1.2.246

*Veröffentlicht am: 28.08.2019*

- Verbesserung der Reservesprachen für lokalisierte Versionen. (Beispielsweise wird FR-CA ordnungsgemäß in Französisch anstelle von Englisch angezeigt.)
- Beim Entfernen eines Abonnements entfernt der Client nun die gespeicherten Anmeldeinformationen ordnungsgemäß aus der Anmeldeinformationsverwaltung.
- Der Updatevorgang des Clients erfolgt jetzt nach dem Starten ohne Benutzereingriff, und der Client wird nach Abschluss neu gestartet.
- Der-Client kann jetzt unter Windows 10 im S-Modus verwendet werden.
- Es wurde ein Problem behoben, das für Benutzer mit einem Leerzeichen im Benutzernamen zu einem Fehler beim Update führte.
