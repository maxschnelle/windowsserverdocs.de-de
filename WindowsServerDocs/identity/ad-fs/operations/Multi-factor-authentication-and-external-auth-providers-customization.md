---
title: Mehrstufige Authentifizierung und externe Authentifizierung Anbieter Anpassung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 6d06c017601003e3b93df32f5fa50190ce54541d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>Mehrstufige Authentifizierung und externe Authentifizierung Anbieter Anpassung 

>Gilt für: Windows Server 2016, Windows Server2012 R2

In AD FS wird die Unterstützung für die mehrstufige Authentifizierung Out-Of\-The\-Box bereitgestellt. Beispielsweise können Sie AD FS für die Verwendung der integrierten Zertifikatauthentifizierung als zweistufige Authentifizierung konfigurieren. Sie können auch externe Authentifizierungsanbieter verwenden. Dieser Ansatz kann AD FS in weitere Dienste, z. B. Azure Multi-Factor Authentication integrieren aktivieren, oder Sie können einen eigenen Anbieter entwickeln. Finden Sie unter [Solution Guide: Manage Risk with Multithread-Factor Access Control](https://technet.microsoft.com/library/dn280937.aspx) für Weitere Informationen zum Registrieren von externen Authentifizierungsanbieters mithilfe von AD FS.  
  
Es wird empfohlen, dass ein externer Authentifizierungsanbieter die Klassen verwenden, die in der CSS-Datei definiert sind, die AD FS bereitgestellt wird, um die Benutzeroberfläche für die Authentifizierung zu erstellen. Sie können das folgende Cmdlet verwenden, das standardwebdesign exportieren und untersuchen Sie die Benutzeroberflächenklassen und Elemente, die in der CSS-Datei definiert sind. Die CSS-Datei kann in die Entwicklung der Benutzeroberfläche Standardparameter in der ein externer Authentifizierungsanbieter verwendet werden.  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
Im folgenden finden ein Beispiel für die Standardparameter in Benutzeroberfläche, die durch ein externer Authentifizierungsanbieter rot markiert ist. Die Benutzeroberfläche verwendet die UI-Klassen in der AD FS-CSS-Datei.  
  
![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
Bevor Sie eine neue benutzerdefinierte Authentifizierungsmethode entwickeln, empfehlen wir, dass Sie die AD FS-Design- und Formatvorlagendefinitionen um Anforderungen an die inhaltsbearbeitung zu verstehen, untersuchen.  
  
-   Eine benutzerdefinierte Authentifizierungsmethode Autoren nur ein HTML-Segment auf der AD FS-Anmeldeseite und nicht die gesamte Seite. Sie sollten Definition der AD FS Stil verwenden, um das einheitliche Aussehen und Verhalten abzurufen.  
  
![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   Beachten Sie, dass AD FS-Administratoren die AD FS-Stile anpassen können. . Nicht empfohlen hartcodierung eigener Formatvorlagen. Stattdessen empfehlen wir, verwenden Sie die AD FS-Formatvorlagen, wann immer möglich.  
  
-   Out-Of\--Formatvorlage AD FS-Stile werden mit einer von links nach rechts \(LTR\) Stil und eine mit der rechten Maustaste-zu-Links-\(RTL\) verfasst. Administratoren können beide anpassen und sprachspezifischen Formatvorlagen über die webdesigndefinition bereitstellen. Jedes Stylesheet verfügt über drei Abschnitt mit entsprechenden Kommentaren:  
  
    -   **Designformatvorlagen** \-diese Formatvorlagen sollten nicht und kann nicht verwendet werden. Diese Stile dienen zum Design für alle Seiten zu definieren. Sie werden absichtlich von einer Element-ID definiert, so, dass sie nicht wiederverwendet werden.  
  
    -   **häufig verwendete Formatvorlagen** \ – Hierbei handelt es sich um die Stile, die für Ihre Inhalte verwendet werden soll.  
  
    -   **formfaktorformatvorlagen** \-diese Formatvorlagen sind für verschiedene Formfaktoren. Sie sollten wissen, dass in diesem Abschnitt, um sicherzustellen, dass Ihre Inhalte mit verschiedenen Formfaktoren arbeiten, z. B. Smartphones und Tablets funktioniert.  
  
Weitere Informationen finden Sie unter [Solution Guide: Manage Risk with Multithread-Factor Access Control](https://technet.microsoft.com/library/dn280937.aspx) und [Lösungshandbuch: Verwalten von Risiken mit zusätzlicher Multithread-Faktor-Authentifizierung für sensible Anwendungen](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) 
