---
title: Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter
description: In diesem Thema erfahren Sie, wie vRSS in Windows Server mithilfe von Geräte-Manager oder Windows PowerShell aktivieren.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133416"
---
# Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Virtuelle RSS-\(vRSS\) erfordert Warteschlange des virtuellen Computers \(VMQ\) aus dem physischen Adapter unterstützen. Wenn VMQ deaktiviert oder wird nicht unterstützt wird Virtual Receive-Side scaling deaktiviert. 

Weitere Informationen finden Sie in [die Verwendung von vRSS planen](vrss-plan.md).

## VRSS auf einem virtuellen Computer aktivieren
 
Gehen Sie folgendermaßen vor, um vRSS mithilfe von Windows PowerShell oder Geräte-Manager zu aktivieren.

-   Geräte-Manager,
-   Windows PowerShell
  
### Geräte-Manager,

Sie können dieses Verfahren verwenden, vRSS mithilfe von Geräte-Manager zu aktivieren.

>[!NOTE]
>Der erste Schritt in diesem Verfahren ist spezifisch für virtuelle Computer, auf denen Windows 10 oder Windows Server 2016 ausgeführt werden. Wenn Ihre virtuellen Computer ein anderes Betriebssystem ausgeführt wird, können Sie Geräte-Manager öffnen, indem zuerst Systemsteuerung, dann suchen öffnen und Geräte-Manager.
  
1.  Geben Sie auf der Taskleiste VM im **Typ hier suchen**, **Gerät**ein. 

2.  Klicken Sie in den Suchergebnissen auf **Geräte-Manager**.

3.  Klicken Sie im Geräte-Manager auf, um **Netzwerkadapter**zu erweitern. 

4.  Mit der rechten Maustaste in des Netzwerkadapters, die, den Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.<p>Das Dialogfeld Netzwerkadapter **Eigenschaften** wird geöffnet.

5.  Klicken Sie im Netzwerkadapter **Eigenschaften**auf der Registerkarte " **Erweitert** ". 

6.  In- **Eigenschaft**einen Bildlauf nach unten zu, und klicken Sie auf **Receive Side scaling**. 

7.  Stellen Sie sicher, dass die Auswahl im **Wert** **aktiviert**ist. 

8.  Klicken Sie auf **OK**.
  
> [!NOTE]
> Auf der Registerkarte " **Erweitert** " anzeigen einige Netzwerkadapter auch die Anzahl der RSS-Warteschlangen, die vom Adapter unterstützt werden.

---

### Windows PowerShell

Gehen Sie folgendermaßen vor, um vRSS zu aktivieren, indem Sie mithilfe von Windows PowerShell.

1. Öffnen Sie **Windows PowerShell**, auf dem virtuellen Computer.

2. Geben Sie folgenden Befehl ein, um sicherzustellen, dass Sie den Wert des *AdapterName* für Ersetzen der **-Namen** Parameter mit dem Namen des Netzwerkadapters, die Sie konfigurieren möchten, und drücken dann die EINGABETASTE. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >Alternativ können Sie den folgenden Befehl verwenden, um vRSS zu aktivieren.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

Weitere Informationen finden Sie unter [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md).

---