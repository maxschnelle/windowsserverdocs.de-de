---
title: Geschütztes Fabric und abgeschirmte VM Planungshandbuch für Hoster
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 392af37f-a02d-4d40-a25d-384211cbbfdd
manager: dongill
author: nirb-ms
ms.technology: security-guarded-fabric
ms.openlocfilehash: 0a43cedf8ce0138e89624ff3df5bc7088f583252
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875301"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-tenants"></a>Geschütztes Fabric und abgeschirmte VM Planungshandbuch für Mandanten

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema konzentriert sich auf VM-Besitzer, die ihre virtuellen Maschinen (VMs), für die Konformitäts- und Sicherheitszwecken schützen möchten. Unabhängig davon, ob die virtuellen Computer auf einem Hostinganbieter geschütztes Fabric oder einem privaten, geschützten Fabric ausgeführt müssen VM-Besitzer die Sicherheitsstufe der geschützten virtuelle Maschinen, zu steuern, die enthält gleichzeitig die Möglichkeit, um sie bei Bedarf zu entschlüsseln.

Es gibt drei Bereiche zu berücksichtigen, wenn mithilfe von abgeschirmten VMs:

- Die Sicherheitsstufe für die virtuellen Computer
- Die kryptografischen Schlüssel verwendet, um sie zu schützen
- Geschützte Daten: vertraulicher Informationen, die zum Erstellen abgeschirmter VMs 

## <a name="security-level-for-the-vms"></a>Sicherheitsstufe für die virtuellen Computer

Bei der Bereitstellung abgeschirmter VMs muss eine der zwei Sicherheitsstufen ausgewählt werden:

- Geschützte 
- Verschlüsselung wird unterstützt

Sowohl abgeschirmte und Verschlüsselung unterstützte VMs haben ein virtuelles TPM angefügt, die sie auch, dass die Ausführung von Windows durch BitLocker geschützt sind. Der Hauptunterschied besteht darin, dass, die abgeschirmte VMs Blockieren des Zugriffs von Fabric-Administratoren, während Verschlüsselung unterstützte VMs Fabric-Administratoren die gleiche Zugriffsebene zulassen wie auf einen normalen virtuellen Computer. Weitere Informationen zu diesen Unterschieden finden Sie unter [überwachten Fabric und abgeschirmte VMs Overview](guarded-fabric-and-shielded-vms.md). 

Wählen Sie **abgeschirmte VMs** , wenn Sie den virtuellen Computer vor einem gefährdeten Fabric (einschließlich Administratoren mit kompromittierte) schützen möchten. Sie sollten in Umgebungen verwendet werden, in dem Fabric-Administratoren und Fabric selbst nicht vertrauenswürdig sind. Wählen Sie **Verschlüsselung unterstützte VMs** Wenn Sie möchten einen Balken Compliance zu erfüllen, die sowohl die Verschlüsselung als auch die Verschlüsselung des virtuellen Computers über das Netzwerk (z. B. bei der Livemigration) erfordern.

Verschlüsselung unterstützte VMs eignen sich ideal in Umgebungen, in denen fabricadministratoren voll vertrauenswürdig sind jedoch die Verschlüsselung ist weiterhin eine Anforderung.

Sie können eine Mischung von reguläre VMs, abgeschirmte VMs und Verschlüsselung unterstützte VMs auf ein geschütztes Fabric und sogar auf demselben Hyper-V-Host ausführen. 

