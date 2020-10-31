---
title: Übersicht über geschütztes Fabric und abgeschirmte VMs
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 62098234f75a35d5c7ab4d386e5d2ce41aaa3641
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071142"
---
# <a name="guarded-fabric-and-shielded-vms-overview"></a>Übersicht über geschütztes Fabric und abgeschirmte VMs

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

## <a name="overview-of-the-guarded-fabric"></a>Übersicht zu geschütztem Fabric

Virtualisierungssicherheit ist ein wichtiger Investitionsbereich in Hyper-V. Zusätzlich zum Schutz von Hosts oder anderen virtuellen Computern vor einem virtuellen Computer mit Malware müssen wir virtuelle Computer auch vor einem gefährdeten Host schützen. Dies ist eine grundlegende Gefahr für jede Virtualisierungsplattform, egal ob Hyper-V, VMware oder eine andere Virtualisierungsplattform. Ganz einfach – wenn ein virtueller Computer aus einer Organisation herausgenommen wird (in böswilliger Absicht oder versehentlich), kann diese VM auf jedem anderen System ausgeführt werden. Der Schutz wertvoller Ressourcen in Ihrer Organisation, z.B. Domänencontroller, vertrauliche Dateiserver und Personalverwaltungssysteme, hat oberste Priorität.

Zur Unterstützung des Schutzes vor kompromittiertem virtualisierungsfabric führte Windows Server 2016 Hyper-V abgeschirmte VMS ein. Eine abgeschirmte VM ist eine VM der Generation 2 (unterstützt unter Windows Server 2012 und höher), die über ein virtuelles TPM verfügt, mit BitLocker verschlüsselt ist und nur auf fehlerfreien und genehmigten Hosts im Fabric ausgeführt werden kann. Abgeschirmte VMs und geschütztes Fabric ermöglichen Clouddienstanbietern oder Private Cloud-Administratoren in Unternehmen, eine sichere Umgebung für Mandanten-VMs bereitzustellen.

Ein geschütztes Fabric besteht aus:

- 1 Host-Überwachungsdienst (Host Guardian Service, HGS) (in der Regel ein Cluster mit 3 Knoten)
- Mindestens ein geschützter Host
- Eine Gruppe abgeschirmter virtueller Computer. Das folgende Diagramm zeigt, wie der Host-Überwachungsdienst den Nachweis verwendet, um sicherzustellen, dass nur bekannte und gültige Hosts die abgeschirmte VM starten können, und den Schlüsselschutzdienst, um die Schlüssel für abgeschirmte VMs sicher freizugeben.

Wenn ein Mandant abgeschirmte VMs erstellt, die auf einem geschützten Fabric ausgeführt werden, werden die Hyper-V-Hosts und die abgeschirmten VMs selbst durch den Host-Überwachungsdienst geschützt. Der Host-Überwachungsdienst bietet zwei verschiedene Dienste: Nachweis und Schlüsselschutz. Der Nachweisdienst stellt sicher, dass nur vertrauenswürdige Hyper-V-Hosts abgeschirmte VMs ausführen können, während der Schlüsselschutzdienst die Schlüssel bereitstellt, die erforderlich sind, um sie einzuschalten und ihre Livemigration zu anderen geschützten Hosts durchzuführen.

![Geschütztes Hostfabric](../media/Guarded-Fabric-Shielded-VM/Guarded-Host-Overview-Diagram.png)

## <a name="video-introduction-to-shielded-virtual-machines"></a>Video: Einführung in abgeschirmte virtuelle Maschinen

> [!VIDEO https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016/player]

## <a name="attestation-modes-in-the-guarded-fabric-solution"></a>Nachweismodi in der „Geschütztes Fabric“-Lösung

Die HGS unterstützen verschiedene Nachweis Modi für ein geschütztes Fabric:

- TPM-vertrauenswürdiger Nachweis (Hardware basiert)
- Host Schlüssel Nachweis (basierend auf asymmetrischen Schlüsselpaaren)

