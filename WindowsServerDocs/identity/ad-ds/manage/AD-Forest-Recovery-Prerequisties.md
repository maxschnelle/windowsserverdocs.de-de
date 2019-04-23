---
title: Voraussetzungen für die Planung für die Wiederherstellung der Active Directory-Gesamtstruktur
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: c8945dd5ccccb27826dd96413b56a070a7452789
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842171"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Voraussetzungen für die Active Directory-Gesamtstruktur Recovery

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Das folgende Dokument erläutert die Voraussetzungen, denen Sie vor dem Ausarbeiten eines Wiederherstellungsplans für die Gesamtstruktur oder es wird versucht, eine Wiederherstellung mit vertraut sein sollten.

## <a name="assumptions-for-using-this-guide"></a>Annahmen für die Verwendung dieses Leitfadens

1. Jetzt haben Sie einen Microsoft-Support-Experten und:
   - Bestimmen der Ursache des Fehlers Gesamtstruktur. Dieses Handbuch nicht vorschlagen eine Ursache des Fehlers oder wird empfohlen, alle Verfahren, um den Fehler zu vermeiden.
   - Bewertet die möglichen Abhilfen.  
   - Hat ergeben, in Abstimmung mit den Microsoft Support ist, Wiederherstellen der gesamten Struktur auf den Zustand vor der Fehler aufgetreten ist die beste Möglichkeit, nach dem Fehler wiederhergestellt. In vielen Fällen sollte die Wiederherstellung der Gesamtstruktur die letzte Option sein.

2. Dass Sie die Microsoft Best Practice-Empfehlungen für die Verwendung von Active Directory-integrierte System DNS (Domain Name) ausgeführt haben. Insbesondere sollte eine Active Directory-integrierte DNS-Zone für jede Active Directory-Domäne vorhanden sein. 
   - Wenn dies nicht der Fall ist, weiterhin können die grundlegenden Prinzipien dieses Handbuchs Sie Wiederherstellung der Gesamtstruktur ausführen. Allerdings müssen Sie bestimmte Maßnahmen für die DNS-Wiederherstellung basierend auf Ihrer eigenen Umgebung ausführen. Weitere Informationen zur Verwendung von Active Directory-integrierte DNS finden Sie unter [erstellen einen DNS-Infrastruktur-Entwurf](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).

3. Obwohl dieses Handbuch als eine allgemeine Anleitung zur Wiederherstellung der Gesamtstruktur vorgesehen ist, werden nicht alle mögliche Szenarien behandelt. Ab Windows Server 2008, besteht eine Server Core-Version, die eine Vollversion von Windows Server, jedoch ohne eine vollständige GUI ist z. B. Obwohl es ist sicherlich möglich, Wiederherstellen eine Gesamtstruktur mit nur DCs, die Server Core ausgeführt wird, enthält dieses Handbuch keine detaillierten Anweisungen. Allerdings werden basierend auf den hier beschriebenen Anweisungen Sie die erforderlichen Befehlszeilenaktionen selbst entwerfen können.  

> ![!NOTE]
> Auch die Ziele dieses Handbuchs zum Wiederherstellen der Gesamtstruktur sind und Verwaltung vollständiger DNS-Funktionalität, kann die Wiederherstellung in einer DNS-Konfiguration führen, das aus der Konfiguration vor Auftreten des Fehlers geändert wird. Nach der Wiederherstellung der Gesamtstruktur ist, können Sie die ursprünglichen DNS-Konfiguration wiederherstellen. Die Empfehlungen in diesem Handbuch werden nicht beschrieben, wie Sie DNS-Server für die namensauflösung von anderen Teilen des Unternehmens-Namespace zu konfigurieren, wenn es sind DNS-Zonen, die nicht in AD DS gespeichert werden.  

## <a name="concepts-for-using-this-guide"></a>Konzepte für die Verwendung dieses Leitfadens

Bevor Sie beginnen mit der Planung für die Wiederherstellung der Active Directory-Gesamtstruktur, sollten Sie mit folgendem vertraut sein:  
  
- Grundlegende Konzepte von Active Directory  
- Die Wichtigkeit der Betriebsmasterrollen (auch bekannt als flexible einfache Mastervorgänge oder FSMO-Funktion). Diese Rollen umfassen Folgendes:  
   - Schemamaster
   - Domänennamenmaster
   - Relative ID (RID) master
   - Primärer Domänencontroller (PDC)-Emulationsmaster
   - Infrastrukturmaster

Darüber hinaus sollten gesichert haben und AD DS und SYSVOL in einer Lab-Umgebung in regelmäßigen Abständen wiederhergestellt haben. Weitere Informationen finden Sie unter [Sicherung der Systemstatusdaten](AD-Forest-Recovery-Procedures.md) und [Ausführen eine nicht autoritative Wiederherstellung von Active Directory Domain Services](AD-Forest-Recovery-Procedures.md).

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md)  
