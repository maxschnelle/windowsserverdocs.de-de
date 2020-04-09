---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Konfigurieren von Anspruchs Regeln
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7051040feb023ec9ab647d6e368136fb04b7db34
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817143"
---
# <a name="configure-claim-rules"></a>Konfigurieren von Anspruchsregeln

In einem Anspruchs\-basierten Identitäts Modell ist die Funktion von Active Directory-Verbunddienste (AD FS) \(AD FS\) als Verbund Dienste, ein Token auszugeben, das einen Satz von Ansprüchen enthält. Anspruchs Regeln steuern die Entscheidungen hinsichtlich der Ansprüche, die Probleme AD FS. Anspruchs Regeln und alle Server Konfigurationsdaten werden in der AD FS Konfigurations Datenbank gespeichert.  
  
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

## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
