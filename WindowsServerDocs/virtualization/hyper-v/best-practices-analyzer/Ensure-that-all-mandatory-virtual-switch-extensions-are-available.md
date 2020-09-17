---
title: Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
ms.date: 8/16/2016
ms.openlocfilehash: 8eeadf6ed8b90ef217d694e2f14b38314b8be7a5
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746855"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.

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
*Mindestens ein virtueller Netzwerkadapter ist mit einem virtuellen Switch mit obligatorischen Erweiterungen verbunden, die deaktiviert oder nicht installiert sind.*

## <a name="impact"></a>Auswirkung
*Der Netzwerk Datenverkehr wird auf einem oder mehreren virtuellen Netzwerkadaptern auf den folgenden virtuellen Computern blockiert:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Stellen Sie zunächst sicher, dass die obligatorische Erweiterung auf dem Host installiert ist, und installieren Sie die Erweiterung bei Bedarf. Wenn die obligatorische Erweiterung deaktiviert ist, verwenden Sie den Virtual Switch-Manager oder das Windows PowerShell-Cmdlet Enable-vmswitchextension, um die Erweiterung zu aktivieren.*



