---
title: Ändern des Abhörports Remotedesktop
description: Enthält Informationen zum Ändern des Abhörports für Remotedesktop-Client.
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
ms.openlocfilehash: b70479b644f4984c93136d6493483c372703244d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297320"
---
# Ändern des Abhörports für Remotedesktop auf Ihrem computer

>Gilt für: Windows 10, Windows 8.1, Windows 8, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, Windows Server 2008 R2

Wenn Sie auf einen Computer (Windows-Client oder Windows Server) über den Remotedesktop-Client eine Verbindung herstellen, das Remotedesktop-Feature auf Ihrem Computer "hört" die Anforderung der Verbindung über einen definierten Abhörports (Port 3389 standardmäßig). Sie können diese Abhörports auf Windows-Computern durch Ändern der Registrierung ändern.

1. Starten Sie den Registrierungs-Editor. (Geben Sie Regedit in das Suchfeld ein.)
2. Navigieren Sie zu den folgenden Registrierungsunterschlüssel: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. Klicken Sie auf **Bearbeiten > ändern**, und klicken Sie dann auf **Decimal**.
4. Geben Sie die neue Portnummer ein, und klicken Sie dann auf **OK**. 
5. Schließen Sie den Registrierungs-Editor, und starten Sie Ihren Computer neu.

Das nächste Mal, das Sie mithilfe der Remotedesktop-Verbindungs mit diesem Computer herstellen, müssen Sie den neuen Port eingeben. Wenn Sie eine Firewall verwenden, stellen Sie sicher, Ihre Firewall zum Zulassen von Verbindungen, die neue Portnummer konfigurieren.
