---
title: Schnellstart für die geschützte Fabric-Bereitstellung
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 8359532113e04e2247b4af34effc7f5b89d36f34
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402416"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>Schnellstart für die geschützte Fabric-Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird erläutert, was ein geschütztes Fabric ist, seine Anforderungen und eine Zusammenfassung des Bereitstellungs Prozesses. Ausführliche Informationen zur Bereitstellung finden Sie unter Bereitstellen [des Host-Überwachungs Diensts für überwachte Hosts und abgeschirmte VMS](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview).

Lieber ein Video ansehen? Weitere Informationen finden Sie im Microsoft Virtual Academy-Kurs bereitstellen [von abgeschirmten VMS und einem geschützten Fabric mit Windows Server 2016](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474).

## <a name="what-is-a-guarded-fabric"></a>Was ist ein geschütztes Fabric?

Bei einem _geschützten Fabric_ handelt es sich um ein Windows Server 2016 Hyper-V-Fabric, mit dem mandantenworkloads vor Untersuchung, Diebstahl und Manipulation durch Schadsoftware, die auf dem Host ausgeführt wird, sowie von Systemadministratoren geschützt werden können. Diese virtualisierten mandantenworkloads – sowohl im Ruhezustand als auch in-Flight – werden als _abgeschirmte VMS_bezeichnet. 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>Welche Anforderungen gelten für ein geschütztes Fabric?

Zu den Anforderungen für ein überwachtes Fabric gehören:

- **Ein Ort zum Ausführen von abgeschirmten VMS, die kostenlos von Schadsoftware ausgeführt werden.**

    Diese werden als _geschützte Hosts_bezeichnet. 
    Geschützte Hosts sind Windows Server 2016 Datacenter Edition Hyper-V-Hosts, die abgeschirmte VMS nur ausführen können, wenn Sie beweisen können, dass Sie in einem bekannten und vertrauenswürdigen Zustand einer externen Zertifizierungsstelle ausgeführt werden, die als Host-Überwachungsdienst (Host-Überwachungsdienst) bezeichnet wird. 
    Die HGS ist eine neue Server Rolle in Windows Server 2016 und wird in der Regel als Cluster mit drei Knoten bereitgestellt. 

- **Eine Möglichkeit zum Überprüfen, ob sich ein Host in einem fehlerfreien Zustand befindet.**

    Die HGS führt _einen_Nachweis durch, wobei die Integrität der überwachten Hosts gemessen wird.

- **Ein Prozess, mit dem Schlüssel für fehlerfreie Hosts sicher freigegeben werden.**

    Die HGS führen den _Schlüsselschutz und die schlüsselfreigabe_aus, bei denen die Schlüssel wieder für fehlerfreie Hosts freigegeben werden.

- **Verwaltungs Tools zum Automatisieren der sicheren Bereitstellung und des Hostings von abgeschirmten VMS.**

    Optional können Sie diese Verwaltungs Tools einem geschützten Fabric hinzufügen:

    - System Center 2016 Virtual Machine Manager (VMM). VMM wird empfohlen, da Sie zusätzliche Verwaltungs Tools bereitstellt, die über das, was Sie bei der Verwendung von PowerShell-Cmdlets, die mit Hyper-V und den geschützten Fabric-Workloads geliefert werden, hinausgehen.
    - System Center 2016 Service Provider Foundation (SPF). Dies ist eine API-Schicht zwischen Windows Azure Pack und VMM und eine Voraussetzung für die Verwendung von Windows Azure Pack.
    - Windows Azure Pack bietet eine gute grafische Webschnittstelle zum Verwalten eines geschützten Fabrics und geschützter VMS. 

In der Praxis muss eine Entscheidung im Vordergrund getroffen werden: der Nachweis [Modus](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution) , der vom geschützten Fabric verwendet wird. Es gibt zwei Möglichkeiten – zwei sich gegenseitig ausschließende Modi –, mit denen HGS messen kann, dass ein Hyper-V-Host fehlerfrei ist. Wenn Sie HGS initialisieren, müssen Sie den folgenden Modus auswählen:  