Gibt an, ob abgeschirmte oder Verschlüsselung unterstützte ein virtuellen Computers wird durch die geschützten Daten bestimmt, die beim Erstellen des virtuellen Computers ausgewählt ist. VM-Besitzer konfigurieren Sie die Sicherheitsstufe, beim Erstellen der geschützten Daten (finden Sie unter den [Schutzdaten](#shielding-data) Abschnitt).
Beachten Sie, sobald diese Entscheidung getroffen wurde, es nicht geändert werden kann während der virtuelle Computer in das virtualisierungsfabric bleibt.

## <a name="cryptographic-keys-used-for-shielded-vms"></a>Kryptografischer Schlüssel für abgeschirmte VMs

Abgeschirmte VMs sind von der Virtualisierung-Fabric-Angriffsvektoren, die mit verschlüsselten Festplatten und verschiedene andere verschlüsselte Elemente geschützt, die nur von entschlüsselt werden können:

- Ein Besitzer-Schlüssel – ist dies ein kryptografischer Schlüssel verwaltet durch den VM-Besitzer, die in der Regel für die letzten-Mittel-Wiederherstellung oder zur Problembehandlung verwendet wird. VM-Besitzer sind verantwortlich für die Verwaltung der Besitzer der Schlüssel an einem sicheren Ort.
- Eine oder mehrere Überwachungen (Host-Überwachungsdienst-Schlüssel) – stellt jeder Überwachungsdienst eine Virtualisierungs-Fabric, das auf der abgeschirmte VMs zum Ausführen von Besitzer autorisiert. Unternehmen häufig ein primäres und ein Disaster Recovery (Notfallwiederherstellung) Virtualisierungs-Fabric und würde in der Regel die abgeschirmte VMs zum Ausführen auf beide autorisieren. In einigen Fällen kann das sekundäre (DR)-Fabric von einem Anbieter öffentlicher Clouds gehostet werden. Der private Schlüssel für alle geschützten Fabrics werden nur für den Virtualisierungs-Fabric verwaltet werden, während der öffentliche Schlüssel heruntergeladen werden können und in der Überwachungsdienst enthalten sind. 

**Wie erstelle ich einen Besitzer-Schlüssel?** Ein Besitzer-Schlüssel wird durch zwei Zertifikate dargestellt. Ein Zertifikat für die Verschlüsselung und ein Zertifikat zum Signieren. Sie können dieser beiden Zertifikate, die mit Ihrer eigenen PKI-Infrastruktur zu erstellen oder Abrufen von SSL-Zertifikate von einer öffentlichen Zertifizierungsstelle (CA). Zu Testzwecken können Sie auch ein selbstsigniertes Zertifikat auf jedem Computer ab Windows 10 oder Windows Server 2016 erstellen.

**Wie viele Besitzer-Schlüssel benötigen Sie?** Sie können einen einzigen Besitzer-Schlüssel oder mehrere Besitzer-Schlüssel verwenden. Bewährte Methoden empfehlen einen einzigen Besitzer-Schlüssel für eine Gruppe von virtuellen Computern, die die gleiche Sicherheit verwenden, vertrauen und Risiken auf, und klicken Sie für die administrative Kontrolle. Können Sie einen einzigen Besitzer-Schlüssel für alle Ihre Domäne abgeschirmte VMs Teilen und hinterlegen, Besitzer-Schlüssel für die Verwaltung durch die Domänenadministratoren.

**Kann ich meine eigenen Schlüssel für den Host-Überwachungsdienst verwenden?** Ja, können Sie "Bringen Sie Ihren eigenen"-Taste, um die hosting-Anbieter und verwenden, die Schlüssel für die abgeschirmten VMs. Dies ermöglicht es Ihnen, Ihre spezifischen Schlüssel (im Vergleich zu mithilfe des hosting-Anbieter-Schlüssels) verwenden und kann verwendet werden, wenn Sie eine bestimmte Sicherheitsgruppe oder Bestimmungen, denen Sie einhalten müssen. Für wichtige Hygiene verwendet die Host-Überwachungsdienst-Schlüssel als der Owner-Schlüssel unterscheiden.

## <a name="shielding-data"></a>Geschützte Daten

Geschützte Daten enthält die geheimen Schlüssel zum Bereitstellen von abgeschirmten oder Verschlüsselung unterstützte VMs erforderlich sind. Es wird auch verwendet, bei der Konvertierung reguläre VMs in abgeschirmte VMs.

Geschützte Daten wird mit dem Assistenten für geschützte Datendateien erstellt und in das Hochladen von VM-Besitzer in geschützten Fabrics PDK-Dateien gespeichert.

Abgeschirmte VMs schützen vor Angriffen von einem gefährdeten Virtualisierungs-Fabric, weshalb wir einen sicheren Mechanismus zum vertrauliche Initialisierungsdaten, z. B. das Kennwort des Administrators, die Anmeldeinformationen für den Domänenbeitritt oder RDP-Zertifikate zu übergeben, ohne diese offenzulegen der Virtualisierungs-Fabric selbst oder auf die Administratoren. Darüber hinaus enthält die geschützten Daten Folgendes:

1. Sicherheit auf Ebene – abgeschirmt oder Verschlüsselung unterstützt
2. Besitzer und die Liste der vertrauenswürdigen Hosts Guardians, in dem der virtuelle Computer ausgeführt werden kann
3. VM-Initialisierung der Daten ("Unattend.xml", RDP-Zertifikat)
4. Liste der vertrauenswürdigen signierte vorlagendatenträger für die Erstellung des virtuellen Computers in der Virtualisierungsumgebung 

Beim Erstellen einer VM abgeschirmten "oder" Verschlüsselung unterstützt, oder Konvertieren einer vorhandenen VM, aufgefordert werden zur Auswahl der geschützten Daten anstatt für die vertraulichen Informationen aufgefordert zu werden.

**Wie viele schutzdatendateien benötige ich?** Eine einzelne geschützte Datendatei kann verwendet werden, um alle geschützten virtuellen Computer zu erstellen. Wenn Sie eine abgeschirmte VM erfordert jedoch, dass eines der vier Elemente unterscheiden, ist eine zusätzliche geschützte Datendatei erforderlich. Beispielsweise müssen Sie eine schutzdatendatei für Ihre IT-Abteilung und eine andere schutzdatendatei für die Personalabteilung evtl., da ihre anfängliche Administratorkennwort und die RDP-Zertifikate Compilerversionen.

Verwenden separate geschützte Datendateien für die einzelnen virtuellen Computer geschützt ist, zwar möglich ist nicht unbedingt die optimale Wahl und sollte aus den richtigen Gründen vorgenommen werden. Wenn alle abgeschirmte VM in ein anderes Administratorkonto-Kennwort muss, betrachten Sie z. B. stattdessen mit einer Kennwort-Management-Dienst oder Abfragetool, z. B. [Microsofts lokalen Administrator Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899).

## <a name="creating-a-shielded-vm-on-a-virtualization-fabric"></a>Erstellen einer abgeschirmten VMs in einem virtualisierungsfabric

Es gibt mehrere Optionen zum Erstellen einer abgeschirmten VMs in einem virtualisierungsfabric (Folgendes gilt für sowohl abgeschirmte als auch Verschlüsselung unterstützte VMs):

1. Erstellen Sie eine geschützte VM in Ihrer Umgebung, und klicken Sie in der Virtualisierungs-Fabric hochladen
2. Erstellen Sie eine neue geschützte VM anhand einer signierten Vorlage in das virtualisierungsfabric
3. Schützen Sie einen vorhandenen virtuellen Computer (der vorhandene virtuellen Computer muss die Generation 2 sein und muss WindowsServer 2012 oder höher ausgeführt werden)

Erstellen neue VMs aus einer Vorlage ist üblich ist. Da es sich bei der vorlagendatenträger, der verwendet wird, um neue abgeschirmte VM erstellen, in das virtualisierungsfabric befindet, sind jedoch zusätzliche Maßnahmen erforderlich, um sicherzustellen, dass es nicht von einem Administrator bösartige fabricadministratoren oder durch Malware auf dem Fabric manipuliert wurde. Dieses Problem gelöst ist, verwenden die signierte vorlagendatenträger: signierte vorlagendatenträger und deren Datenträgersignaturen von vertrauenswürdige Administratoren oder Besitzer der VM erstellt werden. Wenn eine abgeschirmte VM erstellt wird, wird den vorlagendatenträger-Signatur mit den Signaturen, die die angegebene schutzdatendatei enthaltenen verglichen. Wenn eine der Signaturen für die geschützte Datendatei den vorlagendatenträger-Signatur übereinstimmt, wird der Bereitstellungsprozess fortgesetzt. Wenn keine Übereinstimmung gefunden werden kann, der Bereitstellungsprozess abgebrochen wird sichergestellt, dass vertrauliche Informationen nicht aufgrund einer nicht vertrauenswürdigen vorlagendatenträger gestohlen werden.

Verwenden signierte vorlagendatenträger zum Erstellen abgeschirmter VMs stehen zwei Optionen zur Verfügung:

1. Verwenden Sie einen vorhandenen signierten vorlagendatenträger, die von Ihrem virtualisierungsanbieter bereitgestellt wird. In diesem Fall verwaltet der virtualisierungsanbieter signierten vorlagedatenträgern.
2. Laden Sie einen signierten vorlagendatenträger, auf die Virtualisierungs-Fabric. Der VM-Besitzer ist verantwortlich für die Verwaltung von signierten vorlagedatenträgern. 


