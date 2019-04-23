---
title: Aktualisieren Ihrer Remotedesktop-Sitzungshost auf WindowsServer 2016
description: Dieser Artikel beschreibt, wie Sie Ihre vorhandenen Remote Desktop Services-Bereitstellungen auf Windows Server 2016 aktualisieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: 0cf5af29d610ba64d045e10241fd39b01d3f7024
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856061"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>Aktualisieren Ihrer Remotedesktop-Sitzungshost auf WindowsServer 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

> [!IMPORTANT]
> Alle Anwendungen müssen vor dem Upgrade deinstalliert und nach dem Upgrade auf app Kompatibilitätsprobleme zu vermeiden, die aufgrund des Upgrades steigt möglicherweise neu installiert werden.

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützt Upgrades des Betriebssystems mit Remotedesktopdienste-Rolle installiert
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 TP5 unterstützt.

## <a name="upgrading-a-rds-session-based-collection"></a>Upgrade einer RDS-Sitzungen basierende-Auflistung
Um die Ausfallzeit auf ein Minimum zu halten, empfiehlt es sich um die folgenden Schritte, die während des Upgrades von einer sitzungsbasierten RDS-Sammlung unter:

1. Identifizieren Sie die Server aktualisiert werden, z. B. die Hälfte der Server in der Sammlung.
2. Zu verhindern, dass neue Verbindungen mit diesen Servern durch Festlegen von **neue Verbindungen zulassen** auf "false".
3. Melden Sie alle Sitzungen auf diesen Servern. 
4. Entfernen Sie diesen Server aus der Auflistung.
5. Aktualisieren Sie den Server, auf Windows Server 2016.
6. Legen Sie **neue Verbindungen zulassen** auf "false" auf den verbleibenden Servern in der Auflistung.
7. Fügen Sie die aktualisierten Server wieder zur entsprechenden Auflistungen.
8. Entfernen Sie die verbleibende Gruppe von Servern aus der Auflistung aktualisiert werden.
9. Legen Sie **neue Verbindungen zulassen** auf "True", auf den aktualisierten Servern in der Auflistung.
10. Jetzt aktualisieren Sie die verbleibenden Server in der Bereitstellung dazu die folgenden Schritte 3 bis 9 oben.

## <a name="upgrading-a-standalone-rd-session-host-server"></a>Beim Upgrade eines eigenständigen RD-Sitzungshost-Servers
Eine eigenständige RD-Sitzungshostserver kann jederzeit aktualisiert werden.