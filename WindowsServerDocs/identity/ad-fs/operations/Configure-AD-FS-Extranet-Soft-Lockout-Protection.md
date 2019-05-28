---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: Konfigurieren von AD FS-Extranetsperrschutz
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6612c05e664b50c5a50b10b712b91715cc85d230
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189880"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>Konfigurieren von AD FS-Extranetsperrschutz

In AD FS unter Windows Server 2012 R2 vorgestellt eine Sicherheitsfunktion, die Extranet-Sperre aufgerufen.  Mit diesem Feature wird AD FS "stop" das Konto "böswilliger" Benutzer von außerhalb für eine bestimmte Zeitspanne authentifizieren.  Dadurch wird verhindert, dass Ihre Benutzerkonten in Active Directory gesperrt wird.  Zusätzlich zum Schutz von Benutzern aus einer AD-kontosperrungen, schützt AD FS extranet Lockout auch für Kennwortermittlung brute-Force-Angriffen

> [!NOTE]
> Dieses Feature funktioniert nur für die **Extranetszenario** bei der Authentifizierung anfordert, über den Webanwendungsproxy stammen und gilt nur für **Benutzernamen-und Kennwortauthentifizierung**.

## <a name="advantages-of-extranet-lockout"></a>Vorteile der Extranetsperre
Extranetsperre bietet folgende wichtige Vorteile:
- Es schützt Ihre Benutzerkonten aus **Brute-force-Angriffe** , in denen ein Angreifer versucht, das Kennwort eines Benutzers zu erraten, indem Sie kontinuierlich Senden von authentifizierungsanforderungen. In diesem Fall wird AD FS böswilliger Benutzerkonto für den Extranetzugriff gesperrt
- Es schützt Ihre Benutzerkonten aus **böswillige kontosperrung** , in dem ein Angreifer möchte Sperren ein Benutzerkonto durch Senden von authentifizierungsanforderungen durch falsche Kennwörter. In diesem Fall wird jedoch das Benutzerkonto, das von AD FS für Extranetzugriff gesperrt sein wird, das tatsächliche Benutzerkonto in AD nicht gesperrt ist und der Benutzer kann weiterhin Unternehmensressourcen innerhalb der Organisation zugreifen. Dies bezeichnet man als ein **vorläufig Sperre**.

## <a name="how-it-works"></a>Funktionsweise
Es gibt 3 Einstellungen in AD FS, die Sie benötigen, so konfigurieren, dass um dieses Feature zu aktivieren: 
- **EnableExtranetLockout &lt;booleschen&gt;**  legen Sie diesen booleschen Wert gleich "true", wenn Sie Extranetsperre aktivieren möchten.
- **ExtranetLockoutThreshold &lt;Ganzzahl&gt;**  definiert die maximale Anzahl der Versuche mit falschem Kennwort. Sobald der Schwellenwert erreicht ist, AD FS wird sofort die Anforderungen abgelehnt über extranet ohne zu versuchen, den Domänencontroller für die Authentifizierung, ganz gleich, wenden Sie sich an, ob das Kennwort gut oder schlecht, bis das extranet Beobachtung Fenster übergeben wird. Dies bedeutet, dass den Wert des **BadPwdCount** Attribut von einem AD-Konto wird nicht erhöht, während das Konto vorläufig gesperrt wurde.
- **ExtranetObservationWindow &lt;TimeSpan&gt;**  Dadurch wird bestimmt, für wie lange der Benutzer Konto Soft-gesperrt werden. AD FS wird gestartet, Benutzername und Kennwort-Authentifizierung erneut durchgeführt, wenn das Fenster übergeben wird. AD FS verwendet BadPasswordTime der AD-Attribut als Verweis, um zu bestimmen, ob das Fenster extranet Beobachtung oder nicht bestanden hat. Das Fenster wurde übergeben, wenn die aktuelle Uhrzeit > BadPasswordTime + ExtranetObservationWindow. 

> [!NOTE]
> AD FS extranet Lockout Funktionen unabhängig von der AD-Kontosperrungsrichtlinien. Allerdings wird dringend empfohlen, Sie legen die **ExtranetLockoutThreshold** Parameterwert ein Wert, der kleiner als der Schwellenwert für AD-kontosperrung ist. Ist dies nicht der Fall würde dazu führen, dass AD FS nicht verhindern, dass Konten in Active Directory gesperrt wird. 

