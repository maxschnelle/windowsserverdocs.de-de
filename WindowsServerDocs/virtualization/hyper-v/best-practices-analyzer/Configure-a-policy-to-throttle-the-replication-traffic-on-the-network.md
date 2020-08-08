---
title: Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: dcee85911ebcc93e935a7df30d43768a15978ece
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957177"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk

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
*Möglicherweise gibt es keine Beschränkung für die Menge an Netzwerkbandbreite, die von der Replikation beansprucht werden darf.*

## <a name="impact"></a>Auswirkung
*Die Netzwerkbandbreite könnte vollständig von Replikations Datenverkehr dominiert werden Dies wirkt sich auf die folgenden Ports aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Wenn Sie eine andere Methode zum Einschränken des Netzwerk Datenverkehrs verwenden, können Sie dies ignorieren. Verwenden Sie andernfalls Gruppenrichtlinie-Editor, um eine Richtlinie zu konfigurieren, die den Netzwerk Datenverkehr zum relevanten Port des Replikat Servers drosselt.*




