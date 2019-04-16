---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: Exemplarische Vorgehensweise - Arbeitsplatzbeitritt mit einem iOS-Gerät
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a8643bab913dfec07c6bbea0c068e1240f16c5b
ms.sourcegitcommit: a2260c96b0e49519d180c7382b921ce8ddb053fe
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät

>Gilt für: Windows Server 2012 R2

In diesem Thema wird Arbeitsplatzbeitritt auf einem iOS-Gerät. Führen Sie die Schritte in der [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) Abschnitt, bevor Sie diese exemplarische Vorgehensweise ausprobieren können. Sie können das Gerät verwenden, auf dieselbe unternehmenswebanwendung zuzugreifen, die Sie besucht [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md).

## <a name="join-an-ios-device-with-workplace-join"></a>Hinzufügen eines iOS-Geräts mit dem Arbeitsplatzbeitritt

> [!IMPORTANT]
> Wenn lokales DRS konfiguriert ist, muss das iOS-Gerät das Secure Socket Layer (SSL)-Zertifikat, das verwendet wurde, so konfigurieren Sie Active Directory-Verbunddienste (AD FS) in vertrauen [Schritt2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4), für den Arbeitsplatzbeitritt erfolgreich ausgeführt werden kann.
> 
> -   Wenn das AD FS-SSL-Zertifikat von einer Test-Zertifizierungsstelle (CA) ausgestellt wurde, müssen Sie das Zertifikat auf Ihrem iOS-Gerät installieren.
> -   Wenn Ihr Zertifizierungsstellenzertifikat auf einer Website veröffentlicht wird, können Sie von Ihrem iOS-Gerät zu der Website navigieren und installieren Sie das Zertifikat.

In dieser Demo fügen Sie das Gerät am Arbeitsplatz.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>Ein iOS-Gerät mit einem Arbeitsplatz beitreten

1.  -   **Bei Azure Active Directory Device Registration Service der konfigurierte DRS ist:** öffnen Apple Safari und navigieren Sie zum Azure Active Directory Device Registration Service-profilendpunkt für iOS-Geräte, <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` >, <`yourdomainname`> der Domänenname, den Sie mit Azure Active Directory konfiguriert haben. Wenn Ihr Domänenname "contoso.com" ist, z. B. ist die URL: `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

    -   **Wenn der lokale DRS der konfigurierte DRS ist**: Öffnen von Apple Safari, und navigieren Sie zu der profilendpunkt für iOS-Geräte (Device Registration Service, DRS)`https://adf1s.contoso.com/enrollmentserver/otaprofile`

    Es gibt viele Möglichkeiten, um diese URL für Ihre Benutzer zu kommunizieren. Eine empfohlene Methode ist, veröffentlichen Sie diese URL in einer benutzerdefinierten Anwendung den Zugriff verweigert Nachricht in AD FS. Dies wird im folgenden Abschnitt behandelt: [Erstellen einer anwendungszugriffsrichtlinie und benutzerdefinierten Zugriff verweigert](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2.  Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: ** roberth@contoso.com ** und das Kennwort: ** P@ssword **.

3.  Sie werden aufgefordert, um ein Profil zu installieren. Auf der **Profil installieren** auf **installieren**.

4.  Wenn Sie dazu aufgefordert werden, um die Installation des Profils zu bestätigen, klicken Sie auf **jetzt installieren**.

5.  Wenn Ihr Gerät eine PIN zum Entsperren des Geräts erforderlich sind, werden Sie aufgefordert, Ihre PIN einzugeben.

6.  Die Profilinstallation ist abgeschlossen, wenn die **Profil installiert** Bildschirm. Klicken Sie auf **Fertig**.

    Kehren Sie zu Safari zurück. Eine Meldung informiert, dass Sie können Safari schließen oder verlassen.

> [!TIP]
> Um anzuzeigen, oder entfernen Sie das Profil Arbeitsplatzbeitritt, navigieren Sie zu **Einstellungen**, klicken Sie auf **allgemeine**, und klicken Sie dann auf **Profile** auf Ihrem iOS-Gerät.

## <a name="see-also"></a>Siehe auch


- [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



