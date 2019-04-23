---
title: Planen des Hyper-V-Netzwerks in Windows Server
description: Beschreibt, was für grundlegende Netzwerke in Hyper-V ist erforderlich und enthält Links zu Anweisungen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 83c014b917566a78796d061dd88962966ec0c9ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829871"
---
# <a name="plan-for-hyper-v-networking-in-windows-server"></a>Planen des Hyper-V-Netzwerks in Windows Server

>Gilt für: Microsoft Hyper-V Server 2016, WindowsServer 2016 wird Microsoft Hyper-V-Server 2019, WindowsServer 2019
  
Ein grundlegendes Verständnis der Netzwerke in Hyper-V können Sie Netzwerke für virtuelle Maschinen zu planen. Dieser Artikel behandelt auch einige Netzwerkaspekte bei Verwendung von live-Migration, und wenn Sie Hyper-V mit anderen Serverfeatures und-Rollen verwenden.  
  
## <a name="hyper-v-networking-basics"></a>Hyper-V-networking-Grundlagen  
Grundlegende Netzwerke in Hyper-V ist recht einfach. Er verwendet zwei Teilen: einem virtuellen Switch und einen virtuellen Netzwerkadapter. Sie benötigen mindestens eine der einzelnen auf Netzwerkbetrieb für einen virtuellen Computer herzustellen. Der virtuelle Switch stellt eine Verbindung mit einem Ethernet-basierten Netzwerk her. Der virtuelle Netzwerkadapter eine Verbindung mit einem Port auf dem virtuellen Switch an, der für einen virtuellen Computer mit einem Netzwerk ermöglicht.  
  
Einen virtuellen Switch zu erstellen, bei der Installation von Hyper-V ist die einfachste Möglichkeit, grundlegende Netzwerke herstellen werden. Wenn Sie einen virtuellen Computer erstellen, können Sie es dann mit dem Switch verbinden. Herstellen einer Verbindung mit dem Switch automatisch Fügt einen virtuellen Netzwerkadapter mit dem virtuellen Computer. Anweisungen hierzu finden Sie unter [erstellen Sie einen virtuellen Switch für Hyper-V-Maschinen](../get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md).  
  
Um verschiedene Arten von Netzwerken zu behandeln, können Sie virtuelle Switches und virtuelle Netzwerkadapter hinzufügen. Alle Switches sind Teil der Hyper-V-Hosts, jedoch nur einen virtuellen Computer jeden virtuellen Netzwerkadapter gehört.  
  
