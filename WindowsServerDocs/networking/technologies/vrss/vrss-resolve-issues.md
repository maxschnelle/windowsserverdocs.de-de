---
title: Probleme mit vRSS
description: Beheben Sie vRSS Probleme, wenn Sie Lastenausgleich des Datenverkehrs auf die VM-LPs vRSS nicht angezeigt werden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: a2d6eb43149361b4270565b63fc99f483f364f74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824031"
---
## <a name="resolve-vrss-issues"></a>Probleme mit vRSS

Wenn Sie alle Vorbereitungsschritte zur abgeschlossen haben und trotzdem nicht angezeigt. vRSS Lastenausgleich des Datenverkehrs auf die VM-LPs, gibt es verschiedene mögliche Probleme.

1. Bevor Sie die vorbereitenden Schritte ausgeführt, wird vRSS wurde deaktiviert – und nun muss aktiviert werden kann. Sie können ausführen **Set-VMNetworkAdapter** vRSS für den virtuellen Computer zu aktivieren.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS wurde auf dem virtuellen Computer oder auf die Host-vNIC deaktiviert. Windows Server 2016 aktiviert RSS sind standardmäßig; jemand könnte es deaktiviert. 

   - Aktiviert = **"true"**

   **Zeigen Sie die aktuellen Einstellungen an:** 

   Führen das folgende PowerShell-Cmdlet auf dem virtuellen Computer\(für vRSS auf einem virtuellen Computer\) oder auf dem Host \(für Host-vNIC vRSS\).

   ```PowerShell
   Get-NetAdapterRss
   ```

   **Aktivieren Sie das Feature:** 

   Um den Wert von "false" auf "true" zu ändern, führen Sie das folgende PowerShell-Cmdlet.

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   Eine andere systemweite Möglichkeit zum Konfigurieren von RSS verwendet Netsh. Verwendung 
   
    ```cmd
   netsh int tcp show global
   ```
   
   um sicherzustellen, ist nicht diesem RSS global deaktiviert. Und aktivieren sie bei Bedarf. Diese Einstellung wird nicht von berührt *-NetAdapterRSS.

3. Wenn Sie, dass VMMQ nicht aktiviert ist feststellen, nachdem Sie vRSS konfiguriert haben, überprüfen Sie die folgenden Einstellungen für die einzelnen Adapter an den virtuellen Switch angefügt:

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq-enabled](../../media/vmmq-enabled.png)

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **Aktivieren Sie das Feature:** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(WindowsServer 2019)_  VMMQ kann nicht aktiviert werden (VmmqEnabled = False) Einstellung zwar **VrssQueueSchedulingMode** zu **dynamische**. Die VrssQueueSchedulingMode ändert nicht in einen dynamischen, sobald die VMMQ aktiviert ist.<p>Die **VrssQueueSchedulingMode** von **dynamische** Driver-Unterstützung ist erforderlich, wenn VMMQ aktiviert ist.  VMMQ ist eine Auslagerung der Platzierung Paket auf logischen Prozessoren und erfordert das Driver-Unterstützung des dynamischen Algorithmus nutzen.  Installieren des Anbieters, der den NIC-Treiber und Firmware, die dynamische VMMQ unterstützt.



---
