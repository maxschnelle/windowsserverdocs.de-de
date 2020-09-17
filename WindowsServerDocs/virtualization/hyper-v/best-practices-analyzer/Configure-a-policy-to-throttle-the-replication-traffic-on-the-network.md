---
title: Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
ms.date: 8/16/2016
ms.openlocfilehash: 18c1c1e586075dfb1ef477c1d3f21e549791464a
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746985"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk

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
*Möglicherweise gibt es keine Beschränkung für die Menge an Netzwerkbandbreite, die von der Replikation beansprucht werden darf.*

## <a name="impact"></a>Auswirkung
*Die Netzwerkbandbreite könnte vollständig von Replikations Datenverkehr dominiert werden Dies wirkt sich auf die folgenden Ports aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Wenn Sie eine andere Methode zum Einschränken des Netzwerk Datenverkehrs verwenden, können Sie dies ignorieren. Verwenden Sie andernfalls Gruppenrichtlinie-Editor, um eine Richtlinie zu konfigurieren, die den Netzwerk Datenverkehr zum relevanten Port des Replikat Servers drosselt.*




