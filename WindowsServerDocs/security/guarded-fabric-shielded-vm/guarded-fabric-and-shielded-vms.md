---
title: Übersicht über geschütztes Fabric und abgeschirmte VMs
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 579012be66969ffc584b4b4ea021f11acbbdfb78
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855901"
---
# <a name="guarded-fabric-and-shielded-vms-overview"></a>Übersicht über geschütztes Fabric und abgeschirmte VMs

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

## <a name="overview-of-the-guarded-fabric"></a>Übersicht zu geschütztem Fabric

Virtualisierungssicherheit ist ein bedeutender investitionsbereich in Hyper-V. Zusätzlich zum Schutz von Hosts oder anderen virtuellen Computern vor einem virtuellen Computer mit Malware müssen wir virtuelle Computer auch vor einem gefährdeten Host schützen. Dies ist eine grundlegende Gefahr für jede Virtualisierungsplattform heute, ob es sich um Hyper-V, VMware oder andere ist. Ganz einfach – wenn ein virtueller Computer aus einer Organisation herausgenommen wird (in böswilliger Absicht oder versehentlich), kann diese VM auf jedem anderen System ausgeführt werden. Der Schutz wertvoller Ressourcen in Ihrer Organisation, z.B. Domänencontroller, vertrauliche Dateiserver und Personalverwaltungssysteme, hat oberste Priorität.

Windows Server 2016 Hyper-V eingeführt, zum Schutz vor gefährdeten Virtualisierungs-Fabric von abgeschirmten VMs. Eine geschützte VM ist eine Generation 2 VM (unterstützt unter Windows Server 2012 und höher), die ein virtuelles TPM mit BitLocker verschlüsselt ist, und kann nur auf fehlerfreien und genehmigten Hosts im Fabric ausgeführt. Abgeschirmte VMs und geschütztes Fabric ermöglichen Clouddienstanbietern oder Private Cloud-Administratoren in Unternehmen, eine sichere Umgebung für Mandanten-VMs bereitzustellen. 

Ein geschütztes Fabric besteht aus:

- 1 Host-Überwachungsdienst (Host Guardian Service, HGS) (in der Regel ein Cluster mit 3 Knoten)
- Mindestens ein geschützter Host
- Eine Gruppe abgeschirmter virtueller Computer. Das folgende Diagramm zeigt, wie der Host-Überwachungsdienst den Nachweis verwendet, um sicherzustellen, dass nur bekannte und gültige Hosts die abgeschirmte VM starten können, und den Schlüsselschutzdienst, um die Schlüssel für abgeschirmte VMs sicher freizugeben.

Wenn ein Mandant abgeschirmte VMs erstellt, die auf einem geschützten Fabric ausgeführt werden, werden die Hyper-V-Hosts und die abgeschirmten VMs selbst durch den Host-Überwachungsdienst geschützt. Der Host-Überwachungsdienst bietet zwei verschiedene Dienste: Nachweis und Schlüsselschutz. Der Nachweisdienst stellt sicher, dass nur vertrauenswürdige Hyper-V-Hosts abgeschirmte VMs ausführen können, während der Schlüsselschutzdienst die Schlüssel bereitstellt, die erforderlich sind, um sie einzuschalten und ihre Livemigration zu anderen geschützten Hosts durchzuführen.

![Geschütztes Hostfabric](../media/Guarded-Fabric-Shielded-VM/Guarded-Host-Overview-Diagram.png)

## <a name="video-introduction-to-shielded-virtual-machines"></a>Video: Einführung in abgeschirmte VMs 

<iframe src="https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016/player" width="650" height="440" allowFullScreen frameBorder="0"></iframe>

## <a name="attestation-modes-in-the-guarded-fabric-solution"></a>Nachweismodi in der „Geschütztes Fabric“-Lösung

Der Host-Überwachungsdienst unterstützt verschiedene nachweismodi für ein geschütztes Fabric:

- TPM-vertrauenswürdiger Nachweis (Hardware-basiert)
- Host-schlüsselnachweis (auf der Grundlage der asymmetrischer Schlüsselpaaren)

