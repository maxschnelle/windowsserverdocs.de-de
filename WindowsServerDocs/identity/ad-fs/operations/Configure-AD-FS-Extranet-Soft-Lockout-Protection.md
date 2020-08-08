---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: Konfigurieren des sanften AD FS-Extranetsperrschutzes
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.openlocfilehash: 7a4541ca772576ba100c61130f4698cdcaf95778
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962604"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>Konfigurieren von AD FS extranetsperrschutz

In AD FS auf Windows Server 2012 R2 haben wir ein Sicherheits Feature namens extranetsperre eingeführt.  Mit dieser Funktion wird die Authentifizierung des "böswilligen" Benutzerkontos von außerhalb eines bestimmten Zeitraums beendet AD FS.  Dadurch wird verhindert, dass ihre Benutzerkonten in Active Directory gesperrt werden.  Zusätzlich zum Schutz Ihrer Benutzer vor einer AD-Konto Sperre schützt AD FS extranetsperrungs-Lock auch vor Brute-Force-Angriffen, die Kenn Wörter erraten

> [!NOTE]
> Diese Funktion funktioniert nur für das **Extranetszenario** , bei dem die Authentifizierungsanforderungen über den webanwendungsproxy gesendet werden und nur für die **Benutzernamen-und Kenn Wort Authentifizierung**gelten

## <a name="advantages-of-extranet-lockout"></a>Vorteile der extranetsperre
Die extranetsperre bietet die folgenden wichtigen Vorteile:
- Sie schützt Ihre Benutzerkonten vor **Brute-Force-Angriffen** , bei denen ein Angreifer versucht, das Kennwort eines Benutzers zu erraten, indem er kontinuierlich Authentifizierungsanforderungen sendet. In diesem Fall wird das böswillige Benutzerkonto für den Extranetzugriff von AD FS gesperrt.
- Sie schützt Ihre Benutzerkonten vor **böswilliger Konto** Sperre, bei der ein Angreifer ein Benutzerkonto sperren möchte, indem Authentifizierungsanforderungen mit falschen Kenn Wörtern gesendet werden. In diesem Fall wird das tatsächliche Benutzerkonto in AD nicht gesperrt, und der Benutzer kann weiterhin auf Unternehmensressourcen innerhalb der Organisation zugreifen, obwohl das Benutzerkonto von AD FS für den Extranetzugriff gesperrt wird. Dies wird als **Weiche Sperre**bezeichnet.

## <a name="how-it-works"></a>Funktionsweise
Es gibt drei Einstellungen in AD FS, die Sie konfigurieren müssen, um dieses Feature zu aktivieren:
- **Enableextranetlockout &lt; Boolescher &gt; ** Wert legen Sie diesen booleschen Wert auf "true" fest, wenn Sie die extranetsperre aktivieren möchten.
- **Extranetlockoutthreshold &lt; Ganze &gt; ** Zahl, die die maximale Anzahl fehlerhafter Kenn Wort Versuche definiert. Nachdem der Schwellenwert erreicht wurde, lehnt AD FS die Anforderungen vom Extranet sofort ab, ohne zu versuchen, den Domänen Controller für die Authentifizierung zu kontaktieren, unabhängig davon, ob das Kennwort ein gutes oder ungültiges Kennwort ist. Dies bedeutet, dass sich der Wert des **BadPwdCount** -Attributs eines AD-Kontos nicht erhöht, während das Konto vorläufig gesperrt ist.
- **Extranetobservationwindow &lt; TimeSpan &gt; ** legt fest, wie lange das Benutzerkonto vorläufig gesperrt wird. AD FS beginnt, die Benutzernamen-und Kenn Wort Authentifizierung erneut auszuführen, wenn das Fenster überschritten wird. AD FS verwendet das AD-Attribut badpasswordtime als Referenz, um zu bestimmen, ob das extranetbeobachtsfenster übergeben wurde oder nicht. Das Fenster wurde übergeben, wenn die aktuelle Zeit > badpasswordtime + extranetobservationwindow ist.

> [!NOTE]
> AD FS extranetsperr Funktionen unabhängig von den AD-Sperr Richtlinien. Es wird jedoch dringend empfohlen, den Wert des Parameters **extranetlockoutthreshold** auf einen Wert festzulegen, der kleiner als der Schwellenwert für die AD-Konto Sperre ist. Wenn dies nicht der Fall ist, konnte AD FS die Konten nicht vor der Sperrung in Active Directory geschützt werden.

