---
title: 'Abgeschirmte VMs für Mandanten: Erstellen eines Vorlagen Datenträgers (optional)'
ms.prod: windows-server
ms.topic: article
ms.assetid: c1992f8b-6f88-4dbc-b4a5-08368bba2787
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 1f51a0f90f60847929f6fe46732c98f355a6a859
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856443"
---
# <a name="shielded-vms-for-tenants---creating-a-template-disk-optional"></a>Abgeschirmte VMs für Mandanten: Erstellen eines Vorlagen Datenträgers (optional)

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Zum Erstellen einer neuen abgeschirmten VM müssen Sie einen speziell vorbereiteten, signierten Vorlagen Datenträger verwenden. Mithilfe von Metadaten von signierten Vorlagen Datenträgern können Sie sicherstellen, dass die Datenträger nicht geändert werden, nachdem Sie erstellt wurden, und Sie können als Mandant festlegen, welche Datenträger zum Erstellen Ihrer abgeschirmten VMS verwendet werden können. Eine Möglichkeit, diesen Datenträger bereitzustellen, besteht darin, den Mandanten zu erstellen, wie in diesem Thema beschrieben. 

> [!IMPORTANT]
> Wenn Sie möchten, können Sie stattdessen einen vom hostingdienstanbieter bereitgestellten Vorlagen Datenträger verwenden. Wenn Sie dies tun, ist es wichtig, einen virtuellen Testcomputer mit diesem Vorlagen Datenträger bereitzustellen und ihre eigenen Tools (Antivirus, Sicherheitsrisiko Scanner usw.) auszuführen, um zu überprüfen, ob der Datenträger tatsächlich in einem vertrauenswürdigen Zustand ist.

## <a name="prepare-an-operating-system-vhdx"></a>Vorbereiten einer vhdx-Betriebssystem Datei

Um einen geschützten Vorlagen Datenträger zu erstellen, müssen Sie zunächst einen Betriebssystem Datenträger vorbereiten, der über den Vorlagen-Assistenten für Datenträger ausgeführt wird. Dieser Datenträger wird als Betriebssystem Datenträger auf abgeschirmten VMS verwendet. Zum Erstellen dieses Datenträgers können Sie beliebige vorhandene Tools verwenden, z. b. Microsoft Desktop Image Service Manager (Mage), oder Sie können manuell einen virtuellen Computer mit einer leeren vhdx einrichten und das Betriebssystem auf diesem Datenträger installieren. Beim Einrichten des Datenträgers müssen die folgenden Anforderungen erfüllt werden, die für die Generation 2 und/oder abgeschirmte VMS spezifisch sind: 

| Anforderung für vhdx | Grund |
|-----------|----|
|Muss ein GPT-Datenträger (GUID-Partitionstabelle) sein. | Erforderlich für virtuelle Computer der Generation 2 zur Unterstützung von UEFI|
|Der Datenträgertyp muss Standard und nicht **dynamisch** **sein.** <br>Hinweis: Dies bezieht sich auf den Typ des logischen Datenträgers, nicht auf das von Hyper-V unterstützte "dynamisch erweiterbare" vhdx-Feature. | BitLocker unterstützt keine dynamischen Datenträger.|
|Der Datenträger verfügt über mindestens zwei Partitionen. Eine Partition muss das Laufwerk enthalten, auf dem Windows installiert ist. Dies ist das Laufwerk, das von BitLocker verschlüsselt wird. Die andere Partition ist die aktive Partition, die den Bootloader enthält und unverschlüsselt bleibt, damit der Computer gestartet werden kann.|Für BitLocker erforderlich|
|Dateisystem ist NTFS | Für BitLocker erforderlich|
|Das auf der vhdx installierte Betriebssystem ist einer der folgenden:<br>-Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 <br>-Windows 10, Windows 8.1, Windows 8| Erforderlich zur Unterstützung virtueller Maschinen der Generation 2 und der Microsoft-Vorlage für den sicheren Start|
|Das Betriebssystem muss generalisiert sein (führen Sie "syspree. exe" aus). | Die Vorlagen Bereitstellung umfasst spezialisierte VMs für die Arbeitsauslastung eines bestimmten Mandanten.| 

> [!NOTE]
> Kopieren Sie den Vorlagen Datenträger in dieser Phase nicht in die VMM-Bibliothek. 

### <a name="required-packages-to-create-a-nano-server-template-disk"></a>Erforderliche Pakete zum Erstellen eines Nano Server-Vorlagen Datenträgers

Wenn Sie beabsichtigen, Nano Server als Gast Betriebssystem auf abgeschirmten VMS auszuführen, müssen Sie sicherstellen, dass Ihr Nano Server-Image die folgenden Pakete enthält:

- Microsoft-NanoServer-Guest-Package
- Microsoft-NanoServer-SecureStartup-Package

## <a name="run-windows-update-on-the-template-operating-system"></a>Ausführen von Windows Update auf dem Vorlagen Betriebssystem

Vergewissern Sie sich auf dem Vorlagen Datenträger, dass alle aktuellen Windows-Updates auf dem Betriebssystem installiert sind. Kürzlich veröffentlichte Updates verbessern die Zuverlässigkeit des End-to-End-Schutz Vorgangs. Dies ist ein Prozess, der möglicherweise nicht abgeschlossen wird, wenn das Vorlagen Betriebssystem nicht auf dem neuesten Stand ist.

