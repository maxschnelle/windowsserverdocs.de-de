---
title: Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
ms.date: 8/16/2016
ms.openlocfilehash: 792ee7f84694171b7b44602c8bb1a5c307d80c6c
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747075"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.

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
*Für eine differenzierende virtuelle Festplatte mit der übergeordneten und der untergeordneten virtuellen Festplatte auf unterschiedlichen Volumes ist Storage Quality of Service aktiviert.*

## <a name="impact"></a>**Auswirkungen**
*Diese Konfiguration kann zu unerwartetem Speicher Quality of Service Verhalten für die differenzierende virtuelle Festplatte sowie zu anderen virtuellen Festplatten auf den übergeordneten und untergeordneten Volumes führen. Dies wirkt sich auf folgende virtuelle Festplatten aus:*

\<list of virtual hard disks>

## <a name="resolution"></a>**Lösung**
*Deaktivieren Sie Speicher Quality of Service auf den virtuellen Festplatten, auf die verwiesen wird, oder führen Sie eine Speicher Migration aus, um die übergeordnete und die untergeordnete virtuelle Festplatte auf dasselbe Volume zu verschieben.*



