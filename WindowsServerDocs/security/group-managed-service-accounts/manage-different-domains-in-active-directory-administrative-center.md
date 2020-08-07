---
title: Verwalten unterschiedlicher Domänen in Active Directory-Verwaltungscenter
description: Windows Server-Sicherheit
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8ccd183e3450fd6c520790d9130d27b99b06a5ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971447"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Verwalten unterschiedlicher Domänen in Active Directory-Verwaltungscenter

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

  Wenn Sie Active Directory Verwaltung öffnen, wird die \( lokale Domäne \) im linken Bereich im Active Directory-Verwaltungscenter Navigationsbereich angezeigt, bei der Sie auf diesem Computer zurzeit angemeldet sind \( \) . In Abhängigkeit von den Rechten Ihrer aktuellen Anmeldeinformationen können Sie die Active Directory-Objekte in dieser lokalen Domäne anzeigen oder verwalten.

 Sie können auch denselben Satz von Anmelde Informationen und dieselbe Instanz von Active Directory-Verwaltungscenter verwenden, um Active Directory Objekte in einer beliebigen anderen Domäne in derselben Gesamtstruktur anzuzeigen oder zu verwalten, oder eine Domäne in einer anderen Gesamtstruktur, die über eine Vertrauensstellung mit der lokalen Domäne verfügt. Sowohl unidirektionale \- als auch Vertrauens Stellungen \- werden unterstützt.

> [!NOTE]
>  Wenn eine unidirektionale \- Vertrauensstellung zwischen Domäne a und Domäne b vorhanden ist, über die Benutzer in Domäne a auf Ressourcen in Domäne b zugreifen können. Benutzer in Domäne b können jedoch nicht auf Ressourcen in Domäne a zugreifen. Wenn Sie Active Directory-Verwaltungscenter auf dem Computer ausführen, auf dem Domäne a als lokale Domäne festgelegt ist, können Sie eine Verbindung mit Domäne b mit dem aktuellen Satz von Anmelde Informationen und Active Directory-Verwaltungscenter in Wenn Sie allerdings das Active Directory-Verwaltungscenter auf dem Computer ausführen, auf dem Domäne B die lokale Domäne darstellt, können Sie mit denselben Anmeldeinformationen und in derselben Instanz des Active Directory-Verwaltungscenters keine Verbindung mit Domäne A herstellen.

 Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: zum Verwalten einer fremden Domäne in der ausgewählten Instanz von Active Directory-Verwaltungscenter mithilfe des aktuellen Anmelde Informations Satzes

1.  Klicken Sie zum Öffnen von **Server Manager**Active Directory-Verwaltungscenter in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory-Verwaltungscenter**.

    > [!NOTE]
    >  Eine weitere Möglichkeit zum Öffnen von Active Directory-Verwaltungscenter ist, auf **Start**zu klicken und dann **dsac.exe**einzugeben.

2.  Klicken Sie zum Öffnen von **Navigations Knoten hinzufügen**auf **Verwalten**, und klicken Sie dann auf **Navigations Knoten hinzufügen** , wie in der folgenden Abbildung dargestellt.

     ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/ADDS_ADACAddNavNode.gif)

3.  Klicken Sie in **Navigations Knoten hinzufügen**auf **Verbindung mit anderen Domänen herstellen** , wie in der folgenden Abbildung dargestellt.

     ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/ADDS_ADACConnectToDomain.gif)

4.  Geben Sie in **Verbindung herstellen**den Namen der fremden Domäne ein, die Sie verwalten möchten \( , z. b. **contoso.com** \) , und klicken Sie dann auf **OK**.

5.  Wenn Sie erfolgreich mit der fremden Domäne verbunden sind, navigieren Sie in den Spalten im Fenster **Navigationsknoten hinzufügen**. Wählen Sie die Container aus, die dem Navigationsbereich des Active Directory-Verwaltungscenters hinzugefügt werden sollen, und klicken Sie dann auf **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: zum Verwalten einer fremden Domäne in der ausgewählten Instanz von Active Directory-Verwaltungscenter mithilfe des aktuellen Anmelde Informations Satzes

