---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: Konfigurieren von Anspruchsregeln
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 259e2b266b64a3b34c237cfe209a3558124c8ef2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871631"
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In einer Ansprüche\-Identitätsmodell basiert, die Funktion des Active Directory Federation Services (AD FS) als Verbunddienste ist zum Ausstellen eines Tokens, das einen Satz von Ansprüchen enthält. Anspruchsregeln steuern die Entscheidungen im Hinblick auf die Ansprüche, die AD FS-Probleme. Anspruchsregeln und alle serverkonfigurationsdaten werden in der AD FS-Konfigurationsdatenbank gespeichert.  
  
AD FS ermöglicht die Ausstellung von Entscheidungen, die auf Identitätsinformationen, die Sie in Form von Ansprüchen bereitgestellt wird und anderen kontextbezogenen Informationen basieren. Auf einer hohen Ebene funktioniert die AD FS ein regelprozessor mit einer von Ansprüchen als Eingabe festgelegt, führt eine Reihe von Transformationen und gibt dann einen anderen Satz von Ansprüchen als Ausgabe zurück. 

In den folgenden Themen hilft Ihnen bei der die Regeln erstellen, die AD FS verarbeitet werden: 
  
-   [Erstellen Sie eine Regel zum Pass-Through oder Filtern eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Zulassen von allen Benutzern](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Versenden einer Gruppenmitgliedschaft als Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Senden eines Authentifizierungsanspruchs-Methode](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [Erstellen Sie eine Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
