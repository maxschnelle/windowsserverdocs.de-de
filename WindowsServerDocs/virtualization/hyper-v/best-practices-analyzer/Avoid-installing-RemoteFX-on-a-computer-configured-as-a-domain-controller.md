---
title: Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
ms.date: 8/16/2016
ms.openlocfilehash: 1f639998c568035d0c992403cd0b1056ea4607b5
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747055"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.

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
*Remotefx ist auf einem Domänen Controller installiert.*

## <a name="impact"></a>**Auswirkungen**
*Für remotefx konfigurierte virtuelle Computer können auf diesen Computern nicht verwendet werden.*

## <a name="resolution"></a>**Lösung**
*Entscheiden Sie, ob dieser Server entweder mit remotefx für Hyper-V oder als Active Directory-Domäne Controller konfiguriert werden soll, und konfigurieren Sie den Server bei Bedarf neu.*



