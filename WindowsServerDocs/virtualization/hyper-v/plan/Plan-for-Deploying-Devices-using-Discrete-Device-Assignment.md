---
title: Planen der Bereitstellung von Geräten mit diskreter Geräte Zuweisung
description: Weitere Informationen zur Funktionsweise von DDA in Windows Server
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 02/06/2018
ms.openlocfilehash: 7df7dbd1e7252f5bab451ed9272f9cbede63d223
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476496"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>Planen der Bereitstellung von Geräten mit diskreter Geräte Zuweisung
>Gilt für: Microsoft Hyper-v Server 2016, Windows Server 2016, Microsoft Hyper-v Server 2019, Windows Server 2019

Durch die diskrete Geräte Zuweisung kann auf physische PCIe-Hardware direkt von einem virtuellen Computer aus zugegriffen werden.  In diesem Leitfaden werden die Arten von Geräten erläutert, die diskrete Geräte Zuweisungen, Host Systemanforderungen, Einschränkungen der virtuellen Computer sowie Sicherheitsauswirkungen der diskreten Geräte Zuweisung verwenden können.

Bei der erstmaligen Veröffentlichung einer diskreten Geräte Zuweisung haben wir uns auf zwei Geräteklassen konzentriert, die von Microsoft formal unterstützt werden: Grafikadapter und nvme-Speichergeräte.  Andere Geräte sind wahrscheinlich funktionsfähig, und Hardware Anbieter können Unterstützung für diese Geräte anbieten.  Wenden Sie sich für diese anderen Geräte an diese Hardware Anbieter, um Unterstützung zu erhalten.

