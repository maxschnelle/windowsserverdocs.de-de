---
title: Die an einen virtuellen Switch gebundene Team Schnittstelle sollte sich im Standardmodus befinden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
ms.date: 8/16/2016
ms.openlocfilehash: 1e3d701ccc0ac7a6a3765df08f6b039fbb4ca3eb
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746135"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>Die an einen virtuellen Switch gebundene Team Schnittstelle sollte sich im Standardmodus befinden.

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
*Einige virtuelle Switches sind an eine Team Schnittstelle gebunden, aber die Team Schnittstelle übergibt nicht den Datenverkehr für alle VLANs an die virtuellen Switches.*

## <a name="impact"></a>**Auswirkungen**
*Die folgenden virtuellen Switches können nicht auf alle VLANs zugreifen: \n{0}*

## <a name="resolution"></a>**Lösung**
*Verwenden Sie Server-Manager oder das Windows PowerShell-Cmdlet Set-netlbfoteamnic, um die Team Schnittstelle auf den Standardmodus zurückzusetzen.*



