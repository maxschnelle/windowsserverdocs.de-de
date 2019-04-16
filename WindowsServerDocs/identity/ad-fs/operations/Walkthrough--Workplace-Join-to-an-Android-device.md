---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: "Exemplarische Vorgehensweise - Arbeitsplatzbeitritt auf einem Android-Gerät"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cfe26947b6b0de28ea50367f82d52815fff8f323
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Android-Gerät

>Gilt für: Windows Server 2016, Windows Server2012 R2


## <a name="join-your-device-with-workplace-join"></a>Verbinden Sie Ihr Gerät mit dem Arbeitsplatzbeitritt

> [!NOTE]
> Android arbeitsplatzbeitritt erfordert Azure Active Directory Device Registration Service. Um bedingte Gerät Richtlinien lokalen zu erzwingen, muss das Verzeichnissynchronisierungstool (DirSync) Gerät Objekt Write-Back-Option aktiviert bereitgestellt werden. Zeitpunkt vorhanden kann Geräte Zurückschreiben in Active Directory von Azure Active Directory bis zu 3 Stunden dauern. Daher müssen Benutzer drei Stunden auf lokalen Web-Apps nach dem Erstellen eines Geschäftskontos warten. Weitere Informationen zum Bereitstellen von Azure Active Directory Device Registration service, finden Sie unter [Azure Active Directory Device Registration Service Overview](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>Erstellen Sie ein Geschäftskonto, der das Gerät mit einem Arbeitsplatz beitreten hinzugefügt wird.

1.  Sie müssen zum Installieren von Azure Authenticator-Anwendung auf Ihrem Gerät ein Geschäftskonto zu erstellen, die Ihr Gerät mit arbeitsplatzbeitritt hinzugefügt wird. Die folgende URL hat Anweisungen zum Installieren von Azure Authenticator-app auf Ihr Android-Gerät und ein Geschäftskonto hinzufügen. Das Geschäftskonto können Ihr Android-Gerät zu einem vertrauenswürdigen Gerät und einmaliges Anmelden (SSO) auf die Anwendungen auf Gerät enthält. Sie können das vertrauenswürdige Gerät Access-Webanwendungen und moderne Line-of-Business-Anwendungen verwenden, wie von Ihrem IT-Administrator empfohlen. Weitere Informationen finden Sie unter [Azure Authenticator für Android](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

## <a name="see-also"></a>Siehe auch
[Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[lokalen bedingten Zugriff mithilfe von Azure Active Directory Device Registration Service einrichten](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


