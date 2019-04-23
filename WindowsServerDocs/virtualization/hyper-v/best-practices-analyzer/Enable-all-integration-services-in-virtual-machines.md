---
title: Aktivieren Sie alle Integrationsdienste auf virtuellen Computern
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 16e202ad-3795-40c9-8176-7ca319e56d26
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 307e2d407a0defa14a6b57bda95a2f3ab018406d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829431"
---
# <a name="enable-all-integration-services-in-virtual-machines"></a>Aktivieren Sie alle Integrationsdienste auf virtuellen Computern

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
  
*Eine oder mehrere Integrationsdienste sind deaktiviert "oder" funktioniert nicht auf einem virtuellen Computer.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Der Dienst oder eine Integration-Funktion kann für die folgenden virtuellen Computer nicht ordnungsgemäß funktioniert:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie das Dienste-Snap-in "oder" sc Config Befehlszeilentool, um sicherzustellen, dass der Dienst für den automatischen start konfiguriert und nicht beendet ist wird.*  
  
#### <a name="to-configure-how-a-service-is-started-using-the-services-snap-in"></a>So konfigurieren wie ein Dienst gestartet wird, verwenden das Dienste-Snap-in  
  
1.  Verwenden Sie Remote Desktop Services oder die Verbindung mit virtuellen Computern für die Verbindung des virtuellen Computers und das Protokoll auf das Gastbetriebssystem an.  
  
2.  Öffnen Sie Dienste. (Klicken Sie auf **starten**, klicken Sie in der **Suche starten** geben **"Services.msc"**, und drücken Sie dann die EINGABETASTE.)  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Dienst, den Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **allgemeine** Registerkarte **Start** , klicken Sie auf **automatische**.  
  
#### <a name="to-configure-how-a-service-is-started-using-sc-config"></a>So konfigurieren wie ein Dienst gestartet wird, mithilfe des SC Config  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Ersetzen Sie < Service-Name > durch den Namen des Diensts, und geben Sie dann:  
  
    ```  
    sc config <service-name> start=auto  
    ```  
  


