---
title: Schnellstart für die Bereitstellung eines geschützten Fabrics
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 8e1ef34370b1459cd55705bc0069b49a572de303
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447529"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>Schnellstart für die Bereitstellung eines geschützten Fabrics

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird erläutert, was ein geschütztes Fabric ist, die Anforderungen, und eine Zusammenfassung des Bereitstellungsprozesses. Ausführliche Schritte zur Bereitstellung finden Sie unter [Host-Überwachungsdienst für die Bereitstellung von überwachten Hosts und abgeschirmte VMs](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview).

Lieber ein Video ansehen? Finden Sie in der Microsoft Virtual Academy-Kurs [Bereitstellen von abgeschirmten VMs and dem einer geschützten Fabric mit Windows Server 2016](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474).

## <a name="what-is-a-guarded-fabric"></a>Was ist ein geschütztes Fabric

Ein _überwachten Fabric_ ist ein Windows Server 2016 Hyper-V-Fabric kann der Schutz von Workloads von Mandanten für die Untersuchung, Diebstahl und Manipulation von Malware, die auf dem Host ausgeführt, als auch von Systemadministratoren. Diese virtualisierte arbeitsauslastungen sind Mandanten – geschützt, sowohl auf REST-API und in-Flight – heißen _abgeschirmte VMs_. 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>Was sind die Anforderungen für ein geschütztes Fabric

Die Anforderungen für ein geschütztes Fabric umfassen:

- **Eine Möglichkeit zum Ausführen von abgeschirmten VMs, die durch böswillige Software kostenlos ist.**

    Diese heißen _von überwachten Hosts_. 
    Überwachte Hosts sind Windows Server 2016 Datacenter Edition Hyper-V-Hosts, die abgeschirmte VMs ausführen können, nur dann, wenn sie nachweisen können, dass sie in einem bekannten, vertrauenswürdigen Status an eine externe Stelle wird aufgerufen, die Host Guardian Service (HGS) ausgeführt werden. 
    Der Host-Überwachungsdienst ist eine neue Serverrolle in Windows Server 2016 und in der Regel als ein Cluster mit drei Knoten bereitgestellt wird. 

- **Eine Möglichkeit, um zu überprüfen, ob einen Host ist in einem fehlerfreien Zustand.**

    Der Host-Überwachungsdienst führt _Nachweis_, gemessen, in denen die Integrität des überwachten Hosts.

- **Ein Prozess, um Schlüssel für fehlerfreie Hosts sicher freizugeben.**

    Der Host-Überwachungsdienst führt _für den Schutz und wichtige Version_, in dem sie die Schlüssel für fehlerfreie Hosts wieder freigibt.

- **Tools für die sichere Bereitstellung und hosting von automatisieren abgeschirmte VMs.**

    Optional können Sie diese Verwaltungstools in ein geschütztes Fabric hinzufügen:

    - System Center 2016 Virtual Machine Manager (VMM). VMM wird empfohlen, da es zusätzliche Tools bietet, nach was Sie erhalten, verwenden Sie einfach die PowerShell-Cmdlets, die mit Hyper-V und die arbeitsauslastungen geschütztes Fabric stammen).
    - System Center 2016 Service Provider Foundation (SPF). Dies ist eine API-Schicht zwischen Windows Azure Pack und VMM sowie eine Voraussetzung für die Verwendung von Windows Azure Pack.
    - Windows Azure Pack bietet eine gute grafische Weboberfläche zum Verwalten von eines geschützten Fabrics und abgeschirmte VMs. 

In der Praxis eine Entscheidung getroffen werden muss, vorab: die [nachweismodus](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution) von geschütztem Fabric verwendet. Es gibt zwei Möglichkeiten, zwei sich gegenseitig ausschließende Modi, durch die Host-Überwachungsdienst messen können, die Hyper-V-Hosts fehlerfrei ist. Wenn Sie Host-Überwachungsdienst initialisieren, müssen Sie den Modus auswählen:  

