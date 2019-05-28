---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: 'AD FS 2016: Einstellungen für einmaliges Anmelden'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f3719277c80eae2bf2a4d923146920d17546601d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188727"
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS-einzelnen SSO-Einstellungen

Einmaliges Anmelden (SSO) können Benutzer sich einmal authentifizieren und Zugriff auf mehrere Ressourcen ohne weitere Anmeldeinformationen aufgefordert zu werden.  Dieser Artikel beschreibt die standardmäßige AD FS-Verhalten für SSO als auch die Konfigurationseinstellungen, mit die Sie dieses Verhalten anpassen können.  

## <a name="supported-types-of-single-sign-on"></a>Unterstützte Typen des einmaligen Anmeldens

AD FS unterstützt mehrere Typen von Single-Sign-On-Funktionen:  
  
-   **SSO-Sitzung**  
  
     SSO-Sitzungscookies werden für den authentifizierten Benutzer geschrieben, die weitere aufforderungen zu vermeiden, bei der der Benutzer die Anwendungen während einer bestimmten Sitzung wechselt. Aber wenn eine bestimmte Sitzung endet, wird der Benutzer zur Eingabe der Anmeldeinformationen erneut aufgefordert werden.  
  
     AD FS wird Sitzung SSO-Cookies standardmäßig festgelegt, wenn Benutzergeräte nicht registriert sind. Wenn die Browsersitzung beendet wurde und neu gestartet wird, wird diese Sitzungscookie gelöscht und ist nicht mehr gültig.  
  
-   **Beständiges einmaliges Anmelden**  
  
     Permanente SSO-Cookies werden für den authentifizierten Benutzer geschrieben, die weitere aufforderungen zu vermeiden, bei der der Benutzer die Anwendungen für wechselt, solange das dauerhafte SSO-Cookie gültig ist. Der Unterschied zwischen SSO und die SSO-Sitzung persistent ist beständiges einmaliges Anmelden über verschiedene Sitzungen hinweg beibehalten werden kann.  
  
     AD FS wird SSO-Cookies mit persistenten festgelegt, wenn das Gerät registriert ist. AD FS wird auch ein permanentes Cookie für die SSO-festgelegt, wenn ein Benutzer die Option "angemeldet bleiben" auswählt. Wenn das dauerhafte SSO-Cookie mehr nicht gültig ist, wird zurückgewiesen und gelöscht werden.  
  
-   **Anwendung bestimmte SSO**  
  
     In diesem Szenario OAuth wird ein Aktualisierungstoken verwendet, um den SSO-Status des Benutzers innerhalb des Bereichs einer bestimmten Anwendung beizubehalten.  
  
     Wenn ein Gerät registriert ist, wird eine AD FS festgelegt die Ablaufzeit eines aktualisierungstokens basierend auf der persistenten SSO-Cookies-Lebensdauer für ein registriertes Gerät, das standardmäßig 7 Tage für AD FS 2012 R2 und bis zu maximal 90 Tage in AD FS 2016 ist, wenn sie ihr Gerät zu verwenden zugreifen Sie AD FS-Ressourcen in einem Zeitfenster von 14 Tagen an. 

