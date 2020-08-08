---
title: 'NIC: Erweiterte Eigenschaften'
description: Sie können NICs und alle Features über Windows PowerShell oder die Netzwerksystem Steuerung verwalten.
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: aa26e3ef83ec6255da6a386ecfce34a7501ae3f5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955637"
---
# <a name="nic-advanced-properties"></a>NIC: Erweiterte Eigenschaften

Sie können NICs und alle Features mithilfe von Windows PowerShell über das Cmdlet [netadapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps) verwalten.  Sie können auch NICs und alle Features mithilfe der Netzwerksystem Steuerung (ncpa.cpl) verwalten.

1. Führen Sie in **Windows PowerShell**das `Get‑NetAdapterAdvancedProperties` Cmdlet für zwei unterschiedliche Make/Model-NICs aus.

   ![Get-netadapteradvancedproperty M1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![Get-netadapteradvancedproperty C1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   Es gibt Ähnlichkeiten und Unterschiede in diesen beiden Listen der erweiterten NIC-Eigenschaften.

2. Gehen Sie in der **Systemsteuerung** (ncpa.cpl) wie folgt vor:

   a. Klicken Sie mit der rechten Maustaste auf die NIC.

   ![Dialogfeld für Netzwerkverbindungen](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. Klicken Sie im Dialogfeld Eigenschaften auf **Konfigurieren**.

    ![C1-Eigenschaften](../../media/network-offload-and-optimization/c1-properties.png)

   c. Klicken Sie auf die Registerkarte **erweitert** , um die erweiterten Eigenschaften anzuzeigen.<p>Die Elemente in dieser Liste korrelieren mit den Elementen in der `Get-NetAdapterAdvancedProperties` Ausgabe.

   ![Eigenschaften von Chelsio-Netzwerkadaptern](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---