Ein Beispiel für das Aktivieren der extranetsperrungsfunktion mit maximal 15 Anzahl fehlerhafter Kenn Wort Versuche und einer Dauer von 30 Minuten für die Dauer der vorläufigen Sperrung:

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

Diese Einstellungen gelten für alle Domänen, die der AD FS-Dienst authentifizieren kann. Dies funktioniert, wenn AD FS eine Authentifizierungsanforderung empfängt, über einen LDAP-Befehl auf den primären Domänen Controller (PDC) zugreifen und eine Suche nach dem **BadPwdCount** -Attribut für den Benutzer auf dem PDC durchführen. Wenn AD FS den Wert der **BadPwdCount** ->= extranetlockoutthreshold-Einstellung findet und die im extranetbeobachtsfenster definierte Zeit noch nicht weitergegeben wurde, wird die Anforderung von AD FS sofort abgelehnt. Dies bedeutet unabhängig davon, ob der Benutzer ein gutes oder ungültiges Kennwort aus dem exAD FS tranet eingibt. AD FS behält keinen Zustand in Bezug auf **BadPwdCount** oder gesperrte Benutzerkonten bei. AD FS verwendet AD für die gesamte Zustands Nachverfolgung.

> [!warning]
> Wenn AD FS extranetsperre auf Server 2012 R2 aktiviert ist, werden alle Authentifizierungsanforderungen über den WAP durch AD FS auf dem PDC überprüft. Wenn der PDC nicht verfügbar ist, können sich Benutzer nicht über das Extranet authentifizieren.

Server 2016 bietet einen zusätzlichen Parameter, der AD FS ein Fall Back auf einen anderen Domänen Controller ermöglicht, wenn der PDC nicht verfügbar ist:

- **Extranetlockumquirepdc &lt; Boolescher &gt; ** Wert: bei Aktivierung der extranetsperre ist ein primärer Domänen Controller (PDC) erforderlich. Wenn deaktiviert: die extranetsperre wird auf einen anderen Domänen Controller zurückgreifen, falls der PDC nicht verfügbar ist.

Sie können den folgenden Windows PowerShell-Befehl verwenden, um die AD FS extranetsperre auf Server 2016 zu konfigurieren:

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Arbeiten mit der Active Directory Sperrungs Richtlinie
Das extranetsperrungsfeature in AD FS funktioniert unabhängig von der AD-Sperr Richtlinie. Sie müssen jedoch sicherstellen, dass die Einstellungen für die extranetsperre ordnungsgemäß konfiguriert sind, damit Sie Ihren Sicherheits Zweck mit der AD-Sperr Richtlinie erfüllen kann.
Sehen wir uns zunächst die AD-Sperr Richtlinie an. Es gibt drei Einstellungen für die Sperrungs Richtlinie in AD:
- **Schwellenwert für die Kontosperrung**: Diese Einstellung ähnelt der Einstellung extranetlockoutthreshold in AD FS. Es bestimmt die Anzahl der fehlgeschlagenen Anmeldeversuche, die bewirken, dass ein Benutzerkonto gesperrt wird. Um Ihre Benutzerkonten vor einem Sperrungs Angriff mit böswilligen Konten zu schützen, möchten Sie den Wert von extranetlockoutthreshold in AD FS &lt; den Schwellenwert für die Kontosperrung in AD festlegen.
- **Konto Sperr Dauer**: Diese Einstellung bestimmt, wie lange ein Benutzerkonto gesperrt wird. Diese Einstellung ist in dieser Konversation nicht besonders wichtig, da die extranetsperre vor der ordnungsgemäßen Konfiguration immer erfolgen muss, bevor die AD-Sperre erfolgt.
- **Konto Sperr Zähler zurücksetzen nach**: Diese Einstellung bestimmt, wie lange der letzte Anmeldefehler des Benutzers veralten werden muss, bevor **BadPwdCount** auf 0 zurückgesetzt wird. Damit das extranetsperrungsfeature in AD FS gut mit der AD-Sperrungs Richtlinie funktioniert, müssen Sie sicherstellen, dass der Wert von extranetobservationwindow in AD FS die Zurücksetzungs &gt; Sperre für Konto sperren nach Wert in AD. In den folgenden Beispielen wird erläutert, warum.

