---
title: Vermeiden Sie die Zuordnung von einem Speicherpfad zu mehreren Ressourcenpools.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
ms.date: 8/16/2016
ms.openlocfilehash: fb2756889907dd9e268782816a9d035c9e6478d7
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747045"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>Vermeiden Sie die Zuordnung von einem Speicherpfad zu mehreren Ressourcenpools.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Ein Speicher Dateipfad ist mehreren Ressourcenpools zugeordnet.*

## <a name="impact"></a>**Auswirkungen**
*Für den angegebenen Speicher Pooltyp verwenden die folgenden über-und untergeordneten Pools denselben Speicherpfad:*

\<list of pools>

## <a name="resolution"></a>**Lösung**
*Verwenden Sie Windows PowerShell, um die Speicherressourcen Pools so neu zu konfigurieren, dass mehrere Pools nicht denselben Speicherpfad verwenden.*



