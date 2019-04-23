---
title: Erstellen und Verwalten von Servergruppen
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d5b1be8-49fd-4ff7-9580-e4ff21fe4b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32e20040e2cb075e447c0d03d48676c7011a5a92
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889481"
---
# <a name="create-and-manage-server-groups"></a>Erstellen und Verwalten von Servergruppen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema beschreibt, wie Sie benutzerdefinierte, benutzerdefinierte Gruppen von Servern im Server-Manager in Windows Server erstellen.

## <a name="BKMK_groups"></a>Servergruppen
Server, die Sie dem Serverpool hinzufügen, werden angezeigt, auf die **alle Server** Seite im Server-Manager. Sie können benutzerdefinierte Gruppen von Servern erstellen, die Sie hinzugefügt haben. Servergruppen ermöglichen das Anzeigen und Verwalten einer kleinen Untergruppe in Ihrem Serverpool als logische Einheit; Sie können z. B. eine Gruppe namens erstellen **Buchhaltungsserver** für alle Server in Ihrer Organisation die Buchhaltungsabteilung weiterleiten oder eine Gruppe aufgerufen, **Chicago** für alle Server, die geografisch befinden in Chicago. Nachdem Sie eine Servergruppe erstellt haben, wird von der Gruppe-Startseite im Server-Manager zeigt Informationen zu Ereignissen, Diensten, Leistungsindikatoren, Best Practices Analyzer-Ergebnisse und installierten Rollen und Features für die Gruppe als Ganzes.

Server können mehreren Gruppen angehören.

#### <a name="to-create-a-new-server-group"></a>So erstellen Sie eine neue Servergruppe

1.  Auf der **verwalten** Menü klicken Sie auf **Servergruppe erstellen**.

2.  Geben Sie im Textfeld **Servergruppenname** einen Anzeigenamen für die Servergruppe ein, z. B. **Buchhaltungsserver**.

3.  Server Hinzufügen der **ausgewählten** Liste, aus dem Serverpool oder weitere Server zur Gruppe hinzufügen, mit der **active Directory**, **DNS**, oder **importieren**Registerkarten. Weitere Informationen zur Verwendung dieser Registerkarten finden Sie unter [Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md) in diesem Handbuch.

4.  Klicken Sie nach dem Hinzufügen der Server auf **OK**. Die neue Gruppe wird angezeigt, in der Server-Manager-Navigationsbereich unter der **alle Server** Gruppe.

#### <a name="to-edit-an-existing-server-group"></a>So bearbeiten Sie eine vorhandene Servergruppe

1.  Führen Sie eine der folgenden Aktionen aus.

    -   Klicken Sie im Navigationsbereich des Server-Manager Maustaste auf eine Servergruppe, und klicken Sie dann auf **Servergruppe bearbeiten**.

    -   Öffnen Sie auf der Startseite der Servergruppe das **Aufgaben** Menü auf der **Server** Kachel, und klicken Sie dann auf **Servergruppe bearbeiten**.

2.  den Namen der Gruppe ändern oder hinzufügen oder Entfernen von Servern aus der Gruppe.

    > [!NOTE]
    > Entfernen von Servern aus einer Servergruppe werden keine Server im Server-Manager entfernt. Server, die Sie aus einer Gruppe entfernen, bleiben in der Gruppe **Alle Server** im Serverpool erhalten.

3.  Klicken Sie nach dem Ändern der Gruppe auf **OK**.

#### <a name="to-delete-an-existing-server-group"></a>So löschen Sie eine vorhandene Servergruppe

1.  Führen Sie eine der folgenden Aktionen aus.

    -   Klicken Sie im Navigationsbereich des Server-Manager Maustaste auf eine Servergruppe, und klicken Sie dann auf **Servergruppe löschen**.

    -   Öffnen Sie auf der Startseite der Servergruppe das **Aufgaben** Menü auf der **Server** Kachel, und klicken Sie dann auf **Servergruppe löschen**.

2.  Klicken Sie auf **Ja**, wenn Sie aufgefordert werden, das Löschen der Servergruppe zu bestätigen.

    > [!NOTE]
    > Löschen einer Servergruppe werden keine Server im Server-Manager entfernt. Server, die in einer gelöschten Gruppe enthalten waren, bleiben in der Gruppe **Alle Server** im Serverpool erhalten.

3.  Klicken Sie nach dem Ändern der Gruppe auf **OK**.

## <a name="see-also"></a>Siehe auch
[Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md)
[Server-Manager](server-manager.md)



