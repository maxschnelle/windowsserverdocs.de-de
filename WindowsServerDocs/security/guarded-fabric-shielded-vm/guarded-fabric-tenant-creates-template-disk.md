---
title: Abgeschirmte virtuelle Computer für Mandanten – erstellen einen vorlagendatenträger – optional
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: c1992f8b-6f88-4dbc-b4a5-08368bba2787
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2709c84a16dadc2211af4a6f5b43c13266ede155
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874631"
---
# <a name="shielded-vms-for-tenants---creating-a-template-disk-optional"></a>Abgeschirmte virtuelle Computer für Mandanten – erstellen einen vorlagendatenträger (optional)

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um eine neue geschützte VM zu erstellen, müssen Sie einen speziell vorbereitete, signierte vorlagendatenträger zu verwenden. Metadaten über signierte vorlagendatenträgern wird sichergestellt, dass die Datenträger nicht geändert werden, nachdem sie erstellt wurden, und es Ihnen, wie ein Mandant zum Einschränken von welchen Datenträgern verwendet werden kann, um die abgeschirmten VMs zu erstellen. Eine Möglichkeit zum Bereitstellen dieser Datenträger ist für Sie, den Mandanten, er erstellt, wie in diesem Thema beschrieben. 

> [!IMPORTANT]
> Falls gewünscht, können Sie stattdessen einen vorlagendatenträger, die von Ihrem hosting-Anbieter bereitgestellt. Wenn Sie dies tun, ist es wichtig, einen Test bereitzustellen, die virtuellen Computer mithilfe dieser vorlagedatenträgers, und führen Ihren eigenen Tools (Antivirus, Überprüfung auf Sicherheitsrisiken und So weiter) auf den Datenträger zu überprüfen, in der Tat in einem Zustand befindet, denen Sie vertrauen.

## <a name="prepare-an-operating-system-vhdx"></a>Bereiten Sie ein VHDX-Betriebssystem vor.

Um eine abgeschirmte vorlagedatenträger zu erstellen, müssen Sie zuerst einen Betriebssystem-Datenträger vorbereiten, der über den vorlagendatenträger-Assistenten ausgeführt werden. Dieser Datenträger wird als Betriebssystem-Datenträger in abgeschirmte VMs verwendet werden. Sie können alle vorhandenen Tools verwenden, erstellen diesen Datenträger, z. B. Microsoft Desktop Image Service Manager (DISM) oder manuell Einrichten eines virtuellen Computers mit einem leeren VHDX und installieren Sie das Betriebssystem auf diesem Datenträger. Bei der Einrichtung des Datenträgers müssen sie die folgenden Anforderungen erfüllen, die auf Generation 2 gelten bzw. abgeschirmte VMs: 

| Anforderung für VHDX | Grund |
|-----------|----|
|Ein GUID-Partitionstabelle (GPT) Datenträger muss sein werden. | Erforderlich für virtuelle Maschinen der Generation 2 um UEFI zu unterstützen|
|Datenträgertyp muss **grundlegende** im Gegensatz zu **dynamische**. <br>Hinweis: Dies bezieht sich auf den Typ der logischer Datenträger, nicht die "dynamisch erweiterbar" VHDX-Feature von Hyper-V unterstützt. | BitLocker bietet keine Unterstützung für dynamische Datenträger.|
|Der Datenträger verfügt über mindestens zwei Partitionen. Eine Partition muss das Laufwerk enthalten, auf dem Windows installiert ist. Dies ist das Laufwerk, das BitLocker verschlüsselt wird. Die andere Partition ist die aktive Partition, die enthält den Bootloader und bleibt unverschlüsselt, sodass der Computer gestartet werden kann.|Erforderlich für BitLocker|
|Dateisystem ist NTFS | Erforderlich für BitLocker|
|Das Betriebssystem installiert wird, auf die VHDX ist eine der folgenden:<br>– Windows Server 2019, WindowsServer 2016, Windows Server 2012 R2 oder WindowsServer 2012 <br>- Windows 10, Windows 8.1, Windows 8| Erforderlich, um virtuelle Maschinen der Generation 2 und der sichere Start von Microsoft-Vorlage zu unterstützen|
|Betriebssystem muss generalisierten (Ausführung sysprep.exe) sein. | Für die Bereitstellung von Vorlage umfasst spezialisiert sich auf virtuelle Computer für einen bestimmten Mandanten arbeitsauslastung| 

> [!NOTE]
> Kopieren Sie den vorlagendatenträger nicht in der VMM-Bibliothek in dieser Phase. 

### <a name="required-packages-to-create-a-nano-server-template-disk"></a>Erforderlichen Pakete zum Erstellen eines vorlagedatenträgers Nano Server

Wenn Sie Nano Server als Ihr Gastbetriebssystem in abgeschirmte VMs ausführen möchten, müssen Sie sicherstellen, dass Ihre Nano Server-Image die folgenden Pakete enthält:

- Microsoft-NanoServer-Guest-Package
- Microsoft-NanoServer-SecureStartup-Package

## <a name="run-windows-update-on-the-template-operating-system"></a>Führen Sie Windows Update auf dem Betriebssystem der Vorlage

Auf dem vorlagendatenträger stellen Sie sicher, dass das Betriebssystem alle die aktuellsten Windows Updates installiert ist. Vor kurzem veröffentlichten Updates verbessern die Zuverlässigkeit des geschützten Prozesses End-to-End - ein Prozess, der auf abgeschlossen, wenn das Betriebssystem der Vorlage möglicherweise nicht auf dem neuesten Stand.

