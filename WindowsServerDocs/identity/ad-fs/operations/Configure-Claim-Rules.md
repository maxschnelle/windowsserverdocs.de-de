---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Konfigurieren von Anspruchs Regeln
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6ceca4b76ba1744c3cc988fd840453f9391ce3d3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407672"
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

In einem Anspruchs @ no__t-0basierten Identitäts Modell besteht die Funktion von Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-2 als Verbund Dienste darin, ein Token auszugeben, das einen Satz von Ansprüchen enthält. Anspruchs Regeln steuern die Entscheidungen hinsichtlich der Ansprüche, die Probleme AD FS. Anspruchs Regeln und alle Server Konfigurationsdaten werden in der AD FS Konfigurations Datenbank gespeichert.  
  
AD FS trifft Ausstellungs Entscheidungen, die auf Identitätsinformationen basieren, die ihm in Form von Ansprüchen und anderen Kontextinformationen bereitgestellt werden. Auf hoher Ebene wird AD FS als Regel Prozessor betrieben, indem ein Satz von Ansprüchen als Eingabe übernommen wird, eine Reihe von Transformationen durchführt und dann eine andere Gruppe von Ansprüchen als Ausgabe zurückgegeben wird. 

Die folgenden Themen unterstützen Sie beim Erstellen der Regeln, die AD FS verarbeiten soll: 
  
-   [Erstellen einer Regel zum durchlaufen oder Filtern eines eingehenden Anspruchs](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Zulassen aller Benutzer](Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Erstellen einer Regel, mit der Benutzer anhand eines eingehenden Anspruchs zugelassen oder abgelehnt werden](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) 
-   [Erstellen einer Regel zum Senden eines AD FS 1. x-kompatiblen Anspruchs](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md) 
  
-   [Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
