---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: Wann sollte eine benutzerdefinierte Anspruchsregel verwendet werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b08622cd9eefa153e2fe8403fbe85077644182f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813111"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-a-custom-claim-rule"></a>Wann sollte eine benutzerdefinierte Anspruchsregel verwendet werden?
Sie schreiben eine benutzerdefinierte Anspruchsregel in Active Directory-Verbunddienste \(AD FS\) mithilfe der anspruchsregelsprache, die das Framework die anspruchsausstellungs-Engine verwendet wird, um programmgesteuert zu generieren, transformieren, pass-through- und Filtern Ansprüche. Mithilfe einer benutzerdefinierten Regel können Sie Regeln mit komplexerer Logik als bei einer Standardvorlage erstellen. Erwägen Sie eine benutzerdefinierte Regel, wenn Sie Folgendes vorhaben:  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem Structured Query Language extrahiert werden \(SQL\) Attributspeicher.  
  
-   Senden von Ansprüchen basierend auf Werten, die über eine Lightweight Directory Access Protocol extrahiert werden \(LDAP\) Attributspeicher mit einem benutzerdefinierten LDAP-Filter.  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem benutzerdefinierten Attributspeicher extrahiert werden.  
  
-   Senden von Ansprüchen nur dann, wenn zwei oder mehr eingehende Ansprüche vorhanden sind.  
  
-   Senden von Ansprüchen nur dann, wenn ein eingehender Anspruchswert einem komplexen Muster entspricht.  
  
-   Senden von Ansprüchen mit komplexen Änderungen am Wert eines eingehenden Anspruchs.  
  
-   Erstellen von Ansprüchen für die Verwendung in späteren Regeln, ohne die Ansprüche tatsächlich zu senden.  
  
-   Erstellen eines ausgehenden Anspruchs anhand des Inhalts von mindestens einem eingehenden Anspruch.  
  
Sie können auch eine benutzerdefinierte Regel verwenden, wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss, jedoch auch zusätzlichen Inhalt aufweisen muss.  
  
Die Anspruchsregelsprache ist regelbasiert. Sie hat einen Bedingungsteil und einen Ausführungsteil. Sie können die Syntax der Anspruchsregelsprache verwenden, um Ansprüche gemäß den Bedürfnissen Ihrer Organisation aufzulisten, hinzuzufügen, zu löschen oder zu ändern. Weitere Informationen dazu, wie jedes dieser funktioniert Teilen, finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Sie bieten außerdem Details dazu, wann eine benutzerdefinierte Anspruchsregel verwendet werden sollte.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, die einen eingehenden Anspruch dar, die eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt.  
  
> [!IMPORTANT]  
> -   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
> -   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
> -   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
> -   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel durch Definieren der Syntax, die für der Vorgang mithilfe der anspruchsregelsprache und klicken Sie dann einfügen, das Ergebnis in den Text-Feld, in den Send-Anspruch mithilfe bereitgestellt, müssen Sie eine benutzerdefinierte Regelvorlage in den Eigenschaften des entweder einer Anspruchsanbieter tr USt oder eine relying Party trust im AD FS-Verwaltungs-Snap-\-in.  
  
Diese Regelvorlage bietet die folgenden Optionen:  
  
-   Anspruchsregelname angeben  
  
-   Geben Sie eine oder mehrere optionale Bedingungen sowie eine ausgabeanweisung mithilfe der AD FS-anspruchsregelsprache  
  
Weitere Anweisungen zum Erstellen einer benutzerdefinierten Regel mit dieser Vorlage finden Sie [erstellen Sie eine Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](https://technet.microsoft.com/library/dd807049.aspx) in AD FS-Bereitstellungshandbuch.  
  
Zeigen Sie für ein besseres Verständnis der Funktionsweise der anspruchsregelsprache, Syntax der anspruchsregelsprache von anderen Regeln, die bereits vorhanden sind, im Snap\-in durch Klicken auf die **Regelsprache anzeigen** Registerkarte in den Eigenschaften für diese Regel. Anhand der Informationen in diesem Abschnitt und der Syntaxinformationen auf dieser Registerkarte erhalten Sie einen Einblick in die Vorgehensweise zum Erstellen von eigenen benutzerdefinierten Regeln.  
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>Beispiel: Kombinieren von Vor- und Nachnamen basierend auf den Namensattributwerten eines Benutzers  
Die folgende Regelsyntax kombiniert Vor- und Nachnamen aus Attributwerten in einem bestimmten Attributspeicher. Das Richtlinienmodul bildet ein kartesisches Produkt mit den Ergebnissen für jede Bedingung. Beispielsweise ist die Ausgabe für Vornamen {"Frank", "Alan"} und Nachnamen {"Miller", "Shen"} {"Frank Miller", "Frank Shen", "Alan Miller", "Alan Shen"}:  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>Beispiel: Ausstellen eines Vorgesetztenanspruchs basierend darauf, ob Benutzer direkt unterstellte Mitarbeiter haben  
Die folgende Regel stellt einen Vorgesetztenanspruch nur aus, wenn der Benutzer direkt unterstellte Mitarbeiter hat:  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>Beispiel: Ausstellen eines PPID-Anspruchs basierend auf einem LDAP-Attribut  
Die folgende Regel stellt einen privaten persönlichen Bezeichner \(PPID\) Anspruch basierend auf den **Windowsaccountname** und **Originalissuer** Attribute von Benutzern in einem LDAP-Attribut abspeichern:  
  
```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
Zu allgemeinen Attribute, die zur eindeutigen Identifizierung des Benutzers für diese Abfrage verwendet werden können, gehören die folgenden:  
  
-   **Benutzer-SID**  
  
-   **windowsaccountname**  
  
-   **samaccountname**  
  

