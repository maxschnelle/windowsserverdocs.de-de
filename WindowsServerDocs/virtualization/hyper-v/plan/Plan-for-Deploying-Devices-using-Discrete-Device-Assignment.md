---
title: Plan für die Bereitstellung von Geräten verwenden diskrete Gerätezuordnung
description: Erfahren Sie mehr über die Funktionsweise der DDA in Windows Server
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 02/06/2018
ms.openlocfilehash: c64c2b75c00f97622278c3e590db46995e108218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840201"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung
>Gilt für: Microsoft Hyper-V Server 2016, WindowsServer 2016 wird Microsoft Hyper-V-Server 2019, WindowsServer 2019

Diskrete Gerätezuordnung können physischen Hardware PCIe direkt über auf einem virtuellen Computer zugegriffen werden.  Dieses Handbuch wird erläutert, den Typ der Geräte, die verwenden können, dass Sie diskrete Gerätezuordnung, Systemanforderungen, Einschränkungen, die auf den virtuellen Computer sowie die sicherheitsauswirkungen der diskrete Gerätezuordnung.

Für diskrete Gerätezuordnung Veröffentlichung haben wir zwei Geräteklassen offiziell von Microsoft unterstützt werden müssen sich der Fokus auf: Grafikkarten und NVMe-Speicher Geräte.  Andere Geräte sind anzunehmen, dass und Hardwareanbieter können Anweisungen der Unterstützung für diese Geräte bieten.  Für diese wenden andere Geräte, bitte Sie sich an die Hardwareanbieter für die Unterstützung.

