---
title: DirectAccess-Kapazitätsplanung
description: Sie können dieses Thema für einen Bericht über die DirectAccess-Serverleistung von Windows Server 2012 verwenden, um Sie bei der Kapazitätsplanung für DirectAccess in Windows Server 2016 zu unterstützen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 456e5971-3aa7-4a24-bc5d-0c21fec7687e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 413dc88ce9ec551a318b63f3df44ed256f289219
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815793"
---
# <a name="directaccess-capacity-planning"></a>DirectAccess-Kapazitätsplanung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Dokument ist ein Bericht zur DirectAccess-Serverleistung von Windows Server 2012. Anhand von Tests wurde die Durchsatzkapazität für Highend-Computerhardware und Lowend-Computerhardware ermittelt. Die CPU-Leistung der Highend- und Lowend-Hardware war vom Durchsatz an Netzwerkdatenverkehr und den Arten der verwendeten Clients abhängig. Eine typische DirectAccess-Bereitstellung (die Grundlage für diese Tests) besteht zu einem Drittel (30 %) aus IPHTTPS-Clients und zu zwei Dritteln (70 %) aus Teredo-Clients. Teredo-Clients bieten teilweise eine höhere Leistung als IPHTTPS-Clients, weil für Windows Server 2012 die empfangsseitige Skalierung (Receive Side Scaling, RSS) verwendet wird, bei der die Nutzung aller CPU-Cores möglich ist. Da bei diesen Tests RSS aktiviert ist, ist das Hyperthreading deaktiviert. Außerdem unterstützt TCP/IP unter Windows Server 2012 den UDP-Datenverkehr, sodass mit Teredo-Clients der Lastenausgleich über mehrere CPUs hinweg durchgeführt werden kann.  
  
Die Daten wurden sowohl für einen Lowend-Server (4 Core, 4 GB) als auch für Hardware erfasst, die eher im Bereich der Highend-Server anzusiedeln ist (8 Core, 8 GB).  Im folgenden finden Sie einen Screenshot des neuen Windows 8-Task-Managers auf der Low-End-Hardware mit 750 Clients (562 Teredo, 188 IPHTTPS), die ~ 77 MS/Sek. ausführen. Dies dient zum Simulieren von Benutzern, die keine Smartcard-Anmelde Informationen darstellen.  
  
Diese Testergebnisse zeigen, dass die Leistung von Teredo unter Windows 8 höher als für IPHTTPS ist. Gegenüber Windows 7 hat sich die Bandbreitenauslastung jedoch sowohl für Teredo als auch für IPHTTPS verbessert.  
  
![Testergebnisse](../../media/DirectAccess-Capacity-Planning/DACapacityPlanning1.gif)  
  
## <a name="high-end-hardware-test-environment"></a>Testumgebung für Highend-Hardware  
Die folgende Tabelle enthält die Ergebnisse, die mit der Testumgebung zum Ermitteln der Leistung für Highend-Hardware erzielt wurden. In diesem Dokument wird auf alle Testergebnisse und Analysen ausführlich eingegangen.  
  
||||  
|-|-|-|  
|Konfiguration-Hardware|Lowend-Hardware (4 GB RAM, 4 Core)|Highend-Hardware (8 GB RAM, 8 Core)|  
|Doppelter Tunnel<p>-PKI<p>-Einschließlich DNS64/NAT64|750 gleichzeitige Verbindungen bei 50 % CPU, 50 % Arbeitsspeicher mit Corpnet-NIC-Durchsatz von 75 MBit/s. Das %%amp;quot;Stretch Target%%amp;quot; beträgt 1.000 Benutzer bei 50 % CPU.|1500 gleichzeitige Verbindungen bei 50% CPU, 50% Arbeitsspeicher mit Corpnet-NIC-Durchsatz 150 Mbit/s.|  
## <a name="test-environment"></a>Testumgebung

**Perf Bench-Topologie**  
  
![Testumgebung](../../media/DirectAccess-Capacity-Planning/DACapacityPlanning2.gif)  
  