Der TPM-vertrauenswürdige Nachweis wird empfohlen, da er stärkere Garantien bietet, wie in der folgenden Tabelle beschrieben, setzt aber voraus, dass Ihre Hyper-V-Hosts über TPM 2.0 verfügen. Wenn Sie derzeit kein TPM 2.0 oder jede TPM haben, können Sie den schlüsselnachweis Host. Wenn Sie sich für den Wechsel zum TPM-vertrauenswürdigen Nachweis entscheiden, wenn Sie neue Hardware erwerben, können Sie den Nachweismodus auf dem Host-Überwachungsdienst mit minimaler oder ohne Unterbrechung Ihres Fabrics wechseln.

| **Nachweismodus, den Sie für Hosts auswählen**                                            | **Hostgarantien** |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|**TPM-vertrauenswürdiger Nachweis:** Bietet den stärksten Schutz erfordert jedoch auch weitere Konfigurationsschritte erforderlich. Hosthardware und-Firmware müssen TPM 2.0 und UEFI 2.3.1 mit aktiviertem sicheren Start enthalten. | Überwachte Hosts werden genehmigt basierend auf ihre TPM-Identität gemessen Startsequenz und codeintegritätsrichtlinien, um sicherzustellen, dass sie nur genehmigten Code ausgeführt.| 
| **Host-schlüsselnachweise verwenden:** Soll vorhandene Hosthardware unterstützen, in dem kein TPM 2.0 verfügbar. Erfordert weniger Konfigurationsschritte und ist kompatibel mit gängiger Serverhardware. | Überwachte Hosts werden genehmigt basierend auf den Besitz des Schlüssels. | 

Einen anderen Modus mit dem Namen **Admin-vertrauenswürdiger Nachweis** ist veraltet, beginnend mit Windows Server-2019. In diesem Modus basiert auf der Mitgliedschaft von überwachten Hosts in einer angegebenen Sicherheitsgruppe in Active Directory Domain Services (AD DS). Host-schlüsselnachweis ähnliche hostidentifikation und ist leichter einzurichten. 

## <a name="assurances-provided-by-the-host-guardian-service"></a>Garantien, die der Host-Überwachungsdienst bietet

Der Host-Überwachungsdienst bietet zusammen mit den Methoden zum Erstellen abgeschirmter VMs die folgenden Garantien.

| **Typ der Garantie für VMs**                         | **Garantien für abgeschirmte VMs vom Schlüsselschutzdienst und von Erstellungsmethoden für abgeschirmte VMs** |
|----------------------------|--------------------------------------------------|
| **Mit BitLocker verschlüsselte Datenträger (Betriebssystemdatenträger und Datenträger für Daten)**   | Abgeschirmte VMs verwenden BitLocker zum Schutz ihrer Datenträger. Die BitLocker-Schlüssel, die zum Starten der VM und Entschlüsseln der Datenträger werden durch die abgeschirmte VM virtuelles TPM mithilfe von branchenweit bewährten Technologien wie z. B. sicheren kontrollierten Start geschützt. Während abgeschirmte VMs den Betriebssystemdatenträger nur automatisch verschlüsseln und schützen, können Sie der abgeschirmten VM angefügte [Datenlaufwerke gleichermaßen verschlüsseln](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-overview). |
| **Bereitstellung neuer abgeschirmter VMs aus "vertrauenswürdigen" vorlagedatenträgern/-Images** | Bei der Bereitstellung neuer abgeschirmter VMs können Mandanten angeben, welche Vorlagedatenträger sie als vertrauenswürdig einstufen. Abgeschirmte Vorlagedatenträger verfügen über Signaturen, die zu einem Zeitpunkt berechnet werden, wenn ihre Inhalte als vertrauenswürdig eingestuft werden. Die Datenträgersignaturen werden dann in einem Signaturenkatalog gespeichert, den Mandanten beim Erstellen von abgeschirmten VMs sicher dem Fabric bereitstellen. Während der Bereitstellung abgeschirmter VMs wird die Signatur des Datenträgers erneut berechnet und mit den vertrauenswürdigen Signaturen im Katalog verglichen. Wenn die Signaturen übereinstimmen, wird die abgeschirmte VM bereitgestellt. Wenn die Signaturen nicht übereinstimmen, gilt der abgeschirmte Vorlagedatenträger als nicht vertrauenswürdig, und bei der Bereitstellung tritt ein Fehler auf. |
| **Schutz von Kennwörtern und andere Geheimnisse, wenn eine abgeschirmte VM wird erstellt.** | Wenn Sie virtuelle Computer zu erstellen, ist es erforderlich, um sicherzustellen, dass vertrauliche Informationen wie die vertrauenswürdigen Datenträgersignaturen, RDP-Zertifikate und das Kennwort des lokalen Administratorkonto des virtuellen Computers, nicht an das Fabric weitergegeben werden. Diese vertraulichen Informationen befinden sich in einer als geschützte Datendatei (PDK-Datei) bezeichneten verschlüsselten Datei, die von Mandantenschlüsseln geschützt und vom Mandanten in das Fabric hochgeladen wird. Beim Erstellen einer abgeschirmten VM wählt der Mandant die zu verwendenden geschützten Daten aus, wodurch diese Informationen sicher nur den vertrauenswürdigen Komponenten innerhalb des geschützten Fabrics zur Verfügung gestellt werden. |
| **Mandanten steuern, in dem der virtuelle Computer gestartet werden kann** | Zu den geschützten Daten zählt auch eine Liste der geschützten Fabrics, in denen eine bestimmte abgeschirmte VM ausgeführt werden darf. Dies ist z.B. in Fällen hilfreich, in denen eine abgeschirmte VM sich typischerweise in einer lokalen privaten Cloud befindet, jedoch möglicherweise zur Wiederherstellung im Notfall zu einer anderen (öffentlichen oder privaten) Cloud migriert werden muss. Die Zielcloud oder das Zielfabric muss abgeschirmte VMs unterstützen, und die abgeschirmte VM muss dem Fabric die Ausführung genehmigen. |

