---
title: Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 48c8ee80a0044c067d29730c1ec79bd67fdc062b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950254"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Mindestens ein virtueller Netzwerkadapter ist mit einem virtuellen Switch mit obligatorischen Erweiterungen verbunden, die deaktiviert oder nicht installiert sind.*

## <a name="impact"></a>Auswirkung
*Der Netzwerk Datenverkehr wird auf einem oder mehreren virtuellen Netzwerkadaptern auf den folgenden virtuellen Computern blockiert:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Stellen Sie zunächst sicher, dass die obligatorische Erweiterung auf dem Host installiert ist, und installieren Sie die Erweiterung bei Bedarf. Wenn die obligatorische Erweiterung deaktiviert ist, verwenden Sie den Virtual Switch-Manager oder das Windows PowerShell-Cmdlet Enable-vmswitchextension, um die Erweiterung zu aktivieren.*



