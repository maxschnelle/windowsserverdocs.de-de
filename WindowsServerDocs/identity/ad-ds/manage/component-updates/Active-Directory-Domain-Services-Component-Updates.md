---
title: 'Active Directory Domain Services: Komponentenupdates'
description: In diesem Dokument werden die AD DS Komponenten Updates für Windows Server 2012 R2 erläutert.
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 0dfb108067bee1a5f276963116e2a72b99f6aec2
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961122"
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services: Komponentenupdates

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In dieser Unterrichtseinheit werden Komponenten mit geringfügigen Aktualisierungen in den Bereichen Verzeichnisdienste und Identitätstechnologie vorgestellt.  


| Zum Autor |
|------------------|
|   **Autor:**    |
|     **Biografie:**     |
| **Mitwirkende** |
|  **Prüfer**   |

> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  

### <a name="what-you-will-learn"></a>Lernziele  
Nach Abschluss dieses Moduls können Sie Folgendes:  

-   Die Aktualisierungen an den Komponenten in den Bereichen Verzeichnisdienste und Identitätstechnologie von Windows Server 2012 R2 erklären  

    -   [SPN- und UPN-Eindeutigkeit](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  

    -   [Automatisches Anmelden bei Winlogon &#40;ARSO&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  

    -   [TPM-Schlüsselnachweis](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  

    -   [Windows PowerShell-Cmdlets zum Sichern und Wiederherstellen von Zertifizierungsstellen](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  

    -   [Überwachen von Befehlszeilenprozessen](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  

    -   [Schutz und Verwaltung von Anmeldeinformationen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))  

    -   [Directory Services-Komponentenupdates](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  

        -   [Domänen- und Gesamtstrukturfunktionsebenen](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  

        -   [Abschreibung von NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  

        -   [Änderungen am LDAP-Abfrageoptimierer](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  

        -   [Verbesserungen am Ereignis 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  

        -   [Durchsatzverbesserung bei der Active Directory-Replikation](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