Ein Beispiel für die Aktivierung Extranetsperre-Funktion mit maximal 15 Anzahl der Versuche mit falschem Kennwort und 30 Minuten Soft-Sperrdauer lautet wie folgt aus:

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

Diese Einstellungen gelten für alle Domänen, die der AD FS-Dienst authentifizieren können. Es funktioniert so, ist, wenn AD FS eine Authentifizierungsanforderung empfängt, wird Zugriff auf den primären Domänencontroller (PDC) über einen LDAP-Aufruf und führen Sie eine Suche nach der **BadPwdCount** Attribut für den Benutzer auf dem PDC. Wenn AD FS den Wert der findet **BadPwdCount** > = ExtranetLockoutThreshold-Einstellung und die Zeit, die definiert, im Extranet Beobachtung Fenster nicht überschritten hat noch, AD FS lehnt die Anforderung sofort, d. unabhängig davon, ob h. die Benutzer wird ein gut oder schlecht Kennwort eingibt, über extranet die Anmeldung fehl, da AD FS in AD nicht die Anmeldeinformationen sendet. AD FS behält nicht bei einem beliebigen Zustand in Bezug auf **BadPwdCount** oder Benutzerkonten gesperrt. AD FS verwendet AD für alle Zustände, die nachverfolgung. 

> [!warning]
> Wenn AD FS Extranet Lockout auf Server 2012 R2 aktiviert ist, werden alle authentifizierungsanforderungen über das WAP von AD FS auf dem PDC überprüft. Wenn der primäre Domänencontroller nicht verfügbar ist, werden Benutzer kann nicht aus dem extranet authentifiziert werden.

Server 2016 bietet einen zusätzlichen Parameter, der AD FS für fallback auf einen anderen Domänencontroller ermöglicht, wenn der primäre Domänencontroller nicht verfügbar ist:

- **ExtranetLockoutRequirePDC &lt;booleschen&gt;**  – Wenn aktiviert: extranetsperre erfordert primärer Domänencontroller (PDC). Wenn deaktiviert: extranetsperre erfolgt ein Fallback auf einen anderen Domänencontroller für den Fall, dass der PDC nicht verfügbar ist.

Sie können den folgenden Windows PowerShell-Befehl verwenden, so konfigurieren Sie die AD FS extranet Lockout unter Server 2016:

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Arbeiten mit Active Directory-Kontosperrung Richtlinie
Das Feature "Extranetsperre" in AD FS funktioniert unabhängig von der AD-Sperrrichtlinien. Allerdings müssen Sie sicherstellen, die Einstellungen für das Extranet Lockout ordnungsgemäß konfiguriert ist, damit es zwecks Sicherheit mit der AD-Sperrrichtlinien dienen kann.
Werfen wir einen Blick auf die AD-Sperrrichtlinien erste. Es gibt drei Einstellungen in Bezug auf Sperrrichtlinien in AD:
- **Schwellenwert für Computerkontosperrung Konto**: Diese Einstellung entspricht der Einstellung "ExtranetLockoutThreshold" in AD FS. Bestimmt die Anzahl der fehlgeschlagenen Anmeldeversuche, die bewirkt ein Benutzerkonto gesperrt wird. Um Ihre Benutzerkonten von böswillige Account Lockout Angriffen zu schützen, Sie den Wert der ExtranetLockoutThreshold in AD FS festlegen möchten &lt; der Schwellenwert für Computerkontosperrung-Wert in AD
- **Berücksichtigen Sie die Dauer der Sperrung**: Diese Einstellung legt fest, für wie lange ein Benutzer Konto gesperrt ist. Diese Einstellung spielt keine Rolle viel in dieser Konversation wie Extranetsperre immer geschehen soll, bevor die AD-Sperre erfolgt, wenn ordnungsgemäß konfiguriert
- **Kontosperrungszähler nach zurücksetzen**: Diese Einstellung bestimmt, wie viel Zeit verstreichen muss, vom Benutzer des letzten Fehler bei der Anmeldung vor dem **BadPwdCount** auf 0 zurückgesetzt. Damit für in AD FS Extranet Lockout-Funktion kann auch bei AD-Sperrrichtlinien ordnungsgemäß funktionieren, Sie möchten den Wert der ExtranetObservationWindow in AD FS sicherstellen &gt; der Kontosperrungszähler zurückgesetzt nach Wert in Active Directory. Die folgenden Beispiele werden erläutert, warum.  

