---
title: Generation 2 VM-Sicherheitseinstellungen für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die in Hyper-V-Manager für virtuelle Maschinen der Generation 2 verfügbar
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 90a2b7234ee55d8469b6e02ba3de3a0efc080a3e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889501"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Generation 2 VM-Sicherheitseinstellungen für Hyper-V

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Verwenden Sie die Sicherheitseinstellungen für den virtuellen Computer in Hyper-V-Manager, zum Schutz der Daten und des Status eines virtuellen Computers. Sie können virtuelle Computer schützen, von der Untersuchung, Diebstahl und Manipulation von Schadsoftware, die auf dem Host, und Administratoren im Rechenzentrum ausgeführt werden kann. Die Sicherheitsstufe, die Sie erhalten, hängt von der Hosthardware, die Sie die Generation des virtuellen Computers ausgeführt, ein, und, ob Sie den Dienst wird aufgerufen, die Host-Überwachungsdienst einrichten autorisiert, die Hosts abgeschirmte virtuelle Computer zu starten.  

Host-Überwachungsdienst ist eine neue Rolle in Windows Server 2016. Es gibt berechtigte Hyper-V-Hosts und können sie einen bestimmten virtuellen Computer ausgeführt. Sie würden am häufigsten von Host-Überwachungsdienst für ein Datencenter einrichten. Aber Sie können eine geschützte virtuelle Maschine, um sie lokal auszuführen, ohne das Einrichten einer Host-Überwachungsdienst erstellen. Sie können später die geschützte virtuelle Maschine mit einem Host-Überwachungsdienst-Fabric verteilen.  

Wenn Sie Host-Überwachungsdienst eingerichtet haben, oder führen sie im lokalen Modus auf dem Hyper-V-Host und überwachungsschlüssels für den Besitzer des virtuellen Computers auf dem Host ist, können Sie die in diesem Thema beschriebenen Einstellungen ändern.   Besitzer eines Schlüssels Überwachungsdienst ist eine Organisation, die erstellt und Freigaben, die ein privater oder öffentlicher Schlüssel, besitzen alle virtuellen Computer mit diesem Schlüssel erstellt.  

Um zu erfahren, wie Sie Ihre virtuellen Computer mit Host-Überwachungsdienst sicherer machen können, finden Sie unter den folgenden Ressourcen.  