Der virtuelle Switch ist es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch. Es verfügt über integrierte Funktionen für Überwachung, Steuerung, und Blöcke Datenverkehr sowie Sicherheit und -Diagnose.  Sie können den Satz von integrierten Funktionen hinzugefügt, durch die Installation von-Plug-ins, so genannte *Erweiterungen*. Diese werden von unabhängigen Softwareanbietern. Weitere Informationen über die Switches und Erweiterungen finden Sie unter [virtuellen Hyper-V-Switch](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
### <a name="switch-and-network-adapter-choices"></a>Die Auswahl der Switch und Netzwerk-adapter  
Hyper-V bietet drei Typen von virtuellen Switches und zwei Arten von virtuellen Netzwerkadaptern. Wählen Sie dazu die jeweils eine, die bei der Erstellung werden sollen. Sie können Hyper-V-Manager oder Hyper-V-Modul für Windows PowerShell verwenden, erstellen und Verwalten von virtuellen Switches und virtuelle Netzwerkadapter. Einige Erweiterte Netzwerkfunktionen, können wie z. B. erweiterte Port-Access Control lists, (ACLs), nur verwaltet werden mithilfe von Cmdlets im Hyper-V-Modul.  
  
Sie können auf einem virtuellen Switch oder virtuellen Netzwerkadapter für einige Änderungen vornehmen, nach Abschluss des Erstellungsvorgangs. Angenommen, es ist möglich, einen vorhandenen Switch in einen anderen Typ zu ändern, aber dies wirkt sich auf die Netzwerkfunktionen von allen virtuellen Computern mit dem Switch verbunden.  Also, Sie wahrscheinlich nicht dazu, es sei denn, Sie ein Fehler unterlaufen oder etwas getestet werden müssen. Ein weiteres Beispiel können Sie einen virtuellen Netzwerkadapter mit einem anderen Switch verbinden, beispielsweise wenn Sie eine Verbindung mit einem anderen Netzwerk herstellen möchten. Allerdings können Sie einen virtuellen Netzwerkadapter von einem Typ zu einer anderen ändern. Anstatt den Typ ändern, Sie fügen Sie einen anderen Netzwerkadapter hinzu und wählen Sie den entsprechenden Typ.  
  
Virtuelle Switchtypen lauten:  
  
-   **Externer virtueller Switch** -mit einem verkabelten, physischen Netzwerk durch Bindung an einen physischen Netzwerkadapter verbunden.  
  
-   **Interner virtueller Switch** -Verbindung mit einem Netzwerk, das nur von den virtuellen Computern, auf dem Host, die den virtuellen Switch, und zwischen dem Host und die virtuellen Computer verwendet werden kann.  
  
-   **Privater virtueller Switch** -Verbindung mit einem Netzwerk, das verwendet werden kann, nur durch die virtuellen Computer, auf dem Host, die den virtuellen Switch, aber keine Netzwerkverbindung zwischen dem Host und die virtuellen Computer bereitzustellen.  
  
Virtuelle Netzwerkadaptertypen sind:  
  
-   **Bestimmten Hyper-V-Netzwerkadapter** – für die Generation 1 und virtuelle Maschinen der Generation 2 verfügbar. Es wurde speziell für Hyper-V und erfordert einen Treiber, der in Hyper-V-Integrationsdiensten enthalten ist. Diese Art von Netzwerkadapter schneller und ist die empfohlene Option aus, es sei denn, Sie im Netzwerk gestartet müssen oder ein nicht unterstütztes Gastbetriebssystem ausgeführt werden. Die erforderliche Treiber wird nur für unterstützte Gastbetriebssysteme bereitgestellt. Beachten Sie, dass in Hyper-V-Manager und die Netzwerk-Cmdlets, die dieser Typ wird nur als einem Netzwerkadapter bezeichnet.  
  
-   **Ältere Netzwerkkarte** – nur für virtuelle Maschinen der Generation 1 verfügbar. Emuliert ein Intel 21140-basierter PCI Fast Ethernet-Adapter und kann verwendet werden, also mit einem Netzwerk starten können Sie ein Betriebssystem von einem Dienst wie z. B. Windows-Bereitstellungsdienste installieren.  
  
## <a name="hyper-v-networking-and-related-technologies"></a>Hyper-V-Netzwerke und verwandte Technologien  
Aktuelle Windows Server-Versionen, Verbesserungen, mit denen Sie weitere Optionen zum Konfigurieren des Netzwerks für Hyper-V eingeführt. Zum Beispiel: Windows Server 2012 führte die Unterstützung für Netzwerke konvergiert. Dadurch können Sie Weiterleiten von Netzwerkdatenverkehr über einen externen virtuellen Switch. Windows Server 2016 baut auf diesem-Konfigurationsrichtlinien (Remote Direct Memory Access, RDMA) auf den Netzwerkadaptern, die mit einem virtuellen Hyper-V-Switch gebunden. Sie können diese Konfiguration verwenden, entweder mit oder ohne Switch Embedded Teaming (SET). Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;festlegen&#41;](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
Einige Features basieren auf bestimmten Netzwerkkonfigurationen oder erschaffen Sie besser bei bestimmten Konfigurationen. Betrachten Sie diese Option beim Planen oder Aktualisieren Ihrer Netzwerkinfrastruktur.  
  
**Failover-Clusterunterstützung** – es ist eine bewährte Methode, die Clusterdatenverkehr zu isolieren, und Verwenden von Hyper-V Quality of Service (QoS) auf dem virtuellen Switch. Weitere Informationen finden Sie unter [Netzwerkempfehlungen für einen Hyper-V-Cluster](https://technet.microsoft.com/library/dn550728.aspx)  
  
**Live-Migration** -verwenden Sie die Leistungsoptionen, um zu reduzieren, Netzwerk- und CPU-Auslastung und die Zeit zum Abschluss einer Livemigration bis. Anweisungen hierzu finden Sie unter [Einrichten von Hosts für die Livemigration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md).  
  
**"Direkte Speicherplätze"** – diese Funktion basiert auf der SMB3.0-Netzwerkprotokoll und RDMA. Weitere Informationen finden Sie unter ["direkte Speicherplätze" in Windows Server 2016](../../../storage/storage-spaces/storage-spaces-direct-overview.md).