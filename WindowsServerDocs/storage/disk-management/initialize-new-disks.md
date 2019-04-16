---
title: "Initialisieren neuer Datenträger"
description: "In diesem Artikel wird beschrieben, wie neue Datenträger initialisiert werden"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 587553746d45eceab654efd4d120038088d32991
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="initialize-new-disks"></a>Initialisieren neuer Datenträger

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

## <a name="to-initialize-new-disks"></a>So initialisieren Sie neue Datenträger
1.  Klicken Sie in der Datenträgerverwaltung mit der rechten Maustaste auf den zu initialisierenden Datenträger, und klicken Sie dann auf **Datenträgerinitialisierung**.

2.  Wählen Sie im Dialogfeld **Datenträgerinitialisierung** den oder die zu initialisierenden Datenträger aus. Sie können wählen, ob Sie den MBR-Partitionsstil (Master Boot Record) oder den GPT-Partitionsstil (GUID-Partitionstabelle) verwenden möchten.

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Neue Datenträger erscheinen als **nicht initialisiert**. Bevor Sie einen Datenträger verwenden können, müssen Sie ihn zuerst initialisieren. Wenn Sie nach dem Hinzufügen eines Datenträgers die Datenträgerverwaltung starten, erscheint der Assistent zum Initialisieren von Datenträgern, damit Sie den Datenträger initialisieren können.

> [!NOTE]
> Der neue Datenträger wird als Basisdatenträger initialisiert.

