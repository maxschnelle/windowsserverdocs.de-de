---
title: Einschränken des Benutzerzugriffs auf dem server
description: Erfahren Sie, wie Sie gewähren oder Verweigern des Zugriffs auf MultiPoint-Dienste für Benutzer und Gruppen
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 1466e19152847a6c7d88f77162c50ec73a5a7d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830811"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Beschränken Sie Benutzer mit Zugriff auf den Multipoint-server
Ob Sie MultiPoint-Server mit Active Directory-Domäne verknüpfen, oder Sie lokale Benutzerkonten verwenden, haben alle Benutzer Zugriff auf MultiPoint-Server standardmäßig. Bevor Sie Benutzer auf die Stationen in Ihrem MultiPoint Services-Umgebung anmelden können, sollten Sie mit dem Server den Zugriff einschränken.  
  
Jeder Benutzer in der Gruppe Remotedesktopbenutzer kann an MultiPoint Server anmelden. Der Benutzer wird standardmäßig die Gruppe "Jeder" ist ein Mitglied der Gruppe Remotedesktopbenutzer, und daher alle lokalen Benutzer und Domänenbenutzer kann melden Sie sich an den MultiPoint-Server. Entfernen Sie zum Einschränken des Zugriffs mit MultiPoint-Server die jeder Benutzer aus der Gruppe Remotedesktopbenutzer, und fügen Sie dann bestimmte Benutzer oder Gruppen der Remotedesktopbenutzer-Gruppe.  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>Hinzufügen oder Entfernen von Benutzern oder Gruppen aus, die die Remotedesktopbenutzer-Gruppe  
  
1.  Von der **starten** öffnen **Computerverwaltung**.  
  
2.  In der Konsolenstruktur unter **lokale Benutzer und Gruppen**, klicken Sie auf **Gruppen**.  
  
3.  Doppelklick **Remote Desktop Users**, und befolgen Sie die Anweisungen zum Hinzufügen oder Entfernen von Benutzern.  
  
    -   Um allgemeinen Zugriff auf den Server beschränken möchten, entfernen Sie die Gruppe "Jeder".  
  
    -   Um Ihr MultiPoint-Server den Benutzerzugriff auf Stationen, fügen Sie jeder lokales Konto oder die einzelnen Benutzer oder eine Gruppe von Domänenkonten der Remotedesktopbenutzer-Gruppe hinzu.  