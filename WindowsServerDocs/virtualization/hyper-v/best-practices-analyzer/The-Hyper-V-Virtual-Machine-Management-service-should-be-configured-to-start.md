---
title: Der Hyper-V Virtual Machine Management-Dienst sollte für den automatischen start konfiguriert werden
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 222bbe76-c514-4a3f-b61b-860a4dc2826a
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c33f81678d7fdc71e81834a002fd3d7917a6f632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833251"
---
# <a name="the-hyper-v-virtual-machine-management-service-should-be-configured-to-start-automatically"></a>Der Hyper-V Virtual Machine Management-Dienst sollte für den automatischen start konfiguriert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Die Hyper-V Virtual Machine Management-Dienst ist nicht für den automatischen start konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer können nicht verwaltet werden, bis der Dienst gestartet wurde.*  
  
Virtuelle Computer, die ausgeführt werden wird weiterhin ausgeführt. Allerdings ist Sie nicht Verwalten von virtuellen Computern, oder erstellen oder löschen sie, bis der Dienst ausgeführt wird.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie das Dienste-Snap-in "oder" sc Config Befehlszeilentool, um den Dienst für den automatischen start konfigurieren.*  
  
> [!TIP]  
> Wenn Sie nicht den Dienst in der desktop-app finden oder das Befehlszeilentool "" gibt an, dass der Dienst ist nicht vorhanden, die Hyper-V-Verwaltungstools wahrscheinlich nicht installiert. So installieren Sie sie:  
>   
> - Öffnen Sie in Windows Server Server-Manager, und verwenden Sie des Assistenten zum Hinzufügen von Rollen und Features. Weitere Informationen finden Sie unter [Installieren der Hyper-V-Rolle unter Windows Server 2016](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).  
> - Auf Windows, auf dem Desktop mit der Eingabe beginnen **Programme**, klicken Sie auf **Programme und Funktionen** (Systemsteuerung) > **Aktivieren von Windows-Funktionen ein- oder ausschalten**  >   **Hyper-V** > **Hyper-V-Verwaltungstools**. Klicken Sie dann auf **OK**.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>Um den Dienst zum Einstieg in die Dienste-desktop-app automatisch neu zu konfigurieren.  
  
1.  Öffnen Sie die Dienste-desktop-app. (Klicken Sie auf **starten**, klicken Sie in das Suchfeld, mit der Eingabe beginnen **Services**, und klicken Sie auf Dienste in der Liste der Ergebnisse.  
  
2.  Klicken Sie im Detailbereich mit der Maustaste **Hyper-V Virtual Machine Management**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Registerkarte **Start** , klicken Sie auf **automatische**.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-sc-config-command"></a>So konfigurieren Sie den Dienst starten, automatisch mit dem Befehl "SC Config", um neu  
  
1.  Öffnen Sie Windows PowerShell.  
  
2.  Typ:  
  
    ```  
    set-service  vmms -startuptype automatic  
    ```  
  
3.  Wenn der Dienst bereits ausgeführt wird, geben Sie ein:  
  
    ```  
    start-service -name vmms  
    ```  
  


