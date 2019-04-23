---
title: Ändern des Abhörsockets im Remotedesktop
description: Informationen Sie zum Ändern des Abhörports für Remotedesktop-Client.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5bf90010143e742f7a0c9b5c262be01e6ccf8c5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882721"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>Ändern Sie lauschport für den für den Remotedesktop auf dem Computer.

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

Wenn Sie auf einem Computer (Windows-Client oder Windows Server) über den Remotedesktop-Client verbinden, die Remotedesktop-Funktion auf dem Computer "hört" die verbindungsanforderung an einen definierten-Überwachungsport (standardmäßig 3389). Sie können diese-lauschport auf Windows-Computer durch Ändern der Registrierung ändern.

1. Starten Sie den Registrierungs-Editor. (Geben Sie "regedit" im Feld Suchen.)
2. Navigieren Sie zum folgenden Registrierungsunterschlüssel: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. Klicken Sie auf **Bearbeiten > ändern**, und klicken Sie dann auf **Decimal**.
4. Geben Sie die neue Portnummer ein, und klicken Sie dann auf **OK**. 
5. Schließen Sie den Registrierungs-Editor, und starten Sie den Computer neu.

Das nächste Mal, die, das Sie mit diesem Computer herstellen, mithilfe der Remotedesktopverbindung verwenden, müssen Sie den neuen Port eingeben. Wenn Sie eine Firewall verwenden, stellen Sie sicher, dass die Firewall zum Zulassen von Verbindungen, die neue Portnummer konfigurieren.
