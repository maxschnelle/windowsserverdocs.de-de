---
title: Speichercontroller sollte auf virtuellen Computern aktiviert werden, um Zugriff auf den angefügten Speicher bereitzustellen.
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 532548a1-8ffe-4b5b-902e-ed2f0819012b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 42803a0eef84bf006e9f9e7ed6297ea21b4eb7b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849161"
---
# <a name="storage-controllers-should-be-enabled-in-virtual-machines-to-provide-access-to-attached-storage"></a>Speichercontroller sollte auf virtuellen Computern aktiviert werden, um Zugriff auf den angefügten Speicher bereitzustellen.

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
  
*Eine oder mehrere Speichercontroller möglicherweise auf einem virtuellen Computer deaktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer kann nicht mit einem deaktivierten Speichercontroller verbundenen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Geräte-Manager im Gastbetriebssystem, um alle Speichercontroller zu aktivieren. Wenn der Speichercontroller nicht erforderlich ist, verwenden Sie Hyper-V-Manager, um es aus dem virtuellen Computer zu entfernen.*  
  
Anweisungen dazu, wie Sie die Geräte-Manager verwenden finden Sie Hilfe im Gastbetriebssystem. Anweisungen dazu, wie Sie den Storage-Controller zu entfernen finden Sie im folgende Verfahren.  
  
#### <a name="to-remove-a-scsi-storage-controller-from-the-virtual-machine"></a>So entfernen Sie einen SCSI-Controller-Speicher des virtuellen Computers  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den virtuellen Computer, die Sie konfigurieren möchten.  
  
3.  Wenn der virtuelle Computer ausgeführt wird, müssen Sie den virtuellen Computer heruntergefahren. Mit der rechten Maustaste den virtuellen Computer aus, und klicken Sie auf **Herunterfahren**.  
  
4.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
5.  Klicken Sie im linken Bereich die **Einstellungen** Dialogfeld **Hardware**, klicken Sie auf **SCSI-Controller**.  
  
6.  Klicken Sie im rechten Bereich auf **entfernen**.  
  


