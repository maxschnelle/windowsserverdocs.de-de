---
title: Systemanforderungen für Hyper-V unter Windows Server
description: Listet die Hardware und Firmware-Anforderungen für Hyper-V unter Windows Server
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc4a4971-f727-40cd-91f5-2ee6d24b54cb
author: KBDAzure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 97fb1b9003705ba8ad26c2b3e71eda34e88642ee
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812617"
---
# <a name="system-requirements-for-hyper-v-on-windows-server"></a>Systemanforderungen für Hyper-V unter Windows Server

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Hyper-V gelten bestimmte Hardware, und einige Hyper-V-Funktionen verfügen über zusätzliche Anforderungen. Verwenden Sie die Details in diesem Artikel, um zu entscheiden, welche Anforderungen Ihr System erfüllen muss, um Hyper-V die Möglichkeit zu verwenden, der Sie möchten. Überprüfen Sie dann die [Windows Server-Katalog](https://www.windowsservercatalog.com/). Bedenken Sie, dass die Anforderungen für Hyper-V die allgemeine Mindestanforderungen für Windows Server 2016 überschreiten, da es sich bei eine Virtualisierungsumgebung mehr Computerressourcen erfordert.

Wenn Sie bereits Hyper-V verwenden, ist es wahrscheinlich, dass Sie die vorhandene Hardware verwenden können. Die allgemeine hardwareanforderungen wurden deutlich von Windows Server 2012 R2 nicht geändert.  Allerdings benötigen Sie neueren Hardware zu verwenden, die abgeschirmte VMs oder diskrete gerätezuordnung. Diese Funktionen basieren auf bestimmten Hardware-Support, wie unten beschrieben. Davon abgesehen ist der Hauptunterschied besteht darin, in der Hardware die Adresse der zweiten Ebene Translation (SLAT) ist jetzt erforderlich, nicht empfohlen.

Informationen zur maximal unterstützten Konfigurationen für Hyper-V, z. B. die Anzahl der ausgeführten virtuellen Computern finden Sie unter [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md). Die Liste der Betriebssysteme, die Sie, auf Ihren virtuellen Computern ausführen können finden Sie im [unterstützt Windows-Gastbetriebssysteme für Hyper-V unter Windows Server](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md).

## <a name="general-requirements"></a>Allgemeine Anforderungen

Unabhängig von der Hyper-V-Features, die Sie verwenden möchten, benötigen Sie Folgendes:

- Eine 64-Bit-Prozessor mit Second-Level-Adressübersetzung (SLAT). Um die Hyper-V-Virtualisierung-Komponenten wie z.B. Windows Hypervisor installieren zu können, muss der Prozessor SLAT verfügen. Allerdings ist es nicht erforderlich, um Hyper-V-Verwaltungstools wie die Verbindung mit virtuellen Computern (VMConnect), Hyper-V-Manager und Hyper-V-Cmdlets für Windows PowerShell zu installieren. Finden Sie unten unter "Gewusst wie: Überprüfen Sie für Hyper-V-Anforderungen", um zu ermitteln, ob Sie den Prozessor hat SLAT.

- VM Monitor Mode extensions

- Genügend Arbeitsspeicher - Plan für *mindestens* 4 GB RAM. Mehr Arbeitsspeicher ist besser. Sie benötigen genügend Speicher für den Host und alle virtuellen Computer, die zur gleichen Zeit ausgeführt werden soll.

- Virtualisierungsunterstützung im BIOS oder UEFI aktiviert:

  - Hardwareunterstützte Virtualisierung. Dies ist in Prozessoren, die eine Virtualisierungsoption – insbesondere Prozessoren mit Intel Virtualization Technology (Intel VT) oder AMD Virtualization (AMD-V)-Technologie verfügbar.

  - Von der Hardware erzwungene Datenausführungsverhinderung (DEP) muss verfügbar und aktiviert sein. Für Intel-Systemen, ist dies die XD-Bit (execute Disable Bit). AMD-Systeme ist dies das NX-Bit (keine Execute Bit).

## <a name="how-to-check-for-hyper-v-requirements"></a>So prüfen Sie für Hyper-V-Anforderungen

Öffnen Sie Windows PowerShell oder eine Eingabeaufforderung und geben:

```cmd
Systeminfo.exe
```

Scrollen Sie zum Abschnitt Hyper-V-Anforderungen, um den Bericht zu überprüfen.

## <a name="requirements-for-specific-features"></a>Anforderungen für bestimmte Funktionen

Hier sind die Anforderungen für die diskrete gerätezuordnung und geschützten virtuellen Maschinen ein. Beschreibungen dieser Funktionen finden Sie [Neues in Hyper-V unter Windows Server](What-s-new-in-Hyper-V-on-Windows.md).

### <a name="discrete-device-assignment"></a>Diskrete gerätezuordnung

**Host** Anforderungen sind vergleichbar mit der vorhandenen Anforderungen für die SR-IOV-Funktion in Hyper-V.

- Der Prozessor muss es sich um entweder Intel Extended Seite Tabelle (EPT) oder AMD geschachtelte Seite Tabelle (NPT) verfügen.

- Der Chipsatz benötigen:

  - Unterbrechen Sie die neuzuordnung - Intel VT-d mit der Funktion unterbrechen Neuzuordnung (VT-d2) oder eine beliebige Version von AMD-e/a-Speicherverwaltungseinheit (MMU e/a).

  - Neuzuordnen von DMA - Intel VT-d mit Invalidierungen in die Warteschlange eingereiht oder alle AMD-e/a-MMU.

  - Zugriffssteuerungsdienste (ACS) auf der PCI Express-root-Ports.

- Die Firmware-Tabellen müssen die e/a-MMU an den Windows-Hypervisor verfügbar machen. Beachten Sie, dass diese Funktion in der UEFI oder BIOS deaktiviert werden kann. Anleitungen hierzu finden Sie in der Hardwaredokumentation, oder wenden Sie sich an Ihren Hardwarehersteller.

**Geräte** muss express GPU oder nicht flüchtigen Speicher (NVMe). Für GPU unterstützt nur bestimmte Geräte diskrete gerätezuordnung an. Um zu überprüfen, finden Sie in der Hardwaredokumentation, oder wenden Sie sich an Ihren Hardwarehersteller. Ausführliche Informationen zu dieser Funktion, wie Sie es und Überlegungen zu verwenden, finden Sie im Beitrag "[diskrete Gerätezuordnung – Beschreibung und Hintergrund](https://blogs.technet.com/b/virtualization/archive/2015/11/19/discrete-device-assignment.aspx)" in der Blog zum Thema Virtualisierung.

### <a name="shielded-virtual-machines"></a>Abgeschirmte VMs

Diese virtuellen Computer basieren auf Virtualisierung basierende Sicherheitsverfahren und sind ab Windows Server 2016 verfügbar.

**Host** Anforderungen sind:

- UEFI 2.3. 1 c - unterstützt sichere, kontrollierter Start

  Die folgenden zwei sind im Allgemeinen für die virtualisierungsbasierte Sicherheit optional, jedoch für den Host erforderlich, wenn Sie den Schutz wünschen, die, den diese Features bieten:

- TPM-v2. 0 - schützt Bestand der Plattform-Sicherheit
- UNTERSTÜTZT (Intel VT-D): damit der Hypervisor direct Memory Access (DMA) Schutz bereitstellen können

**VM** Anforderungen sind:

- Zweite Generation
- WindowsServer 2012 oder höher als Gastbetriebssystem

