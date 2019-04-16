---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: Konfigurieren von Anspruchsregeln
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 259e2b266b64a3b34c237cfe209a3558124c8ef2
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

>Gilt für: Windows Server 2016, Windows Server2012 R2

Die Funktion des Active Directory-Verbunddienste (AD FS) als Verbunddienste werden in einem Identitätsmodell Claims\-basierten ein Token ausstellen, die eine Gruppe von Ansprüchen enthält. Anspruchsregeln Regeln die Entscheidungen in Bezug auf Ansprüche, die AD FS ausstellt. Anspruchsregeln und alle Server Konfigurationsdaten werden in der AD FS-Konfigurationsdatenbank gespeichert.  
  
AD FS entscheidet Ausstellung, die auf Informationen zur Identität, die sie in Form von Ansprüchen bereitgestellt wird, und andere kontextbezogene Informationen basieren. Auf hoher Ebene arbeitet die AD FS ein Prozessor Regeln durch eine Gruppe von Ansprüchen als Eingabe, führt eine Reihe von Transformationen und gibt dann einen anderen Satz von Ansprüchen als Ausgabe zurück. 

In den folgenden Themen helfen Ihnen bei der Regeln erstellen, die AD FS verarbeitet: 
  
-   [Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Zulassen aller Benutzer](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
