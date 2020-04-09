---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: Verwenden einer Regel zum Senden von LDAP-Attributen als Ansprüche
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bc7b98a5d65bf03eb11ed57a8a5f9a0ea696df19
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853773"
---
# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>Verwenden einer Regel zum Senden von LDAP-Attributen als Ansprüche
Sie können diese Regel in Active Directory-Verbunddienste (AD FS) \(AD FS\) verwenden, wenn Sie ausgehende Ansprüche ausgeben möchten, die tatsächliche Lightweight Directory Access Protocol-\(LDAP-\) Attributwerte enthalten, die in einem Attribut Speicher vorhanden sind, und dann jedem der LDAP-Attribute einen Anspruchstyp zuordnen. Weitere Informationen zu Attribut speichern finden Sie [unter der Rolle von Attribut speichern](The-Role-of-Attribute-Stores.md).  
  
Wenn Sie diese Regel verwenden, geben Sie einen Anspruch für jedes angegebene LDAP-Attribut aus, das der Regellogik entspricht, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen|Wenn der Attributspeicher dem *angegebenen Attributspeicher* entspricht und das LDAP-Attribut dem *angegebenen Wert*, dann wird der LDAP-Attributwert dem *angegebenen ausgehenden Anspruch* zugeordnet, und der Anspruch wird ausgegeben.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Darüber hinaus werden Details zu Anwendungsszenarios für die Verwendung der Regel „LDAP-Attribute als Ansprüche senden“ beschrieben.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchs Regel stellt eine Instanz der Geschäftslogik dar, die einen eingehenden Anspruch annimmt, eine Bedingung darauf anwenden \(wenn x, dann y\) und einen ausgehenden Anspruch basierend auf den Bedingungs Parametern erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS Verwaltungs-Snap\-in können Anspruchs Regeln nur mithilfe von Anspruchs Regel Vorlagen erstellt werden.  
  
