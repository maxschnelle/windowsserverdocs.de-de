---
title: "Verwalten Sie anderer Domänen im Active Directory-Verwaltungscenter"
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
ms.openlocfilehash: 5f253bd4952d8a347e97eafdb38d86fa98024b8d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Verwalten Sie anderer Domänen im Active Directory-Verwaltungscenter

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

  Beim Öffnen von Active Directory Administrative, die Domäne, die Sie derzeit auf diesem Computer angemeldet sind \ (lokale Domäne\) angezeigt wird, klicken Sie im Active Directory-Verwaltungscenter Navigationsbereich \(the left pane\). Abhängigkeit von den rechten Ihrer aktuellen Satz von Anmeldeinformationen können Sie anzeigen oder Verwalten von Active Directory-Objekte in dieser lokalen Domäne.

 Sie können auch den gleichen Satz von Anmeldeinformationen und derselben Instanz von Active Directory Administrative Center anzeigen oder Verwalten von Active Directory-Objekte in einer beliebigen anderen Domäne in derselben Gesamtstruktur oder einer Domäne in einer anderen Gesamtstruktur, die über eine Vertrauensstellung mit der lokalen verfügt. Domäne. Sowohl einmaligen-Wege- und Two\-Wege-Vertrauensstellungen werden unterstützt.

> [!NOTE]
>  Wenn es eine einmaligen unidirektionalen Vertrauensstellung zwischen Domäne A und Domäne B über die Benutzer in Domäne A Zugriff auf Ressourcen in Domäne B jedoch Benutzer in Domäne B nicht auf Ressourcen in Domäne A zugreifen, wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausführen, bei der es steht für Domäne A  der lokalen Domäne ist, können Sie mit Domäne B mit den aktuellen Satz von Anmeldeinformationen und in derselben Instanz des Active Directory-Verwaltungscenters verbinden. Wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausgeführt werden, in dem Domäne B die lokale Domäne ist, Sie jedoch keine Verbindung mit Domäne A mit den gleichen Satz von Anmeldeinformationen in der gleichen Instanz von Active Directory-Verwaltungscenter.

 Es gibt keine zum Durchführen dieses Verfahrens mindestens eine Gruppenmitgliedschaft.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: Eine fremde Domäne in der ausgewählten Instanz des Active Directory-Verwaltungscenters mithilfe der aktuellen Anmeldeinformationen verwalten

1.  Zum Öffnen von Active Directory-Verwaltungscenter in **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.

    > [!NOTE]
    >  Eine weitere Möglichkeit zum Öffnen von Active Directory-Verwaltungscenter ist auf **starten**, und geben Sie dann **dsac.exe**.

2.  Zum Öffnen **Navigationsknoten hinzufügen**, klicken Sie auf **verwalten**, klicken Sie dann auf **Navigationsknoten hinzufügen** wie in der folgenden Abbildung dargestellt.

     ![Screenshot der ** Navigation Knoten ** UI hinzufügen](media/ADDS_ADACAddNavNode.gif)

3.  In **Navigationsknoten hinzufügen**, klicken Sie auf **Verbinden mit anderen Domänen** wie in der folgenden Abbildung dargestellt.

     ![Screenshot der ** Navigation Knoten ** UI hinzufügen](media/ADDS_ADACConnectToDomain.gif)

4.  In **Verbinden mit**, geben Sie den Namen der fremden Domäne ein, die Sie verwalten möchten \ (z. B. **"contoso.com"**\), und klicken Sie dann auf **OK**.

5.  Wenn Sie mit der fremden Domäne verbunden sind, Durchsuchen Sie die Spalten in der **Navigationsknoten hinzufügen** Fenster, wählen Sie den oder die Container Navigationsbereich des Active Directory Administrative Center hinzufügen, und klicken Sie dann auf **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: Eine fremde Domäne in der ausgewählten Instanz des Active Directory-Verwaltungscenters mithilfe der aktuellen Anmeldeinformationen verwalten

