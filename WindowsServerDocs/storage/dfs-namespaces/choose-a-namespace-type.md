---
title: "Namespacetyp auswählen"
description: "Dieser Artikel beschreibt, wie Sie einen Namespacetyp auswählen."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: eb471b5bf4e12a05b36973eb1ea5350469f6acd5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="choose-a-namespace-type"></a>Namespacetyp auswählen

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Wenn Sie einen Namespace erstellen, müssen Sie einen von zwei Namespacetypen auswählen: einen eigenständigen Namespace oder einen domänenbasierten Namespace. Darüber hinaus müssen Sie bei der Auswahl eines domänenbasierten Namespaces einen Namespacemodus auswählen: Windows2000 Server-Modus oder Windows Server2008-Modus.

## <a name="choosing-a-namespace-type"></a>Auswählen eines Namespacetyps

Wählen Sie einen eigenständigen Namespace aus, wenn eine der folgenden Bedingungen für Ihre Umgebung zutrifft:

-   Ihre Organisation verwendet keine Active Directory Domain Services (AD DS).
-   Sie sollten einen Failovercluster zum Erhöhen der Verfügbarkeit der Namespace verwenden.
-   Sie müssen einen einzigen Namespace mit mehr als 5.000 DFS-Ordnern in einer Domäne erstellen, die die Anforderungen für einen domänenbasierten Namespace (Windows Server2008-Modus) nicht erfüllt, wie weiter unten in diesem Thema beschrieben.

> [!NOTE]
> Um die Größe des Namespaces zu überprüfen, klicken Sie mit der rechten Maustaste auf den Namespace in der Konsolenstruktur der DFS-Verwaltung und dann auf **Eigenschaften**, und zeigen Sie die Namespace-Größe im Dialogfeld **Namespace Eigenschaften** an. Weitere Informationen zur Skalierbarkeit von DFS-Namespaces, finden Sie auf der Microsoft-Website [Dateidienste](https://technet.microsoft.com/library/cc771548.aspx).

Wählen Sie einen domänenbasierten Namespace aus, wenn eine der folgenden Bedingungen für Ihre Umgebung zutrifft:

-   Sie sollten mehrere Namespaceserver zum Sichern der Verfügbarkeit des Namespaces verwenden.
-   Sie sollten den Namen des Namespaceservers vor den Benutzern ausblenden. Dies erleichtert das Ersetzen des Namespaceservers oder das Migrieren des Namespaces auf einen anderen Server.

## <a name="choosing-a-domain-based-namespace-mode"></a>Auswählen eines domänenbasierten Namespacemodus

Sie müssen bei der Auswahl eines domänenbasierten Namespaces entscheiden, ob Sie Windows2000 Server-Modus oder Windows Server2008-Modus verwenden. Der Windows Server2008-Modus unterstützt Support für die zugriffsbasierte Aufzählung und eine bessere Skalierbarkeit. Der domänenbasierte Namespace, der in Windows2000 Server eingeführt wurde, wird jetzt als "domänenbasierter Namespace (Windows2000 Server-Modus)" bezeichnet.

Um den Windows Server2008-Modus zu verwenden, müssen die Domäne und der Namespace die folgenden Mindestanforderungen erfüllen:

-   Die Gesamtstruktur verwendet die Funktionsebene von WindowsServer2003 oder höher.
-   Die Domäne verwendet die Funktionsebene von WindowsServer2008 oder höher.
-   Alle Namespaceserver verwenden Windows Server2012 R2, Windows Server2012, Windows Server2008 R2 oder Windows Server2008.

Wenn Ihre Umgebung dies unterstützt, wählen Sie den Windows Server2008-Modus bei der Erstellung des neuen domänenbasierten Namespaces aus. Dieser Modus bietet zusätzliche Features und Skalierbarkeiten. Außerdem entfällt die notwendige Migration des Namespaces aus dem Windows2000 Server-Modus.

Informationen zum Migrieren eines Namespaces zum Windows Server2008-Modus finden Sie unter [Migrieren eines domänenbasierten Namespaces zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).

Wenn Ihre Umgebung keine domänenbasierten Namespaces im Windows Server2008-Modus unterstützt, verwenden Sie den vorhandenen Windows2000 Server-Modus für den Namespace.

## <a name="comparing-namespace-types-and-modes"></a>Vergleichen von Namespacetypen und -Modi

Die Merkmale der einzelnen Namespacetypen und Modi werden in der folgenden Tabelle beschrieben.

|Merkmal|Eigenständiger Namespace|Domänenbasierter Namespace (Windows Server2000 Server-Modus) |Domänenbasierter Namespace (Windows Server2008 Server Modus) | 
|---|---|---|---|
|Namespacepfad|\\\ *ServerName\RootName* |\\\ *NetBIOSDomainName\RootName* <br />\\\ *DNSDomainName\RootName*|\\\ *NetBIOSDomainName\RootName* <br /> \\\ *DNSDomainName\RootName*|
|Speicherort der Namespaceinformationen|In der Registrierung und in einem Speichercache auf dem Namespaceserver|In AD DS und in einem Speichercache auf jedem Namespaceserver|In AD DS und in einem Speichercache auf jedem Namespaceserver|
|Empfehlungen für die Größe des Namespaces|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. Die empfohlene Grenze beträgt 50.000 Ordner mit Zielen|Die Größe des Namespace-Objekts in AD DS sollte geringer als 5 Megabyte (MB) sein, um die Kompatibilität mit Domänencontrollern aufrecht zu erhalten, die nicht unter Windows Server2008 ausgeführt werden. Dies bedeutet nicht mehr als ca. 5.000 Ordner mit Zielen.|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. Die empfohlene Grenze beträgt 50.000 Ordner mit Zielen |
|Minimale AD DS Gesamtstruktur-Funktionsebene|AD DS ist nicht erforderlich|Windows 2000|Windows Server 2003|
|Minimale AD DS Domän-Funktionsebene|AD DS ist nicht erforderlich|Windows2000 im gemischten Modus|Windows Server 2008|
|Minimale unterstützte Namespaceserver|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|Support für die zugriffsbasierte Aufzählung (falls aktiviert)|Ja, erfordert Windows Server2008-Namespaceserver|Nein|Ja|
|Unterstützte Methoden zum Gewährleisten der Verfügbarkeit von Namespace|Erstellen Sie einen eigenständigen Namespace auf einem Failovercluster.|Verwenden Sie mehrerer Namespaceserver zum Hosten des Namespace. (Die Namespaceserver müssen in der gleichen Domäne sein.)|Verwenden Sie mehrerer Namespaceserver zum Hosten des Namespace. (Die Namespaceserver müssen in der gleichen Domäne sein.)|
|Unterstützung für die Verwendung der DFS-Replikation zum Replizieren von Ordnerzielen|Unterstützt, wenn einer AD DS-Domäne beigetreten|Unterstützt|Unterstützt|

## <a name="see-also"></a>Weitere Informationen:

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Migrieren Sie einen domänenbasierten Namespace zum Windows Server2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


