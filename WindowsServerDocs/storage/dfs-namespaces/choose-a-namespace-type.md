---
title: Auswählen eines Namespacetyps
description: In diesem Artikel wird beschrieben, wie Sie einen Namespace-Typ auswählen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b4addd18629bd54cd9d5fc2df5c660c621e735de
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473787"
---
# <a name="choose-a-namespace-type"></a>Wählen Sie einen Namespace aus.

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Wenn Sie einen Namespace erstellen, müssen Sie einen von zwei Namespace Typen auswählen: einen eigenständigen Namespace oder einen domänenbasierten Namespace. Wenn Sie einen domänenbasierten Namespace auswählen, müssen Sie außerdem einen Namespace Modus auswählen: Windows 2000-Server Modus oder Windows Server 2008-Modus.

## <a name="choosing-a-namespace-type"></a>Auswählen eines Namespace Typs

Wählen Sie einen eigenständigen Namespace aus, wenn für Ihre Umgebung eine der folgenden Bedingungen zutrifft:

-   Ihre Organisation verwendet nicht Active Directory Domain Services (AD DS).
-   Sie möchten die Verfügbarkeit des Namespace mithilfe eines Failoverclusters erhöhen.
-   Sie müssen einen einzelnen Namespace mit mehr als 5.000 DFS-Ordnern in einer Domäne erstellen, die die Anforderungen für einen domänenbasierten Namespace (Windows Server 2008-Modus) nicht erfüllt, wie weiter unten in diesem Thema beschrieben.

> [!NOTE]
> Um die Größe eines Namespaces zu überprüfen, klicken Sie in der Struktur der DFS-Verwaltungskonsole mit der rechten Maustaste auf den Namespace, klicken Sie auf **Eigenschaften**, und zeigen Sie dann die Namespace Größe im Dialogfeld **Namespace Eigenschaften** an. Weitere Informationen zur Skalierbarkeit von DFS-Namespaces finden Sie in den Microsoft-Website- [Datei Diensten](https://technet.microsoft.com/library/cc771548.aspx).

Wählen Sie einen domänenbasierten Namespace aus, wenn für Ihre Umgebung eine der folgenden Bedingungen zutrifft:

-   Sie möchten sicherstellen, dass der Namespace mit mehreren Namespace Servern verfügbar ist.
-   Sie möchten den Namen des Namespace Servers vor Benutzern ausblenden. Dadurch wird der Namespace Server einfacher ersetzt oder der Namespace zu einem anderen Server migriert.

## <a name="choosing-a-domain-based-namespace-mode"></a>Auswählen eines domänenbasierten Namespace Modus

Wenn Sie einen domänenbasierten Namespace auswählen, müssen Sie auswählen, ob der Windows 2000-Server Modus oder der Windows Server 2008-Modus verwendet werden soll. Der Windows Server 2008-Modus bietet Unterstützung für die Zugriffs basierte Aufzählung und eine größere Skalierbarkeit. Der Domänen basierte Namespace, der in Windows Server Server 2000 eingeführt wurde, wird jetzt als "Domänen basierter Namespace (Windows 2000-Server Modus)" bezeichnet.

Um den Windows Server 2008-Modus zu verwenden, müssen die Domäne und der Namespace die folgenden Mindestanforderungen erfüllen:

-   Die Gesamtstruktur verwendet die Gesamtstruktur Funktionsebene Windows Server 2003 oder höher.
-   Die Domäne verwendet die Domänen Funktionsebene Windows Server 2008 oder höher.
-   Auf allen Namespace Servern wird Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt.

Wenn Sie von Ihrer Umgebung unterstützt wird, wählen Sie den Windows Server 2008-Modus aus, wenn Sie neue Domänen basierte Namespaces erstellen. Dieser Modus bietet zusätzliche Features und Skalierbarkeit und entfällt außerdem die Möglichkeit, einen Namespace aus dem Windows 2000-Server Modus zu migrieren.

Informationen zum Migrieren eines Namespaces zum Windows Server 2008-Modus finden Sie unter [Migrieren eines domänenbasierten Namespace zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).

Wenn Ihre Umgebung Domänen basierte Namespaces im Windows Server 2008-Modus nicht unterstützt, verwenden Sie den vorhandenen Windows 2000-Server Modus für den Namespace.

## <a name="comparing-namespace-types-and-modes"></a>Vergleichen von Namespace Typen und-Modi

Die Merkmale der einzelnen Namespacetyp und-Modi werden in der folgenden Tabelle beschrieben.

|Merkmal|Eigenständiger Namespace|Domänen basierter Namespace (Windows 2000-Server Modus) |Domänen basierter Namespace (Windows Server 2008-Modus) |
|---|---|---|---|
|Pfad zu Namespace|\\\ *Servername\rootname* |\\\ *Netbiosdomainname\rootname* <br />\\\ *Dnsdomainname\rootname*|\\\ *Netbiosdomainname\rootname* <br /> \\\ *Dnsdomainname\rootname*|
|Speicherort der Namespace Informationen|In der Registrierung und in einem Arbeitsspeicher Cache auf dem Namespace Server|In AD DS und in einem Arbeitsspeicher Cache auf jedem Namespace Server|In AD DS und in einem Arbeitsspeicher Cache auf jedem Namespace Server|
|Empfehlungen zur Namespace Größe|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. der empfohlene Grenzwert ist 50.000 Ordner mit Zielen.|Die Größe des Namespace Objekts in AD DS sollte kleiner als 5 Megabyte (MB) sein, um die Kompatibilität mit Domänen Controllern zu gewährleisten, auf denen nicht Windows Server 2008 ausgeführt wird. Dies bedeutet, dass nicht mehr als ungefähr 5.000 Ordner mit Zielen.|Der Namespace kann mehr als 5.000 Ordner mit Zielen enthalten. der empfohlene Grenzwert ist 50.000 Ordner mit Zielen. |
|Minimale AD DS Gesamtstruktur Funktionsebene|AD DS ist nicht erforderlich.|Windows 2000|Windows Server 2003|
|Minimale AD DS Domänen Funktionsebene|AD DS ist nicht erforderlich.|Windows 2000 im gemischten Modus bezeichnet|Windows Server 2008|
|Mindestens unterstützte Namespace Server|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|Unterstützung für die Zugriffs basierte Enumeration (sofern aktiviert)|Ja, erfordert Windows Server 2008-Namespace Server|Nein|Ja|
|Unterstützte Methoden zum Sicherstellen der Namespace Verfügbarkeit|Erstellen Sie einen eigenständigen Namespace auf einem Failovercluster.|Verwenden Sie mehrere Namespace Server, um den Namespace zu hosten. (Die Namespace Server müssen sich in der gleichen Domäne befinden.)|Verwenden Sie mehrere Namespace Server, um den Namespace zu hosten. (Die Namespace Server müssen sich in der gleichen Domäne befinden.)|
|Unterstützung für die Verwendung DFS-Replikation zum Replizieren von Ordner Zielen|Unterstützt, wenn einer AD DS Domäne hinzugefügt wird|Unterstützt|Unterstützt|

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Migrieren Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


