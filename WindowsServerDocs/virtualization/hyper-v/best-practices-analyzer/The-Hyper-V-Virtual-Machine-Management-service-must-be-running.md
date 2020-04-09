---
title: Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss ausgeführt werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f44d6887-6458-4438-9d93-574587e3f7d1
author: kbdazure
ms.date: 10/03/2016
ms.openlocfilehash: 50f101f9dad824e13fa5827175cc1c944a96a91b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859323"
---
# <a name="the-hyper-v-virtual-machine-management-service-must-be-running"></a>Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss ausgeführt werden.

>Gilt für: Windows Server 2016
  
Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Erforderliche Komponenten|  

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Der zum Verwalten virtueller Maschinen erforderliche Dienst wird nicht ausgeführt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Es können keine Virtual Machine Management-Vorgänge ausgeführt werden.*  
  
Virtuelle Computer, auf denen ausgeführt wird, werden weiterhin ausgeführt. Es ist jedoch nicht möglich, virtuelle Computer zu verwalten oder zu erstellen oder zu löschen, bis der Dienst ausgeführt wird.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie das Snap-in "Dienste" oder das Befehlszeilen Tool "SC config", um den Dienst für den automatischen Start neu zu konfigurieren.*  
  
> [!TIP]  
> Wenn Sie den Dienst nicht in der Desktop-App finden oder das Befehlszeilen Tool meldet, dass der Dienst nicht vorhanden ist, sind die Hyper-V-Verwaltungs Tools wahrscheinlich nicht installiert. Wenn Sie die Hyper-v-MMC-Konsole nicht über das Startmenü anzeigen können, müssen Sie die Hyper-v-Verwaltungs Tools installieren.

So installieren Sie die Hyper-V-Verwaltungs Tools:  
>   
> - Öffnen Sie unter Windows Server Server-Manager, und verwenden Sie den Assistenten zum Hinzufügen von Rollen und Features. Weitere Informationen finden Sie unter [Installieren der Hyper-V-Rolle auf Windows Server 2016](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).  Sie können auch PowerShell verwenden, um die Tools zu installieren (`Install-WindowsFeature -Name Hyper-V-Tools, Hyper-V-PowerShell`). 
> - Starten Sie unter Windows auf dem Desktop die Eingabe **Programme**, klicken Sie auf **Programme und Funktionen** (Systemsteuerung), > Windows-Features > **Hyper-v** - > **Hyper-v-Verwaltungs Tools**ein- **oder ausschalten** . Klicken Sie dann auf **OK**.  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>So konfigurieren Sie den Dienst für den automatischen Start mithilfe der Desktop-App für Dienste neu  
  
1.  Öffnen Sie die Desktop-App für Dienste. (Klicken Sie auf **Start**, klicken Sie in das Feld **Suche starten** , geben Sie **Services. msc**ein, und drücken Sie dann die EINGABETASTE.)  
  
2.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **Hyper-V-Verwaltung virtueller Computer**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Registerkarte **Allgemein** unter **Starttyp** auf **automatisch**.  
  
4.  Klicken Sie auf **Start**, um den Dienst zu starten.  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-sc-config"></a>So konfigurieren Sie den Dienst so neu, dass er automatisch mit SC config gestartet wird  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Um den Dienst neu zu konfigurieren, geben Sie Folgendes ein:  
  
    ```  
    sc config vmms start=auto  
    ```  
  
4.  Geben Sie Folgendes ein, um den Dienst zu starten:  
  
    ```  
    sc start vmms  
    ```  
  
Wenn der Dienst bereits für den automatischen Start konfiguriert ist und Sie lediglich den Dienst neu starten müssen, können Sie dies über den Hyper-V-Manager oder über den oben gezeigten Befehl SC Start VMMS durchführen.  
  
#### <a name="to-restart-the-service-from-hyper-v-manager"></a>So starten Sie den Dienst mit dem Hyper-V-Manager neu  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Navigationsbereich auf den Namen des Servers, wenn er nicht bereits ausgewählt ist.  
  
3.  Klicken Sie im **Aktions** Bereich auf **Dienst starten**.  
  


