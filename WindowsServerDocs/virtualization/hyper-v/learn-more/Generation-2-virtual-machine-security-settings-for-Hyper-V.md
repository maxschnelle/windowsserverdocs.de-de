---
title: Sicherheitseinstellungen für virtuelle Computer der Generation 2 für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die im Hyper-V-Manager für virtuelle Maschinen der Generation 2 verfügbar sind
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 82544a58a8d46b3063605557be3c63cfa799e4fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364238"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Sicherheitseinstellungen für virtuelle Computer der Generation 2 für Hyper-V

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Verwenden Sie die Sicherheitseinstellungen des virtuellen Computers im Hyper-V-Manager, um die Daten und den Zustand einer virtuellen Maschine zu schützen. Sie können virtuelle Computer vor Untersuchung, Diebstahl und Manipulation durch Schadsoftware schützen, die auf dem Host ausgeführt werden kann, und Daten Center Administratoren. Die Sicherheitsstufe, die Sie erhalten, hängt von der Host Hardware, die Sie ausführen, von der Generierung des virtuellen Computers und davon ab, ob Sie den Dienst einrichten, der als Host-Überwachungsdienst bezeichnet wird, der Hosts autorisiert, abgeschirmte virtuelle Computer zu starten.  

Der Host-Überwachungsdienst ist eine neue Rolle in Windows Server 2016. Es identifiziert legitime Hyper-V-Hosts und ermöglicht Ihnen die Durchführung einer bestimmten virtuellen Maschine. Am häufigsten richten Sie den Host-Überwachungsdienst für ein Daten Center ein. Sie können jedoch einen abgeschirmten virtuellen Computer erstellen, um ihn lokal auszuführen, ohne einen Host-Überwachungsdienst einzurichten. Sie können den abgeschirmten virtuellen Computer später an ein Host-überwachungsfabric verteilen.  

Wenn Sie den Host-Überwachungsdienst nicht eingerichtet haben oder ihn im lokalen Modus auf dem Hyper-V-Host ausführen und der Host den Wächter Schlüssel des virtuellen Computers besitzt, können Sie die in diesem Thema beschriebenen Einstellungen ändern.   Ein Besitzer eines Wächter Schlüssels ist eine Organisation, die einen privaten oder öffentlichen Schlüssel erstellt und freigibt, um alle mit diesem Schlüssel erstellten virtuellen Computer zu besitzen.  

Informationen dazu, wie Sie Ihre virtuellen Computer mit dem Host-Überwachungsdienst sicherer machen können, finden Sie in den folgenden Ressourcen.  

