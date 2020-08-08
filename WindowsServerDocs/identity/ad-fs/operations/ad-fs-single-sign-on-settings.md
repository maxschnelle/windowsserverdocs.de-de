---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: 'AD FS 2016: Einstellungen für einmaliges Anmelden'
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.openlocfilehash: 5d558717e3baa2f849636f4a8f347ce327cb787c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966937"
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS Einstellungen für einmaliges Anmelden

Einmaliges Anmelden (Single Sign-on, SSO) ermöglicht Benutzern das einmalige authentifizieren und den Zugriff auf mehrere Ressourcen, ohne zur Eingabe zusätzlicher Anmelde Informationen aufgefordert zu werden.  In diesem Artikel wird das standardmäßige AD FS Verhalten für SSO sowie die Konfigurationseinstellungen beschrieben, mit denen Sie dieses Verhalten anpassen können.

## <a name="supported-types-of-single-sign-on"></a>Unterstützte Arten von einmaligem Anmelden

AD FS unterstützt verschiedene Arten von einmaligem Anmelden:

-   **Sitzungs-SSO**

     Sitzungs-SSO-Cookies werden für den authentifizierten Benutzer geschrieben, wodurch weitere Aufforderungen beseitigt werden, wenn der Benutzer während einer bestimmten Sitzung Anwendungen wechselt. Wenn jedoch eine bestimmte Sitzung beendet wird, wird der Benutzer erneut zur Eingabe seiner Anmelde Informationen aufgefordert.

     AD FS werden standardmäßig Sitzungs-SSO-Cookies festlegen, wenn die Benutzer Geräte nicht registriert sind. Wenn die Browsersitzung beendet wurde und neu gestartet wird, wird dieses Sitzungs Cookie gelöscht und ist nicht mehr gültig.

-   **Persistentes SSO**

     Persistente SSO-Cookies werden für den authentifizierten Benutzer geschrieben, wodurch weitere Aufforderungen beseitigt werden, wenn der Benutzer Anwendungen so lange umschaltet, wie das persistente SSO-Cookie gültig ist. Der Unterschied zwischen permanentem SSO und SSO für die Sitzung besteht darin, dass persistentes SSO über verschiedene Sitzungen hinweg verwaltet werden kann.

     Wenn das Gerät registriert ist, werden AD FS persistente SSO-Cookies festlegen. AD FS wird auch ein dauerhaftes SSO-Cookie festgelegt, wenn ein Benutzer die Option "angemeldet bleiben" auswählt. Wenn das persistente SSO-Cookie nicht mehr gültig ist, wird es zurückgewiesen und gelöscht.

-   **Anwendungsspezifisches SSO**

     Im OAuth-Szenario wird ein Aktualisierungs Token verwendet, um den SSO-Status des Benutzers innerhalb des Gültigkeits Bereichs einer bestimmten Anwendung beizubehalten.

     Wenn ein Gerät registriert ist, legt AD FS die Ablaufzeit eines Aktualisierungs Tokens basierend auf der Dauer der dauerhaften SSO-Cookies für ein registriertes Gerät fest, das standardmäßig 7 Tage für AD FS 2012r2 und maximal 90 Tage mit AD FS 2016 ist, wenn Sie über Ihr Gerät auf AD FS Ressourcen innerhalb eines 14-tägigen Fensters zugreifen.

