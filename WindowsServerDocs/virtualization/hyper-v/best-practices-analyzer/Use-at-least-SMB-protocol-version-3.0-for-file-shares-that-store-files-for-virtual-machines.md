---
title: Verwenden Sie mindestens SMB-Protokollversion 3,0 für Dateifreigaben, in denen Dateien für virtuelle Maschinen gespeichert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
ms.date: 8/16/2016
ms.openlocfilehash: a979035c5b58542865faf6254baf49815f81cc2d
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746785"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>Verwenden Sie mindestens SMB-Protokollversion 3,0 für Dateifreigaben, in denen Dateien für virtuelle Maschinen gespeichert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Dateien für virtuelle Computer oder virtuelle Festplatten Dateien werden in einer Dateifreigabe gespeichert, die mindestens SMB-Protokollversion 3,0 nicht unterstützt.*

## <a name="impact"></a>**Auswirkungen**
*Diese Konfiguration wird von Microsoft nicht unterstützt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Verschieben Sie die Dateien in eine Dateifreigabe, die mindestens die SMB-Protokollversion 3,0 verwendet.*