- [„Harden the Fabric: Schützen von Mandanten Geheimnissen in Hyper-V (Ignite-Video) ](https://go.microsoft.com/fwlink/?LinkId=746379)
- [Geschütztes Fabric und abgeschirmte VMS](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Einstellung für den sicheren Start im Hyper-V-Manager  

Der sichere Start ist ein Feature, das bei virtuellen Computern der Generation 2 verfügbar ist, mit denen verhindert wird, dass nicht autorisierte Firmware, Betriebssysteme oder Unified Extensible Firmware Interface (UEFI)-Treiber (auch als Options-Roms bezeichnet) zur Startzeit ausgeführt werden. Der sichere Start ist standardmäßig aktiviert. Sie können den sicheren Start mit virtuellen Computern der Generation 2 verwenden, auf denen Windows-oder Linux-Verteilungs Betriebssysteme ausgeführt werden.  

Die in der folgenden Tabelle beschriebenen Vorlagen beziehen sich auf die Zertifikate, die Sie benötigen, um die Integrität des Startvorgangs zu überprüfen.  

|Vorlagenname|Beschreibung|  
|-----------------|---------------|  
|Microsoft Windows|Wählen Sie diese Option aus, um den virtuellen Computer für ein Windows-Betriebssystem zu starten.|  
|Microsoft UEFI-Zertifizierungsstelle|Wählen Sie diese Option aus, um den virtuellen Computer für ein Linux-Verteilungs Betriebssystem zu schützen.|  
|Geschützte Open Source-VM|Diese Vorlage wird zum Sichern des Starts für [Linux-basierte abgeschirmte VMS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template)genutzt.|

Weitere Informationen finden Sie in den folgenden Themen.  

- [Übersicht über die Sicherheit in Windows 10](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Linux-und FreeBSD-Virtual Machines unter Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Verschlüsselungs Unterstützungs Einstellungen in Hyper-V-Manager

Sie können zum Schutz der Daten und des Zustands des virtuellen Computers beitragen, indem Sie die folgenden Optionen für die Verschlüsselungs Unterstützung auswählen.  

- **Trusted Platform Module aktivieren** : bei dieser Einstellung wird dem virtuellen Computer ein virtualisierter Trusted Platform Module (TPM)-Chip zur Verfügung gestellt. Dies ermöglicht es dem Gast, den Datenträger des virtuellen Computers mithilfe von BitLocker zu verschlüsseln.
  - Wenn auf Ihrem Hyper-V-Host Windows 10 1511 ausgeführt wird, müssen Sie den isolierten Benutzermodus aktivieren. 
- **Verschlüsseln von Zustands-und VM-Migrations Datenverkehr** : verschlüsselt den gespeicherten Zustand des virtuellen Computers und den Datenverkehr für die Live Migration.

### <a name="enable-isolated-user-mode"></a>Isolierten Benutzermodus aktivieren

Wenn Sie Trusted Platform Module auf Hyper-V-Hosts **aktivieren** , auf denen ältere Windows-Versionen als Windows 10 Anniversary Update ausgeführt werden, müssen Sie den isolierten Benutzermodus aktivieren. Dies ist für Hyper-V-Hosts, auf denen Windows Server 2016 oder Windows 10 Anniversary Update oder höher ausgeführt wird, nicht erforderlich.

Der isolierte Benutzermodus ist die Laufzeitumgebung, die Sicherheitsanwendungen im virtuellen sicheren Modus auf dem Hyper-V-Host hostet. Der virtuelle sichere Modus wird verwendet, um den Status des virtuellen TPM-Chips zu sichern und zu schützen.  

So aktivieren Sie den isolierten Benutzermodus auf dem Hyper-V-Host, auf dem frühere Versionen von Windows 10 ausgeführt werden  

1.  Öffnen Sie die Windows PowerShell als Administrator.  

2.  Führen Sie die folgenden Befehle aus:  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

Sie können einen virtuellen Computer mit aktiviertem virtuellem TPM zu einem beliebigen Host migrieren, auf dem Windows Server 2016, Windows 10 Build 10586 oder höhere Versionen ausgeführt werden. Wenn Sie Sie jedoch zu einem anderen Host migrieren, können Sie Sie möglicherweise nicht starten. Sie müssen die Schlüssel Schutzvorrichtung für diesen virtuellen Computer aktualisieren, um den neuen Host zum Ausführen der virtuellen Maschine zu autorisieren. Weitere Informationen finden Sie unter geschütztes [Fabric und abgeschirmte VMS](https://go.microsoft.com/fwlink/?LinkId=746381) und [System Anforderungen für Hyper-V unter Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).  

## <a name="security-policy-in-hyper-v-manager"></a>Sicherheitsrichtlinie im Hyper-V-Manager  
Verwenden Sie für eine höhere Sicherheit der virtuellen Computer die Option Schutz **aktivieren** , um Verwaltungsfunktionen wie Konsolen Verbindung, PowerShell Direct und einige Integrations Komponenten zu deaktivieren. Wenn Sie diese Option auswählen, werden die Optionen " **sicherer Start**", " **Trusted Platform Module aktivieren**" und " **Verschlüsselungs Status und VM-Migration** " ausgewählt und erzwungen.   

Sie können den abgeschirmten virtuellen Computer lokal ausführen, ohne einen Host-Überwachungsdienst einzurichten. Wenn Sie Sie jedoch zu einem anderen Host migrieren, können Sie Sie möglicherweise nicht starten. Sie müssen die Schlüssel Schutzvorrichtung für diesen virtuellen Computer aktualisieren, um den neuen Host zum Ausführen der virtuellen Maschine zu autorisieren. Weitere Informationen finden Sie unter [Geschütztes Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381).  

Weitere Informationen zur Sicherheit in Windows Server finden Sie unter [Sicherheit und](../../../security/Security-and-Assurance.md)Sicherheit.  
