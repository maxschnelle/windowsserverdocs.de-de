---
title: Planungs Handbuch für geschütztes Fabric und abgeschirmte VMs für Hoster
ms.prod: windows-server
ms.topic: article
ms.assetid: 854defc8-99f8-4573-82c0-f484e0785859
manager: dongill
author: nirb-ms
ms.author: nirb
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2e64f8a43318f10db3bfcb604adcef4b0bdc9837
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856513"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-hosters"></a>Planungs Handbuch für geschütztes Fabric und abgeschirmte VMs für Hoster

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden Planungsentscheidungen behandelt, die vorgenommen werden müssen, damit abgeschirmte virtuelle Maschinen in Ihrem Fabric ausgeführt werden können. Unabhängig davon, ob Sie ein vorhandenes Hyper-V-Fabric aktualisieren oder ein neues Fabric erstellen, besteht das Ausführen von abgeschirmten VMS aus zwei Hauptkomponenten:

- Der Host-Überwachungsdienst (Host Guardian Service, HGS) bietet Nachweis-und Schlüsselschutz, sodass Sie sicherstellen können, dass abgeschirmte VMS nur auf genehmigten und fehlerfreien Hyper-V-Hosts ausgeführt werden. 
- Genehmigte und fehlerfreie Hyper-V-Hosts, auf denen abgeschirmte VMS (und reguläre VMS) ausgeführt werden können – diese werden als geschützte Hosts bezeichnet.

![HGS und einen überwachten Host](../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-plus-host-diagram-basic.png)

## <a name="decision-1-trust-level-in-the-fabric"></a>Entscheidungs #1: Vertrauens Ebene im Fabric

Die Implementierung des Host-Überwachungs Diensts und der geschützten Hyper-V-Hosts hängt hauptsächlich von der Vertrauens Stärke ab, die Sie in Ihrem Fabric erreichen möchten. Die Stärke der Vertrauensstellung wird durch den Nachweis Modus gesteuert. Es gibt zwei Optionen, die sich gegenseitig ausschließen:

1. TPM-vertrauenswürdiger Nachweis

    Wenn Ihr Ziel darin besteht, virtuelle Computer vor böswilligen Administratoren oder einem kompromittierten Fabric zu schützen, verwenden Sie den TPM-vertrauenswürdigen Nachweis. Diese Option eignet sich gut für Szenarien mit mehreren Mandanten und für hochwertige Assets in Unternehmensumgebungen, wie z. b. Domänen Controllern oder Inhalts Servern wie SQL oder SharePoint.
    Hvci-Richtlinien (Hypervisor-Protected Code Integrity) werden gemessen und deren Gültigkeit durch HGS erzwungen, bevor der Host abgeschirmte VMS ausführen darf. 

2. Host Schlüssel Nachweis

    Wenn Ihre Anforderungen hauptsächlich von der Konformität abhängig sind, bei der virtuelle Computer sowohl im Ruhezustand als auch in-Flight verschlüsselt werden müssen, verwenden Sie den Host Schlüssel Nachweis. Diese Option eignet sich gut für allgemeine Rechenzentren, in denen Sie mit Hyper-V-Hosts und Fabric-Administratoren vertraut sind, die für tägliche Wartungsarbeiten und Vorgänge auf die Gast Betriebssysteme virtueller Computer zugreifen können. 

    In diesem Modus ist der Fabric-Administrator allein dafür verantwortlich, die Integrität der Hyper-V-Hosts sicherzustellen. 
    Da HGS bei der Entscheidung, was nicht ausgeführt werden kann, keine Rolle spielt, funktionieren Schadsoftware und-Debug-Anwendungen wie vorgesehen. 
    
    Debugger, die versuchen, direkt an einen Prozess anzufügen (z. b. WinDbg. exe), werden jedoch für abgeschirmte VMS blockiert, da der Arbeitsprozess des virtuellen Computers (VMWP. exe) ein geschütztes Prozess Licht (PPL) ist. 
    Alternative Debuggingtechniken, z. b. die von LiveKd. exe verwendeten, werden nicht blockiert. 
    Anders als bei abgeschirmten VMS wird der Arbeitsprozess für die Verschlüsselung unterstützte VMS nicht als ppl ausgeführt, sodass herkömmliche Debugger wie WinDBG. exe weiterhin normal funktionieren.

    Ein ähnlicher Nachweis Modus mit dem Namen admin-Trusted Nachweis (Active Directory basiert) ist ab Windows Server 2019 veraltet. 

Die von Ihnen gewählte Vertrauens Ebene übernimmt die Hardwareanforderungen für Ihre Hyper-V-Hosts sowie die Richtlinien, die Sie auf dem Fabric anwenden. Falls erforderlich, können Sie Ihr überwachtes Fabric mit vorhandenem Hardware-und Administrator vertrauenswürdigem Nachweis bereitstellen und dann in einen TPM-vertrauenswürdigen Nachweis konvertieren, wenn die Hardware aktualisiert wurde und Sie die fabricsicherheit verstärken müssen.

