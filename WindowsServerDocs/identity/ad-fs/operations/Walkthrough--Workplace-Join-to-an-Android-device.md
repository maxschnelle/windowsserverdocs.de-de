---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: 'Exemplarische Vorgehensweise: Workplace Join zu einem Android-Gerät'
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a52c5b6e808094e1ef31c800e8a724dd0a37f3d3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816083"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Exemplarische Vorgehensweise: Workplace Join zu einem Android-Gerät



## <a name="join-your-device-with-workplace-join"></a>Hinzufügen Ihres Geräts mit dem Arbeitsplatzbeitritt

> [!NOTE]
> Der Android Workplace Join erfordert Azure Active Directory Device Registration-Dienst. Um Richtlinien für bedingte Geräte lokal zu erzwingen, muss das Verzeichnis Synchronisierungs Tool (Dirsync) mit aktivierter Option für das Zurückschreiben von Geräte Objekten bereitgestellt werden. Zum jetzigen Zeitpunkt kann das Zurückschreiben von Geräten auf Active Directory von Azure Active Directory bis zu drei Stunden dauern. Daher müssen Benutzer nach dem Erstellen eines Geschäfts Kontos 3 Stunden auf lokale Webanwendungen warten. Weitere Informationen zum Bereitstellen Azure Active Directory Device Registration Dienstanbieter finden Sie unter Übersicht über den [Azure Active Directory Device Registration-Dienst](https://msdn.microsoft.com/library/azure/dn788908.aspx) .

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>Erstellen eines Geschäfts Kontos, das Ihr Gerät mit dem Arbeitsplatz Beitritt verknüpft

1.  Sie müssen Azure Authenticator Anwendung auf Ihrem Gerät installieren, um ein Geschäftskonto zu erstellen, mit dem Ihr Gerät mit dem Arbeitsplatz Beitritt verknüpft wird. Die folgende URL enthält Anweisungen zum Installieren der Azure Authenticator-App auf Ihrem Android-Gerät und zum Hinzufügen eines Geschäfts Kontos. Das Geschäftskonto macht Ihr Android-Gerät in ein vertrauenswürdiges Gerät und bietet einmaliges Anmelden (Single Sign-on, SSO) für die Anwendungen auf dem Gerät. Sie können das vertrauenswürdige Gerät verwenden, um auf Webanwendungen und moderne Branchen Anwendungen zuzugreifen, wie Sie vom IT-Administrator empfohlen werden. Weitere Informationen finden Sie unter [Azure Authenticator für Android](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

## <a name="see-also"></a>Weitere Informationen
[Arbeitsplatz Beitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Einrichten des lokalen bedingten Zugriffs mithilfe Azure Active Directory Device Registration Dienstanbieter](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