Der TPM-vertrauenswürdige Nachweis wird empfohlen, da er stärkere Garantien bietet, wie in der folgenden Tabelle beschrieben, setzt aber voraus, dass Ihre Hyper-V-Hosts über TPM 2.0 verfügen. Wenn Sie derzeit nicht über TPM 2,0 oder ein TPM verfügen, können Sie den Host Schlüssel Nachweis verwenden. Wenn Sie sich für den Wechsel zum TPM-vertrauenswürdigen Nachweis entscheiden, wenn Sie neue Hardware erwerben, können Sie den Nachweismodus auf dem Host-Überwachungsdienst mit minimaler oder ohne Unterbrechung Ihres Fabrics wechseln.

| **Nachweismodus, den Sie für Hosts auswählen** | **Hostgarantien** |
|--|--|
| **TPM-vertrauenswürdiger Nachweis:** bietet den stärksten Schutz, erfordert jedoch auch weitere Konfigurationsschritte. Host Hardware und Firmware müssen TPM 2,0 und UEFI 2.3.1 mit aktiviertem sicheren Start einschließen. | Geschützte Hosts werden basierend auf der TPM-Identität, der gemessenen Startsequenz und den Code Integritäts Richtlinien genehmigt, um sicherzustellen, dass Sie nur genehmigten Code ausführen. |
| **Host Schlüssel Nachweis:** Dient zur Unterstützung vorhandener Host Hardware, bei der TPM 2,0 nicht verfügbar ist. Erfordert weniger Konfigurationsschritte und ist kompatibel mit gängiger Serverhardware. | Geschützte Hosts werden basierend auf dem Besitz des Schlüssels genehmigt. |

Ein anderer Modus mit dem Namen **Admin-Trusted Nachweis** ist ab Windows Server 2019 veraltet. Dieser Modus basiert auf der überwachten Host Mitgliedschaft in einer festgelegten Active Directory Domain Services (AD DS)-Sicherheitsgruppe. Der Host Schlüssel Nachweis bietet eine ähnliche Host Identifizierung und ist leichter einzurichten.

## <a name="assurances-provided-by-the-host-guardian-service"></a>Garantien, die der Host-Überwachungsdienst bietet

Der Host-Überwachungsdienst bietet zusammen mit den Methoden zum Erstellen abgeschirmter VMs die folgenden Garantien.

| **Typ der Garantie für VMs**                         | **Garantien für abgeschirmte VMs vom Schlüsselschutzdienst und von Erstellungsmethoden für abgeschirmte VMs.** |
|----------------------------|--------------------------------------------------|
| **Mit BitLocker verschlüsselte Datenträger (Betriebssystemdatenträger und Datenträger)**   | Abgeschirmte VMs verwenden BitLocker zum Schutz ihrer Datenträger. Die BitLocker-Schlüssel, die zum Starten des virtuellen Computers und zum Entschlüsseln der Datenträger erforderlich sind, werden vom virtuellen TPM der abgeschirmten VM mithilfe von branchenspezifischen Technologien wie dem sicheren gemessenen Start geschützt. Während abgeschirmte VMs den Betriebssystemdatenträger nur automatisch verschlüsseln und schützen, können Sie der abgeschirmten VM angefügte [Datenlaufwerke gleichermaßen verschlüsseln](/windows/security/information-protection/bitlocker/bitlocker-overview). |
| **Bereitstellung neuer abgeschirmter VMS aus "vertrauenswürdigen" Vorlagen Datenträgern/Images** | Bei der Bereitstellung neuer abgeschirmter VMs können Mandanten angeben, welche Vorlagedatenträger sie als vertrauenswürdig einstufen. Abgeschirmte Vorlagedatenträger verfügen über Signaturen, die zu einem Zeitpunkt berechnet werden, wenn ihre Inhalte als vertrauenswürdig eingestuft werden. Die Datenträgersignaturen werden dann in einem Signaturenkatalog gespeichert, den Mandanten beim Erstellen von abgeschirmten VMs sicher dem Fabric bereitstellen. Während der Bereitstellung abgeschirmter VMs wird die Signatur des Datenträgers erneut berechnet und mit den vertrauenswürdigen Signaturen im Katalog verglichen. Wenn die Signaturen übereinstimmen, wird die abgeschirmte VM bereitgestellt. Wenn die Signaturen nicht übereinstimmen, gilt der abgeschirmte Vorlagedatenträger als nicht vertrauenswürdig, und bei der Bereitstellung tritt ein Fehler auf. |
| **Schutz von Kennwörtern und anderen geheimen Schlüsseln beim Erstellen einer abgeschirmten VM** | Beim Erstellen von VMS muss sichergestellt werden, dass die VM-Geheimnisse, wie z. b. die vertrauenswürdigen Datenträger Signaturen, RDP-Zertifikate und das Kennwort des lokalen Administrator Kontos der VM, nicht an das Fabric weitergegeben werden. Diese vertraulichen Informationen befinden sich in einer als geschützte Datendatei (PDK-Datei) bezeichneten verschlüsselten Datei, die von Mandantenschlüsseln geschützt und vom Mandanten in das Fabric hochgeladen wird. Beim Erstellen einer abgeschirmten VM wählt der Mandant die zu verwendenden geschützten Daten aus, wodurch diese Informationen sicher nur den vertrauenswürdigen Komponenten innerhalb des geschützten Fabrics zur Verfügung gestellt werden. |
| **Mandanten steuern, wo die VM gestartet werden kann.** | Zu den geschützten Daten zählt auch eine Liste der geschützten Fabrics, in denen eine bestimmte abgeschirmte VM ausgeführt werden darf. Dies ist z.B. in Fällen hilfreich, in denen eine abgeschirmte VM sich typischerweise in einer lokalen privaten Cloud befindet, jedoch möglicherweise zur Wiederherstellung im Notfall zu einer anderen (öffentlichen oder privaten) Cloud migriert werden muss. Die Zielcloud oder das Zielfabric muss abgeschirmte VMs unterstützen, und die abgeschirmte VM muss dem Fabric die Ausführung genehmigen. |

