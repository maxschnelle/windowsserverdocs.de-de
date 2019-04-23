---
title: RDS - RemoteFX vGPU Setup und Konfiguration
description: Informationen zum Konfigurieren von RemoteFX vGPU Grafiken Virtualisierung zur Planung.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876841"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>Einrichten und Konfigurieren von RemoteFX vGPU für Remotedesktopdienste


Die vGPU-Funktion von RemoteFX ermöglicht es mehreren virtuellen Computern freigeben eines physischen Adapters. Die virtuellen Computer sind zum Rendern des grafischen Informationen aus der Prozessor in der dedizierten Grafikkarte Auslagern können. Die CPU-Auslastung verringern wird und verbessert die Skalierbarkeit im Hinblick auf die Grafik ressourcenintensive arbeitsauslastungen, die in der VDI-VMs ausgeführt. 

## <a name="remotefx-vgpu-requirements"></a>Anforderungen für RemoteFX vGPU

Anforderungen für die Host-Systeme: 

- WindowsServer 2016 oder Windows 10
- DX-11.0-kompatiblen GPU mit kompatiblen Treiber für WDDM 1.2 
- Windows Server-Remotedesktop-Virtualisierungshost-Rolle aktiviert (ermöglicht das Hyper-V-Rolle) 
- Server mit einer CPU, die SLAT (Second Level Address Translation) unterstützt 

Gast-VM-Anforderungen:

- Gast-VM, die unter einem Windows Enterprise-Client (Windows 7 mit Service Pack 1, Windows 8.1, Windows 10) oder Windows Server (Windows Server 2012 R2 oder Windows Server 2016). Für zusätzliche Betriebssysteme unterstützen finden Sie unter [unterstützte Konfiguration für Remote Desktop Services](rds-supported-config.md).

Zusätzliche Überlegungen zu Gast-VMs:

- OpenGL- und OpenCL-Funktionalität ist nur in Windows 10 oder Windows Server 2016 verfügbar.  
- DirectX-11.0 ist nur mit Windows 8 oder neueren Gast-VMs verfügbar. 
- Remotedesktop-Sitzungshost wird nur mit RemoteFX vGPU unterstützt, wenn die Ausführung als ein [persönliche Sitzung Desktop](rds-personal-session-desktops.md).

