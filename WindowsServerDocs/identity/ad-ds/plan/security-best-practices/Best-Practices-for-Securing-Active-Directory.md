---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Bewährte Methoden für die Sicherung von Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 972def668634e794908a3ff2933d038ae38be5d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817081"
---
# <a name="best-practices-for-securing-active-directory"></a>Bewährte Methoden für die Sicherung von Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Dokument enthält die Factoryvorlage Perspektive, und es enthält eine Reihe von praktische Techniken zum IT-Führungskräfte, die eine Active Directory-unternehmensumgebung schützen können. Active Directory spielt eine wichtige Rolle in der IT-Infrastruktur und stellt harmonische Abläufe und Sicherheit verschiedenster Netzwerkressourcen innerhalb einer globalen, ineinander verwobenen Umgebung sicher. Erläuterten Methoden basieren größtenteils auf der Microsoft Information Security and Risk Management (ISRM) Erfahrungen der Organisation, die für den Schutz der Ressourcen von Microsoft IT und anderer Geschäftsbereiche, zusätzlich zu berät verantwortlich ist ein ausgewählte Anzahl von Microsoft Global 500-Kunden.  
  
-   [Abstrakt](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [Einführung](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [Angriffswege](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [Attraktive Konten für den Diebstahl von Anmeldeinformationen](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Reduzieren der Angriffsfläche für Active Directory](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [Implementieren von Verwaltungsmodellen der geringsten](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [Implementieren sichere Administrative Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [Schützen von Domänencontrollern vor Angriffen](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [Überwachen von Active Directory auf Anzeichen einer Kompromittierung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [Empfehlungen zu Überwachungsrichtlinien](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [Planen der Gefährdung](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [Verwalten einer sicheren Umgebung](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [Anhänge](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [Anhang B: Privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [Anhang H: Schützen lokaler Administratorkonten und-Gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [Anhang M: Links zu Dokumenten und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


