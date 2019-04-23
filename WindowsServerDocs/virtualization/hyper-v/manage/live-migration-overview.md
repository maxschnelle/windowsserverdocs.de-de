---
title: Übersicht über die Livemigration
description: Überblick über live-Migration-Funktionalität in Windows Server 2016.
ms.prod: windows-server-threshold
ms.service: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: 2bbe897ffb8b200a72fac5a662e518d4a4be1131
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887851"
---
# <a name="live-migration-overview"></a>Übersicht über die Livemigration

Livemigration ist ein Hyper-V-Feature in Windows Server.  Sie können ausgeführte virtuelle Computer von einem Hyper-V-Host auf einen anderen ohne wahrnehmbare Ausfallzeit transparent zu verschieben.  Der Hauptvorteil der Livemigration ist Flexibilität. ausgeführte virtuelle Computer sind nicht auf einem einzelnen Hostcomputer gebunden.  Dadurch können Aktionen wie das leeren eines bestimmten Hosts virtueller Computer vor der Außerbetriebnahme oder diese zu aktualisieren.  In Kombination mit Windows-Failoverclustering ermöglicht die Livemigration die Erstellung von hoher Verfügbarkeit und Fehlertoleranz fehlertolerante Systemen. 

## <a name="related-technologies-and-documentation"></a>Verwandte Technologien und Dokumentation

Live-Migration wird häufig in Verbindung mit einigen verwandten Technologien wie Failoverclustering und System Center Virtual Machine Manager verwendet.  Wenn Sie Live Migration über diese Technologien nutzen, sind hier Zeiger auf die neueste Dokumentation:
* [Failover-Clusterunterstützung](../../../failover-clustering/failover-clustering-overview.md) (WindowsServer 2016) 
* [System Center Virtual Machine Manager-](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

Wenn Sie ältere Versionen von Windows Server verwenden, oder benötigen Details zu Features, die in älteren Versionen von Windows Server eingeführt wurden, sind hier Verweise auf historische Dokumentation: 
* [Live-Migration](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx) (Windows Server 2008 R2)  
* [Live-Migration](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx) (Windows Server 2012 R2) 
* [Failover-Clusterunterstützung](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx) (Windows Server 2012 R2)
* [Failover-Clusterunterstützung](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx) (Windows Server 2008 R2)
* [System Center Virtual Machine Manager-](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager-](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Livemigration unter WindowsServer 2016

In Windows Server 2016 sind weniger Einschränkungen bei der Bereitstellung von live-Migration.  Dies funktioniert nun ohne Failoverclustering.  Andere Funktionen bleibt unverändert aus früheren Versionen von Live Migration.  Weitere Informationen zum Konfigurieren und Verwenden der Livemigration ohne Failoverclustering: 
* [Einrichten von Hosts für die Livemigration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [Verwenden der Livemigration ohne Failoverclustering zum Verschieben eines virtuellen Computers](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)