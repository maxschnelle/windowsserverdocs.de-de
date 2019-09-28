---
title: Initialisieren von HGS
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 07c40b1da829239dda5210dde0dabe485f659ae0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403588"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>Initialisieren des Host-Überwachungs Diensts (HGS)

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie HGS initialisieren, geben Sie den Modus an, der von HGS zum Messen der Integrität der überwachten Hosts verwendet wird. Es gibt zwei Optionen, die sich gegenseitig ausschließen. Hintergrundinformationen zum ausgewählten Modus finden Sie im [Planungs Handbuch für geschützte Fabric und abgeschirmte VMs für Hoster](guarded-fabric-planning-for-hosters.md).

In den folgenden Themen werden die Bereitstellungs Schritte für die einzelnen Modi behandelt:

- [TPM-vertrauenswürdiger Nachweis (TPM-Modus)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [Host Schlüssel Nachweis (Schlüssel Modus)](guarded-fabric-initialize-hgs-key-mode.md)
- [Admin-vertrauenswürdiger Nachweis (AD-Modus)](guarded-fabric-initialize-hgs-ad-mode.md)

Sie sollten diese Schritte auf einem physischen Server ausführen.