---
title: 'RDS – RemoteFX vGPU: Setup und Konfiguration'
description: Informationen zur Planung der Konfiguration der RemoteFX vGPU-Grafikvirtualisierung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/23/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0263fa6b-2185-4cc3-99ef-3588e2f4ada5
author: lizap
manager: scottman
ms.openlocfilehash: 3e7da1a70826dc720a96ceb3fe5d04868943f163
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712113"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>Einrichten und Konfigurieren von RemoteFX vGPU für Remotedesktopdienste


Mithilfe des vGPU-Features von RemoteFX können sich mehrere virtuelle Computer eine physische Grafikkarte teilen. Die virtuellen Computer sind in der Lage, das Rendering von Grafikinformationen vom Prozessor auf die dedizierte Grafikkarte zu übertragen. Dadurch wird die CPU-Auslastung verringert und die Skalierbarkeit für grafikintensive Workloads, die auf den virtuellen VDI-Computern ausgeführt werden, verbessert. 

## <a name="remotefx-vgpu-requirements"></a>Anforderungen für RemoteFX vGPU

Anforderungen an Hostsysteme: 

- Windows Server 2016 oder Windows 10
- DX 11.0-kompatible GPU mit WDDM 1.2-kompatiblem Treiber 
- Aktivierte Windows Server-RD-Virtualisierungshostrolle (ermöglicht die Hyper-V-Rolle) 
- Server mit einer CPU, die SLAT (Second Level Address Translation) unterstützt. 

Anforderungen an die Gast-VM:

- Gast-VM mit einem Windows Enterprise-Client (Windows 7 mit Service Pack 1, Windows 8.1, Windows 10) oder Windows Server (Windows Server 2012 R2 oder Windows Server 2016). Informationen zur weiteren Unterstützung von Betriebssystemen finden Sie unter [Unterstützte Konfiguration für Remotedesktopdienste](rds-supported-config.md).

Weitere Überlegungen zu Gast-VMs:

- Die OpenGL- und OpenCL-Funktionen sind nur unter Windows 10 oder Windows Server 2016 verfügbar.  
- DirectX 11.0 ist nur mit Windows 8 oder neueren Gast-VMs verfügbar. 
- Der Remotedesktop-Sitzungshost wird von RemoteFX vGPU nur unterstützt, wenn er als [persönlicher Sitzungsdesktop](rds-personal-session-desktops.md) ausgeführt wird.

