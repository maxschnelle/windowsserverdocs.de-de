---
title: Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter
description: In diesem Thema erfahren Sie, wie Sie vRSS in Windows Server zu aktivieren, indem Sie mit Geräte-Manager oder Windows PowerShell.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cb48315c-0204-4927-aa24-64f6789c2e20
manager: dougkim
ms.localizationpriority: medium
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19e8011fb98b84c20e8237792664551d2362d589
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882681"
---
# <a name="enable-vrss-on-a-virtual-network-adapter"></a>Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Virtuelle \(vRSS\) erfordert von Virtual Machine Queue \(VMQ\) aus dem physischen Adapter zu unterstützen. Wenn VMQ deaktiviert ist, oder wird nicht unterstützt wird dann virtuelle empfangsseitige Skalierung deaktiviert. 

Weitere Informationen finden Sie unter [planen die Verwendung von vRSS](vrss-plan.md).

## <a name="enable-vrss-on-a-vm"></a>Aktivieren Sie vRSS auf einem virtuellen Computer
 
Verwenden Sie die folgenden Verfahren, um vRSS zu aktivieren, indem Sie mithilfe von Windows PowerShell oder Geräte-Manager.

-   Geräte-Manager
-   Windows PowerShell
  
### <a name="device-manager"></a>Geräte-Manager

Sie können dieses Verfahren verwenden, so aktivieren Sie vRSS mit Geräte-Manager.

>[!NOTE]
>Der erste Schritt in diesem Verfahren bezieht sich auf virtuelle Computer, auf denen Windows 10 oder Windows Server 2016 ausgeführt werden. Wenn Ihr virtueller Computer ein anderes Betriebssystem ausgeführt wird, können Sie die Geräte-Manager öffnen, vom ersten Systemsteuerung öffnen, klicken Sie dann suchen, und öffnen die Geräte-Manager.
  
1.  Auf der VM-Taskleiste im **hier Suchtext eingeben**, Typ **Gerät**. 

2.  Klicken Sie in den Suchergebnissen auf **-Geräte-Manager**.

3.  Erweitern im Geräte-Manager klicken **Netzwerkadapter**. 

4.  Mit der rechten Maustaste in des Netzwerkadapters, die Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.<p>Der Netzwerkadapter **Eigenschaften** Dialogfeld wird geöffnet.

5.  Im Netzwerkadapter **Eigenschaften**, klicken Sie auf die **erweitert** Registerkarte. 

6.  In **Eigenschaft**, scrollen Sie zu, und klicken Sie auf **empfangsseitige Skalierung**. 

7.  Stellen Sie sicher, dass die Auswahl im **Wert** ist **aktiviert**. 

8.  Klicken Sie auf **OK**.
  
> [!NOTE]
> Auf der **erweitert** Registerkarte zeigen einige Netzwerkadapter auch die Anzahl der RSS-Warteschlangen, die vom Adapter unterstützt werden.

---

### <a name="windows-powershell"></a>Windows PowerShell

Verwenden Sie das folgende Verfahren, um vRSS zu aktivieren, indem Sie mithilfe von Windows PowerShell.

1. Öffnen Sie auf der virtuellen Maschine **Windows PowerShell**.

2. Geben Sie den folgenden Befehl aus, um sicherzustellen, dass Sie ersetzen die *AdapterName* Wert für die **-Namen** Parameter mit dem Namen des Netzwerkadapters, die Sie konfigurieren möchten, und dann die EINGABETASTE drücken. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >Alternativ können Sie den folgenden Befehl aus, aktivieren Sie vRSS.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md).

---