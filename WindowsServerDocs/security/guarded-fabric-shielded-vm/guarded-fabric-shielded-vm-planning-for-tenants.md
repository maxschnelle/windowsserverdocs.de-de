---
title: Planungs Handbuch für geschütztes Fabric und abgeschirmte VMs für Hoster
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 392af37f-a02d-4d40-a25d-384211cbbfdd
manager: dongill
author: nirb-ms
ms.technology: security-guarded-fabric
ms.openlocfilehash: d361dfee0cbb06c4b7908b80145c09327dac3956
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870428"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-tenants"></a>Planungs Handbuch für geschütztes Fabric und abgeschirmte VMs für Mandanten

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema konzentriert sich auf VM-Besitzer, die Ihre virtuellen Computer (Virtual Machines, VMS) zu Kompatibilitäts-und Sicherheitszwecken schützen möchten. Unabhängig davon, ob die virtuellen Computer auf dem geschützten Fabric eines hostinganbieters oder einem privaten geschützten Fabric ausgeführt werden, müssen die VM-Besitzer die Sicherheitsstufe ihrer abgeschirmten VMS steuern. dazu gehört auch die Beibehaltung der Möglichkeit, Sie bei Bedarf zu entschlüsseln.

Bei der Verwendung von abgeschirmten VMS sind drei Bereiche zu beachten:

- Die Sicherheitsstufe für die VMs
- Die kryptografischen Schlüssel, mit denen Sie geschützt werden.
- Schutz Daten – vertrauliche Informationen, die zum Erstellen von abgeschirmten VMS verwendet werden 

## <a name="security-level-for-the-vms"></a>Sicherheitsstufe für die VMs

Beim Bereitstellen von abgeschirmten VMS muss eine von zwei Sicherheitsstufen ausgewählt werden:

- Abgesch 
- Verschlüsselung unterstützt

Sowohl abgeschirmte als auch durch Verschlüsselung unterstützte VMS sind einem virtuellen TPM angefügt, und diejenigen, die Windows ausführen, werden durch BitLocker geschützt. Der Hauptunterschied besteht darin, dass abgeschirmte VMS den Zugriff durch Fabric-Administratoren blockieren, während von Verschlüsselungs gestützten VMS Fabric-Administratoren die gleiche Zugriffsebene wie bei einer regulären VM gestattet wird. Weitere Informationen zu diesen Unterschieden finden Sie unter [Übersicht über geschützte Fabric und abgeschirmte VMS](guarded-fabric-and-shielded-vms.md). 

Wählen Sie **abgeschirmte VMS** aus, wenn Sie den virtuellen Computer vor einem kompromittierten Fabric schützen möchten (einschließlich kompromittierter Administratoren). Sie sollten in Umgebungen verwendet werden, in denen Fabric-Administratoren und das Fabric selbst nicht vertrauenswürdig sind. Wählen Sie **Verschlüsselung unterstützte VMS** aus, wenn Sie eine Kompatibilitäts Leiste erreichen möchten, die ggf. Verschlüsselung ruhender Daten und Verschlüsselung des virtuellen Computers (z. b. während der Live Migration) erfordert.

Durch Verschlüsselung unterstützte VMS sind ideal in Umgebungen, in denen Fabric-Administratoren voll vertrauenswürdig sind, die Verschlüsselung jedoch weiterhin erforderlich ist.

Sie können eine Mischung aus regulären VMS, abgeschirmten VMS und von der Verschlüsselung unterstützten VMs in einem geschützten Fabric und sogar auf demselben Hyper-V-Host ausführen. 

Ob ein virtueller Computer abgeschirmt oder die Verschlüsselung unterstützt wird, hängt von den geschützten Daten ab, die beim Erstellen des virtuellen Computers ausgewählt werden. VM-Besitzer konfigurieren die Sicherheitsstufe beim Erstellen der geschützten Daten (siehe Abschnitt "Schutz [Daten](#shielding-data) ").
Beachten Sie, dass diese Option nicht geändert werden kann, wenn die VM im virtualisierungsfabric verbleibt.

## <a name="cryptographic-keys-used-for-shielded-vms"></a>Für abgeschirmte VMS verwendete kryptografische Schlüssel

Abgeschirmte VMS sind vor virtualisierungsfabric-Angriffsvektoren mithilfe verschlüsselter Datenträger und verschiedener anderer verschlüsselter Elemente geschützt, die nur entschlüsselt werden können:

