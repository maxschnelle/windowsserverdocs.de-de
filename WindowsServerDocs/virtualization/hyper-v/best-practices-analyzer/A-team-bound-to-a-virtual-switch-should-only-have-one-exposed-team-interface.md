---
title: Ein Team, das an einen virtuellen Switch gebunden ist, darf nur über eine Team Schnittstelle verfügen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7ec4c25a86bf90f1b2416e0d53ded8f5319960ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968517"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>Ein Team, das an einen virtuellen Switch gebunden ist, darf nur über eine Team Schnittstelle verfügen.

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
*Ein oder mehrere virtuelle Switches sind an ein Team gebunden, das über mehrere Team Schnittstellen verfügt.*

## <a name="impact"></a>Auswirkung
*Die folgenden virtuellen Switches haben möglicherweise keinen Zugriff auf VLANs und Bandbreite, die von anderen Team Schnittstellen verwendet werden:*

\<list of virtual switches>

## <a name="resolution"></a>Lösung
*Verwenden Sie das Windows PowerShell-Cmdlet Remove-netlbfoteamnic, um alle Team Schnittstellen aus dem anderen Team als der standardmäßigen Team Schnittstelle zu entfernen.*



