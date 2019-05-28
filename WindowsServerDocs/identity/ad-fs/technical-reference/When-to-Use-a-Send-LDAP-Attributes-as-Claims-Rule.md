---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: Verwenden einer Regel zum Senden von LDAP-Attributen als Ansprüche
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5af00db05c572a45811eea49b832a054a9e0e492
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188249"
---
# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>Verwenden einer Regel zum Senden von LDAP-Attributen als Ansprüche
Verwenden Sie diese Regel in Active Directory-Verbunddienste \(AD FS\) sollen ausgehende Ansprüche ausgeben, die tatsächliche Lightweight Directory Access Protocol enthalten \(LDAP\) Attributwerte, die im vorhanden ein Attribut speichern, und klicken Sie dann den einzelnen LDAP-Attribute einen Anspruchstyp zuordnen. Weitere Informationen zu attributspeichern finden Sie unter [The Role of Attribute Stores](The-Role-of-Attribute-Stores.md).  
  
Wenn Sie diese Regel verwenden, geben Sie einen Anspruch für jedes angegebene LDAP-Attribut aus, das der Regellogik entspricht, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen|Wenn der Attributspeicher dem *angegebenen Attributspeicher* entspricht und das LDAP-Attribut dem *angegebenen Wert*, dann wird der LDAP-Attributwert dem *angegebenen ausgehenden Anspruch* zugeordnet, und der Anspruch wird ausgegeben.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Darüber hinaus werden Details zu Anwendungsszenarios für die Verwendung der Regel „LDAP-Attribute als Ansprüche senden“ beschrieben.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
  
-   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
Wenn Sie das Senden von LDAP-Attributen als Ansprüche Regelvorlage verwenden, können Sie Attribute auswählen, aus einem LDAP-Attributspeicher wie Active Directory oder Active Directory Domain Services \(AD DS\) , deren Werte als Ansprüche an die vertrauende Seite senden . Damit werden im Prinzip bestimmte LDAP-Attribute aus einem von Ihnen festgelegten Attributspeicher einem Satz von ausgehenden Ansprüchen zugeordnet, der für die Autorisierung verwendet werden kann.  
  
Mithilfe dieser Vorlage können Sie mehrere Attribute hinzufügen, die von einer Regel aus als mehrere Ansprüche gesendet werden. Sie können diese Regelvorlage z. B. verwenden, um eine Regel zu erstellen, die Attributwerte für authentifizierte Benutzer aus den Active Directory-Attributen **Unternehmen** und **Abteilung** heraussucht und dann diese Werte als zwei unterschiedliche ausgehende Ansprüche sendet.  
  