Wenn das Gerät ist nicht registriert, aber der Benutzer wählt die Option "angemeldet bleiben", die Ablaufzeit für das Aktualisierungstoken, das ist die permanente SSO-Cookies-Lebensdauer für "Keep angemeldet" gleich wird 1 Tag, die standardmäßig mit bis zu 7 Tage. Andernfalls aktualisieren Sie Tokengültigkeitsdauer Equals SSO-Cookie Sitzungsdauer handelt es sich standardmäßig auf 8 Stunden  
  
 Wie oben erwähnt, erhalten Benutzer registrierter Geräte immer ein beständiges einmaliges Anmelden, es sei denn, die beständige einmaliges Anmelden deaktiviert ist. Nicht registrierte Geräte beständiges einmaliges Anmelden erzielt werden, indem die "angemeldet bleiben in" aktivieren ("angemeldet bleiben")-Funktion. 
 
 Für Windows Server 2012 R2 PSSO für das Szenario "Angemeldet bleiben" aktivieren. Sie müssen zum Installieren dieses [Hotfix](https://support.microsoft.com/en-us/kb/2958298/) ebenfalls Teil der von [August 2014 update Rollup für Windows RT 8.1, Windows 8.1 und Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/2975719).   

Aufgabe | PowerShell | Beschreibung
------------ | ------------- | -------------
Beständiges einmaliges Anmelden aktivieren/deaktivieren | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| Beständiges einmaliges Anmelden ist standardmäßig aktiviert. Wenn sie deaktiviert ist, wird kein Cookie PSSO geschrieben werden.
"Aktivieren/Deaktivieren von"angemeldet bleiben" | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | Funktion "Angemeldet bleiben" ist standardmäßig deaktiviert. Wenn es aktiviert ist, wird Benutzer eine Wahl "angemeldet bleiben" auf AD FS-Anmeldeseite angezeigt.



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016 - Single-Sign-On und authentifizierte Geräte
AD FS 2016 ändert die PSSO aus, wenn der anforderer von einem registrierten Gerät, auf maximal 90 Tage zu erhöhen, jedoch erfordern eine Authenticvation innerhalb von 14 Tagen (Gerätefenster Nutzung) authentifiziert wird.
Nach der Eingabe von Anmeldeinformationen zum ersten Mal erhalten standardmäßig Benutzer mit registrierten Geräten einmaliges Anmelden für einen Zeitraum von 90 Tagen, sofern sie das Gerät verwenden, AD FS Zugriff auf Ressourcen in mindestens einmal alle 14 Tage.  Wenn sie 15 Tage nach der Bereitstellung von Anmeldeinformationen warten, werden Benutzer erneut zur Eingabe von Anmeldeinformationen aufgefordert werden.  

Beständiges einmaliges Anmelden ist standardmäßig aktiviert. Wenn er deaktiviert ist, wird kein Cookie PSSO geschrieben werden. |  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
Das Gerätefenster Nutzung (standardmäßig 14 Tage) werden, unterliegt die AD FS-Eigenschaft **DeviceUsageWindowInDays**.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
Der maximale einmalige Anmelden Zeitraum (standardmäßig alle 90 Tage) werden, unterliegt die AD FS-Eigenschaft **PersistentSsoLifetimeMins**.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>Bleiben Sie für nicht authentifizierte Geräte angemeldet 
Für nicht registrierte Geräte, die einzelne Punkt anmelden hängt von der **behalten Sie mir signiert In ("angemeldet bleiben")** featureeinstellungen.  "Angemeldet bleiben" ist standardmäßig deaktiviert und kann aktiviert werden, indem Sie die AD FS-Eigenschaft KmsiEnabled auf "true".

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

Mit "angemeldet bleiben" deaktiviert ist der einmalige Anmelden Standardzeitraum 8 Stunden.  Dies kann mithilfe der Eigenschaft SsoLifetime konfiguriert werden.  Die Eigenschaft wird in Minuten gemessen, also der Standardwert 480.  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

Mit "angemeldet bleiben" aktiviert ist der einmalige Anmelden Standardzeitraum für das 24 Stunden.  Dies kann mithilfe der Eigenschaft KmsiLifetimeMins konfiguriert werden.  Die Eigenschaft wird in Minuten gemessen, daher ist der Standardwert 1440.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>Multi-Factor Authentication (MFA)-Verhalten  
Es ist wichtig zu beachten, dass gleichzeitig relativ lange Zeiträume hinweg Einmaliger Anmeldung auf AD FS für die zusätzliche Authentifizierung (Multi-Factor Authentication) fordert bei einer vorherigen Anmeldung basiert auf der primären Anmeldeinformationen und nicht für MFA, aber das aktuelle anmelden erfordert MFA an.  Dies ist unabhängig von SSO-Konfiguration. AD FS, wenn er eine Authentifizierungsanforderung empfängt, zuerst bestimmt, ob es ein SSO-Kontext (z. B. ein Cookie gibt), und klicken Sie dann, wenn MFA erforderlich ist (z. B. wenn die Anforderung stammt außerhalb) bewertet, und zwar unabhängig davon, ob der SSO-Kontext MFA enthält.  Wenn dies nicht der Fall ist, wird MFA aufgefordert.  


  
## <a name="psso-revocation"></a>PSSO Sperrung  
 Um Sicherheit zu schützen, lehnt die AD FS permanentes SSO-Cookie, das zuvor ausgegeben, wenn die folgenden Bedingungen erfüllt sind. Dies erfordert, dass Benutzer ihre Anmeldeinformationen angeben, um die erneute Authentifizierung mit AD FS. 
  
-   Änderung des Kennworts durch Benutzer  
  
-   Persistente SSO-Einstellung ist in AD FS deaktiviert.  
  
-   Gerät wurde vom Administrator bei der verloren gegangenen oder gestohlenen deaktiviert.  
  
-   AD FS empfängt ein permanentes SSO-Cookie für einen registrierten Benutzer jedoch vom Benutzer ausgegeben wird, oder das Gerät ist nicht mehr registriert  
  
-   AD FS empfängt ein permanentes SSO-Cookie für einen registrierten Benutzer, aber der Benutzer erneut registriert.  
  
-   AD FS empfängt ein permanentes SSO-Cookie die als Ergebnis "angemeldet bleiben" jedoch "angemeldet bleiben" ausgegeben wird Einstellung ist in AD FS deaktiviert  
  
-   AD FS empfängt ein persistentes SSO-Cookie für einen registrierten Benutzer ausgegeben wird, aber Gerätezertifikat ist nicht vorhanden oder geändert, während der Authentifizierung  
  
-   AD FS-Administrator verfügt über einen Zeitraum Umstellungsjahr für Angaben mit für beständiges einmaliges Anmelden festgelegt werden. Wenn dies konfiguriert ist, wird AD FS alle permanentes SSO-Cookie ausgegeben, die vor diesem Zeitpunkt ablehnen.  
  
 Führen Sie zum Festlegen der Zeit Umstellungsjahr für Angaben mit das folgende PowerShell-Cmdlet ein:  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Aktivieren Sie PSSO für Office 365-Benutzer den Zugriff auf SharePoint Online  
 Sobald PSSO aktiviert und AD FS konfiguriert, wird AD FS ein permanentes Cookie schreiben, nachdem ein Benutzer authentifiziert wurde. Das nächste Mal, die, das der Benutzer, wird angezeigt, wenn ein dauerhaftes Cookie noch gültig ist, wird, muss ein Benutzer nicht für die Anmeldeinformationen erneut authentifizieren. Sie können auch vermeiden, die zusätzliche authentifizierungsaufforderung für Office 365 und SharePoint Online-Benutzer, indem Sie die folgenden beiden Konfigurieren von Anspruchsregeln in AD FS für die Trigger-Persistenz, bei Microsoft Azure AD und SharePoint Online.  Um PSSO für Office 365-Benutzer auf SharePoint online zugreifen können, müssen Sie zum Installieren dieses [Hotfix](https://support.microsoft.com/en-us/kb/2958298/) ebenfalls Teil der von [August 2014 update-Rollup für Windows RT 8.1, Windows 8.1 und Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/2975719).  
  
 Eine Regel Ausstellung transformieren, um den Anspruch InsideCorporateNetwork durchlaufen  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "http://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
Zusammenfassung:
<table>
  <tr>
    <th colspan="1">Möglichkeit zum einmaligen Anmelden</th>
    <th colspan="3">ADFS 2012 R2 <br> Werden Gerät wird registriert?</th>
        <th colspan="1"></th>
    <th colspan="3">ADFS 2016 <br> Werden Gerät wird registriert?</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>NEIN</th>
    <th>Nein, aber "angemeldet bleiben"</th>
    <th>JA</th>
    <th></th>
    <th>NEIN</th>
    <th>Nein, aber "angemeldet bleiben"</th>
    <th>JA</th>
  </tr>
 <tr align="center">
    <td>SSO = > Festlegen von Aktualisierungstoken = ></td>
    <td>8 Stunden</td>
    <td>Nicht zutreffend</td>
    <td>Nicht zutreffend</td>
    <th></th>
    <td>8 Stunden</td>
    <td>Nicht zutreffend</td>
    <td>Nicht zutreffend</td>
  </tr>

 <tr align="center">
    <td>PSSO = > Festlegen von Aktualisierungstoken = ></td>
    <td>Nicht zutreffend</td>
    <td>24 Stunden</td>
    <td>7 Tage</td>
    <th></th>
    <td>Nicht zutreffend</td>
    <td>24 Stunden</td>
    <td>Maximal 90 Tage mit 14-Tage-Fenster</td>
  </tr>

 <tr align="center">
    <td>Tokengültigkeitsdauer</td>
    <td>1 Std.</td>
    <td>1 Std.</td>
    <td>1 Std.</td>
    <th></th>
    <td>1 Std.</td>
    <td>1 Std.</td>
    <td>1 Std.</td>
  </tr>
</table>

**Registriert Gerät?** Sie erhalten eine PSSO / beständiges einmaliges Anmelden <br>
**Registriert Gerät nicht?** Sie erhalten die SSO-Funktionen <br>
**"Angemeldet bleiben", aber nicht registriertes Gerät?** Sie erhalten eine PSSO / beständiges einmaliges Anmelden <p>
IF:
 - [X]-Administrator hat die Funktion "angemeldet bleiben" [und] aktiviert.
 - [X] Benutzer klickt auf das Kontrollkästchen "angemeldet bleiben" auf der Anmeldeseite von Formularen
 
**Gut zu wissen:** <br>
Verbundbenutzer, die keine der **LastPasswordChangeTimestamp** Attribut synchronisiert werden ausgegeben, Sitzungs-Cookies und Aktualisierungstoken, die eine **Max-Age-Wert von 12 Stunden**.<br>
Dies tritt auf, da Azure AD ermitteln kann, wann Token widerrufen, die an alte Anmeldeinformationen (z. B. ein Kennwort, das geändert wurde) verknüpft sind. Aus diesem Grund muss häufiger Azure AD überprüfen, um sicherzustellen, dass die Benutzer und den zugeordneten Token keine Probleme sind.