Stellen Sie für Gast-VMS sicher, dass Sie [VDI-Bereitstellung – Unterstützte Gastbetriebssysteme](rds-supported-config.md#vdi-deployment--supported-guest-oss) lesen.

## <a name="install-remotefx-vgpu"></a>Installieren von RemoteFX vGPU

Führen Sie die folgenden Schritte aus, um RemoteFX auf dem Host für Windows Server 2016 und Windows 10 zu installieren und zu konfigurieren:

1. Installieren Sie das Betriebssystem.
2. Installieren Sie die neuesten GPU-Treiber für Windows 10/Windows Server 2016, die auf der Website des Grafikkartenherstellers erhältlich sind.
3. Installieren Sie RemoteFX vGPU auf dem Windows 10-/Windows Server 2016-Host:
   1. Aktivieren Sie auf einem Windows 10-Host das Hyper-V-Feature in der Systemsteuerung (wechseln Sie zu „Systemsteuerung/Programme und Features/Windows-Features aktivieren oder deaktivieren“):

      ![Fenster „Windows-Features“ zum Aktivieren des Hyper-V-Features](media/rds-hyperv-settings.png)

   2. Installieren Sie auf einem Windows Server 2016-Host die RDVH-Rolle (Remotedesktop-Virtualisierungshost).
   

4. Erstellen und konfigurieren Sie jetzt eine Gast-VM:
   1. Erstellen Sie eine VM mit Windows 10 Enterprise oder Windows Server 2016.
   2. Fügen Sie die RemoteFX 3D-Grafikkarte hinzu. Informationen dazu, wie Sie dies entweder mit Hyper-V-Manager oder PowerShell-Cmdlets erreichen, finden Sie unter [Konfigurieren des RemoteFX vGPU 3D-Adapters](#configure-the-remotefx-vgpu-3d-adapter). 

RemoteFX vGPU verwendet alle GPUs, wenn mehrere verfügbar sind. In bestimmten Fällen können Sie jedoch einschränken, welche GPUs von RemoteFX verwendet werden. In der Hyper-V-Umgebung steuern Sie dies, indem Sie gezielt auswählen, welche GPUs *nicht* von RemoteFX verwendet werden sollen. Gehen Sie wie folgt vor: 

   1. Navigieren Sie zu den Hyper-V-Einstellungen in Hyper-V-Manager.
   2. Klicken Sie in den Hyper-V-Einstellungen auf die Option für **physische GPUs**.
   3. Wählen Sie die nicht zu verwendende GPU aus, und deaktivieren Sie die Option **Diese GPU mit RemoteFX verwenden**.


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>Konfigurieren des RemoteFX vGPU 3D-Adapters
Sie können entweder die Hyper-V-Manager-Benutzeroberfläche oder die PowerShell-Cmdlets verwenden, um die RemoteFX vGPU 3D-Grafikkarte zu konfigurieren. 

#### <a name="through-hyper-v-manager"></a>Über Hyper-V-Manager:

1. Stellen Sie sicher, dass das System mit Hyper-V eingerichtet wurde und eine VM konfiguriert ist.  
2. Stoppen Sie die VM, wenn sie aktiv ist. 
3. Navigieren Sie in Hyper-V-Manager zu den **VM-Einstellungen**, und klicken Sie dann auf **Hardware hinzufügen**.
4. Wählen Sie **RemoteFX 3D-Grafikkarte** aus, und klicken Sie auf **Hinzufügen**. 
5. Legen Sie die maximale Anzahl der Monitore, die maximale Monitorauflösung und den dedizierten Videospeicher fest oder übernehmen Sie die Standardwerte.

   > [!NOTE]
   > - Wenn Sie für eine dieser Optionen höhere Werte festlegen, wirkt sich dies auf die Skalierung aus, daher sollten Sie nur die unbedingt erforderlichen Einstellungen vornehmen.
   >
   > - Wenn Sie 1 GB dediziertes VRAM verwenden müssen, verwenden Sie eine 64-Bit-Gast-VM anstelle einer 32-Bit-Gast-VM (x86), um die besten Ergebnisse zu erhalten.
6. Klicken Sie auf **OK**, um die Konfiguration abzuschließen.

#### <a name="with-powershell-cmdlets"></a>Über PowerShell-Cmdlets:

Führen Sie die folgenden Cmdlets aus, um den Adapter hinzuzufügen, zu überprüfen und zu konfigurieren: 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Weitere Informationen finden Sie unter [Add-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter).

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

Weitere Informationen finden Sie unter [Get-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter).

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Weitere Informationen finden Sie unter [Set-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter).

Führen Sie das folgende Cmdlet aus, um die physischen GPUs zu überprüfen:

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

Weitere Informationen finden Sie unter [Get-VMRemoteFXPhysicalVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter).

## <a name="monitor-performance"></a>Überwachen der Leistung

Die Leistung und Größe eines VDI-Systems wird durch eine Vielzahl von Faktoren bestimmt, z. B. den Gesamtspeicher der GPU, die Menge an Systemarbeitsspeicher und Arbeitsspeichergeschwindigkeit, die Anzahl der CPU-Kerne und die CPU-Taktfrequenz, die Speichergeschwindigkeit und die NUMA-Implementierung.

Die Remote-vGPU-Unterstützung in RDS umfasst die folgenden Leistungsindikatoren, die Sie im Systemmonitor (perfmon.exe) anzeigen können, um Informationen über den Bildfrequenzdurchsatz zu erhalten.

- RemoteFX Graphics – Leistungsindikatoren für die Komprimierung von Remotedesktopprotokoll-Grafiken. Wenn Sie z. B. die Anzahl der Bilder anzeigen möchten, die dem RDP zur Komprimierung präsentiert werden, schauen Sie sich den Indikator für **Eingabebilder/Sekunde** an.
- RemoteFX Network – Zähler für den Netzwerkdatenverkehr mit dem Remotedesktopprotokoll. Beispiel: **Roundtripzeit (RTT)** .
- RemoteFX Root GPU-Management – Misst das verfügbare und reservierte VRAM.
- RemoteFX Software – Stellt Indikatoren für Erfassungsrate, GPU-Antwortzeit und andere zur Verfügung.

Zur weiteren Low-Level-Überwachung der Leistung, insbesondere zur Fehlerbehebung, können Sie die folgenden zusätzlichen Leistungsindikatoren verwenden:

- RemoteFX Synth3D VSC VM-Gerät 
- RemoteFX Synth3D VSC VM-Transportkanal 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP VM-Gerät 
- RemoteFX Synth3D VSP VM-Kanal
