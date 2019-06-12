---
title: Wechseln zwischen Modi
description: Informationen Sie zum Wechseln zwischen Konsole und die Station-Modus in MultiPoint Services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: a9c00d65ad1c59e91f4011ab932bf9f921957c59
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446156"
---
# <a name="switch-between-modes"></a>Wechseln zwischen Modi
MultiPoint-Manager umfasst die folgenden Modi aus, um Sie verschiedene Arten von MultiPoint Services-systemverwaltung zu unterstützen:  
  
-   *Stationsmodus*: Standardmäßig wird die MultiPoint Services-Systems im stationsmodus gestartet. Im Stationsmodus weisen die MultiPoint Server-Stationen folgendes Verhalten auf: Jede Station wird als separater Computer mit Windows ausgeführt, und das System kann von mehreren Benutzern gleichzeitig verwendet werden. Sie und Ihre Benutzer können Dateien freigeben und die erforderlichen Aufgaben erledigen.  
  
-   *Konsolenmodus*: Bei der MultiPoint Services-System im Konsolenmodus ausgeführt wird, installieren und Aktualisieren von Software und Treiber und andere Verwaltungsaufgaben ausführen. Im Konsolenmodus sind keine anderen *Stationen* zur Verwendung durch andere Computerbenutzer verfügbar. Diese Stationen werden nicht im MultiPoint-Manager angezeigt. Alle Monitore, die direkt mit dem Server verbunden werden als zeigt dieses behandelt.   
  
> [!NOTE]
> Um den Start des Systems im Konsolenmodus zu erzwingen, ändern Sie die Standardeinstellung in den Einstellungen für den Server.  
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>So wechseln Sie aus dem Stationsmodus in den Konsolenmodus  
  
1.  Öffnen Sie MultiPoint-Manager im stationsmodus, und klicken Sie dann auf die **Startseite** Registerkarte.  
  
2.  Klicken Sie in der Spalte **Computer** auf den Computer, für den Sie den Modus ändern möchten.  
  
3.  Klicken Sie unter *Computername* **Aufgaben**, klicken Sie auf **wechseln Sie in den Konsolenmodus**. Der Computer wird neu gestartet, und keine Station ist mehr verfügbar.  
  
## <a name="to-switch-from-console-mode-to-station-mode"></a>So wechseln Sie aus dem Konsolenmodus in den Stationsmodus  
  
1.  Öffnen Sie MultiPoint-Manager im Konsolenmodus ausgeführt werden soll, und klicken Sie dann auf die **Startseite** Registerkarte.  
  
2.  Klicken Sie in der Spalte **Computer** auf den Computer, für den Sie den Modus ändern möchten.  
  
3.  Klicken Sie unter *Computername* **Aufgaben**, klicken Sie auf **wechseln Sie in den stationsmodus**. Der Computer wird neu gestartet, und alle Stationen sind verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)