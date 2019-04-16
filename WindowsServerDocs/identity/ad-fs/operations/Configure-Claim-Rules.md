---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Konfigurieren von Anspruchsregeln
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f9e0509e2f870fd0edc7f0c6a241d789945e7ccb
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

>Gilt für: Windows Server 2016, Windows Server2012 R2

Die Funktion des Active Directory Federation Services \(AD FS\) als Verbunddienste werden in einem Identitätsmodell Claims\-basierten ein Token ausstellen, die eine Gruppe von Ansprüchen enthält. Anspruchsregeln Regeln die Entscheidungen in Bezug auf Ansprüche, die AD FS ausstellt. Anspruchsregeln und alle Server Konfigurationsdaten werden in der AD FS-Konfigurationsdatenbank gespeichert.  
  
AD FS entscheidet Ausstellung, die auf Informationen zur Identität, die sie in Form von Ansprüchen bereitgestellt wird, und andere kontextbezogene Informationen basieren. Auf hoher Ebene arbeitet die AD FS ein Prozessor Regeln durch eine Gruppe von Ansprüchen als Eingabe, führt eine Reihe von Transformationen und gibt dann einen anderen Satz von Ansprüchen als Ausgabe zurück. 

In den folgenden Themen helfen Ihnen bei der Regeln erstellen, die AD FS verarbeitet: 
  
-   [Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Zulassen aller Benutzer](Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) 
-   [Erstellen einer Regel zum Senden eines AD FS 1.x-kompatiblen Anspruchs](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md) 
  
-   [Erstellen einer Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