## <a name="what-is-shielding-data-and-why-is-it-necessary"></a>Was sind geschützte Daten, und warum sind sie notwendig?

Eine geschützte Datendatei (auch als Bereitstellungsdatendatei oder PDK-Datei bezeichnet) ist eine verschlüsselte Datei, die ein Mandant oder VM-Besitzer erstellt, um wichtige VM-Konfigurationsinformationen, z.B. Administratorkennwort, RDP und andere identitätsbezogene Zertifikate, Domänenbeitritts-Anmeldeinformationen usw. zu schützen. Ein Fabricadministrator verwendet die geschützte Datendatei beim Erstellen einer abgeschirmten VM, kann die in der Datei enthaltenen Informationen allerdings nicht anzeigen oder verwenden.

Unter anderem enthalten geschützte Datendateien geheime Schlüssel wie z. B.:

- Administratoranmeldeinformationen
- Eine Antwortdatei („unattend.xml“)
- Eine Sicherheitsrichtlinie, die bestimmt, ob der virtuelle Computer erstellt, mit diesen geschützten Daten werden so konfiguriert, als abgeschirmt oder durch Verschlüsselung unterstützt
    - Beachten Sie, dass als abgeschirmt konfigurierte VMs vor Fabricadministratoren geschützt sind, durch Verschlüsselung unterstützte VMs hingegen nicht.
- Ein RDP-Zertifikat zum Sichern der Remotedesktopkommunikation mit der VM
- Ein Volumesignaturkatalog, der eine Liste vertrauenswürdiger, signierter Vorlagedatenträger-Signaturen enthält, auf deren Basis eine neue VM erstellt werden kann
- Eine Schlüsselschutzvorrichtung (Key Protector, KP), die definiert, auf welchen geschützten Fabrics eine abgeschirmte VM ausgeführt werden darf

Die geschützte Datendatei (PDK) gewährleistet, dass die VM wie vom Mandanten vorgesehen erstellt wird. Wenn der Mandant z.B. eine Antwortdatei („unattend.xml“) in die geschützte Datendatei einfügt und sie an den Hostinganbieter übermittelt, kann der Hostinganbieter sie nicht anzeigen oder ändern. Ebenso kann der Hostinganbieter beim Erstellen der abgeschirmten VM keine andere VHDX verwenden, da die geschützte Datendatei die Signaturen des vertrauenswürdigen Datenträgers enthält, auf dessen Basis abgeschirmte VMs erstellt werden können.

Die folgende Abbildung zeigt die geschützte Datendatei und zugehörige Konfigurationselemente.

