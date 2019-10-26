---
title: Bereitstellen von Grafik Geräten mithilfe von remotefx vgpu
description: Erfahren Sie, wie Sie remotefx vgpu in Windows Server bereitstellen und konfigurieren.
ms.prod: windows-server-threshold
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 08/21/2019
ms.openlocfilehash: 7111899557279d825191948e737d83d7467ce786
ms.sourcegitcommit: 81198fbf9e46830b7f77dcd345b02abb71ae0ac2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2019
ms.locfileid: "72923912"
---
# <a name="deploy-graphics-devices-using-remotefx-vgpu"></a>Bereitstellen von Grafik Geräten mithilfe von remotefx vgpu

> Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016

Die vgpu-Funktion für remotefx ermöglicht es mehreren virtuellen Computern, eine physische GPU gemeinsam zu nutzen. Rendering-und computeressourcen werden dynamisch zwischen virtuellen Computern gemeinsam genutzt, sodass remotefx vgpu für hochleistungsfähige Workloads geeignet ist, bei denen keine dedizierten GPU-Ressourcen erforderlich sind. Beispielsweise kann in einem VDI-Dienst remotefx vgpu zum Auslagern von App-renderingkosten an die GPU verwendet werden, wobei die CPU-Auslastung verringert und die Dienst Skalierbarkeit verbessert wird.

## <a name="remotefx-vgpu-requirements"></a>Anforderungen für RemoteFX vGPU

Systemanforderungen für den Host:

- Windows Server 2016
- Eine DirectX 11,0-kompatible GPU mit einem WDDM 1,2-kompatiblen Treiber
- Eine CPU mit slat-Unterstützung (Second Level Address Translation)

Anforderungen an die Gast-VM:

- Unterstützte Gast Betriebssysteme. Weitere Informationen finden Sie [unter Unterstützung von remotefx 3D-Video Adaptern (vgpu)](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support).

Weitere Überlegungen zu Gast-VMs:

- Die Funktionen OpenGL und OpenCL sind nur in Gästen verfügbar, auf denen Windows 10 oder Windows Server 2016 ausgeführt wird.  
- DirectX 11,0 ist nur für Gäste verfügbar, auf denen Windows 8 oder höher ausgeführt wird.

## <a name="enable-remotefx-vgpu"></a>Remotefx-vgpu aktivieren

So konfigurieren Sie remotefx vgpu auf dem Windows Server 2016-Host:

