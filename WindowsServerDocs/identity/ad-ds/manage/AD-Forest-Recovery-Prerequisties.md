---
title: Voraussetzungen für die Planung der Active Directory Gesamtstruktur Wiederherstellung
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 6dcd1185ba4d4c847cfe212f78ccc9661fd2aead
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823783"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Erforderliche Wiederherstellungs Voraussetzungen für Active Directory

> Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Im folgenden Dokument werden die Voraussetzungen erläutert, mit denen Sie vertraut sein sollten, bevor Sie einen Wiederherstellungs Plan für die Gesamtstruktur oder eine Wiederherstellung

## <a name="assumptions-for-using-this-guide"></a>Annahmen zur Verwendung dieses Handbuchs

1. Sie haben mit einem Microsoft-Support Professional gearbeitet und:
   - Die Ursache für den Gesamtstruktur weiten Ausfall wurde ermittelt. In dieser Anleitung wird nicht der Fehler ausgelöst, oder es werden Prozeduren empfohlen, um den Fehler zu verhindern.
   - Alle möglichen Abhilfemaßnahmen wurden ausgewertet.  
   - In Abstimmung mit Microsoft-Support wurde eine vollständige Wiederherstellung der gesamten Gesamtstruktur in den Zustand vor dem Auftreten des Fehlers empfohlen. In vielen Fällen sollte die Wiederherstellung der Gesamtstruktur die letzte Option sein.

1. Sie haben die bewährten Microsoft-Empfehlungen für die Verwendung von Active Directory – Integrated Domain Name System (DNS) befolgt. Insbesondere sollte für jede Active Directory Domäne eine Active Directory integrierte DNS-Zone vorhanden sein.
   - Wenn dies nicht der Fall ist, können Sie weiterhin die grundlegenden Prinzipien dieses Handbuchs zum Durchführen der Wiederherstellung in der Gesamtstruktur verwenden. Sie müssen jedoch bestimmte Maßnahmen für die DNS-Wiederherstellung basierend auf Ihrer eigenen Umgebung ausführen. Weitere Informationen zum Verwenden von Active Directory – Integrated DNS finden Sie unter [Erstellen eines DNS-Infrastruktur Entwurfs](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).

1. Obwohl dieses Handbuch als allgemeine Richtlinie für die Wiederherstellung in der Gesamtstruktur gedacht ist, werden nicht alle möglichen Szenarien behandelt. Ab Windows Server 2008 gibt es beispielsweise eine Server Core-Version, die eine Vollversion von Windows Server ist, aber ohne eine vollständige GUI. Obwohl es durchaus möglich ist, eine Gesamtstruktur wiederherzustellen, die aus nur DCS besteht, auf denen Server Core ausgeführt wird, enthält dieses Handbuch keine detaillierten Anweisungen. Basierend auf den hier beschriebenen Anleitungen können Sie jedoch die erforderlichen Befehlszeilen Aktionen selbst entwerfen.  

> [!NOTE]
> Obwohl die Ziele dieses Leitfadens in der Wiederherstellung der Gesamtstruktur und der Wartung oder Wiederherstellung vollständiger DNS-Funktionen sind, kann die Wiederherstellung zu einer DNS-Konfiguration führen, die vor dem Auftreten des Fehlers von der Konfiguration geändert Nachdem die Gesamtstruktur wieder hergestellt wurde, können Sie die ursprüngliche DNS-Konfiguration wiederherstellen. In den Empfehlungen in diesem Handbuch wird nicht beschrieben, wie DNS-Server für die Namensauflösung anderer Teile des Unternehmens Namespace konfiguriert werden, in denen DNS-Zonen vorhanden sind, die nicht in AD DS gespeichert sind.  

## <a name="concepts-for-using-this-guide"></a>Konzepte für die Verwendung dieses Handbuchs

Bevor Sie mit der Planung der Wiederherstellung einer Active Directory Gesamtstruktur beginnen, sollten Sie mit folgenden Informationen vertraut sein:  
  
- Grundlegende Active Directory Konzepte  
- Die Wichtigkeit von Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet). Diese Rollen umfassen Folgendes:  
  - Schema Master
  - Domänen Namen Master
  - Relative ID (RID)-Master
  - Emulator-Master des primären Domänen Controllers (PDC)
  - Infrastruktur Master

Außerdem sollten Sie in regelmäßigen Abständen AD DS und SYSVOL in einer Lab-Umgebung gesichert und wieder hergestellt haben. Weitere Informationen finden Sie unter [Sichern der System Statusdaten](AD-Forest-Recovery-Procedures.md) und [Durchführen einer nicht autoritativen Wiederherstellung Active Directory Domain Services](AD-Forest-Recovery-Procedures.md).

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)

> [!div class="nextstepaction"]
> [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)

> [!div class="nextstepaction"]
> [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)

> [!div class="nextstepaction"]
> [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)

> [!div class="nextstepaction"]
> [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)

> [!div class="nextstepaction"]
> [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)

> [!div class="nextstepaction"]
> [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)

> [!div class="nextstepaction"]
> [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)

> [!div class="nextstepaction"]
> [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)