## <a name="sign-and-protect-the-vhdx-with-the-template-disk-wizard"></a>Signieren und schützen der vhdx mit dem Vorlagen Datenträger-Assistenten

Um einen Vorlagen Datenträger mit abgeschirmten VMS zu verwenden, muss der Datenträger signiert und mit BitLocker verschlüsselt werden. Zu diesem Zweck verwenden Sie den Assistenten zum Erstellen einer abgeschirmten Vorlage. Dieser Assistent generiert einen Hash für den Datenträger und fügt ihn einem volumesignaturkatalog (VSC) hinzu. Der VSC wird mit einem von Ihnen angegebenen Zertifikat signiert und während des Bereitstellungs Prozesses verwendet, um sicherzustellen, dass der Datenträger, der für einen Mandanten bereitgestellt wird, nicht geändert oder durch einen Datenträger ersetzt wurde, dem der Mandant nicht vertraut. Schließlich wird BitLocker auf dem Betriebssystem des Datenträgers installiert (sofern es noch nicht vorhanden ist), um den Datenträger für die Verschlüsselung während der VM-Bereitstellung vorzubereiten.

> [!NOTE]
> Der Vorlagen Datenträger-Assistent ändert den Vorlagen Datenträger, den Sie direkt angeben. Sie sollten eine Kopie der ungeschützten vhdx-Datei erstellen, bevor Sie den Assistenten ausführen, um die Datenträger zu einem späteren Zeitpunkt zu aktualisieren. Sie können einen Datenträger, der mit dem Vorlagen Datenträger-Assistenten geschützt wurde, nicht ändern.

Führen Sie die folgenden Schritte auf einem Computer aus, auf dem Windows Server 2016 ausgeführt wird (es muss sich nicht um einen überwachten Host oder VMM-Server handeln):

1. Kopieren Sie die in [Vorbereiten einer Betriebssystem-vhdx](#prepare-an-operating-system-vhdx) erstellte generalisierte vhdx auf den Server, sofern diese nicht bereits vorhanden ist.

2. Installieren Sie das Feature der **abgeschirmten VM-Tools** aus **Remoteserver-Verwaltungstools** auf dem Computer.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart

3. Abrufen oder Erstellen eines Zertifikats zum Signieren der vhdx-Datei, die als Vorlagen Datenträger für neue abgeschirmte VMS verwendet wird. Details zu diesem Zertifikat werden in eine geschützte Datendatei eingebunden, die den Datenträger als vertrauenswürdigen Datenträger autorisiert. Daher ist es wichtig, dass Sie dieses Zertifikat von einer Zertifizierungsstelle abrufen, der Sie und Ihrem hostingdienstanbieter Vertrauen. In Unternehmens Szenarios, in denen Sie sowohl der Host als auch der Mandant sind, sollten Sie das Zertifikat aus Ihrer PKI ausgeben.

    Wenn Sie eine Testumgebung einrichten und nur ein selbst signiertes Zertifikat verwenden möchten, um den Vorlagen Datenträger zu signieren, führen Sie einen Befehl aus, der dem folgenden auf dem Computer ähnelt:

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. Starten Sie den Vorlagen Datenträger- **Assistenten** im Ordner " **Verwaltung** " im Startmenü, oder geben Sie " **templatediskwizard. exe** " an einer Eingabeaufforderung ein.

5. Klicken Sie auf der Seite **Zertifikat** auf **Durchsuchen** , um eine Liste mit Zertifikaten anzuzeigen. Wählen Sie das Zertifikat aus, mit dem die Datenträger Vorlage signiert werden soll. Klicken Sie auf **OK** und dann auf **Weiter**.

6. Klicken Sie auf der Seite virtueller Datenträger auf **Durchsuchen** , um das vhdx auszuwählen, das Sie vorbereitet haben, und klicken Sie dann auf **weiter**.

7. Geben Sie auf der Seite Signatur Katalog einen anzeigen **Amen** und eine **Version** des Datenträgers an. Diese Felder sind vorhanden, damit Sie den Datenträger nach der Signierung identifizieren können.

    Beispielsweise können Sie **disk name** für den Datenträger Namen _WS2016_ und für **Version**, _1.0.0.0_ eingeben.

8. Überprüfen Sie Ihre Auswahl auf der Seite Einstellungen überprüfen des Assistenten. Wenn Sie auf **generieren**klicken, aktiviert der Assistent BitLocker auf dem Vorlagen Datenträger, berechnet den Hash des Datenträgers und erstellt den volumensignaturkatalog, der in den vhdx-Metadaten gespeichert ist.

    Warten Sie, bis der Signatur Vorgang abgeschlossen ist, bevor Sie versuchen, den Vorlagen Datenträger zu starten Der Vorgang kann je nach Größe des Datenträgers einige Zeit in Anspruch nehmen. 

9. Auf der Seite **Zusammenfassung** werden Informationen zur Datenträger Vorlage, zum Zertifikat, das zum Signieren der Vorlage verwendet wird, und zum Aussteller des Zertifikats angezeigt. Klicken Sie auf **Schließen**, um den Assistenten zu beenden.


Geben Sie dem hostingdienstanbieter die Vorlage für abgeschirmte Datenträger sowie eine geschützte Datendatei an, die Sie erstellen, wie unter [Erstellen von Schutz Daten zum Definieren einer abgeschirmten VM](guarded-fabric-tenant-creates-shielding-data.md)beschrieben.

## <a name="see-also"></a>Siehe auch

- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
