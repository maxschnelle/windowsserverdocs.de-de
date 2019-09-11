---
ms.assetid: ''
title: Insider Preview für Windows-Zeit Dienst Features in Windows Server 2019
description: Neue Windows-Zeit Dienst Features in Windows Server 2019
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: a0c4d01d095e8052a2192d6b6352732a6fe60919
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871793"
---
# <a name="insider-preview"></a>Insider preview 


## <a name="leap-second-support"></a>Unterstützung für Schaltsekunden


>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Eine Schaltsekunde ist eine Anpassung von 1 Sekunde auf UTC. Wenn die Drehung der Erde verlangsamt wird, weicht [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (eine atomarische Zeitspanne) von der [durchschnittlichen Sonnenzeit](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) oder der astronomischen Zeit ab.  Wenn die UTC höchstens 0,9 Sekunden voneinander abweigelte, wird eine [Schaltsekunde](https://en.wikipedia.org/wiki/Leap_second) eingefügt, um die UTC-Zeit mit der durchschnittlichen Sonnenzeit synchron zu halten.

Schaltsekunden sind wichtig, um die gesetzlichen Anforderungen an Genauigkeit und Nachverfolgbarkeit sowohl in der USA als auch in der Europäischen Union zu erfüllen.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unseren [Ankündigungs Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungs Handbuch für [Entwickler](https://aka.ms/Dev-LeapSecond)

-  Validierungs Handbuch für [IT](https://aka.ms/ITPro-LeapSecond) -Experten


## <a name="precision-time-protocol"></a>Genauigkeits Zeitprotokoll

>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Ein neuer Zeit Anbieter, der in Windows Server 2019 und Windows 10 (Version 1809) enthalten ist, ermöglicht es Ihnen, die Zeit mithilfe des Zeit Protokolls (Precision Time Protocol, PTP) zu synchronisieren. Wenn die Zeit über ein Netzwerk verteilt wird, wird eine Verzögerung (Wartezeit) festgestellt. wenn diese nicht berücksichtigt wird oder wenn Sie nicht symmetrisch ist, wird es zunehmend schwieriger, den vom Zeitserver gesendeten Zeitstempel zu verstehen. Mit PTP können Netzwerkgeräte die Wartezeit, die von jedem Netzwerkgerät eingeführt wurde, den Zeit Steuerungs Messungen hinzufügen. Dadurch wird dem Windows-Client ein weitaus genaueres Zeit Beispiel bereitgestellt.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unseren [Ankündigungs Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungs Handbuch für [IT](https://aka.ms/PTPValidation) -Experten


## <a name="software-timestamping"></a>Software Zeitstempel

>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Beim Empfang eines Zeit Steuerungs Pakets über das Netzwerk von einem Zeitserver aus muss es vom Netzwerk Stapel des Betriebssystems verarbeitet werden, bevor er im Zeit Dienst verwendet werden kann. Jede Komponente im Netzwerk Stapel führt eine Variable Menge an Latenz ein, die sich auf die Genauigkeit der zeitlichen Steuerung auswirkt.

![Software Zeitstempel](../media/Windows-Time-Service/software-timestamping.png)

Um dieses Problem zu beheben, können wir mit dem Software Zeitstempel vor und nach den oben gezeigten "Windows-Netzwerkkomponenten" Zeitstempel für die Verzögerung des Betriebssystems berücksichtigen.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unseren [Ankündigungs Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungs Handbuch für [IT](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx) -Experten



---