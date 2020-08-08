---
title: Migrieren des AD FS 2,0-Verbund Proxyservers
description: Bietet Informationen zum Migrieren eines AD FS Proxy Servers zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: a8345f587e7fe4119e46dc390e9240dee6071ce6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940833"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Migrieren des Active Directory-Verbunddienste (AD FS) Proxy Servers zu Windows Server 2012 R2

In Active Directory-Verbunddienste (AD FS) (AD FS) in Windows Server 2012 R2 wird die Rolle eines Verbund Server Proxys von einem neuen Remote Zugriffs Rollen Dienst namens webanwendungsproxy behandelt. Wenn Sie in Windows Server 2012 R2 ihren AD FS für die Barrierefreiheit von außerhalb des Unternehmensnetzwerks aktivieren möchten, können Sie einen oder mehrere webanwendungsproxys bereitstellen. Es ist jedoch nicht möglich, einen Verbund Server Proxy unter Windows Server 2008 R2 oder Windows Server 2012 zu einem webanwendungsproxy zu migrieren, der unter Windows Server 2012 R2 ausgeführt wird.

> [!IMPORTANT]
>  Die Migration eines Verbund Server Proxys unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 zu einem webanwendungsproxy, der unter Windows Server 2012 R2 ausgeführt wird, wird nicht unterstützt.

Wenn Sie AD FS in einer migrierten Windows Server 2012 R2-Farm für den Extranetzugriff konfigurieren möchten, müssen Sie eine neue Bereitstellung von einem oder mehreren webanwendungsproxy-Computern als Teil Ihrer AD FS-Infrastruktur ausführen.

Wenn Sie die Bereitstellung eines Webanwendungsproxys planen, lesen Sie die Informationen in den folgenden Themen:

- [Planen der Infrastruktur für den Webanwendungsproxy](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))

- [Planen des Webanwendungsproxy-Servers](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))

  Sie können zum Bereitstellen eines Webanwendungsproxys die Schritte in den folgenden Themen ausführen:

- [Konfigurieren der Infrastruktur für den Webanwendungsproxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))

- [Installieren und Konfigurieren des Webanwendungsproxy-Servers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))

## <a name="next-steps"></a>Nächste Schritte
 [Migrieren Active Directory-Verbunddienste (AD FS) Rollen Dienste zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md) [Vorbereiten der Migration des AD FS Verbund Servers migrieren](prepare-migrate-ad-fs-server-r2.md) [des AD FS Verbund Servers migrieren](migrate-ad-fs-fed-server-r2.md) der [AD FS Migration zu Windows Server 2012 R2](verify-ad-fs-migration.md)