![Geschützte Datendatei](../media/Guarded-Fabric-Shielded-VM/shielded-vms-shielding-data-file.png)

## <a name="what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run"></a>Welche Typen virtueller Computer kann ein geschütztes Fabric ausführen?

Geschützte Fabrics können VMs in einer von drei möglichen Arten ausführen:

1.  Eine normale VM, die gegenüber früheren Versionen von Hyper-V weder mehr noch weniger Schutz bietet
2.  Eine durch Verschlüsselung unterstützte VM, deren Schutzmaßnahmen durch einen Fabricadministrator konfiguriert werden können
3.  Eine abgeschirmte VM, bei der alle Schutzmaßnahmen aktiviert sind und nicht durch einen Fabricadministrator deaktiviert werden können

Durch Verschlüsselung unterstützte VMs sollen dort eingesetzt werden, wo die Fabricadministratoren voll vertrauenswürdig sind.  Beispielsweise könnte ein Unternehmen ein geschütztes Fabric bereitstellen, um sicherzustellen, dass VM-Datenträger zur Einhaltung von Vorschriften im Ruhezustand verschlüsselt werden. Fabricadministratoren können weiterhin komfortable Verwaltungsfunktionen wie VM-Konsolenverbindungen, PowerShell Direct und andere Tools zur täglichen Verwaltung und Problembehandlung verwenden.

Abgeschirmte virtuelle Computer dienen zur Verwendung in Fabrics, in denen Daten und Status des virtuellen Computers sowohl vor Fabricadministratoren als auch nicht vertrauenswürdiger Software, die möglicherweise auf den Hyper-V-Hosts ausgeführt wird, geschützt werden müssen. Abgeschirmte VMs würden z.B. nie eine VM-Konsolenverbindung zulassen, während ein Fabricadministrator diesen Schutz für durch Verschlüsselung unterstützte VMs aktivieren oder deaktivieren kann.

Die folgende Tabelle fasst die Unterschiede zwischen verschlüsselungsunterstützung und abgeschirmten VMs.

| Funktion        | Generation 2 – durch Verschlüsselung unterstützt     | Generation 2 – abgeschirmt         |
|----------|--------------------|----------------|
|Sicherer Start        | Ja, erforderlich, aber konfigurierbar        | Ja, erforderlich und erzwungen    |
|Vtpm               | Ja, erforderlich, aber konfigurierbar        | Ja, erforderlich und erzwungen    |
|Verschlüsseln des VM-Status und Livemigrations-Datenverkehr | Ja, erforderlich, aber konfigurierbar |  Ja, erforderlich und erzwungen  |
|Integrationskomponenten | Konfigurierbar durch Fabricadministrator      | Bestimmte Integrationskomponenten blockiert (z.B. Datenaustausch, PowerShell Direct) |
|Verbindung mit virtuellen Computern (Konsole), HID-Geräte (z.B. Tastatur, Maus) | Ein, kann nicht deaktiviert werden | Aktiviert auf Hosts mit Windows Server-Version 1803 ab. Auf früheren Hosts deaktiviert |
|COM/serielle Anschlüsse   | Unterstützt                             | Deaktiviert (kann nicht aktiviert werden) |
|Anfügen eines Debuggers (an der VM-Prozess)<sup>1</sup>| Unterstützt          | Deaktiviert (kann nicht aktiviert werden) |

<sup>1</sup> herkömmliche Debugger, die direkt an einen Prozess, z. B. WinDbg.exe, sind für abgeschirmte VMs blockiert, weil die VM Arbeitsprozess (VMWP.exe) eines geschützten Prozesses Lichts (PPL) ist. Alternative Debugtechniken, wie z. B. von LiveKd.exe, werden nicht blockiert. Im Gegensatz zu abgeschirmten VMs wird der Arbeitsprozess für die Verschlüsselung unterstützte VMs nicht ausgeführt, wie eine PPL, so wie von herkömmliche Debuggern WinDbg.exe weiterhin normal ausgeführt werden. 

Sowohl abgeschirmte als auch durch Verschlüsselung unterstützte VMs unterstützen weiterhin gängige Fabricverwaltungsfunktionen wie Livemigration, Hyper-V-Replikat, VM-Prüfpunkt usw.

