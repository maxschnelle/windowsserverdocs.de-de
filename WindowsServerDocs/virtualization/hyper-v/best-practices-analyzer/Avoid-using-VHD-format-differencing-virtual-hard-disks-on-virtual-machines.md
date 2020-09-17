---
title: Vermeiden Sie die Verwendung differenzierender virtueller Festplatten im VHD-Format auf virtuellen Computern, die Server Arbeits Auslastungen in einer Produktionsumgebung ausführen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
ms.date: 8/16/2016
ms.openlocfilehash: 688dd348a7b00a32a50778cf0fb6350b37232f58
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747015"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>Vermeiden Sie die Verwendung differenzierender virtueller Festplatten im VHD-Format auf virtuellen Computern, die Server Arbeits Auslastungen in einer Produktionsumgebung ausführen.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Mindestens eine virtuelle Maschine verwendet differenzierende virtuelle Festplatten im VHD-Format.*

## <a name="impact"></a>**Auswirkungen**
*Bei differenzierenden virtuellen Festplatten im VHD-Format können Konsistenzprobleme auftreten, wenn ein Stromausfall auftritt. Konsistenzprobleme können auftreten, wenn die physische Festplatte ein unvollständiges oder falsches Update eines Sektors in einer VHD-Datei ausführt, die bei einem Stromausfall geändert wird. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Fahren Sie den virtuellen Computer herunter, und konvertieren Sie die Kette der differenzierenden virtuellen Festplatten im VHD-Format in das vhdx-Format, oder führen Sie die Kette mit einer festen virtuellen Festplatte zusammen. (Das vhdx-Format verfügt über Zuverlässigkeits Mechanismen, mit denen der Datenträger vor Beschädigungen aufgrund von Stromausfällen geschützt wird.) Konvertieren Sie die virtuelle Festplatte jedoch nicht, wenn Sie zu einem bestimmten Zeitpunkt wahrscheinlich an eine frühere Version von Windows angefügt wird. Ältere Windows-Versionen als Windows Server 2012 unterstützen das vhdx-Format nicht.*



