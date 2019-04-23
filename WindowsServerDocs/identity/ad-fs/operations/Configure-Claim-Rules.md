---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Konfigurieren von Anspruchsregeln
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f9e0509e2f870fd0edc7f0c6a241d789945e7ccb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829411"
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In einer Ansprüche\-Identitätsmodell basiert, die Funktion des Active Directory Federation Services \(AD FS\) als Verbund ist Dienste zum Ausstellen eines Tokens, das einen Satz von Ansprüchen enthält. Anspruchsregeln steuern die Entscheidungen im Hinblick auf die Ansprüche, die AD FS-Probleme. Anspruchsregeln und alle serverkonfigurationsdaten werden in der AD FS-Konfigurationsdatenbank gespeichert.  
  
AD FS ermöglicht die Ausstellung von Entscheidungen, die auf Identitätsinformationen, die Sie in Form von Ansprüchen bereitgestellt wird und anderen kontextbezogenen Informationen basieren. Auf einer hohen Ebene funktioniert die AD FS ein regelprozessor mit einer von Ansprüchen als Eingabe festgelegt, führt eine Reihe von Transformationen und gibt dann einen anderen Satz von Ansprüchen als Ausgabe zurück. 

In den folgenden Themen hilft Ihnen bei der die Regeln erstellen, die AD FS verarbeitet werden: 
  
-   [Erstellen Sie eine Regel zum Pass-Through oder Filtern eines eingehenden Anspruchs](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Zulassen von allen Benutzern](Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Versenden einer Gruppenmitgliedschaft als Anspruch](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs](Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Senden eines Authentifizierungsanspruchs-Methode](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) 
-   [Erstellen Sie eine Regel zum Senden eines-kompatibler Anspruchs von AD FS 1.x](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md) 
  
-   [Erstellen Sie eine Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
