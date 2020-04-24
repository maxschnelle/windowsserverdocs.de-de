---
title: Größenbestimmung virtueller Computer
description: Größenempfehlungen für jeden Workloadtyp.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 12/02/2019
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 1d6a7daa3966488c951117b083411587d13be56b
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857103"
---
# <a name="virtual-machine-sizing-guidance"></a>Leitfaden zur Größenbestimmung virtueller Computer

Unabhängig davon, ob du den virtuellen Computer auf Remotedesktopdiensten oder dem virtuellen Windows-Desktop ausführst, erfordern unterschiedliche Arten von Workloads unterschiedliche Konfigurationen für die virtuellen Sitzungshostcomputer (VM). Um die bestmögliche Erfahrung zu gewährleisten, skaliere deine Bereitstellung gemäß den Anforderungen deiner Benutzer.

## <a name="multi-session-recommendations"></a>Empfehlungen für mehrere Sitzungen

In der folgenden Tabelle ist die maximal empfohlene Anzahl von Benutzern pro vCPU (Virtual Central Processing Unit) und die minimale VM-Konfiguration für jede Workload aufgeführt. Diese Empfehlungen basieren auf [Remotedesktop-Workloads](remote-desktop-workloads.md).

| Workloadtyp | Maximale Anzahl von Benutzern pro vCPU | vCPU/RAM/BS-Mindestspeicher | Azure-Beispielinstanzen | Profilcontainer-Mindestspeicher |
| --- | --- | --- | --- | --- |
| Leicht | 6 | 2 vCPUs, 8 GB RAM, 16 GB Speicher | D2s_v3, F2s_v2 | 30 GB |
| Medium (Mittel) | 4 | 4 vCPUs, 16 GB RAM, 32 GB Speicher | D4s_v3, F4s_v2 | 30 GB |
| Schwer | 2 | 4 vCPUs, 16 GB RAM, 32 GB Speicher | D4s_v3, F4s_v2 | 30 GB |
| Leistung | 1 | 6 vCPUs, 56 GB RAM, 340 GB Speicher | D4s_v3, F4s_v2, NV6 | 30 GB |

## <a name="single-session-recommendations"></a>Empfehlungen für Einzelsitzungen

Als Empfehlungen für die VM-Größenbestimmung in Szenarien mit nur einer Sitzung empfehlen wir mindestens zwei physische CPU-Kerne pro VM (in der Regel vier vCPUs mit Hyperthreading). Wenn du spezifischere VM-Größenempfehlungen für Szenarien mit nur einer Sitzung benötigst, frage bei den Softwareanbietern nach, die für deine Workload spezifisch sind. Die VM-Größenbestimmung für virtuelle Einzelsitzungscomputer wird sich wahrscheinlich an Richtlinien für physische Geräte orientieren.

## <a name="general-virtual-machine-recommendations"></a>Allgemeine Empfehlungen für virtuelle Computer

Informationen zu den VM-Anforderungen zum Ausführen des Betriebssystems finden Sie unter [Windows 10-Computerspezifikationen und -Systemanforderungen](https://www.microsoft.com/windows/windows-10-specifications).

Es wird empfohlen, für Produktionsworkloads, die eine Vereinbarung zum Servicelevel (SLA) erfordern, SSD Premium Speicher für deinen Betriebssystemdatenträger zu verwenden. Weitere Informationen findest du in der [SLA für virtuelle Computer](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_8/).

GPUs sind eine gute Wahl für Benutzer, die regelmäßig grafikintensive Programme zum Rendern von Videos, für 3D-Entwürfe und für Simulationen verwenden. Weitere Informationen zur Grafikbeschleunigung findest du unter [Auswählen der Grafikrenderingtechnologie](rds-graphics-virtualization.md). Azure bietet mehrere Bereitstellungsoptionen für Grafikbeschleunigung sowie mehrere verfügbare GPU-VM-Größen. Weitere Informationen dazu findest du unter [Für GPU optimierte VM-Größen](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).

[Burstfähige VMs der B-Serie](https://docs.microsoft.com/azure/virtual-machines/windows/b-series-burstable) sind eine gute Wahl für Benutzer, die nicht immer maximale CPU-Leistung benötigen. Weitere Informationen zu VM-Typen und -Größen findest du unter [Größen für virtuelle Windows-Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) und in den Preisinformationen auf [unserer Seite zu den Serien virtueller Computer](https://azure.microsoft.com/pricing/details/virtual-machines/series/).

## <a name="test-your-workload"></a>Testen deiner Workload

Schließlich empfehlen wir, dass du Simulationstools verwendest, um deine Bereitstellung sowohl mit Belastungstests als auch mit Echtzeit-Anwendungssimulationen zu testen. Stelle sicher, dass dein System reaktionsfähig und robust genug ist, um die Benutzeranforderungen zu erfüllen, und denke daran, die Ladegröße zu verändern, um böse Überraschungen zu vermeiden.
