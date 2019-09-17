---
title: RDS – Welche Grafikvirtualisierungstechnologie ist die richtige für Sie?
description: Informationen zur Planung, die Ihnen bei der Auswahl der richtigen Grafikvirtualisierungsoption für Ihre RDS-Bereitstellung helfen.
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
ms.openlocfilehash: ce10575d38bccc0b22dadf55bd89156c6ce5ea7b
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871048"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>Welche Grafikvirtualisierungstechnologie ist die richtige für Sie?

Es stehen Ihnen eine Reihe von Optionen zur Verfügung, um die das Rendering von Grafiken in Remotedesktopdiensten zu aktivieren. Bei der Planung Ihrer Virtualisierungsumgebung spielen die folgenden Überlegungen eine Rolle, welche Technologie Sie für das Rendering von Grafiken auswählen:

![Überlegungen zum Rendering von Grafiken – Vergleicht Benutzerskalierung und GPU-Anforderungen, um die beste GPU-Technologie für Ihre Umgebung zu ermitteln.](media/rds-gpu.png)

In Windows Server 2016 stehen Ihnen mit Hyper-V zwei Technologien zur Grafikvirtualisierung zur Verfügung, mit denen Sie die GPU-Hardware nutzen können:

- [Diskrete Gerätezuweisung (Discrete Device Assignment, DDA)](#discrete-device-assignment) – Für höchste Leistung bei Verwendung einer oder mehrerer GPUs, die einer VM zugeordnet sind und native GPU-Treiberunterstützung innerhalb der VM bieten. Die Dichte ist gering, da sie durch die Anzahl der im Server verfügbaren physischen GPUs begrenzt ist. 
- [Remote FX vGPU](#remotefx-vgpu) – Für Büroanwender und High-Burst-GPU-Szenarien, bei denen mehrere VMs eine oder mehrere GPUs durch Paravirtualisierung nutzen. Diese Lösung bietet eine höhere Benutzerdichte pro Server.

Die folgende Abbildung zeigt die Optionen zur Grafikvirtualisierung in Windows Server 2016.

![Optionen zur Grafikvirtualisierung in Windows Server 2016 mit RDS – zeigt die drei verfügbaren Technologien und wie sie sich in Umfang und Leistung unterscheiden](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>Diskrete Gerätezuweisung
Die diskrete Gerätzuweisung (Discrete Device Assignment, DDA) ist eine Pass-Through-Hardwarelösung, die die beste Leistung bietet, da die VM über den nativen Treiber uneingeschränkten Zugriff auf die GPU hat. Ihr VM-Benutzer kann auf die vollen Funktionen seines Geräts sowie auf den nativen Treiber des Geräts zugreifen. Dies umfasst die Features und Funktionen zum Betreiben des Geräts in einem VM-Spiegel, der dasselbe Gerät ohne Betriebssystem (Bare-Metal) ausführt.

Weitere Informationen zu DDA finden Sie unter [Planen der Bereitstellung der diskreten Gerätezuweisung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU ist eine Technologie zur Grafikvirtualisierung, die es ermöglicht, die Rechenleistung einer GPU auf verschiedene Gastbetriebssysteme aufzuteilen, um Szenarien von Büroanwendern zu ermöglichen (siehe erste Grafik oben). Die Neuerungen in Windows Server 2016 ermöglichen weitere Verbesserungen für GPU-Burst-Szenarien, z. B. für Designeranwendungen und Datenvisualisierung. Weitere Verbesserungen sind:

- Unterstützung für Gast-VMs der zweiten Generation, Windows Server 2016 Gast-VMs und Windows-Client-Hyper-V-Host.
  >[!NOTE] 
  > Der Remotedesktop-Sitzungshost wird auf einer Gast-VM mit Windows Server 2016 nicht unterstützt. Pro Gast-VM mit Windows Server 2016 kann nur eine Sitzung gehostet werden.

- Verbesserte Anwendungskompatibilität und -stabilität.
- Erweiterter Sitzungsmodus für VM Connect, der die Umleitung von USB und Zwischenablage über VM Connect zu einer VM ermöglicht, die für RemoteFX vGPU aktiviert ist.

Weitere Informationen finden Sie unter [Einrichten und Konfigurieren von RemoteFX vGPU für Remotedesktopdienste](rds-remotefx-vgpu.md).

## <a name="which-should-you-use"></a>Welche Option sollten Sie verwenden?

Wichtige Überlegungen zur Virtualisierungstechnologie hängen möglicherweise von den Hardwarespezifikationen oder Anwendungsanforderungen in Ihrer Umgebung ab. Hier folgt eine kurze Tabelle zu den DDA- und RemoteFX vGPU-Funktionen:

| Feature               | RemoteFX vGPU                                                                       | Diskrete Gerätezuweisung                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| Geräte-GPU-Zuweisung | Paravirtualisierung (viele VMs für eine oder mehrere GPUs)                                     | mindestens eine GPU für eine VM                                                  |
| Skalierung                 | Beste Skalierung/1 GPU für viele VMs                                                      | Geringe Skalierung/Mindestens eine GPU für eine VM                                     |
| Anwendungskompatibilität     | DX 11.1, OpenGL 4.4, OpenCL 1.1                                                     | Alle GPU-Funktionen werden vom Hersteller bereitgestellt (DX 12, OpenGL, CUDA)          |
| AVC444                | Standardmäßig aktiviert (Windows 10 und Windows Server 2016)                             | Verfügbar über Gruppenrichtlinie (Windows 10 und Windows Server 2016)    |
| GPU VRAM              | Bis zu 1 GB dediziertes VRAM                                                           | Bis zur Menge des von der GPU unterstützen VRAMs                                        |
| Bildfrequenz            | Bis zu 30 Bilder pro Sekunde                                                                         | Bis zu 60 Bilder pro Sekunde                                                            |
| GPU-Treiber im Gastbetriebssystem   | Anzeigetreiber für RemoteFX 3D-Adapter (Microsoft)                                      | Treiber des GPU-Herstellers (Nvidia, AMD, Intel)                                 |
| Unterstützung des Gastbetriebssystems      |  Windows Server 2012 R2, Windows Server 2016, Windows 7 SP1, Windows 8.1, Windows 10 |  Windows Server 2012 R2, Windows Server 2016, Windows 10, Linux         |
| Hypervisor            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| Verfügbarkeit des Hostbetriebssystems  |  Windows Server 2012 R2, Windows Server 2016, Windows 10                             | Windows Server 2016                                                    |
| GPU-Hardware          | Enterprise-GPUs (z. B. Nvidia Quadro/GRID oder AMD FirePro)                         | Enterprise-GPUs (z. B. Nvidia Quadro/GRID oder AMD FirePro)            |
| Serverhardware       | Keine speziellen Anforderungen                                                             | Moderner Server, stellt IOMMU dem Betriebssystem zur Verfügung (meist SR-IOV-kompatible Hardware) |

Eine allgemeine Faustregel ist die Verwendung von DDA für die beste Anwendungskompatibilität, da der virtuelle Computer direkten Zugriff auf die GPU hat. Wenn Ihre Anwendungen oder Workloads nicht die strengen GPU-Anforderungen erfüllen und Sie eine breitere Basis von Benutzern bedienen möchten, ist RemoteFX vGPU vielleicht am besten für Sie geeignet.