---
title: Übersicht über die Livemigration
description: Bietet eine Übersicht über die Live Migrations Funktionen in Windows Server 2016.
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: 11fd67f5b4b3c9ce6a8aebe7dac4008f38d0f08e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815173"
---
# <a name="live-migration-overview"></a>Übersicht über die Livemigration

Die Live Migration ist eine Hyper-V-Funktion in Windows Server.  So können Sie die Ausführung Virtual Machines transparent von einem Hyper-V-Host zu einem anderen migrieren, ohne dass Ausfallzeiten auftreten.  Der Hauptvorteil der Live Migration ist die Flexibilität. das Ausführen von Virtual Machines ist nicht an einen einzelnen Host Computer gebunden.  Dies ermöglicht Aktionen wie das Ableiten eines bestimmten Hosts Virtual Machines vor dem Außerbetriebsetzen oder aktualisieren.  In Kombination mit Windows-Failoverclustering ermöglicht die Live Migration die Erstellung von hochverfügbaren und fehlertoleranten Systemen. 

## <a name="related-technologies-and-documentation"></a>Verwandte Technologien und Dokumentationen

Die Live Migration wird häufig in Verbindung mit einigen verwandten Technologien wie Failoverclustering und System Center Virtual Machine Manager verwendet.  Wenn Sie Livemigration über diese Technologien verwenden, finden Sie hier folgende Verweise auf die aktuelle Dokumentation:
* [Failoverclustering](../../../failover-clustering/failover-clustering-overview.md) (Windows Server 2016) 
* [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

Wenn Sie ältere Versionen von Windows Server verwenden oder Details zu den Funktionen benötigen, die in älteren Versionen von Windows Server eingeführt wurden, finden Sie hier Hinweise auf die historische Dokumentation: 
* [Livemigration](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx) (Windows Server 2008 R2)  
* [Livemigration](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx) (Windows Server 2012 R2) 
* [Failoverclustering](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx) (Windows Server 2012 R2)
* [Failoverclustering](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx) (Windows Server 2008 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Livemigration in Windows Server 2016

In Windows Server 2016 gibt es weniger Einschränkungen bei der Bereitstellung von Live Migrationen.  Sie funktioniert nun ohne Failoverclustering.  Andere Funktionen bleiben gegenüber früheren Versionen von Livemigration unverändert.  Weitere Informationen zum Konfigurieren und Verwenden der Live Migration ohne Failoverclustering: 
* [Einrichten von Hosts für die Live Migration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [Verwenden der Live Migration ohne Failoverclustering zum Verschieben einer virtuellen Maschine](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)