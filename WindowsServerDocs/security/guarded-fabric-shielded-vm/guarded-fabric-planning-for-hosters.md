---
title: Geschütztes Fabric und abgeschirmte VM Planungshandbuch für Hoster
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 854defc8-99f8-4573-82c0-f484e0785859
manager: dongill
author: nirb-ms
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f280fbe682ebf706ce6ea5b53ea8af5e6f39d75d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857811"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-hosters"></a>Geschütztes Fabric und abgeschirmte VM Planungshandbuch für Hoster

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema behandelt die planungsentscheidungen, die abgeschirmte virtuelle Computer zur Ausführung auf Ihrem Fabric vorgenommen werden müssen. Ob Sie eine vorhandene Hyper-V-Fabric aktualisieren oder erstellen eine neue Fabric, ausführen abgeschirmter VMs besteht aus zwei Hauptkomponenten:

- Die Host Guardian Service (HGS) bietet Nachweis und Schlüsselschutz, sodass Sie sicherstellen können, dass nur auf genehmigte und fehlerfrei Hyper-V-Hosts abgeschirmte VMs ausgeführt werden. 
- Genehmigt und fehlerfrei Hyper-V-Hosts, die auf dem abgeschirmte VMs (und reguläre VMs) ausführen können – diese werden als überwachten Hosts bezeichnet.

![Host-Überwachungsdiensts und überwachter host](../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-plus-host-diagram-basic.png)

## <a name="decision-1-trust-level-in-the-fabric"></a>Entscheidungsstruktur #1: Vertrauensebene im fabric

Wie Sie die Host-Überwachungsdiensts und überwachter Hyper-V-Hosts implementieren hängt hauptsächlich Stärke Vertrauensstellung, die Sie benötigen für eine im Fabric. Die Stärke der Vertrauensstellung wird durch den nachweismodus bestimmt. Es gibt zwei sich gegenseitig ausschließende Optionen aus:

1. TPM-vertrauenswürdiger Nachweis

    Wenn Ihr Ziel ist es, virtuelle Computer vor böswilligen Administratoren oder einem gefährdeten Fabric zu schützen, werden Sie TPM-vertrauenswürdiger Nachweis verwenden. Diese Option eignet sich gut für Szenarien mit mehreren Mandanten hosting als auch für wertvolle Assets in unternehmensumgebungen ausgeführt werden, z. B. Domänencontrollern oder Inhaltsserver wie SQL oder SharePoint.
    Hypervisor-geschützte codeintegritätsrichtlinien (HVCI) werden gemessen, und ihre Gültigkeit, die vom Host-Überwachungsdienst erzwungen werden, bevor der Host ausgeführt werden darf, abgeschirmte VMs. 

2. Host-schlüsselnachweis

    Wenn Ihre Anforderungen in erster Linie gesteuert werden nach Konformität, die erforderlich sind virtuelle Computer verschlüsselt im Ruhezustand sowie in-Flight, den schlüsselnachweis Host verwenden wird. Diese Option eignet sich gut für allgemeine Zwecke Rechenzentren, in denen Sie vertraut sind mit Hyper-V-Host und der Fabric-Administratoren den Zugriff auf die Gastbetriebssysteme von virtuellen Computern für die tägliche Wartung und Betrieb. 

    In diesem Modus ist der fabricadministrator allein verantwortlich für das Sicherstellen der Integritäts der Hyper-V-Hosts. 
    Da die Host-Überwachungsdienst wiedergegeben wird, keinen Teil bei der Entscheidung, was ist, oder kann nicht ausgeführt wird, funktioniert Schadsoftware und Debugger wie vorgesehen. 
    
    Debugger, die versuchen, direkt an einen Prozess (z. B. WinDbg.exe) angefügt werden jedoch für abgeschirmte VMs blockiert, da der VM Arbeitsprozess (VMWP.exe) eines geschützten Prozesses Lichts (PPL) ist. 
    Alternative Debugtechniken, wie z. B. von LiveKd.exe, werden nicht blockiert. 
    Im Gegensatz zu abgeschirmten VMs wird der Arbeitsprozess für die Verschlüsselung unterstützte VMs nicht ausgeführt, wie eine PPL, so wie von herkömmliche Debuggern WinDbg.exe weiterhin normal ausgeführt werden.

    Eine ähnliche nachweismodus, mit dem Namen Admin-vertrauenswürdiger Nachweis (Active Directory-basiert) ist veraltet ab Windows Server-2019. 

Die Vertrauensebene, die Sie auswählen, bestimmen die hardwareanforderungen für Hyper-V-Hosts sowie die Richtlinien, die im Fabric angewendet werden. Bei Bedarf können Sie Ihr geschützte Fabric mithilfe der vorhandenen Hardware und der Admin-vertrauenswürdiger Nachweis bereitstellen und dann in der TPM-vertrauenswürdiger Nachweis konvertieren, wenn die Hardware aktualisiert wurde, und Sie zum Fabric-Sicherheit zu erhöhen müssen.

