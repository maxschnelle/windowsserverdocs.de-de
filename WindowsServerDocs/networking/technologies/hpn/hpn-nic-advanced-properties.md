---
title: NIC erweiterte Eigenschaften
description: Sie können NICs und alle Funktionen, die über Windows PowerShell oder mithilfe der Netzwerk-Systemsteuerung verwalten.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: d1a5fb57bf71fd981e001cfd9ac595ab5bc3cfc5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819901"
---
# <a name="nic-advanced-properties"></a>NIC erweiterte Eigenschaften

Sie können NICs und alle Funktionen über die Verwendung von Windows PowerShell verwalten die [NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps) Cmdlet.  Sie können auch Netzwerkkarten und alle Funktionen, die mit den Netzwerk-Systemsteuerung (ncpa.cpl) verwalten. 

1. In **Windows PowerShell**führen die `Get‑NetAdapterAdvancedProperties` -Cmdlets in zwei verschiedene Hersteller/Modell von Netzwerkkarten.

   ![Get-NetAdapterAdvancedProperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![Get-NetAdapterAdvancedProperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   Es gibt ähnlichkeiten und Unterschiede in diesen beiden NIC erweiterte Eigenschaften angezeigt.

2. In der **Network Control Panel** (ncpa.cpl), gehen Sie folgendermaßen vor:

   a. mit der rechten Maustaste die NIC.

   ![Dialogfeld für Netzwerk-Verbindungen](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. Klicken Sie im Eigenschaftendialogfeld auf **konfigurieren**.

    ![C1-Eigenschaften](../../media/network-offload-and-optimization/c1-properties.png)

   c. Klicken Sie auf die **erweitert** Registerkarte, um die erweiterten Eigenschaften anzuzeigen.<p>Die Elemente in dieser Liste entspricht der Elemente in der `Get-NetAdapterAdvancedProperties` Ausgabe.

   ![Eigenschaften für Chelsio des Netzwerkadapters](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---