- Der Host Schlüssel Nachweis oder Schlüssel Modus ist weniger sicher, aber leichter zu übernehmen.  
- Der TPM-basierte Nachweis oder der TPM-Modus ist sicherer, erfordert jedoch mehr Konfiguration und spezielle Hardware

Falls erforderlich, können Sie die Bereitstellung im Schlüssel Modus mithilfe vorhandener Hyper-V-Hosts durchführen, die auf Windows Server 2019 Datacenter Edition aktualisiert wurden, und dann in den sichereren TPM-Modus konvertieren, wenn die Server Hardware (einschließlich TPM 2,0) unterstützt wird. 

Nun, da Sie wissen, was die Teile sind, sehen wir uns ein Beispiel für das Bereitstellungs Modell an.

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>So gelangen Sie von einem aktuellen Hyper-V-Fabric zu einem geschützten Fabric

Stellen Sie sich dieses Szenario vor – Sie haben ein vorhandenes Hyper-V-Fabric, wie z. b. contoso.com in der folgenden Abbildung, und Sie möchten ein geschütztes Windows Server 2016-Fabric erstellen.

![Vorhandenes Hyper-V-Fabric](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>Schritt 1: Bereitstellen von Hyper-V-Hosts unter Windows Server 2016 

Auf den Hyper-V-Hosts muss Windows Server 2016 Datacenter Edition oder höher ausgeführt werden. Wenn Sie Hosts aktualisieren, können Sie ein [Upgrade](https://technet.microsoft.com/windowsserver/dn527667.aspx) von der Standard Edition auf Datacenter Edition durchführen.

![Aktualisieren von Hyper-V-Hosts](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>Schritt 2: Bereitstellen des Host-Überwachungs Diensts (HGS)

Installieren Sie dann die HGS-Server Rolle, und stellen Sie Sie als Cluster mit drei Knoten bereit, wie z. b. das relecloud.com-Beispiel in der folgenden Abbildung. Hierfür sind drei PowerShell-Cmdlets erforderlich:

- Verwenden Sie zum Hinzufügen der HGS-Rolle`Install-WindowsFeature` 
- Verwenden Sie zum Installieren der HGS`Install-HgsServer` 
- Um die HGS mit dem gewählten Nachweis Modus zu initialisieren, verwenden Sie`Initialize-HgsServer` 

Wenn Ihre vorhandenen Hyper-V-Server die Voraussetzungen für den TPM-Modus nicht erfüllen (z. b. Wenn Sie nicht über TPM 2,0 verfügen), können Sie HGS mit dem Administrator basierten Nachweis (AD-Modus) initialisieren, für den eine Active Directory Vertrauensstellung mit der Fabric-Domäne erforderlich ist. 

Nehmen wir in unserem Beispiel an, dass "Configuration Manager" zuerst im AD-Modus bereitgestellt wird, um die Konformitätsanforderungen sofort zu erfüllen, und plant die Konvertierung in den sichereren TPM-basierten Nachweis, nachdem die geeignete Server Hardware erworben werden kann. 

![Installieren von HGS](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>Schritt 3: Extrahieren von Identitäten, hardwarebaselines und Code Integritäts Richtlinien

Der Prozess zum Extrahieren von Identitäten von Hyper-V-Hosts hängt vom verwendeten Nachweis Modus ab.

Für den AD-Modus ist die ID des Hosts das in die Domäne eingebundenen Computer Konto, das Mitglied einer bestimmten Sicherheitsgruppe in der Fabric-Domäne sein muss.
Die Mitgliedschaft in der angegebenen Gruppe ist die einzige Bestimmung, ob der Host fehlerfrei ist oder nicht. 

In diesem Modus ist der Fabric-Administrator allein dafür verantwortlich, die Integrität der Hyper-V-Hosts sicherzustellen. Da HGS bei der Entscheidung, was nicht ausgeführt werden kann, keine Rolle spielt, funktionieren Schadsoftware und-Debug-Anwendungen wie vorgesehen. 

Debugger, die versuchen, direkt an einen Prozess anzufügen (z. b. WinDbg. exe), werden jedoch für abgeschirmte VMS blockiert, da der Arbeitsprozess des virtuellen Computers (VMWP. exe) ein geschütztes Prozess Licht (PPL) ist.
Alternative Debuggingtechniken, z. b. die von LiveKd. exe verwendeten, werden nicht blockiert. Anders als bei abgeschirmten VMS wird der Arbeitsprozess für die Verschlüsselung unterstützte VMS nicht als ppl ausgeführt, sodass herkömmliche Debugger wie WinDBG. exe weiterhin normal funktionieren.

Anders ausgedrückt: die strengen Validierungs Schritte, die für den TPM-Modus verwendet werden, werden in keiner Weise für den AD-Modus verwendet.

Für den TPM-Modus sind drei Schritte erforderlich: 

1.  Einen _öffentlichen Endorsement Key_ (oder _ekpub_) von TPM 2,0 auf jedem und jedem Hyper-V-Host. Verwenden `Get-PlatformIdentifier`Sie zum Erfassen von ekpub. 
2.  Eine _hardwarebaseline_. Wenn jeder ihrer Hyper-V-Hosts identisch ist, benötigen Sie nur eine einzige Baseline. Wenn dies nicht der Fall ist, benötigen Sie für jede Hardware Klasse einen. Die Baseline hat die Form einer Trusted Computing Group Logfile oder tcglog. Tcglog enthält alle Elemente, die der Host von der UEFI-Firmware über den Kernel verwendet hat, und zwar direkt bis zu dem Ort, an dem der Host vollständig gestartet wurde. Zum Erfassen der hardwarebaseline installieren Sie die Hyper-v-Rolle und die Hyper-v-Unterstützung `Get-HgsAttestationBaselinePolicy`des Host-Überwachungs Diensts und verwenden. 
3.  Eine _Code Integritätsrichtlinie_. Wenn jeder ihrer Hyper-V-Hosts identisch ist, benötigen Sie nur eine einzige CI-Richtlinie. Wenn dies nicht der Fall ist, benötigen Sie für jede Hardware Klasse einen. Windows Server 2016 und Windows 10 verfügen jeweils über eine neue Form der Erzwingung für CI-Richtlinien, die als _Hypervisor-erzwungene Code Integrität (hvci)_ bezeichnet wird. Hvci bietet eine starke Erzwingung und stellt sicher, dass ein Host nur Binärdateien ausführen darf, die von einem vertrauenswürdigen Administrator ausgeführt werden dürfen. Diese Anweisungen sind in einer CI-Richtlinie umschließt, die zu HGS hinzugefügt wird. HGS misst die CI-Richtlinie jedes Hosts, bevor Sie geschützte VMS ausführen dürfen. Verwenden `New-CIPolicy`Sie zum Erfassen einer CI-Richtlinie. Die Richtlinie muss dann mithilfe `ConvertFrom-CIPolicy`von in das binäre Formular konvertiert werden.

![Extrahieren von Identitäten, Baseline und CI-Richtlinie](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

Das ist alles – das geschützte Fabric wird in Bezug auf die Infrastruktur für die Durchführung erstellt.  
Nun können Sie einen abgeschirmten VM-Vorlagen Datenträger und eine geschützte Datendatei erstellen, damit abgeschirmte VMS einfach und sicher bereitgestellt werden können. 

## <a name="step-4-create-a-template-for-shielded-vms"></a>Schritt 4: Erstellen einer Vorlage für abgeschirmte VMS

Eine geschützte VM-Vorlage schützt Vorlagen Datenträger, indem eine Signatur des Datenträgers zu einem bekannten vertrauenswürdigen Zeitpunkt erstellt wird. 
Wenn der Vorlagen Datenträger später durch Schadsoftware infiziert wird, unterscheidet sich seine Signatur von der ursprünglichen Vorlage, die durch den sicheren abgeschirmten VM-Bereitstellungs Prozess erkannt wird. 
Geschützte Vorlagen Datenträger werden erstellt, indem der Assistent zum Erstellen `Protect-TemplateDisk` einer **abgeschirmten Vorlage** oder eine reguläre Vorlagen Festplatte ausgeführt wird. 

Jede ist in der [Remoteserver-Verwaltungstools für Windows 10](https://www.microsoft.com/download/details.aspx?id=45520)in der Funktion der **abgeschirmten VM-Tools** enthalten.
Nachdem Sie RSAT heruntergeladen haben, führen Sie den folgenden Befehl aus, um das Feature der **abgeschirmten VM-Tools**

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

Ein vertrauenswürdiger Administrator (z. b. der Fabric-Administrator oder der Besitzer der VM) benötigt ein Zertifikat (häufig von einem hostingdienstanbieter bereitgestellt) zum Signieren des vhdx-Vorlagen Datenträgers 

![Assistent für geschützte Vorlagen-Datenträger](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

Die Datenträger Signatur wird über die Betriebssystem Partition des virtuellen Datenträgers berechnet.
Wenn Änderungen an der Betriebssystem Partition vorgenommen werden, ändert sich auch die Signatur.
Dies ermöglicht es Benutzern, die entsprechenden Datenträger durch Angabe der entsprechenden Signatur stark zu identifizieren.

Überprüfen Sie die [Vorlagen Anforderungen](guarded-fabric-create-a-shielded-vm-template.md) für Datenträger, bevor Sie loslegen. 

## <a name="step-5-create-a-shielding-data-file"></a>Schritt 5: Erstellen einer Schutz Datendatei 

Eine geschützte Datendatei, die auch als PDK-Datei bezeichnet wird, erfasst vertrauliche Informationen über den virtuellen Computer, z. b. das Administrator Kennwort. 

![Geschützte Daten](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

Die Schutz Datendatei enthält auch die Sicherheitsrichtlinien Einstellung für den abgeschirmten virtuellen Computer. Wenn Sie eine geschützte Datendatei erstellen, müssen Sie eine von zwei Sicherheitsrichtlinien auswählen:

- Abgesch
   
    Die sicherste Option, bei der viele administrative Angriffsvektoren vermieden werden.

- Verschlüsselung unterstützt

    Ein kleineres Maß an Schutz, das immer noch die Kompatibilitäts Vorteile der Verschlüsselung eines virtuellen Computers bietet, aber Hyper-V-Administratoren die Verwendung von VM Console Connection und PowerShell Direct ermöglicht. 

    ![Neuer Verschlüsselungs unterstützter virtueller Computer](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

Sie können optionale Verwaltungs Elemente wie VMM oder Windows Azure Pack hinzufügen. Wenn Sie einen virtuellen Computer erstellen möchten, ohne diese Komponenten zu installieren, finden Sie weitere Informationen unter [Schritt für Schritt – Erstellen von abgeschirmten VMS ohne VMM](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/).

## <a name="step-6-create-a-shielded-vm"></a>Schritt 6: Erstellen einer abgeschirmten VM

Das Erstellen von abgeschirmten virtuellen Computern unterscheidet sich nur geringfügig von herkömmlichen virtuellen Computern. In Windows Azure Pack ist die-Funktion sogar noch einfacher als das Erstellen einer regulären VM, da Sie lediglich einen Namen, eine geschützte Datendatei (mit den restlichen Spezialisierungs Informationen) und das VM-Netzwerk angeben müssen. 

![Neue abgeschirmte VM in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Voraussetzungen für HGS](guarded-fabric-prepare-for-hgs.md)
