---
title: Reservieren Sie eine oder mehrere externe virtuelle Netzwerke für die ausschließliche Verwendung von virtuellen Computern
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f7732258-93f1-44e8-835b-5ad2d1c45cd9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c8c90a74352bae0b348608db0fc05107e4d09010
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884741"
---
# <a name="reserve-one-or-more-external-virtual-networks-for-exclusive-use-by-virtual-machines"></a>Reservieren Sie eine oder mehrere externe virtuelle Netzwerke für die ausschließliche Verwendung von virtuellen Computern

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Alle externen virtuellen Netzwerke werden für die Verwendung durch das Verwaltungsbetriebssystem und die virtuellen Computer konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Netzwerkleistung kann im Verwaltungsbetriebssystem beeinträchtigt.*  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Manager für virtuelle Switches, um ein externes virtuelles Netzwerk für das Verwaltungsbetriebssystem freigeben zu beenden.*  
  
#### <a name="to-stop-sharing-the-external-virtual-network-with-the-management-operating-system"></a>Zum Beenden des externen virtuellen Netzwerks für das Verwaltungsbetriebssystem freigeben  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Menü **Aktionen** auf **Manager für virtuelle Switches**.  
  
3.  Klicken Sie unter **virtuelle Switches**, klicken Sie auf den Namen des externen virtuellen Switches an.  
  
4.  In der **Verbindungstyp** deaktivieren Sie im Bereich unter dem Namen des physischen Netzwerkadapters, der **ermöglichen das Verwaltungsbetriebssystem gemeinsames Verwenden dieses Netzwerkadapters** Kontrollkästchen.  
  
5.  Klicken Sie auf **OK**.  
  