- Einen Besitzer Schlüssel – Dies ist ein kryptografischer Schlüssel, der vom VM-Besitzer verwaltet wird und in der Regel für die letzte Wiederherstellung oder Problembehandlung verwendet wird. VM-Besitzer sind verantwortlich für die Verwaltung von Besitzer Schlüsseln an einem sicheren Ort.
- Mindestens ein Wächter (Host-Überwachungs Schlüssel) – jeder Wächter stellt ein virtualisierungsfabric dar, in dem ein Besitzer abgeschirmte VMs für die Durchführung autorisiert. Unternehmen verfügen häufig über ein primäres und Notfall Wiederherstellungs Fabric (Disaster Recovery, Dr) und autorisieren Ihre abgeschirmten VMs in der Regel auf beiden Computern. In einigen Fällen kann das sekundäre Fabric (Dr) von einem Public Cloud-Anbieter gehostet werden. Die privaten Schlüssel für ein beliebiges geschütztes Fabric werden nur im virtualisierungsfabric verwaltet, während ihre öffentlichen Schlüssel heruntergeladen werden können und in Ihrem Wächter enthalten sind. 

**Gewusst wie einen Besitzer Schlüssel erstellen?** Ein Besitzer Schlüssel wird durch zwei Zertifikate repräsentiert. Ein Zertifikat für die Verschlüsselung und ein Zertifikat für die Signierung. Sie können diese beiden Zertifikate mithilfe ihrer eigenen PKI-Infrastruktur erstellen oder SSL-Zertifikate von einer öffentlichen Zertifizierungsstelle (ca) abrufen. Zu Testzwecken können Sie auch ein selbst signiertes Zertifikat auf allen Computern erstellen, die mit Windows 10 oder Windows Server 2016 beginnen.

**Wie viele Besitzer Schlüssel sollten Sie haben?** Sie können einen einzelnen Besitzer Schlüssel oder mehrere Besitzer Schlüssel verwenden. Bewährte Methoden empfehlen einen einzelnen Besitzer Schlüssel für eine Gruppe von virtuellen Computern, die die gleiche Sicherheit, Vertrauensstufe und Risikostufe und für administrative Kontrolle haben. Sie können einen einzelnen Besitzer Schlüssel für alle in die Domäne eingebundenen abgeschirmten VMS freigeben und diesen Besitzer Schlüssel zur Verwaltung durch die Domänen Administratoren hinterlegen.

**Kann ich meine eigenen Schlüssel für den Host-Wächter verwenden?** Ja, Sie können Ihren eigenen Schlüssel in den Hostinganbieter einbringen und diesen Schlüssel für Ihre abgeschirmten VMS verwenden. Dies ermöglicht Ihnen die Verwendung ihrer speziellen Schlüssel (im Gegensatz zum Verwenden des Hostinganbietern) und kann verwendet werden, wenn Sie über bestimmte Sicherheits-oder Sicherheitsbestimmungen verfügen, die Sie einhalten müssen. Aus Gründen der Schlüssel Pflege sollten sich die Host-Überwachungs Schlüssel vom Besitzer Schlüssel unterscheiden.

## <a name="shielding-data"></a>Geschützte Daten

Geschützte Daten enthalten die geheimen Schlüssel, die für die Bereitstellung von abgeschirmten oder Verschlüsselungs gestützten VMS erforderlich sind. Sie wird auch verwendet, wenn reguläre VMs in abgeschirmte VMS umgerechnet werden.

Geschützte Daten werden mithilfe des Assistenten zum Schützen von Datendateien erstellt und in PDK-Dateien gespeichert, die von VM-Besitzern in das geschützte Fabric hochgeladen werden.

Abgeschirmte VMS tragen zum Schutz vor Angriffen von einem kompromittierten virtualisierungsfabric bei. Daher benötigen wir einen sicheren Mechanismus, um sensible Initialisierungs Daten zu übergeben, z. b. das Administrator Kennwort, Anmelde Informationen für den Domänen Beitritt oder RDP-Zertifikate, ohne diese zu verdeutlichen Das virtualisierungsfabric selbst oder seine Administratoren. Außerdem enthalten die geschützten Daten Folgendes:

