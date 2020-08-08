---
title: Mit einem virtuellen Fibre Channel Adapter konfigurierte virtuelle Computer müssen für hohe Verfügbarkeit im Fibre Channel basierten Speicher konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 60a96d6e559f3fefe6f8c1c52c2d145efa006c99
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960183"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>Mit einem virtuellen Fibre Channel Adapter konfigurierte virtuelle Computer müssen für hohe Verfügbarkeit im Fibre Channel basierten Speicher konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Information|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Mindestens einer virtuellen Maschine fehlt eine hoch verfügbare Verbindung mit Fibre Channel basiertem Speicher, da diese virtuellen Computer mit einem virtuellen Fibre Channel Adapter konfiguriert sind, der nur mit einem Hostbus Adapter (HBA) verbunden ist.*

## <a name="impact"></a>**Auswirkungen**
*Ein Ausfall des Hostbus Adapters blockiert möglicherweise die Fibre Channel Verbindung zwischen dem Speicher und den virtuellen Computern. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Fügen Sie dem Hostbus Adapter eine weitere Verbindung vom virtuellen Computer hinzu, und konfigurieren Sie Multipfad-e/a (MPIO) im Gast Betriebssystem, um redundante Fibre Channel Verbindungen herzustellen.*



