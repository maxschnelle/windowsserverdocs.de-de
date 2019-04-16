---
title: "Voraussetzungen für die Planung für die Wiederherstellung der Active Directory-Gesamtstruktur"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 672e1f4d0de9bfb2cbe291c5ed715814c8acacd0
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
#<a name="active-directory-forest-recovery-prerequisites"></a>Voraussetzungen für die Wiederherstellung von Active Directory-Gesamtstruktur

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Das folgende Dokument erläutert die erforderlichen Komponenten, denen Sie vor einen Gesamtstruktur Wiederherstellungsplan Konzipierung oder versuchen, eine Wiederherstellung mit vertraut sein sollten.

## <a name="assumptions-for-using-this-guide"></a>Annahmen für die Verwendung dieses Handbuchs 

1.  Jetzt haben Sie ein Microsoft-Support-Mitarbeiter und:

    - Bestimmen Sie die Ursache des Fehlers Gesamtstruktur. Dieses Handbuch nicht die Fehlerursache vorschlagen oder sollten alle Verfahren, um den Fehler zu verhindern.  
    - Möglichen Abhilfen wird ausgewertet.  
    - Abgeschlossen ist, in Zusammenarbeit mit Microsoft-Support ist, Wiederherstellung der Gesamtstruktur in den Zustand vor dem Auftreten des die beste Möglichkeit, den Fehler beheben. In vielen Fällen sollte die Wiederherstellung der Gesamtstruktur die letzte Option.  </br></br>

2. Die von der Microsoft empfohlenen Vorgehensweisen für die Verwendung von Active Directory-integrierte Domain Name System (DNS) befolgen. Insbesondere sollte eine Active Directory-integrierte DNS-Zone für jede Active Directory-Domäne vorhanden sein. Wenn dies nicht der Fall ist, weiterhin können die Grundprinzipien dieses Handbuchs Sie Wiederherstellung der Gesamtstruktur ausführen. Allerdings müssen Sie bestimmte Maßnahmen für die DNS-Wiederherstellung basierend auf Ihrer eigenen Umgebung ausführen. Weitere Informationen zur Verwendung von Active Directory-integrierte DNS finden Sie unter [erstellen einen DNS-Infrastruktur-Entwurf ](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).
3. Obwohl dieses Handbuch als allgemeinen Leitfaden für die Wiederherstellung der Gesamtstruktur vorgesehen ist, werden nicht alle möglichen Szenarien behandelt. Ab Windows Server2008, ist es beispielsweise eine Server Core-Version, die eine Vollversion von Windows Server jedoch ohne eine vollständige GUI ist. Obwohl es natürlich möglich ist, eine Gesamtstruktur nur Domänencontroller, die Server Core ausgeführt bestehend aus wiederherstellen, enthält dieses Handbuch keine detaillierten Anweisungen. Allerdings werden basierend auf den hier beschriebenen Richtlinien Sie die erforderlichen Befehlszeilenaktionen selbst entwerfen können.  
 
>![!NOTE]
> Zwar die Ziele dieses Handbuchs Wiederherstellung der Gesamtstruktur und verwalten oder Wiederherstellen der vollständigen DNS-Funktionalität, ergeben Wiederherstellung in einer DNS-Konfiguration, die von der Konfiguration vor Auftreten des Fehlers geändert wird. Nach der Wiederherstellung der Gesamtstruktur können Sie die ursprüngliche DNS-Konfiguration zurückkehren. Die Empfehlungen in diesem Handbuch ist beschrieben, wie Sie DNS-Server für die Namensauflösung von anderen Teilen des Unternehmens Namespaces konfigurieren, werden DNS-Zonen, die nicht in AD DS gespeichert sind.  

## <a name="concepts-for-using-this-guide"></a>Konzepte für die Verwendung dieses Handbuchs
 Bevor Sie beginnen mit der Planung für die Wiederherstellung der Active Directory-Gesamtstruktur, sollten Sie mit folgendem vertraut sein:  
  
-   Grundlegende Konzepte der Active Directory  
  
-   Die Bedeutung von Betriebsmasterrollen (auch als flexible einfache Mastervorgänge oder FSMO). Diese Rollen umfassen Folgendes:  
  
    -   Schemamaster  
  
    -   Domänennamenmaster  
  
    -   Relative ID RID-master  
  
    -   Primärer Domänencontroller (PDC)-Emulatormaster  
  
    -   Infrastrukturmaster  
  
 Darüber hinaus sollte gesichert haben und AD DS und SYSVOL in einer Testumgebung in regelmäßigen Abständen wiederhergestellt. Weitere Informationen finden Sie unter [Sicherung der Systemstatusdaten](AD-Forest-Recovery-Procedures.md) und [eine nicht autoritative Wiederherstellung der Active Directory-Domänendienste ausführen ](AD-Forest-Recovery-Procedures.md).

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md)  
