---
title: Verwalten unterschiedlicher Domänen in Active Directory-Verwaltungscenter
ms.prod: windows-server
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
ms.openlocfilehash: 71edf6bb38cc665fe5c780ce986d0c0b8807d6ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386929"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Verwalten unterschiedlicher Domänen in Active Directory-Verwaltungscenter

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

  Wenn Sie Active Directory Verwaltung öffnen, wird die Domäne, bei der Sie zurzeit auf diesem Computer angemeldet sind \(die lokale Domäne\) im Active Directory-Verwaltungscenter Navigationsbereich \(linken Bereich\)angezeigt. Abhängig von den rechten Ihres aktuellen Anmelde Informations Satzes können Sie die Active Directory Objekte in dieser lokalen Domäne anzeigen oder verwalten.

 Sie können auch denselben Satz von Anmelde Informationen und dieselbe Instanz von Active Directory-Verwaltungscenter verwenden, um Active Directory Objekte in einer beliebigen anderen Domäne in derselben Gesamtstruktur anzuzeigen oder zu verwalten, oder eine Domäne in einer anderen Gesamtstruktur, die eine Vertrauensstellung mit dem lokalen -. Sowohl eine\-Way-Vertrauensstellung als auch zwei\-, wie Vertrauens Stellungen unterstützt werden.

> [!NOTE]
>  Wenn eine\-Weise Vertrauensstellung zwischen Domäne a und Domäne b vorhanden ist, über die Benutzer in Domäne a auf Ressourcen in Domäne b zugreifen können, aber Benutzer in Domäne b können nicht auf Ressourcen in Domäne a zugreifen, wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausführen, auf dem Domäne a als lokale Domäne festgelegt ist, können Sie mit dem aktuellen Satz von Anmelde Informationen und in derselben Instanz von Active Directory-Verwaltungscenter eine Verbindung mit Wenn Sie jedoch Active Directory-Verwaltungscenter auf dem Computer ausführen, auf dem Domäne B Ihre lokale Domäne ist, können Sie keine Verbindung mit Domäne A mit demselben Satz von Anmelde Informationen in derselben Instanz des Active Directory-Verwaltungscenter herstellen.

 Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: zum Verwalten einer fremden Domäne in der ausgewählten Instanz von Active Directory-Verwaltungscenter mithilfe des aktuellen Anmelde Informations Satzes

1.  Klicken Sie zum Öffnen vonActive Directory-Verwaltungscenter in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory-Verwaltungscenter**.

    > [!NOTE]
    >  Sie können Active Directory-Verwaltungscenter auch öffnen, indem Sie auf **Start**klicken und dann **Dsac. exe**eingeben.

2.  Klicken Sie zum Öffnen von **Navigations Knoten hinzufügen**auf **Verwalten**, und klicken Sie dann auf **Navigations Knoten hinzufügen** , wie in der folgenden Abbildung dargestellt.

     ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/ADDS_ADACAddNavNode.gif)

3.  Klicken Sie in **Navigations Knoten hinzufügen**auf **Verbindung mit anderen Domänen herstellen** , wie in der folgenden Abbildung dargestellt.

     ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/ADDS_ADACConnectToDomain.gif)

4.  Geben Sie in **Verbindung herstellen**den Namen der fremden Domäne ein, die Sie verwalten möchten \(z. b. **contoso.com**\), und klicken Sie dann auf **OK**.

5.  Wenn Sie erfolgreich eine Verbindung mit der fremden Domäne hergestellt haben, Durchsuchen Sie die Spalten im Fenster **Navigations Knoten hinzufügen** , wählen Sie den Container aus, den Sie dem Navigationsbereich Active Directory-Verwaltungscenter hinzufügen möchten, und klicken Sie dann auf **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: zum Verwalten einer fremden Domäne in der ausgewählten Instanz von Active Directory-Verwaltungscenter mithilfe des aktuellen Anmelde Informations Satzes

