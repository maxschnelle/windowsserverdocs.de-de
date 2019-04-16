---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Best Practices for Securing Active Directory
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ecef0c173677d379524189b1769d4721ab0774a8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="best-practices-for-securing-active-directory"></a>Best Practices for Securing Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Dokument bietet einen Fachleuten und enthält eine Reihe von praktischen Verfahren, mit IT-Fachleute, die eine Enterprise-Active Directory-Umgebung zu schützen. Active Directory spielt eine wichtige Rolle in der IT-Infrastruktur und stellt die harmonische Abläufe und Sicherheit verschiedenster Netzwerkressourcen innerhalb einer globalen, ineinander verwobenen Umgebung sicher. Vorgestellten Methoden basieren größtenteils auf das Microsoft Information Security and Risiko-Management (ISRM) des Unternehmens zu verbessern, die für den Schutz der Ressourcen von Microsoft-IT und andere Microsoft Business Abteilungen, zusätzlich zu eine ausgewählte Reihe von Microsoft Global 500-Kunden verantwortlich ist.  
  
-   [Vorbemerkung](https://technet.microsoft.com/library/dn487451.aspx)  
  
-   [Bestätigungen](https://technet.microsoft.com/library/dn487445.aspx)  
  
-   [Zusammenfassung](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [Einführung in](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [Wege der Gefährdung](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [Attraktive Konten für den Diebstahl von Anmeldeinformationen](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Reduzieren der Angriffsfläche für Active Directory](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [Implementieren von Verwaltungsmodellen der geringsten Berechtigungen](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [Implementieren sichere Administrative Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [Sichern von Domänencontrollern vor Angriffen](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [Überwachen der Richtlinie Empfehlungen](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [Planen der Gefährdung](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [Verwalten einer sicheren Umgebung](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [Anhängen](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [Anhang B: privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [Anhang H: schützen lokaler Administratorkonten und-Gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [Anhang M: Links dokumentieren und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


