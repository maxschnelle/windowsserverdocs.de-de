---
title: Verwalten Sie unterschiedliche Domänen im Active Directory-Verwaltungscenter
ms.prod: windows-server-threshold
description: Windows Server-Sicherheit
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd5650724272422d09e87b7eecf10f825b00fabf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447040"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Verwalten Sie unterschiedliche Domänen im Active Directory-Verwaltungscenter

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

  Beim Öffnen von Active Directory Administrative, die Domäne, die Sie zurzeit auf diesem Computer angemeldet sind \(der lokalen Domäne\) wird in den Navigationsbereich des Active Directory Administrative Center \(im linken Bereich\). Je nach den rechten Ihrer aktuellen Satz von Anmeldeinformationen können Sie anzeigen oder Verwalten von Active Directory-Objekte in dieser lokalen Domäne.

 Sie können auch den gleichen Satz von Anmeldeinformationen und der gleichen Instanz von Active Directory-Verwaltungscenter verwenden, anzeigen oder Verwalten von Active Directory-Objekte in einer beliebigen anderen Domäne in der gleichen Gesamtstruktur oder einer Domäne in einer anderen Gesamtstruktur, die eine Vertrauensstellung mit der lokalen die Domäne. Sowohl\-bidirektionaler Vertrauensstellung und zwei\-bidirektionaler Vertrauensstellung werden unterstützt.

> [!NOTE]
>  Wenn eine Version\-Weise Vertrauensstellung zwischen Domäne A und Domäne B über die Benutzer in Domäne A können Ressourcen in Domäne B zugreifen, aber Benutzer in Domäne B nicht auf Ressourcen in Domäne A zugreifen, wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausgeführt werden steht Ihrer lokalen Domäne, in Domäne A können Sie zu Domäne B mit den aktuellen Satz von Anmeldeinformationen und in der gleichen Instanz von Active Directory Administrative Center eine Verbindung herstellen. Wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausgeführt werden, in Domäne B Ihrer lokalen Domäne ist, Sie aber nicht mit den gleichen Satz von Anmeldeinformationen in der gleichen Instanz von Active Directory-Verwaltungscenter-Domäne ein.

 Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: Um eine fremde Domäne in der ausgewählten Instanz von Active Directory Administrative Center, die mit den aktuellen Satz von Anmeldeinformationen zu verwalten.

1.  Um in Active Directory-Verwaltungscenter öffnen **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Active Directory Administrative Center**.

    > [!NOTE]
    >  Klicken Sie auf eine andere Möglichkeit, Active Directory-Verwaltungscenter zu öffnen ist **starten**, und geben Sie dann **dsac.exe**.

2.  Zum Öffnen **Navigationsknoten hinzufügen**, klicken Sie auf **verwalten**, klicken Sie dann auf **Navigationsknoten hinzufügen** wie in der folgenden Abbildung dargestellt.

     ![Screenshot mit ** Navigation Knoten ** UI hinzufügen](media/ADDS_ADACAddNavNode.gif)

3.  In **Navigationsknoten hinzufügen**, klicken Sie auf **Herstellen einer Verbindung mit anderen Domänen** wie in der folgenden Abbildung dargestellt.

     ![Screenshot mit ** Navigation Knoten ** UI hinzufügen](media/ADDS_ADACConnectToDomain.gif)

4.  In **Herstellen einer Verbindung mit**, geben Sie den Namen der fremden Domäne ein, die Sie verwalten möchten \(z. B. **"contoso.com"** \), und klicken Sie dann auf **OK**.

5.  Wenn Sie mit der fremden Domäne verbunden sind, navigieren Sie in den Spalten im der **Navigationsknoten hinzufügen** Fenster, wählen Sie den Container oder den Container, um den Navigationsbereich des Active Directory Administrative Center, hinzufügen und Klicken Sie dann auf **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: Um eine fremde Domäne in der ausgewählten Instanz von Active Directory Administrative Center, die mit den aktuellen Satz von Anmeldeinformationen zu verwalten.

