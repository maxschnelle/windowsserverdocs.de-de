---
title: Planen der Hyper-V-Netzwerke in Windows Server
description: Hier wird beschrieben, was für grundlegende Netzwerke in Hyper-V erforderlich ist, und enthält Links zu Anweisungen.
manager: dongill
ms.topic: article
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: b31d942e8d7890a8f699f743bcd24953d2a3e760
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996072"
---
# <a name="plan-for-hyper-v-networking-in-windows-server"></a>Planen der Hyper-V-Netzwerke in Windows Server

>Gilt für: Microsoft Hyper-V Server 2016, Windows Server 2016, Microsoft Hyper-V Server 2019, Windows Server 2019

Ein grundlegendes Verständnis von Netzwerken in Hyper-V hilft Ihnen beim Planen von Netzwerken für virtuelle Computer. Außerdem werden in diesem Artikel einige Netzwerk Aspekte bei der Verwendung der Live Migration und bei Verwendung von Hyper-V mit anderen Serverfunktionen und-Rollen behandelt.

## <a name="hyper-v-networking-basics"></a>Grundlagen zum Hyper-V-Netzwerk
Grundlegende Netzwerke in Hyper-V sind recht einfach. Es verwendet zwei Teile: einen virtuellen Switch und einen virtuellen Netzwerkadapter. Sie benötigen mindestens eine von jedem, um Netzwerke für einen virtuellen Computer einzurichten. Der virtuelle Switch stellt eine Verbindung mit einem beliebigen Ethernet-basierten Netzwerk her. Der virtuelle Netzwerkadapter stellt eine Verbindung mit einem Port auf dem virtuellen Switch her, sodass ein virtueller Computer ein Netzwerk verwenden kann.

Die einfachste Möglichkeit zum Einrichten von grundlegenden Netzwerken besteht darin, einen virtuellen Switch zu erstellen, wenn Sie Hyper-V installieren. Wenn Sie dann einen virtuellen Computer erstellen, können Sie ihn mit dem Switch verbinden. Beim Herstellen einer Verbindung mit dem Switch wird dem virtuellen Computer automatisch ein virtueller Netzwerkadapter hinzugefügt. Anweisungen hierzu finden Sie unter [Erstellen eines virtuellen Switches für virtuelle Hyper-V-](../get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)Computer.

Um unterschiedliche Netzwerktypen zu verarbeiten, können Sie virtuelle Switches und virtuelle Netzwerkadapter hinzufügen. Alle Switches sind Teil des Hyper-V-Hosts, aber jeder virtuelle Netzwerkadapter gehört nur einem virtuellen Computer an.

