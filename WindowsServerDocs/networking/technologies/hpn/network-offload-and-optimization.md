---
title: Netzwerk-Offload- und Optimierungstechnologien
description: Dieses Thema bietet einen Überblick über die Auslagerung und Optimierung von Technologien in Windows Server 2016, und enthält Links zu weiteren Anleitungen zu diesen Technologien.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 9cd63ae557eab6e8e4f69fedd20619d4e7af9184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847851"
---
# <a name="network-offload-and-optimization-technologies"></a>Netzwerk-Offload- und Optimierungstechnologien

In diesem Thema haben wir bieten Ihnen einen Überblick über die verschiedenen Auslagerung und Optimierung von Netzwerkfeatures in Windows Server 2016 verfügbar und erläutern, wie sie dabei helfen, Netzwerke effizienter zu gestalten. Zu diesen Technologien zählen Software nur (SO)-Features und Technologien, Software und Hardware (SH) integriert, Features und Technologien und Hardware nur (HO)-Features und Technologien.

Die drei Kategorien von Netzwerkfeatures in Windows Server 2016 verfügbar sind: 

1.  [Nur Software (SO) Features und Technologien](hpn-software-only-features.md): Diese Features werden als Teil des Betriebssystems implementiert und sind unabhängig von der Anzahl der zugrunde liegenden NICs. Manchmal werden diese Funktionen erfordern eine Optimierung der NIC für eine optimale Vorgang. Beispiele: Hyper-V-Features wie z. B. VmQoS, ACL- und nicht-Hyper-V-Features wie die NIC-Teamvorgang.   

2.  [Software und Hardware (SH) integriert, Features und Technologien](hpn-software-hardware-features.md): Diese Funktionen haben sowohl Software-und Hardwarekomponenten. Die Software ist auf Hardwarefunktionen, die für das Feature funktioniert erforderlich sind-Desktopplattform gebunden. Beispiele dafür sind VMMQ, VMQ, für die sendeseitige IPv4-Prüfsummenoffload und RSS.   

3.  [Hardware nur (HO) Features und Technologien](hpn-hardware-only-features.md): Diese Hardware beschleunigungen Verbesserung der netzwerkleistung in Verbindung mit der Software sind jedoch nicht Repositoryschicht eng Bestandteil jeder Softwarefunktion. Beispiele: Interruptüberprüfung, flusssteuerung und Receive-Side-IPv4-Prüfsummenoffload. 

4. [Erweiterte Eigenschaften NIC](hpn-nic-advanced-properties.md): Sie können NICs und alle Funktionen, die über Windows PowerShell mit dem Cmdlet "NetAdapter" verwalten.  Sie können auch Netzwerkkarten und alle Funktionen, die mit den Netzwerk-Systemsteuerung (ncpa.cpl) verwalten. 

>[!TIP]
>- Daher stehen Features und Technologien im alle Hardwarearchitekturen, unabhängig von der NIC-Geschwindigkeit oder NIC-Funktionen.
>
>- SH und HO stehen nur, wenn die Netzwerkadapter die Funktionen und Technologien unterstützt.

---