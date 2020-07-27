---
title: Problembehandlung bei Nano Server
description: Wiederherstellungskonsole, Notverwaltungsdienste, Kerneldebugging
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.topic: article
ms.assetid: e427c66f-9571-4b8c-b65d-e7370d91544d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: ce71c2d11343be62d47f8957fa9414915fcc7847
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964412"
---
# <a name="troubleshooting-nano-server"></a>Problembehandlung bei Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet. 

Dieses Thema enthält Informationen zu Tools, die Sie verwenden können, um eine Verbindung zu Nano Server-Installationen herzustellen, diese zu diagnostizieren und zu reparieren.  
  
## <a name="using-the-nano-server-recovery-console"></a>Verwenden der Nano Server-Wiederherstellungskonsole 
 
Nano Server verfügt über eine Wiederherstellungskonsole, die sicherstellt, dass Sie auf Ihren Nano-Server zugreifen können, auch wenn eine Netzwerk-Fehlkonfiguration die Verbindung zum Nano Server beeinträchtigt. Sie können mithilfe der Wiederherstellungskonsole das Netzwerk reparieren und anschließend Ihre üblichen Remoteverwaltungstools verwenden.  
  
Wenn Sie Nano Server entweder auf einem virtuellen Computer oder auf einem physischen Computer verwenden, der über einen Monitor und eine Tastatur verfügt, wird eine Eingabeaufforderung im Textmodus im Vollbildmodus angezeigt. Melden Sie sich bei dieser Aufforderung mit einem Administratorkonto an, um den Computernamen und die IP-Adresse des Nano Servers anzuzeigen. Sie können diese Befehle verwenden, um in dieser Konsole zu navigieren:  
  
-   Verwenden Sie die Pfeiltasten zum Scrollen  
  
-   Verwenden Sie die TAB-TASTE, um zu jedem beliebigen Text zu wechseln, der mit **>** beginnt. Drücken Sie anschließend zur Auswahl die EINGABETASTE.  
  
-   Drücken Sie die ESC-TASTE, um zu einem Bildschirm oder zu einer Seite zurückzukehren. Wenn Sie sich auf der Startseite befinden, werden Sie durch Drücken der ESC-TASTE abgemeldet.  
  
-   Einige Bildschirme verfügen über zusätzliche Funktionen, die in der letzten Zeile des Bildschirms aufgeführt sind. Wenn Sie z.B. einen Netzwerkadapter durchsuchen, deaktiviert F4 den Netzwerkadapter.  
  
Mit der Wiederherstellungskonsole können Sie Netzwerkadapter, TCP/IP-Einstellungen sowie Firewallregeln anzeigen und konfigurieren.
> [!NOTE]
> Die Wiederherstellungskonsole unterstützt nur grundlegende Tastaturfunktionen. Tastaturbeleuchtung, Nummernblöcke und Tastaturlayoutwechsel wie z.B. FESTSTELLTASTE und Num-Lock-Taste werden nicht unterstützt. Es werden nur englische Tastaturen und Zeichensätze unterstützt.

## <a name="accessing-nano-server-over-a-serial-port-with-emergency-management-services"></a>Zugreifen auf Nano Server über einen seriellen Anschluss mit Notverwaltungsdiensten  
Mit den Notverwaltungsdiensten (Management Services, EMS) können Sie die grundlegende Problembehandlung durchführen, den Netzwerkstatus abrufen und Konsolensitzungen öffnen (einschließend CMD/PowerShell), indem Sie einen Terminalemulator auf einem seriellen Port verwenden. Durch diese Option ist es nicht mehr notwendig, dass eine Tastatur und ein Monitor die Fehlerbehebung für einen Server ausführen müssen. Weitere Informationen zu EMS finden Sie unter [Emergency Management Services Technical Reference (Technische Referenz zu den Notverwaltungsdiensten)](/previous-versions/windows/it-pro/windows-server-2003/cc784411(v=ws.10)).

