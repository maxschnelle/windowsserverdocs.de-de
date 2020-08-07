---
title: Entfernen eines Knotens aus aktiver Failoverclustermitgliedschaft
description: In diesem Artikel wird das Auffinden von Knoten behandelt, die aus der Mitgliedschaft des aktiven Failoverclusters entfernt wurden
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: da46b39f853476676a06bcaaa20338dd1a178586
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935570"
---
# <a name="nodes-being-removed-from-failover-cluster-membership-on-vmware-esx"></a>Knoten, die aus der failoverclustermitgliedschaft in VMware ESX entfernt werden

In diesem Artikel wird das Auffinden von Knoten, die aus der aktiven failoverclustermitgliedschaft entfernt werden, beim Hosten der Knoten in VMware ESX behandelt.

## <a name="symptom"></a>Symptom

Wenn das Problem auftritt, wird im System Ereignisprotokoll des Ereignisanzeige Folgendes angezeigt:

![Ereignis 1135](media/nodes-failover-cluster-vmware/1135.png)

## <a name="resolution"></a>Lösung

Ein bestimmtes Problem besteht darin, dass die VMXNET3-Adapter eingehende Netzwerkpakete verwerfen, weil der eingehende Puffer zu niedrig eingestellt ist, um große Mengen an Datenverkehr zu verarbeiten. Wir können mühelos feststellen, ob es sich um ein Problem handelt. verwenden Sie hierzu den System Monitor, um den Leistungsindikatoren "Netzwerkschnittstelle\Empfangene Pakete erhalten" zu betrachten

![Leistungsindikatoren hinzufügen](media/nodes-failover-cluster-vmware/0527.png)

Wenn Sie diesen Leistungs Besatz hinzugefügt haben, sehen Sie sich die durchschnittlichen, minimalen und maximalen Zahlen an, und wenn es sich um einen Wert handelt, der größer als 0 (null) ist, muss der Empfangs Puffer für den Adapter angepasst werden. Dieses Problem ist in der Knowledge Base von VMware dokumentiert: [großer Paketverlust auf der Ebene des Gast Betriebssystems auf der VMXNET3-vNIC in ESXi 5. x/4. x](https://kb.vmware.com/s/article/2039495).
