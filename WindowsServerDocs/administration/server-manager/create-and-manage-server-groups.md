---
title: Erstellen und Verwalten von Server Gruppen
description: Server-Manager
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: 9d5b1be8-49fd-4ff7-9580-e4ff21fe4b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f4ad512c55bcd1391ad55bdbdeb9a2ba3bfd7f0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851543"
---
# <a name="create-and-manage-server-groups"></a>Erstellen und Verwalten von Server Gruppen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, wie benutzerdefinierte benutzerdefinierte Server Gruppen in Server-Manager in Windows Server erstellt werden.

## <a name="server-groups"></a><a name=BKMK_groups></a>Server Gruppen
Server, die Sie dem Server Pool hinzufügen, werden auf der Seite **alle Server** in Server-Manager angezeigt. Sie können benutzerdefinierte Gruppen von Servern erstellen, die Sie hinzugefügt haben. Mit Server Gruppen können Sie eine kleinere Teilmenge des Server Pools als logische Einheit anzeigen und verwalten. Sie können z. b. eine Gruppe namens **Buchhaltungsserver** für alle Server in der Buchhaltungsabteilung Ihrer Organisation oder eine Gruppe namens **Chicago** für alle Server erstellen, die sich geografisch in Chicago befinden. Nachdem Sie eine Server Gruppe erstellt haben, werden auf der Startseite der Gruppe in Server-Manager Informationen zu Ereignissen, Diensten, Leistungsindikatoren, Best Practices Analyzer Ergebnissen sowie zu installierten Rollen und Features für die Gruppe als Ganzes angezeigt.

Server können mehreren Gruppen angehören.

#### <a name="to-create-a-new-server-group"></a>So erstellen Sie eine neue Servergruppe

1.  Klicken Sie im Menü **Verwalten** auf **Server Gruppe erstellen**.

2.  Geben Sie im Textfeld **Servergruppenname** einen Anzeigenamen für die Servergruppe ein, z. B. **Buchhaltungsserver**.

3.  Fügen Sie der **ausgewählten** Liste Server aus dem Server Pool hinzu, oder fügen Sie der Gruppe mithilfe der Registerkarten **Active Directory**, **DNS**oder **importieren** weitere Server hinzu. Weitere Informationen zur Verwendung dieser Registerkarten finden [Sie unter Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md) in diesem Handbuch.

4.  Klicken Sie nach dem Hinzufügen der Server auf **OK**. Die neue Gruppe wird im Navigationsbereich Server-Manager unter der Gruppe **alle Server** angezeigt.

#### <a name="to-edit-an-existing-server-group"></a>So bearbeiten Sie eine vorhandene Servergruppe

1.  Führen Sie einen der folgenden Schritte aus:

    -   Klicken Sie im Navigationsbereich Server-Manager mit der rechten Maustaste auf eine Server Gruppe, und klicken Sie dann auf **Server Gruppe bearbeiten**.

    -   Öffnen Sie auf der Startseite der Server Gruppe das Menü **Aufgaben** auf der Kachel **Server** , und klicken Sie dann auf **Server Gruppe bearbeiten**.

2.  Ändern Sie den Gruppennamen, oder fügen Sie der Gruppe Server hinzu, oder entfernen Sie Sie.

    > [!NOTE]
    > durch das Entfernen von Servern aus einer Server Gruppe werden keine Server aus Server-Manager entfernt. Server, die Sie aus einer Gruppe entfernen, bleiben in der Gruppe **Alle Server** im Serverpool erhalten.

3.  Klicken Sie nach dem Ändern der Gruppe auf **OK**.

#### <a name="to-delete-an-existing-server-group"></a>So löschen Sie eine vorhandene Servergruppe

1.  Führen Sie einen der folgenden Schritte aus:

    -   Klicken Sie im Navigationsbereich Server-Manager mit der rechten Maustaste auf eine Server Gruppe, und klicken Sie dann auf **Server Gruppe löschen**.

    -   Öffnen Sie auf der Startseite der Server Gruppe das Menü **Aufgaben** auf der Kachel **Server** , und klicken Sie dann auf **Server Gruppe löschen**.

2.  Klicken Sie auf **Ja**, wenn Sie aufgefordert werden, das Löschen der Servergruppe zu bestätigen.

    > [!NOTE]
    > durch das Löschen einer Server Gruppe werden keine Server aus Server-Manager entfernt. Server, die in einer gelöschten Gruppe enthalten waren, bleiben in der Gruppe **Alle Server** im Serverpool erhalten.

3.  Klicken Sie nach dem Ändern der Gruppe auf **OK**.

## <a name="see-also"></a>Weitere Informationen
[fügen Sie Server-Manager
Server hinzu](add-servers-to-server-manager.md) [Server-Manager](server-manager.md)



