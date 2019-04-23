---
title: Namespacetyp auswählen
description: Dieser Artikel beschreibt, wie Sie einen Namespacetyp auswählen.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f83be7b2ec7dbe2383deb2d0a79e33d7c73f8849
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873801"
---
# <a name="choose-a-namespace-type"></a>Namespacetyp auswählen

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Wenn Sie einen Namespace erstellen, müssen Sie einen von zwei Namespacetypen auswählen: einen eigenständigen Namespace oder einen domänenbasierten Namespace. Wenn Sie einen domänenbasierten Namespace auswählen, müssen Sie außerdem einen Namespacemodus auswählen: Windows 2000 Server oder Windows Server 2008-Modus.

## <a name="choosing-a-namespace-type"></a>Auswählen eines Namespacetyps

Wählen Sie einen eigenständigen Namespace aus, wenn eine der folgenden Bedingungen für Ihre Umgebung zutrifft:

-   Ihre Organisation wird Active Directory Domain Services (AD DS) nicht verwendet werden.
-   Sie sollten einen Failovercluster zum Erhöhen der Verfügbarkeit der Namespace verwenden.
-   Sie müssen einen einzelnen Namespace mit mehr als 5.000 DFS-Ordner in einer Domäne zu erstellen, die nicht die Anforderungen für einen domänenbasierten Namespace (Windows Server 2008-Modus) entspricht, wie weiter unten in diesem Thema beschrieben.

> [!NOTE]
> Um die Größe des Namespaces zu überprüfen, klicken Sie mit der rechten Maustaste auf den Namespace in der Konsolenstruktur der DFS-Verwaltung und dann auf **Eigenschaften**, und zeigen Sie die Namespace-Größe im Dialogfeld **Namespace Eigenschaften** an. Weitere Informationen zur Skalierbarkeit von DFS-Namespaces, finden Sie auf der Microsoft-Website [Dateidienste](https://technet.microsoft.com/library/cc771548.aspx).

Wählen Sie einen domänenbasierten Namespace aus, wenn eine der folgenden Bedingungen für Ihre Umgebung zutrifft:

-   Sie sollten mehrere Namespaceserver zum Sichern der Verfügbarkeit des Namespaces verwenden.
-   Sie sollten den Namen des Namespaceservers vor den Benutzern ausblenden. Dies erleichtert das Ersetzen des Namespaceservers oder das Migrieren des Namespaces auf einen anderen Server.

## <a name="choosing-a-domain-based-namespace-mode"></a>Auswählen eines domänenbasierten Namespacemodus

Wenn Sie einen domänenbasierten Namespace auswählen, müssen Sie, ob die Windows 2000 Server oder die Windows Server 2008-Modus verwendet auswählen. Der Windows Server 2008-Modus umfasst Unterstützung für zugriffsbasierte Aufzählung und erhöhte Skalierbarkeit. Die Windows 2000 Server eingeführte domänenbasierten Namespace wird nun als "domänenbasierten Namespace (Windows 2000 Server-Modus)." bezeichnet

Um die Windows Server 2008-Modus zu verwenden, müssen die Domäne und des Namespace die folgenden Mindestanforderungen erfüllen:

-   Die Gesamtstruktur verwendet die Funktionsebene von Windows Server 2003 oder höher.
-   Die Domäne wird verwendet, die Windows Server 2008 oder eine höhere Funktionsebene der Domäne.
-   Alle Namespaceserver werden Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt.

Wenn Ihre Umgebung unterstützt wird, wählen Sie den Windows Server 2008-Modus, bei der Erstellung des neuen domänenbasierte Namespaces. Dieser Modus bietet zusätzliche Funktionen und die Skalierbarkeit und umgeht die Notwendigkeit mögliche, einen Namespace von der Windows 2000 Server-Modus migrieren.

Weitere Informationen zur Migration von eines Namespaces in den Windows Server 2008-Modus finden Sie unter [einen domänenbasierten Namespace zu Windows Server 2008-Modus migrieren](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).

Wenn Ihre Umgebung domänenbasierte Namespaces in Windows Server 2008-Modus nicht unterstützt, verwenden Sie den vorhandenen Windows 2000 Server-Modus für den Namespace ein.

## <a name="comparing-namespace-types-and-modes"></a>Vergleichen von Namespacetypen und -Modi

Die Merkmale der einzelnen Namespacetypen und Modi werden in der folgenden Tabelle beschrieben.

|Merkmal|Eigenständiger Namespace|Domänenbasierter Namespace (Windows Server 2000 Server-Modus) |Domänenbasierter Namespace (Windows Server 2008 Server Modus) | 
|---|---|---|---|
|Namespacepfad|\\\ *ServerName\RootName* |\\\ *NetBIOSDomainName\RootName* <br />\\\ *DNSDomainName\RootName*|\\\ *NetBIOSDomainName\RootName* <br /> \\\ *DNSDomainName\RootName*|
|Speicherort der Namespaceinformationen|In der Registrierung und in einem Speichercache auf dem Namespaceserver|In AD DS und in einem Speichercache auf jedem Namespaceserver|In AD DS und in einem Speichercache auf jedem Namespaceserver|
|Empfehlungen für die Größe des Namespaces|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. Die empfohlene Grenze beträgt 50.000 Ordner mit Zielen|Die Größe des Namespace-Objekts in AD DS sollte geringer als 5 Megabyte (MB) sein, um die Kompatibilität mit Domänencontrollern aufrecht zu erhalten, die nicht unter Windows Server 2008 ausgeführt werden. Dies bedeutet nicht mehr als ca. 5.000 Ordner mit Zielen.|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. Die empfohlene Grenze beträgt 50.000 Ordner mit Zielen |
|Minimale AD DS Gesamtstruktur-Funktionsebene|AD DS ist nicht erforderlich|Windows 2000|Windows Server 2003|
|Minimale AD DS Domän-Funktionsebene|AD DS ist nicht erforderlich|Windows 2000 im gemischten Modus|WindowsServer 2008|
|Minimale unterstützte Namespaceserver|Windows 2000 Server|Windows 2000 Server|WindowsServer 2008|
|Support für die zugriffsbasierte Aufzählung (falls aktiviert)|Ja, erfordert Windows Server 2008-Namespaceserver|Nein|Ja|
|Unterstützte Methoden zum Gewährleisten der Verfügbarkeit von Namespace|Erstellen Sie einen eigenständigen Namespace auf einem Failovercluster.|Verwenden Sie mehrerer Namespaceserver zum Hosten des Namespace. (Die Namespaceserver müssen in der gleichen Domäne sein.)|Verwenden Sie mehrerer Namespaceserver zum Hosten des Namespace. (Die Namespaceserver müssen in der gleichen Domäne sein.)|
|Unterstützung für die Verwendung der DFS-Replikation zum Replizieren von Ordnerzielen|Unterstützt, wenn einer AD DS-Domäne beigetreten|Unterstützt|Unterstützt|

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Migrieren Sie einen domänenbasierten Namespace zu Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