## <a name="what-is-shielding-data-and-why-is-it-necessary"></a>Was sind geschützte Daten, und warum sind sie notwendig?

Eine geschützte Datendatei (auch als Bereitstellungsdatendatei oder PDK-Datei bezeichnet) ist eine verschlüsselte Datei, die ein Mandant oder VM-Besitzer erstellt, um wichtige VM-Konfigurationsinformationen, z.B. Administratorkennwort, RDP und andere identitätsbezogene Zertifikate, Domänenbeitritts-Anmeldeinformationen usw. zu schützen. Ein Fabricadministrator verwendet die geschützte Datendatei beim Erstellen einer abgeschirmten VM, kann die in der Datei enthaltenen Informationen allerdings nicht anzeigen oder verwenden.

Unter anderem enthalten geschützte Datendateien geheime Schlüssel wie z. B.:

- Administratoranmeldeinformationen
- Eine Antwortdatei („unattend.xml“)
- Eine Sicherheitsrichtlinie, die bestimmt, ob mit diesen Schutz Daten erstellte virtuelle Computer als abgeschirmt oder Verschlüsselung unterstützt werden.
    - Beachten Sie, dass als abgeschirmt konfigurierte VMs vor Fabricadministratoren geschützt sind, durch Verschlüsselung unterstützte VMs hingegen nicht.
- Ein RDP-Zertifikat zum Sichern der Remotedesktopkommunikation mit der VM
- Ein Volumesignaturkatalog, der eine Liste vertrauenswürdiger, signierter Vorlagedatenträger-Signaturen enthält, auf deren Basis eine neue VM erstellt werden kann
- Eine Schlüsselschutzvorrichtung (Key Protector, KP), die definiert, auf welchen geschützten Fabrics eine abgeschirmte VM ausgeführt werden darf

Die geschützte Datendatei (PDK) gewährleistet, dass die VM wie vom Mandanten vorgesehen erstellt wird. Wenn der Mandant z.B. eine Antwortdatei („unattend.xml“) in die geschützte Datendatei einfügt und sie an den Hostinganbieter übermittelt, kann der Hostinganbieter sie nicht anzeigen oder ändern. Ebenso kann der Hostinganbieter beim Erstellen der abgeschirmten VM keine andere VHDX verwenden, da die geschützte Datendatei die Signaturen des vertrauenswürdigen Datenträgers enthält, auf dessen Basis abgeschirmte VMs erstellt werden können.

Die folgende Abbildung zeigt die geschützte Datendatei und zugehörige Konfigurationselemente.

![Geschützte Datendatei](../media/Guarded-Fabric-Shielded-VM/shielded-vms-shielding-data-file.png)

## <a name="what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run"></a>Welche Typen virtueller Computer kann ein geschütztes Fabric ausführen?

