---
title: Active Directory-Verwaltungscenter Navigationsbereich anpassen
ms.prod: windows-server
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
ms.openlocfilehash: 63038014207acd3846cb8db20c7836718615df51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403753"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory-Verwaltungscenter Navigationsbereich anpassen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

  Sie können den Navigationsbereich Active Directory-Verwaltungscenter in der Strukturansicht durchsuchen, die der Konsolen Struktur Active Directory Benutzer und Computer ähnelt, oder indem Sie die Listenansicht verwenden.

 Unabhängig davon, ob Sie die Strukturansicht oder die Listenansicht verwenden, können Sie den Active Directory-Verwaltungscenter Navigationsbereich jederzeit anpassen, indem Sie verschiedene Container aus der lokalen Domäne oder einer beliebigen fremden Domäne hinzufügen \(d. h. eine andere Domäne als die lokale Domäne, die über eine Vertrauensstellung mit der lokalen Domäne verfügt\) zum Navigationsbereich als separate Knoten. Durch das Anpassen des Active Directory-Verwaltungscenter Navigationsbereichs können Sie einen schnelleren Zugriff auf Active Directory Objekte bereitstellen. Weitere Informationen finden Sie unter [Verwalten unterschiedlicher Domänen in Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

 Um den Navigationsbereich weiter anzupassen, können Sie die manuell hinzugefügten Navigationsbereichsknoten umbenennen oder entfernen, die Knoten duplizieren oder im Navigationsbereich nach oben oder unten verschieben.

> [!NOTE]
>  Der Standardknoten für die lokale Domäne kann nicht angepasst werden.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>So passen Sie den Active Directory-Verwaltungscenter Navigationsbereich an

1. Klicken Sie im Navigationsbereich Active Directory-Verwaltungscenter mit der rechten\-auf den Knoten, den Sie ändern möchten. Sie können die Position oder den Namen des Knotens ändern oder den Knoten duplizieren.

2. Klicken Sie auf einen der folgenden Befehle:

   -   **Umbenennen**

   -   **Duplizierten Knoten erstellen**

   -   **Entfernen**

   -   **Nach oben**

   -   **Nach unten**

   Mithilfe der Listenansicht können Sie die zuletzt verwendete \(MRU-\) Liste nutzen. Die MRU-Liste wird automatisch unter einem Navigations Knoten angezeigt, wenn Sie mindestens einen Container in diesem Navigations Knoten besuchen. Sie können die aktuelle MRU-Liste auch anzeigen, indem Sie die Breadcrumb-Leiste am oberen Rand des Active Directory-Verwaltungscenter Fensters erweitern. Die MRU-Liste enthält immer die letzten drei Container, die Sie in einem bestimmten Navigations Knoten besucht haben. Jedes Mal, wenn Sie einen bestimmten Container auswählen, wird dieser Container am Anfang der Liste der zuletzt besuchten Objekte hinzugefügt, und der letzte Container in der Liste der zuletzt besuchten Objekte wird entfernt.

  

