---
title: Ändern des Lauschports in Remotedesktop
description: Hier erfährst du, wie du den Lauschport für den Remotedesktopclient änderst.
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c28fbc7e453121e0a885e390f4b8435023a007e
ms.sourcegitcommit: 67a486b4fb3937a457eb00d21a2e33b753489fd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88149544"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>Ändern des Lauschports für Remotedesktop auf deinem Computer

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

Wenn du über den Remotedesktopclient eine Verbindung mit einem Computer (entweder einem Windows-Client oder einer Windows Server-Instanz) herstellst, „hört“ die Remotedesktop-Funktion auf deinem Computer die Verbindungsanforderung über einen festgelegten Lauschport (standardmäßig 3389). Du kannst diesen Lauschport auf Windows-Computern durch Anpassen der Registrierung ändern.

1. Starte den Registrierungs-Editor. (Gib „regedit“ ins Suchfeld ein.)
2. Navigieren Sie zum folgenden Registrierungsunterschlüssel: **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp**
3. **PortNumber** suchen
4. Klicke auf **Bearbeiten > Ändern** und anschließend auf **Dezimal**.
5. Gib die neue Portnummer ein, und klicke auf **OK**. 
6. Schließe den Registrierungs-Editor, und starte den Computer neu.

Wenn du das nächste Mal eine Remotedesktopverbindung mit diesem Computer herstellst, musst du den neuen Port eingeben. Stelle bei Verwendung einer Firewall sicher, dass diese so konfiguriert ist, dass sie Verbindungen mit der neuen Portnummer zulässt.