Sehen wir uns nun zwei Beispiele an, und Sie sehen, wie **BadPwdCount** sich im Laufe der Zeit auf der Grundlage unterschiedlicher Einstellungen und Zustände ändert. Nehmen wir an, dass in beiden Beispielen **Konto Sperr Schwellenwert** = 4 und **extranetlockoutthreshold** = 2. Der **Rote** Pfeil stellt einen ungültigen Kenn Wort Versuch dar, der **grüne** Pfeil stellt einen guten Kenn Wort Versuch dar. Beispiel #1: **extranetobservationwindow** setzt den Konto Sperrungs &gt; **Zählers nach zurück**. Beispiel #2: **extranetobservationwindow** setzt den Konto Sperrungs &lt; **Zählers nach zurück**.

### <a name="example-1"></a>Beispiel 1
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>Beispiel 2
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

Wie Sie oben sehen können, gibt es zwei Bedingungen, wenn **BadPwdCount** auf 0 zurückgesetzt wird. Eine ist, wenn eine erfolgreiche Anmeldung vorliegt. Der andere Zeitpunkt liegt vor, wenn dieser Leistungswert zurückgesetzt werden soll, wie unter **Zurücksetzen des Konto Sperrungs Zählers nach** der Einstellung definiert. Beim **Zurücksetzen des Konto Sperrungs Zählers nach** &lt; **extranetobservationwindow**besteht kein Risiko, dass das Konto durch AD gesperrt wird. Wenn Sie die **Kontosperrung jedoch nach** &gt; **extranetobservationwindow**zurücksetzen, besteht die Möglichkeit, dass ein Konto durch AD gesperrt wird, aber in einer "verzögerten Art". Abhängig von Ihrer Konfiguration kann es eine Weile dauern, bis ein Konto von AD gesperrt ist, da AD FS während des Überwachungs Fensters nur einen ungültigen Kenn Wort Versuch zulässt, bis **BadPwdCount** den **Schwellenwert für die Kontosperrung**erreicht.

Weitere Informationen finden Sie unter [Konfigurieren der Kontosperrung](/archive/blogs/secguide/configuring-account-lockout).

## <a name="known-issues"></a>Bekannte Probleme
Es gibt ein bekanntes Problem, bei dem das AD-Benutzerkonto nicht mit AD FS authentifiziert werden kann, da das **BadPwdCount** -Attribut nicht auf den Domänen Controller repliziert wird, den ADFS abfragt. Weitere Informationen finden Sie unter [2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc) . [Hier](../deployment/updates-for-active-directory-federation-services-ad-fs.md)finden Sie alle AD FS QFEs, die bisher veröffentlicht wurden.

## <a name="key-points-to-remember"></a>Wichtige Punkte zu merken
- Das extranetsperrungsfeature funktioniert nur für das **Extranetszenario** , bei dem die Authentifizierungsanforderungen über den webanwendungsproxy gesendet werden.
- Die extranetsperrungsfunktion gilt nur für **Benutzername & Kenn Wort Authentifizierung** .
- AD FS behält weder **BadPwdCount** noch Benutzer bei, die vorläufig gesperrt sind. AD FS verwendet AD für die gesamte Zustandsüberwachung.
- AD FS führt für jeden Authentifizierungs Versuch eine Suche nach dem **BadPwdCount** -Attribut durch LDAP-Aufrufe für den Benutzer auf dem PDC aus.
- AD FS älter als 2016 schlägt fehl, wenn der Zugriff auf den PDC nicht möglich ist. In AD FS 2016 wurden Verbesserungen eingeführt, die AD FS für den Fall, dass der PDC nicht verfügbar ist, auf andere Domänen Controller zurückgreifen können.
- Bei der AD FS werden Authentifizierungsanforderungen vom Extranet zugelassen, wenn BadPwdCount < extranetlockoutthreshold
- Wenn **BadPwdCount**  >=  **extranetlockoutthreshold** und **badpasswordtime**  +  **extranetobservationwindow** < aktuelle Zeit, lehnt AD FS Authentifizierungsanforderungen aus dem Extranet ab.
- Um eine böswillige Kontosperrung zu vermeiden, sollten Sie sicherstellen, dass der **extranetlockoutthreshold**  <  -Konto Sperrungs**Schwellenwert** und der **extranetobservationwindow**den  >  **Konto Sperr Wert zurücksetzen** .


## <a name="additional-references"></a>Weitere Verweise
- [Bewährte Methoden zum Sichern von Active Directory-Verbunddienste (AD FS)](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [Delegieren des AD FS-PowerShell-Cmdlet-Zugriffs an Benutzer ohne Administratorrechte](delegate-ad-fs-pshell-access.md)
- [Set-ADF sproperties](/powershell/module/adfs/set-adfsproperties?view=win10-ps)

[AD FS-Vorgänge](../ad-fs-operations.md)