Wenn Sie zum Testen der diskreten Geräte Zuweisung bereit sind, können Sie zum Einstieg zum Bereitstellen von [Grafik Geräten mithilfe einer diskreten Geräte Zuweisung](../deploy/Deploying-graphics-devices-using-dda.md) oder Bereitstellen von [Speichergeräten mithilfe von diskreten Geräte Zuweisungen](../deploy/Deploying-storage-devices-using-dda.md) wechseln.

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>Unterstützte Virtual Machines und Gast Betriebssysteme
Für VMS der Generation 1 oder 2 wird eine diskrete Geräte Zuweisung unterstützt.  Zu den unterstützten Gästen zählen zusätzlich Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 mit angewendetem [KB 3133690](https://support.microsoft.com/kb/3133690) und verschiedene Verteilungen des [Linux-Betriebssystems.](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)

## <a name="system-requirements"></a>Systemanforderungen
Zusätzlich zu den [Systemanforderungen für Windows Server](../../../get-started/System-Requirements--and-Installation.md) und den [Systemanforderungen für Hyper-V](../System-requirements-for-Hyper-V-on-Windows.md)erfordert die diskrete Geräte Zuweisung Server Klassen Hardware, die die Betriebs System Steuerung über das Konfigurieren des PCIe erteilen kann. Fabric (System eigenes PCI Express-Steuerelement). Außerdem muss das komplexe PCIe-Stammverzeichnis "Access Control Services (ACS)" unterstützen, mit dem Hyper-V den gesamten PCIe-Datenverkehr über die e/a-MMU erzwingen kann.

Diese Funktionen werden in der Regel nicht direkt im BIOS des Servers verfügbar gemacht und sind häufig hinter anderen Einstellungen verborgen.  Beispielsweise sind die gleichen Funktionen für die SR-IOV-Unterstützung erforderlich, und im BIOS müssen Sie möglicherweise "SR-IOV aktivieren" festlegen.  Wenden Sie sich an Ihren Systemhersteller, wenn Sie die richtige Einstellung in Ihrem BIOS nicht identifizieren können.

Um sicherzustellen, dass die Hardware von der Hardware diskret Geräte zugewiesen werden kann, haben unsere Techniker ein [Machine profile-Skript](#machine-profile-script) eingefügt, das Sie auf einem Hyper-V-fähigen Host ausführen können, um zu testen, ob der Server ordnungsgemäß eingerichtet ist und welche Geräte in der Lage sind. Diskrete Geräte Zuweisung.

## <a name="device-requirements"></a>Geräteanforderungen
Nicht jedes PCIe-Gerät kann mit diskreter Geräte Zuweisung verwendet werden.  Beispielsweise werden ältere Geräte, die Legacy-PCI-Interrupts (intX) nutzen, nicht unterstützt. Die [Blogbeiträge](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/) von Jake Oshin werden ausführlicher behandelt, aber für den Consumer wird bei der Ausführung des [Machine profile-Skripts](#machine-profile-script) angezeigt, welche Geräte für die diskrete Geräte Zuweisung eingesetzt werden können.

Gerätehersteller können sich an Ihren Microsoft-Vertreter wenden, um weitere Informationen zu erhalten.

## <a name="device-driver"></a>Gerätetreiber
Da die diskrete Geräte Zuweisung das gesamte PCIe-Gerät an die Gast-VM übergibt, muss vor dem Bereitstellen des Geräts innerhalb des virtuellen Computers kein Host Treiber installiert werden.  Die einzige Voraussetzung für den Host ist, dass der [PCIe-Speicherort Pfad](#pcie-location-path) des Geräts bestimmt werden kann.  Der Treiber des Geräts kann optional installiert werden, wenn dies zur Identifizierung des Geräts beiträgt.  Beispielsweise wird eine GPU, auf der der Gerätetreiber auf dem Host installiert ist, möglicherweise als Microsoft Basic-Rendering-Gerät angezeigt.  Wenn der Gerätetreiber installiert ist, werden der Hersteller und das Modell wahrscheinlich angezeigt.

Nachdem das Gerät innerhalb des Gast Betriebssystems bereitgestellt wurde, kann der Gerätetreiber des Herstellers jetzt wie üblich innerhalb des virtuellen Gast Computers installiert werden.  

## <a name="virtual-machine-limitations"></a>Einschränkungen für virtuelle Computer
Aufgrund der Art, wie die diskrete Geräte Zuweisung implementiert ist, werden einige Features eines virtuellen Computers eingeschränkt, während ein Gerät angefügt wird.  Die folgenden Funktionen sind nicht verfügbar:
- Speichern/Wiederherstellen virtueller Computer
- Live Migration eines virtuellen Computers
- Die Verwendung von dynamischem Arbeitsspeicher
- Hinzufügen des virtuellen Computers zu einem hoch Verfügbarkeits Cluster (ha)

## <a name="security"></a>Sicherheit
Die diskrete Geräte Zuweisung übergibt das gesamte Gerät an den virtuellen Computer.  Dies bedeutet, dass alle Funktionen dieses Geräts über das Gast Betriebssystem zugänglich sind. Einige Funktionen, wie z. b. Firmwareupdates, können sich negativ auf die Stabilität des Systems auswirken. Daher werden dem Administrator beim Aufheben der Einbindung des Geräts vom Host zahlreiche Warnungen angezeigt. Es wird dringend empfohlen, die diskrete Geräte Zuweisung nur dann zu verwenden, wenn die Mandanten der VMS vertrauenswürdig sind.  

Wenn der Administrator ein Gerät mit einem nicht vertrauenswürdigen Mandanten verwenden möchte, haben wir Geräteherstellern die Möglichkeit gegeben, einen geräteentschärfungs-Treiber zu erstellen, der auf dem Host installiert werden kann.  Wenden Sie sich an den Gerätehersteller, um zu erfahren, ob er einen Geräte Entschärfungs Treiber bereitstellt.

Wenn Sie die Sicherheitsüberprüfungen für ein Gerät umgehen möchten, das keinen Treiber für die Geräte Entschärfung hat, müssen Sie den `-Force` Parameter an das `Dismount-VMHostAssignableDevice` Cmdlet übergeben.  Dabei haben Sie sich bewusst, dass Sie das Sicherheitsprofil des Systems geändert haben und dies nur während der Erstellung von Prototypen oder vertrauenswürdigen Umgebungen empfohlen wird.

## <a name="pcie-location-path"></a>PCIe-Speicherort Pfad
Der Pfad für den PCIe-Speicherort ist erforderlich, um das Gerät vom Host zu entfernen und zu binden.  Ein Beispiel für einen Speicherort Pfad sieht wie `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`folgt aus:.   Das [Computer Profil Skript](#machine-profile-script) gibt auch den Speicherort Pfad des PCIe-Geräts zurück.

### <a name="getting-the-location-path-by-using-device-manager"></a>Der Speicherort Pfad wird mithilfe Geräte-Manager
![Geräte-Manager](../deploy/media/dda-devicemanager.png)
- Öffnen Sie Geräte-Manager, und suchen Sie nach dem Gerät.  
- Klicken Sie mit der rechten Maustaste auf das Gerät und wählen Sie "Eigenschaften"
- Navigieren Sie zur Registerkarte Details, und wählen Sie in der Dropdown-Eigenschaft die Option "Location Path" aus.  
- Klicken Sie mit der rechten Maustaste auf den Eintrag, der mit pciroot beginnt, und wählen Sie "Kopieren".  Sie verfügen nun über den Speicherort Pfad für das Gerät.

## <a name="mmio-space"></a>MMIO-Speicherplatz
Einige Geräte, insbesondere GPUs, erfordern zusätzlichen MMIO-Speicherplatz, der dem virtuellen Computer zugeordnet werden muss, damit der Arbeitsspeicher des Geräts zugänglich ist. Standardmäßig beginnt jede VM mit 128 MB geringem MMIO-Speicherplatz und 512 MB hohem MMIO-Speicherplatz. Ein Gerät benötigt jedoch möglicherweise mehr MMIO-Speicherplatz, oder es können mehrere Geräte durchlaufen werden, sodass die kombinierten Anforderungen diese Werte überschreiten.  Das Ändern des MMIO-Speicherplatzes erfolgt direkt und kann in PowerShell mithilfe der folgenden Befehle ausgeführt werden:

```PowerShell
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```

Die einfachste Möglichkeit, um zu bestimmen, wie viel MMIO-Speicherplatz belegt werden soll, ist die Verwendung des [Computer Profil Skripts](#machine-profile-script). Führen Sie die folgenden Befehle in einer PowerShell-Konsole aus, um das Computer Profil Skript herunterzuladen und auszuführen:

```PowerShell
curl -o SurveyDDA.ps1 https://raw.githubusercontent.com/MicrosoftDocs/Virtualization-Documentation/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1
.\SurveyDDA.ps1
```

Bei Geräten, die zugewiesen werden können, zeigt das Skript die MMIO-Anforderungen eines bestimmten Geräts wie im folgenden Beispiel an:

```PowerShell
NVIDIA GRID K520
Express Endpoint -- more secure.
    ...
    And it requires at least: 176 MB of MMIO gap space
...
```

Der niedrige MMIO-Speicherplatz wird nur von 32-Bit-Betriebssystemen und Geräten verwendet, die 32-Bit-Adressen verwenden. In den meisten Fällen reicht das Festlegen des hohen MMIO-Speicherplatzes eines virtuellen Computers aus, da 32-Bit-Konfigurationen nicht sehr häufig verwendet werden.

> [!IMPORTANT]
> Beim Zuweisen von MMIO-Speicherplatz zu einem virtuellen Computer muss der Benutzer sicherstellen, dass der MMIO-Speicherplatz auf die Summe des angeforderten MMIO-Speicherplatzes für alle gewünschten zugewiesenen Geräte zuzüglich eines zusätzlichen Puffers festgelegt wird, wenn es andere virtuelle Geräte gibt, die einige MB MMIO-Speicherplatz erfordern. Verwenden Sie die oben beschriebenen MMIO-Standardwerte als Puffer für niedriges und hohes MMIO (128 MB bzw. 512 MB).

Wenn ein Benutzer eine einzelne K520-GPU wie im obigen Beispiel zuweisen würde, muss er den MMIO-Speicherplatz der VM auf den Wert festlegen, der vom Computer Profil Skript und einem Puffer--176 MB + 512 MB ausgegeben wird. Wenn ein Benutzer drei K520-GPUs zuweisen würde, muss er den MMIO-Speicherplatz auf drei Mal 176 MB plus einen Puffer oder 528 MB + 512 MB festlegen.

Eine ausführlichere Betrachtung von MMIO Space finden Sie im techcommunity [-Blog unter diskrete Geräte Zuweisung-GPUs](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266) .

## <a name="machine-profile-script"></a>Skript für Computer Profil
Um zu vereinfachen, ob der Server ordnungsgemäß konfiguriert ist und welche Geräte durch diskrete Geräte Zuweisung übermittelt werden können, stellt einer unserer Techniker das folgende PowerShell-Skript bereit: [Surveydda. ps1.](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1)

Stellen Sie vor der Verwendung des Skripts sicher, dass die Hyper-V-Rolle installiert ist, und führen Sie das Skript in einem PowerShell-Befehlsfenster aus, das über Administrator Rechte verfügt.

Wenn das System nicht ordnungsgemäß für die Unterstützung der diskreten Geräte Zuweisung konfiguriert ist, zeigt das Tool eine Fehlermeldung an, die falsch ist. Wenn das Tool feststellt, dass das System ordnungsgemäß konfiguriert ist, werden alle Geräte aufgelistet, die auf dem PCIe-Bus gefunden werden können.

Das Tool zeigt für jedes gefundene Gerät an, ob es mit diskreter Geräte Zuweisung verwendet werden kann. Wenn ein Gerät als kompatibel mit der diskreten Geräte Zuweisung identifiziert wird, stellt das Skript einen Grund dar.  Wenn ein Gerät erfolgreich als kompatibel identifiziert wurde, wird der Speicherort Pfad des Geräts angezeigt.  Wenn dieses Gerät außerdem [MMIO-Speicherplatz](#mmio-space)erfordert, wird es ebenfalls angezeigt.

![Surveydda. ps1](./images/hyper-v-surveydda-ps1.png)

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="how-does-remote-desktops-remotefx-vgpu-technology-relate-to-discrete-device-assignment"></a>Wie verhält sich die remotefx-vgpu-Technologie von Remotedesktop mit der diskreten Geräte Zuweisung?
Dabei handelt es sich um vollständig getrennte Technologien. Remotefx vgpu muss nicht installiert werden, damit die diskrete Geräte Zuweisung funktioniert. Außerdem müssen keine weiteren Rollen installiert werden. Für remotefx vgpu muss die RDVH-Rolle installiert sein, damit der remotefx-vgpu-Treiber auf der VM vorhanden ist. Bei einer diskreten Geräte Zuweisung müssen keine weiteren Rollen vorhanden sein, da Sie den Treiber des Hardware Herstellers in der virtuellen Maschine installieren werden.  

### <a name="ive-passed-a-gpu-into-a-vm-but-remote-desktop-or-an-application-isnt-recognizing-the-gpu"></a>Ich habe eine GPU an einen virtuellen Computer übermittelt, aber Remotedesktop oder eine Anwendung erkennt die GPU nicht.
Dies kann eine Reihe von Ursachen haben. es gibt jedoch einige häufige Probleme, die unten aufgeführt sind.
- Stellen Sie sicher, dass der Treiber des aktuellen GPU-Anbieters installiert ist und keinen Fehler meldet, indem Sie den Gerätestatus in der Geräte-Manager überprüfen.
- Stellen Sie sicher, dass auf dem Gerät ausreichend [MMIO-Speicherplatz](#mmio-space) auf dem virtuellen Computer zugeordnet ist.
- Stellen Sie sicher, dass Sie eine GPU verwenden, die der Anbieter unterstützt, die in dieser Konfiguration verwendet wird. Beispielsweise verhindern einige Anbieter, dass Ihre verbraucherkarten funktionieren, wenn Sie an einen virtuellen Computer übermittelt werden.
- Stellen Sie sicher, dass die Anwendung, die ausgeführt wird, auf einem virtuellen Computer ausgeführt wird und dass sowohl die GPU als auch die zugehörigen Treiber von der Anwendung unterstützt werden. Einige Anwendungen haben Whitelists von GPUs und Umgebungen.
- Wenn Sie die Remotedesktop-Sitzungshost-Rolle oder Windows MultiPoint Services auf dem Gast verwenden, müssen Sie sicherstellen, dass ein bestimmter Gruppenrichtlinie Eintrag festgelegt ist, um die Verwendung der Standard-GPU zuzulassen. Wenn Sie ein Gruppenrichtlinie Objekt verwenden, das auf den Gast angewendet wird (oder auf den Editor für lokale Gruppenrichtlinien auf dem Gast), navigieren Sie zu folgendem Gruppenrichtlinie Element:
   - Computerkonfiguration
   - Administrator Vorlagen
   - Windows-Komponenten
   - Remotedesktopdienste
   - Remotedesktop-Sitzungshost
   - Remote Sitzungs Umgebung
   - Verwenden des Hardware-Standard Grafikadapters für alle Remotedesktopdienste Sitzungen

    Legen Sie diesen Wert auf aktiviert fest, und starten Sie den virtuellen Computer neu, sobald die Richtlinie angewendet wurde.

### <a name="can-discrete-device-assignment-take-advantage-of-remote-desktops-avc444-codec"></a>Kann die diskrete Geräte Zuweisung den AVC444-Codec von Remotedesktop nutzen?
Ja, weitere Informationen finden Sie in diesem Blogbeitrag: [Remotedesktopprotokoll (RDP) 10 AVC/H. 264 Verbesserungen in Windows 10 und Windows Server 2016 Technical Preview.](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

### <a name="can-i-use-powershell-to-get-the-location-path"></a>Kann ich PowerShell verwenden, um den Speicherort Pfad zu erhalten?
Ja, es gibt verschiedene Möglichkeiten, dies zu tun. Im folgenden finden Sie ein Beispiel:
```
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
```

### <a name="can-discrete-device-assignment-be-used-to-pass-a-usb-device-into-a-vm"></a>Kann die diskrete Geräte Zuweisung verwendet werden, um ein USB-Gerät an einen virtuellen Computer zu übergeben?
Obwohl es nicht offiziell unterstützt wird, haben unsere Kunden eine diskrete Geräte Zuweisung verwendet, indem Sie den gesamten USB3-Controller an einen virtuellen Computer übergeben.  Während der gesamte Controller übertragen wird, kann auf jedem USB-Gerät, das in diesen Controller eingebunden ist, auch auf dem virtuellen Computer zugegriffen werden.  Beachten Sie, dass nur einige USB3-Controller funktionieren, und USB2-Controller können nicht mit diskreter Geräte Zuweisung verwendet werden.
