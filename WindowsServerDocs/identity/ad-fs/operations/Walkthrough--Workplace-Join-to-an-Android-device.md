---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: 'Exemplarische Vorgehensweise: Arbeitsplatzbeitritt auf einem Android-Gerät'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73dbe4d62d460f9487467c7d4198d62b3b6af539
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188932"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt auf einem Android-Gerät



## <a name="join-your-device-with-workplace-join"></a>Hinzufügen Ihres Geräts mit dem Arbeitsplatzbeitritt

> [!NOTE]
> Android arbeitsplatzbeitritt erfordert Azure Active Directory Device Registration Service. Um die bedingten Richtlinien für ein lokales zu erzwingen, muss die Tool für die Verzeichnissynchronisierung (DirSync) Gerät Objekt kennwortrückschreiben-Feature-Option aktiviert bereitgestellt werden. Momentan ist kann gerätezurückschreibung in Active Directory von Azure Active Directory bis zu drei Stunden dauern. Daher müssen Benutzer drei Stunden auf lokale Webanwendungen zugreifen, nach dem Erstellen eines Geschäftskontos warten. Weitere Informationen zum Bereitstellen von Azure Active Directory Device Registration service, finden Sie unter, [Azure Active Directory Device Registration Service Overview](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>Erstellen Sie ein Geschäftskonto, die Ihr Gerät bei Workplace Join verknüpft.

1.  Sie benötigen, installieren Azure Authenticator-App auf Ihrem Gerät um ein Geschäftskonto zu erstellen, der Ihr Gerät mit arbeitsplatzbeitritt verbunden. Die folgende URL umfasst Anweisungen zum Installieren der Azure Authenticator-app auf Ihrem Android-Gerät und Hinzufügen eines Geschäftskontos. Das Geschäftskonto können Ihr Android-Gerät in einem vertrauenswürdigen Gerät und bietet einmaliges Anmelden (SSO) für die Anwendungen auf dem Gerät. Gemäß Empfehlung von Ihrem IT-Administrator, können Sie das vertrauenswürdige Gerät Access-Webanwendungen und moderne Branchen-Anwendungen. Weitere Informationen finden Sie unter [Azure Authenticator für Android](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

## <a name="see-also"></a>Siehe auch
[Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Einrichten des lokalen bedingten Zugriffs, die mithilfe der Azure Active Directory Device Registration Service](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


