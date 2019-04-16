---
title: "Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung"
description: "In diesem Artikel wird beschrieben, wie Sie vererbte Berechtigungen mit zugriffsbasierten Aufzählungen verwenden"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e8210a6abede3a8ee5317e5b6b2a90bd17013fc4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="using-inherited-permissions-with-access-based-enumeration"></a>Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Standardmäßig werden die Berechtigungen für einen DFS-Ordner vom lokalen Dateisystem des Namespaceservers geerbt. Die Berechtigungen werden aus dem Stammverzeichnis des Systemlaufwerks geerbt und erteilen der DOMAIN\\Anwendergruppe die Berechtigung zum Lesen. Daher bleiben auch nach der Aktivierung der zugriffsbasierten Aufzählung alle Ordner im Namespace für alle Domänenbenutzer sichtbar.

## <a name="advantages-and-limitations-of-inherited-permissions"></a>Vor- und Nachteile der geerbten Berechtigungen

Es gibt zwei Hauptvorteile für die Kontrolle geerbter Berechtigungen, um zu bestimmen, welche Benutzer Ordner in einem DFS-Namespace sehen können oder nicht:

-   Sie können mehreren Ordnern schnell vererbte Berechtigungen zuweisen, ohne Skripts zu verwenden.
-   Sie können vererbte Berechtigungen auf Namespacestämme und Ordner ohne Ziele anwenden.

Trotz der Vorteile haben vererbte Berechtigungen in DFS-Namespaces viele Einschränkungen, die nicht für die meisten Umgebungen geeignet sind:

-   Änderungen für geerbte Berechtigungen werden nicht in anderen Namespaceservern repliziert. Verwenden Sie daher vererbte Berechtigungen nur für eigenständige Namespaces oder in Umgebungen, in denen Sie ein Drittanbieter-Replikationssystem implementieren können, um die Zugriffssteuerungslisten (ACLs) auf allen Namespaceservern zu synchronisieren.
-   DFS-Verwaltung und **Dfsutil** können keine geerbten Berechtigungen anzeigen oder ändern. Aus diesem Grund müssen Sie Windows-Explorer oder den Befehl **Icacls** zusätzlich zur DFS-Verwaltung oder **Dfsutil** verwenden, um den Namespace zu verwalten.
-   Wenn Sie geerbte Berechtigungen verwenden, können Sie die Berechtigungen für einen Ordner mit Zielen nicht ändern, es sei denn, Sie verwenden den Befehl **Dfsutil**. DFS-Namespaces entfernt automatisch Berechtigungen vom Ordner mit Zielen, die über andere Tools und Methoden festgelegt wurden.
-   Wenn Sie Berechtigungen für einen Ordner mit Zielen während der Verwendung von geerbten Berechtigungen festlegen, kombiniert die ACL, die Sie für den Ordner mit Zielen festlegen, die geerbten Berechtigungen vom übergeordneten Element des Ordners im Dateisystem. Sie müssen beide Berechtigungensätze untersuchen, um zu bestimmen, welche Berechtigungen gelten.

> [!NOTE]
> Wenn Sie geerbte Berechtigungen verwenden, ist es am einfachsten, Berechtigungen für Namespacestämme und Ordner ohne Ziele festzulegen. Verwenden Sie dann geerbte Berechtigungen für Ordner mit Zielen, damit sie alle Berechtigungen von ihren übergeordneten Elementen erben.

## <a name="using-inherited-permissions"></a>Verwenden von geerbten Berechtigungen

Um einzuschränken, welche Benutzer einen DFS-Ordner anzeigen können, müssen Sie eine der folgenden Aufgaben ausführen:

-   **Legen Sie explizite Berechtigungen für den Ordner fest, und deaktivieren Sie die Vererbung.** Um explizite Berechtigungen für einen Ordner mit Zielen (Links) mithilfe der DFS-Verwaltung oder **Dfsutil** festzulegen, lesen Sie weitere Informationen unter [Aktivieren der zugriffsbasierten Aufzählung für einen Namespace](enable-access-based-enumeration-on-a-namespace.md).
-   **Ändern von geerbten Berechtigungen um übergeordneten Element des lokalen Dateisystems**. Um die geerbten Berechtigungen eines Ordners mit Zielen zu ändern, wenn Sie bereits explizite Berechtigungen für den Ordner festgelegt haben, wechseln Sie zu geerbten Berechtigungen von expliziten Berechtigungen, wie im folgenden Verfahren beschrieben. Verwenden Sie anschließend Windows Explorer oder den Befehl **Icacls**, um die Berechtigungen des Ordners zu ändern, von dem der Ordner mit Zielen seine Berechtigungen erbt.

> [!NOTE]
> Benutzer können trotz der zugriffsbasierten einen Verweis auf ein Ordnerziel abrufen, wenn sie den DFS-Pfad des Ordners mit Zielen bereits kennen. Berechtigungen, die mithilfe von Windows-Explorer oder dem Befehl **Icacls** im Namespacestammverzeichniss oder Ordner ohne Steuerung der Ziele festgelegt wurden steuern, wie Benutzer auf den DFS-Ordner oder Namespacestamm zugreifen können. Allerdings verhindern sie nicht, dass Benutzer einen direkten Zugriff auf einen Ordner mit Zielen haben. Nur die Freigabeberechtigungen oder die NTFS-Dateisystemberechtigungen für den freigegebenen Ordner selbst kann verhindern, dass Benutzer den Zugriff auf Ordnerziele erhalten.

## <a name="to-switch-from-explicit-permissions-to-inherited-permissions"></a>So Wechseln Sie von expliziten Berechtigungen auf geerbte Berechtigungen

1.  Suchen Sie in der Konsolenstruktur unter dem **Namespaces** Knoten den Ordner mit den Zielen, für die Sie die Sichtbarkeit steuern möchten, klicken Sie mit der rechten Maustaste auf den Ordner und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert**.

3.  Klicken Sie auf **Vererbte Berechtigungen aus dem lokalen Dateisystem verwenden** und klicken Sie dann auf **OK** im Dialogfeld **Verwenden von vererbten Berechtigungen bestätigen**. Auf diese Weise werden alle explizit festgelegten Berechtigungen für diesen Ordner entfernt und die vererbten NTFS-Berechtigungen aus dem lokalen Dateisystem des Namespaceservers wiederhergestellt.

4.  Um die geerbten Berechtigungen für Ordner oder Namespacestämme in einem DFS-Namespace zu ändern, verwenden Sie Windows-Explorer oder den Befehl **ICacls**.

## <a name="see-also"></a>Weitere Informationen:

-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)