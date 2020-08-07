---
title: Probleme mit vRSS
description: Beheben Sie vrss-Probleme, wenn der vrss-Lasten Ausgleichs-Datenverkehr für die VM-LPs nicht angezeigt wird.
ms.topic: article
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/04/2018
ms.openlocfilehash: a7f0a3b190232cafb68e3a39104c357972831441
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951950"
---
# <a name="resolve-vrss-issues"></a>Probleme mit vRSS

Wenn Sie alle Vorbereitungsschritte abgeschlossen haben und der vrss-Lasten Ausgleichs-Datenverkehr für die VM-LPs noch immer nicht angezeigt wird, sind unterschiedliche mögliche Probleme aufgetreten.

1. Bevor Sie Vorbereitungsschritte durchgeführt haben, wurde vrss deaktiviert und muss nun aktiviert werden. Sie können **Set-vmnetworkadapter** ausführen, um vrss für den virtuellen Computer zu aktivieren.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS wurde auf dem virtuellen Computer oder auf der Host-vNIC deaktiviert. Windows Server 2016 aktiviert RSS standardmäßig. möglicherweise hat jemand Sie deaktiviert.

   - Aktiviert = **true**

   **Anzeigen der aktuellen Einstellungen:**

   Führen Sie das folgende PowerShell-Cmdlet auf dem virtuellen Computer \( für vrss auf einem virtuellen Computer \) oder auf dem Host \( für Host-vNIC-vrss aus \) .

   ```PowerShell
   Get-NetAdapterRss
   ```

   **Aktivieren Sie das Feature:**

   Um den Wert von false in true zu ändern, führen Sie das folgende PowerShell-Cmdlet aus.

   ```PowerShell
   Enable-NetAdapterRss *
   ```

   Eine weitere systemweite Methode zum Konfigurieren von RSS ist die Verwendung von Netsh. Verwendung

    ```cmd
   netsh int tcp show global
   ```

   um sicherzustellen, dass RSS nicht global deaktiviert ist. Und aktivieren Sie es bei Bedarf. Diese Einstellung wird von *-netadapterrss nicht berührt.

3. Wenn vmmq nach dem Konfigurieren von vrss nicht aktiviert ist, überprüfen Sie die folgenden Einstellungen auf jedem Adapter, der an den virtuellen Switch angefügt ist:

   - Vmmqaktivierte = **false**
   - Vmmqenabledrequessiv = **true**

   ![vmmq-aktiviert](../../media/vmmq-enabled.png)

   **Anzeigen der aktuellen Einstellungen:**

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **Aktivieren Sie das Feature:**

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```

4. _(Windows Server 2019)_ Beim Festlegen von **vrssqueueschedulingmode** auf **Dynamic**können Sie vmmq (vmmqenable = false) nicht aktivieren. Der vrssqueueschedulingmode ändert sich nicht in "dynamisch", sobald vmmq aktiviert ist.<p>Der **vrssqueueschedulingmode** von **Dynamic** erfordert die Treiberunterstützung, wenn vmmq aktiviert ist.  Vmmq ist eine Auslagerung der Paket Platzierung auf logischen Prozessoren und erfordert daher Treiberunterstützung, um den dynamischen Algorithmus zu nutzen.  Installieren Sie den Treiber und die Firmware des NIC-Anbieters, die dynamisches vmmq unterstützt.



---