Die Testumgebung für die Leistung ist eine Bench mit fünf Computern. Für den Lowend-Hardwaretest wurde ein 4-Core-DirectAccess-Server mit 4 GB verwendet, und für den Highend-Hardwaretest wurde ein 8-Core-DirectAccess-Server mit 16 GB verwendet. Für Lowend- und Highend-Testumgebungen wurde Folgendes verwendet: ein Back-End-Server (Absender) und zwei Clientcomputer (Empfänger).  Die Empfänger sind auf die beiden Clientcomputer aufgeteilt. Andernfalls wären die Empfänger an die CPU gebunden und würden so zu einer Beschränkung der Anzahl von Clients und der Bandbreite führen. Auf der empfangenden Seite wurde ein Simulator zum Simulieren von Hunderten von Clients eingesetzt (Simulation von HTTPS- oder Teredo-Clients). IPsec und DOSp wurden jeweils konfiguriert. RSS ist auf dem DirectAccess-Server aktiviert. Die RSS-Warteschlangengröße ist auf 8 festgelegt.  Ohne Konfiguration von RSS weist ein Prozessor eine hohe Auslastung auf, während die anderen Cores über eine zu geringe Auslastung verfügen. Außerdem ist zu beachten, dass der DirectAccess-Server ein 4-Core-Computer mit deaktiviertem Hyperthreading ist.  Das Hyperthreading ist deaktiviert, da RSS nur auf physischen Cores funktioniert und die Nutzung von Hyperthreading zu fehlerhaften Ergebnissen führt. (Dies bedeutet, dass nicht alle Cores einheitlich geladen werden.)  
  
## <a name="testing-results-for-low-end-hardware"></a>Testergebnisse für Lowend-Hardware:

Die Tests wurden sowohl mit 1.000 Clients als auch mit 750 Clients durchgeführt.  In allen Fällen wurde der Datenverkehr zu 70 % auf Teredo und zu 30 % auf IPHTTPS aufgeteilt.  Bei allen Tests verlief der TCP-Datenverkehr über Nat64, indem zwei IPsec-Tunnel pro Client verwendet wurden.  In allen Tests war die Arbeitsspeicherauslastung gering und die CPU-Auslastung akzeptabel.  
  
**Einzelner Testergebnisse:**  
  
Die folgenden Abschnitte enthalten Informationen zu den einzelnen Tests. Im Titel eines Abschnitts sind jeweils die wichtigsten Elemente des Tests gefolgt von einer Zusammenfassung der Ergebnisse angegeben. In einer Tabelle sind dann die ausführlichen Ergebnisse aufgeführt.  
  
**Low-End-Leistung: 750 Clients, 70/30 Split, 84,17 MBits/Sek. Durchsatz:**  
  
Die folgenden drei Tests zeigen die Ergebnisse für Lowend-Hardware.  In den unten angegebenen Testläufen wurden 750 Clients mit einem Durchsatz von 84,17 MBit/s und einer Datenverkehrsaufteilung von 562 (Teredo) zu 188 (IPHTTPS) verwendet. Teredo-MTU war auf 1.472 festgelegt, und Teredo-Shunt war aktiviert. Die CPU-Auslastung erreichte bei den drei Tests im Durchschnitt 46,42 %. Die durchschnittliche Arbeitsspeicherauslastung, die als Prozentsatz der zugesicherten Bytes des gesamten verfügbaren Arbeitsspeichers von 4 GB ausgedrückt wird, lag bei 25,95 %.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Szenario**|**Cpuavg (aus Indikator)**|**Mbit/s (Corp-Seite)**|**Mbit/s (Internet seitig)**|**Aktive qmsa**|**Aktives mmsa**|**Arbeitsspeicher Auslastung (4-GB-System)**|  
|**Low-End-HW.  562 Teredo-Clients.  188 IPHTTPS-Clients.**|47,7472542|84,3|119,13|1502,05|1502,1|26,27%|  
|**Low-End-HW.  562 Teredo-Clients.  188 IPHTTPS-Clients.**|46,3889778|84,146|118,73|1501,25|1501,2|25,90%|  
|**Low-End-HW.  562 Teredo-Clients.  188 IPHTTPS-Clients.**|45,113082|84,0494|118,43|1546,14|1546,1|25,68%|  
  
**1000 Clients, 70/30 Teilung, 78 MS/Sek. Durchsatz:**  
  
Mit den folgenden drei Tests wurde die Leistung für Lowend-Hardware ermittelt. In den unten angegebenen Testläufen wurden 1.000 Clients mit einem durchschnittlichen Durchsatz von ca. 78,64 MBit/s und einer Datenverkehrsaufteilung von 700 (Teredo) zu 300 (IPHTTPS) verwendet.  Teredo-MTU war auf 1.472 festgelegt, und Teredo-Shunt war aktiviert.  Die CPU-Auslastung erreichte im Durchschnitt ca. 50,7 %. Die durchschnittliche Arbeitsspeicherauslastung, die als Prozentsatz der zugesicherten Bytes des gesamten verfügbaren Arbeitsspeichers von 4 GB ausgedrückt wird, lag bei ca. 28,7%.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Szenario**|**Cpuavg (aus Indikator)**|**Mbit/s (Corp-Seite)**|**Mbit/s (Internet seitig)**|**Aktive qmsa**|**Aktives mmsa**|**Arbeitsspeicher Auslastung (4-GB-System)**|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|51,28406247|78,6432|113,19|2002,42|1502,1|25,59%|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|51,06993128|78,6402|113,22|2001,4|1501,2|30,87%|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|49,75235617|78,6387|113,2|2002,6|1546,1|30,66%|  
  
