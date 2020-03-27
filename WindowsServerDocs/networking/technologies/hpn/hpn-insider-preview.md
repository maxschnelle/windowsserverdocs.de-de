---
ms.assetid: ''
title: Insider Preview für HPN-Features in Windows Server 2019
description: Erfahren Sie mehr über die neuen hochleistungsfähigen Netzwerk Features in Windows Server 2019.
manager: dougkim
author: eross-msft
ms.author: lizross
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 03a652372fd86b11a87863330bf9536a28367167
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316954"
---
# <a name="new-hpn-features-in-windows-server-2019"></a>Neue HPN-Features in Windows Server 2019


## <a name="dynamic-vrss-and-vmmq"></a>Dynamisches vrss und vmmq

>Gilt für: Windows Server 2019

In der Vergangenheit konnten virtuelle Computer Warteschlangen und multiwarteschlangen für virtuelle Computer einen deutlich höheren Durchsatz für einzelne VMS erzielen, da die Netzwerk Durchgängen zunächst die 10-GbE-Markierung und darüber hinaus erreicht haben. Leider wurde die Planung, das Baselining, die Optimierung und die Überwachung für den Erfolg zu einem großen Unternehmen. häufig sind mehr als der IT-Administrator für die Ausgaben vorgesehen. 

Windows Server 2019 verbessert diese Optimierungen durch dynamisches verteilen und Optimieren der Verarbeitung von Netzwerk Arbeits Auslastungen nach Bedarf. Windows Server 2019 sorgt für eine optimale Effizienz und entfernt die Konfigurations Belastung für IT-Administratoren.

Weitere Informationen finden Sie unter:

-   [Ankündigungs Blog](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [Validierungs Handbuch für IT-Experten](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>Empfangen von Segmentkoaleszenz (RSC) im vSwitch

>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Die Empfangs Segment Zusammenfügung (RSC) im Vswitch ist eine Erweiterung, bei der mehrere TCP-Segmente vor dem Durchlaufen des vSwitches in ein größeres Segment zusammengebracht werden. Das große Segment verbessert die Netzwerkleistung für virtuelle Arbeits Auslastungen.

Zuvor war dies eine von der NIC implementierte Auslagerung. Leider ist dies der Zeitpunkt, an dem Sie den Adapter an einen virtuellen Switch angefügt haben, deaktiviert. RSC im Vswitch unter Windows Server 2019 und Windows 10 Oktober 2018 Update entfernt diese Einschränkung.

Standardmäßig ist RSC im Vswitch auf externen virtuellen Switches aktiviert.

Weitere Informationen finden Sie unter:

-  [Ankündigungs Blog](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [Validierungs Handbuch für IT-Experten](https://aka.ms/RSC-Validation)
