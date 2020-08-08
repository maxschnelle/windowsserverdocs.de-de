---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: Vorbereiten von Clientcomputern des Kontopartners
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b78c3d3b4c5562acfcc7b2657f6e49119fc491e2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967597"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>Vorbereiten von Clientcomputern des Kontopartners

Die einfachste Möglichkeit für einen Administrator in einer Konto Partnerorganisation, Client Computer für den Zugriff auf Active Directory-Verbunddienste (AD FS) \( AD FS \) Verbund Anwendungen vorzubereiten, ist die Verwendung von Gruppenrichtlinie. Gruppenrichtlinien bieten eine bequeme Möglichkeit, bestimmte Zertifikate und Einstellungen auf alle für den Verbund erforderlichen Clientcomputer auszubringen, die für den Zugriff auf Verbundanwendungen verwendet werden.

Damit Ihre Client Computer nahtlos auf Verbund Anwendungen zugreifen können, ohne dass Zertifikat Aufforderungen oder vertrauenswürdige Website – entsprechende Eingabe Aufforderungen angezeigt werden, empfiehlt es sich, zuerst jeden Client Computer vorzubereiten, bevor Sie AD FS in Ihrer Organisation umfassend bereitstellen. Gruppenrichtlinien können zur Automatisierung folgender Aufgaben verwendet werden:

-   Konfigurieren Sie Internet Explorer auf jedem Client Computer, um dem Konto Verbund Server zu vertrauen.

    Weitere Informationen finden Sie unter [Configure Client Computers to Trust the Account Federation Server](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md).

-   Installieren Sie den entsprechenden Konto Verbund Server, den Ressourcen Verbund Server und den Webserver Secure Sockets Layer \( SSL- \) Zertifikate \( oder entsprechende Zertifikate, die mit einem vertrauenswürdigen Stamm \) auf jedem Client Computer verkettet sind.

    Weitere Informationen finden Sie unter [Verteilen von Zertifikaten an Client Computer mithilfe Gruppenrichtlinie](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md).


## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