-   Anspruchs Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchs Anbieter \(z. b. Active Directory oder einer anderen Verbunddienst\) oder aus der Ausgabe der Akzeptanz Transformationsregeln für eine Anspruchs Anbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchs Regeln und Anspruchs Regelsätzen finden Sie [unter Rolle der Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen zur Verarbeitung von Anspruchs Regelsätzen finden Sie [unter der Rolle der Anspruchs Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
Wenn Sie die Regel Vorlage "LDAP-Attribute als Ansprüche senden" verwenden, können Sie Attribute aus einem LDAP-Attribut Speicher auswählen, z. b. Active Directory oder Active Directory Domain Services \(AD DS\), um deren Werte als Ansprüche an die vertrauende Seite zu senden. Damit werden im Prinzip bestimmte LDAP-Attribute aus einem von Ihnen festgelegten Attributspeicher einem Satz von ausgehenden Ansprüchen zugeordnet, der für die Autorisierung verwendet werden kann.  
  
Mithilfe dieser Vorlage können Sie mehrere Attribute hinzufügen, die von einer Regel aus als mehrere Ansprüche gesendet werden. Sie können diese Regelvorlage z. B. verwenden, um eine Regel zu erstellen, die Attributwerte für authentifizierte Benutzer aus den Active Directory-Attributen **Unternehmen** und **Abteilung** heraussucht und dann diese Werte als zwei unterschiedliche ausgehende Ansprüche sendet.  
  
Mit dieser Regel können Sie auch alle Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie die Regelvorlage „Gruppenmitgliedschaft als Anspruch senden“. Weitere Informationen finden Sie unter [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie können diese Regel entweder mithilfe der Anspruchs Regel Sprache oder mithilfe der Regel Vorlage "LDAP-Attribute als Ansprüche senden" im AD FS-Verwaltungs-Snap\-in erstellen. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Wählen Sie einen Attributspeicher aus, aus dem die LDAP-Attribute extrahiert werden.  
  
-   Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
  
Weitere Informationen zum Erstellen dieser Regel finden [Sie unter Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn die Abfrage zum Active Directory, AD DS oder Active Directory Lightweight Directory Services \(AD LDS\) mit einem anderen LDAP-Attribut als **sAMAccountName**verglichen werden muss, müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Enthält der Eingabesatz keinen Windows-Kontonamenanspruch, müssen Sie ebenfalls eine benutzerdefinierte Regel verwenden, um den Anspruch anzugeben, der für die Abfrage von AD DS oder AD LDS verwendet wird.  
  
Die folgenden Beispielen sollen die verschiedenen Methoden zum Erstellen von benutzerdefinierten Regeln mithilfe der Anspruchsregelsprache für das Abfragen und Extrahieren von Daten in einem Attributspeicher veranschaulichen.  
  
### <a name="example-how-to-query-an-adlds-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines AD LDS-Attributspeichers und Zurückgeben eines angegebenen Werts  
Die Parameter müssen durch ein Semikolon voneinander getrennt werden. Der erste Parameter ist der LDAP-Filter. Die nachfolgende Parameter sind die Attribute, die bei allen übereinstimmenden Objekten zurückgegeben werden sollen.  
  
Das folgende Beispiel zeigt, wie Sie einen Benutzer anhand des **sAMAccountName** -Attributs suchen und einen e\-e-Mail-Adress Anspruchs mithilfe des Werts des Mail-Attributs des Benutzers ausgeben:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
Im folgenden Beispiel wird gezeigt, wie Sie einen Benutzer anhand des **Mail** -Attributs suchen und Titel-und Anzeige Namen Ansprüche mithilfe der Werte der Attribute **Title** und Display **Name** des Benutzers ausgeben:  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
Das folgende Beispiel zeigt, wie Sie einen Benutzer per e-Mail und Titel suchen und dann einen anzeigen Amen mit dem **Display Name** -Attribut des Benutzers ausstellen:  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines Active Directory-Attributspeichers und Zurückgeben eines angegebenen Werts  
Die Active Directory Abfrage muss den Namen des Benutzers enthalten \(der den Domänen Namen\) als letzten Parameter hat, damit der Active Directory Attribut Speicher die richtige Domäne Abfragen kann. Ansonsten wird die gleiche Syntax unterstützt.  
  
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
  
-   LDAP-Filter: Sie geben diesen Teil der Abfrage an, um die Objekte abzurufen, für die Sie Attribute abfragen möchten. Allgemeine Informationen zu gültigen LDAP-Abfragen finden Sie in RFC 2254. Wenn Sie einen Active Directory-Attribut Speicher Abfragen und keinen LDAP-Filter angeben, wird die sAMAccountName-\={0}-Abfrage angenommen, und der Active Directory-Attribut Speicher erwartet einen Parameter, der den Wert für {0}Feed erhalten kann. Andernfalls wird für die Abfrage ein Fehler zurückgegeben. Für andere LDAP-Attributspeicher als Active Directory dürfen Sie den LDAP-Filter in der Abfrage nicht weggelassen, da die Abfrage einen Fehler zurückgibt.  
  
-   Attribut Spezifikation – in diesem zweiten Teil der Abfrage geben Sie die Attribute \(die durch Kommas getrennt sind\-, wenn Sie mehrere Attributwerte\), die Sie aus den gefilterten Objekten heraus verwenden möchten. Die Anzahl der angegebenen Attribute muss die Anzahl der Anspruchstypen entsprechen, die Sie in der Abfrage definiert haben.  
  
-   Active Directory-Domäne: Den letzten Teil der Abfrage geben Sie nur an, wenn der Attributspeicher Active Directory ist. \(dies nicht erforderlich ist, wenn Sie andere Attribut Speicher Abfragen.\) dieser Teil der Abfrage wird verwendet, um das Benutzerkonto in der Form "Domäne\\Name" anzugeben. Der Active Directory-Attributspeicher bestimmt mithilfe des Domänenteils den entsprechenden Domänencontroller, um mit diesem eine Verbindung herzustellen, die Abfrage auszuführen und die Attribute anzufordern.  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-activedirectory"></a>Beispiel: Verwenden von zwei benutzerdefinierten Regeln zum Extrahieren des Vorgesetzten e\-Mail aus einem Attribut in Active Directory  
Die folgenden beiden benutzerdefinierten Regeln, die in der unten gezeigten Reihenfolge verwendet werden, Fragen Active Directory für das **Manager** -Attribut des Benutzerkontos \(Regel 1\) und verwenden dann dieses Attribut, um das Benutzerkonto des Managers für das **Mail** -Attribut \(Regel 2\)abzufragen. Schließlich wird das **Mail** -Attribut als "ManagerEmail"-Anspruch ausgestellt. Zusammenfassend gilt: Regel 1 fragt Active Directory ab und übergibt das Ergebnis der Abfrage an Regel 2, die dann die e\-e-Mail-Werte des Vorgesetzten extrahiert.  
  
Wenn diese Regeln z. b. ausgeführt werden, wird ein Anspruch ausgegeben, der die e\--e-Mail-Adresse des Vorgesetzten für einen Benutzer in der Corp.fabrikam.com-Domäne enthält.  
  
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
> Diese Regeln funktionieren nur, wenn sich der Manager des Benutzers in derselben Domäne befindet wie der Benutzer \(Corp.fabrikam.com in diesem Beispiel\).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