## <a name="the-host-guardian-service-in-action-how-a-shielded-vm-is-powered-on"></a>Host-Überwachungsdienst in Aktion: Wie ein abgeschirmter virtuelle Computer eingeschaltet wird

![Geschützte Datendatei](../media/Guarded-Fabric-Shielded-VM/shielded-vms-how-a-shielded-vm-is-powered-on.png)

1. VM01 ist eingeschaltet.

    Bevor ein geschützter Host einen abgeschirmten virtuellen Computer einschalten kann, muss zuerst positiv nachgewiesen werden, dass er fehlerfrei ist. Um ihre Integrität nachzuweisen, muss sie dem Schlüsselschutzdienst (Key Protection Service, KPS) ein Integritätszertifikat vorlegen. Das Integritätszertifikat wird über den Nachweisprozess abgerufen.

2. Der Host fordert einen Nachweis an.

    Der geschützte Host fordert einen Nachweis an. Der Nachweismodus wird durch den Host-Überwachungsdienst vorgegeben:

    **TPM-vertrauenswürdiger Nachweis**: Hyper-V-Host sendet Informationen einschließlich:

       - TPM-identifizierende Informationen (seinen Endorsement Key)
       - Informationen zu Prozessen, die während der letzten Startsequenz (TCG-Protokoll) gestartet wurden
       - Informationen zur Codeintegritätsrichtlinie (CI)-Richtlinie, die auf dem Host angewendet wurde. 

       Attestation happens when the host starts and every 8 hours thereafter. If for some reason a host doesn't have an attestation certificate when a VM tries to start, this also triggers attestation.

    **Hosten Sie den schlüsselnachweis**: Hyper-V-Host sendet dem öffentlichen Hälfte des Schlüsselpaars. Host-Überwachungsdienst überprüft den Host Schlüssel registriert ist. 
    
    **Admin-vertrauenswürdiger Nachweis**: Hyper-V-Host sendet ein Kerberos-Ticket, das die Sicherheitsgruppen identifiziert, denen der Host ist. Der Host-Überwachungsdienst überprüft, ob der Host zu einer Sicherheitsgruppe gehört, die zuvor vom vertrauenswürdigen HGS-Administrator konfiguriert wurde.

3. Nachweis erfolgreich (oder mit Fehler).

    Der nachweismodus wird bestimmt, welche Überprüfungen erforderlich sind, erfolgreich bestätigen, dass der Host fehlerfrei ist. Mit TPM-vertrauenswürdiger Nachweis des Hosts TPM Identität, kontrollierten Starts und codeintegritätsrichtlinie überprüft. Mit den schlüsselnachweis hosten wird nur die Registrierung des hostschlüssels überprüft. 

4. Nachweiszertifikat wird an den Host gesendet.

    Vorausgesetzt, dass ein Nachweis war erfolgreich, ein Integritätszertifikat wird an den Host gesendet, und der Host gilt als "geschützt" (autorisiert zum Ausführen geschützter VMs). Der Host verwendet das Integritätszertifikat, um den Schlüsselschutzdienst zur sicheren Freigabe der Schlüssel zu autorisieren, die zur Arbeit mit abgeschirmten virtuellen Computern benötigt werden.

5. Der Host fordert einen VM-Schlüssel an.

    Geschützte Hosts besitzen keine Schlüssel zum Einschalten einer abgeschirmten VM (in diesem Fall VM01). Um die erforderlichen Schlüssel zu erhalten, muss der geschützte Host den folgenden KPS bieten:

    - Das aktuelle Integritätszertifikat
    - Einen verschlüsselten geheimen Schlüssel (Schlüsselschutzvorrichtung oder KP), der die erforderlichen Schlüssel zum Einschalten von VM01 enthält. Der geheime Schlüssel wird mit anderen Schlüsseln verschlüsselt, die nur KPS bekannt sind.

6. Freigabe des Schlüssels.

    KPS untersucht das Integritätszertifikat, um seine Gültigkeit zu überprüfen. Das Zertifikat darf nicht abgelaufen sein, und KPS muss dem Nachweisdienst vertrauen, der es ausgestellt hat.

7. Der Schlüssel wird an den Host zurückgegeben.

    Wenn das Integritätszertifikat gültig ist, versucht KPS, den geheimen Schlüssel zu entschlüsseln und die zum Einschalten der VM erforderlichen Schlüssel sicher zurückzugeben. Beachten Sie, dass die Schlüssel, der geschützte Host VBS verschlüsselt werden.