1. Klicken Sie zum Öffnen von Active Directory-Verwaltungscenter auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.

   > [!NOTE]
   >  Sie können Active Directory-Verwaltungscenter auch öffnen, indem Sie auf **Start**und auf **Ausführen**klicken und dann **Dsac. exe**eingeben.

2. Um **Navigations Knoten hinzufügen**zu öffnen, klicken Sie im oberen Bereich des Fensters Active Directory-Verwaltungscenter auf **Navigations Knoten hinzufügen** , wie in der folgenden Abbildung dargestellt.

    ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  Eine weitere Möglichkeit zum Öffnen von **Navigations Knoten hinzufügen** besteht darin, mit der rechten\-auf eine beliebige Stelle im leeren Bereich im Active Directory-Verwaltungscenter Navigationsbereich zu klicken und dann auf **Navigations Knoten hinzufügen**zu klicken.

3. Klicken Sie in **Navigations Knoten hinzufügen**auf **Verbindung mit anderen Domänen herstellen** , wie in der folgenden Abbildung dargestellt.

    ![Screenshot: * * Navigations Knoten hinzufügen * * * * Verbindung mit anderen Domänen herstellen * * UI](media/add_nav_nodes.gif)

4. Geben Sie in **Verbindung herstellen**den Namen der fremden Domäne ein, die Sie verwalten möchten \(z. b. **contoso.com**\), und klicken Sie dann auf **OK**.

5. Wenn Sie erfolgreich eine Verbindung mit der fremden Domäne hergestellt haben, Durchsuchen Sie die Spalten im Fenster **Navigations Knoten hinzufügen** , wählen Sie den Container aus, den Sie dem Navigationsbereich Active Directory-Verwaltungscenter hinzufügen möchten, und klicken Sie dann auf **OK**.

   Weitere Informationen zum Anpassen des Navigationsbereichs Active Directory-Verwaltungscenter finden Sie unter [Anpassen des Navigationsbereichs Active Directory-Verwaltungscenter](customize-the-active-directory-administrative-center-navigation-pane.md).

   Sie können Active Directory-Verwaltungscenter auch öffnen, indem Sie einen Satz von Anmelde Informationen verwenden, der sich von dem aktuellen Satz von Anmelde Informationen unterscheidet. Der Befehl im folgenden Verfahren kann nützlich sein, wenn Sie auf dem Computer angemeldet sind, auf dem Active Directory-Verwaltungscenter mit normalen Benutzer Anmelde Informationen ausgeführt wird. Sie möchten jedoch Active Directory-Verwaltungscenter auf diesem Computer verwenden, um Ihre lokale Domäne als Administrator. \(dieser Befehl kann auch nützlich sein, wenn Sie Active Directory-Verwaltungscenter verwenden möchten, um eine fremde fremde Domäne, die sich von Ihrer lokalen Domäne unterscheidet, mit einem Satz von Anmelde Informationen, die sich von den aktuellen Anmelde Informationen unterscheiden, Remote zu verwalten. Allerdings muss die fremde Domäne über eine festgelegte Vertrauensstellung mit der lokalen Domäne verfügen.\)

   Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>So verwalten Sie eine Domäne mithilfe von Anmeldeinformationen, die nicht mit den aktuellen Anmeldeinformationen identisch sind

1.  Um Active Directory-Verwaltungscenter zu öffnen, geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

     `runas /user:<domain\user> dsac`

     Dabei ist `<domain\user>` der Satz von Anmelde Informationen, die Sie mit Active Directory-Verwaltungscenter öffnen möchten, und `dsac` den Namen der Active Directory-Verwaltungscenter ausführbaren Datei \(Dsac. exe\).

     Geben Sie beispielsweise den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

     `runas /user:contoso\administrator dsac`

2.  Wenn Active Directory-Verwaltungscenter geöffnet ist, navigieren Sie zum Navigationsbereich, um Ihre Active Directory Domäne anzuzeigen oder zu verwalten.

  

