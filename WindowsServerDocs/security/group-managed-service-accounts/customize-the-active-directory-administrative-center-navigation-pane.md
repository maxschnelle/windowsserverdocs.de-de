---
title: Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenter
ms.prod: windows-server-threshold
description: Windows Server-Sicherheit
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: c9933d16-e153-435a-b5b7-3e594db42d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: e7b1128d93912f724225905bedd38131f8aab0b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854841"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenter

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

  Sie können mithilfe der Strukturansicht, die in der Konsolenstruktur Active Directory-Benutzer und-Computer vergleichbar ist, oder Verwenden der Listenansicht im Navigationsbereich des Active Directory Administrative Center durchsuchen.

 Unabhängig davon, ob Sie die Strukturansicht oder der Liste angezeigt, können Sie den Navigationsbereich des Active Directory Administrative Center jederzeit anpassen, indem Sie verschiedene Container aus der lokalen Domäne oder einer beliebigen fremden Domäne hinzufügen \(, also einer anderen Domäne als der lokalen Domäne eine Vertrauensstellung mit der lokalen Domäne Listenfeldsteuerelement\) zum Navigationsbereich als separate Knoten. Anpassen des Navigationsbereichs des Active Directory Administrative Center bieten schnelleren Zugriff auf Active Directory-Objekte. Weitere Informationen finden Sie unter [verwalten Unterschiedlicher Domänen im Active Directory Administrative Center](manage-different-domains-in-active-directory-administrative-center.md).

 Um den Navigationsbereich weiter anzupassen, können Sie die manuell hinzugefügten Navigationsbereichsknoten umbenennen oder entfernen, die Knoten duplizieren oder im Navigationsbereich nach oben oder unten verschieben.

> [!NOTE]
>  Der Standardknoten für die lokale Domäne kann nicht angepasst werden.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Um die Anpassung des Navigationsbereichs des Active Directory-Verwaltungscenter

1.  Direkt in den Navigationsbereich des Active Directory Administrative Center,\-klicken Sie auf den Knoten, die Sie ändern möchten. Sie können die Position oder den Namen des Knotens ändern oder den Knoten duplizieren.

2.  Klicken Sie auf die folgenden Befehle aus:

    -   **Umbenennen**

    -   **Doppelten Knoten erstellen**

    -   **Entfernen**

    -   **Nach oben**

    -   **Nach unten verschieben**

 Mithilfe der Listenansicht können Sie profitieren von der zuletzt verwendeten \(MRU\) Liste. Die MRU-Liste wird automatisch unter einem Navigationsknoten angezeigt, wenn Sie mindestens einen Container in dieses Navigationsknotens besuchen. Sie können auch die aktuelle MRU-Liste anzeigen, erweitern Sie die Breadcrumb-Leiste am oberen Rand des Fensters für die Active Directory Administrative Center. Die MRU-Liste enthält immer die letzten drei Container, die Sie in einem bestimmten Navigationsknoten besucht haben. Jedes Mal, wenn Sie einen bestimmten Container auswählen, wird dieser Container am Anfang der Liste der zuletzt besuchten Objekte hinzugefügt, und der letzte Container in der Liste der zuletzt besuchten Objekte wird entfernt.

  

