---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: "AD FS 2016 für einmaliges Anmelden Einstellungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e8c24399949efc1b8d0b1782e299593c02374c62
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS Single Sign-On Einstellungen

>Gilt für: Windows Server 2016, Windows Server2012 R2

Einmaliges Anmelden (SSO) können Benutzer sich einmal authentifizieren und Zugriff auf mehrere Ressourcen ohne weitere Anmeldeinformationen aufgefordert werden.  Dieser Artikel beschreibt das Standardverhalten von AD FS für SSO-als auch die Konfigurationseinstellungen, die Sie dieses Verhalten anpassen können.  

## <a name="supported-types-of-single-sign-on"></a>Unterstützte Arten des einmaligen Anmeldens

AD FS unterstützt verschiedene Arten von SSO-Funktionen:  
  
-   **Sitzung SSO**  
  
     SSO Sitzungscookies sind für den authentifizierten Benutzer geschrieben, die weiteren Anweisungen beseitigt, wenn der Benutzer während einer bestimmten Sitzung Anwendungen wechselt. Jedoch eine bestimmte Sitzung endet, wird der Benutzer zur Eingabe ihrer Anmeldeinformationen erneut aufgefordert.  
  
     AD FS wird Sitzung SSO Cookies standardmäßig festgelegt, wenn den Geräten der Benutzer nicht registriert sind. Wenn die Browsersitzung beendet wurde und neu gestartet wird, wird diese Sitzungscookie gelöscht, und ist nicht mehr gültig.  
  
-   **Ein beständiges einmaliges Anmelden**  
  
     Beständige Cookies von SSO sind für den authentifizierten Benutzer geschrieben, die Anweisungen weiter beseitigt, wenn der Benutzer Anwendungen für wechselt, solange das persistente SSO-Cookie ungültig ist. Der Unterschied zwischen permanente SSO und die Sitzung SSO ist, dass ein beständiges einmaliges Anmelden unterschiedliche sitzungsübergreifend beibehalten werden kann.  
  
     AD FS wird beständige Cookies von SSO festgelegt, wenn das Gerät registriert ist. AD FS wird auch ein permanente SSO-Cookie festgelegt, wenn ein Benutzer die Option "angemeldet bleiben" auswählt. Wenn das persistente SSO-Cookie mehr nicht gültig ist, wird zurückgewiesen und gelöscht werden.  
  