Stellen Sie für Gast-VMS, überprüfen Sie [VDI-Bereitstellung – Gastbetriebssysteme OSs](rds-supported-config.md#vdi-deployment--supported-guest-oss).

## <a name="install-remotefx-vgpu"></a>Installieren von RemoteFX vGPU

Verwenden Sie zum Installieren und Konfigurieren von RemoteFX auf dem Host für Windows Server 2016 und Windows 10 die folgenden Schritte aus:

1. Installieren Sie das Betriebssystem.
2. Installieren Sie das neueste Windows 10/Windows Server 2016-GPU-Treibern zur Verfügung, von der Website des Anbieters des Grafik-Karte.
3. Installieren Sie auf dem Windows 10/Windows Server 2016-Host RemoteFX vGPU:
   1. Aktivieren Sie das Hyper-V-Feature in der Systemsteuerung (Wechseln Sie zu Control Panel/Programme und Funktionen/Turn Windows Features ein- oder ausschalten), auf einem Windows 10-Host:

      ![Features von Windows-Fenster, das Hyper-V-Feature aktivieren](media/rds-hyperv-settings.png)

   2. Installieren Sie die Rolle Remote Desktop Virtualization Host (RDVH) auf einem Windows Server 2016-Host.
   

4. Nun erstellen und Konfigurieren einer Gasts-VM:
   1. Erstellen eines virtuellen Computers mit Windows 10 Enterprise oder WindowsServer 2016.
   2. Fügen Sie der RemoteFX-3D-Grafikkarte hinzu. Finden Sie unter [konfigurieren Sie die RemoteFX vGPU-3D-Grafikkarte](#configure-the-remotefx-vgpu-3d-adapter) Informationen zur Vorgehensweise, die entweder Hyper-V-Manager oder PowerShell-Cmdlets. 

RemoteFX vGPU wird alle GPUs verwenden, wenn mehrere verfügbar sind. Allerdings werden in bestimmten Fällen können Sie die GPUs beschränken von RemoteFX verwendet. In der Hyper-V-Umgebung Sie steuern, indem explizit auszuwählen, welche die GPUs sollten *nicht* von RemoteFX verwendet werden. Gehen Sie wie folgt vor: 

   1. Navigieren Sie zu die Hyper-V-Einstellungen in Hyper-V-Manager.
   2. Klicken Sie auf **physischen GPUs** in Hyper-V-Einstellungen.
   3. Wählen Sie die GPU, die Sie nicht verwenden möchten, und deaktivieren Sie **verwenden Sie dieses GPU mit RemoteFX**.


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>Konfigurieren Sie die RemoteFX vGPU-3D-Grafikkarte
Sie können das Hyper-V-Manager-Benutzeroberfläche oder PowerShell-Cmdlets verwenden, den RemoteFX vGPU 3D-Grafiken-Adapter konfigurieren. 

#### <a name="through-hyper-v-manager"></a>Durch Hyper-V-Manager:

1. Stellen Sie sicher, das System eingerichtet ist, mit Hyper-V und verfügt über ein virtuellen Computer konfiguriert.  
2. Beenden Sie den virtuellen Computer aus, wenn er ausgeführt wird. 
3. Navigieren Sie im Hyper-V-Manager zu den **VM-Einstellungen**, und klicken Sie dann auf **Hardware hinzufügen**.
4. Wählen Sie **RemoteFX 3D-Grafikkarte**, und klicken Sie auf **hinzufügen**. 
5. Legen Sie die maximale Anzahl von Monitoren, maximale monitorauflösung und dedizierten, oder übernehmen Sie die Standardwerte.

   > [!NOTE]
   > - Höhere Werte für eine dieser Optionen festlegen, müssen die Auswirkungen auf die zu skalieren, damit nur festgelegt werden soll, absolut notwendig sind.
   >
   > - Wenn Sie dedizierte VRAM 1 GB verwenden möchten, verwenden Sie eine 64-Bit-Gast-VM anstelle von 32-Bit-(x86) für optimale Ergebnisse.
6. Klicken Sie auf **OK** um die Konfiguration abzuschließen.

#### <a name="with-powershell-cmdlets"></a>Mit PowerShell-Cmdlets:

Führen Sie die folgenden Cmdlets zum Hinzufügen, überprüfen, und konfigurieren Sie den Adapter aus: 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Weitere Informationen finden Sie [Add-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter).

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

Weitere Informationen finden Sie [Get-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter)

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Weitere Informationen finden Sie [Set-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter).

Führen Sie das folgende Cmdlet aus, um die physischen GPUs zu überprüfen:

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

Weitere Informationen finden Sie [Get-VMRemoteFXPhysicalVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter).

## <a name="monitor-performance"></a>Überwachen der Leistung

Die Leistung und Skalierung einer VDI-Systems ergeben sich eine Vielzahl von Faktoren wie z. B. GPUs-Arbeitsspeicher gesamt, Menge an Arbeitsspeicher und Speicher Geschwindigkeit, Anzahl der CPU-Kerne und CPU-Taktfrequenz speichergeschwindigkeit und NUMA-Implementierung.

Remote-vGPU-Unterstützung in RDS umfasst die folgenden Leistungsindikatoren, die Sie im Systemmonitor (perfmon.exe) zum Sammeln von Informationen zu Frame Rate Durchsatz anzeigen können.

- RemoteFX-Grafik - Leistungsindikatoren für die Komprimierung für Remote Desktop Protocol-Grafiken. Beispielsweise sollten Sie die Anzahl der Frames, die RDP-Verbindung angezeigt wird, für die Komprimierung betrachten, sehen Sie sich die **Eingabe Frames/Second** Leistungsindikator.
- RemoteFX-Netzwerk - Leistungsindikatoren für Remote Desktop Protocol-Netzwerkverkehr. Z. B. **(Round Trip Time, RTT)**.
- RemoteFX Root GPU-Management - Measures VRAM verfügbar und reserviert.
- RemoteFX-Software - enthält Leistungsindikatoren für die Erfassung Rate, GPU-Antwortzeit und andere.

Auf eher niedrigeren Ebenen für die Leistungsüberwachung für, insbesondere für die Problembehandlung können Sie die folgenden zusätzlichen Leistungsindikatoren:

- RemoteFX Synth3D VSC-VM-Gerät 
- RemoteFX Synth3D VSC-VM-Transportkanal 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP-VM-Gerät 
- RemoteFX Synth3D VSP-VM-Kanal
