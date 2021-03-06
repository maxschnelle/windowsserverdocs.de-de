---
title: Vermeiden Sie die Verwendung virtueller Festplatten mit einer Sektorgröße, die kleiner ist als die Sektorgröße des physischen Speichers, in dem die virtuelle Festplatten Datei gespeichert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
ms.date: 8/16/2016
ms.openlocfilehash: 946168aa200ec80e5d2c9a69e0ecfad2477dcb6e
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745885"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>Vermeiden Sie die Verwendung virtueller Festplatten mit einer Sektorgröße, die kleiner ist als die Sektorgröße des physischen Speichers, in dem die virtuelle Festplatten Datei gespeichert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Operating** <br />**System**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Mindestens eine virtuelle Festplatte verfügt über eine physische Sektorgröße, die kleiner ist als die physische Sektorgröße des Speichers, in dem sich die Datei der virtuellen Festplatte befindet.*

## <a name="impact"></a>**Auswirkungen**
*Auf dem virtuellen Computer oder der Anwendung, die die virtuelle Festplatte verwenden, können Leistungsprobleme auftreten. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Führen Sie eines der folgenden Verfahren aus:*

-   *Durchführen einer Speicher Migration zum Verschieben der virtuellen Festplatte in ein neues physisches System*

-   *Verwenden Sie Windows PowerShell oder WMI, um eine virtuelle Festplatte im vhdx-Format zum Melden einer bestimmten Sektorgröße zu aktivieren.*

-   *Verwenden Sie eine Registrierungs Einstellung, um eine virtuelle Festplatte im VHD-Format zum Melden einer physischen Sektorgröße von 4K zu aktivieren.*



