---
title: Alle virtuellen Funktionen für das Netzwerk verwenden, wenn diese verfügbar sind
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
ms.date: 8/16/2016
ms.openlocfilehash: 4a1502180350c338793bf811cddc675785e9c67a
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746805"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>Alle virtuellen Funktionen für das Netzwerk verwenden, wenn diese verfügbar sind

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
*Einige Hardware Beschleunigungsfunktionen werden nicht verwendet.*

## <a name="impact"></a>Auswirkung
*Diese Konfiguration kann dazu führen, dass die CPU-Gesamtauslastung höher als notwendig ist. Die Netzwerkleistung ist auf den folgenden virtuellen Computern möglicherweise nicht optimal:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Sie sollten den virtuellen Netzwerkadapter für SR-IOV konfigurieren, wenn die physische Hardware SR-IOV unterstützt und wenn diese Konfiguration nicht mit den Netzwerk Features in Konflikt steht, die für die virtuelle Maschine erforderlich sind.*



