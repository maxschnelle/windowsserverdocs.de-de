---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Bewährte Methoden für die Sicherung von Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0d6f4abbf5dd071a2e229acbda2057c1f81851e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408626"
---
# <a name="best-practices-for-securing-active-directory"></a>Bewährte Methoden für die Sicherung von Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Dokument enthält eine Reihe praktischer Techniken, die IT-Führungskräften dabei helfen, eine Unternehmens Active Directory Umgebung zu schützen. Active Directory spielt eine wichtige Rolle in der IT-Infrastruktur und stellt harmonische Abläufe und Sicherheit verschiedenster Netzwerkressourcen innerhalb einer globalen, ineinander verwobenen Umgebung sicher. Die erörterten Methoden basieren größtenteils auf der Microsoft Information Security and Risk Management (isrm)-Organisation, die für den Schutz der Assets von Microsoft IT und anderen Microsoft-Geschäftsbereichen verantwortlich ist, zusätzlich zur Beratung eines ausgewählte Anzahl von Microsoft Global 500-Kunden.  
  
-   [Abstrakt](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [Einführung](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [Angriffswege](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [Attraktive Konten für den Diebstahl von Anmeldeinformationen](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Reduzieren der Angriffsfläche für Active Directory](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [Implementieren von Verwaltungs Modellen mit geringstmöglichen Berechtigungen](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [Implementieren sicherer Verwaltungshosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [Sichern von Domänen Controllern gegen Angriffe](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [Überwachungs Active Directory auf Anzeichen einer Gefährdung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [Empfehlungen zu Überwachungsrichtlinien](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [Planen der Gefährdung](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [Beibehalten einer sichereren Umgebung](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [Anhänge](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [Anhang B: Privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [Anhang H: Schützen lokaler Administratorkonten und -gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [Anhang M: Links zu Dokumenten und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


