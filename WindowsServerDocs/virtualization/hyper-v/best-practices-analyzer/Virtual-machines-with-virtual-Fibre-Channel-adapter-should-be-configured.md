---
title: Mit einem virtuellen Fibre Channel Adapter konfigurierte virtuelle Computer müssen für hohe Verfügbarkeit im Fibre Channel basierten Speicher konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
ms.date: 8/16/2016
ms.openlocfilehash: 8a6c86f34f42dd88b29653096fbcb67919081a08
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746215"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>Mit einem virtuellen Fibre Channel Adapter konfigurierte virtuelle Computer müssen für hohe Verfügbarkeit im Fibre Channel basierten Speicher konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Information|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Mindestens einer virtuellen Maschine fehlt eine hoch verfügbare Verbindung mit Fibre Channel basiertem Speicher, da diese virtuellen Computer mit einem virtuellen Fibre Channel Adapter konfiguriert sind, der nur mit einem Hostbus Adapter (HBA) verbunden ist.*

## <a name="impact"></a>**Auswirkungen**
*Ein Ausfall des Hostbus Adapters blockiert möglicherweise die Fibre Channel Verbindung zwischen dem Speicher und den virtuellen Computern. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Fügen Sie dem Hostbus Adapter eine weitere Verbindung vom virtuellen Computer hinzu, und konfigurieren Sie Multipfad-e/a (MPIO) im Gast Betriebssystem, um redundante Fibre Channel Verbindungen herzustellen.*



