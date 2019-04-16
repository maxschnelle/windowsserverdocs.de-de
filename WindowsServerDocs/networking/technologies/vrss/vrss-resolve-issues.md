---
title: Probleme mit vRSS
description: Lösen Sie vRSS Probleme, wenn Sie nicht vRSS Netzwerklastenausgleich Datenverkehr auf die VM-LPs Laden angezeigt werden.
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
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232519"
---
## Probleme mit vRSS

Wenn Sie alle Vorbereitungsschritte zur abgeschlossen haben, und Sie immer noch nicht anzeigen vRSS Netzwerklastenausgleich Datenverkehr auf die VM-LPs zu laden, gibt es verschiedene mögliche Probleme.

1. Bevor Sie vorbereitenden Schritte ausgeführt haben, wird vRSS wurde deaktiviert - und kann jetzt muss aktiviert sein. Sie können **Set-VMNetworkAdapter** zum Aktivieren der vRSS für den virtuellen Computer ausführen.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS wurde auf dem virtuellen Computer oder auf die Host-vNIC deaktiviert. Windows Server 2016 aktiviert RSS sind standardmäßig; eine Person möglicherweise deaktiviert. 

   - Aktiviert = **"true"**

   **Zeigen Sie die aktuellen Einstellungen an:** 

   Führen Sie das folgende PowerShell-Cmdlet in der VM\ (für vRSS in einer VM\) oder auf dem Host \ (für die Host-vNIC vRSS\).

   ```PowerShell
   Get-NetAdapterRss
   ```

   **Das Feature zu aktivieren:** 

   Um den Wert von "false" auf "true" zu ändern, führen Sie das folgende PowerShell-Cmdlet.

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   Eine andere systemweiten Möglichkeit zum Konfigurieren von RSS verwendet Netsh. Verwendung 
   
    ```cmd
   netsh int tcp show global
   ```
   
   um sicherzustellen, nicht, RSS global deaktiviert ist. Und es aktivieren, falls erforderlich. Diese Einstellung ist nicht berührt hat, indem Sie *-NetAdapterRSS.

3. Wenn Sie, dass VMMQ nicht aktiviert ist feststellen, nachdem Sie vRSS konfiguriert, überprüfen Sie die folgenden Einstellungen für die einzelnen Adapter mit dem virtuellen Switch verbunden:

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **"true"**

   ![Vmmq aktiviert](../../media/vmmq-enabled.png)

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **Das Feature zu aktivieren:** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(WindowsServer 2019)_ Sie können keine VMMQ aktivieren (VmmqEnabled = "false") beim Festlegen der **VrssQueueSchedulingMode** in einen **dynamischen**. Die VrssQueueSchedulingMode wird nicht in einen dynamischen geändert, sobald die VMMQ aktiviert ist.<p>Die **VrssQueueSchedulingMode** des **dynamischen** benötigt treiberunterstützung VMMQ aktiviert ist.  VMMQ ist ein Offload der Anordnung Paket auf logischen Prozessoren und als solches benötigt treiberunterstützung den dynamischen Algorithmus nutzen.  Installieren Sie die NIC-Herstellers Treiber- und Firmwareversionen, die dynamische VMMQ unterstützt.



---
