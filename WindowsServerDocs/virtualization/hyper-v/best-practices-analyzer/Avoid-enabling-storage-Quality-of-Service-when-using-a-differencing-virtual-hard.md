---
title: Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b208a7a10679804666ff41a02d4cddbb4d8c6762
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939182"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Für eine differenzierende virtuelle Festplatte mit der übergeordneten und der untergeordneten virtuellen Festplatte auf unterschiedlichen Volumes ist Storage Quality of Service aktiviert.*

## <a name="impact"></a>**Auswirkungen**
*Diese Konfiguration kann zu unerwartetem Speicher Quality of Service Verhalten für die differenzierende virtuelle Festplatte sowie zu anderen virtuellen Festplatten auf den übergeordneten und untergeordneten Volumes führen. Dies wirkt sich auf folgende virtuelle Festplatten aus:*

\<list of virtual hard disks>

## <a name="resolution"></a>**Lösung**
*Deaktivieren Sie Speicher Quality of Service auf den virtuellen Festplatten, auf die verwiesen wird, oder führen Sie eine Speicher Migration aus, um die übergeordnete und die untergeordnete virtuelle Festplatte auf dasselbe Volume zu verschieben.*