Geschützte Fabrics können VMs in einer von drei möglichen Arten ausführen:

1. Eine normale VM, die gegenüber früheren Versionen von Hyper-V weder mehr noch weniger Schutz bietet
2. Eine durch Verschlüsselung unterstützte VM, deren Schutzmaßnahmen durch einen Fabricadministrator konfiguriert werden können
3. Eine abgeschirmte VM, bei der alle Schutzmaßnahmen aktiviert sind und nicht durch einen Fabricadministrator deaktiviert werden können

Durch Verschlüsselung unterstützte VMs sollen dort eingesetzt werden, wo die Fabricadministratoren voll vertrauenswürdig sind.  Beispielsweise könnte ein Unternehmen ein geschütztes Fabric bereitstellen, um sicherzustellen, dass VM-Datenträger zur Einhaltung von Vorschriften im Ruhezustand verschlüsselt werden. Fabricadministratoren können weiterhin komfortable Verwaltungsfunktionen wie VM-Konsolenverbindungen, PowerShell Direct und andere Tools zur täglichen Verwaltung und Problembehandlung verwenden.

Abgeschirmte virtuelle Computer dienen zur Verwendung in Fabrics, in denen Daten und Status des virtuellen Computers sowohl vor Fabricadministratoren als auch nicht vertrauenswürdiger Software, die möglicherweise auf den Hyper-V-Hosts ausgeführt wird, geschützt werden müssen. Abgeschirmte VMs würden z.B. nie eine VM-Konsolenverbindung zulassen, während ein Fabricadministrator diesen Schutz für durch Verschlüsselung unterstützte VMs aktivieren oder deaktivieren kann.

In der folgenden Tabelle werden die Unterschiede zwischen Verschlüsselungs unterstütztem und abgeschirmten VMS zusammengefasst.

| Funktion        | Generation 2 – durch Verschlüsselung unterstützt     | Generation 2 – abgeschirmt         |
|----------|--------------------|----------------|
|Sicherer Start        | Ja, erforderlich, aber konfigurierbar        | Ja, erforderlich und erzwungen    |
|Vtpm               | Ja, erforderlich, aber konfigurierbar        | Ja, erforderlich und erzwungen    |
|Verschlüsseln des VM-Status und Livemigrations-Datenverkehr | Ja, erforderlich, aber konfigurierbar |  Ja, erforderlich und erzwungen  |
|Integrationskomponenten | Konfigurierbar durch Fabricadministrator      | Bestimmte Integrationskomponenten blockiert (z.B. Datenaustausch, PowerShell Direct) |
|Verbindung mit virtuellen Computern (Konsole), HID-Geräte (z.B. Tastatur, Maus) | Ein, kann nicht deaktiviert werden | Aktiviert auf Hosts ab Windows Server-Version 1803; Auf früheren Hosts deaktiviert |
|COM/serielle Anschlüsse   | Unterstützt                             | Deaktiviert (kann nicht aktiviert werden) |
|Anfügen eines Debuggers (an den VM-Prozess)<sup>1</sup>| Unterstützt          | Deaktiviert (kann nicht aktiviert werden) |

<sup>1</sup> herkömmliche Debugger, die direkt an einen Prozess angefügt werden (z. b. WinDbg.exe), werden für abgeschirmte VMS blockiert, da der Arbeitsprozess des virtuellen Computers (VMWP.exe) eine geschützte Prozess Beleuchtung (PPL) ist.
Alternative Debuggingtechniken, z. b. die von LiveKd.exe verwendeten, werden nicht blockiert.
Anders als bei abgeschirmten VMS wird der Arbeitsprozess für die Verschlüsselung unterstützte VMS nicht als ppl ausgeführt, sodass herkömmliche Debugger wie WinDbg.exe weiterhin normal funktionieren.

Sowohl abgeschirmte als auch durch Verschlüsselung unterstützte VMs unterstützen weiterhin gängige Fabricverwaltungsfunktionen wie Livemigration, Hyper-V-Replikat, VM-Prüfpunkt usw.

## <a name="the-host-guardian-service-in-action-how-a-shielded-vm-is-powered-on"></a>Der Host-Überwachungsdienst in Aktion: Wie ein abgeschirmter virtuelle Computer eingeschaltet wird

