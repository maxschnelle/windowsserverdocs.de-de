---
title: Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung
description: In diesem Artikel wird beschrieben, wie geerbte Berechtigungen mit Zugriffs basierter Enumeration verwendet werden.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 112ec4363177ac6dd560493843c8937bdfbac4de
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475147"
---
# <a name="using-inherited-permissions-with-access-based-enumeration"></a>Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Standardmäßig werden die Berechtigungen, die für einen DFS-Ordner verwendet werden, vom lokalen Dateisystem des Namespace Servers geerbt. Die Berechtigungen werden vom Stammverzeichnis des System Laufwerks geerbt und gewähren der Domänen \\ Benutzergruppe Leseberechtigungen. Folglich bleiben alle Ordner im-Namespace auch nach der Aktivierung der Zugriffs basierten Enumeration für alle Domänen Benutzer sichtbar.

## <a name="advantages-and-limitations-of-inherited-permissions"></a>Vorteile und Einschränkungen von geerbten Berechtigungen

Es gibt zwei Hauptvorteile bei der Verwendung von geerbten Berechtigungen, um zu steuern, welche Benutzerordner in einem DFS-Namespace anzeigen können:

-   Sie können geerbte Berechtigungen schnell auf viele Ordner anwenden, ohne Skripts verwenden zu müssen.
-   Sie können geerbte Berechtigungen auf Namespace Stämme und Ordner ohne Ziele anwenden.

Trotz der Vorteile haben geerbte Berechtigungen in DFS-Namespaces viele Einschränkungen, die Sie für die meisten Umgebungen ungeeignet machen:

-   Änderungen an geerbten Berechtigungen werden nicht auf andere Namespace Server repliziert. Verwenden Sie daher geerbte Berechtigungen nur für eigenständige Namespaces oder Umgebungen, in denen Sie ein Replikationssystem eines Drittanbieters implementieren können, um die Access Control Listen (ACLs) auf allen Namespace Servern zu synchronisieren.
-   Die DFS-Verwaltung und **dfsutil** können geerbte Berechtigungen nicht anzeigen oder ändern. Daher müssen Sie Windows-Explorer oder den **icacls** -Befehl zusätzlich zur DFS-Verwaltung oder **dfsutil** verwenden, um den-Namespace zu verwalten.
-   Wenn Sie geerbte Berechtigungen verwenden, können Sie die Berechtigungen eines Ordners mit Zielen nur dann ändern, wenn Sie den **dfsutil** -Befehl verwenden. DFS-Namespaces entfernt automatisch Berechtigungen aus Ordnern mit Zielen, die mit anderen Tools oder Methoden festgelegt wurden.
-   Wenn Sie Berechtigungen für einen Ordner mit Zielen festlegen, während Sie geerbte Berechtigungen verwenden, kombiniert die ACL, die Sie für den Ordner mit Zielen festlegen, mit geerbten Berechtigungen aus dem übergeordneten Element des Ordners im Dateisystem. Sie müssen beide Berechtigungs Sätze überprüfen, um zu bestimmen, was die Netto Berechtigungen sind.

> [!NOTE]
> Wenn geerbte Berechtigungen verwendet werden, ist es am einfachsten, Berechtigungen für Namespace Stämme und Ordner ohne Ziele festzulegen. Verwenden Sie dann geerbte Berechtigungen für Ordner mit Zielen, damit Sie alle Berechtigungen von ihren übergeordneten Elementen erben.

## <a name="using-inherited-permissions"></a>Verwenden von geerbten Berechtigungen

Um einzuschränken, welche Benutzer einen DFS-Ordner anzeigen können, müssen Sie eine der folgenden Aufgaben ausführen:

-   **Legen Sie explizite Berechtigungen für den Ordner fest, und deaktivieren Sie die Vererbung.** Informationen zum Festlegen von expliziten Berechtigungen für einen Ordner mit Zielen (ein Link) mithilfe der DFS-Verwaltung oder des **dfsutil** -Befehls finden Sie unter [Aktivieren der Zugriffs basierten Enumeration für einen Namespace](enable-access-based-enumeration-on-a-namespace.md).
-   **Ändern Sie geerbte Berechtigungen für das übergeordnete Element im lokalen Dateisystem**. Wenn Sie die Berechtigungen ändern möchten, die von einem Ordner mit Zielen geerbt wurden, können Sie, wenn Sie bereits explizite Berechtigungen für den Ordner festgelegt haben, zu geerbten Berechtigungen von expliziten Berechtigungen wechseln, wie im folgenden Verfahren erläutert. Verwenden Sie dann Windows-Explorer oder den Befehl **icacls** , um die Berechtigungen des Ordners zu ändern, von dem der Ordner mit Zielen seine Berechtigungen erbt.

> [!NOTE]
> Die Zugriffs basierte Enumeration verhindert nicht, dass Benutzer einen Verweis auf ein Ordner Ziel erhalten, wenn Sie den DFS-Pfad des Ordners mit den Zielen bereits kennen. Berechtigungen, die mit Windows Explorer oder dem Befehl **icacls** für Namespace Stämme oder Ordner ohne Ziele festgelegt wurden, Steuern, ob Benutzer auf den DFS-Ordner oder den Namespace Stamm zugreifen können. Allerdings wird nicht verhindert, dass Benutzer direkt auf einen Ordner mit Zielen zugreifen. Nur die Freigabe Berechtigungen oder die NTFS-Dateisystem Berechtigungen des freigegebenen Ordners selbst können verhindern, dass Benutzer auf die Ordner Ziele zugreifen.

## <a name="to-switch-from-explicit-permissions-to-inherited-permissions"></a>So wechseln Sie von expliziten Berechtigungen zu geerbten Berechtigungen

1.  Suchen Sie in der Konsolen Struktur unter dem Knoten **Namespaces** den Ordner mit Zielen, deren Sichtbarkeit Sie steuern möchten, klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert**.

3.  Klicken Sie im **lokalen Dateisystem auf geerbte Berechtigungen verwenden** , und klicken Sie dann im Dialogfeld **Verwendung von geerbten Berechtigungen bestätigen** auf **OK** . Dadurch werden alle explizit festgelegten Berechtigungen für diesen Ordner entfernt, und die geerbten NTFS-Berechtigungen werden aus dem lokalen Dateisystem des Namespace Servers wieder hergestellt.

4.  Verwenden Sie Windows-Explorer oder den Befehl **icacls** , um die geerbten Berechtigungen für Ordner oder Namespace Stämme in einem DFS-Namespace zu ändern.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)