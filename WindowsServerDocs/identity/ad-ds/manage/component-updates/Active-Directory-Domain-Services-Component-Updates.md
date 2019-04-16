---
title: 'Active Directory Domain Services: Komponentenupdates'
description: "Dieses Dokument beschreibt die AD DS-Komponentenupdates für Windows Server2012 R2"
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 52d3dab542b4250670067e927f42ddf1597fc852
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services: Komponentenupdates

>Gilt für: Windows Server 2016, Windows Server2012 R2

Dieses Modul stellt die Komponenten, die in den Bereichen Verzeichnisdienste und identitätstechnologie kleinere Updates empfangen.  
  
|Informationen zum Autor|  
|--------------------|  
|**Autor:**|Justin Hingucker|  
|**BIOS:**|Justin ist Senior Support Escalation Engineer mit dem Verzeichnisdienste-Team in Irving, Texas, USA basiert.  Er hat erstellt oder in den vergangenen 12 Jahren zahlreiche Schulungskurse und Knowledge Base-Artikel für die Microsoft Knowledgebase beigetragen. Er leitet Microsoft-Mitarbeitern und Kunden neue Produktarchitektur, ist Produktarchitekturen Microsoft Certified Master (MCM), Microsoft Certified Trainer (MCT) und enthält eine Master Abschluss in Computer Education and Cognitive Systems.|  
|**Mitwirkende**|Dieses Trainingsmodul enthält Beiträge von *Michiko Short*, *Dean Wells*, *Alan Jowett*, *Manu Pushpendran*, *Yashar Bahman*, *Anoosh Saboori*, *Rashmi Jha*, *Justin Halle* und *Herbert Mauerer*|  
|**Prüfer**|Unser Dank gilt den folgenden Personen, die ihre eigenen Zeit überprüfen und Feedback aufgewendet: *Joey Seifert*, *Justin Halle*|  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
### <a name="what-you-will-learn"></a>Lernziele  
Nach Abschluss dieses Moduls, werden Sie kann:  
  
-   Erklären Sie die Komponente Aktualisierungen in den Bereichen Verzeichnisdienste und Identitätstechnologie in Windows Server 2012 R2  
  
    -   [SPN- und UPN-Eindeutigkeit](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  
  
    -   [Winlogon automatischer Neustart anmelden & #40; Nach einem & #41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  
  
    -   [TPM-Schlüsselnachweis](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  
  
    -   [Zertifizierungsstelle sichern und Wiederherstellen von Windows PowerShell-cmdlets](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  
  
    -   [Befehlszeilenprozessen](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  
  
    -   [Schutz von Anmeldeinformationen und Verwaltung](https://technet.microsoft.com/library/dn408190.aspx)  
  
    -   [Directory Services: Komponentenupdates](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  
  
        -   [Domänen- und Gesamtstrukturfunktionsebenen](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
        -   [Abschreibung von NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
        -   [Änderungen des LDAP-Abfrageoptimierer](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
        -   [Ereignis 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
        -   [Durchsatzverbesserung bei der Active Directory-Replikation](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  


