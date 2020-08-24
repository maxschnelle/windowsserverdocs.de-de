---
title: Insider Preview für Windows-Zeitdienstfunktionen in Windows Server 2019
description: Neue Windows-Zeitdienstfunktionen in Windows Server 2019
author: dahavey
ms.author: dahavey
ms.date: 06/06/2020
ms.topic: article
ms.openlocfilehash: 01968fe51d25f394e346cebc8dbeafd2dd17ca4a
ms.sourcegitcommit: b5b040a47cf48c94852de9aad8b91475f891d2f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563370"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="leap-second-support"></a>Unterstützung für Schaltsekunden

> Gilt für: Windows Server 2019 und Windows 10, Version 1809

Eine Schaltsekunde ist eine gelegentliche Anpassung der UTC um 1 Sekunde. Wenn sich die Erdrotation verlangsamt, weicht die [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (eine Atomzeitskala) von der [mittleren Sonnenzeit](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) oder der astronomischen Zeit ab. Sobald die UTC um maximal 0,9 Sekunden abweicht, wird eine [Schaltsekunde](https://en.wikipedia.org/wiki/Leap_second) eingefügt, um die UTC mit der mittleren Sonnenzeit synchron zu halten.

Schaltsekunden sind ein wichtiges Mittel geworden, um die gesetzlichen Anforderungen an Genauigkeit und Nachverfolgbarkeit sowohl in den USA als auch in der Europäischen Union zu erfüllen.

Weitere Informationen finden Sie unter:

- Unser [Ankündigungsblog](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- Validierungshandbuch für [Entwickler](https://aka.ms/Dev-LeapSecond)

- Validierungshandbuch für [IT-Experten](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>Präzisionszeitprotokoll (PTP)

> Gilt für: Windows Server 2019 und Windows 10, Version 1809

Ein neuer Zeitanbieter, der in Windows Server 2019 und Windows 10 (Version 1809) enthalten ist, ermöglicht es dir, die Zeit mithilfe des Präzisionszeitprotokolls (Precision Time Protocol, PTP) zu synchronisieren. Während die Zeit über ein Netzwerk verteilt wird, kommt es zu Verzögerungen (Latenzen), durch die es, wenn sie unberücksichtigt bleiben oder asymmetrisch sind, zunehmend schwierig wird, den vom Zeitserver gesendeten Zeitstempel zu verstehen. Mit PTP können Netzwerkgeräte die Latenz, die von jedem Netzwerkgerät eingeführt wird, zu jeder Zeitmessung addieren, wodurch dem Windows-Client eine weitaus genauere Zeitstichprobe bereitgestellt wird.

Weitere Informationen finden Sie unter:

- Unser [Ankündigungsblog](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- Validierungshandbuch für [IT-Experten](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>Software-Zeitstempelung

> Gilt für: Windows Server 2019 und Windows 10, Version 1809

Beim Empfang eines Zeitsteuerungspakets über das Netzwerk von einem Zeitserver muss es vom Netzwerkstapel des Betriebssystems verarbeitet werden, bevor es im Zeitdienst verwendet werden kann. Jede Komponente im Netzwerkstapel führt eine variable Menge an Latenz ein, die sich auf die Genauigkeit der Zeitmessung auswirkt.

![Software-Zeitstempelung](../media/Windows-Time-Service/software-timestamping.png)

Um dieses Problem zu beheben, gestattet die Software-Zeitstempelung die Vergabe eines Zeitstempels für Pakete vor und nach den oben gezeigten „Windows-Netzwerkkomponenten“, um die Verzögerung im Betriebssystem zu berücksichtigen.

Weitere Informationen finden Sie unter:

- Unser [Ankündigungsblog](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [Validierungsleitfäden für Entwickler und IT-Experten](https://github.com/microsoft/W32Time/tree/master/Leap%20Seconds)


---
