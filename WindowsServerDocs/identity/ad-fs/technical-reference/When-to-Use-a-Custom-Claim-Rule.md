---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: Wann sollte eine benutzerdefinierte Anspruchsregel verwendet
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5398f0b10d9e62548145fdde0354a3d047eb0ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-a-custom-claim-rule"></a>Wann sollte eine benutzerdefinierte Anspruchsregel verwendet
Sie schreiben eine benutzerdefinierte Anspruchsregel in Active Directory Federation Services \(AD FS\) mithilfe der anspruchsregelsprache, die das Framework, das anspruchsausstellungsmodul verwendet, um programmgesteuert zu generieren, zu transformieren, weiterleiten, und Filtern von Ansprüchen. Mithilfe einer benutzerdefinierten Regel können Sie Regeln mit komplexerer Logik als eine standardregelvorlage erstellen. Sollten Sie eine benutzerdefinierte Regel verwenden, wenn Sie möchten:  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem Structured Query Language \(SQL\) Attributspeicher extrahiert werden.  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem mit einem benutzerdefinierten LDAP-Filter \(LDAP\) Lightweight Directory Access Protocol-Attributspeicher extrahiert werden.  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem benutzerdefinierten Attributspeicher extrahiert werden.  
  
-   Senden von Ansprüchen nur dann, wenn zwei oder mehr eingehende Ansprüche vorhanden sind.  
  
-   Senden von Ansprüchen nur dann, wenn ein eingehender Anspruch entspricht ein komplexes Muster.  
  
-   Senden Sie die eingehenden Ansprüche mit komplexen Änderungen am Wert geltend machen.  
  
-   Erstellen von Ansprüchen für die Verwendung in späteren Regeln, ohne die Ansprüche tatsächlich zu senden.  
  
-   Erstellen eines ausgehenden Anspruchs anhand des Inhalts von mehr als einem eingehenden Anspruch.  
  
Sie können auch eine benutzerdefinierte Regel verwenden, wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss, aber es muss auch zusätzlichen Inhalt aufweisen.  
  
Die anspruchsregelsprache ist regelbasiert. Es hat einen Bedingungsteil und einen ausführungsteil. Sie können mithilfe der Syntax der anspruchsregelsprache aufzählen, hinzufügen, löschen oder Ansprüche gemäß den Bedürfnissen Ihrer Organisation ändern. Weitere Informationen, wie diese funktioniert Teile, finden Sie unter [The Role of the Claim Rule Language ](The-Role-of-the-Claim-Rule-Language.md).  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Sie bieten außerdem Detail dazu, wann eine benutzerdefinierte Anspruchsregel verwendet.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, die einen eingehenden Anspruch, eine Bedingung anwendet \ (wenn x, dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter.  
  
> [!IMPORTANT]  
> -   In AD FS-Verwaltungs-Snap-In die Ansprüche Regeln nur mit anspruchsregelvorlagen erstellt werden können  
> -   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
> -   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
> -   Anspruchsregelvorlagen erfordern immer einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie erstellen diese Regel definieren der Syntax benötigen Sie für den Vorgang mithilfe der anspruchsregelsprache und Vertrauensstellung mithilfe einer benutzerdefinierten Vorlage auf die Eigenschaften entweder einer Anspruchsanbieter fügen Sie das Ergebnis in das Textfeld ein, das in der senden bereitgestellt wird, oder eine vertrauende Seite vertrauen, das in der AD FS-Verwaltungs-Snap-In.  
  
Diese Regelvorlage bietet die folgenden Optionen:  
  
-   Anspruchsregelname angeben  
  
-   Geben Sie einen oder mehrere optionale Bedingung und eine ausstellungsanweisung mithilfe der AD FS-anspruchsregelsprache  
  
Weitere Informationen zum Erstellen einer benutzerdefinierten Regel mit dieser Vorlage finden Sie unter [erstellen eine Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](https://technet.microsoft.com/library/dd807049.aspx) in AD FS-Bereitstellungshandbuch.  
  
Für ein besseres Verständnis der Funktionsweise der anspruchsregelsprache, Anzeigen der Syntax der anspruchsregelsprache von anderen Regeln an, die bereits in das Snap-In durch Klicken auf die **Regelsprache anzeigen** Registerkarte in den Eigenschaften für diese Regel. Verwenden die Informationen in diesem Abschnittund der Syntaxinformationen auf dieser Registerkarte können Sie einen Einblick in die Vorgehensweise beim Erstellen eigener benutzerdefinierten Regeln bereitstellen.  
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>Beispiel: Zum Kombinieren von vor- und Nachnamen umzukehren, basierend auf den Attributwerten eines Benutzers  
Die folgende Regelsyntax kombiniert vor- und Nachnamen umzukehren aus Attributwerten in einem bestimmten Attributspeicher. Das Richtlinienmodul bildet ein kartesisches Produkt mit den Ergebnissen für jede Bedingung. Beispielsweise ist die Ausgabe für Vornamen {"Frank", "Alan"} und Nachnamen {"Miller", "Shen"} {"Frank Miller", "Frank Shen", "Alan Miller", "Alan Shen"}:  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>Beispiel: Zum Ausstellen eines vorgesetztenanspruchs basierend auf, ob Benutzer direkt unterstellte Mitarbeiter haben  
Die folgende Regel stellt einen vorgesetztenanspruch nur dann, wenn der Benutzer direkt unterstellte Mitarbeiter hat:  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>Beispiel: Zum Ausstellen eines PPID-Anspruchs basierend auf einem LDAP-Attribut  
Die folgende Regel stellt eine Private persönliche ID \(PPID\)-Anspruchs basierend auf den **Windowsaccountname** und **Originalissuer** Attribute von Benutzern in einem LDAP-Attributspeicher:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
Die folgenden: allgemeinen Attribute, die zur eindeutigen Identifizierung den Benutzer für diese Abfrage verwendet werden können  
  
-   **Benutzer-SID**  
  
-   **windowsaccountname**  
  
-   **"sAMAccountName"**  
  

