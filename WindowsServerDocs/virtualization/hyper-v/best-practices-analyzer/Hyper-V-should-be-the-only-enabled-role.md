---
title: Hyper-V sollte die einzige aktivierte Rolle sein.
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5a0ed176-048f-40b1-b56c-8391b805fd37
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bd03554396696a43b4821aff0f4ed893933484c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886461"
---
# <a name="hyper-v-should-be-the-only-enabled-role"></a>Hyper-V sollte die einzige aktivierte Rolle sein.

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
  
*Rollen, ausgenommen Hyper-V sind auf diesem Server aktiviert.*  
  
In den meisten Fällen ist es nicht über eine gute Idee, andere Rollen auf einem Server mit Hyper-V-Rolle installieren. Remote Remotedesktop-Virtualisierungshost-Rollendienst ist eine Ausnahme aus, da sie Teil der Rolle "Remotedesktopdienste ist" und Hyper-V auf dem gleichen Server installiert werden muss.  
  
## <a name="impact"></a>Auswirkungen  
  
*Hyper-V-Rolle sollte die einzige Rolle auf einem Server aktiviert sein.*  
  
Dieser bewährten Methode können Sie das Hostbetriebssystem keine Rollen, Features und Anwendungen, die Hyper-V ausführen, nicht erforderlich. Durch Befolgen dieser bewährten Methode und die Ausführung von Hyper-V auf Nano Server reduziert die Anzahl der Updates, die Sie benötigen, da nur die Nano Server, die Hyper-V-Dienstkomponenten und der Windows-Hypervisor unterliegen Softwareupdates wäre.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Server-Manager, um alle Serverrollen außer Hyper-V zu entfernen.*  
  
Server-Manager enthält den Assistenten zum Entfernen von Rollen. Mit diesem Assistenten können Sie mehrere Rollen gleichzeitig zu entfernen. Vor dem Entfernen von Rollen, überprüft den Assistenten zum Entfernen von Rollen für Abhängigkeiten, um das Risiko des Entfernens der Software, die anderen Rollen abhängig. Wenn Abhängigkeiten gefunden werden, fordert der Assistent Sie so genehmigen Sie das Entfernen von anderen Rollen, Rollendienste oder Software, die von den installierten Rollen benötigt.   
  
Um Server-Manager zu verwenden, müssen Sie auf den Computer als Administrator angemeldet sein.  
  
#### <a name="to-remove-a-role"></a>So entfernen Sie eine Rolle  
  
1.  Öffnen Sie Server-Manager mithilfe von Tastenkombinationen auf der **starten** im Menü auf der Windows-Taskleiste oder in der Verwaltung.  
2.   In der **Rollenübersicht** Bereich des Server-Manager-Hauptfensters, klicken Sie auf **Entfernen von Rollen**. Führen Sie die Anweisungen im Assistenten, um die Rolle zu entfernen.   
  
  
  