-   **Anwendung bestimmte SSO**  
  
     Im OAuth-Szenario wird ein Aktualisierungstoken verwendet, um den SSO-Status des Benutzers innerhalb des Bereichs einer bestimmten Anwendung beizubehalten.  
  
     Wenn ein Gerät registriert ist, wird AD FS die Ablaufzeit für ein Aktualisierungstoken basierend auf der dauerhafte SSO Cookies-Lebensdauer für ein registriertes Gerät, das 7Tage ist standardmäßig festgelegt. Wenn ein Benutzer die Option "angemeldet bleiben" auswählt, ist die Ablaufzeit für das Aktualisierungstoken die permanente Cookies SSO-Lebensdauer "beibehalten, die ich angemeldet" gleich 1.Tag werden standardmäßig mit bis zu 7Tage ist. Andernfalls refresh Token Lebensdauer Equals SSO-Cookie Sitzungsdauer handelt es sich standardmäßig acht Stunden  
  
 Wie bereits erwähnt, erhalten Benutzer auf registrierte Geräte immer ein beständiges einmaliges Anmelden, es sei denn, der ein beständige einmaliges Anmelden deaktiviert ist. Für nicht registrierten Geräte kann ein beständiges einmaliges Anmelden aktivieren "bleiben mich angemeldet" erreicht werden (KMSI)-Funktion. 
 
 Für Windows Server2012 R2 PSSO für das Szenario "Angemeldet bleiben" aktivieren Sie diese installieren müssen [Hotfix](https://support.microsoft.com/en-us/kb/2958298/) auch Teil der von [August 2014 Updaterollup für Windows RT 8.1, Windows8.1 und Windows Server2012 R2](https://support.microsoft.com/en-us/kb/2975719).   
 
  
## <a name="single-sign-on-and-authenticated-devices"></a>Einmaliges Anmelden und authentifizierten Geräte  
Nach dem Bereitstellen von Anmeldeinformationen zum ersten Mal, erhalten standardmäßig Benutzer mit registrierten Geräten einmaliges Anmelden für einen Zeitraum von 90Tagen, sofern sie das Gerät verwenden, um sich mindestens einmal alle 14Tage auf AD FS-Ressourcen zugreifen.  Wenn sie 15Tage nach der Bereitstellung von Anmeldeinformationen warten, werden Benutzer erneut zur Eingabe von Anmeldeinformationen aufgefordert.  

Ein beständiges einmaliges Anmelden ist standardmäßig aktiviert. Wenn es deaktiviert ist, wird kein Cookie PSSO geschrieben werden. |  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
Die Verwendung Gerätefenster (standardmäßig alle 14Tage) unterliegt der AD FS-Eigenschaft **DeviceUsageWindowInDays**.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
Die einzelne anmelden Höchstdauer (standardmäßig alle 90Tage) unterliegt der AD FS-Eigenschaft **PersistentSsoLifetimeMins**.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>Bleiben Sie für nicht authentifizierte Geräte angemeldet 
Für nicht registrierte Geräte, die einzelne anmelden Punkt wird anhand der **beibehalten, die ich im (KMSI) protokolliert** Feature Einstellungen.  KMSI ist standardmäßig deaktiviert und kann aktiviert werden, indem Sie die AD FS-Eigenschaft KmsiEnabled auf True.

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

Mit KMSI deaktiviert ist der einzige anmelden Standardzeitraum 8 Stunden.  Dies kann mithilfe der Eigenschaft SsoLifetime konfiguriert werden.  Die Eigenschaft wird in Minuten gemessen, also der Standardwert 480.  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

Mit KMSI aktiviert ist der einzige anmelden Standardzeitraum 24 Stunden.  Dies kann mithilfe der Eigenschaft KmsiLifetimeMins konfiguriert werden.  Die Eigenschaft wird in Minuten gemessen, also der Standardwert 1440.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>Verhalten von Multi-Factor Authentication (MFA)  
Es ist wichtig, beachten Sie, dass während Bereitstellung relativ längere Zeiträume für einmaliges Anmelden, wird AD FS für die zusätzliche Authentifizierung (Multi-Factor Authentication) aufgefordert Wenn eine Anmeldung bei der vorherigen basiert auf primären Anmeldeinformationen und nicht MFA, aber die aktuelle Anmeldung MFA erforderlich ist.  Dies ist unabhängig von SSO-Konfiguration. AD FS, wenn er eine Authentifizierungsanforderung erhält, zuerst bestimmt, ob ein SSO-Kontext (z.B. ein Cookie) vorhanden ist und klicken Sie dann, wenn MFA erforderlich ist (z.B. wenn die Anforderung kommt von außerhalb) wird sie bewerten, ob die SSO-Kontext MFA enthält oder nicht.  Wenn dies nicht der Fall ist, wird MFA aufgefordert.  


  
## <a name="psso-revocation"></a>PSSO Sperrung  
 Um die Sicherheit zu schützen, lehnt die AD FS alle permanente SSO-Cookie, das zuvor ausgegeben, wenn die folgenden Bedingungen erfüllt sind. Dies erfordert, dass den Benutzer, ihre Anmeldeinformationen einzugeben, um mit AD FS erneut authentifizieren. 
  
-   Kennwort des Benutzers geändert wird  
  
-   Permanente SSO-Einstellung ist in AD FS deaktiviert.  
  
-   Gerät wird vom Administrator im Fall von verloren gegangenen oder gestohlenen deaktiviert.  
  
-   AD FS empfängt ein permanente SSO-Cookie für registrierte Benutzer jedoch dem Benutzer ausgestellt wird, oder das Gerät ist nicht mehr registriert  
  
-   AD FS empfängt ein permanente SSO-Cookie für einen registrierten Benutzer, aber der Benutzer erneut registriert  
  
-   AD FS empfängt ein permanente SSO-Cookie als Ergebnis "angemeldet bleiben" aber "angemeldet bleiben" ausgestellt ist in AD FS ist deaktiviert  
  
-   AD FS empfängt ein permanente SSO-Cookie für einen registrierten Benutzer ausgestellt wird aber Gerätezertifikat fehlt oder geänderte während der Authentifizierung  
  
-   AD FS-Administrator festgelegt eine Stichtagsdatum Zeit für ein beständiges einmaliges Anmelden. Wenn dies konfiguriert ist, wird AD FS permanenten SSO-Cookie ausgestellt vor diesem Zeitpunkt ablehnen.  
  
 Führen Sie das folgende PowerShell-Cmdlet, um das Abschneiden eines einstellen:  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Aktivieren Sie PSSO für Office365-Benutzer auf SharePoint Online zugreifen.  
 Sobald PSSO aktiviert und in AD FS konfiguriert ist, wird AD FS persistente Cookies schreiben, nachdem ein Benutzer authentifiziert hat. Beim nächsten Start des Benutzers, kommt, wenn ein dauerhaftes Cookie weiterhin gültig ist, muss ein Benutzer nicht für die Anmeldeinformationen erneut authentifizieren. Sie können auch vermeiden, die Aufforderung für Office365 und SharePoint Online-Benutzer durch die Konfiguration die folgenden zwei Anspruchsregeln in AD FS to Trigger Persistenz bei Microsoft Azure AD und SharePoint Online.  Um PSSO für SharePoint online Zugriff auf Office365-Benutzer zu aktivieren, müssen Sie diese installieren [Hotfix](https://support.microsoft.com/en-us/kb/2958298/) auch Teil der von [August 2014 Updaterollup für Windows RT 8.1, Windows8.1 und Windows Server2012 R2](https://support.microsoft.com/en-us/kb/2975719).  
  
 Eine Regel Ausstellung transformieren, um den Anspruch InsideCorporateNetwork passieren  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "https://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
  
    


