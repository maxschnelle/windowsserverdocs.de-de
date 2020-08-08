---
title: Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 5a5c2d23794ba2328da9a2a8c668a8525f6c6322
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960673"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Remotefx ist auf einem Domänen Controller installiert.*

## <a name="impact"></a>**Auswirkungen**
*Für remotefx konfigurierte virtuelle Computer können auf diesen Computern nicht verwendet werden.*

## <a name="resolution"></a>**Lösung**
*Entscheiden Sie, ob dieser Server entweder mit remotefx für Hyper-V oder als Active Directory-Domäne Controller konfiguriert werden soll, und konfigurieren Sie den Server bei Bedarf neu.*



