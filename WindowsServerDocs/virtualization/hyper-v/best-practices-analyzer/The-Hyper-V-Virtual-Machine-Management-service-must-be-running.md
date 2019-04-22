---
title: Der Hyper-V Virtual Machine Management-Dienst muss ausgeführt werden
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f44d6887-6458-4438-9d93-574587e3f7d1
author: KBDAzure
ms.date: 10/03/2016
ms.openlocfilehash: 58886b68ca30ddeb064fc12c6cb4c00183399715
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826111"
---
# <a name="the-hyper-v-virtual-machine-management-service-must-be-running"></a>Der Hyper-V Virtual Machine Management-Dienst muss ausgeführt werden

>Gilt für: Windows Server 2016
  
Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Vorraussetzungen|  

In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Der Dienst erforderlich, um die Verwaltung virtueller Computer wird nicht ausgeführt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Es können keine Verwaltungsvorgänge für den virtuellen Computer ausgeführt werden.*  
  
Virtuelle Computer, die ausgeführt werden wird weiterhin ausgeführt. Allerdings ist Sie nicht Verwalten von virtuellen Computern, oder erstellen oder löschen sie, bis der Dienst ausgeführt wird.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie die Dienste-Snap-in oder das Befehlszeilentool "Sc Config", um den Serverdienst für automatischen start konfigurieren.*  
  
> [!TIP]  
> Wenn Sie nicht den Dienst in der desktop-app finden oder das Befehlszeilentool "" gibt an, dass der Dienst ist nicht vorhanden, die Hyper-V-Verwaltungstools wahrscheinlich nicht installiert. Und wenn Sie nicht finden in der Hyper-V-MMC-Konsole über das Startmenü zugreifen können, sollten Sie die Hyper-V-Verwaltungstools installieren.

So installieren Sie die Hyper-V-Verwaltungstools  
>   
> - Öffnen Sie in Windows Server Server-Manager, und verwenden Sie des Assistenten zum Hinzufügen von Rollen und Features. Weitere Informationen finden Sie unter [Installieren der Hyper-V-Rolle unter Windows Server 2016](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).  Sie können auch PowerShell verwenden, um die Tools installieren (`Install-WindowsFeature -Name Hyper-V-Tools, Hyper-V-PowerShell`) 
> - Auf Windows, auf dem Desktop mit der Eingabe beginnen **Programme**, klicken Sie auf **Programme und Funktionen** (Systemsteuerung) > **Aktivieren von Windows-Funktionen ein- oder ausschalten**  >   **Hyper-V** > **Hyper-V-Verwaltungstools**. Klicken Sie dann auf **OK**.  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>Um den Dienst zum Einstieg in die Dienste-desktop-app automatisch neu zu konfigurieren.  
  
1.  Öffnen Sie die Dienste-desktop-app. (Klicken Sie auf **starten**, klicken Sie in der **Suche starten** geben **"Services.msc"**, und drücken Sie dann die EINGABETASTE.)  
  
2.  Klicken Sie im Detailbereich mit der Maustaste **Hyper-V Virtual Machine Management**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Registerkarte **Start** , klicken Sie auf **automatische**.  
  
4.  Um den Dienst zu starten, klicken Sie auf **starten**.  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-sc-config"></a>Den Dienst zum Einstieg in SC Config automatisch neu konfigurieren.  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Geben Sie Folgendes ein, um den Dienst neu zu konfigurieren:  
  
    ```  
    sc config vmms start=auto  
    ```  
  
4.  Um den Dienst zu starten, geben Sie Folgendes ein:  
  
    ```  
    sc start vmms  
    ```  
  
Wenn der Dienst bereits für den automatischen start konfiguriert ist, Sie nur den Dienst neu starten müssen möglich, die von Hyper-V-Manager oder von der zuvor gezeigten Befehl "sc start Vmms".  
  
#### <a name="to-restart-the-service-from-hyper-v-manager"></a>Die von Hyper-V-Manager-Dienst neu starten  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Navigationsbereich auf den Namen des Servers, wenn es nicht bereits ausgewählt ist.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf **Dienst starten**.  
  