- [Absichern des Fabrics: Schützen die Mandanten-Geheimnisse in Hyper-V (Ignite-video)](https://go.microsoft.com/fwlink/?LinkId=746379)
- [Geschütztes Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Secure Boot-Einstellung im Hyper-V-Manager  

Der sichere Start ist ein Feature, mit virtuellen Maschinen der Generation 2 zur Verfügung, das wird verhindert, dass nicht autorisierte Firmware, Betriebssysteme oder Unified Extensible Firmware Interface (UEFI)-Treiber (auch bekannt als Options-ROMs) zur Startzeit ausgeführt. Der sichere Start ist standardmäßig aktiviert. Sie können der sichere Start mit virtuellen Maschinen der Generation 2 verwenden, auf denen Windows oder Linux-Distribution-Betriebssystemen ausgeführt.  

Die in der folgenden Tabelle beschriebenen Vorlagen finden Sie in der Zertifikate, die Sie zum Überprüfen der Integrität des Startvorgangs benötigen.  

|Vorlagenname|Beschreibung|  
|-----------------|---------------|  
|Microsoft Windows|Wählen Sie den virtuellen Computer für ein Windows-Betriebssystem, für den sicheren Start.|  
|Microsoft-UEFI-Zertifizierungsstelle|Wählen Sie für den sicheren Start des virtuellen Computers für eine Linux-Distribution-Betriebssystem.|  
|Open-Source-abgeschirmte VM|Mit dieser Vorlage wird genutzt, um den sicheren Start für [Linux-basierte abgeschirmte VMs](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template).|

Weitere Informationen finden Sie in den folgenden Themen.  

- [Sicherheitsübersicht für Windows 10](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Sollte ich virtuelle Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Linux- und FreeBSD-Maschinen in Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Unterstützung der verschlüsselungseinstellungen im Hyper-V-Manager

Sie können dazu die folgenden Verschlüsselungsoptionen für die Unterstützung der Daten und des Status des virtuellen Computers zu schützen.  

- **Aktivieren von Trusted Platform Module** -diese Einstellung wird einen virtualisierte Trusted Platform Module (TPM)-Chip zur Verfügung, mit dem virtuellen Computer. Dadurch wird den Gast Datenträger des virtuellen Computers mit BitLocker verschlüsselt.
  - Wenn Ihre Hyper-V-Host mit Windows 10 1511 ausgeführt wird, müssen Sie isolierten Benutzermodus zu aktivieren. 
- **Verschlüsseln von Status und die VM-Migration-Traffic** - verschlüsselt-Status des virtuellen Computers gespeichert und livemigrations-Datenverkehr.

### <a name="enable-isolated-user-mode"></a>Isolierter Benutzermodus aktivieren

Bei Auswahl von **aktivieren Trusted Platform Module** auf Hyper-V-Hosts, auf denen Versionen von Windows vor Windows 10 Anniversary Update ausgeführt, müssen Sie die isolierten Benutzermodus aktivieren. Sie müssen nicht dies tun, Hyper-V-Hosts, Ausführen von Windows Server 2016 oder Windows 10 Anniversary Update oder höher.

Isolierter Benutzermodus ist die Runtime-Umgebung, die Anwendungen innerhalb virtueller sicherer Modus auf dem Hyper-V-Host hostet. Virtueller sicherer Modus dient zum Sichern und schützen den Status des virtuellen TPM-Chips.  

So aktivieren Sie isolierten Benutzermodus, auf dem Hyper-V-Host, auf denen frühere Versionen von Windows 10 ausgeführt,  

1.  Öffnen Sie die Windows PowerShell als Administrator.  

2.  Führen Sie die folgenden Befehle aus:  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

Sie können einen virtuellen Computer migrieren, mit virtuellen TPM aktiviert, um alle Hosts, die die Ausführung von Windows Server 2016, Windows 10 build 10586 oder höhere Versionen. Aber wenn Sie es auf einen anderen Host migrieren, möglicherweise nicht gestartet werden können. Sie müssen die Schlüsselschutzvorrichtung für die virtuelle Maschine zum Autorisieren des neuen Hosts zum Ausführen des virtuellen Computers aktualisieren. Weitere Informationen finden Sie unter [geschützten Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381) und [Systemanforderungen für Hyper-V unter Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).  

## <a name="security-policy-in-hyper-v-manager"></a>Die Sicherheitsrichtlinien in Hyper-V-Manager  
Verwenden Sie für weitere VM-Sicherheit, die **Schutz aktivieren** Option aus, um Verwaltungsfunktionen wie Konsolenverbindung, PowerShell Direct und einige Komponenten zu deaktivieren. Bei Auswahl dieser Option **sicherer Start**, **aktivieren Trusted Platform Module**, und **Encrypt-Status und die VM-Migration-Traffic** Optionen aktiviert und erzwungen werden.   

Sie können die abgeschirmten virtuellen Computer lokal ausführen, ohne eine Host-Überwachungsdienst einrichten zu müssen. Aber wenn Sie es auf einen anderen Host migrieren, möglicherweise nicht gestartet werden können. Sie müssen die Schlüsselschutzvorrichtung für die virtuelle Maschine zum Autorisieren des neuen Hosts zum Ausführen des virtuellen Computers aktualisieren. Weitere Informationen finden Sie unter [Geschütztes Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381).  

Weitere Informationen zur Sicherheit in Windows Server finden Sie unter [Sicherheit und Zusicherungen](../../../security/Security-and-Assurance.md).  
