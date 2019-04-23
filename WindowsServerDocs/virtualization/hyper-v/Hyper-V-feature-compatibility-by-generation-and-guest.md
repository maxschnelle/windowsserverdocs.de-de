---
title: Hyper-V-Feature Compatibility nach Generation und Gast
description: Listet die Generationen und Betriebssystemen, die mit den wichtigsten Features von Hyper-V kompatibel sind
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81c1f32d-7814-4992-8a66-dd4b77c939b4
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 1863c1736d3c8573b3d11c6bef492c6645d28a77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859761"
---
# <a name="hyper-v-feature-compatibility-by-generation-and-guest"></a>Hyper-V-Feature Compatibility nach Generation und Gast

>Gilt für: Windows Server 2016
  
Die Tabellen in diesem Artikel zeigen Sie die Generationen und die Betriebssysteme, die kompatibel mit den Hyper-V-Funktionen, die nach Kategorien gruppiert sind. Im Allgemeinen erhalten Sie die beste Verfügbarkeit der Features mit einem virtuellen Computer der Generation 2 an, die das neueste Betriebssystem ausgeführt wird.  
  
Bedenken Sie, die einige Funktionen auf Hardware oder andere Infrastruktur basieren. Hardwaredetails, finden Sie unter [Systemanforderungen für Hyper-V unter Windows Server 2016](System-requirements-for-Hyper-V-on-Windows.md). In einigen Fällen kann eine Funktion mit einem beliebigen unterstützten Gast-Betriebssystem verwendet werden. Details für die Betriebssysteme unterstützt werden, finden Sie unter:  
  
* [Unterstützte Linux- und FreeBSD-VMs](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
* [Unterstützte Windows-Gastbetriebssysteme](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)  
  
## <a name="availability-and-backup"></a>Verfügbarkeit und Sicherung  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Prüfpunkte | 1 und 2 | Alle Gastbetriebssysteme  
Gast-clustering | 1 und 2 | Gäste, die clusterfähige Anwendungen ausführen und iSCSI-Ziel-Software installiert sein  
Replikation | 1 und 2 | Alle Gastbetriebssysteme  
Domänencontroller | 1 und 2 | Alle unterstützten Windows Server-Gast nur produktionsprüfpunkte verwenden. Finden Sie unter [unterstützt Windows Server-Gastbetriebssysteme](https://docs.microsoft.com/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows#supported-windows-server-guest-operating-systems)   
  
## <a name="compute"></a>Compute  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Dynamischer Arbeitsspeicher | 1 und 2 | Bestimmte Versionen der unterstützten Gäste. Finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht](https://technet.microsoft.com/library/hh831766.aspx) für Versionen vor Windows Server 2016 und Windows 10.  
Hinzufügen/Entfernen von Speicher | 1 und 2 | WindowsServer 2016, Windows 10  
Virtuelle NUMA | 1 und 2 | Alle Gastbetriebssysteme  
  
## <a name="development-and-test"></a>Entwicklung und Tests  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
COM/serielle Anschlüsse | 1 und 2 <br>**Hinweis**: Verwenden Sie für die Generation 2 Windows PowerShell zum Konfigurieren. Weitere Informationen finden Sie unter [fügen Sie einen COM-Port für das Kerneldebuggen](./plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md#BKMK_Debug). | Alle Gastbetriebssysteme  
  
## <a name="mobility"></a>Mobilität  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Livemigration  | 1 und 2 |  Alle Gastbetriebssysteme  
Importieren/Exportieren | 1 und 2 |  Alle Gastbetriebssysteme  
  
## <a name="networking"></a>Netzwerk  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Hinzufügen/Entfernen von virtuellen Netzwerkadapter | 2 | Alle Gastbetriebssysteme  
Legacy-Netzwerkadapter | 1 | Alle Gastbetriebssysteme  
E/a-Virtualisierung mit einzelstamm (SR-IOV) | 1 und 2 | 64-Bit-Windows-Gäste, beginnend mit Windows Server 2012 und Windows 8.  
Warteschlange für virtuelle Computer mit mehreren (VMMQ) | 1 und 2  | Alle Gastbetriebssysteme  
  
## <a name="remote-connection-experience"></a>Remoteverbindungsoptionen  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Diskrete gerätezuordnung (DDA) | 1 und 2 | Windows Server 2016, Windows Server 2012 R2 mit Update 3133690 nur installiert, Windows 10 <br> **Hinweis**: Ausführliche Informationen zum Update 3133690, finden Sie unter [dies](https://support.microsoft.com/kb/3133690) Support-Artikel.  
Verbesserter Sitzungsmodus | 1 und 2 | Windows Server 2016, Windows Server 2012 R2, Windows 10 und Windows 8.1, mit Remote Desktop Services aktiviert <br>**Hinweis**: Sie müssen möglicherweise auch den Host konfigurieren. Weitere Informationen finden Sie unter [Verwenden lokaler Ressourcen auf Hyper-V-VM mit VMConnect](./learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md).  
RemoteFx | 1 und 2 | Generation 1 auf 32-Bit und 64-Bit-Windows-Versionen ab Windows 8. <br> Generation 2 auf 64-Bit-Windows 10-Versionen  
  
## <a name="security"></a>Sicherheit  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Sicherer Start | 2 | **Linux**: Ubuntu 14.04 und höher, SUSE Linux Enterprise Server 12 und höher, Red Hat Enterprise Linux 7.0 und höher und CentOS 7.0 und höher<br>**Windows**: Alle unterstützten Versionen, die auf virtuelle Computer der Generation 2 ausgeführt werden können  
Abgeschirmte VMs | 2 | **Windows**: Alle unterstützten Versionen, die auf virtuelle Computer der Generation 2 ausgeführt werden können  
  
## <a name="storage"></a>Speicher  
  
Feature  | codegenerierung | Gastbetriebssystem  
------------- | ------------- | -----------  
Freigegebene virtuelle Festplatten (VHDX nur) | 1 und 2  | Windows Server 2016, Windows Server 2012 R2, Windows Server 2012  
SMB3 | 1 und 2 | Alle, die die SMB3 unterstützen  
Direkte Speicherplätze | 2 | Windows Server 2016  
Virtueller Fibre Channel | 1 und 2 | Windows Server 2016, Windows Server 2012 R2, Windows Server 2012  
VHDX-format | 1 und 2 | Alle Gastbetriebssysteme   
  
  
  
  
    