1. Installieren Sie die von Ihrem GPU-Anbieter empfohlenen Grafiktreiber für Windows Server 2016.
2. Erstellen eines virtuellen Computers, auf dem ein von remotefx vgpu unterstütztes Gast Betriebssystem ausgeführt wird Weitere Informationen finden Sie [unter Unterstützung von remotefx 3D-Video Adaptern (vgpu)](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support).
3. Fügen Sie den remotefx 3D-Grafikadapter der VM hinzu. Weitere Informationen finden Sie unter [Konfigurieren des remotefx-vgpu-3D-Adapters](#configure-the-remotefx-vgpu-3d-adapter).

Standardmäßig verwendet remotefx vgpu alle verfügbaren und unterstützten GPUs. Führen Sie die folgenden Schritte aus, um die von remotefx vgpu verwendeten GPUs einzuschränken:

1. Navigieren Sie zu den Hyper-V-Einstellungen in Hyper-V-Manager.
2. Wählen Sie **physische GPUs** in den Hyper-V-Einstellungen aus.
3. Wählen Sie die nicht zu verwendende GPU aus, und deaktivieren Sie die Option **Diese GPU mit RemoteFX verwenden**.

### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>Konfigurieren des RemoteFX vGPU 3D-Adapters

Sie können entweder die Hyper-V-Manager-Benutzeroberfläche oder die PowerShell-Cmdlets verwenden, um die RemoteFX vGPU 3D-Grafikkarte zu konfigurieren.

#### <a name="configure-remotefx-vgpu-with-hyper-v-manager"></a>Konfigurieren von remotefx vgpu mit dem Hyper-V-Manager

1. Beendet den virtuellen Computer, wenn er gerade ausgeführt wird.
2. Öffnen Sie den Hyper-V-Manager, navigieren Sie zu **VM-Einstellungen**, und wählen Sie dann **Hardware hinzufügen**
3. Wählen Sie **remotefx 3D-Grafik Adapter**und dann **Hinzufügen**aus.
4. Legen Sie die maximale Anzahl der Monitore, die maximale Monitorauflösung und den dedizierten Videospeicher fest oder übernehmen Sie die Standardwerte.

   > [!NOTE]
   > - Wenn Sie höhere Werte für eine dieser Optionen festlegen, wirkt sich dies auf die Dienst Skalierung aus, daher sollten Sie nur die erforderlichen Werte festlegen.
   > - Wenn Sie 1 GB dedizierten VRAM verwenden müssen, verwenden Sie eine 64-Bit-Gast-VM anstelle von 32-Bit (x86), um optimale Ergebnisse zu erzielen.

5. Wählen Sie **OK** aus, um die Konfiguration abzuschließen.

#### <a name="configure-remotefx-vgpu-with-powershell-cmdlets"></a>Konfigurieren von remotefx vgpu mit PowerShell-Cmdlets

Verwenden Sie die folgenden PowerShell-Cmdlets, um den Adapter hinzuzufügen, zu überprüfen und zu konfigurieren:

- [Add-VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/add-vmremotefx3dvideoadapter?view=win10-ps)
- [Get-VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefx3dvideoadapter?view=win10-ps)
- [Set-VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/set-vmremotefx3dvideoadapter?view=win10-ps)
- [Get-vmremotefxphysicalvideoadapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefxphysicalvideoadapter?view=win10-ps)

## <a name="monitor-performance"></a>Überwachen der Leistung

Die Leistung und Skalierbarkeit eines remotefx-vgpu-fähigen dienstangs werden durch eine Vielzahl von Faktoren festgelegt, wie z. b. die Anzahl von GPUs auf Ihrem System, den gesamten GPU-Arbeitsspeicher, die Menge an System Arbeitsspeicher und die Arbeitsspeicher Geschwindigkeit, die Anzahl der CPU-Kerne und die CPU-Taktfrequenz Ausführungs.

### <a name="host-system-memory"></a>Host System Arbeitsspeicher

Für jede mit einer vgpu aktivierte VM verwendet remotefx den System Arbeitsspeicher sowohl im Gast Betriebssystem als auch auf dem Host Server. Der Hypervisor gewährleistet die Verfügbarkeit von System Arbeitsspeicher für ein Gast Betriebssystem. Auf dem Host muss jeder vgpu-fähige virtuelle Desktop seine Systemspeicher Anforderung für den Hypervisor ankündigen. Beim Starten des vgpu-fähigen virtuellen Desktops reserviert der Hypervisor zusätzlichen System Arbeitsspeicher auf dem Host.

Die Arbeitsspeicher Anforderung für den remotefx-fähigen Server ist dynamisch, weil der auf dem remotefx-fähigen Server belegte Arbeitsspeicher von der Anzahl der Monitore abhängig ist, die den vgpu-fähigen virtuellen Desktops zugeordnet sind, und der maximalen Auflösung für Diese Monitore.

### <a name="host-gpu-video-memory"></a>Host-GPU-Videospeicher

Jeder für vgpu aktivierte virtuelle Desktop verwendet den GPU-Hardware Videospeicher auf dem Host Server zum Rendering des Desktops. Außerdem verwendet ein Codec den Videospeicher, um den gerenderten Bildschirm zu komprimieren. Der erforderliche Arbeitsspeicher für das Rendering und die Komprimierung basiert direkt auf der Anzahl der Monitore, die für den virtuellen Computer bereitgestellt werden. Die Menge des reservierten Grafik Speichers variiert abhängig von der System Bildschirmauflösung und der Anzahl der Monitore, die vorhanden sind. Für einige Benutzer ist eine höhere Bildschirmauflösung für bestimmte Aufgaben erforderlich, aber es gibt eine größere Skalierbarkeit mit Einstellungen mit niedrigerer Auflösung, wenn alle anderen Einstellungen konstant bleiben.

### <a name="host-cpu"></a>Host-CPU

Der Hypervisor plant den Host und die VMs auf der CPU. Der mehr Aufwand wird auf einem remotefx-fähigen Host gesteigert, da das System einen zusätzlichen Prozess (rdvgm. exe) pro vgpu-aktiviertem virtuellen Desktop ausführt. Dieser Prozess verwendet den Grafikgeräte Treiber zum Ausführen von Befehlen auf der GPU. Der Codec verwendet die CPU auch zum Komprimieren von Bildschirm Daten, die an den Client zurückgesendet werden müssen.

Mehr virtuelle Prozessoren bedeuten eine bessere Benutzer Leistung. Es wird empfohlen, mindestens zwei virtuelle CPUs pro vgpu-aktiviertem virtuellen Desktop zuzuordnen. Außerdem wird die Verwendung der x64-Architektur für vgpu-fähige virtuelle Desktops empfohlen, da die Leistung auf virtuellen x64-Computern besser als x86 Virtual Machines ist.

### <a name="gpu-processing-power"></a>GPU-Verarbeitungsleistung

Jeder für vgpu aktivierte virtuelle Desktop verfügt über einen entsprechenden DirectX-Prozess, der auf dem Host Server ausgeführt wird. Dieser Prozess gibt alle Grafikbefehle wieder, die er vom virtuellen remotefx-Desktop empfängt, auf die physische GPU. Dies ist vergleichbar mit der gleichzeitig Ausführung mehrerer DirectX-Anwendungen auf derselben physischen GPU.

Normalerweise sind Grafikgeräte und Treiber darauf abgestimmt, nur einige Anwendungen auf dem Desktop auszuführen, aber remotefx dehnt die GPUs noch weiter aus. vgpus enthalten Leistungsindikatoren, die die GPU-Antwort auf remotefx-Anforderungen messen und Sie dabei unterstützen, sicherzustellen, dass die GPUs nicht zu weit gestreckt werden.

Wenn eine GPU wenig Ressourcen hat, dauert die Ausführung von Lese-und Schreibvorgängen lange. Administratoren können mithilfe von Leistungsindikatoren erkennen, wann Ressourcen angepasst und Ausfallzeiten für Benutzer verhindert werden sollen.

Weitere Informationen zu Leistungsindikatoren zum Überwachen von remotefx vgpu-Verhalten finden Sie unter [Diagnostizieren von Problemen mit der Grafikleistung in Remotedesktop](https://docs.microsoft.com/azure/virtual-desktop/remotefx-graphics-performance-counters).