1.  Um Active Directory-Verwaltungscenter zu öffnen, klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.

    > [!NOTE]
    >  Eine weitere Möglichkeit zum Öffnen von Active Directory-Verwaltungscenter ist auf **starten**, klicken Sie auf **ausführen**, und geben Sie dann **dsac.exe**.

2.  Zum Öffnen **Navigationsknoten hinzufügen**, klicken Sie im oberen Bereich des Fensters Active Directory-Verwaltungscenter auf **Navigationsknoten hinzufügen** wie in der folgenden Abbildungdargestellt.

     ![Screenshot der ** Navigation Knoten ** UI hinzufügen](media/click_add_nav_nodes.gif)

    > [!NOTE]
    >  Eine weitere Möglichkeit zum Öffnen **Navigationsknoten hinzufügen** ist, klicken Sie auf eine beliebige Stelle in dem leeren Bereich im Navigationsbereich Active Directory Administrative Center, und klicken Sie dann auf **Navigationsknoten hinzufügen**.

3.  In **Navigationsknoten hinzufügen**, klicken Sie auf **Verbinden mit anderen Domänen** wie in der folgenden Abbildung dargestellt.

     ![Screenshot der ** hinzufügen Navigation Knoten ** ** verbinden mit anderen Domänen ** UI](media/add_nav_nodes.gif)

4.  In **Verbinden mit**, geben Sie den Namen der fremden Domäne ein, die Sie verwalten möchten \ (z. B. **"contoso.com"**\), und klicken Sie dann auf **OK**.

5.  Wenn Sie mit der fremden Domäne verbunden sind, Durchsuchen Sie die Spalten in der **Navigationsknoten hinzufügen** Fenster, wählen Sie den oder die Container Navigationsbereich des Active Directory Administrative Center hinzufügen, und klicken Sie dann auf **OK**.

 Weitere Informationen zum Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenter finden Sie unter [Active Directory Administrative Center im Navigationsbereich anpassen](customize-the-active-directory-administrative-center-navigation-pane.md).

 Sie können auch Active Directory-Verwaltungscenter öffnen, mit einem Satz von Anmeldeinformationen, der von Ihren aktuellen Satz von Anmeldeinformationen unterscheidet. Der Befehl im folgenden Verfahren ist hilfreich, wenn Sie am Computer angemeldet sind, die Active Directory-Verwaltungscenter mit normalen ausgeführt wird, aber Sie Active Directory-Verwaltungscenter auf diesem Computer verwenden, verwalten möchten Ihre lokale Domäne als Administrator. \ (Dieser Befehl kann auch nützlich sein, wenn Sie Active Directory-Verwaltungscenter eine fremde Domäne Remote zu verwalten, die von der lokalen Domäne mit einem Satz von Anmeldeinformationen unterscheidet, die von Ihren aktuellen Satz von Anmeldeinformationen unterscheidet verwenden möchten. Die fremde Domäne muss jedoch eine Vertrauensstellung mit der lokalen Domäne sein. \)

 Es gibt keine zum Durchführen dieses Verfahrens mindestens eine Gruppenmitgliedschaft.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>Zum Verwalten einer Domäne mithilfe von Anmeldeinformationen, die nicht mit den aktuellen Anmeldeinformationen identisch sind

1.  Um Active Directory-Verwaltungscenter an einer Eingabeaufforderung zu öffnen, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:

     `runas /user:<domain\user> dsac`

     Wo `<domain\user>`ist ein Satz von Anmeldeinformationen, mit denen Sie Active Directory-Verwaltungscenter öffnen möchten und `dsac`ist der Active Directory-Verwaltungscenter ausführbare Datei Namen \(Dsac.exe\).

     Geben Sie z. B. den folgenden Befehl, und drücken Sie dann die EINGABETASTE:

     `runas /user:contoso\administrator dsac`

2.  Wenn die Active Directory-Verwaltungscenter geöffnet ist, Durchsuchen Sie im Navigationsbereich zum Anzeigen oder Verwalten von Active Directory-Domäne.

  

