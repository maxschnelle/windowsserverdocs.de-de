---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: Einsatzbereiche für das Versenden einer Gruppenmitgliedschaft als Anspruchsregel
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 266f46ef30082541d49bf62d933c551f00fa08da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853793"
---
# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>Einsatzbereiche für das Versenden einer Gruppenmitgliedschaft als Anspruchsregel
Sie können diese Regel in Active Directory-Verbunddienste (AD FS) \(AD FS\) verwenden, wenn Sie nur für die Benutzer, die Mitglieder einer angegebenen Active Directory Sicherheitsgruppe sind, einen neuen ausgehenden Anspruchs Wert ausgeben möchten. Wenn Sie diese Regel anwenden, stellen Sie einen einzelnen Anspruch aus, der nur für die angegebene Gruppe gilt, wie in folgender Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Ausgehender Anspruchswert|Wenn die Gruppenmitgliedschaft eines Benutzers gleich der *angegebenen Gruppe* und der ausgehende Anspruchstyp dem *angegebenen Anspruchstyp*entspricht, ersetzen Sie den vorhandenen Wert des Gruppennamens durch den *angegebenen ausgehenden Anspruchs Wert* , und geben Sie den Anspruch aus.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Darüber hinaus werden Details zu Einsatzbereichen für das Versenden der Gruppenmitgliedschaft als Anspruchsregel angesprochen.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchs Regel stellt eine Instanz der Geschäftslogik dar, die einen eingehenden Anspruch annimmt, eine Bedingung darauf anwenden \(wenn x, dann y\) und einen ausgehenden Anspruch basierend auf den Bedingungs Parametern erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS Verwaltungs-Snap\-in können Anspruchs Regeln nur mithilfe von Anspruchs Regel Vorlagen erstellt werden.  
  
-   Anspruchs Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchs Anbieter \(z. b. Active Directory oder einer anderen Verbunddienst\) oder aus der Ausgabe der Akzeptanz Transformationsregeln für eine Anspruchs Anbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchs Regeln und Anspruchs Regelsätzen finden Sie [unter Rolle der Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen zur Verarbeitung von Anspruchs Regelsätzen finden Sie [unter der Rolle der Anspruchs Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="outgoing-claim-value"></a>Ausgehender Anspruchswert  
Mithilfe der Regelvorlage „Send Group Membership as a Claim“, können Sie einen Anspruch ausstellen, der abhängig davon ist, ob ein Benutzer Mitglied einer von Ihnen festgelegten Gruppe ist.  
  
Mit anderen Worten: Diese Regel Vorlage gibt nur dann einen Anspruch aus, wenn der Benutzer die Gruppensicherheits-ID \(sid\) hat, die mit der Active Directory Gruppe übereinstimmt, die der Administrator angibt. Alle Benutzer, die sich bei Active Directory Domain Services \(AD DS\) authentifizieren, haben für jede Gruppe, der Sie angehören, eingehende Gruppen-SID-Ansprüche. Standardmäßig leiten die Akzeptanztransformationsregeln in der Active Directory-Anspruchsanbieter-Vertrauensstellung diese Gruppen-SID-Ansprüche durch. Die Verwendung dieser Gruppen-SIDs als Grundlage für das Ausstellen von Ansprüchen ist viel schneller als das Nachschlagen der Benutzergruppen in AD DS.  
  
Wenn Sie diese Regel verwenden, wird nur ein einzelner Anspruch anhand der ausgewählten Active Directory-Gruppe gesendet. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel nutzen, die einen Gruppenanspruch mit dem Wert „Admin“ sendet, wenn der Benutzer ein Mitglied der Sicherheitsgruppe „Domänenadmins“ ist.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel in einer Anspruchsanbietervertrauensstellung  
Administratoren sollten diesen Regeltyp in Akzeptanztransformationsregeln des Anspruchsanbieters nur dann verwenden, wenn von dem Anspruchsanbieter Gruppen-SIDs empfangen werden. Das ist für Anspruchsanbieter außer Active Directory oder AD DS sehr ungewöhnlich.  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel entweder mithilfe der Anspruchs Regel Sprache oder mithilfe der Regel Vorlage "Send LDAP Group Membership as a Claim" im AD FS-Verwaltungs-Snap\-in. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Auswählen der Gruppe eines Benutzers mithilfe der Objektauswahl  
  
-   Auswählen eines ausgehenden Anspruchstyps  
  
-   Wählen Sie ein Ausgeh Endes namens-ID-Format aus \(das nur verfügbar ist, wenn die namens-ID aus dem Feld Ausgangs Anspruchstyp ausgewählt wird\)  
  
-   Angeben eines ausgehenden Anspruchswerts  
  
Weitere Informationen zum Erstellen dieser Regel finden [Sie unter Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](https://technet.microsoft.com/library/ee913569.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn Ansprüche anhand einer eingehenden SID ausgestellt werden sollen, die keine Gruppen-ID ist, können Sie hierzu die Regelvorlage „Transform an Incoming Claim“ verwenden. Wenn der Administrator die Namen aller Gruppen abrufen möchte, in welcher der Benutzer Mitglied ist, verwenden Sie stattdessen die Regelvorlage „Send LDAP Attributes as Claims“ mit dem **TokenGroups**-Attribut.  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>Beispiel: Ausstellen von Gruppen Ansprüchen basierend auf der Gruppenmitgliedschaft des Benutzers  
Die folgende Regel stellt Gruppenansprüche für einen Benutzer anhand einer eingehenden Gruppen-SID aus:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

