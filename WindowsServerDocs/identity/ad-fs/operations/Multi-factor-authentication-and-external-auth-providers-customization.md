---
title: Multi-Factor Authentication und externe Authentifizierung-Anbieter-Anpassung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 6d06c017601003e3b93df32f5fa50190ce54541d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864801"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>Multi-Factor Authentication und externe Authentifizierung-Anbieter-Anpassung 

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In AD FS ist die Unterstützung für die mehrstufige Authentifizierung bereitgestellt\-von\-der\-Feld. Sie können z. B. AD FS konfigurieren erstellt verwenden\-bei Zertifikatauthentifizierung als zweistufige Authentifizierung. Sie können auch externe Authentifizierungsanbieter verwenden. Dieser Ansatz kann AD FS für die Integration in zusätzliche Dienste wie Azure Multi-Factor Authentication, aktivieren, oder Sie können Ihren eigenen Anbieter entwickeln. Finden Sie unter [Lösungshandbuch: Verwalten von Risiken mit mehreren\-rechnen Sie Access Control](https://technet.microsoft.com/library/dn280937.aspx) für Weitere Informationen zur Verwendung externer Authentifizierungsanbieter zu registrieren, indem Sie mithilfe von AD FS.  
  
Es wird empfohlen, dass ein externer Authentifizierungsanbieter die Klassen verwenden, die in der CSS-Datei definiert sind, die AD FS, die zum Erstellen der Benutzeroberfläche für der Authentifizierungs bereitstellt. Mit dem folgenden Cmdlet können Sie das Standardwebdesign exportieren und die Benutzeroberflächenklassen und -elemente inspizieren, die in der CSS-Datei definiert sind. Die CSS-Datei kann verwendet werden, bei der Entwicklung der Anmeldeseite\-in der Benutzeroberfläche eines externen Authentifizierungsanbieters.  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
Folgendes ist ein Beispiel für die Anmeldung\-in der Benutzeroberfläche, die wird rot hervorgehoben, von einem externen Authentifizierungsanbieter. Die Benutzeroberfläche verwendet die UI-Klassen in der AD FS-CSS-Datei.  
  
![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
Bevor Sie eine neue benutzerdefinierte Authentifizierungsmethode entwickeln, empfehlen wir, dass Sie die AD FS--Design- und Formatvorlagendefinitionen um die Anforderungen an die inhaltsbearbeitung zu verstehen, zu untersuchen.  
  
-   Eine benutzerdefinierte Authentifizierungsmethode wird nur ein HTML-Segment für die AD FS-Anmeldeseite Autoren\-auf Seite und nicht die gesamte Seite. Sie sollten des AD FS Style-Definition verwenden, um das konsistente Erscheinungsbild und Verhalten zu erhalten.  
  
![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   Denken Sie daran, dass AD FS-Administratoren der AD FS-Stile anpassen können. . Eine Hartcodierung eigener Formatvorlagen wird nicht empfohlen. Stattdessen empfehlen wir, AD FS-Formatvorlagen, wann immer möglich verwenden.  
  
-   Out\-von\-Feld AD FS--Formatvorlagen mit einer "Links" erstellt\-zu\-rechten \(LTR\) Stil und eine rechts\-zu\-linken \(RTL\). Administratoren können beide anpassen und bieten Sprache\-bestimme Formatvorlagen über die webdesigndefinition. Jedes Stylesheet verfügt über drei Abschnitt mit entsprechenden Kommentaren:  
  
    -   **Design-Stilen** \- diese Formatvorlagen sollten nicht und kann nicht verwendet werden. Sie sind für die Definition des Designs für alle Seiten vorgesehen. Sie werden absichtlich von einer Element-ID definiert, damit sie nicht wiederverwendet werden.  
  
    -   **Allgemeine Formatvorlagen** \- Hierbei handelt es sich um die Stile, die für Ihre Inhalte verwendet werden soll.  
  
    -   **formfaktorformatvorlagen** \- diese Formatvorlagen sind für verschiedene Formfaktoren. Sie sollten diesen Abschnitt verstehen, um sicherzustellen, dass Ihre Inhalte mit verschiedenen Formfaktoren arbeiten, beispielsweise Telefone und Tablets.  
  
Weitere Informationen finden Sie unter [Solution Guide: Verwalten von Risiken mit mehreren\-rechnen Sie Access Control](https://technet.microsoft.com/library/dn280937.aspx) und [Solution Guide: Verwalten von Risiken mit zusätzlicher Multi\-zweistufige Authentifizierung für sensible Anwendungen](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md) 