- Host-schlüsselnachweis und Modus-Taste, ist weniger sicheren, jedoch einfacher zu verwenden  
- Mit der TPM-basierten Nachweis und TPM-Modus ist sicherer, aber erfordert weitere Konfiguration und spezielle hardware

Bei Bedarf können Sie im Modus-Taste mit vorhandenen Hyper-V-Hosts, die auf Windows Server 2019 Datacenter Edition aktualisiert wurden bereitstellen und dann in der sicherer Modus des TPM konvertieren, wenn Server Hardwaresupport (einschließlich TPM 2.0) zur Verfügung steht. 

Jetzt wissen Sie, was die einzelnen Teile sind betrachten wir ein Beispiel für das Bereitstellungsmodell.

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>Gewusst wie: Abrufen aus einem aktuellen Hyper-V-Fabric in ein geschütztes fabric

Nehmen wir dieses Szenario: Sie haben eine vorhandene Hyper-V-Fabric, z. B. "contoso.com" in der folgenden Abbildung ist und Sie eine Windows Server 2016 überwachten Fabric erstellen möchten.

![Vorhandene Hyper-V-fabric](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>Schritt 1: Bereitstellen von Hyper-V-Hosts unter Windows Server 2016 

Hyper-V-Hosts müssen zum Ausführen von Windows Server 2016 Datacenter-Edition oder höher. Wenn Sie Hosts aktualisieren, können Sie [upgrade](https://technet.microsoft.com/windowsserver/dn527667.aspx) aus Standard Edition, Datacenter Edition.

![Aktualisieren von Hyper-V-hosts](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>Schritt 2: Bereitstellen des Host-Überwachungsdienst (Host-Überwachungsdienst)

Klicken Sie dann die Host-Überwachungsdienst-Serverrolle installiert und stellen es einen Cluster mit drei Knoten, wie im Beispiel relecloud.com in der folgenden Abbildung. Dies erfordert drei PowerShell-Cmdlets:

- Verwenden Sie zum Hinzufügen der Rolle des Host-Überwachungsdienst `Install-WindowsFeature` 
- Verwenden Sie zum Installieren der Host-Überwachungsdienst `Install-HgsServer` 
- Verwenden Sie zum Initialisieren der Host-Überwachungsdienst mit Ihrem ausgewählten Modus Nachweis `Initialize-HgsServer` 

Wenn die vorhandenen Hyper-V-Server die Voraussetzungen für die TPM-Modus nicht entsprechen (angenommen, sie müssen keinen TPM 2.0), können Sie die Host-Überwachungsdienst mit Admin-basierten Nachweis (Active Directory-Modus), müssen Sie eine Active Directory-Vertrauensstellung mit der Domäne Fabric initialisieren. 

In unserem Beispiel nehmen wir an Contoso anfänglich wird die in AD-Modus bereitgestellt werden, um Compliance-Anforderungen sofort zu erfüllen, und plant, in die sicherere TPM-basierten Nachweis zu konvertieren, nachdem geeignete Server-Hardware erworben werden kann. 

![Installieren von HGS](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>Schritt 3: Extrahieren von Identitäten, Hardware-Baselines und anwendungssteuerungscode-Integritätsrichtlinien

Der Prozess zum Extrahieren von Identitäten aus Hyper-V-Hosts, hängt von den nachweismodus, die verwendet wird.

Für AD-Modus ist die ID des Hosts für die Domäne eingebundenen Computer-Konto, die Mitglied einer bestimmten Sicherheitsgruppe in der Fabric-Domäne sein muss.
Mitgliedschaft in der angegebenen Gruppe ist die einzige Festlegung, ob der Host fehlerfrei ist. 

In diesem Modus ist der fabricadministrator allein verantwortlich für das Sicherstellen der Integritäts der Hyper-V-Hosts. Da die Host-Überwachungsdienst wiedergegeben wird, keinen Teil bei der Entscheidung, was ist, oder kann nicht ausgeführt wird, funktioniert Schadsoftware und Debugger wie vorgesehen. 

Debugger, die versuchen, direkt an einen Prozess (z. B. WinDbg.exe) angefügt werden jedoch für abgeschirmte VMs blockiert, da der VM Arbeitsprozess (VMWP.exe) eines geschützten Prozesses Lichts (PPL) ist.
Alternative Debugtechniken, wie z. B. von LiveKd.exe, werden nicht blockiert. Im Gegensatz zu abgeschirmten VMs wird der Arbeitsprozess für die Verschlüsselung unterstützte VMs nicht ausgeführt, wie eine PPL, so wie von herkömmliche Debuggern WinDbg.exe weiterhin normal ausgeführt werden.

Anders ausgedrückt, die strengen Validierungsschritte für den TPM-Modus werden nicht für AD-Modus in keiner Weise verwendet.

Für den TPM-Modus sind drei Schritte erforderlich: 

1.  Ein _öffentlichen Endorsement Key_ (oder _EKpub_) aus der TPM 2.0 auf jeder einzelnen Hyper-V-Host. Verwenden Sie zum Erfassen der EKpub `Get-PlatformIdentifier`. 
2.  Ein _Hardware Baseline_. Wenn Hyper-V-Hosts identisch sind, ist eine einzelne Baseline alles, was, die Sie benötigen. Ist dies nicht der Fall ist, müssen Sie eine für jede Klasse von Hardware dafür. Die Baseline ist in Form einer Protokolldatei Trustworthy Computing Group und TCGlog. Die TCGlog enthält alle Daten, die der Host aus der UEFI-Firmware über den Kernel, bis, in dem der Host vollständig gestartet wurde. Um die Hardware-Baseline zu erfassen, installieren Sie die Hyper-V-Rolle und das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts, und verwenden Sie `Get-HgsAttestationBaselinePolicy`. 
3.  Ein _codeintegritätsrichtlinie_. Wenn Ihre Hyper-V-Hosts identisch sind, ist eine einzelne codeintegritätsrichtlinie alles, was, die Sie benötigen. Ist dies nicht der Fall ist, müssen Sie eine für jede Klasse von Hardware dafür. Windows Server 2016 und Windows 10 verfügen jeweils über eine neue Art der Erzwingung für CI-Richtlinien, die Namen _(Hypervisor enforced Code Integrity, HVCI)_ . HVCI bietet sicheres Erzwingung und stellt sicher, dass ein Host darf nur Binärdateien ausgeführt werden, die ein vertrauenswürdiger Administrator Ausführung zulässig ist. Diese Anweisungen werden in einer codeintegritätsrichtlinie eingeschlossen, die Host-Überwachungsdienst hinzugefügt wird. Host-Überwachungsdienst misst die codeintegritätsrichtlinie des Hosts, bevor sie zum Ausführen geschützter VMs zulässig sind. Verwenden Sie zum Erfassen einer codeintegritätsrichtlinie `New-CIPolicy`. Anschließend muss die Richtlinie mit seiner binären Form konvertiert `ConvertFrom-CIPolicy`.

![Extrahieren von Identitäten, Baseline und codeintegritätsrichtlinie](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

Das ist alles – des geschützten Fabrics erstellt wird, im Hinblick auf die Infrastruktur für die Ausführung.  
Nun können Sie eine abgeschirmte VM vorlagendatenträger und eine geschützte Datendatei so abgeschirmte erstellen können der virtuelle Computer einfach und sicher bereitgestellt werden. 

## <a name="step-4-create-a-template-for-shielded-vms"></a>Schritt 4: Erstellen Sie eine Vorlage für abgeschirmte VMs

Vorlage für eine abgeschirmte VM schützt vorlagedatenträger durch das Erstellen einer Signatur des Datenträgers zu einem bekannten, vertrauenswürdigen Zeitpunkt rechtzeitig an. 
Wenn Sie der vorlagendatenträger später mit Schadsoftware infiziert ist, wird die Signatur Originalvorlage unterscheiden sich die durch die sichere abgeschirmte VM-Bereitstellung erkannt wird. 
Abgeschirmte vorlagedatenträger werden erstellt, indem Sie Ausführung der **geschützte Datenträger Assistent zum Erstellen von** oder `Protect-TemplateDisk` für einen regulären vorlagendatenträger. 

Jede ist im Lieferumfang der **Tools für geschützte VMs** Features in der [Remote Server Administration Tools für Windows 10](https://www.microsoft.com/download/details.aspx?id=45520).
Nachdem Sie RSAT heruntergeladen haben, führen Sie diesen Befehl zum Installieren der **Tools für geschützte VMs** Feature:

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

Ein trustworthy-Administrator, z. B. der Fabric-Administrator oder Besitzer der virtuellen Computer benötigen ein Zertifikat (häufig von einem Hostingdienstanbieter bereitgestellten) zum Signieren der VHDX-Datenträger-Vorlage. 

![Geschützte vorlagendatenträger-Assistenten](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

Die Datenträgersignatur ist für die Partition für das Betriebssystem des virtuellen Datenträgers berechnet.
Wenn alles für die Betriebssystempartition ändert, ändert sich die Signatur auch.
Dadurch können Benutzer stark die Datenträger ermitteln sie durch Angabe der entsprechenden Signatur vertrauen.

Überprüfen Sie die [Vorlage datenträgeranforderungen](guarded-fabric-create-a-shielded-vm-template.md) bevor Sie beginnen. 

## <a name="step-5-create-a-shielding-data-file"></a>Schritt 5: Erstellen Sie eine geschützte Datendatei 

Eine geschützte Datendatei, auch bekannt als PDK-Datei, erfasst die vertrauliche Informationen über den virtuellen Computer, z. B. das Administratorkennwort ein. 

![Geschützte Daten](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

Die geschützte Datendatei enthält auch die sicherheitsrichtlinieneinstellung für den geschützten virtuellen Computer. Sie müssen eine der beiden Sicherheitsrichtlinien auswählen, wenn Sie eine schutzdatendatei erstellen:

- Geschützte
   
    Die sicherste Option, die viele administrative Angriffsvektoren beseitigt.

- Verschlüsselung wird unterstützt

    Verwenden Sie ein geringerem Maß an Schutz, die immer noch bietet die Vorteile der Compliance werden können, um einen virtuellen Computer zu verschlüsseln, sondern kann Hyper-V-Administratoren folgende Möglichkeiten, VM-Konsolenverbindung und PowerShell Direct. 

    ![Neue Verschlüsselung unterstützten virtuellen Computer](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

Sie können Teile optionale Verwaltungs-, wie VMM oder Windows Azure Pack hinzufügen. Wenn Sie möchten, zum Erstellen eines virtuellen Computers ohne Installation dieser Komponenten finden Sie unter [Schritt-für-Schritt: Erstellen von abgeschirmten VMs ohne VMM](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/).

## <a name="step-6-create-a-shielded-vm"></a>Schritt 6: Erstellen einer abgeschirmten VMs

Erstellen von geschützten virtuellen Maschinen unterscheidet sich geringfügig von reguläre VMs. In Windows Azure Pack ist die Benutzeroberfläche sogar noch einfacher als einen normalen virtuellen Computer erstellen, da Sie nur benötigen, geben Sie einen Namen, geschützte Datendatei (mit den Rest der Spezialisierung Informationen), und das VM-Netzwerk. 

![Neue geschützte VM in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Host-Überwachungsdienst-Voraussetzungen](guarded-fabric-prepare-for-hgs.md)
