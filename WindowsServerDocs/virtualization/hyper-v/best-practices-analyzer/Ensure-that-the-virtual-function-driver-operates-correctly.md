---
title: Stellen Sie sicher, dass der virtuelle Funktions Treiber ordnungsgemäß funktioniert, wenn ein virtueller Computer für die Verwendung von SR-IOV konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 8fc14e14ff66b59099ebad1f3b9643b94427346a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954487"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>Stellen Sie sicher, dass der virtuelle Funktions Treiber ordnungsgemäß funktioniert, wenn ein virtueller Computer für die Verwendung von SR-IOV konfiguriert ist.

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
*Der Treiber für virtuelle Funktionen wird im Gast Betriebssystem von mindestens einer virtuellen Maschine nicht ordnungsgemäß ausgeführt.*

## <a name="impact"></a>Auswirkung
*Die Netzwerkleistung ist auf den folgenden virtuellen Computern nicht optimal:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Gehen Sie im Gast Betriebssystem wie folgt vor: Überprüfen Sie, ob die entsprechenden Treiber installiert sind und alle Netzwerkgeräte aktiviert sind, und überprüfen Sie das Ereignisprotokoll auf Fehler oder Warnungen.*



