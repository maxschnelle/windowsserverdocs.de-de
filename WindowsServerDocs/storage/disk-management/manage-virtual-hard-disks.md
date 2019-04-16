---
title: Verwalten virtueller Festplatten (VHD)
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten virtueller Festplatten.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2e371710752d59ebc7a1f8aa2dad3d9189872c47
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="manage-virtual-hard-disks-vhd"></a>Verwalten virtueller Festplatten (VHD)

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema beschreibt die Vorgehensweise beim Erstellen, Hinzufügen und Trennen virtueller Festplatten mit der Datenträgerverwaltung. Virtuelle Festplatten (VHDs) sind virtuelle Festplattendateien, die, sobald Sie bereitgestellt sind, mehr oder weniger wie eine physische Festplatte aussehen und sich verhalten. Sie werden am häufigsten mit Hyper-V-Computern verwendet. 

## <a name="viewing-vhds-in-disk-management"></a>VHDs in der Datenträgerverwaltung ansehen

VHDs sehen genau wie physische Datenträger in der Datenträgerverwaltung aus. Wenn eine virtuelle Festplatte angefügt wurde (d. h. im System für die Verwendung verfügbar gemacht wurde), wird sie blau dargestellt. Wenn die Festplatte getrennt ist (d. h. nicht zur Verfügung gestellt wird), wird das zugehörige Symbol grau dargestellt.

## <a name="creating-a-vhd"></a>Erstellen einer virtuellen Festplatte

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

**So erstellen Sie eine virtuelle Festplatte**

1.  Klicken Sie im Menü **Aktion** auf **VHD erstellen**.

2.  Geben Sie im Dialogfeld **Erstellen und Anfügen einer virtuellen Festplatte** sowohl den Speicherort auf dem physischen Computer, auf dem die VHD-Datei gespeichert werden soll, als auch die Größe der virtuellen Festplatte an.

3.  Wählen Sie unter **Format der virtuellen Festplatte** die Option **Dynamisch erweiterbar** oder **Feste Größe** aus, und klicken Sie dann auf **OK**.

## <a name="attaching-and-detaching-a-vhd"></a>Anfügen und Trennen einer virtuellen Festplatte

So machen Sie eine virtuelle Festplatte für die Verwendung verfügbar (entweder eine existierende oder eine andere vorhandene virtuelle Festplatte): 

1. Wählen Sie im Menü **Aktion** die Option **VHD auswählen** aus.

2. Geben Sie den vollständigen Pfad zum Standort der VHD an.

Trennen Sie die virtuelle Festplatte, indem Sie diese nicht verfügbar machen: Klicken Sie mit der rechten Maustaste auf den Datenträger, und wählen Sie **virtuelle Festplatte trennen** aus und klicken Sie dann auf **OK**. Das Trennen einer virtuellen Festplatte löscht nicht die virtuelle Festplatte oder die darin gespeicherten Daten.

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Der Pfad zur Angabe des Speicherort für die virtuelle Festplatte muss vollständig qualifiziert sein und kann sich nicht im Verzeichnis \\Windows-Verzeichnis befinden.
-   Die Mindestgröße für eine virtuelle Festplatte ist 3 Megabyte (MB).
-   Eine virtuelle Festplatte kann nur ein Basisdatenträger sein.
-   Da die virtuelle Festplatte bei der Erstellung initialisiert wird, kann das Erstellen einer virtuelle Festplatten mit fester Größe einige Zeit dauern.