Führen Sie folgendes Cmdlet aus, um die Notverwaltungsdienste (Emergency Management Services, EMS) auf einem Nano Server-Image zu aktivieren, sodass sie für den späteren Gebrauch bereit sind:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\EnablingEMS.vhdx   -EnableEMS   -EMSPort 3   -EMSBaudRate 9600`  
  
Dieses Beispiel-Cmdlet aktiviert EMS auf dem seriellen Port 3 mit einer Baudrate von 9.600 Bits/s. Wenn Sie diese Parameter nicht einschließen, sind die Standardeinstellungen Port 1 und 115.200 Bits/s. Um dieses Cmdlet für VHDX-Medien zu verwenden, stellen Sie sicher, dass Sie das Hyper-V-Feature und die zugehörigen Windows PowerShell-Module eingeschlossen haben.

## <a name="kernel-debugging"></a>Kerneldebugging  
Sie können das Nano Server-Image konfigurieren, um Kerneldebugging mit einer Vielzahl von Methoden zu unterstützen. Um Kerneldebugging mit einem VHDX-Image zu verwenden, stellen Sie sicher, dass Sie das Hyper-V-Feature und die zugehörigen Windows PowerShell-Module eingeschlossen haben. Weitere Informationen über allgemeines remotes Kernelbugging finden Sie unter [Setting Up Kernel-Mode Debugging over a Network Cable Manually (Manuelles Einrichten von Kernel-Modus-Debugging über ein Netzwerkkabel)](/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection) und [Remote Debugging Using WinDbg (Remotes Debugging mithilfe von WinDbg)](/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection).  
  
### <a name="debugging-using-a-serial-port"></a>Debuggen mit einem seriellen Port  
Verwenden Sie dieses Cmdlet, um das zu debuggende Image mithilfe eines seriellen Port zu aktivieren:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingSerial   -DebugMethod Serial   -DebugCOMPort 1   -DebugBaudRate 9600`  
  
In diesem Beispiel wird das serielle Debuggen über Port 2 mit einer Baudrate von 9.600 Bits/s aktiviert. Wenn Sie diese Parameter nicht angeben, sind die Standardeinstellungen Port 2 und 115.200 Bits/s. Wenn Sie jeweils EMS und Kerneldebugging verwenden möchten, müssen Sie diese so konfigurieren, dass sie zwei separate serielle Ports verwenden.  
  
### <a name="debugging-over-a-tcpip-network"></a>Debuggen über ein TCP/IP-Netzwerk  
Verwenden Sie dieses Cmdlet, um das zu debuggende Image über ein TCP/IP-Netzwerk zu aktivieren:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000`  
  
Dieses Cmdlet ermöglicht das Kerneldebugging in einer Weise, dass nur der Computer mit der IP-Adresse 192.168.1.100 eine Verbindung mit allen Kommunikationen über Anschluss 64000 herstellen kann. Die -DebugRemoteIP und die -DebugPort-Parameter sind für eine Portnummer höher als 49152 verbindlich. Dieses Cmdlet generiert einen Verschlüsselungsschlüssel in einer Datei zusammen mit der resultierenden VHD, die für die Kommunikation über einen Anschluss erforderlich ist. Alternativ können Sie Ihren eigenen Schlüssel mit dem -DebugKey-Parameter angeben, so wie im folgenden Beispiel gezeigt:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000   -DebugKey 1.2.3.4`  
  
### <a name="debugging-using-the-ieee1394-protocol-firewire"></a>Debuggen mithilfe des Protokolls IEEE1394 (Firewire)  
Verwenden Sie folgendes Beispiel-Cmdlet, um das Debuggen über IEEE1394 zu aktivieren:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingFireWire   -DebugMethod 1394   -DebugChannel 3`  
  
Der -DebugChannel-Parameter ist obligatorisch.  
  
### <a name="debugging-using-usb"></a>Debuggen mithilfe von USB  
Sie können das Debuggen über USB mit folgendem Cmdlet aktivieren:  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingUSB   -DebugMethod USB   -DebugTargetName KernelDebuggingUSBNano`  
  
Wenn Sie den remoten Debugger mit dem resultierenden Nano Server verbinden, geben Sie den Zielnamen an, wie vom -DebugTargetName-Parameter festgelegt.    
