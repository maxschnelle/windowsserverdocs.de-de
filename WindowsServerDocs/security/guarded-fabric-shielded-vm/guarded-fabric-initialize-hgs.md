---
title: Initialisieren von HGS
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c689a1d5f69731db0cb85a884f5af2ee0230e7be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865451"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>Initialisieren Sie die Host-Überwachungsdienst (Host-Überwachungsdienst)

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie Host-Überwachungsdienst initialisieren, geben Sie den Modus an, dem Host-Überwachungsdienst verwendet werden, um die Integrität der überwachten Hosts messen. Es gibt zwei sich gegenseitig ausschließende Optionen. Hintergrundinformationen zu welchen Modus Sie auswählen, finden Sie unter [geschützten Fabric und abgeschirmte VM Planungshandbuch für Hoster](guarded-fabric-planning-for-hosters.md).

In den folgenden Themen behandeln die Bereitstellungsschritte für jeden Modus:

- [TPM-vertrauenswürdiger Nachweis (TPM-Modus)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [Host-schlüsselnachweis (Schlüssel-Modus)](guarded-fabric-initialize-hgs-key-mode.md)
- [Admin-vertrauenswürdiger Nachweis (Active Directory-Modus)](guarded-fabric-initialize-hgs-ad-mode.md)

Sie sollten diese Schritte auf einem physischen Server ausführen.