Wenn Sie diskrete Gerätezuordnung ausprobieren möchten, können Sie direkt über zum [Bereitstellung von Grafiken Geräte verwenden diskrete Gerätezuordnung](../deploy/Deploying-graphics-devices-using-dda.md) oder [bereitstellen Speichergeräte verwenden diskrete Gerätezuordnung](../deploy/Deploying-storage-devices-using-dda.md) um zu beginnen!

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>Unterstützten virtuellen Computern und Gastbetriebssystemen
Diskrete Gerätezuordnung wird für die Generation 1 oder 2 virtuellen Computern unterstützt.  Darüber hinaus enthalten die Gäste unterstützt, Windows 10, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2 mit [KB 3133690](https://support.microsoft.com/kb/3133690) angewendet, und verschiedenen Distributionen von der [Linux-Betriebssystem.](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)

## <a name="system-requirements"></a>Systemanforderungen
Zusätzlich zu den [System Requirements for Windows Server](../../../get-started/System-Requirements--and-Installation.md) und [Systemanforderungen für Hyper-V](../System-requirements-for-Hyper-V-on-Windows.md), diskrete Gerätezuordnung, erfordert Klasse Serverhardware, die gewähren kann die Betriebssystem-Kontrolle über die Konfiguration des PCIe-Fabrics (Native PCI Express-Steuerelement). Darüber hinaus enthält die PCIe Stamm komplexe, zur Unterstützung von "Access Control Services" (ACS), die Hyper-V zu erzwingen, dass alle PCIe-Datenverkehr über die e/a-MMU ermöglicht.

Diese Funktionen werden in der Regel werden nicht direkt in das BIOS auf dem Server verfügbar gemacht und sind oft hinter der anderen Einstellungen.  Beispielsweise die gleichen Funktionen für die SR-IOV-Unterstützung erforderlich sind und in das BIOS müssen Sie möglicherweise festlegen "SR-IOV zu aktivieren."  Bitte wenden Sie sich an den Hersteller Ihres Systems, wenn Sie nicht die richtige Einstellung im BIOS identifizieren können.

Helfen sicherzustellen, dass die Hardware die Hardware kann diskrete Gerätezuordnung, unsere Techniker haben zusammengestellt, die eine [Computer Profilskript](#machine-profile-script) , Sie, auf einem aktiviertem Hyper-V-Host ausführen können zu testen, ob Ihr Server ordnungsgemäß Setup- und was ist Geräte können diskrete Gerätezuordnung.

## <a name="device-requirements"></a>Anforderungen für Geräte
Nicht alle PCIe-Geräte kann mit diskrete Gerätezuordnung verwendet werden.  Beispielsweise werden die ältere Geräten, die ältere (INTx) PCI unterbricht nutzen nicht unterstützt. Jake Oshins [Blogbeiträge](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/) ausführlicher - jedoch wechseln Sie für den Consumer ein, mit der [Computer Profilskript](#machine-profile-script) wird angezeigt, welche Geräte verwendet werden, für die diskrete Gerätezuordnung kann sind.

Gerätehersteller können Sie ihren Microsoft-Vertreter, um mehr erreichen.

## <a name="device-driver"></a>Gerätetreiber
Diskrete Gerätezuordnung das gesamte PCIe-Gerät in der Gast-VM übergibt, ist ein Host-Treiber nicht erforderlich, bevor das Gerät bereitgestellt wird, auf dem virtuellen Computer installiert werden.  Die einzige Anforderung besteht, auf dem Host ist, die des Geräts die [PCIe-Location-Path](#pcie-location-path) bestimmt werden kann.  Das Gerät die Treiber kann optional installiert werden, wenn dies beim Identifizieren des Geräts hilft.  Beispielsweise kann eine GPU, ohne die Gerätetreiber auf dem Host installiert als Microsoft grundlegenden Rendern Gerät angezeigt.  Wenn der Gerätetreiber installiert ist, werden die Hersteller und Modell wahrscheinlich angezeigt.

Sobald das Gerät auf dem Gast bereitgestellt ist, kann der Hersteller des Gerätetreibers jetzt wie üblich, in dem virtuellen Gastcomputer installiert werden.  

## <a name="virtual-machine-limitations"></a>VM-Einschränkungen
Aufgrund der Natur der Implementierung von diskrete Gerätezuordnung sind einige Features von einem virtuellen Computer beschränkt, während ein Gerät angeschlossen ist.  Die folgenden Funktionen sind nicht verfügbar:
- VM-speichern/wiederherstellen
- Livemigration eines virtuellen Computers
- Die Verwendung des dynamischen Arbeitsspeichers
- Hinzufügen des virtuellen Computers zu einem Cluster für hohe Verfügbarkeit (HA)

## <a name="security"></a>Sicherheit
Diskrete Gerätezuordnung übergibt das gesamte Gerät, auf dem virtuellen Computer.  Dies bedeutet, dass alle Funktionen des Geräts aus dem Gast-Betriebssystem zugänglich sind. Einige Funktionen, wie die Firmware aktualisieren, können sich negativ auf die Stabilität des Systems beeinträchtigen. Daher sind viele Warnungen, die dem Administrator angezeigt, wenn es sich bei Aufheben der Bereitstellung des Geräts auf dem Host. Es wird dringend empfohlen, dass diskrete Gerätezuordnung nur verwendet wird, in denen die Mandanten der virtuellen Computer als vertrauenswürdig gelten.  

Wenn der Administrator ein Gerät mit einem nicht vertrauenswürdigen Mandanten verwenden möchte, haben wir den Gerätehersteller bereitgestellt, mit der Möglichkeit, einen Treiber für die Gerät-Lösung zu erstellen, der auf dem Host installiert werden können.  Wenden Sie sich an den Gerätehersteller, Einzelheiten gibt an, ob sie einen Gerätetreiber für die Lösung bereitstellen.

Wenn Sie möchten die sicherheitsüberprüfungen für ein Gerät zu umgehen, die nicht über einen Gerätetreiber für die Lösung verfügt, müssen Sie übergeben die `-Force` Parameter, um die `Dismount-VMHostAssignableDevice` Cmdlet.  Beachten Sie, dass dadurch das Sicherheitsprofil des Systems geändert haben und dies ist nur während der Erstellung von Prototypen empfohlen oder vertrauenswürdigen Umgebungen.

## <a name="pcie-location-path"></a>PCIe-Location-Path
Der Pfad zum Speicherort der PCIe ist erforderlich, Aufheben der Bereitstellung erstellt und das Gerät vom Host eingebunden.  Ein Speicherortpfad Beispiel sieht wie folgt: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.   Die [Computer Profilskript](#machine-profile-script) wird auch der Pfad zum Speicherort des Geräts PCIe zurückgeben.

### <a name="getting-the-location-path-by-using-device-manager"></a>Abrufen des Pfads zum Speicherort mit Geräte-Manager
![Geräte-Manager](../deploy/media/dda-devicemanager.png)
- Öffnen Sie die Geräte-Manager, und suchen Sie das Gerät.  
- Klicken Sie mit der rechten Maustaste auf das Gerät, und wählen Sie "Eigenschaften".
- Navigieren Sie zur Registerkarte "Details", und wählen Sie in der Dropdownliste für Eigenschaft "Location-Paths".  
- Klicken Sie mit der rechten Maustaste auf den Eintrag, der mit "PCIROOT" beginnt, und wählen Sie "Kopieren".  Sie haben jetzt den Pfad zum Speicherort für das Gerät.

## <a name="mmio-space"></a>MMIO-Speicher
Bei einigen Geräten, insbesondere GPUs, erfordern zusätzlichen MMIO Speicherplatz mit dem virtuellen Computer für den Speicher des Geräts zugegriffen werden. Standardmäßig beginnt jede VM mit 128MB wenig MMIO-Speicherplatz und 512MB hohe MMIO-Speicherplatz zugeordnet. Jedoch ein Gerät möglicherweise mehr MMIO-Speicherplatz benötigt wird, oder mehrere Geräte können durch übergeben werden, so, dass die kombinierten Anforderungen diese Werte überschreiten.  Ändern die MMIO-Speicher ist unkompliziert und in PowerShell mithilfe der folgenden Befehle ausgeführt werden kann:

```
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```
Die einfachste Möglichkeit, um zu bestimmen, wie viel Speicherplatz MMIO zuweisen ist die Verwendung der [Computer Profilskript](#machine-profile-script).  Alternativ können Sie mit der Geräte-Manager berechnen. Sie finden Sie im TechNet-Blogbeitrag [diskrete Gerätezuordnung - GPUs](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/) Weitere Details.

## <a name="machine-profile-script"></a>Computer-Profilskript
Um zu vereinfachen, angibt, ob der Server ordnungsgemäß konfiguriert ist und welche Geräte übergeben werden, durch die Verwendung von diskrete Gerätezuordnung verfügbar sind, zusammengestellt, die eine der unsere Techniker das folgende PowerShell-Skript: [SurveyDDA.ps1.](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1)

Vor der Verwendung des Skripts, vergewissern Sie sich die Hyper-V-Rolle installiert haben, und führen Sie das Skript in einem PowerShell-Befehlsfenster, das über Administratorrechte verfügt.

Wenn das System zur Unterstützung von diskrete Gerätezuordnung falsch konfiguriert ist, zeigt das Tool eine Fehlermeldung angezeigt, was falsch ist. Findet das Tool das System ordnungsgemäß konfiguriert sind, werden alle Geräte aufgezählt, die auf dem PCIe-Bus gefunden werden kann.

Für jedes Gerät, die sie findet, zeigt das Tool, ob es mit diskrete Gerätezuordnung verwendet werden kann. Wenn ein Gerät als kompatibel mit diskrete Gerätezuordnung identifiziert wird, wird das Skript einen Grund angeben.  Wenn ein Gerät als kompatibel erfolgreich identifiziert wird, wird der Pfad zum Speicherort des Geräts angezeigt.  Darüber hinaus, wenn das Gerät erfordert [MMIO-Speicher](#mmio-space), er wird auch angezeigt werden.

![SurveyDDA.ps1](./images/hyper-v-surveydda-ps1.png)

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="how-does-remote-desktops-remotefx-vgpu-technology-relate-to-discrete-device-assignment"></a>In welcher Beziehung steht Remote Desktop RemoteFX vGPU-Technologie auf diskrete Gerätezuordnung?
Sie sind vollständig separate Technologien. RemoteFX vGPU muss nicht für die diskrete Gerätezuordnung funktioniert installiert werden. Darüber hinaus sind ohne zusätzlichen Rollen muss installiert sein. RemoteFX vGPU erfordert die RDVH-Rolle für die Installation in der Reihenfolge für den RemoteFX vGPU-Treiber auf dem virtuellen Computer vorhanden sein. Für diskrete Gerätezuordnung da Sie der Hardwarehersteller Treiber in der virtuellen Maschine installieren möchten, ohne zusätzlichen Rollen müssen vorhanden sein.  

### <a name="ive-passed-a-gpu-into-a-vm-but-remote-desktop-or-an-application-isnt-recognizing-the-gpu"></a>Ich habe eine GPU übergeben, in einen virtuellen Computer jedoch Remotedesktop oder eine Anwendung ist nicht die GPU erkennen
Es gibt zahlreiche Gründe, warum dies kann passieren, aber einige allgemeine Probleme sind unten aufgeführt.
- Stellen Sie sicher die neuesten GPU-Hersteller Treiber installiert ist, und meldet einen Fehler nicht durch Überprüfen des Gerätestatus im Geräte-Manager.
- Stellen Sie sicher, das Gerät verfügt über genug [MMIO-Speicher](#mmio-space) für dieses Volume auf dem virtuellen Computer zugewiesene.
- Stellen Sie sicher, dass Sie eine GPU verwenden, die der Anbieter in dieser Konfiguration unterstützt verwendet wird. Beispielsweise verhindern, dass einige Anbieter ihre Consumer Karten arbeiten, die bei der Übergabe an einen virtuellen Computer.
- Vergewissern Sie sich die Anwendung ausgeführt wird, unterstützt die Ausführung auf einem virtuellen Computer, und dass sowohl die GPU als auch die zugehörigen Treiber von der Anwendung unterstützt werden. Einige Anwendungen verfügen über Whitelists mit GPUs und Umgebungen.
- Wenn Sie die Remote Desktop Session Host-Rolle oder Windows Multipoint Services auf dem Gast verwenden, müssen Sie sicherstellen, dass für ein bestimmten Eintrag für die Gruppenrichtlinie festgelegt ist, um die Verwendung des standardmäßigen GPU zulassen. Verwenden ein Gruppenrichtlinienobjekt angewendet, auf dem Gast (oder den Editor für lokale Gruppenrichtlinien auf dem Gast), navigieren Sie zum folgenden Element der Gruppenrichtlinie:
   - Computerkonfiguration
   - Administrator-Vorlagen
   - Windows-Komponenten
   - Remotedesktopdienste
   - Remotedesktop-Sitzungshost
   - Remotesitzung-Umgebung
   - Verwenden der Grafikkarte des Hardware-Standard für alle Remotedesktopdienste-Sitzungen

    Dieser Wert auf aktiviert festgelegt, und starten Sie den virtuellen Computer neu, nachdem die Richtlinie angewendet wurde.

### <a name="can-discrete-device-assignment-take-advantage-of-remote-desktops-avc444-codec"></a>Können diskrete Gerätezuordnung Remote Desktop AVC444 Codec nutzen?
Ja, besuchen Sie diesen Blogbeitrag, um weitere Informationen ein: [Remote Desktop Protocol (RDP) 10 AVC/H.264-Verbesserungen in Windows 10 und Windows Server 2016 Technical Preview.](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

### <a name="can-i-use-powershell-to-get-the-location-path"></a>Kann ich PowerShell verwenden, um den Pfad zum Speicherort zu erhalten?
Ja, es gibt verschiedene Möglichkeiten zur Verfügung. Es folgt ein Beispiel aus:
```
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
```

### <a name="can-discrete-device-assignment-be-used-to-pass-a-usb-device-into-a-vm"></a>Kann diskrete Gerätezuordnung, übergeben ein USB-Gerät auf einem virtuellen Computer werden verwendet?
Jedoch nicht offiziell unterstützt, haben Kunden diskrete Gerätezuordnung verwendet, dies, indem Sie den gesamten USB3 Controller auf einem virtuellen Computer übergeben.  Wie in der gesamte Controller übergeben wird, werden jede USB-Gerät angeschlossen, Controller auch auf dem virtuellen Computer zugegriffen werden kann.  Beachten Sie, dass nur einige USB3 Controller funktioniert möglicherweise USB2 Controller können nicht mit diskrete Gerätezuordnung verwendet werden.
