---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: 'Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät'
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 979802469737066612bc6242f942fd3acd077479
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444791"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät


> [!IMPORTANT] 
> Diese Methode gilt für nur vollständig lokalen Kunden zur Verfügung. Hybride oder nur-Cloud-Kunden müssen diese Methode nicht zum Registrieren ihrer iOS-Geräte verwenden. Und diese Methode ist nicht kompatibel, wenn Sie möchten, dass die lokalen Kunden in die cloud verschieben. Das Gerät muss deren Registrierung aufgehoben wird und mit der Cloud registriert. 

In diesem Thema wird der Arbeitsplatzbeitritt mit einem iOS-Gerät dargestellt. Sie müssen die Schritte in der [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) Abschnitt, bevor Sie in dieser exemplarischen Vorgehensweise ausprobieren können. Sie können das Gerät verwenden, auf dem dieselbe unternehmenswebanwendung zuzugreifen, die Sie in der Zugriff auf [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md).


## <a name="join-an-ios-device-with-workplace-join"></a>Hinzufügen eines iOS-Geräts mit dem Arbeitsplatzbeitritt

> [!IMPORTANT]
> Wenn lokales DRS konfiguriert ist, muss das iOS-Gerät das Secure Socket Layer (SSL)-Zertifikat, das verwendet wurde, so konfigurieren Sie Active Directory-Verbunddienste (AD FS) vertrauen, in [Schritt2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4), damit der Arbeitsplatzbeitritt erfolgreich ist.
> 
> -   Wenn das AD FS-SSL-Zertifikat von einer Testzertifizierungsstelle ausgegeben wurde, müssen Sie das Zertifizierungsstellenzertifikat auf Ihrem iOS-Gerät installieren.
> -   Wenn Ihr Zertifizierungsstellenzertifikat auf einer Website veröffentlicht ist, können Sie von Ihrem iOS-Gerät zu der Website navigieren und das Zertifikat installieren.

In dieser Demo fügen Sie das Gerät dem Arbeitsplatz hinzu.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>So fügen Sie ein iOS-Gerät zu einem Arbeitsplatz hinzu

1. -   **Wenn der Dienst Azure Active Directory Device Registration der konfigurierte DRS ist:** Öffnen Sie Apple Safari, und navigieren Sie zu Azure Active Directory Device Registration Service-profilendpunkt für iOS-Geräten <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` >, <`yourdomainname`> ist der Domänenname, den Sie in Azure Active Directory konfiguriert haben. Wenn Ihr Domänenname z. B. "contoso.com" lautet, ist die URL: `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

   -   **Wenn der lokale DRS der konfigurierte DRS ist**: Öffnen Sie Apple Safari, und navigieren Sie zu der profilendpunkt für iOS-Geräte (Device Registration Service, DRS), `https://adf1s.contoso.com/enrollmentserver/otaprofile`

   Es gibt viele Methoden, diese URL Ihren Benutzern mitzuteilen. Ein empfohlenes Verfahren ist das Veröffentlichen dieser URL in einer benutzerdefinierten Meldung vom Typ "Anwendungszugriff verweigert" in AD FS. Dies wird im folgenden Abschnitt behandelt: [Erstellen einer anwendungszugriffsrichtlinie und benutzerdefinierten Nachricht zur verweigerten Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2. Melden Sie sich bei der Website mit einem unternehmensdomänenkonto an: <strong>roberth@contoso.com</strong> und das Kennwort: <strong>P@ssword</strong>.

3. Sie werden aufgefordert, ein Profil zu installieren. Klicken Sie auf dem Bildschirm **Profil installieren** auf **Installieren**.

4. Wenn Sie aufgefordert werden, die Installation des Profils zu bestätigen, klicken Sie auf **Jetzt installieren**.

5. Wenn für das Entsperren Ihres Geräts eine PIN erforderlich ist, werden Sie aufgefordert, Ihre PIN einzugeben.

6. Die Profilinstallation ist abgeschlossen, wenn der Bildschirm **Profil installiert** angezeigt wird. Klicken Sie auf **Fertig**.

   Kehren Sie zu Safari zurück. Sie werden in einer Meldung informiert, dass Sie Safari schließen oder verlassen können.

> [!TIP]
> Navigieren Sie zum Anzeigen oder Entfernen des Profils für den Arbeitsplatzbeitritt zu **Einstellungen**, klicken Sie auf **Allgemein**, und klicken Sie dann auf **Profile** auf Ihrem iOS-Gerät.

## <a name="see-also"></a>Siehe auch


- [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Einrichten der Laborumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



