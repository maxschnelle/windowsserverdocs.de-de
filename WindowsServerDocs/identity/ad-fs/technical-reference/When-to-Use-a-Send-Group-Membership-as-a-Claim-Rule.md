---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: Einsatzbereiche für das Versenden einer Gruppenmitgliedschaft als Anspruchsregel
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ea537aa61cd7bfbe05ed1dd151eddd4a0bfc5ca7
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188298"
---
# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>Einsatzbereiche für das Versenden einer Gruppenmitgliedschaft als Anspruchsregel
Sie können diese Regel in Active Directory-Verbunddienste \(AD FS\) sollen nur für Benutzer einen neuen ausgehenden Anspruchswert ausstellen, die Mitglieder einer angegebenen Active Directory-Sicherheitsgruppe sind. Wenn Sie diese Regel anwenden, stellen Sie einen einzelnen Anspruch aus, der nur für die angegebene Gruppe gilt, wie in folgender Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Ausgehender Anspruchswert|Wenn die Gruppenmitgliedschaft des Benutzers gleich der *angegebenen Gruppe* und der Typ des ausgehenden Anspruchs gleich dem *angegebenen Anspruchstyp* ist, ersetzen Sie den vorhandenen Wert des Gruppennamens durch den *angegebenen ausgehenden Anspruchswert* und stellen den Anspruch aus.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Darüber hinaus werden Details zu Einsatzbereichen für das Versenden der Gruppenmitgliedschaft als Anspruchsregel angesprochen.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
  
-   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="outgoing-claim-value"></a>Ausgehender Anspruchswert  
Mithilfe der Regelvorlage „Send Group Membership as a Claim“, können Sie einen Anspruch ausstellen, der abhängig davon ist, ob ein Benutzer Mitglied einer von Ihnen festgelegten Gruppe ist.  
  
Das heißt, stellt diese Regelvorlage einen Anspruch, nur, wenn der Benutzer die Gruppe Sicherheits-ID hat \(SID\) , die mit Active Directory-Gruppe, der angibt, der Administrator übereinstimmt. Alle Benutzer, die Active Directory Domain Services authentifizieren \(AD DS\) müssen eingehenden Gruppen-SID-Ansprüche für jede Gruppe, der sie angehören. Standardmäßig leiten die Akzeptanztransformationsregeln in der Active Directory-Anspruchsanbieter-Vertrauensstellung diese Gruppen-SID-Ansprüche durch. Das Verwenden dieser Gruppen-SIDs als Basis für das Ausstellen von Ansprüchen ist sehr viel schneller als das Nachschlagen der Benutzergruppen in AD DS.  
  
Wenn Sie diese Regel verwenden, wird nur ein einzelner Anspruch anhand der ausgewählten Active Directory-Gruppe gesendet. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel nutzen, die einen Gruppenanspruch mit dem Wert „Admin“ sendet, wenn der Benutzer ein Mitglied der Sicherheitsgruppe „Domänenadmins“ ist.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel in einer Anspruchsanbietervertrauensstellung  
Administratoren sollten diesen Regeltyp in Akzeptanztransformationsregeln des Anspruchsanbieters nur dann verwenden, wenn von dem Anspruchsanbieter Gruppen-SIDs empfangen werden. Das ist für Anspruchsanbieter außer Active Directory oder AD DS sehr ungewöhnlich.  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel entweder mithilfe der anspruchsregelsprache oder mithilfe der Send LDAP Group Membership als eine anspruchsregelvorlage in der AD FS-Verwaltung ausrichten\-in. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Auswählen der Gruppe eines Benutzers mithilfe der Objektauswahl  
  
-   Auswählen eines ausgehenden Anspruchstyps  
  
-   Wählen Sie eine ausgehende namensbezeichnerformat \(steht nur, wenn namens-ID aus dem Feld ausgehenden Anspruchs ausgewählt wird\)  
  
-   Angeben eines ausgehenden Anspruchswerts  
  
Weitere Informationen zum Erstellen dieser Regel finden Sie unter [Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](https://technet.microsoft.com/library/ee913569.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn Ansprüche anhand einer eingehenden SID ausgestellt werden sollen, die keine Gruppen-ID ist, können Sie hierzu die Regelvorlage „Transform an Incoming Claim“ verwenden. Wenn der Administrator die Namen aller Gruppen abrufen möchte, in welcher der Benutzer Mitglied ist, verwenden Sie stattdessen die Regelvorlage „Send LDAP Attributes as Claims“ mit dem **TokenGroups**-Attribut.  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>Beispiel: Ausstellen von Gruppenansprüchen auf Basis der Gruppenmitgliedschaft des Benutzers  
Die folgende Regel stellt Gruppenansprüche für einen Benutzer anhand einer eingehenden Gruppen-SID aus:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

