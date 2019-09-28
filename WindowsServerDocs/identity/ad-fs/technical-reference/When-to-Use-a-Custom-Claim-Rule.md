---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: Wann sollte eine benutzerdefinierte Anspruchsregel verwendet werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 61c129ab8472d7e85602fa0a0244c4a925050d93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407304"
---
# <a name="when-to-use-a-custom-claim-rule"></a>Wann sollte eine benutzerdefinierte Anspruchsregel verwendet werden?
Sie schreiben eine benutzerdefinierte Anspruchs Regel in \(Active Directory-Verbunddienste (AD FS)\) AD FS mithilfe der Anspruchs Regel Sprache. dabei handelt es sich um das Framework, das von der Anspruchs Ausstellungs-Engine zum programmgesteuerten generieren, transformieren, weiterleiten und Filtern verwendet wird. Claims. Mithilfe einer benutzerdefinierten Regel können Sie Regeln mit komplexerer Logik als bei einer Standardvorlage erstellen. Erwägen Sie eine benutzerdefinierte Regel, wenn Sie Folgendes vorhaben:  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem strukturierte Abfragesprache \(SQL\) -Attribut Speicher extrahiert werden.  
  
-   Senden von Ansprüchen basierend auf Werten, die mit einem benutzerdefinierten LDAP- \(Filter\) aus einem LDAP-Attribut Speicher für Lightweight Directory Access Protocol extrahiert werden.  
  
-   Senden von Ansprüchen basierend auf Werten, die aus einem benutzerdefinierten Attributspeicher extrahiert werden.  
  
-   Senden von Ansprüchen nur dann, wenn zwei oder mehr eingehende Ansprüche vorhanden sind.  
  
-   Senden von Ansprüchen nur dann, wenn ein eingehender Anspruchswert einem komplexen Muster entspricht.  
  
-   Senden von Ansprüchen mit komplexen Änderungen am Wert eines eingehenden Anspruchs.  
  
-   Erstellen von Ansprüchen für die Verwendung in späteren Regeln, ohne die Ansprüche tatsächlich zu senden.  
  
-   Erstellen eines ausgehenden Anspruchs anhand des Inhalts von mindestens einem eingehenden Anspruch.  
  
Sie können auch eine benutzerdefinierte Regel verwenden, wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss, jedoch auch zusätzlichen Inhalt aufweisen muss.  
  
Die Anspruchsregelsprache ist regelbasiert. Sie hat einen Bedingungsteil und einen Ausführungsteil. Sie können die Syntax der Anspruchsregelsprache verwenden, um Ansprüche gemäß den Bedürfnissen Ihrer Organisation aufzulisten, hinzuzufügen, zu löschen oder zu ändern. Weitere Informationen zur Funktionsweise der einzelnen Teile finden Sie [unter der Rolle der Anspruchs Regel Sprache](The-Role-of-the-Claim-Rule-Language.md).  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Sie bieten außerdem Details dazu, wann eine benutzerdefinierte Anspruchsregel verwendet werden sollte.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchs Regel stellt eine Instanz der Geschäftslogik dar, die einen eingehenden Anspruch annimmt, eine Bedingung \(darauf anwendet, wenn x\) , dann y und einen ausgehenden Anspruch basierend auf den Bedingungs Parametern erzeugt.  
  
> [!IMPORTANT]  
> -   Im Snap\--in "AD FS-Verwaltung" können Anspruchs Regeln nur mithilfe von Anspruchs Regel Vorlagen erstellt werden.  
> -   Anspruchs Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchs \(Anbieter (z. b.\) Active Directory oder einem anderen Verbunddienst oder von der Ausgabe der Akzeptanz Transformationsregeln für eine Anspruchs Anbieter-Vertrauensstellung.  
> -   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
> -   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchs Regeln und Anspruchs Regelsätzen finden Sie [unter Rolle der Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen zur Verarbeitung von Anspruchs Regelsätzen finden Sie [unter der Rolle der Anspruchs Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel, indem Sie zuerst die für Ihren Vorgang benötigte Syntax mithilfe der Anspruchs Regel Sprache erstellen und das Ergebnis dann in das Textfeld einfügen, das in der Vorlage senden von Ansprüchen mithilfe einer benutzerdefinierten Regel für die Eigenschaften eines der beiden Anspruchs Anbieter (TR) bereitgestellt wird. USt oder eine Vertrauensstellung der vertrauenden Seite im Snap\--in "AD FS-Verwaltung".  
  
Diese Regelvorlage bietet die folgenden Optionen:  
  
-   Anspruchsregelname angeben  
  
-   Geben Sie eine oder mehrere optionale Bedingungen und eine Ausstellungs Anweisung mithilfe der AD FS Anspruchs Regel Sprache ein.  
  
Weitere Anweisungen zum Erstellen einer benutzerdefinierten Regel mit dieser Vorlage finden Sie unter [Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](https://technet.microsoft.com/library/dd807049.aspx) im AD FS Bereitstellungs Handbuch.  
  
Um besser zu verstehen, wie die Anspruchs Regel Sprache funktioniert, zeigen Sie die Syntax der Anspruchs Regel Sprache von anderen Regeln an, die bereits\-im Snap-in vorhanden sind, indem Sie in den Eigenschaften für diese Regel auf die Registerkarte **Regel Sprache anzeigen** klicken. Anhand der Informationen in diesem Abschnitt und der Syntaxinformationen auf dieser Registerkarte erhalten Sie einen Einblick in die Vorgehensweise zum Erstellen von eigenen benutzerdefinierten Regeln.  
  
Weitere Informationen zum Verwenden der Anspruchs Regel Sprache finden Sie [unter der Rolle der Anspruchs Regel Sprache](The-Role-of-the-Claim-Rule-Language.md).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>Beispiel: Vorgehensweise beim Kombinieren von vor-und Nachnamen basierend auf den Namensattribut Werten eines Benutzers  
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
Die folgende Regel stellt einen privaten \(persönlichen Bezeichner PPID-Anspruch auf Grundlage der Attribute **windowsaccountname** und **originalissuer** von Benutzern in einem LDAP-\) Attribut Speicher aus:  
  
```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
Zu allgemeinen Attribute, die zur eindeutigen Identifizierung des Benutzers für diese Abfrage verwendet werden können, gehören die folgenden:  
  
-   **Benutzer-sid**  
  
-   **windowsaccountname**  
  
-   **sAMAccountName**  
  