## <a name="decision-2-existing-hyper-v-fabric-versus-a-new-separate-hyper-v-fabric"></a>Entscheidungsstruktur #2: Vorhandene Hyper-V-Fabric im Vergleich zu einem neuen separaten Hyper-V-fabric

Wenn Sie eine vorhandene Fabric verfügen (Hyper-V oder anderweitig), ist es sehr wahrscheinlich, dass Sie ihn zum Ausführen geschützter VMs zusammen mit regulären virtuellen Computern verwenden können. Einige Kunden entscheiden sich für abgeschirmte VMs in ihre vorhandenen Tools und -Fabrics zu integrieren, während andere trennen Sie das Fabric aus geschäftlichen Gründen.

## <a name="hgs-admin-planning-for-the-host-guardian-service"></a>HGS-Administrator, die Planung für die Host-Überwachungsdienst

Die Host Guardian Service (HGS) in eine äußerst sichere Umgebung, Bereitstellen von, ob die Freigabe, die auf einem dedizierten physischen Server, eine abgeschirmte VM, einen virtuellen Computer in einem isolierten Hyper-V-Host (getrennt aus dem Fabric schützenden) bzw. auf eine, die mithilfe ein anderen Azure logisch getrennt das Abonnement.   

| Bereich | Details |
|------|---------|
| Installationsanforderungen | <ul><li>Ein Server (drei Knoten-Cluster für hohe Verfügbarkeit empfohlen)</li><li>Für ein Fallback sind mindestens zwei HGS-Server erforderlich</li><li>Server werden können, ob virtuell oder physisch (physische Server mit TPM 2.0 empfohlen. TPM 1.2 ebenfalls unterstützt)</li><li>Server Core-Installation von Windows Server 2016 oder höher</li><li>Netzwerk-sichtverbindung zum Zulassen von HTTP-Fabric oder [Fallbackkonfiguration](guarded-fabric-manage-branch-office.md#fallback-configuration)</li><li>HTTPS-Zertifikat für zugriffsvalidierungen empfohlen</li></ul> |
| Größenanpassung | Jedem Serverknoten für mittelgroße (8 Kerne/4 GB) Host-Überwachungsdienst kann 1.000 Hyper-V-Hosts behandeln. |
| Management | Legen Sie bestimmte Personen, die Host-Überwachungsdienst verwalten. Sie sollten getrennt von Fabric-Administratoren sein. Für den Vergleich können Host-Überwachungsdienst-Cluster auf die gleiche Weise wie eine Zertifizierungsstelle (CA) in Bezug auf administrative Isolation "," physikalischen Bereitstellung "und" Grad der Vertraulichkeit betrachtet werden. |
| Host Guardian Service, Active Directory | Host-Überwachungsdienst installiert standardmäßig seinen eigenen internen Active Directory für die Verwaltung. Dies ist eine eigenständige, selbstverwalteten Gesamtstruktur und ist die empfohlene Konfiguration zum Isolieren von Host-Überwachungsdienst aus Ihr Fabric.<br><br>Wenn Sie bereits über eine sehr privilegierten Active Directory-Gesamtstruktur, die Sie für die Isolation verwenden verfügen, können Sie anstelle der Host-Überwachungsdienst standardmäßige Gesamtstruktur dieser Gesamtstruktur. Es ist wichtig, dass der Host-Überwachungsdienst nicht zu einer Domäne in der gleichen Gesamtstruktur wie die Hyper-V-Hosts oder der Fabric-Management-Tools verknüpft ist. Auf diese Weise kann ein fabricadministrator Kontrolle über die Host-Überwachungsdienst ermöglichen. |
| Notfallwiederherstellung | Drei Optionen stehen zur Verfügung:<br><ol><li>Installieren Sie einen separaten Host-Überwachungsdienst-Cluster in jedem Datencenter aus, und Autorisieren von abgeschirmten VMs in der primären und den backup-Rechenzentren ausgeführt. Dies vermeidet die Notwendigkeit, die stretch-Cluster in einem WAN und ermöglicht es Ihnen, virtuelle Maschinen zu isolieren, sodass sie nur in den angegebenen Standort ausgeführt werden.</li><li>Installieren Sie Host-Überwachungsdienst auf einem Stretched Cluster zwischen Rechenzentren, die zwei (oder mehr). Dies bietet Flexibilität, wenn das WAN ausfällt, sondern die Grenzen des Failover legt-Clusterunterstützung. Sie können keine Workloads mit einem Standort isolieren; ein virtuellen Computer berechtigt, führen Sie an einem Standort kann in jedem anderen ausführen.</li><li>Registrieren Sie Ihre Hyper-V-Host mit einem anderen Host-Überwachungsdienst als Failover.</li></ol>Sie sollten auch jeder Host-Überwachungsdienst sichern, durch den Export von der Konfigurations, damit Sie immer lokal wiederhergestellt werden können. Weitere Informationen finden Sie unter [Export-HgsServerState](https://technet.microsoft.com/library/mt652164.aspx) und [Import-HgsServerState](https://technet.microsoft.com/library/mt652168.aspx). |
| Host-Überwachungsdienst-Schlüssel | Eine Host-Überwachungsdienst verwendet zwei asymmetrische Schlüsselpaaren, einen Verschlüsselungsschlüssel und einen Signaturschlüssel, jeweils durch ein SSL-Zertifikat dargestellt werden. Es gibt zwei Möglichkeiten, um diese Schlüssel zu generieren:<br><ol><li>Interne Zertifizierungsstelle – können Sie diese über Ihre interne PKI-Infrastruktur Schlüssel generieren. Dies eignet sich für ein Datencenter-Umgebung.</li><li>Öffentlich vertrauenswürdige Zertifizierungsstellen – verwenden Sie einen Satz von Schlüsseln, die von einer öffentlich vertrauenswürdigen Zertifizierungsstelle abgerufen. Dies ist die Option, die Hoster verwendet werden soll.</li></ol>Beachten Sie, dass es zwar möglich, die selbstsignierten Zertifikate verwenden, es sich nicht für die Bereitstellung als Proof-of-Concept-Labs empfiehlt.<br><br>Darüber hinaus müssen auch die Host-Überwachungsdienst-Schlüssel können ein Hoster "bring your own Key,", in denen Mandanten ihre eigenen Schlüssel bereitstellen kann, damit einige (oder alle)-Mandanten ihre eigenen bestimmte Host-Überwachungsdienst-Schlüssel haben. Diese Option eignet sich für Hoster, die einen Out-of-Band-Prozess für Mandanten, um ihren Schlüssel hochladen bereitstellen können. |
| Host-Überwachungsdienst-Schlüsselspeicher | Für die höchste Sicherheit zu gewährleisten empfehlen wir, dass der Host-Überwachungsdienst-Schlüssel erstellt und ausschließlich in einem Hardwaresicherheitsmodul (HSM) gespeichert werden. Wenn Sie kein HSM verwenden, empfiehlt es sich dringend, Anwenden von BitLocker auf den Host-Überwachungsdienst-Servern. |

## <a name="fabric-admin-planning-for-guarded-hosts"></a>Fabric Admin Planen von überwachten hosts

| Bereich | Details |
|------|---------|
| Hardware | <ul><li>Host-schlüsselnachweise verwenden: Sie können die vorhandenen Hardware als überwachten Host verwenden. Es gibt jedoch einige Ausnahmen (um sicherzustellen, dass Ihr Host die neuen Sicherheitsmechanismen, die ab Windows Server 2016 verwenden kann, finden Sie unter [kompatible Hardware mit Windows Server 2016-Virtualisierung mit dem Schutz der Codeintegrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).</li><li>TPM-vertrauenswürdiger Nachweis: Können Sie keine Hardware, die die [Hardware Assurance zusätzliche Qualifikation](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/systems#system-server-assurance) solange er entsprechend konfiguriert ist (finden Sie unter [Server-Konfigurationen, die kompatibel mit abgeschirmten VMs sind und Virtualisierung basierende Schutz der Codeintegrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md) für die jeweilige Konfiguration). Dies schließt TPM 2.0 und UEFI Version 2.3. 1 c und höher.</li></ul> |
| Betriebssystem | Es wird empfohlen, mithilfe von Server Core-Option für die Hyper-V-Host-Betriebssystem. |
| Auswirkungen auf die Leistung | Basierend auf Leistung testen, die wir erwarten eine ungefähr 5 % Dichte-Differenz zwischen dem ausgeführtem geschützt, und nicht abgeschirmten virtuellen Computern. Dies bedeutet, dass wenn 20 nicht geschützte virtuelle Computer von ein bestimmter Hyper-V-Host ausgeführt werden kann, wir erwarten, dass es 19 abgeschirmte VMs ausführen kann.<br><br>Stellen Sie sicher, um zu überprüfen, ob zur größenanpassung für Ihre typischen Workloads. Möglicherweise gibt es z. B. einiger Ausreißer mit intensiven schreibende e/a-Workloads, die den Unterschied Dichte weiter auswirken. |
| Überlegungen zu Filialen | Ab Windows Server-Version 1709, können Sie eine alternative URL für einen virtualisierten Host-Überwachungsdienst-Server, die lokal ausgeführt als eine abgeschirmte VM in der Zweigstelle angeben. Der fallback-URL kann verwendet werden, wenn die Zweigstelle Konnektivität mit HGS-Servern im Datencenter verliert. In früheren Versionen von Windows Server ein Hyper-V-Host, die in einen Branch Office Anforderungen Konnektivität Host-Überwachungsdienst einschalten oder Livemigration ausgeführt von abgeschirmten VMs. Weitere Informationen finden Sie unter [Branch Office Überlegungen](guarded-fabric-manage-branch-office.md). |