![Geschützte Datendatei](../media/Guarded-Fabric-Shielded-VM/shielded-vms-how-a-shielded-vm-is-powered-on.png)

1. **VM01 ist eingeschaltet.** Bevor ein geschützter Host einen abgeschirmten virtuellen Computer einschalten kann, muss zuerst positiv nachgewiesen werden, dass er fehlerfrei ist. Um ihre Integrität nachzuweisen, muss sie dem Schlüsselschutzdienst (Key Protection Service, KPS) ein Integritätszertifikat vorlegen. Das Integritätszertifikat wird über den Nachweisprozess abgerufen.

2. **Der Host fordert einen Nachweis an.** Der geschützte Host fordert einen Nachweis an. Der Nachweismodus wird durch den Host-Überwachungsdienst vorgegeben:

    - **TPM-vertrauenswürdiger** Nachweis: der Hyper-V-Host sendet Informationen, die Folgendes beinhalten:
      - TPM-identifizierende Informationen (seinen Endorsement Key)
      - Informationen zu Prozessen, die während der letzten Startsequenz (TCG-Protokoll) gestartet wurden
      - Informationen zur Richtlinie für die Code Integrität (CI), die auf dem Host angewendet wurde.

        Nachweis geschieht beim Starten des Hosts und danach alle 8 Stunden. Wenn ein Host aus irgendeinem Grund kein Nachweis Zertifikat besitzt, wenn ein virtueller Computer versucht, zu starten, wird auch der Nachweis ausgelöst.

    - **Host Schlüssel** Nachweis: der Hyper-V-Host sendet die öffentliche Hälfte des Schlüssel Paars. HGS überprüft, dass der Host Schlüssel registriert ist.

    - **Admin-vertrauenswürdiger Nachweis** : Hyper-V-Host sendet ein Kerberos-Ticket, das die Sicherheitsgruppen identifiziert, zu denen der Host gehört. Der Host-Überwachungsdienst überprüft, ob der Host zu einer Sicherheitsgruppe gehört, die zuvor vom vertrauenswürdigen HGS-Administrator konfiguriert wurde.

3. **Nachweis erfolgreich (oder mit Fehler).** Der Nachweis Modus bestimmt, welche Überprüfungen erforderlich sind, um erfolgreich zu bestätigen, dass der Host fehlerfrei ist. Mit dem TPM-vertrauenswürdigen Nachweis werden die TPM-Identität des Hosts, Start Messungen und die Code Integritätsrichtlinie überprüft. Beim Nachweis des Host Schlüssels wird nur die Registrierung des Host Schlüssels überprüft.

4. **Nachweiszertifikat wird an den Host gesendet.** Wenn der Nachweis erfolgreich war, wird ein Integritäts Zertifikat an den Host gesendet, und der Host wird als "geschützt" (autorisiert zum Ausführen von abgeschirmten VMS) betrachtet. Der Host verwendet das Integritätszertifikat, um den Schlüsselschutzdienst zur sicheren Freigabe der Schlüssel zu autorisieren, die zur Arbeit mit abgeschirmten virtuellen Computern benötigt werden.

5. **Der Host fordert einen VM-Schlüssel an.** Geschützte Hosts besitzen keine Schlüssel zum Einschalten einer abgeschirmten VM (in diesem Fall VM01). Um die erforderlichen Schlüssel zu erhalten, muss der geschützte Host den folgenden KPS bieten:

   - Das aktuelle Integritätszertifikat
   - Einen verschlüsselten geheimen Schlüssel (Schlüsselschutzvorrichtung oder KP), der die erforderlichen Schlüssel zum Einschalten von VM01 enthält. Der geheime Schlüssel wird mit anderen Schlüsseln verschlüsselt, die nur KPS bekannt sind.

6. **Freigabe des Schlüssels.** KPS untersucht das Integritätszertifikat, um seine Gültigkeit zu überprüfen. Das Zertifikat darf nicht abgelaufen sein, und KPS muss dem Nachweisdienst vertrauen, der es ausgestellt hat.

7. **Der Schlüssel wird an den Host zurückgegeben.** Wenn das Integritätszertifikat gültig ist, versucht KPS, den geheimen Schlüssel zu entschlüsseln und die zum Einschalten der VM erforderlichen Schlüssel sicher zurückzugeben. Beachten Sie, dass die Schlüssel in den VSB des geschützten Hosts verschlüsselt werden.

