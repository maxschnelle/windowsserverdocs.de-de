---
title: Planen der GPU-Beschleunigung in Windows Server
description: Erfahren Sie mehr über die verschiedenen Hyper-V-Technologien für die GPU-Beschleunigung, einschließlich DDA und remotefx vgpu
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 07/14/2020
ms.openlocfilehash: afdb856fc84bcee634381f04054a97f545056882
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938793"
---
# <a name="plan-for-gpu-acceleration-in-windows-server"></a>Planen der GPU-Beschleunigung in Windows Server

> Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

In diesem Artikel werden die in Windows Server verfügbaren Funktionen für die Grafikvirtualisierung vorgestellt.

## <a name="when-to-use-gpu-acceleration"></a>Verwendung der GPU-Beschleunigung

Abhängig von der Arbeitsauslastung sollten Sie die GPU-Beschleunigung in Erwägung gezogen. Vor der Auswahl von GPU-Beschleunigung sollten Sie Folgendes berücksichtigen:

- **App-und desktopremoting-Workloads (VDI/daas)**: Wenn Sie einen app-oder desktopremotingdienst mit Windows Server entwickeln, sollten Sie den Katalog der apps in Erwägung gezogen haben, die Ihre Benutzer erwarten. Einige Arten von apps, wie z. b. CAD/CAM-apps, Simulations-apps, Spiele und Render/Visualisierungs-apps, basieren stark auf 3D-Rendering, um eine reibungslose und reaktionsfähige Interaktivität zu ermöglichen Die meisten Kunden werden GPUs in Erwägung gezogen, dass Sie mit diesen Arten von apps eine angemessene Benutzer Leistung haben.
- **Remoterendering-, Codierungs-und Visualisierungs Arbeits Auslastungen**: Diese Grafik orientierten Workloads basieren tendenziell stark auf den spezialisierten Funktionen von GPU, wie z. b. effizientes 3D-Rendering und Frame Codierung/Decodierung, um Kosten Effektivität und Durchsatz Ziele zu erreichen. Für diese Art der Arbeitsauslastung kann ein einzelner GPU-fähiger virtueller Computer in der Lage sein, den Durchsatz von vielen virtuellen CPU-Computern abzugleichen.
- **HPC-und ml-Arbeits Auslastungen**: für hoch Daten parallele Compute-Workloads, wie z. b. Hochleistungsmodelle für Compute-und Machine Learning-Modelle, können GPUs die Zeit bis zum Ergebnis, die Zeit bis zum Rückschluss und die Trainingszeit drastisch verkürzen. Alternativ bieten Sie möglicherweise eine bessere Kosteneffizienz als eine reine CPU-Architektur auf einer vergleichbaren Leistungs Ebene. Viele HPC-und Machine Learning-Frameworks haben eine Option zum Aktivieren der GPU-Beschleunigung. Stellen Sie sich vor, ob dies für die jeweilige Arbeitsauslastung von Vorteil

## <a name="gpu-virtualization-in-windows-server"></a>GPU-Virtualisierung in Windows Server

GPU-Virtualisierungstechnologien ermöglichen eine GPU-Beschleunigung in einer virtualisierten Umgebung, in der Regel auf virtuellen Computern Wenn Ihre Arbeitsauslastung mit Hyper-V virtualisiert ist, müssen Sie die Grafikvirtualisierung verwenden, um eine GPU-Beschleunigung von der physischen GPU zu Ihren virtualisierten Apps oder Diensten bereitzustellen. Wenn Ihre Arbeitsauslastung jedoch direkt auf physischen Windows Server-Hosts ausgeführt wird, ist keine Grafik Virtualisierung erforderlich. Ihre apps und Dienste haben bereits Zugriff auf die GPU-Funktionen und APIs, die in Windows Server System intern unterstützt werden.

Die folgenden Technologien zur Grafik Virtualisierung sind für Hyper-V-VMs in Windows Server verfügbar:

- [Diskrete Geräte Zuweisung (DDA)](#discrete-device-assignment-dda)
- [RemoteFX vGPU](#remotefx-vgpu)

Zusätzlich zu VM-Workloads unterstützt Windows Server auch die GPU-Beschleunigung von containerisierten Workloads innerhalb von Windows-Containern. Weitere Informationen finden Sie unter [GPU-Beschleunigung in Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/gpu-acceleration).

## <a name="discrete-device-assignment-dda"></a>Diskrete Geräte Zuweisung (DDA)

Bei der diskreten Geräte Zuweisung (DDA), auch als GPU-Pass-Through bezeichnet, können Sie einen oder mehrere physische GPUs für einen virtuellen Computer verwenden. In einer DDA-Bereitstellung werden virtualisierte Arbeits Auslastungen auf dem systemeigenen Treiber ausgeführt und verfügen in der Regel über vollständigen Zugriff auf die GPU-Funktionalität. DDA bietet die höchste Ebene der APP-Kompatibilität und der möglichen Leistung. DDA kann auch eine GPU-Beschleunigung für Linux-VMs bereitstellen, die unterstützt werden.

Eine DDA-Bereitstellung kann nur eine begrenzte Anzahl von virtuellen Computern beschleunigen, da jede physische GPU eine Beschleunigung für höchstens eine VM bereitstellen kann. Wenn Sie einen Dienst entwickeln, dessen Architektur freigegebene virtuelle Computer unterstützt, sollten Sie mehrere beschleunigte Workloads pro VM verwenden. Wenn Sie z. b. einen Desktop Remoting-Dienst mit RDS entwickeln, können Sie die Benutzer Skalierung verbessern, indem Sie die Multi-Session-Funktionen von Windows Server verwenden, um auf jedem virtuellen Computer mehrere Benutzer Desktops zu hosten. Diese Benutzer haben die Vorteile der GPU-Beschleunigung gemeinsam.

Weitere Informationen finden Sie in den folgenden Themen:

- [Planen der Bereitstellung einer diskreten Geräte Zuweisung](plan-for-deploying-devices-using-discrete-device-assignment.md)
- [Bereitstellen von Grafikgeräten mit Discrete Device Assignment](../deploy/Deploying-graphics-devices-using-dda.md)

## <a name="remotefx-vgpu"></a>RemoteFX vGPU

> [!NOTE]
> Aufgrund von Sicherheitsbedenken ist RemoteFX vGPU auf allen Windows-Versionen ab dem Sicherheitsupdate vom 14. Juli 2020 standardmäßig deaktiviert. Weitere Informationen dazu finden Sie in [KB 4570006](https://support.microsoft.com/help/4570006).

Remotefx vgpu ist eine Grafik-Virtualisierungstechnologie, die die gemeinsame Nutzung einer einzelnen physischen GPU zwischen mehreren virtuellen Computern ermöglicht. In einer remotefx-vgpu-Bereitstellung werden virtualisierte Arbeits Auslastungen auf dem remotefx 3D-Adapter von Microsoft ausgeführt, mit dem GPU-Verarbeitungsanforderungen zwischen dem Host und den Gästen koordiniert werden. Remotefx vgpu eignet sich am besten für Wissensarbeiter und hochleistungsfähige Workloads, bei denen keine dedizierten GPU-Ressourcen erforderlich sind. Remotefx vgpu kann nur GPU-Beschleunigung für Windows-VMS bereitstellen.

Weitere Informationen finden Sie in den folgenden Themen:

- [Bereitstellen von Grafikgeräten mit RemoteFX vGPU](../deploy/deploy-graphics-devices-using-remotefx-vgpu.md)
- [Unterstützung für RemoteFX 3D-Grafikkarte (vGPU)](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)

## <a name="comparing-dda-and-remotefx-vgpu"></a>Vergleichen von DDA und remotefx vgpu

Beachten Sie bei der Planung der Bereitstellung die folgenden Funktionen, und unterstützen Sie die Unterschiede zwischen den Technologien für die

| BESCHREIBUNG | RemoteFX vGPU | Diskrete Gerätezuweisung |
|--|--|--|
| GPU-Ressourcenmodell | Dediziert oder freigegeben | Nur dediziert |
| VM-Dichte | Hoch (mindestens ein GPUs zu vielen VMS) | Niedrig (mindestens ein GPUs zu einer VM) |
| Anwendungskompatibilität | DX 11.1, OpenGL 4.4, OpenCL 1.1 | Alle GPU-Funktionen werden vom Hersteller bereitgestellt (DX 12, OpenGL, CUDA) |
| AVC444 | Standardmäßig aktiviert | Verfügbar über Gruppenrichtlinie |
| GPU VRAM | Bis zu 1 GB dediziertes VRAM | Bis zur Menge des von der GPU unterstützen VRAMs |
| Bildfrequenz | Bis zu 30 Bilder pro Sekunde | Bis zu 60 Bilder pro Sekunde |
| GPU-Treiber im Gastbetriebssystem | Anzeigetreiber für RemoteFX 3D-Adapter (Microsoft) | GPU-Anbieter Treiber (nVidia, AMD, Intel) |
| Host Betriebssystem | Windows Server 2016 | Windows Server 2016; Windows Server 2019 |
| Unterstützung des Gastbetriebssystems | Windows Server 2012 R2; Windows Server 2016; Windows 7 SP1; Windows 8.1; Windows 10 | Windows Server 2012 R2; Windows Server 2016; Windows Server 2019; Windows 10; Linux |
| Hypervisor | Microsoft Hyper-V | Microsoft Hyper-V |
| GPU-Hardware | Enterprise-GPUs (z. B. Nvidia Quadro/GRID oder AMD FirePro) | Enterprise-GPUs (z. B. Nvidia Quadro/GRID oder AMD FirePro) |
| Serverhardware | Keine speziellen Anforderungen | Moderner Server, stellt IOMMU dem Betriebssystem zur Verfügung (meist SR-IOV-kompatible Hardware) |
