---
title: Netzwerk-Offload- und Optimierungstechnologien
description: Dieses Thema bietet einen Überblick über die Auslagerungs-und Optimierungstechnologien in Windows Server 2016 und enthält Links zu weiteren Anleitungen zu diesen Technologien.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 57e8a61bc54be05a32daa7eabc55a09553cee28a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405683"
---
# <a name="network-offload-and-optimization-technologies"></a>Netzwerk-Offload- und Optimierungstechnologien

In diesem Thema erhalten Sie einen Überblick über die verschiedenen Features für die netzwerkabladung und-Optimierung, die in Windows Server 2016 verfügbar sind, und es wird erläutert, wie Sie die Netzwerke effizienter gestalten können. Zu diesen Technologien gehören nur Software-Features und-Technologien, integrierte Features und Technologien für Software und Hardware (SH) und Features und Technologien, die ausschließlich Hardware (Ho) sind.

Die drei Kategorien von Netzwerk Features, die in Windows Server 2016 verfügbar sind, sind: 

1.  [Nur Software Features und Technologien](hpn-software-only-features.md): Diese Funktionen werden als Teil des Betriebssystems implementiert und sind unabhängig von den zugrunde liegenden NIC (s). Manchmal müssen diese Features eine Optimierung der NIC für optimalen Betrieb erfordern. Beispiele hierfür sind Hyper-v-Features wie vmqos, ACLs und nicht-Hyper-v-Features wie NIC-Team Vorgänge.   

2.  [Integrierte Features und Technologien für Software und Hardware (SH)](hpn-software-hardware-features.md): Diese Features verfügen sowohl über Software-als auch Hardwarekomponenten. Die Software ist eng an Hardwarefunktionen gebunden, die für die Funktionsfähigkeit des Features erforderlich sind. Beispiele hierfür sind vmmq, VMQ, sende seitige IPv4-Prüfsumme Offload und RSS.   

3.  [Features und Technologien für Hardware only (Ho)](hpn-hardware-only-features.md): Diese Hardwarebeschleunigung verbessern die Netzwerkleistung in Verbindung mit der Software, sind aber nicht eng Teil eines Software Features. Beispiele hierfür sind Interrupt-Moderation, Fluss Steuerung und Empfangs seitige IPv4-Prüfsummen Abladung. 

4. [Erweiterte NIC-Eigenschaften](hpn-nic-advanced-properties.md): Sie können NICs und alle Features mithilfe von Windows PowerShell über das Cmdlet netadapter verwalten.  Sie können auch NICs und alle Features mithilfe der Netzwerk Steuerungs Option (ncpa. cpl) verwalten. 

>[!TIP]
>- Daher sind Features und Technologien in allen Hardwarearchitekturen verfügbar, unabhängig von NIC-Geschwindigkeit oder NIC-Funktionen.
>
>- SH-und Ho-Features sind nur verfügbar, wenn Ihr Netzwerkadapter die Features oder Technologien unterstützt.

---