Wenn das Gerät nicht registriert ist, aber ein Benutzer die Option "angemeldet bleiben" auswählt, entspricht die Ablaufzeit des Aktualisierungs Tokens der dauerhaften SSO-Cookies-Gültigkeitsdauer für "angemeldet bleiben". die Standardeinstellung ist 1 Tag und der Höchstwert 7 Tage. Andernfalls entspricht die Gültigkeitsdauer des Aktualisierungs Tokens dem Sitzungs-SSO-Cookie, das standardmäßig 8 Stunden beträgt

 Wie bereits erwähnt, erhalten Benutzer auf registrierten Geräten immer ein dauerhaftes SSO, es sei denn, das permanente einmalige Anmelden ist deaktiviert. Bei nicht registrierten Geräten kann das permanente einmalige Anmelden erreicht werden, indem die Funktion "angemeldet bleiben" aktiviert wird.

 Für Windows Server 2012 R2 müssen Sie diesen Hotfix installieren, um PSSO für das Szenario "angemeldet bleiben" zu aktivieren. dieser [Hotfix](https://support.microsoft.com/kb/2958298/) ist auch Bestandteil des Updaterollup vom [August 2014 für Windows RT 8,1, Windows 8.1 und Windows Server 2012 R2](https://support.microsoft.com/kb/2975719).

Aufgabe | PowerShell | BESCHREIBUNG
------------ | ------------- | -------------
Persistentes SSO aktivieren/deaktivieren | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| Persistentes SSO ist standardmäßig aktiviert. Wenn Sie deaktiviert ist, wird kein PSSO-Cookie geschrieben.
"Aktivieren/deaktivieren" "angemeldet bleiben" | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | Die Funktion "angemeldet bleiben" ist standardmäßig deaktiviert. Wenn Sie aktiviert ist, wird dem Endbenutzer auf AD FS Anmeldeseite die Option "angemeldet bleiben" angezeigt.



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016: einmaliges Anmelden und authentifizierte Geräte
AD FS 2016 ändert das PSSO, wenn der Anforderer von einem registrierten Gerät authentifiziert wird, das auf max. 90 Tage ansteigt, aber eine Authentifizierung innerhalb eines Zeitraums von 14 Tagen (Fenster "Geräte Verwendung") erfordert.
Nachdem Sie die Anmelde Informationen zum ersten Mal eingegeben haben, erhalten Benutzer mit registrierten Geräten standardmäßig einmaliges Anmelden für einen maximalen Zeitraum von 90 Tagen, vorausgesetzt, Sie verwenden das Gerät, um mindestens alle 14 Tage auf AD FS Ressourcen zuzugreifen.  Wenn Sie nach der Angabe von Anmelde Informationen 15 Tage warten, werden die Benutzer erneut zur Eingabe von Anmelde Informationen aufgefordert.

Persistentes SSO ist standardmäßig aktiviert. Wenn Sie deaktiviert ist, wird kein PSSO-Cookie geschrieben. |

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```

Das Fenster "Geräte Verwendung" (standardmäßig 14 Tage) wird von der AD FS-Eigenschaft " **deviceusagewindowindays**" gesteuert.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```
Der maximale Zeitraum für einmaliges Anmelden (standardmäßig 90 Tage) wird durch die AD FS-Eigenschaft **persistentssolifetimemins**geregelt.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>Angemeldet bleiben für nicht authentifizierte Geräte
Bei nicht registrierten Geräten wird der Single Sign-on Zeitraum durch die Funktion " **angemeldet bleiben" (kmsi)** festgelegt.  Kmsi ist standardmäßig deaktiviert und kann aktiviert werden, indem Sie die AD FS-Eigenschaft "kmsiaktivierte" auf "true" festlegen.

``` powershell
Set-AdfsProperties -EnableKmsi $true
```

Bei deaktiviertem kmsi beträgt der Standard Single Sign-on Zeitraum 8 Stunden.  Dies kann mithilfe der ssolifetime-Eigenschaft konfiguriert werden.  Die-Eigenschaft wird in Minuten gemessen, d. h., der Standardwert ist 480.

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\>
```

Bei aktiviertem kmsi beträgt der Standard Single Sign-on Zeitraum 24 Stunden.  Dies kann mithilfe der Eigenschaft "kmsilifetimemins" konfiguriert werden.  Die-Eigenschaft wird in Minuten gemessen, d. h., der Standardwert ist 1440.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\>
```

## <a name="multi-factor-authentication-mfa-behavior"></a>Multi-Factor Authentication (MFA)-Verhalten
Es ist wichtig zu beachten, dass bei der Bereitstellung relativ langer Zeiträume für das einmalige Anmelden AD FS eine zusätzliche Authentifizierung (Multi-Factor Authentication) angefordert wird, wenn ein vorheriger Anmeldevorgang auf primären Anmelde Informationen basiert und nicht auf MFA, aber für die aktuelle Anmeldung ist MFA erforderlich.  Dies ist unabhängig von der SSO-Konfiguration. Wenn AD FS eine Authentifizierungsanforderung empfängt, bestimmt zuerst, ob ein SSO-Kontext (z. b. ein Cookie) vorhanden ist. wenn MFA erforderlich ist (z. b., wenn die Anforderung von außerhalb eingeht), wird überprüft, ob der SSO-Kontext MFA enthält.  Wenn dies nicht der Wert ist, wird MFA aufgefordert.



## <a name="psso-revocation"></a>PSSO-Sperrung
 Um die Sicherheit zu schützen, lehnt AD FS alle permanenten SSO-Cookies ab, die zuvor ausgegeben wurden, wenn die folgenden Bedingungen erfüllt sind. Dies erfordert, dass der Benutzer seine Anmelde Informationen bereitstellt, um sich erneut bei AD FS zu authentifizieren.

- Änderung des Kennworts durch den Benutzer

- Die Einstellung für persistentes SSO ist in AD FS deaktiviert.

- Das Gerät wurde vom Administrator im verlorenen oder gestohlenen Fall deaktiviert.

- AD FS empfängt ein dauerhaftes SSO-Cookie, das für einen registrierten Benutzer ausgestellt wird, der Benutzer oder das Gerät aber nicht mehr registriert ist.

- AD FS empfängt ein dauerhaftes SSO-Cookie für einen registrierten Benutzer, aber der Benutzer registriert sich erneut.

- AD FS empfängt ein dauerhaftes SSO-Cookie, das als Ergebnis der Einstellung "angemeldet bleiben" ausgegeben wird, aber "angemeldet bleiben" in AD FS

- AD FS empfängt ein dauerhaftes SSO-Cookie, das für einen registrierten Benutzer ausgestellt wird, das Gerätezertifikat aber während der Authentifizierung fehlt oder geändert wird.

- AD FS Administrator hat eine Umstellungszeit für persistentes SSO festgelegt. Wenn dies konfiguriert ist, lehnt AD FS alle vor diesem Zeitpunkt ausgestellten permanenten SSO-Cookies ab.

  Führen Sie das folgende PowerShell-Cmdlet aus, um die Umstellungszeit festzulegen:


``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```

## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Aktivieren von PSSO für Office 365-Benutzer für den Zugriff auf SharePoint Online
 Nachdem PSSO in AD FS aktiviert und konfiguriert wurde, wird AD FS ein dauerhaftes Cookie schreiben, nachdem ein Benutzer authentifiziert wurde. Wenn der Benutzer das nächste Mal kommt und ein dauerhaftes Cookie noch gültig ist, muss ein Benutzer keine Anmelde Informationen zur erneuten Authentifizierung angeben. Sie können auch die zusätzliche Authentifizierungs Aufforderung für Office 365-und SharePoint Online-Benutzer vermeiden, indem Sie die folgenden beiden Anspruchs Regeln in AD FS konfigurieren, um die Persistenz bei Microsoft Azure AD und SharePoint Online zu auslösen.  Um PSSO für Office 365-Benutzer für den Zugriff auf SharePoint Online zu aktivieren, müssen Sie diesen [Hotfix](https://support.microsoft.com/kb/2958298/) installieren, der auch Bestandteil des Updaterollup vom [August 2014 für Windows RT 8,1, Windows 8.1 und Windows Server 2012 R2](https://support.microsoft.com/kb/2975719)ist.

 Eine Ausstellungs Transformations Regel zum Durchlaufen des insiencorporatenetwork-Anspruchs.

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

Zusammenfassung:
<table>
  <tr>
    <th colspan="1">Einmaliges Anmelden</th>
    <th colspan="3">AD FS 2012 R2 <br> Ist das Gerät registriert?</th>
        <th colspan="1"></th>
    <th colspan="3">AD FS 2016 <br> Ist das Gerät registriert?</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>Nein</th>
    <th>Nein, aber kmsi</th>
    <th>YES</th>
    <th></th>
    <th>Nein</th>
    <th>Nein, aber kmsi</th>
    <th>YES</th>
  </tr>
 <tr align="center">
    <td>SSO = &gt; Aktualisierungs Token festlegen =&gt;</td>
    <td>8 Std.</td>
    <td>Nicht zutreffend</td>
    <td>Nicht zutreffend</td>
    <th></th>
    <td>8 Std.</td>
    <td>Nicht zutreffend</td>
    <td>Nicht zutreffend</td>
  </tr>

 <tr align="center">
    <td>PSSO = &gt; Aktualisierungs Token festlegen =&gt;</td>
    <td>Nicht zutreffend</td>
    <td>24 Stunden</td>
    <td>7 Tage</td>
    <th></th>
    <td>Nicht zutreffend</td>
    <td>24 Stunden</td>
    <td>Max. 90 Tage mit 14 Tagen (Fenster)</td>
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

**Registriertes Gerät?** Sie erhalten das einmalige Anmelden (PSSO/persistent). <br>
**Nicht registriertes Gerät?** Sie erhalten ein SSO <br>
**Nicht registriertes Gerät, aber kmsi?** Sie erhalten das einmalige Anmelden (PSSO/persistent). <p>
Sei
 - [x] Administrator hat die kmsi-Funktion aktiviert [und]
 - [x] Benutzer klickt auf der Formular Anmeldeseite auf das Kontrollkästchen "kmsi".

  
ADFS gibt nur dann ein neues Aktualisierungs Token aus, wenn die Gültigkeit des neueren Aktualisierungs Tokens länger ist als das vorherige Token. Die maximale Lebensdauer eines Tokens beträgt 84 Tage, AD FS jedoch das Token in einem 14-tägigen gleitenden Fenster gültig hält. Wenn das Aktualisierungs Token 8 Stunden lang gültig ist (d. h. die reguläre SSO-Zeit), wird kein neues Aktualisierungs Token ausgegeben.
 

**Gut zu wissen:** <br>
Verbund Benutzer, die das Attribut " **lastpasswordchangetimestamp** " nicht synchronisiert haben, werden Sitzungs Cookies und Aktualisierungs Token mit einem **maximalen Alters Wert von 12 Stunden**ausgegeben.<br>
Dies liegt daran, dass Azure AD nicht bestimmen kann, wann Token im Zusammenhang mit alten Anmelde Informationen (z. b. ein Kennwort, das geändert wurde) widerrufen werden muss. Daher müssen Azure AD häufiger überprüfen, um sicherzustellen, dass sich der Benutzer und die zugehörigen Token weiterhin in einem guten Zustand befinden.