1. Um Active Directory-Verwaltungscenter zu öffnen, klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory Administrative Center**.

   > [!NOTE]
   >  Klicken Sie auf eine andere Möglichkeit, Active Directory-Verwaltungscenter zu öffnen ist **starten**, klicken Sie auf **ausführen**, und geben Sie dann **dsac.exe**.

2. Zum Öffnen **Navigationsknoten hinzufügen**, klicken Sie im oberen Bereich des Fensters Active Directory-Verwaltungscenter auf **Navigationsknoten hinzufügen** wie in der folgenden Abbildung dargestellt.

    ![Screenshot mit ** Navigation Knoten ** UI hinzufügen](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  Eine weitere Möglichkeit zum Öffnen **Navigationsknoten hinzufügen** nach rechts ist\-klicken Sie auf eine beliebige Stelle in den leeren Bereich in den Navigationsbereich des Active Directory Administrative Center, und klicken Sie dann auf **Navigationsknoten hinzufügen**.

3. In **Navigationsknoten hinzufügen**, klicken Sie auf **Herstellen einer Verbindung mit anderen Domänen** wie in der folgenden Abbildung dargestellt.

    ![Screenshot mit ** hinzufügen Navigation Knoten ** ** Herstellen einer Verbindung mit anderen Domänen ** UI](media/add_nav_nodes.gif)

4. In **Herstellen einer Verbindung mit**, geben Sie den Namen der fremden Domäne ein, die Sie verwalten möchten \(z. B. **"contoso.com"** \), und klicken Sie dann auf **OK**.

5. Wenn Sie mit der fremden Domäne verbunden sind, navigieren Sie in den Spalten im der **Navigationsknoten hinzufügen** Fenster, wählen Sie den Container oder den Container, um den Navigationsbereich des Active Directory Administrative Center, hinzufügen und Klicken Sie dann auf **OK**.

   Weitere Informationen zum Anpassen des Navigationsbereichs des Active Directory Administrative Center finden Sie unter [Anpassen von Active Directory Administrative Center im Navigationsbereich](customize-the-active-directory-administrative-center-navigation-pane.md).

   Sie können auch die Active Directory Administrative Center öffnen, mithilfe eines Satzes von Anmeldeinformationen, das sich mit Ihren aktuellen Anmeldeinformationen unterscheidet. Der Befehl im folgenden Verfahren ist hilfreich, wenn Sie auf dem Computer angemeldet sind, die Active Directory Administrative Center mit normalen Anmeldeinformationen ausgeführt wird, aber Sie Active Directory-Verwaltungscenter auf diesem Computer verwenden, um verwalten möchten Ihre lokale Domäne als Administrator. \(Mit diesem Befehl kann auch nützlich sein, wenn Sie Active Directory Administrative Center zur Remoteverwaltung von einer fremden Domäne ein, die mit Ihrer lokalen Domäne mit einem Satz von Anmeldeinformationen unterscheidet, die sich von den aktuellen Satz von Anmeldeinformationen verwenden möchten. Allerdings muss die fremde Domäne eine Vertrauensstellung mit der lokalen Domäne müssen.\)

   Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>So verwalten Sie eine Domäne mithilfe von Anmeldeinformationen, die nicht mit den aktuellen Anmeldeinformationen identisch sind

1.  Um Active Directory Administrative Center, an der Eingabeaufforderung zu öffnen, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE:

     `runas /user:<domain\user> dsac`

     In denen `<domain\user>` ist ein Satz von Anmeldeinformationen, mit denen Sie Active Directory-Verwaltungscenter öffnen möchten, und `dsac` ist der Name des Active Directory Administrative Center ausführbare Datei \(Dsac.exe\).

     Geben Sie beispielsweise den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

     `runas /user:contoso\administrator dsac`

2.  Wenn Active Directory-Verwaltungscenter geöffnet ist, navigieren Sie im Navigationsbereich anzeigen oder Verwalten von Active Directory-Domäne.

  