1. Um das Active Directory-Verwaltungscenter zu öffnen, klicken Sie auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.

   > [!NOTE]
   >  Eine andere Möglichkeit, das Active Directory-Verwaltungscenter zu öffnen, besteht darin, dass Sie auf **Start** und dann auf **Ausführen** klicken und anschließend **dsac.exe** eingeben.

2. Um **Navigations Knoten hinzufügen**zu öffnen, klicken Sie im oberen Bereich des Fensters Active Directory-Verwaltungscenter auf **Navigations Knoten hinzufügen** , wie in der folgenden Abbildung dargestellt.

    ![Screenshot: * * Navigations Knoten hinzufügen * * UI](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  Eine weitere Möglichkeit zum Öffnen von **Navigations Knoten hinzufügen** besteht darin, mit der rechten Maustaste auf einen \- leeren Bereich im Navigationsbereich Active Directory-Verwaltungscenter zu klicken und dann auf **Navigations Knoten hinzufügen**zu klicken.

3. Klicken Sie in **Navigations Knoten hinzufügen**auf **Verbindung mit anderen Domänen herstellen** , wie in der folgenden Abbildung dargestellt.

    ![Screenshot: * * Navigations Knoten hinzufügen * * * * Verbindung mit anderen Domänen herstellen * * UI](media/add_nav_nodes.gif)

4. Geben Sie in **Verbindung herstellen**den Namen der fremden Domäne ein, die Sie verwalten möchten \( , z. b. **contoso.com** \) , und klicken Sie dann auf **OK**.

5. Wenn Sie erfolgreich mit der fremden Domäne verbunden sind, navigieren Sie in den Spalten im Fenster **Navigationsknoten hinzufügen**. Wählen Sie die Container aus, die dem Navigationsbereich des Active Directory-Verwaltungscenters hinzugefügt werden sollen, und klicken Sie dann auf **OK**.

   Weitere Informationen zum Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenters finden Sie unter [Anpassen des Navigationsbereichs des Active Directory-Verwaltungscenters (möglicherweise in englischer Sprache)](customize-the-active-directory-administrative-center-navigation-pane.md).

   Sie können das Active Directory-Verwaltungscenter auch mithilfe von Anmeldeinformationen öffnen, die nicht mit Ihren aktuellen Anmeldeinformationen identisch sind. Der Befehl im folgenden Verfahren kann hilfreich sein, wenn Sie an dem Computer, auf dem das Active Directory-Verwaltungscenter ausgeführt wird, mit normalen Anmeldeinformationen angemeldet sind, aber das Active Directory-Verwaltungscenter auf diesem Computer zum Verwalten der lokalen Domäne als Administrator verwenden möchten. \(Dieser Befehl kann auch nützlich sein, wenn Sie Active Directory-Verwaltungscenter verwenden möchten, um eine fremde fremde Domäne, die sich von Ihrer lokalen Domäne unterscheidet, mit einem Satz von Anmelde Informationen, die sich von ihren aktuellen Anmelde Informationen unterscheiden, Remote zu verwalten. Allerdings muss die fremde Domäne über eine festgelegte Vertrauensstellung mit der lokalen Domäne verfügen.\)

   Zum Abschließen dieses Verfahrens besteht keine Mindestanforderung an eine Gruppenmitgliedschaft.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>So verwalten Sie eine Domäne mithilfe von Anmeldeinformationen, die nicht mit den aktuellen Anmeldeinformationen identisch sind

1.  Zum Öffnen des Active Directory-Verwaltungscenters geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

     `runas /user:<domain\user> dsac`

     `<domain\user>`Dabei ist der Satz von Anmelde Informationen, mit denen Sie Active Directory-Verwaltungscenter öffnen möchten, und `dsac` ist der Name der ausführbaren Datei Active Directory-Verwaltungscenter \(Dsac.exe\) .

     Geben Sie beispielsweise folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

     `runas /user:contoso\administrator dsac`

2.  Wenn das Active Directory-Verwaltungscenter geöffnet ist, navigieren Sie im Navigationsbereich, um Ihre Active Directory-Domäne anzuzeigen oder zu verwalten.



