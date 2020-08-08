---
title: Konfigurieren Sie die TCP/IP-Failover-Einstellungen, die der virtuelle Replikat Computer im Falle eines Failovers verwenden soll.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 713be5cf428617287e0be0bc65b3e2beb2d11400
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948448"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>Konfigurieren Sie die TCP/IP-Failover-Einstellungen, die der virtuelle Replikat Computer im Falle eines Failovers verwenden soll.

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
*Virtuelle Replikat Computer, die mit einer statischen IP-Adresse konfiguriert sind, müssen so konfiguriert werden, dass Sie im Fall eines Failovers eine andere IP-Adresse von Ihrem primären virtuellen Computer verwenden.*

## <a name="impact"></a>Auswirkung
*Clients, die die Arbeitsauslastung verwenden, die vom primären virtuellen Computer unterstützt wird, können nach einem Failover möglicherweise keine Verbindung mit dem virtuellen Replikat Computer herstellen. Außerdem ist die ursprüngliche IP-Adresse des primären virtuellen Computers in der Netzwerktopologie des virtuellen Replikat Computers nicht gültig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Hyper-V-Manager, um die IP-Adresse zu konfigurieren, die vom virtuellen Replikat Computer bei einem Failover verwendet werden soll.*



