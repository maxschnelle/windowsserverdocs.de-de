---
title: Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss für den automatischen Start konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 222bbe76-c514-4a3f-b61b-860a4dc2826a
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 26122d40b3fbdbdc40a94801d5e3ff8fcf4fa646
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859313"
---
# <a name="the-hyper-v-virtual-machine-management-service-should-be-configured-to-start-automatically"></a>Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss für den automatischen Start konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Der Hyper-V-Verwaltungsdienst für virtuelle Computer ist nicht für den automatischen Start konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer können erst verwaltet werden, nachdem der Dienst gestartet wurde.*  
  
Virtuelle Computer, auf denen ausgeführt wird, werden weiterhin ausgeführt. Es ist jedoch nicht möglich, virtuelle Computer zu verwalten oder zu erstellen oder zu löschen, bis der Dienst ausgeführt wird.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie das Snap-in "Dienste" oder das Befehlszeilen Tool "SC config", um den Dienst für den automatischen Start neu zu konfigurieren.*  
  
> [!TIP]  
> Wenn Sie den Dienst nicht in der Desktop-App finden oder das Befehlszeilen Tool meldet, dass der Dienst nicht vorhanden ist, sind die Hyper-V-Verwaltungs Tools wahrscheinlich nicht installiert. So installieren Sie Sie:  
>   
> - Öffnen Sie unter Windows Server Server-Manager, und verwenden Sie den Assistenten zum Hinzufügen von Rollen und Features. Weitere Informationen finden Sie unter [Installieren der Hyper-V-Rolle auf Windows Server 2016](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).  
> - Starten Sie unter Windows auf dem Desktop die Eingabe **Programme**, klicken Sie auf **Programme und Funktionen** (Systemsteuerung), > Windows-Features > **Hyper-v** - > **Hyper-v-Verwaltungs Tools**ein- **oder ausschalten** . Klicken Sie dann auf **OK**.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>So konfigurieren Sie den Dienst für den automatischen Start mithilfe der Desktop-App für Dienste neu  
  
1.  Öffnen Sie die Desktop-App für Dienste. (Klicken Sie auf **Start**, klicken Sie in das Suchfeld, geben Sie **Dienste**ein, und klicken Sie dann auf Dienste in der Ergebnisliste.  
  
2.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **Hyper-V-Verwaltung virtueller Computer**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Registerkarte **Allgemein** unter **Starttyp** auf **automatisch**.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-sc-config-command"></a>So konfigurieren Sie den Dienst so neu, dass er automatisch mit dem Befehl sc config gestartet wird  
  
1.  Öffnen Sie Windows PowerShell.  
  
2.  Typ:  
  
    ```  
    set-service  vmms -startuptype automatic  
    ```  
  
3.  Wenn der Dienst nicht bereits ausgeführt wird, geben Sie Folgendes ein:  
  
    ```  
    start-service -name vmms  
    ```  
  


