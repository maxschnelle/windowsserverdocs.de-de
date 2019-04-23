---
title: RDS - gibt an, welche Technologie zur Registrierungsvirtualisierung Grafiken für Sie geeignet ist?
description: Informationen zur Planung können Sie die richtigen Grafiken Virtualization-Option für Ihre RDS-Bereitstellung ausgewählt haben.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/16/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d6ff5b22-7695-4fee-b1bd-6c9dce5bd0e8
author: lizap
manager: scottman
ms.openlocfilehash: 7cf7fdf3510fcaaa955bd0031fb3564fe4372472
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875801"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>Die Grafik-Virtualisierungstechnologie für Sie geeignet ist?

Sie haben eine Reihe von Optionen, wenn es darum geht, aktivieren die Grafik-Rendering in Remote Desktop Services. Wenn Sie Ihre Virtualisierungsumgebung planen, Laufwerk die folgenden Aspekte der Technologie, die Sie auswählen, das Rendern von Grafiken:

![Grafik-Rendering-Überlegungen - vergleicht die Anzahl der Benutzer und GPU-Anforderungen können Sie die beste GPU-Technologie für Ihre Umgebung zu bestimmen](media/rds-gpu.png)

In Windows Server 2016 haben Sie Virtualisierungstechnologien mit zwei Grafiken zur Verfügung, mit Hyper-V, mit denen Sie die GPU-Hardware besser zu nutzen:

- [Diskrete Gerät Zuweisung (DDA)](#discrete-device-assignment) – speziell die höchste Leistung mit einem oder mehreren GPUs zu einem virtuellen Computer, die systemeigene Unterstützung von GPU-Treiber auf dem virtuellen Computer bereitstellen. Die Dichte ist gering, da es durch die Anzahl der physischen GPUs auf dem Server verfügbaren beschränkt ist. 
- [Remote FX vGPU](#remotefx-vgpu) – Knowledge Worker und High-Burst-GPU-Szenarien, die mehrere VMs, in denen eine oder mehrere GPUs über Para-Virtualisierung nutzen. Diese Lösung bietet höhere benutzerdichte pro Server.

Die folgende Abbildung zeigt die Grafiken Virtualisierungsoptionen in Windows Server 2016.

![Grafik-Virtualisierungsoptionen in Windows Server 2016 mit RDS - zeigt die drei verfügbaren Technologien und deren Unterschiede zur Skalierung und Leistung](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>Diskrete Gerätezuweisung
Diskrete Gerät Zuweisung (DDA) ist eine Pass-Through-Hardware-Lösung, die die beste Leistung bietet, angesichts der Tatsache, dass der virtuelle Computer vollständigen Zugriff auf die GPU, die mit dem nativen Treiber verfügt. Ihre VM-Benutzer kann den vollständigen Funktionsumfang von seinem Gerät als auch die native Treiber des Geräts zugreifen. Dies bedeutet, dass die Features und Funktionen des Geräts in einer VM-Spiegelung bare-Metal-Computern unter dem gleichen Gerät ausführen.

Finden Sie weitere Informationen zu DDA, [Planen für die Bereitstellung von diskrete Gerätezuordnung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU ist eine Technologie zur Registrierungsvirtualisierung Grafiken, die die verarbeitungsgeschwindigkeit GPU auf verschiedene Gastbetriebssysteme aus, um Szenarios zu aktivieren (Siehe obigen ersten Grafik) aufgeteilt werden kann. Verbesserungen in Windows Server 2016 können weitere Verbesserungen für GPU-Burst-Szenarien, z. B. für die Designer-Anwendungen und datenvisualisierung. Andere Verbesserungen von Features umfassen:

-   Unterstützung für die Generation 2-Gast-VMs, Windows Server 2016-Gast-VMs und Windows Client Hyper-V-Host.
   >[!NOTE] 
   > Remotedesktop-Sitzungshost wird auf einem Windows Server 2016-Gast-VM nicht unterstützt. nur 1-Sitzung kann pro Windows Server 2016-Gast-VM gehostet werden.

-   Verbesserte Anwendungskompatibilität und Stabilität.
-   VM verbinden erweiterter Sitzungsmodus, sodass USB- und die Zwischenablage, um umleitungen VM verbinden zu einem virtuellen Computer, die für RemoteFX vGPU aktiviert ist.

Weitere Informationen finden Sie in [festgelegt einrichten und Konfigurieren von RemoteFX vGPU für Remote Desktop Services](rds-remotefx-vgpu.md).

## <a name="which-should-you-use"></a>Welche sollten Sie verwenden?

Wichtige Überlegungen, die auf der Technologie der Hardware oder andere Anforderungen der Anwendung in Ihrer Umgebung möglicherweise abhängig ist. Hier ist eine kurze Tabelle zu DDA und RemoteFX vGPU-Funktionen:

| Feature               | RemoteFX vGPU                                                                       | Diskrete Gerätezuweisung                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| GPU-gerätezuweisung | Para-virtualisierter (Anzahl der virtuellen Computer ein oder mehrere GPUs)                                     | mindestens 1 GPU 1 virtuellen Computer                                                  |
| Skalierung                 | Am besten erweitern / 1 GPU zu viele virtuelle Computer                                                      | Skalierung wenig / 1 oder mehrere GPUs auf 1 VM                                     |
| App-Kompatibilität     | DX 11.1, OpenGL 4.4, OpenCL 1.1                                                     | Alle GPU-Funktionen, die vom Hersteller (DX 12, OpenGL, CUDA) bereitgestellt wird          |
| AVC444                | (Windows 10 und Windows Server 2016) standardmäßig aktiviert                             | Verfügbar über die Gruppenrichtlinie (Windows 10 und WindowsServer 2016)    |
| GPU VRAM              | Bis zu 1 GB dedizierte VRAM                                                           | Bis zu VRAM, die von der GPU unterstützt                                        |
| Bildfrequenz            | Bis zu 30 BpS.                                                                         | Bis zu 60fps                                                            |
| GPU-Treiber im Gastbetriebssystem   | Anzeigetreiber für RemoteFX-3D-Adapter (Microsoft)                                      | GPU-Hersteller-Treiber (Nvidia, AMD, Intel)                                 |
| Gast-BS-Unterstützung      |  Windows Server 2012 R2 Windows Server 2016 Windows 7 SP1, Windows 8.1, Windows 10 |  Windows Server 2012 R2  Windows Server 2016  Windows 10 Linux         |
| Hypervisor            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| Host-BS-Verfügbarkeit  |  Windows Server 2012 R2 Windows Server 2016-Windows 10                             | Windows Server 2016                                                    |
| GPU-hardware          | Enterprise-GPUs (z. B. Nvidia Quadro/Raster oder AMD FirePro)                         | Enterprise-GPUs (z. B. Nvidia Quadro/Raster oder AMD FirePro)            |
| Server-hardware       | Keine besonderen Anforderungen                                                             | Moderne Server, macht IOMMU für Betriebssystem (in der Regel SR-IOV-kompatibler Hardware) |

Als allgemeine Faustregel werden DDA um die bestmögliche Anwendungskompatibilität verwenden, da der virtuelle Computer direkten Zugriff auf die GPU hat. Wenn Ihre Anwendungen oder Workloads nicht als strenge Anforderungen für GPU müssen und Server auf breitere Basis von Benutzern möchten, funktionieren möglicherweise RemoteFX vGPU am besten für Sie.