---
ms.assetid: ''
title: Insider Preview für Windows-Zeitdienst-Features in Windows Server-2019
description: Neue Windows-Zeitdienst-Features in Windows Server-2019
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: ef0ff317f5957add5ecbe9f88ef83753b805ec41
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829021"
---
# <a name="insider-preview"></a>Insider preview 


## <a name="leap-second-support"></a>Schaltsekunden-Unterstützung


>Gilt für: 2019 für Windows Server und Windows 10, Version 1809

Eine Schaltsekunde ist eine gelegentlich 1-Sekunden-Anpassung in UTC. Wie der Erde Drehung verlangsamt wird, [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (atomic Zeitskala) weicht von [bedeutet, dass ein Sonnen-Zeit](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) oder astronomische Zeit.  Nach der UTC höchstens.9 Sekunden abweichend hat eine [Schaltsekunden](https://en.wikipedia.org/wiki/Leap_second) wird eingefügt, um UTC mit Mean Sonne Zeit zu synchronisieren.

Schaltsekunden geworden wichtig, um die Genauigkeit und die nachverfolgbarkeit gesetzliche Anforderungen in den USA und der Europäischen Union zu erfüllen.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unsere [ankündigungs-Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Überprüfung Anleitung für die [Entwickler](https://aka.ms/Dev-LeapSecond)

-  Überprüfung Anleitung für die [IT Pro](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>Precision-Time-Protokoll

>Gilt für: 2019 für Windows Server und Windows 10, Version 1809

Ein neuer Time-Anbieter, die in Windows Server-2019 und Windows 10 (Version 1809) enthalten, können Sie Zeit, die mit der Genauigkeit Time-Protokoll (PTP) zu synchronisieren. Wie Zeit in einem Netzwerk verteilt, auf Verzögerung (Latenz), die bei nicht berücksichtigt, trifft oder wenn sie nicht symmetrisch ist, wird es zunehmend schwieriger, die vom Time-Server gesendeten Zeitstempel zu verstehen. PTP kann Netzwerkgeräte, um die Wartezeit durch jedes Netzwerkgerät, in der zeitsteuerungsmessungen, wodurch eine viel genauere Time-Beispiel für dem Windows-Client hinzufügen.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unsere [ankündigungs-Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Überprüfung Anleitung für die [IT Pro](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>Software-Zeitstempel

>Gilt für: 2019 für Windows Server und Windows 10, Version 1809

Beim Empfangen eines Pakets für die zeitliche Steuerung über das Netzwerk mit einem Zeitserver muss es vom Netzwerkstapel des Betriebssystems verarbeitet werden, bevor Sie in der Zeitdienst verwendet. Jede Komponente in den Netzwerkstapel führt eine Variable Menge an Wartezeit, die die Genauigkeit der Messung Timing betroffen sind.

![Software-Zeitstempel](../media/Windows-Time-Service/software-timestamping.png)

Um dieses Problem zu beheben, kann Software Zeitstempel wir Zeitstempel Pakete vor und nach der "Windows Networking Components" oben, um die Verzögerung bei der das Betriebssystem zu berücksichtigen.

Weitere Informationen finden Sie in den folgenden Themen:

-  Unsere [ankündigungs-Blog](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  Überprüfung Anleitung für die [IT Pro](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx)



---