Mit dieser Regel können Sie auch alle Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie die Regelvorlage „Gruppenmitgliedschaft als Anspruch senden“. Weitere Informationen finden Sie unter [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie können erstellen diese Regel entweder mithilfe der anspruchsregelsprache oder mithilfe der senden-LDAP-Attribute als Ansprüche Regelvorlage in AD FS-Verwaltungs ausrichten\-in. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Wählen Sie einen Attributspeicher aus, aus dem die LDAP-Attribute extrahiert werden.  
  
-   Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
  
Weitere Informationen zum Erstellen dieser Regel finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn die Abfrage an Active Directory, AD DS und Active Directory Lightweight Directory Services \(AD LDS\) müssen Vergleich mit einem LDAP-Attribut als **"sAMAccountName"** , müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Enthält der Eingabesatz keinen Windows-Kontonamenanspruch, müssen Sie ebenfalls eine benutzerdefinierte Regel verwenden, um den Anspruch anzugeben, der für die Abfrage von AD DS oder AD LDS verwendet wird.  
  
Die folgenden Beispielen sollen die verschiedenen Methoden zum Erstellen von benutzerdefinierten Regeln mithilfe der Anspruchsregelsprache für das Abfragen und Extrahieren von Daten in einem Attributspeicher veranschaulichen.  
  
### <a name="example-how-to-query-an-adlds-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines AD LDS-Attributspeichers und Zurückgeben eines angegebenen Werts  
Die Parameter müssen durch ein Semikolon voneinander getrennt werden. Der erste Parameter ist der LDAP-Filter. Die nachfolgende Parameter sind die Attribute, die bei allen übereinstimmenden Objekten zurückgegeben werden sollen.  
  
Das folgende Beispiel zeigt, wie Sie das Suchen eines Benutzers von der **"sAMAccountName"** Attribut, und geben Sie einen e\-Anspruch e-Mail-Adresse, unter Verwendung des Werts des Mail-Attribut des Benutzers:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
Das folgende Beispiel veranschaulicht das Suchen eines Benutzers mithilfe des **mail**-Attributs und das Ausstellen eines Titel- und Anzeigenamenanspruchs mithilfe des Werts der Attribute **title** und **displayname** des Benutzers:  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
Das folgende Beispiel veranschaulicht das Suchen eines Benutzers mithilfe der Attribute mail und title und das Ausstellen eines Anzeigenamenanspruchs mithilfe des **displayname**-Attributs des Benutzers:  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines Active Directory-Attributspeichers und Zurückgeben eines angegebenen Werts  
Die Active Directory-Abfrage muss den Namen des Benutzers enthalten \(mit dem Domänennamen\) wie der letzte Parameter, damit die Active Directory-Attributspeicher die richtige Domäne Abfragen kann. Ansonsten wird die gleiche Syntax unterstützt.  
  
Das folgenden Beispiel veranschaulicht das Suchen eines Benutzers mithilfe des **sAMAccountName**-Attributs in seiner Domäne und das Zurückgeben des zugehörigen **mail**-Attributs:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>Beispiel: Abfragen des Active Directory-Attributspeichers anhand des Werts eines eingehenden Anspruchs  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
Die vorherige Abfrage besteht aus den folgenden drei Teilen:  
  
-   LDAP-Filter: Sie geben diesen Teil der Abfrage an, um die Objekte abzurufen, für die Sie Attribute abfragen möchten. Allgemeine Informationen zu gültigen LDAP-Abfragen finden Sie in RFC 2254. Wenn Sie einen Active Directory-Attributspeicher Abfragen und Sie keinen LDAP-Filter, der "sAMAccountName" angeben\= {0} Abfrage wird davon ausgegangen, dass und der Active Directory-Attributspeicher erwartet einen Parameter, der den Wert für feedkann{0}. Andernfalls wird für die Abfrage ein Fehler zurückgegeben. Für andere LDAP-Attributspeicher als Active Directory dürfen Sie den LDAP-Filter in der Abfrage nicht weggelassen, da die Abfrage einen Fehler zurückgibt.  
  
-   Attributspezifikation: In diesem zweiten Teil der Abfrage geben Sie die Attribute \(die sind durch Kommas\-getrennt, wenn Sie mehrere Attributwerte können\) , die aus die gefilterten Objekte werden sollen. Die Anzahl der angegebenen Attribute muss die Anzahl der Anspruchstypen entsprechen, die Sie in der Abfrage definiert haben.  
  
-   Active Directory-Domäne: Den letzten Teil der Abfrage geben Sie nur an, wenn der Attributspeicher Active Directory ist. \(Es ist nicht erforderlich, wenn die Abfrage anderer Attributspeicher.\) Dieser Teil der Abfrage wird verwendet, um das Benutzerkonto anzugeben, in der Form Domain\\Name. Der Active Directory-Attributspeicher bestimmt mithilfe des Domänenteils den entsprechenden Domänencontroller, um mit diesem eine Verbindung herzustellen, die Abfrage auszuführen und die Attribute anzufordern.  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-activedirectory"></a>Beispiel: Gewusst wie: Verwenden Sie zwei benutzerdefinierte Regeln zum Extrahieren des e-Managers\-e-Mail-Nachrichten aus einem Attribut in Active Directory  
Die folgenden zwei benutzerdefinierten Regeln, wenn in der unten gezeigten Reihenfolge zusammen verwendet fragt Active Directory für die **Manager** Attribut des Benutzerkontos \(Regel 1\) und klicken Sie dann dieses Attribut verwenden, um vom Benutzer abzufragen Konto des Managers für die **-e-Mails** Attribut \(Regel 2\). Abschließend wird das **mail**-Attribut als „ManagerEmail“-Anspruch ausgestellt. Zusammenfassend Regel 1 fragt Active Directory und übergibt das Ergebnis der Abfrage an Regel 2, die Sie dann den Manager e extrahiert\-e-Mail-Werte.  
  
Z. B. wenn diese Regeln Ausführung beendet ist, ein Anspruch wird ausgegeben, der den Vorgesetzten e enthält\-e-Mail-Adresse für einen Benutzer in der Domäne "corp.Fabrikam.com".  
  
**Regel 1**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
=> add(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"), query = "sAMAccountName=  
{0};mail,userPrincipalName,extensionAttribute5,manager,department,extensionAttribute2,cn;{1}", param = regexreplace(c.Value, "(?  
<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
**Regel 2**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
&& c1:[Type == "http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerEmail"), query = "distinguishedName={0};mail;{1}", param = c1.Value,   
param = regexreplace(c1.Value, ".*DC=(?<domain>.+),DC=corp,DC=fabrikam,DC=com", "${domain}\username"));  
```  
  
> [!NOTE]  
> Diese Regeln funktionieren nur, wenn Sie den Manager des Benutzers in der gleichen Domäne wie der Benutzer ist \("corp.Fabrikam.com" in diesem Beispiel\).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