## <a name="sign-and-protect-the-vhdx-with-the-template-disk-wizard"></a>Signieren Sie und schützen Sie die VHDX mit den vorlagendatenträger-Assistenten

Um einen vorlagendatenträger mit abgeschirmten virtuellen Computern zu verwenden, muss der Datenträger registriert und mit BitLocker verschlüsselt werden. Zu diesem Zweck verwenden Sie den geschützten Vorlagendatenträger erstellen-Assistenten. Dieser Assistent generiert einen Hashwert für den Datenträger und ein Volume-signaturkatalogs (VSC) hinzugefügt. Dem VSC bzw. ist mit einem Zertifikat signiert Sie angeben, und werden während der Bereitstellung verwendet, um sicherzustellen, dass der Datenträger für einen Mandanten bereitgestellt wird nicht geändert oder ersetzt, die mit einem Datenträger, die, den der Mandanten nicht vertraut. Schließlich wird BitLocker auf dem Datenträger-Betriebssystem installiert (sofern sie nicht bereits vorhanden ist) zum Vorbereiten des Datenträgers für die Verschlüsselung während der Bereitstellung des virtuellen Computers.

> [!NOTE]
> Der vorlagendatenträger-Assistenten ändern Sie den vorlagendatenträger, die Sie für ein direktes angeben. Möglicherweise möchten eine Kopie des ungeschützten VHDX vor dem Ausführen des Assistenten zum vornehmen von Aktualisierungen auf den Datenträger zu einem späteren Zeitpunkt zu erstellen. Es werden nicht möglich, einen Datenträger zu ändern, der mit den vorlagendatenträger-Assistenten geschützt wurde.

Führen Sie die folgenden Schritte aus, auf einem Computer unter Windows Server 2016 (muss nicht auf einem bewachten Host oder dem VMM-Server sein):

1. Kopieren Sie im erstellten generalisierte VHDX [vorbereiten ein Betriebssystems VHDX](#prepare-an-operating-system-vhdx) auf dem Server, wenn sie nicht bereits vorhanden ist.

2. Installieren Sie die **Tools für geschützte VMs** Funktion **Remoteserver-Verwaltungstools** auf dem Computer.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart

3. Abrufen Sie oder erstellen Sie ein Zertifikat zum Signieren der VHDX, der den vorlagendatenträger für neue abgeschirmte VMs werden soll. Details zu diesem Zertifikat werden in eine geschützte Datendatei integriert werden, die die Datenträger als Datenträger an vertrauenswürdigen autorisiert. Aus diesem Grund ist es wichtig, um dieses Zertifikat von einer Zertifizierungsstelle zu erhalten, die Sie und Ihr hosting--Vertrauensstellung Dienst. In Enterprise-Szenarien, in denen Sie sowohl Hoster als auch Mandant sind, sollten Sie dieses Zertifikat von Ihrer PKI ausgegeben.

    Wenn Sie zum Einrichten einer testumgebung und nur ein selbst signiertes Zertifikat zum Signieren Ihrer vorlagendatenträger verwenden möchten, führen Sie einen Befehl ähnlich dem folgenden auf Ihrem Computer:

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. Starten Sie den **Vorlagendatenträger-Assistenten** aus der **Verwaltung** Ordner im Startmenü oder durch Eingabe **TemplateDiskWizard.exe** an einer Eingabeaufforderung.

5. Auf der **Zertifikat** auf **Durchsuchen** um eine Liste der Zertifikate anzuzeigen. Wählen Sie das Zertifikat mit dem die datenträgervorlage signieren. Klicken Sie auf **OK** und dann auf **Weiter**.

6. Klicken Sie auf der Seite virtuelle Datenträger auf **Durchsuchen** um VHDX auszuwählen, den Sie vorbereitet haben, klicken Sie dann auf **Weiter**.

7. Geben Sie auf der Seite Signaturkatalog einen aussagekräftigen **Datenträgernamen** und **Version.** Diese Felder sind vorhanden, können Sie den Datenträger zu identifizieren, sobald sie signiert wurde.

    Beispielsweise **Datenträgernamen** Geben Sie _WS2016_ und **Version**, _1.0.0.0_

8. Überprüfen Sie Ihre Auswahl auf der Seite überprüfen Sie die Einstellungen des Assistenten aus. Beim Klicken auf **generieren**, der Assistent Aktivieren von BitLocker auf dem vorlagendatenträger, berechnen Sie den Hashwert des Datenträgers, und erstellen Sie die Volume-Signaturkatalogs, die in den VHDX-Metadaten gespeichert ist.

    Warten Sie, bis der Prozess der signaturvergabe abgeschlossen ist, bevor Sie versuchen, bereitstellen, oder verschieben den vorlagendatenträger. Dieser Vorgang kann etwas Zeit in Anspruch, je nach Größe des Datenträgers dauern. 

9. Auf der **Zusammenfassung** Seite Informationen über datenträgervorlage, das Zertifikat zum Signieren der Vorlage verwendet, und den Aussteller des Zertifikats angezeigt wird. Klicken Sie auf **Schließen**, um den Assistenten zu beenden.


Die datenträgervorlage geschützten auf der hosting-Anbieter sowie eine geschützte Datendatei, die Sie erstellen, bereitstellen, wie in beschrieben [erstellen, die geschützten Daten, die zum Definieren einer abgeschirmten VM](guarded-fabric-tenant-creates-shielding-data.md).

## <a name="see-also"></a>Siehe auch

- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
