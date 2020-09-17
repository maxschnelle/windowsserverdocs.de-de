---
title: Test Failover sollten mindestens monatlich durchgeführt werden, um zu überprüfen, ob das Failover erfolgreich ist und die Arbeits Auslastungen virtueller Computer nach dem Failover erwartungsgemäß ausgeführt werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
ms.date: 8/16/2016
ms.openlocfilehash: 4ec97d55f1a6caf33b1b46d0a6bdb4e99005c971
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744093"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>Test Failover sollten mindestens monatlich durchgeführt werden, um zu überprüfen, ob das Failover erfolgreich ist und die Arbeits Auslastungen virtueller Computer nach dem Failover erwartungsgemäß ausgeführt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Es gab in mindestens einem Monat kein Test Failover.*

## <a name="impact"></a>Auswirkung
*Es gibt keine Bestätigung, dass ein geplantes oder ungeplantes Failover erfolgreich ist oder Arbeits Auslastungs Vorgänge nach einem Failover ordnungsgemäß fortgesetzt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Hyper-V-Manager, um ein Test Failover durchzuführen.*



