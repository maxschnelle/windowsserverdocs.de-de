---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: Versenden einer Gruppenmitgliedschaft als Anspruchsregel verwenden
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10e027b4de463aad2b05eae40a622aebf8f12a3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>Versenden einer Gruppenmitgliedschaft als Anspruchsregel verwenden
Sie können diese Regel in Active Directory Federation Services \(AD FS\) verwenden, um einen neuen ausgehenden Anspruchswert nur für Benutzer ausstellen, die Mitglieder einer angegebenen Active Directory-Sicherheitsgruppe sind. Wenn Sie diese Regel verwenden, Sie stellen einen einzelnen Anspruch nur die Gruppe, die Sie angeben, und, die der Regellogik entspricht, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Ausgehender Anspruchswert|Wenn die Gruppenmitgliedschaft des Benutzers entspricht der *angegebenen Gruppe* und Typ des ausgehenden Anspruchs gleich *angegebenen Anspruchstyp*, ersetzen Sie den vorhandenen Gruppe Name-Wert mit der *angegebenen ausgehenden Anspruchswert* und der Anspruch wird ausgegeben.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Sie bieten außerdem Detail zu Einsatzbereichen für das Versenden der Gruppenmitgliedschaft als Anspruchsregel verwenden.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \ (wenn x dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter. Die folgende Liste enthält wichtige Tipps, die Sie kennen sollten Anspruchsregeln bevor Sie weiter lesen in diesem Thema:  
  
-   In der AD FS-Verwaltungs-Snap-In können Anspruchsregeln nur erstellt werden mithilfe von anspruchsregelvorlagen  
  
-   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
  
-   Anspruchsregelvorlagen werden immer müssen Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="outgoing-claim-value"></a>Ausgehender Anspruchswert  
Das Versenden der Gruppenmitgliedschaft als eine anspruchsregelvorlage verwenden, können Sie einen Anspruch ausstellen, die abhängig, ob ein Benutzer Mitglied einer Gruppe ist, die Sie angeben.  
  
Diese Regel Vorlage Probleme ein Anspruch nur, wenn der Benutzer die Security verfügt ID in anderen Worten: \(SID\), die Active Directory-Gruppe entspricht, die der Administrator gibt. Alle Benutzer, die Active Directory-Domänendienste \(AD DS\) authentifizieren müssen eingehenden Gruppen-SID für jede Gruppe-Ansprüche, der sie angehören. Standardmäßig wird diese Gruppen-SID-Ansprüche akzeptanztransformationsregeln in Active Directory Anspruchsanbieter-Vertrauensstellung durchlaufen. Mithilfe dieser Gruppen-SIDs als Basis für das Ausstellen von Ansprüchen viel schneller als das Nachschlagen der Benutzergruppen in AD DS ist.  
  
Bei Verwendung dieser Regel wird nur ein einzelner Anspruch ist gesendet basierend auf der Active Directory-Gruppe, die Sie auswählen. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die einen Gruppenanspruch mit dem Wert "Admin" sendet, wenn der Benutzer ein Mitglied der Sicherheitsgruppe "Domänen-Admins" ist.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel auf eine Anspruchsanbieter-Vertrauensstellung  
Administratoren sollten diesen Regeltyp verwenden akzeptanztransformationsregeln von einem Anspruchsanbieter-Vertrauensstellung, wenn vom Anspruchsanbieter, der was für Anspruchsanbieter außer Active Directory oder AD DS sehr ungewöhnlich ist Gruppen-SIDs empfangen werden.  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie erstellen diese Regel entweder mithilfe der anspruchsregelsprache oder mithilfe der Send LDAP Group Membership als Anspruch Regel Vorlage in AD FS-Verwaltungs-Snap-In. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Wählen Sie die Gruppe eines Benutzers mithilfe der Objektauswahl  
  
-   Wählen Sie einen Typ des ausgehenden Anspruchs  
  
-   Wählen Sie eine ausgehende namensbezeichnerformat \ (das ist nur, wenn Name-ID aus der ausgehende Anspruch Typ Field\ ausgewählt ist)  
  
-   Angeben eines ausgehenden anspruchswerts  
  
Weitere Informationen zum Erstellen dieser Regel finden Sie unter [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](https://technet.microsoft.com/en-us/library/ee913569.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Wenn Sie anhand einer eingehenden SID keine Gruppen-SID Ansprüche ausgeben möchten, verwenden der Transformation einer eingehenden Anspruchs-Vorlage. Wenn der Administrator die Namen aller Gruppen abzurufen, die der Benutzer Mitglied ist möchte, verwenden Sie das Senden von LDAP-Attributen als Ansprüche Regelvorlage stattdessen mit der **TokenGroups** Attribut.  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>Beispiel: Zum Ausstellen von Gruppenansprüchen auf Basis der Gruppenmitgliedschaft des Benutzers  
Die folgende Regel stellt Gruppenansprüche für einen Benutzer anhand einer eingehenden Gruppen-SID:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