## <a name="decision-2-existing-hyper-v-fabric-versus-a-new-separate-hyper-v-fabric"></a>Entscheidungs #2: vorhandenes Hyper-v-Fabric im Vergleich zu einem neuen separaten Hyper-v-Fabric

Wenn Sie über ein vorhandenes Fabric (Hyper-V oder anderweitig) verfügen, ist es sehr wahrscheinlich, dass Sie es verwenden können, um abgeschirmte VMS zusammen mit regulären VMS auszuführen. Einige Kunden entscheiden sich dafür, abgeschirmte VMs in Ihre vorhandenen Tools und Fabrics zu integrieren, während andere das Fabric aus geschäftlichen Gründen voneinander trennen.

## <a name="hgs-admin-planning-for-the-host-guardian-service"></a>Planen von HGS-Administratoren für den Host-Überwachungsdienst

Stellen Sie den Host-Überwachungsdienst (Host Guardian Service, HGS) in einer äußerst sicheren Umgebung bereit, egal ob Sie sich auf einem dedizierten physischen Server, einem abgeschirmten virtuellen Computer, einem virtuellen Computer auf einem isolierten Hyper-V-Host (getrennt von dem Fabric, das geschützt ist) oder einem logisch getrennten Azure-Abonnement.   

| Fläche | Details |
|------|---------|
| Installationsanforderungen | <ul><li>Ein Server (Cluster mit drei Knoten wird für Hochverfügbarkeit empfohlen)</li><li>Für einen Fallback sind mindestens zwei HGS-Server erforderlich.</li><li>Server können entweder virtuell oder physisch (physischer Server mit TPM 2,0 empfohlen) sein. TPM 1,2 wird ebenfalls unterstützt)</li><li>Server Core-Installation von Windows Server 2016 oder höher</li><li>Netzwerkverbindung mit dem Fabric, das die http-oder [Fall Back Konfiguration](guarded-fabric-manage-branch-office.md#fallback-configuration) zulässt</li><li>Für die Zugriffs Überprüfung empfohlenes HTTPS-Zertifikat</li></ul> |
| Größe ändern | Der HGS-Server Knoten der mittleren Größe (8 Kerne/4 GB) kann 1.000 Hyper-V-Hosts verarbeiten. |
| Verwaltung | Bestimmen Sie bestimmte Personen, die HGS verwalten werden. Sie sollten von Fabric-Administratoren getrennt sein. Zum Vergleich können sich HGS-Cluster auf die gleiche Weise wie eine Zertifizierungsstelle (Certificate Authority, ca) im Hinblick auf administrative Isolation, physische Bereitstellung und allgemeine Sicherheits Empfindlichkeit vorstellen. |
| Active Directory des Host-Überwachungs Diensts | Standardmäßig installiert HGS seine eigenen internen Active Directory für die Verwaltung. Dabei handelt es sich um eine eigenständige, selbstverwaltete Gesamtstruktur, die für die Isolierung von HGS von Ihrem Fabric empfohlen wird.<br><br>Wenn Sie bereits über eine Active Directory-Gesamtstruktur mit hohen Privilegien verfügen, die Sie für die Isolation verwenden, können Sie diese Gesamtstruktur anstelle der HGS-Standard Gesamtstruktur verwenden. Es ist wichtig, dass HGS nicht zu einer Domäne in derselben Gesamtstruktur wie die Hyper-V-Hosts oder die Fabric-Verwaltungs Tools hinzugefügt werden. Dies könnte einem Fabric-Administrator ermöglichen, die Kontrolle über HGS zu erlangen. |
| Notfallwiederherstellung | Sie haben drei Möglichkeiten:<br><ol><li>Installieren Sie einen separaten HGS-Cluster in jedem Rechenzentrum, und autorisieren Sie abgeschirmte VMS, die sowohl in den primären als auch in den Sicherungs Datacenter ausgeführt werden. Dadurch ist es nicht mehr erforderlich, den Cluster über ein WAN zu Strecken, und Sie können virtuelle Maschinen so isolieren, dass Sie nur an dem vorgesehenen Standort ausgeführt werden.</li><li>Installieren Sie HGS in einem Stretch-Cluster zwischen zwei (oder mehr) Rechenzentren. Dies sorgt für Resilienz, wenn das WAN ausfällt, legt jedoch die Grenzen des Failoverclustering fest. Sie können Arbeits Auslastungen nicht zu einem Standort isolieren. eine VM, die zur Laufzeit an einem Standort autorisiert ist, kann auf jedem anderen Standort ausgeführt werden.</li><li>Registrieren Sie den Hyper-V-Host bei einem anderen HGS als Failover.</li></ol>Sie sollten auch alle HGS sichern, indem Sie die Konfiguration exportieren, sodass Sie jederzeit lokal wieder hergestellt werden können. Weitere Informationen finden Sie unter " [Export-hgsserverstate](https://docs.microsoft.com/powershell/module/hgsserver/export-hgsserverstate) " und " [Import-hgsserverstate](https://docs.microsoft.com/powershell/module/hgsserver/import-hgsserverstate)". |
| Schlüssel des Host-Überwachungs Diensts | Ein Host-Überwachungsdienst verwendet zwei asymmetrische Schlüsselpaare – einen Verschlüsselungsschlüssel und einen Signatur Schlüssel – die jeweils durch ein SSL-Zertifikat dargestellt werden. Es gibt zwei Optionen, um diese Schlüssel zu generieren:<br><ol><li>Interne Zertifizierungsstelle – Sie können diese Schlüssel mithilfe ihrer internen PKI-Infrastruktur generieren. Dies eignet sich für eine Rechenzentrumsumgebung.</li><li>Öffentlich vertrauenswürdige Zertifizierungsstellen – verwenden Sie einen Satz von Schlüsseln, die von einer öffentlich vertrauenswürdigen Zertifizierungsstelle abgerufen werden. Dies ist die Option, die Hoster verwenden sollten.</li></ol>Beachten Sie, dass es zwar möglich ist, selbst signierte Zertifikate zu verwenden, aber es ist nicht empfehlenswert für andere Bereitstellungs Szenarien als Proof-of-Concept-Labs.<br><br>Zusätzlich zu den HGS-Schlüsseln kann ein hoester "Bring your own Key" verwenden, wo Mandanten ihre eigenen Schlüssel bereitstellen können, damit einige (oder alle) Mandanten einen eigenen spezifischen HGS-Schlüssel haben können. Diese Option eignet sich für Hoster, die einen Out-of-Band-Prozess für Mandanten bereitstellen können, um Ihre Schlüssel hochzuladen. |
| Schlüsselspeicher des Host-Überwachungs Diensts | Um die größtmögliche Sicherheit zu erzielen, wird empfohlen, dass HGS-Schlüssel ausschließlich in einem Hardware Sicherheitsmodul (HSM) erstellt und gespeichert werden. Wenn Sie keine HSMs verwenden, wird dringend empfohlen, BitLocker auf den HGS-Servern anzuwenden. |

## <a name="fabric-admin-planning-for-guarded-hosts"></a>Fabric-Administrator Planung für geschützte Hosts

| Fläche | Details |
|------|---------|
| Hardware | <ul><li>Host Schlüssel Nachweis: Sie können eine beliebige vorhandene Hardware als überwachten Host verwenden. Es gibt einige Ausnahmen (um sicherzustellen, dass Ihr Host neue Sicherheitsmechanismen ab Windows Server 2016 verwenden kann, siehe [kompatible Hardware mit virtualisierungsbasiertem Windows Server 2016-Schutz der Code Integrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).</li><li>TPM-vertrauenswürdiger Nachweis: Sie können jede Hardware verwenden, die über die [Hardware Assurance zusätzliche Qualifikation](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/systems#system-server-assurance) verfügt, sofern diese ordnungsgemäß konfiguriert ist (siehe [Server Konfigurationen, die mit abgeschirmten VMS kompatibel sind, und virtualisierungsbasierter Schutz der Code Integrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md) für die jeweilige Konfiguration). Dies umfasst TPM 2,0 und UEFI, Version 2.3.1 c und höher.</li></ul> |
| Betriebssystem | Wir empfehlen die Verwendung der Server Core-Option für das Hyper-V-Host Betriebssystem. |
| Auswirkungen auf die Leistung | Auf der Grundlage von Leistungstests erwarten wir einen Dichteunterschied von ungefähr 5% zwischen der Ausführung von abgeschirmten VMS und nicht abgeschirmten VMS. Dies bedeutet Folgendes: Wenn auf einem bestimmten Hyper-V-Host 20 nicht abgeschirmte VMS ausgeführt werden können, wird davon ausgegangen, dass 19 abgeschirmte VMS ausgeführt werden können.<br><br>Stellen Sie sicher, dass Sie die Größe mit ihren typischen Workloads überprüfen. Beispielsweise gibt es möglicherweise einige Ausreißer mit intensiven Schreib orientierten e/a-Arbeits Auslastungen, die sich weiter auf den Dichteunterschied auswirken. |
| Überlegungen zu Filialen | Ab Windows Server, Version 1709, können Sie eine Fall Back-URL für einen virtualisierten HGS-Server angeben, der lokal als abgeschirmte VM in der Zweigstelle ausgeführt wird. Die Fall Back-URL kann verwendet werden, wenn die Zweigstelle die Konnektivität mit den HGS-Servern im Daten Center verliert. In früheren Versionen von Windows Server benötigt ein Hyper-V-Host, der in einer Zweigstelle ausgeführt wird, eine Verbindung mit dem Host-Überwachungsdienst, um abgeschirmte VMS einschalten oder Live migrieren zu können. Weitere Informationen finden Sie unter [Überlegungen zu Zweig](guarded-fabric-manage-branch-office.md)stellen. |