**1000 Clients, 70/30 Teilung, 109 MS/Sek. Durchsatz:**  
  
In den folgenden drei Testläufen wurden 1.000 Clients mit einem durchschnittlichen Durchsatz von ca. 109,2 MBit/s und einer Datenverkehrsaufteilung von 700 (Teredo) zu 300 (IPHTTPS) verwendet. Teredo-MTU war auf 1.472 festgelegt, und Teredo-Shunt war aktiviert. Die CPU-Auslastung erreichte bei den drei Tests im Durchschnitt ca. 59,06%. Die durchschnittliche Arbeitsspeicherauslastung, die als Prozentsatz der zugesicherten Bytes des gesamten verfügbaren Arbeitsspeichers von 4 GB ausgedrückt wird, lag bei ca. 27,34 %.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Szenario**|**Cpuavg (aus Indikator)**|**Mbit/s (Corp-Seite)**|**Mbit/s (Internet seitig)**|**Aktive qmsa**|**Aktives mmsa**|**Arbeitsspeicher Auslastung (4-GB-System)**|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|59,81640675|108,305|153,14|2001,64|2001,6|24,38%|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|59,46473798|110,969|157,53|2005,22|2005,2|28,72%|  
|**Low-End-HW.  700 Teredo-Clients.  300 IPHTTPS-Clients.**|57,89089768|108,305|153,14|1999,53|2018,3|24,38%|  
  
## <a name="testing-results-for-high-end-hardware"></a>Testergebnisse für Highend-Hardware:  
Die Tests wurden mit 1.500 Clients durchgeführt. Der Datenverkehr wurde zu 70 % auf Teredo und zu 30 % auf IPHTTPS aufgeteilt. Bei allen Tests verlief der TCP-Datenverkehr über Nat64, indem zwei IPsec-Tunnel pro Client verwendet wurden. In allen Tests war die Arbeitsspeicherauslastung gering und die CPU-Auslastung akzeptabel.  
  
**Einzelner Testergebnisse:**  
  
Die folgenden Abschnitte enthalten Informationen zu den einzelnen Tests. Im Titel eines Abschnitts sind jeweils die wichtigsten Elemente des Tests gefolgt von einer Zusammenfassung der Ergebnisse angegeben. In einer Tabelle sind dann die ausführlichen Ergebnisse aufgeführt.  
  
**1500 Clients, 70/30 Teilung, 153,2 Mbits/s Durchsatz**  
  
Die folgenden fünf Tests zeigen die Ergebnisse für Highend-Hardware. In den unten angegebenen Testläufen wurden 1.500 Clients mit einem durchschnittlichen Durchsatz von 153,2 MBit/s und einer Datenverkehrsaufteilung von 1050 (Teredo) zu 450 (IPHTTPS) verwendet. Die CPU-Auslastung erreichte bei den fünf Tests im Durchschnitt 50,68%. Die durchschnittliche Arbeitsspeicherauslastung, die als Prozentsatz der zugesicherten Bytes des gesamten verfügbaren Arbeitsspeichers von 8 GB ausgedrückt wird, lag bei 22,25 %.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Szenario**|**Cpuavg (aus Indikator)**|**Mbit/s (Corp-Seite)**|**Mbit/s (Internet seitig)**|**Aktive qmsa**|**Aktives mmsa**|**Arbeitsspeicher Auslastung (4-GB-System)**|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|51,712437|157,029|216,29|3000,31|3046|21,58%|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|48,86020205|151,012|206,53|3002,86|3045,3|21,15%|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|52,23979519|155,511|213,45|3001,15|3002,9|22,90%|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|51,26269767|155,09|212,92|3000,74|3002,4|22,91%|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|50,15751307|154,772|211,92|3000,9|3002,1|22,93%|  
|**High-End-HW.  1050 Teredo-Clients.  450 IPHTTPS-Clients.**|49,83665607|145,994|201,92|3000,51|3006|22,03%|  
  
![High-End-Hardware Testergebnisse](../../media/DirectAccess-Capacity-Planning/DACapacityPlanning3.gif)  
  


