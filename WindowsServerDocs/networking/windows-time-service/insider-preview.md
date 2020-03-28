---
ms.assetid: ''
title: Insider Preview für Windows-Zeitdienstfunktionen in Windows Server 2019
description: Neue Windows-Zeitdienstfunktionen in Windows Server 2019
author: eross-msft
ms.author: lizross
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 3c61b1ca7a11e01d2d8234cb505998946a774691
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315014"
---
# <a name="insider-preview"></a>Insider Preview 


## <a name="leap-second-support"></a>Unterstützung für Schaltsekunden


>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Eine Schaltsekunde ist eine gelegentliche Anpassung der UTC um 1 Sekunde. Wenn sich die Erdrotation verlangsamt, weicht die [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (eine Atomzeitskala) von der [mittleren Sonnenzeit](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) oder der astronomischen Zeit ab.  Sobald die UTC um maximal 0,9 Sekunden abweicht, wird eine [Schaltsekunde](https://en.wikipedia.org/wiki/Leap_second) eingefügt, um die UTC mit der mittleren Sonnenzeit synchron zu halten.

Schaltsekunden sind ein wichtiges Mittel geworden, um die gesetzlichen Anforderungen an Genauigkeit und Nachverfolgbarkeit sowohl in den USA als auch in der Europäischen Union zu erfüllen.

Weitere Informationen finden Sie unter:

-  Unser [Ankündigungsblog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungshandbuch für [Entwickler](https://aka.ms/Dev-LeapSecond)

-  Validierungshandbuch für [IT-Experten](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>Präzisionszeitprotokoll (PTP)

>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Ein neuer Zeitanbieter, der in Windows Server 2019 und Windows 10 (Version 1809) enthalten ist, ermöglicht es dir, die Zeit mithilfe des Präzisionszeitprotokolls (Precision Time Protocol, PTP) zu synchronisieren. Während die Zeit über ein Netzwerk verteilt wird, kommt es zu Verzögerungen (Latenzen), durch die es, wenn sie unberücksichtigt bleiben oder asymmetrisch sind, zunehmend schwierig wird, den vom Zeitserver gesendeten Zeitstempel zu verstehen. Mit PTP können Netzwerkgeräte die Latenz, die von jedem Netzwerkgerät eingeführt wird, zu jeder Zeitmessung addieren, wodurch dem Windows-Client eine weitaus genauere Zeitstichprobe bereitgestellt wird.

Weitere Informationen finden Sie unter:

-  Unser [Ankündigungsblog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungshandbuch für [IT-Experten](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>Software-Zeitstempelung

>Gilt für: Windows Server 2019 und Windows 10, Version 1809

Beim Empfang eines Zeitsteuerungspakets über das Netzwerk von einem Zeitserver muss es vom Netzwerkstapel des Betriebssystems verarbeitet werden, bevor es im Zeitdienst verwendet werden kann. Jede Komponente im Netzwerkstapel führt eine variable Menge an Latenz ein, die sich auf die Genauigkeit der Zeitmessung auswirkt.

![Software-Zeitstempelung](../media/Windows-Time-Service/software-timestamping.png)

Um dieses Problem zu beheben, gestattet die Software-Zeitstempelung die Vergabe eines Zeitstempels für Pakete vor und nach den oben gezeigten „Windows-Netzwerkkomponenten“, um die Verzögerung im Betriebssystem zu berücksichtigen.

Weitere Informationen finden Sie unter:

-  Unser [Ankündigungsblog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Validierungshandbuch für [IT-Experten](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx)



---