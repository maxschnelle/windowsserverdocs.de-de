---
title: Initialisieren von HGS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: e36451c90fd543ea49989e51832ab3104d4137c0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939591"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>Initialisieren des Host-Überwachungs Diensts (HGS)

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie HGS initialisieren, geben Sie den Modus an, der von HGS zum Messen der Integrität der überwachten Hosts verwendet wird. Es gibt zwei Optionen, die sich gegenseitig ausschließen. Hintergrundinformationen zum ausgewählten Modus finden Sie im [Planungs Handbuch für geschützte Fabric und abgeschirmte VMs für Hoster](guarded-fabric-planning-for-hosters.md).

In den folgenden Themen werden die Bereitstellungs Schritte für die einzelnen Modi behandelt:

- [TPM-vertrauenswürdiger Nachweis (TPM-Modus)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [Host Schlüssel Nachweis (Schlüssel Modus)](guarded-fabric-initialize-hgs-key-mode.md)
- [Admin-vertrauenswürdiger Nachweis (AD-Modus)](guarded-fabric-initialize-hgs-ad-mode.md)

Sie sollten diese Schritte auf einem physischen Server ausführen.