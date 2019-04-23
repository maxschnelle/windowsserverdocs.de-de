---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: 'Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fd222eb47982591e051594e8a572443b65c0357f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864001"
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In diesem Thema wird gezeigt, wie Sie den Arbeitsplatzbeitritt verwenden, um Ihr Windows-Gerät mit Ihrem Arbeitsplatz zu verbinden. Sie erfahren außerdem, wie Sie über das einmalige Anmelden auf eine Webanwendung zugreifen. Sie müssen die Schritte in der [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) Abschnitt, bevor Sie in dieser exemplarischen Vorgehensweise ausprobieren können.

## <a name="access-the-web-application-before-device-registration"></a>Zugriff auf die Webanwendung vor der Geräteregistrierung
In dieser exemplarischen Vorgehensweise greifen Sie auf eine Unternehmenswebanwendung zu, bevor Sie Ihr Gerät mit dem Arbeitsplatz verbinden. Auf der Webseite werden die Ansprüche angezeigt, die in Ihrem Sicherheitstoken enthalten sind. Beachten Sie, dass die Liste der Ansprüche keine Informationen zu Ihrem Gerät enthält. Möglicherweise beobachten Sie auch, dass Ihnen kein anmaliges Anmelden zur Verfügung steht.

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>So greifen Sie auf die Webanwendung zu, bevor Sie den Arbeitsplatzbeitritt auf Ihrem Gerät verwenden

1.  Melden Sie sich mit Ihrem Microsoft-Konto bei Client1 an.

2.  Öffnen Sie Internet Explorer und navigieren zu Ihrer generischen anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

3.  Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: **roberth@contoso.com**, Kennwort: **P@ssword**.

4.  Auf der Webseite werden alle Ansprüche in Ihrem Sicherheitstoken aufgelistet. In Ihrem Sicherheitstoken sind nur Benutzeransprüche vorhanden.

5.  Schließen Sie Internet Explorer.

6.  Öffnen Sie Internet Explorer, und navigieren Sie zu derselben anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

7.  Beachten Sie, dass Sie aufgefordert werden, Ihre Anmeldeinformationen erneut einzugeben. Sie werden nicht mit dem Arbeitsplatz von einem Gerät mit dem Arbeitsplatzbeitritt verbunden und verfügen deshalb nicht über ein einmaliges Anmelden.

## <a name="join-your-device-with-workplace-join"></a>Hinzufügen Ihres Geräts mit dem Arbeitsplatzbeitritt

> [!IMPORTANT]
> Damit der Arbeitsplatzbeitritt erfolgreich ist, muss der Clientcomputer (Client1) das SSL-Zertifikat, das zum Konfigurieren von Active Directory-Verbunddienste (AD FS) verwendet wurde im vertrauen [Schritt2: Konfigurieren des Verbundservers mit dem Geräteregistrierungsdienst (ADFS1)](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Darüber hinaus muss er die Sperrinformationen für das Zertifikat validieren können. Falls beim Arbeitsplatzbeitritt Probleme auftreten, können Sie das Ereignisprotokoll auf %%amp;quot;Client1%%amp;quot; anzeigen.
> 
> Öffnen Sie zum Anzeigen des Protokolls die Ereignisanzeige, erweitern Sie **Anwendungs- und Dienstprotokolle**, **Microsoft**und **Windows**, und klicken Sie dann auf **Arbeitsplatzbeitritt**.

#### <a name="to-join-your-device-with-workplace-join"></a>So fügen Sie Ihr Gerät mit dem Arbeitsplatzbeitritt hinzu

1.  Melden Sie sich mit Ihrem Microsoft-Konto bei Client1 an.

2.  Öffnen Sie auf dem Bildschirm **Start** die **Charmleiste** , und wählen Sie dann den Charm **Einstellungen** aus. Wählen Sie **PC-Einstellungen ändern** aus.

3.  Wählen Sie auf der Seite **PC-Einstellungen** die Option **Netzwerk**aus, und klicken Sie dann auf **Arbeitsplatz**.

4.  In der **Geben Sie Ihre Benutzer-ID zum Zugriff auf den Arbeitsplatz zu erhalten oder die geräteverwaltung aktivieren** geben **roberth@contoso.com**, und klicken Sie dann auf **Join**.

5.  Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie **roberth@contoso.com**, und das Kennwort: **P@ssword**. Klicken Sie auf **OK**.

6.  Jetzt sollte die Meldung „Dieses Gerät wurde Ihrem Arbeitsplatznetzwerk hinzugefügt.“ angezeigt werden.

### <a name="access-the-web-application-after-joining-the-workplace"></a>Zugriff auf die Webanwendung nach dem Arbeitsplatzbeitritt
In diesem Teil der Demo greifen Sie von Ihrem Gerät, das mit dem Arbeitsblattbeitritt verbunden ist, auf diene Unternehmenswebanwendung zu. Auf der Webseite werden die Ansprüche angezeigt, die in Ihrem Sicherheitstoken enthalten sind. Beachten Sie, dass die Liste der Ansprüch sowohl Geräte- als auch Benutzerinformationen enthält. Möglicherweise bemerken Sie auch, dass Ihnen jetzt das einmalige Anmelden zur Verfügung steht.

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>So greifen Sie nach dem Arbeitsplatzbeitritt auf die Webanwendung zu

1.  Melden Sie sich mit Ihrem Microsoft-Konto bei **Client1** an.

2.  Öffnen Sie Internet Explorer und navigieren zu Ihrer generischen anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

3.  Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: **roberth@contoso.com**, Kennwort: **P@ssword**.

4.  Auf der Webseite werden die Ansprüche in Ihrem Sicherheitstoken aufgelistet. Das Token enthält sowohl Benutzer- als auch Geräteansprüche.

5.  Schließen Sie Internet Explorer.

6.  Öffnen Sie Internet Explorer, und navigieren Sie zu derselben anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

7.  Beachten Sie, dass Sie **nicht** aufgefordert werden, Ihre Anmeldeinformationen erneut einzugeben. Sie sind von einem Gerät mit Arbeitsplatzbeitritt verbunden und verfügen deshalb über das einmalige Anmelden.

## <a name="see-also"></a>Siehe auch
[Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 
 [ Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



