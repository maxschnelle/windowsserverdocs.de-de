---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: Wann sollte eine Send LDAP Attributes as Claims Rule verwenden
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05a2dd88057b64675bbc3bd30724d1eda0880c44
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>Wann sollte eine Send LDAP Attributes as Claims Rule verwenden
Sie können mit dieser Regel in Active Directory Federation Services \(AD FS\) verwenden, wenn Sie ausgehende Ansprüche ausgeben, die tatsächliche Lightweight Directory Access Protocol \(LDAP\) Attributwerte enthalten, die in einem Attributspeicher und dann einen Anspruchstyp jeweils der LDAP-Attribute zuordnen möchten. Weitere Informationen zu attributspeichern finden Sie unter [The Role of Attribute Stores](The-Role-of-Attribute-Stores.md).  
  
Wenn Sie diese Regel verwenden, Sie stellen einen Anspruch für jedes LDAP-Attribut, die Sie angeben, und, die der Regellogik entspricht, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen|Wenn der Attributspeicher dem *angegebenen Attributspeicher* und LDAP-Attribut entspricht *angegebenen Wert*, ordnen Sie die LDAP-Attributwert der *angegebenen ausgehenden Anspruch* geben und der Anspruch wird ausgegeben.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln. Sie bieten außerdem Detail zu Einsatzbereichen für das Senden von LDAP-Attributen als Ansprüche Regel verwenden.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \ (wenn x dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter. Die folgende Liste enthält wichtige Tipps, die Sie kennen sollten Anspruchsregeln bevor Sie weiter lesen in diesem Thema:  
  
-   In der AD FS-Verwaltungs-Snap-In können Anspruchsregeln nur erstellt werden mithilfe von anspruchsregelvorlagen  
  
-   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
  
-   Anspruchsregelvorlagen werden immer müssen Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
Wenn Sie das Senden von LDAP-Attributen als Ansprüche Regelvorlage verwenden, können Sie Attribute aus einem LDAP-Attributspeicher wie Active Directory oder Active Directory-Domänendienste \(AD DS\), senden ihre Werte als Ansprüche an die vertrauende Seite auswählen. Im Wesentlichen zugeordnet bestimmte LDAP-Attribute aus einem Attributspeicher, den auf einen Satz von ausgehenden Ansprüchen zu definieren, die für die Autorisierung verwendet werden können.  
  
Mithilfe dieser Vorlage können Sie mehrere Attribute, die als mehrere Ansprüche gesendet werden, aus einer einzigen Regel hinzufügen. Beispielsweise können diese Regelvorlage zum Erstellen einer Regel, an denen Attributwerte für authentifizierte Benutzer aus der **Unternehmen** und **Abteilung** Active Directory-Attribute, und klicken Sie dann diese Werte als zwei unterschiedliche ausgehende Ansprüche senden.  
  
Mit dieser Regel können auch Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie das Versenden der Gruppenmitgliedschaft als eine anspruchsregelvorlage. Weitere Informationen finden Sie unter [ein Senden der Gruppenmitgliedschaft als Anspruchsregel Verwendung](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie können erstellen diese Regel entweder mithilfe der anspruchsregelsprache oder mit dem Senden von LDAP-Attribute als Ansprüche Regel Vorlage in AD FS-Verwaltungs-Snap-In. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Wählen Sie einen Attributspeicher aus dem LDAP-Attribute extrahiert werden.  
  
-   Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen  
  
Weitere Informationen zum Erstellen dieser Regel finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx).  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Wenn die Abfrage an Active Directory, AD DS oder Active Directory Lightweight Directory Services \(AD LDS\) nicht mit einem LDAP-Attribut verglichen muss **SamAccountname**, müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Wenn keine Windows-Kontoname Anspruch gesetzt ist, müssen Sie auch eine benutzerdefinierte Regel an den Anspruch zum Abfragen von AD DS oder AD LDS verwenden.  
  
In den folgenden Beispielen werden bereitgestellt, mit denen Sie einige der zahlreichen Möglichkeiten kennen, können Sie eine benutzerdefinierte Regel mithilfe der anspruchsregelsprache für Abfragen und Extrahieren von Daten in einem Attributspeicher erstellen.  
  
### <a name="example-how-to-query-an-ad-lds-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines AD LDS-Attributspeichers und Zurückgeben eines angegebenen Werts  
Parameter müssen durch ein Semikolon getrennt werden. Der erste Parameter ist der LDAP-Filter. Die nachfolgende Parameter sind die Attribute bei allen übereinstimmenden Objekten zurückgegeben.  
  
Im folgende Beispiel veranschaulicht das Suchen eines Benutzers von der **sAMAccountName** -Attributs und das Ausstellen eines Anspruchs E\-Mail-Adresse, mit dem Wert der Mail-Attribut des Benutzers:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
Im folgende Beispiel veranschaulicht das Suchen eines Benutzers von der **Mail** -Attributs und das Ausstellen von Titel- und Ansprüche, die mit den Werten der des Benutzers **Titel** und **Displayname** Attribute:  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
Das folgende Beispiel zeigt, wie Sie das Suchen eines Benutzers von Mail und Title und das Ausstellen eines anzeigenamenanspruchs mithilfe des Benutzers **Displayname** Attribut:  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-and-return-a-specified-value"></a>Beispiel: Abfragen eines Active Directory-Attributspeichers und Zurückgeben eines angegebenen Werts  
Die Active Directory-Abfrage muss den Namen des Benutzers enthalten \ (mit der Domäne Tokentypen) als der letzte Parameter, damit die Active Directory-Attributspeicher die richtige Domäne Abfragen kann. Andernfalls wird die gleiche Syntax unterstützt.  
  
Im folgende Beispiel veranschaulicht das Suchen eines Benutzers von der **sAMAccountName** -Attribut in seiner Domäne und kehren Sie die **Mail** Attribut:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>Beispiel: Zum Abfragen eines Active Directory-Attributspeichers anhand des Werts eines eingehenden Anspruchs  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
Die vorherige Abfrage besteht aus den folgenden drei Teilen:  
  
-   Der LDAP-Filter – Sie geben diesen Teil der Abfrage die Objekte abgerufen, für die Sie Attribute abfragen möchten. Allgemeine Informationen zu gültigen LDAP-Abfragen finden Sie in RFC 2254. Wenn Sie einen Active Directory-Attributspeicher Abfragen und Sie keinen LDAP-Filter, die SamAccountName\ = {0} Abfrage wird davon ausgegangen, und der Active Directory-Attributspeicher erwartet einen Parameter, der den Wert für {0} Feed kann. Andernfalls wird ein Fehler zurückgegeben. Für einen LDAP-Attributspeicher als Active Directory die LDAP-Filter in der Abfrage nicht weggelassen, oder die Abfrage führt zu einem Fehler.  
  
-   Attributspezifikation: In diesem zweiten Teil der Abfrage, legen Sie die Attribute \ (das sind durch Kommas getrennt, wenn Sie mehrere Attribut Values\ verwenden), die Objekte zu Filtern werden sollen. Die Anzahl von Attributen, die Sie angeben, muss die Anzahl der Anspruchstypen entsprechen, die Sie in der Abfrage definieren.  
  
-   Active Directory-Domäne – nur, wenn der Attributspeicher Active Directory ist, geben Sie den letzten Teil der Abfrage. \ (Es ist nicht erforderlich, bei der Abfrage anderer Attribute Stores. \) dieser Teil der Abfrage wird verwendet, um das Benutzerkonto in der Form Domain\\name angeben. Der Active Directory-Attributspeicher anhand des Domänenteils den entsprechenden Domänencontroller herstellen, und führen Sie die Abfrage, und die Attribute anzufordern.  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-active-directory"></a>Beispiel: Verwendung zwei benutzerdefinierte Regeln zum Extrahieren der Manager E\-Nachricht aus einem Attribut in Active Directory  
Die folgenden zwei benutzerdefinierten Regeln, wenn in der unten angegebenen Reihenfolge zusammen verwendet, fragt Active Directory für die **Manager** -Attribut des Benutzers \(Rule 1\)-Konto und dann dieses Attribut verwenden, um das Benutzerkonto des Managers für die Abfrage der **Mail** -Attribut \(Rule 2\). Zum Schluss die **Mail** Attribut wird als "ManagerEmail"-Anspruch ausgestellt. Zusammenfassend Regel 1 fragt Active Directory und übergibt das Ergebnis der Abfrage an Regel 2, die dann den Manager extrahiert E\-Mail-Werte.  
  
Wenn beispielsweise diese Regeln Ausführung beendet wird, wird ein Anspruch ausgestellt, die der Manager E\ E-Mail-Adresse für einen Benutzer in der Domäne corp.fabrikam.com enthält.  
  
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
> Diese Regeln können nur dann, wenn der Manager eines Benutzers in derselben Domäne wie der Benutzer ist \ (in diesem Example\ corp.fabrikam.com).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](https://technet.microsoft.com/library/dd807115.aspx)  
  

