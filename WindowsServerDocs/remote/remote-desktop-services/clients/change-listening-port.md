---
title: Ändern des Lauschports in Remotedesktop
description: Hier erfährst du, wie du den Lauschport für den Remotedesktopclient änderst.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6b5a48435a99b1bf1392acb6a5764b106984bbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404186"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>Ändern des Lauschports für Remotedesktop auf deinem Computer

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

Wenn du über den Remotedesktopclient eine Verbindung mit einem Computer (entweder einem Windows-Client oder einer Windows Server-Instanz) herstellst, „hört“ die Remotedesktop-Funktion auf deinem Computer die Verbindungsanforderung über einen festgelegten Lauschport (standardmäßig 3389). Du kannst diesen Lauschport auf Windows-Computern durch Anpassen der Registrierung ändern.

1. Starte den Registrierungs-Editor. (Gib „regedit“ ins Suchfeld ein.)
2. Navigieren Sie zum folgenden Registrierungsunterschlüssel: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. Klicke auf **Bearbeiten > Ändern** und anschließend auf **Dezimal**.
4. Gib die neue Portnummer ein, und klicke auf **OK**. 
5. Schließe den Registrierungs-Editor, und starte den Computer neu.

Wenn du das nächste Mal eine Remotedesktopverbindung mit diesem Computer herstellst, musst du den neuen Port eingeben. Stelle bei Verwendung einer Firewall sicher, dass diese so konfiguriert ist, dass sie Verbindungen mit der neuen Portnummer zulässt.
