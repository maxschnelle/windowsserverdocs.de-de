---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: Konfigurieren von Anspruchs Regeln in AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b2c653aa7339815ce22c256cf2c6c931ca7c7fc9
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87863686"
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

In einem Anspruchs \- basierten Identitäts Modell besteht die Funktion von Active Directory-Verbunddienste (AD FS) (AD FS) als Verbund Dienste darin, ein Token auszugeben, das einen Satz von Ansprüchen enthält. Anspruchs Regeln steuern die Entscheidungen hinsichtlich der Ansprüche, die Probleme AD FS. Anspruchs Regeln und alle Server Konfigurationsdaten werden in der AD FS Konfigurations Datenbank gespeichert.  
  
AD FS trifft Ausstellungs Entscheidungen, die auf Identitätsinformationen basieren, die ihm in Form von Ansprüchen und anderen Kontextinformationen bereitgestellt werden. Auf hoher Ebene wird AD FS als Regel Prozessor betrieben, indem ein Satz von Ansprüchen als Eingabe übernommen wird, eine Reihe von Transformationen durchführt und dann eine andere Gruppe von Ansprüchen als Ausgabe zurückgegeben wird. 

Die folgenden Themen unterstützen Sie beim Erstellen der Regeln, die AD FS verarbeiten soll: 
  
-   [Erstellen einer Regel zum durchlaufen oder Filtern eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Zulassen aller Benutzer](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel, mit der Benutzer anhand eines eingehenden Anspruchs zugelassen oder abgelehnt werden](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../ad-fs-operations.md) 