8. **Host schaltet auf VM01 ein.**

## <a name="guarded-fabric-and-shielded-vm-glossary"></a>Glossar zu geschütztem Fabric und abgeschirmten VMs

| Begriff              | Definition           |
|----------|------------|
| Host-Überwachungsdienst (Host Guardian Service, HGS) | Eine Windows Server-Rolle, die auf einem gesicherten Cluster von Bare-Metal-Servern installiert ist, die die Integrität eines Hyper-V-Hosts messen und Schlüssel für fehlerfreie Hyper-V-Hosts freigeben können, wenn sie abgeschirmte VMs einschalten bzw. mit ihnen eine Livemigration durchführen. Diese zwei Funktionen sind ein wesentlicher Bestandteil einer Lösung mit einer abgeschirmten VM und werden als **Nachweisdienst** und **Schlüsselschutzdienst** bezeichnet. |
| geschützter Host | Ein Hyper-V-Host, auf dem abgeschirmte VMs ausgeführt werden können. Ein Host kann nur als _geschützt_ betrachtet werden, wenn er vom HGS-Nachweis Dienst als fehlerfrei eingestuft wurde. Abgeschirmte VMs können nicht eingeschaltet oder live auf einen Hyper-V-Host migriert werden, für den noch kein Nachweis geführt werden konnte, bzw. der den Nachweis nicht erbringen konnte. |
| geschütztes Fabric    | Dies ist der Sammelbegriff zur Beschreibung eines Fabrics mit Hyper-V-Hosts und deren Host-Überwachungsdienst, der die Fähigkeit zum Verwalten und Ausführen abgeschirmter VMs hat. |
| abgeschirmter virtueller Computer (VM) | Ein virtueller Computer, der nur auf geschützten Hosts ausgeführt werden kann und vor Untersuchung, Manipulation und Diebstahl durch bösartige Fabricadministratoren und Hostmalware geschützt ist. |
| Fabricadministrator | Ein Public Cloud- oder Private Cloud-Administrator, der virtuelle Computer verwalten kann. Im Rahmen eines geschützten Fabrics hat ein Fabricadministrator keinen Zugriff auf abgeschirmte VMs oder die Richtlinien, die bestimmen, auf welchen Hosts abgeschirmte VMs ausgeführt werden können. |
| HGS-Administrator | Ein vertrauenswürdiger Administrator in der Public oder Private Cloud, der über die Berechtigung zum Verwalten der Richtlinien und des kryptografischen Materials für geschützte Hosts verfügt, d.h. Hosts, auf denen eine abgeschirmte VM ausgeführt werden kann.|
| Bereitstellungsdatendatei oder geschützte Datendatei (PDK-Datei) | Eine verschlüsselte Datei, die ein Mandant oder Benutzer erstellt, um wichtige Informationen der VM-Konfiguration zu speichern und vor dem Zugriff anderer Benutzern zu schützen. Eine geschützte Datendatei kann z.B. das Kennwort enthalten, das dem lokalen Administratorkonto zugewiesen wird, wenn die VM erstellt wird. |
| Virtualisierungsbasierte Sicherheit (VBS) | Eine Hyper-V-basierte Verarbeitungs-und Speicherumgebung, die vor Administratoren geschützt ist. Virtueller sicherer Modus gibt dem System die Möglichkeit zum Speichern von Betriebssystemschlüsseln, die für den Betriebssystemadministrator unsichtbar sind.|
| virtuelles TPM | Eine virtualisierte Version eines Trusted Platform Module (TPM). Ab Hyper-V in Windows Server 2016 können Sie ein virtuelles TPM 2,0-Gerät bereitstellen, damit virtuelle Computer verschlüsselt werden können, so wie ein physisches TPM die Verschlüsselung eines physischen Computers ermöglicht.|

## <a name="additional-references"></a>Weitere Verweise

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
- Blog: [Daten Center-und Private Cloud-Sicherheitsblog](/archive/blogs/datacentersecurity/)
- Video: [Einführung in abgeschirmte Virtual Machines](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- Video: [Einblicke in abgeschirmte VMS mit Windows Server 2016 Hyper-V](https://channel9.msdn.com/events/Ignite/2016/BRK3124)