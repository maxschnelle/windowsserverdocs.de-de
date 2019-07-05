---
title: Verwalten virtueller Festplatten (Virtual Hard Disk, VHD)
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten virtueller Festplatten.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2e371710752d59ebc7a1f8aa2dad3d9189872c47
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63751753"
---
# <a name="manage-virtual-hard-disks-vhd"></a>Verwalten virtueller Festplatten (Virtual Hard Disk, VHD)

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema beschreibt die Vorgehensweise beim Erstellen, Hinzufügen und Trennen virtueller Festplatten mit der Datenträgerverwaltung. Virtuelle Festplatten (VHDs) sind virtuelle Festplattendateien, die nach ihrer Einbindung in etwa wie eine physische Festplatte angezeigt und verwendet werden. Sie werden am häufigsten mit virtuellen Hyper-V-Computern verwendet. 

## <a name="viewing-vhds-in-disk-management"></a>Anzeigen von VHDs in der Datenträgerverwaltung

VHDs werden in der Datenträgerverwaltung genau wie physische Datenträger angezeigt. Wenn eine virtuelle Festplatte angefügt wurde (d. h., wenn sie im System für die Verwendung verfügbar gemacht wurde), wird sie blau dargestellt. Wenn die Festplatte getrennt ist (d. h., wenn sie nicht verfügbar ist), wird das zugehörige Symbol grau dargestellt.

## <a name="creating-a-vhd"></a>Erstellen einer VHD

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

**So erstellst du eine virtuelle Festplatte**

1.  Wähle im Menü **Aktion** die Option **VHD erstellen** aus.

2.  Gib im Dialogfeld **Erstellen und Anfügen einer virtuellen Festplatte** sowohl den Speicherort auf dem physischen Computer, auf dem die VHD-Datei gespeichert werden soll, als auch die Größe der virtuellen Festplatte an.

3.  Wählen Sie unter **Format der virtuellen Festplatte** die Option **Dynamisch erweiterbar** oder **Feste Größe** aus, und klicken Sie dann auf **OK**.

## <a name="attaching-and-detaching-a-vhd"></a>Anfügen und Trennen einer VHD

So machst du eine virtuelle Festplatte für die Verwendung verfügbar (entweder eine soeben erstellte oder eine andere vorhandene virtuelle Festplatte): 

1. Wähle im Menü **Aktion** die Option **Virtuelle Festplatte anfügen** aus.

2. Gib den Speicherort der virtuellen Festplatte unter Verwendung des vollständig qualifizierten Pfads an.

Wenn du die virtuelle Festplatte trennen möchtest, hebe ihre Verfügbarkeit auf: Klicke mit der rechten Maustaste auf den Datenträger, und wähle **Virtuelle Festplatte trennen** und dann **OK** aus. Beim Trennen einer virtuellen Festplatte wird weder die virtuelle Festplatte noch werden die darauf gespeicherte Daten gelöscht.

## <a name="additional-considerations"></a>Weitere Aspekte

-   Der Pfad zur Angabe des Speicherorts für die virtuelle Festplatte muss vollständig qualifiziert sein und kann sich nicht im Verzeichnis „\\Windows“ befinden.
-   Die Mindestgröße für eine virtuelle Festplatte beträgt 3 Megabyte (MB).
-   Eine virtuelle Festplatte kann nur eine Basisfestplatte sein.
-   Da eine virtuelle Festplatte bei der Erstellung initialisiert wird, kann das Erstellen einer virtuellen Festplatten mit fester Größe einige Zeit dauern.