Wir betrachten Sie zwei Beispiele für und finden Sie unter wie **BadPwdCount** ändert sich im Laufe der Zeit, die basierend auf unterschiedlichen Einstellungen und Status. Nehmen wir an, in beiden Beispielen **Kontensperrungsschwelle** = 4 und **ExtranetLockoutThreshold** = 2. Die **roten** Pfeil stellt Kennworteingabeversuchen, die **Grün** Pfeil stellt einen guten Kennworteingabe dar. Im Beispiel #1 **ExtranetObservationWindow** &gt; **Kontosperrungszähler zurückgesetzt nach**. Im Beispiel #2 **ExtranetObservationWindow** &lt; **Kontosperrungszähler zurückgesetzt nach**. 

### <a name="example-1"></a>Beispiel 1
![Beispiel 1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>Beispiel 2
![Beispiel 1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

Wie Sie oben sehen können, es gibt zwei Bedingungen, wenn **BadPwdCount** wird auf 0 zurückgesetzt. Eines ist, wenn eine erfolgreiche Anmeldung vorhanden ist. Die andere ist, wenn es darum, diese Zähler zurückgesetzt wird, gemäß **Kontosperrungszähler zurückgesetzt nach** festlegen. Wenn **Kontosperrungszähler zurückgesetzt nach** &lt; **ExtranetObservationWindow**, ein Konto verfügt nicht über alle in Bezug auf, die Sie von AD gesperrt werden. Aber wenn **Kontosperrungszähler zurückgesetzt nach** &gt; **ExtranetObservationWindow**, besteht die Möglichkeit, die ein Konto von AD jedoch in "verzögert Weise" gesperrt werden kann. Es dauert eine Weile erhalten Sie ein Konto gesperrt, durch AD abhängig von Ihrer Konfiguration wie AD FS nur ein Kennworteingabeversuchen während des Zeitfensters für die Beobachtung erst zugelassen wird **BadPwdCount** erreicht **Schwellenwert für Computerkontosperrung** .

Weitere Informationen finden Sie unter [Kontosperrung konfigurieren](https://blogs.technet.microsoft.com/secguide/2014/08/13/configuring-account-lockout/). 

## <a name="known-issues"></a>Bekannte Probleme
Es ist ein bekanntes Problem, der AD-Benutzerkonto mit AD FS authentifizieren kann, da, die **BadPwdCount** Attribut wird nicht repliziert, an den Domänencontroller, die AD FS abgefragt wird. Finden Sie unter [2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc) Weitere Details. Sie finden alle AD FS QFEs, die bisher veröffentlicht wurden [hier](../deployment/updates-for-active-directory-federation-services-ad-fs.md).

## <a name="key-points-to-remember"></a>Wichtige Punkte beachtet
- Die Extranetsperre-Funktion funktioniert nur für die **Extranetszenario** kommen die authentifizierungsanforderungen über den Webanwendungsproxy
- Die Extranetsperre-Funktion gilt nur für **Benutzernamen und das Kennwort-Authentifizierung**
- AD FS hält keine verfolgen **BadPwdCount** oder Benutzer, die Sie vorläufig gesperrt sind. AD FS verwendet AD für alle Zustände, die nachverfolgung
- AD FS führt eine Suche nach der **BadPwdCount** über LDAP-Aufruf für den Benutzer auf dem PDC bei jedem Authentifizierungsversuch Attribut  
- AD FS, die älter als 2016 schlägt fehl, wenn es sich bei den PDC nicht darauf zugreifen können. AD FS 2016 eingeführten Verbesserungen, die ermöglichen, dass AD FS Fallback auf andere Domänencontroller, bei dem PDC nicht verfügbar ist. 
- AD FS können authentifizierungsanforderungen aus dem extranet bei BadPwdCount < ExtranetLockoutThreshold 
- Wenn **BadPwdCount** >= **ExtranetLockoutThreshold** und **BadPasswordTime** + **ExtranetObservationWindow** < Aktuelle Uhrzeit in AD FS lehnt authentifizierungsanforderungen aus dem extranet
- Um böswillige kontosperrungen zu vermeiden, stellen Sie sicher **ExtranetLockoutThreshold** < **Kontensperrungsschwelle** und **ExtranetObservationWindow**  >  **Kontosperrungszähler zurücksetzen**


## <a name="additional-references"></a>Weitere Verweise  
- [Bewährte Methoden zum Schützen von Active Directory Federation Services](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [Delegieren des AD FS-PowerShell-Cmdlet-Zugriffs an Benutzer ohne Administratorrechte](delegate-ad-fs-pshell-access.md)
- [Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)

    
