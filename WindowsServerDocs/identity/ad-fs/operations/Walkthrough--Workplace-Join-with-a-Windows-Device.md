---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: "Exemplarische Vorgehensweise - Arbeitsplatzbeitritt mit einem Windows-Gerät"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fd222eb47982591e051594e8a572443b65c0357f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät

>Gilt für: Windows Server 2016, Windows Server2012 R2

In diesem Thema wird veranschaulicht, wie Arbeitsplatzbeitritt verwenden, um Ihr Windows-Gerät mit Ihrem Arbeitsplatz zu verbinden und wie einmaliges Anmelden mit eine Web-Anwendung zugreifen. Führen Sie die Schritte in der [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) Abschnitt, bevor Sie diese exemplarische Vorgehensweise ausprobieren können.

## <a name="access-the-web-application-before-device-registration"></a>Zugriff auf die Webanwendung vor der geräteregistrierung
In dieser exemplarischen Vorgehensweise wird eine unternehmenswebanwendung zugreifen, bevor Sie Ihr Gerät dem Arbeitsplatz verbinden. Die Webseite zeigt die Ansprüche, die in Ihrem Sicherheitstoken enthalten waren. Beachten Sie, dass die Liste der Ansprüche keine Informationen über Ihr Gerät enthält. Möglicherweise bemerken Sie auch, dass Sie nicht einmaliges Anmelden verfügen.

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>Auf die Anwendung zugreifen, vor der Verwendung von Arbeitsplatzbeitritt auf Ihrem Gerät

1.  Melden Sie sich mit Ihrem Microsoft-Konto auf "client1" an.

2.  Öffnen von Internet Explorer und navigieren Sie zu Ihrer generischen anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

3.  Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: ** roberth@contoso.com **, Kennwort: ** P@ssword **.

4.  Der Webseite werden alle Ansprüche in Ihrem Sicherheitstoken aufgelistet. Es sind nur Benutzeransprüche in Ihrem Sicherheitstoken enthalten.

5.  Schließen Sie InternetExplorer.

6.  Öffnen Sie Internet Explorer und navigieren Sie zu derselben anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

7.  Beachten Sie, dass Sie aufgefordert werden, Ihre Anmeldeinformationen erneut einzugeben. Sie sind nicht mit dem Arbeitsplatz von einem Gerät mit Arbeitsplatzbeitritt verbunden und daher kein einmaliges Anmelden.

## <a name="join-your-device-with-workplace-join"></a>Verbinden Sie Ihr Gerät mit dem Arbeitsplatzbeitritt

> [!IMPORTANT]
> Für den Arbeitsplatzbeitritt erfolgreich ausgeführt werden kann, muss der Clientcomputer (Client1) das SSL-Zertifikat, das verwendet wurde, so konfigurieren Sie Active Directory-Verbunddienste (AD FS) in vertrauen [Schritt2: Configure the Federation Server with Device Registration Service (ADFS1)](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Sie müssen auch Sperrinformationen für das Zertifikat validieren können. Wenn Sie Probleme mit dem Arbeitsplatzbeitritt verbunden haben, können Sie das Ereignisprotokoll auf Client1 anzeigen.
> 
> Um das Ereignisprotokoll anzuzeigen, öffnen Sie die Ereignisanzeige, erweitern Sie **Anwendungs- und Dienstprotokolle**, erweitern Sie **Microsoft**, erweitern Sie **Windows**, und klicken Sie dann auf **Arbeitsplatzbeitritt**.

#### <a name="to-join-your-device-with-workplace-join"></a>Um Ihr Gerät mit dem Arbeitsplatzbeitritt verbinden

1.  Melden Sie sich mit Ihrem Microsoft-Konto auf "client1" an.

2.  Auf der **starten** -Bildschirm, die **Charms** Registerkartenleiste, und wählen Sie dann die **Einstellungen** Charm. Wählen Sie **PC-Einstellungen ändern**.

3.  Auf der **PC-Einstellungen** Seite **Netzwerk**, und klicken Sie dann auf **Arbeitsplatz**.

4.  In der **Geben Sie Ihre Benutzer-ID, um erhalten Zugriff auf den Arbeitsplatz oder Aktivieren der geräteverwaltung** geben ** roberth@contoso.com **, und klicken Sie dann auf **beitreten**.

5.  Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie ** roberth@contoso.com **, und das Kennwort: ** P@ssword **. Klicken Sie auf **OK**.

6.  Jetzt sollte die Meldung angezeigt: "dieses Gerät wurde Ihrem Arbeitsplatznetzwerk hinzugefügt."

### <a name="access-the-web-application-after-joining-the-workplace"></a>Zugriff auf die Webanwendung nach dem arbeitsplatzbeitritt
In diesem Teil der Demo greifen Sie auf eine unternehmenswebanwendung von Ihrem Gerät, das mit dem Arbeitsplatzbeitritt verbunden ist. Die Webseite zeigt die Ansprüche, die in Ihrem Sicherheitstoken enthalten waren. Beachten Sie, dass die Liste der Ansprüche auf Geräte und Benutzer Informationen enthält. Möglicherweise bemerken Sie auch, dass Sie jetzt einmaliges Anmelden.

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>Zugreifen auf die Webanwendung nach dem arbeitsplatzbeitritt

1.  Melden Sie sich **Client1** mit Ihrem Microsoft-Konto.

2.  Öffnen von Internet Explorer und navigieren Sie zu Ihrer generischen anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

3.  Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: ** roberth@contoso.com **, Kennwort: ** P@ssword **.

4.  Der Webseite werden die Ansprüche in Ihrem Sicherheitstoken aufgelistet. Das Token enthält sowohl Benutzer- und Geräteansprüche.

5.  Schließen Sie InternetExplorer.

6.  Öffnen Sie Internet Explorer und navigieren Sie zu derselben anspruchsanwendung **https://webserv1.contoso.com/claimapp**.

7.  Beachten Sie, die Sie **nicht** aufgefordert, Ihre Anmeldeinformationen erneut einzugeben. Sie werden von einem Gerät mit Arbeitsplatzbeitritt verbunden und muss daher einmaliges Anmelden.

## <a name="see-also"></a>Siehe auch
[Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
[Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