1. Sicherheitsstufe – abgeschirmt oder Verschlüsselung unterstützt
2. Besitzer und Liste der vertrauenswürdigen hostwächter, auf denen die VM ausgeführt werden kann
3. Initialisierungs Daten für virtuelle Computer ("Unattend. xml", RDP-Zertifikat)
4. Liste der vertrauenswürdigen signierten Vorlagen Datenträger zum Erstellen der VM in der Virtualisierungsumgebung 

Wenn Sie einen geschützten oder Verschlüsselungs gestützten virtuellen Computer erstellen oder einen vorhandenen virtuellen Computer umrechnen, werden Sie aufgefordert, die geschützten Daten auszuwählen, anstatt zur Angabe der sensiblen Informationen aufgefordert zu werden.

**Wie viele geschützte Datendateien benötige ich?** Sie können eine einzelne geschützte Datendatei zum Erstellen jeder abgeschirmten VM verwenden. Wenn eine bestimmte abgeschirmte VM jedoch erfordert, dass eines der vier Elemente anders ist, ist eine zusätzliche Schutz Datendatei erforderlich. Angenommen, Sie verfügen über eine Schutz Datendatei für Ihre IT-Abteilung und eine andere Schutz Datendatei für die Personalabteilung, da Ihr anfängliches Administrator Kennwort und RDP-Zertifikate voneinander abweichen.

Die Verwendung separater Schutz Datendateien für jede abgeschirmte VM ist zwar möglich, ist aber nicht unbedingt die optimale Wahl und sollte aus den richtigen Gründen erfolgen. Wenn z. b. jeder geschützte virtuelle Computer über ein anderes Administrator Kennwort verfügen muss, sollten Sie stattdessen einen Kenn Wort Verwaltungsdienst oder ein Tool wie [die lokale Administrator Kennwort-Lösung (Runden) von Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=46899)verwenden.

## <a name="creating-a-shielded-vm-on-a-virtualization-fabric"></a>Erstellen einer abgeschirmten VM in einem virtualisierungsfabric

Es gibt mehrere Optionen zum Erstellen einer abgeschirmten VM in einem virtualisierungsfabric (Folgendes ist für abgeschirmte und durch Verschlüsselung unterstützte VMS relevant):

1. Erstellen einer abgeschirmten VM in Ihrer Umgebung und Hochladen der VM in das virtualisierungsfabric
2. Erstellen einer neuen abgeschirmten VM aus einer signierten Vorlage auf dem virtualisierungsfabric
3. Schützen eines vorhandenen virtuellen Computers (die vorhandene VM muss die Generation 2 sein und Windows Server 2012 oder höher ausführen)

Das Erstellen neuer virtueller Computer aus einer Vorlage ist üblich. Da sich der Vorlagen Datenträger, der zum Erstellen einer neuen abgeschirmten VM verwendet wird, auf dem virtualisierungsfabric befindet, sind jedoch zusätzliche Maßnahmen erforderlich, um sicherzustellen, dass er nicht von einem böswilligen Fabric-Administrator oder von Schadsoftware manipuliert wurde, die auf dem Fabric ausgeführt wird. Dieses Problem wird mithilfe von signierten Vorlagen Datenträgern gelöst – signierte Vorlagen Datenträger und deren Datenträger Signaturen werden von vertrauenswürdigen Administratoren oder dem Besitzer der Wenn eine abgeschirmte VM erstellt wird, wird die Signatur des Vorlagen Datenträgers mit den Signaturen in der angegebenen Schutz Datendatei verglichen. Wenn eine der Signaturen der Schutz Datendatei mit der Signatur des Vorlagen Datenträgers identisch ist, wird der Bereitstellungs Prozess fortgesetzt. Wenn keine Entsprechung gefunden werden kann, wird der Bereitstellungs Prozess abgebrochen, um sicherzustellen, dass die VM-Geheimnisse aufgrund eines nicht vertrauenswürdigen Vorlagen Datenträgers nicht beeinträchtigt werden

Wenn Sie signierte Vorlagen Datenträger verwenden, um geschützte VMS zu erstellen, sind zwei Optionen verfügbar:

1. Verwenden Sie einen vorhandenen signierten Vorlagen Datenträger, der vom Virtualisierungsanbieter bereitgestellt wird. In diesem Fall verwaltet der Virtualisierungsanbieter signierte Vorlagen Datenträger.
2. Hochladen eines signierten Vorlagen Datenträgers in das virtualisierungsfabric. Der Besitzer der VM ist für die Verwaltung signierter Vorlagen Datenträger verantwortlich 


