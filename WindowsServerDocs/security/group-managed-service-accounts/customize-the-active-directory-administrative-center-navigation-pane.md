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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenter

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

  Durchsuchen Sie den Navigationsbereich des Active Directory-Verwaltungscenter mithilfe der Strukturansicht, das mit der Konsolenstruktur Active Directory-Benutzer und -Computer vergleichbar ist, oder mithilfe der Listenansicht angezeigt.

 Ob Sie die Strukturansicht oder die Listenansicht verwenden, können Sie den Navigationsbereich des Active Directory Administrative Center jederzeit anpassen, indem Sie verschiedene Container aus der lokalen Domäne oder einer beliebigen fremden Domäne hinzufügen \ (d.h. einer anderen Domäne als der lokalen Domäne mit einem bestehende Vertrauensstellung mit der lokalen Domäne\) für den Navigationsbereich als separate Knoten. Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenter können Sie einen schnelleren Zugriff auf Active Directory-Objekte bereitstellen. Weitere Informationen finden Sie unter [Verwalten anderer Domänen im Active Directory-Verwaltungscenter ](manage-different-domains-in-active-directory-administrative-center.md).

 Auch, um den Navigationsbereich weiter anzupassen, Sie können umbenennen entfernen diese manuell hinzugefügten Navigationsbereichsknoten, Duplikate dieser Knoten erstellen oder verschieben nach oben oder unten im Navigationsbereich.

> [!NOTE]
>  Der Standardknoten für die lokale Domäne kann nicht angepasst werden.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Um den Navigationsbereich des Active Directory-Verwaltungscenter anpassen

1.  In Active Directory Administrative Center im Navigationsbereich mit der rechten Maustaste auf den Knoten, die Sie ändern möchten. Sie können die Position oder den Namen des Knotens ändern, oder Sie können ein Duplikat erstellen.

2.  Klicken Sie auf einen der folgenden Befehle:

    -   **Umbenennen**

    -   **Doppelten Knoten erstellen**

    -   **Entfernen**

    -   **Nach oben verschieben**

    -   **Nach unten verschieben**

 Mithilfe der Listenansicht können Sie die Liste der zuletzt verwendeten \(MRU\) nutzen. Die MRU-Liste wird automatisch unter einem Navigationsknoten angezeigt, wenn Sie mindestens einen Container in dieses Navigationsknotens besuchen. Sie können die aktuelle Liste der MRU-Liste auch anzeigen, durch Erweitern der Breadcrumb-Leiste am oberen Rand des Fensters Active Directory-Verwaltungscenter. Die MRU-Liste enthält immer die letzten drei Container, die Sie in einem bestimmten Navigationsknoten besucht haben. Jedes Mal, wenn Sie einen bestimmten Container auswählen, wird dieser Container am Anfang der MRU-Liste hinzugefügt und der letzte Container in der MRU-Liste wird entfernt.

  

