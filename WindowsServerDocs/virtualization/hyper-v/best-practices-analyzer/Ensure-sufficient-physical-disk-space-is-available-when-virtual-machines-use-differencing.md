---
title: Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer differenzierende virtuelle Festplatten verwenden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
ms.date: 8/16/2016
ms.openlocfilehash: d5a8c5d38aa47845a88077eaa6b785dc5ebb148c
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746275"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer differenzierende virtuelle Festplatten verwenden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Mindestens eine virtuelle Maschine verwendet differenzierende virtuelle Festplatten.*

## <a name="impact"></a>Auswirkung
*Bei differenzierenden virtuellen Festplatten ist verfügbarer Speicherplatz auf dem hostingvolume erforderlich, damit Speicherplatz zugewiesen werden kann, wenn Schreibvorgänge auf den virtuellen Festplatten stattfinden. Wenn der verfügbare Speicherplatz erschöpft ist, kann der virtuelle Computer, der auf dem physischen Speicher basiert, beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Überwachen Sie den verfügbaren Speicherplatz, um sicherzustellen, dass ausreichend Speicherplatz für die Erweiterung virtueller Festplatten Sie sollten differenzierende virtuelle Festplatten mit ihrem übergeordneten Element zusammenführen. Überprüfen Sie im Hyper-V-Manager den differenzierenden Datenträger, um die übergeordnete virtuelle Festplatte zu ermitteln. Wenn Sie einen differenzierenden Datenträger mit einem übergeordneten Datenträger zusammenführen, der von anderen differenzierenden Datenträgern gemeinsam verwendet wird, wird durch diese Aktion die Beziehung zwischen den anderen differenzierenden Datenträgern und dem übergeordneten Datenträger beschädigt, sodass Sie unbrauchbar werden. Nachdem Sie überprüft haben, dass die übergeordnete virtuelle Festplatte nicht freigegeben ist, können Sie mit dem Assistenten zum Bearbeiten von Datenträgern den differenzierenden Datenträger mit der übergeordneten virtuellen Festplatte zusammenführen.*