8. Host schaltet auf VM01 ein.

## <a name="guarded-fabric-and-shielded-vm-glossary"></a>Glossar zu geschütztem Fabric und abgeschirmten VMs

| Begriff              | Definition           |
|----------|------------|
| Host-Überwachungsdienst (Host Guardian Service, HGS) | Eine Windows Server-Rolle, die auf einem gesicherten Cluster von Bare-Metal-Servern installiert ist, die die Integrität eines Hyper-V-Hosts messen und Schlüssel für fehlerfreie Hyper-V-Hosts freigeben können, wenn sie abgeschirmte VMs einschalten bzw. mit ihnen eine Livemigration durchführen. Diese zwei Funktionen sind ein wesentlicher Bestandteil einer Lösung mit einer abgeschirmten VM und werden als **Nachweisdienst** und **Schlüsselschutzdienst** bezeichnet. |
| geschützter Host | Ein Hyper-V-Host, auf dem abgeschirmte VMs ausgeführt werden können. Ein Host kann nur betrachtet werden _überwachten_ wenn er wurde als fehlerfrei eingestuft wurde vom HGS nachweisdienst. Abgeschirmte VMs können nicht eingeschaltet oder live auf einen Hyper-V-Host migriert werden, für den noch kein Nachweis geführt werden konnte, bzw. der den Nachweis nicht erbringen konnte. |
| geschütztes Fabric    | Dies ist der Sammelbegriff zur Beschreibung eines Fabrics mit Hyper-V-Hosts und deren Host-Überwachungsdienst, der die Fähigkeit zum Verwalten und Ausführen abgeschirmter VMs hat. |
| abgeschirmter virtueller Computer (VM) | Ein virtueller Computer, der nur auf geschützten Hosts ausgeführt werden kann und vor Untersuchung, Manipulation und Diebstahl durch bösartige Fabricadministratoren und Hostmalware geschützt ist. |
| Fabricadministrator | Ein Public Cloud- oder Private Cloud-Administrator, der virtuelle Computer verwalten kann. Im Rahmen eines geschützten Fabrics hat ein Fabricadministrator keinen Zugriff auf abgeschirmte VMs oder die Richtlinien, die bestimmen, auf welchen Hosts abgeschirmte VMs ausgeführt werden können. |
| HGS-Administrator | Ein vertrauenswürdiger Administrator in der Public oder Private Cloud, der über die Berechtigung zum Verwalten der Richtlinien und des kryptografischen Materials für geschützte Hosts verfügt, d.h. Hosts, auf denen eine abgeschirmte VM ausgeführt werden kann.|
| Bereitstellungsdatendatei oder geschützte Datendatei (PDK-Datei) | Eine verschlüsselte Datei, die ein Mandant oder Benutzer erstellt, um wichtige Informationen der VM-Konfiguration zu speichern und vor dem Zugriff anderer Benutzern zu schützen. Eine geschützte Datendatei kann z.B. das Kennwort enthalten, das dem lokalen Administratorkonto zugewiesen wird, wenn die VM erstellt wird. |
| Virtualisierungsbasierte Sicherheit (VBS) | Eine Hyper-V-basierte Verarbeitungs- und speicherumgebung, die vor Administratoren geschützt ist. Virtueller sicherer Modus gibt dem System die Möglichkeit zum Speichern von Betriebssystemschlüsseln, die für den Betriebssystemadministrator unsichtbar sind.|
| virtuelles TPM | Eine virtualisierte Version eines Trusted Platform Module (TPM). Beginnen mit Hyper-V in Windows Server 2016, können Sie ein virtuelles TPM 2.0-Gerät bereitstellen, damit virtuelle Computer verschlüsselt werden können, wie ein physisches TPM die Verschlüsselung ein physisches Computers ermöglicht.|

## <a name="see-also"></a>Siehe auch

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
- Blog: [Datacenter and Private Cloud Security-Blog](https://blogs.technet.microsoft.com/datacentersecurity/)
- Video: [Einführung in abgeschirmte VMs](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- Video: [Einführung in abgeschirmte VMs mit Windows Server 2016 Hyper-V](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