Bei dem virtuellen Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerk Switch. Es bietet integrierte Funktionen zum überwachen, Steuern und Segmentieren von Datenverkehr sowie zur Sicherheit und Diagnose.  Sie können dem Satz integrierter Funktionen hinzufügen, indem Sie Plug-ins installieren, die auch als *Erweiterungen*bezeichnet werden. Diese sind für unabhängige Softwarehersteller verfügbar. Weitere Informationen zu Switch und Erweiterungen finden Sie unter [virtueller Hyper-V-Switch](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="switch-and-network-adapter-choices"></a>Optionen für Switch und Netzwerkadapter
Hyper-V bietet drei Arten von virtuellen Switches und zwei Arten von virtuellen Netzwerkadaptern. Wählen Sie aus, welche der beiden Optionen bei der Erstellung ausgewählt werden sollen. Sie können Hyper-v-Manager oder das Hyper-v-Modul für Windows PowerShell verwenden, um virtuelle Switches und virtuelle Netzwerkadapter zu erstellen und zu verwalten. Einige erweiterte Netzwerkfunktionen wie erweiterte Port-Zugriffs Steuerungs Listen (Access Control Lists, ACLs) können nur mithilfe von Cmdlets im Hyper-V-Modul verwaltet werden.

Sie können einige Änderungen an einem virtuellen Switch oder virtuellen Netzwerkadapter vornehmen, nachdem Sie ihn erstellt haben. Beispielsweise ist es möglich, einen vorhandenen Switch in einen anderen Typ zu ändern, dies wirkt sich jedoch auf die Netzwerkfunktionen aller virtuellen Computer aus, die mit diesem Switch verbunden sind.  Dies geschieht wahrscheinlich nicht, es sei denn, Sie haben einen Fehler gemacht oder müssen etwas testen. Ein weiteres Beispiel: Sie können einen virtuellen Netzwerkadapter mit einem anderen Switch verbinden, was Sie möglicherweise tun, wenn Sie eine Verbindung mit einem anderen Netzwerk herstellen möchten. Es ist jedoch nicht möglich, einen virtuellen Netzwerkadapter von einem Typ in einen anderen zu ändern. Anstatt den Typ zu ändern, fügen Sie einen weiteren virtuellen Netzwerkadapter hinzu, und wählen Sie den entsprechenden Typ aus.

Die Typen virtueller Switches lauten:

-   **Externer virtueller Switch** : stellt eine Verbindung mit einem verkabelten, physischen Netzwerk her, indem es an einen physischen Netzwerkadapter gebunden wird.

-   **Interner virtueller Switch** : stellt eine Verbindung mit einem Netzwerk her, das nur von den virtuellen Maschinen auf dem Host mit dem virtuellen Switch und zwischen dem Host und den virtuellen Maschinen verwendet werden kann.

-   **Privater virtueller Switch** : stellt eine Verbindung mit einem Netzwerk her, das nur von den virtuellen Maschinen verwendet werden kann, die auf dem Host ausgeführt werden und über den virtuellen Switch verfügen, aber keine Netzwerkverbindungen zwischen dem Host und den virtuellen Maschinen bereitstellen.

Typen von virtuellen Netzwerkadaptern:

-   **Hyper-V-spezifischer Netzwerkadapter** : verfügbar für virtuelle Computer der Generation 1 und der Generation 2. Sie wurde speziell für Hyper-v entwickelt und erfordert einen Treiber, der in Hyper-v-Integrationsdiensten enthalten ist. Diese Art von Netzwerkadapter ist schneller und wird empfohlen, es sei denn, Sie müssen im Netzwerk starten oder ein nicht unterstütztes Gast Betriebssystem ausführen. Der erforderliche Treiber wird nur für unterstützte Gast Betriebssysteme bereitgestellt. Beachten Sie, dass dieser Typ im Hyper-V-Manager und in den Netzwerk-Cmdlets nur als Netzwerkadapter bezeichnet wird.

-   **Legacy-Netzwerkadapter** : nur in virtuellen Computern der Generation 1 verfügbar. Emuliert einen Intel 21140-basierten PCI-Fast-Ethernet-Adapter und kann verwendet werden, um in einem Netzwerk zu starten, sodass Sie ein Betriebssystem von einem Dienst wie Windows-Bereitstellungs Dienste installieren können.

## <a name="hyper-v-networking-and-related-technologies"></a>Hyper-V-Netzwerke und zugehörige Technologien
Die neuesten Versionen von Windows Server enthalten Verbesserungen, die Ihnen weitere Optionen zum Konfigurieren des Netzwerks für Hyper-V zur Verfügung stehen. Windows Server 2012 führte z. b. Unterstützung für konvergierte Netzwerke ein. Auf diese Weise können Sie Netzwerk Datenverkehr über einen externen virtuellen Switch weiterleiten. Windows Server 2016 baut darauf auf, indem der Remote Zugriff auf den direkten Speicher (RDMA) auf Netzwerkadaptern zugelassen wird, die an einen virtuellen Hyper-V-Switch gebunden sind. Sie können diese Konfiguration entweder mit oder ohne Switch Embedded Teaming (Set) verwenden. Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;Set&#41;](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)

Einige Features basieren auf bestimmten Netzwerkkonfigurationen oder unter bestimmten Konfigurationen besser. Beachten Sie diese Punkte beim Planen oder Aktualisieren der Netzwerkinfrastruktur.

**Failoverclustering** : Es empfiehlt sich, den Cluster Datenverkehr zu isolieren und Hyper-V-Quality of Service (QoS) auf dem virtuellen Switch zu verwenden. Weitere Informationen finden Sie unter [Netzwerk Empfehlungen für einen Hyper-V-Cluster](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn550728(v=ws.11)) .

**Live Migration** : Verwenden Sie Leistungsoptionen, um die Netzwerk-und CPU-Auslastung zu reduzieren und die Zeit, die zum Durchführen einer Live Migration benötigt wird. Anweisungen finden Sie unter [Einrichten von Hosts für die Live Migration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md).

**Direkte Speicherplätze** : dieses Feature basiert auf dem SMB 3.0-Netzwerkprotokoll und RDMA. Weitere Informationen finden Sie unter [direkte Speicherplätze in Windows Server 2016](../../../storage/storage-spaces/storage-spaces-direct-overview.md).