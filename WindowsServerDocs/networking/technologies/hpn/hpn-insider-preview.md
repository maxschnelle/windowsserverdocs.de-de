---
ms.assetid: ''
title: Insider Preview für HPN-Features in Windows Server-2019
description: Erfahren Sie, bis die neuen Hochleistungs-Netzwerkfunktionen in Windows Server-2019.
manager: dougkim
author: shortpatti
ms.author: pashort
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 3d3e974472f28c30d093fbd1094ef3693d984d19
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886271"
---
# <a name="insider-preview"></a>Insider-Vorschau


## <a name="dynamic-vrss-and-vmmq"></a>Dynamische vRSS und VMMQ

>Gilt für: Windows Server 2019

In der Vergangenheit aktiviert Virtual Machine und VM mit mehreren Warteschlangen auf einzelnen virtuellen Computern viel höheren Durchsatz als Netzwerk-Durchsatz, die zuerst erreicht die 10-GbE-Markierung und darüber hinaus. Die Planung, basislinienüberwachung mit zwei erforderlich leider Anpassung und Überwachung für Erfolg eine große Unternehmen geworden ist. häufig sollen mehr als der IT-Administrator verbringen. 

Windows Server-2019 verbessert diese Optimierungen durch dynamisch verteilen und Optimierung der Verarbeitung von Netzwerk-Workloads nach Bedarf. Windows Server-2019 ständig höchste Effizienz sicherstellt und den Aufwand für die Konfiguration für IT-Administratoren entfernt.

Weitere Informationen finden Sie in den folgenden Themen:

-   [Ankündigungs-blog](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [Überprüfungshandbuchs für IT-Experten](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>Empfangen von Segmentkoaleszenz (RSC) im vSwitch

>Gilt für: 2019 für Windows Server und Windows 10, Version 1809

Empfangen von Segment Coalescing (RSC) in der vSwitch ist eine Erweiterung, die mehrere TCP-Segmente in einem größeren Segment vor Daten durchlaufen die vSwitch Koaliert. Das große Segment verbessert die netzwerkleistung für virtuelle auslastungen.

Früher war dies eine Auslagerung durch die NIC implementiert Leider wurde dies dem Moment deaktiviert, bis, den Sie den Adapter mit einem virtuellen Switch angefügt. RSC in vSwitches unter Windows Server-2019 und Windows 10 Oktober 2018 Update entfernt diese Einschränkung.

Standardmäßig ist die RSC in die vSwitch auf externen virtuellen Switches aktiviert.

Weitere Informationen finden Sie in den folgenden Themen:

-  [Ankündigungs-blog](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [Überprüfungshandbuchs für IT-Experten](https://aka.ms/RSC-Validation)
