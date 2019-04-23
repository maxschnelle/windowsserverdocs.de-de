---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: 4e8e3234b89630bf16148eef644f0c6607ad38bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852341"
---
## <a name="importance-of-time-protocols"></a>Wichtigkeit der Time-Protokolle
Zeit Protokolle kommunizieren zwischen zwei Computern zum Austauschen von Informationen aus, und klicken Sie dann anhand dieser Informationen ihre Uhren synchronisieren. Mit dem Windows Time Service Time-Protokoll ein Client fordert Informationen von einem Server und synchronisiert die Uhr basierend auf den Informationen, der empfangen werden.
  
Der Windows-Zeitdienst verwendet NTP um zeitsynchronisierung in einem Netzwerk. NTP ist ein Internetprotokoll für die Zeit, die die Disziplin Algorithmen erforderlich für die Synchronisierung von Uhren enthält. NTP ist eine genauere Time-Protokoll als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. allerdings weiterhin W32Time SNTP zum Aktivieren der Abwärtskompatibilität mit der Zeit SNTP-basierte Dienste, z. B. Windows 2000-Computern unterstützt.

Es gibt viele verschiedene Gründe, dass Sie möglicherweise die genaue Zeit benötigen.  Die typische Fall für Windows ist Kerberos verwendet, die 5 Minuten der Genauigkeit zwischen Client und Server erforderlich ist.  Es gibt jedoch viele andere Bereiche, die dazu zählen Genauigkeit auswirken können:


- Gesetzliche Vorschriften wie folgt vor:
    - 50 ms beträgt die Genauigkeit für FINRA in den USA
    - 1 ms ESMA (MiFID II) in der EU.
- Kryptografischen Algorithmen
- Verteilte Systeme wie Cluster/SQL/Exchange und der Dokument-Datenbanken
- Blockchain-Framework für Bitcoin-Transaktionen
- Verteilte Protokolle und Bedrohungsanalyse 
- AD-Replikation
- PCI (Payment Card Industry), Zeit 1 Sekunde Genauigkeit