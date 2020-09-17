---
title: System Anforderungen für Hyper-V unter Windows Server
description: Listet die Hardware-und Firmwareanforderungen für Hyper-V in Windows Server auf.
ms.topic: article
ms.assetid: bc4a4971-f727-40cd-91f5-2ee6d24b54cb
ms.author: benarm
author: BenjaminArmstrong
ms.date: 9/30/2016
ms.openlocfilehash: f56d6476bbe3db49b220f6e1652ea099b97e7108
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746715"
---
# <a name="system-requirements-for-hyper-v-on-windows-server"></a>System Anforderungen für Hyper-V unter Windows Server

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Für Hyper-v gelten bestimmte Hardwareanforderungen, und einige Hyper-v-Features haben zusätzliche Anforderungen. Verwenden Sie die Details in diesem Artikel, um zu entscheiden, welche Anforderungen Ihr System erfüllen muss, damit Sie Hyper-V wie geplant verwenden können. Überprüfen Sie anschließend den [Windows Server-Katalog](https://www.windowsservercatalog.com/). Beachten Sie, dass die Anforderungen für Hyper-V die allgemeinen Mindestanforderungen für Windows Server 2016 überschreiten, da eine Virtualisierungsumgebung mehr computeressourcen erfordert.

Wenn Sie Hyper-V bereits verwenden, ist es wahrscheinlich, dass Sie Ihre vorhandene Hardware verwenden können. Die allgemeinen Hardwareanforderungen wurden von Windows Server 2012 R2 nicht signifikant geändert.  Sie benötigen jedoch neuere Hardware, um abgeschirmte virtuelle Computer oder eine diskrete Geräte Zuweisung zu verwenden. Diese Features basieren auf einer bestimmten Hardwareunterstützung, wie unten beschrieben. Der wichtigste Unterschied bei der Hardware besteht darin, dass die Adressübersetzung (slat) der zweiten Ebene jetzt anstelle von "empfohlen" erforderlich ist.

Ausführliche Informationen zu den maximal unterstützten Konfigurationen für Hyper-v, wie z. b. die Anzahl der aktiven virtuellen Maschinen, finden Sie unter [Planen der Hyper-v-Skalierbarkeit in Windows Server 2016](./plan/plan-hyper-v-scalability-in-windows-server.md). Die Liste der Betriebssysteme, die Sie auf Ihren virtuellen Computern ausführen können, finden Sie [unter Unterstützte Windows-Gast Betriebssysteme für Hyper-V unter Windows Server](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md).

## <a name="general-requirements"></a>Allgemeine Anforderungen

Unabhängig von den Hyper-V-Features, die Sie verwenden möchten, benötigen Sie Folgendes:

- Ein 64-Bit-Prozessor mit Adressübersetzung der zweiten Ebene (Address Translation, slat). Zum Installieren der Hyper-V-Virtualisierungskomponenten, z. b. Windows-Hypervisor, muss der Prozessor über slat verfügen. Es ist jedoch nicht erforderlich, Hyper-v-Verwaltungs Tools wie die Verbindung mit virtuellen Computern (VMConnect), den Hyper-v-Manager und die Hyper-v-Cmdlets für Windows PowerShell zu installieren. Weitere Informationen finden Sie unter "Vorgehensweise beim Überprüfen der Hyper-V-Anforderungen" unten, um zu ermitteln, ob Ihr Prozessor slat hat.

- Erweiterungen des VM-Monitor Modus

- Ausreichender Speicher Plan für mindestens *4 GB* RAM. Mehr Arbeitsspeicher ist besser. Für den Host und alle virtuellen Computer, die Sie gleichzeitig ausführen möchten, benötigen Sie ausreichend Arbeitsspeicher.

- Virtualisierungsunterstützung im BIOS oder UEFI aktiviert:

  - Hardwaregestützte Virtualisierung. Dies ist in Prozessoren verfügbar, die eine Virtualisierungsoption enthalten, insbesondere Prozessoren mit Intel-Virtualisierungstechnologie (Intel VT) oder AMD Virtualization (AMD-V)-Technologie.

  - Die auf der Hardware erzwungene Datenausführungsverhinderung (Data Execution Protection, DEP) muss verfügbar und aktiviert sein. Bei Intel-Systemen ist dies das XD-Bit (Execute Disable-Bit). Bei AMD-Systemen ist dies das NX-Bit (No Execute-Bit).

## <a name="how-to-check-for-hyper-v-requirements"></a>Überprüfen der Hyper-V-Anforderungen

Öffnen Sie Windows PowerShell oder eine Eingabeaufforderung, und geben Sie Folgendes ein:

```cmd
Systeminfo.exe
```

Scrollen Sie zum Abschnitt "Hyper-V-Anforderungen", um den Bericht zu überprüfen.

## <a name="requirements-for-specific-features"></a>Anforderungen für bestimmte Features

Dies sind die Anforderungen für die diskrete Geräte Zuweisung und geschützte virtuelle Computer. Beschreibungen dieser Features finden Sie unter [Neues in Hyper-V unter Windows Server](What-s-new-in-Hyper-V-on-Windows.md).

### <a name="discrete-device-assignment"></a>Diskrete Geräte Zuweisung

Die **Host** Anforderungen ähneln den vorhandenen Anforderungen für die SR-IOV-Funktion in Hyper-v.

- Der Prozessor muss entweder die erweiterte Seiten Tabelle (EPT) von Intel oder die Nested Page Table (Atom) der AMD (Nested Page Table) enthalten.

- Der Chipsatz muss Folgendes aufweisen:

  - Neuzuordnung unterbrechen: die VT-d von Intel mit der Funktion zum Neuzuordnen von Unterbrechungen (VT-D2) oder eine beliebige Version der AMD-e/a-Speicherverwaltungseinheit (e/a-MMU).

  - DMA-Neuzuordnung: die VT-d von Intel mit Invalidierungen in der Warteschlange oder eine beliebige AMD-e/a-MMU.

  - Zugriffs Steuerungs Dienste (ACS) auf PCI Express-stammports.

- In den firmwaretabellen muss das e/a-MMU für den Windows-Hypervisor verfügbar gemacht werden. Beachten Sie, dass diese Funktion in UEFI oder BIOS deaktiviert werden kann. Anweisungen finden Sie in der Hardware Dokumentation, oder wenden Sie sich an den Hardwarehersteller.

**Geräte** benötigen GPU oder Non-volatile Memory Express (nvme). Bei GPU unterstützen nur bestimmte Geräte die diskrete Geräte Zuweisung. Informationen zur Überprüfung finden Sie in der Hardware Dokumentation, oder wenden Sie sich an den Hardwarehersteller Ausführliche Informationen zu diesem Feature, einschließlich der Verwendungsweise und Überlegungen, finden Sie im Beitrag "[diskrete Geräte Zuweisung--Beschreibung und Hintergrund](https://blogs.technet.com/b/virtualization/archive/2015/11/19/discrete-device-assignment.aspx)" im virtualisierungsblog.

### <a name="shielded-virtual-machines"></a>Abgeschirmte VMs

Diese virtuellen Computer basieren auf virtualisierungsbasierter Sicherheit und sind ab Windows Server 2016 verfügbar.

Die **Host** Anforderungen lauten:

- UEFI 2.3.1 c: unterstützt sicheren, gemessenen Start

  Die folgenden beiden sind optional für die virtualisierungsbasierte Sicherheit im Allgemeinen, aber für den Host erforderlich, wenn Sie den Schutz der Features gewährleisten möchten:

- TPM v 2.0: schützt Platt Form sicherheitsassets
- IOMMU (Intel VT-D): der Hypervisor kann somit den Zugriff auf den direkten Speicher (DMA) bereitstellen.

Anforderungen an **virtuelle Computer** :

- Generation 2
- Windows Server 2012 oder höher als Gast Betriebssystem