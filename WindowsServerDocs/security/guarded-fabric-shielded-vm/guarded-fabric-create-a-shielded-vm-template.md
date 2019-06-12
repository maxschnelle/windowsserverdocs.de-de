---
title: Erstellen eines Windows abgeschirmten VM vorlagedatenträgers
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 9c8b84e8-1f5a-47a1-83ca-b1dbd801cb0b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/29/2019
ms.openlocfilehash: d9f07d2e6e93d4f8d198c2fc3b62c28c940bdefb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447509"
---
# <a name="create-a-windows-shielded-vm-template-disk"></a>Erstellen eines Windows abgeschirmten VM vorlagedatenträgers

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wie bei regulären VMs eine VM-Vorlage erstellt wird (z. B. eine [VM-Vorlage in Virtual Machine Manager (VMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-library-add-vm-templates)) zu erleichtern für Mandanten und Administratoren, um neue VMs im Fabric mithilfe eines vorlagedatenträgers bereitzustellen. Da abgeschirmte VMs sicherheitsrelevante Objekte sind, stehen zusätzliche Schritte zum Erstellen einer VM-Vorlage, die Schutz unterstützt. Dieses Thema enthält die Schritte zum Erstellen einer abgeschirmte vorlagedatenträger und eine VM-Vorlage in VMM.

Um zu verstehen, wie in diesem Thema in den gesamten Vorgang der Bereitstellung von abgeschirmten VMs passt, finden Sie unter [Service Provider-Konfigurationsschritte für das Hosten von überwachten Hosts und abgeschirmte VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="prepare-an-operating-system-vhdx"></a>Bereiten Sie ein VHDX-Betriebssystem vor.

Zunächst vorbereiten Sie einen Betriebssystem-Datenträger, den Sie dann mit der abgeschirmten Vorlage Datenträger Projekterstellungs-Assistent ausgeführt werden. Dieser Datenträger wird als Betriebssystem-Datenträger in den VMs des Mandanten verwendet werden. Sie können alle vorhandenen Tools verwenden, erstellen diesen Datenträger, z. B. Microsoft Desktop Image Service Manager (DISM) oder manuell Einrichten eines virtuellen Computers mit einem leeren VHDX und installieren Sie das Betriebssystem auf diesem Datenträger. Bei der Einrichtung des Datenträgers müssen sie die folgenden Anforderungen erfüllen, die auf Generation 2 gelten bzw. abgeschirmte VMs: 

| Anforderung für VHDX | Grund |
|-----------|----|
|Ein GUID-Partitionstabelle (GPT) Datenträger muss sein werden. | Erforderlich für virtuelle Maschinen der Generation 2 um UEFI zu unterstützen|
|Datenträgertyp muss **grundlegende** im Gegensatz zu **dynamische**. <br>Hinweis: Dies bezieht sich auf den Typ der logischer Datenträger, nicht die "dynamisch erweiterbar" VHDX-Feature von Hyper-V unterstützt. | BitLocker bietet keine Unterstützung für dynamische Datenträger.|
|Der Datenträger verfügt über mindestens zwei Partitionen. Eine Partition muss das Laufwerk enthalten, auf dem Windows installiert ist. Dies ist das Laufwerk, das BitLocker verschlüsselt wird. Die andere Partition ist die aktive Partition, die enthält den Bootloader und bleibt unverschlüsselt, sodass der Computer gestartet werden kann.|Erforderlich für BitLocker|
|Dateisystem ist NTFS | Erforderlich für BitLocker|
|Das Betriebssystem installiert wird, auf die VHDX ist eine der folgenden:<br>– Windows Server 2016, Windows Server 2012 R2 oder WindowsServer 2012 <br>- Windows 10, Windows 8.1, Windows 8| Erforderlich, um virtuelle Maschinen der Generation 2 und der sichere Start von Microsoft-Vorlage zu unterstützen|
|Betriebssystem muss generalisierten (Ausführung sysprep.exe) sein. | Für die Bereitstellung von Vorlage umfasst spezialisiert sich auf virtuelle Computer für einen bestimmten Mandanten arbeitsauslastung| 

> [!NOTE]
> Wenn Sie VMM verwenden, kopieren Sie nicht den vorlagendatenträger in der VMM-Bibliothek in dieser Phase. 

## <a name="run-windows-update-on-the-template-operating-system"></a>Führen Sie Windows Update auf dem Betriebssystem der Vorlage

Auf dem vorlagendatenträger stellen Sie sicher, dass das Betriebssystem alle die aktuellsten Windows Updates installiert ist. Vor kurzem veröffentlichten Updates verbessern die Zuverlässigkeit des geschützten Prozesses End-to-End - ein Prozess, der auf abgeschlossen, wenn das Betriebssystem der Vorlage möglicherweise nicht auf dem neuesten Stand.

## <a name="prepare-and-protect-the-vhdx-with-the-template-disk-wizard"></a>Vorbereiten Sie und schützen Sie die VHDX mit den vorlagendatenträger-Assistenten

Um einen vorlagendatenträger mit abgeschirmten virtuellen Computern zu verwenden, muss der Datenträger vorbereitet und mit der abgeschirmten Vorlage Datenträger Projekterstellungs-Assistent mit BitLocker verschlüsselt werden. Dieser Assistent generiert einen Hashwert für den Datenträger und ein Volume-signaturkatalogs (VSC) hinzugefügt. Dem VSC bzw. ist mit einem Zertifikat signiert Sie angeben, und werden während der Bereitstellung verwendet, um sicherzustellen, dass der Datenträger für einen Mandanten bereitgestellt wird nicht geändert oder ersetzt, die mit einem Datenträger, die, den der Mandanten nicht vertraut. Schließlich wird BitLocker auf dem Datenträger-Betriebssystem installiert (sofern sie nicht bereits vorhanden ist) zum Vorbereiten des Datenträgers für die Verschlüsselung während der Bereitstellung des virtuellen Computers.

> [!NOTE]
> Der vorlagendatenträger-Assistenten ändern Sie den vorlagendatenträger, die Sie für ein direktes angeben. Möglicherweise möchten eine Kopie des ungeschützten VHDX vor dem Ausführen des Assistenten zum vornehmen von Aktualisierungen auf den Datenträger zu einem späteren Zeitpunkt zu erstellen. Es werden nicht möglich, einen Datenträger zu ändern, der mit den vorlagendatenträger-Assistenten geschützt wurde.

Führen Sie die folgenden Schritte aus, auf einem Computer unter Windows Server 2016 (muss nicht auf einem bewachten Host oder einem VMM-Server sein):

1. Kopieren Sie im erstellten generalisierte VHDX [vorbereiten ein Betriebssystems VHDX](#prepare-an-operating-system-vhdx) auf dem Server, wenn sie nicht bereits vorhanden ist.

2. Installieren Sie den Server lokal zu verwalten, die **Tools für geschützte VMs** Funktion **Remoteserver-Verwaltungstools** auf dem Server.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
        
    Sie können auch den Server von einem Clientcomputer, auf dem Sie installiert haben, verwalten die [Remote Server Administration Tools von Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=45520).

3. Abrufen Sie oder erstellen Sie ein Zertifikat zum Signieren von dem VSC bzw. für die VHDX, der den vorlagendatenträger für neue abgeschirmte VMs werden soll. Details zu diesem Zertifikat werden für Mandanten angezeigt werden, bei der Erstellung ihrer schutzdatendateien und Autorisieren von Datenträgern, denen, die Sie vertrauen, werden. Aus diesem Grund ist es wichtig, um dieses Zertifikat von einer Zertifizierungsstelle, die von Ihnen und Ihren Mandanten sich gegenseitig vertrauenswürdigen zu erhalten. In Enterprise-Szenarien, in denen Sie sowohl Hoster als auch Mandant sind, sollten Sie dieses Zertifikat von Ihrer PKI ausgegeben.

    Wenn Sie zum Einrichten einer testumgebung und ein selbstsigniertes Zertifikat verwenden, um Ihre vorlagendatenträger vorzubereiten möchten, führen Sie einen Befehl, der etwa wie folgt:

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. Starten Sie den **Vorlagendatenträger-Assistenten** aus der **Verwaltung** Ordner im Startmenü oder durch Eingabe **TemplateDiskWizard.exe** an einer Eingabeaufforderung.

5. Auf der **Zertifikat** auf **Durchsuchen** um eine Liste der Zertifikate anzuzeigen. Wählen Sie das Zertifikat mit dem die Vorlage für die Datenträger vorzubereiten. Klicken Sie auf **OK** und dann auf **Weiter**.

6. Klicken Sie auf der Seite virtuelle Datenträger auf **Durchsuchen** um VHDX auszuwählen, den Sie vorbereitet haben, klicken Sie dann auf **Weiter**.

7. Geben Sie auf der Seite Signaturkatalog einen aussagekräftigen **Datenträgernamen** und **Version.** Diese Felder sind vorhanden, können Sie den Datenträger zu identifizieren, sobald es vorbereitet wurde.

    Beispielsweise **Datenträgernamen** Geben Sie _WS2016_ und **Version**, _1.0.0.0_

8. Überprüfen Sie Ihre Auswahl auf der Seite überprüfen Sie die Einstellungen des Assistenten aus. Beim Klicken auf **generieren**, der Assistent Aktivieren von BitLocker auf dem vorlagendatenträger, berechnen Sie den Hashwert des Datenträgers, und erstellen Sie die Volume-Signaturkatalogs, die in den VHDX-Metadaten gespeichert ist.

    Warten Sie, bis der datenvorbereitung Vorgang abgeschlossen wurde, bevor Sie versuchen, bereitstellen, oder verschieben den vorlagendatenträger. Dieser Vorgang kann etwas Zeit in Anspruch, je nach Größe des Datenträgers dauern.

    > [!IMPORTANT]
    > Vorlagedatenträger können nur mit der sicheren abgeschirmte VM-Bereitstellung verwendet werden.
    > Versuchen, einen normalen (nicht geschirmten) virtuellen Computer mithilfe eines vorlagedatenträgers zu starten, werden Sie wahrscheinlich einen Stop-Fehler (blauer Bildschirm) und wird nicht unterstützt.

9. Auf der **Zusammenfassung** Seite Informationen über datenträgervorlage, das Zertifikat, mit dem VSC bzw. anmelden und den Aussteller des Zertifikats wird angezeigt. Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

Wenn Sie VMM verwenden, führen Sie die Schritte in den übrigen Abschnitten in diesem Thema, um einen vorlagendatenträger in eine abgeschirmte VM-Vorlage in VMM zu integrieren. 

## <a name="copy-the-template-disk-to-the-vmm-library"></a>Kopieren Sie den vorlagendatenträger die VMM-Bibliothek

Wenn Sie VMM verwenden, nachdem Sie einen vorlagendatenträger erstellen, müssen Sie kopieren Sie ihn in einer VMM-Bibliotheksfreigabe aus, damit Hosts herunterladen und verwenden Sie den Datenträger aus, wenn Sie neue VMs bereitstellen können. Verwenden Sie das folgende Verfahren, kopieren Sie den vorlagendatenträger, in der VMM-Bibliothek, und aktualisieren Sie die Bibliothek.

1. Kopieren Sie die VHDX-Datei, in der Freigabeordner des VMM-Bibliothek. Wenn Sie die VMM-Standardkonfiguration verwendet haben, kopieren Sie den vorlagendatenträger,  _\\ <vmmserver>\MSSCVMMLibrary\VHDs_.

2. Aktualisieren Sie den Bibliothekserver an. Öffnen der **Bibliothek** Arbeitsbereich, erweitern Sie **Bibliothekserver**mit der rechten Maustaste auf den Bibliothekserver, den Sie aktualisieren möchten, und klicken Sie auf **aktualisieren**.

3. Als Nächstes stellen Sie VMM mit Informationen über das Betriebssystem auf dem vorlagendatenträger installiert:

    a. Finden Sie den Datenträger neu importierte Vorlage, auf dem Bibliotheksserver in der **Bibliothek** Arbeitsbereich.

    b. Mit der rechten Maustaste in des Datenträgers, und klicken Sie dann auf **Eigenschaften**.

    c. Für **Betriebssystem**, erweitern Sie die Liste, und wählen Sie das Betriebssystem auf dem Datenträger installiert. Auswählen eines Betriebssystems wird VMM mitgeteilt, dass die VHDX nicht leer ist.

    d. Klicken Sie auf **OK**.

Das kleine Shield-Symbol neben dem Datenträger kennzeichnet den Datenträger als Datenträger vorbereitete-Vorlage für abgeschirmte VMs. Sie können auch nach rechts klicken Sie auf die Spaltenkopfzeilen und ein-/Ausschalten der **abgeschirmte** Spalte finden Sie unter einer Textdarstellung, der angibt, ob ein Datenträger für die reguläre oder eine geschützte VM-Bereitstellungen vorgesehen ist.

![Vorlagendatenträger für abgeschirmte vm](../media/Guarded-Fabric-Shielded-VM/shielded-vm-template-disk.png)

## <a name="create-the-shielded-vm-template-in-vmm-using-the-prepared-template-disk"></a>Erstellen Sie die abgeschirmte VM-Vorlage in VMM mithilfe des Datenträgers, vorbereitete-Vorlage

Mit einem vorbereiteten vorlagendatenträger in der VMM-Bibliothek können Sie eine VM-Vorlage für abgeschirmte VMs zu erstellen. VM-Vorlagen für abgeschirmte VMs unterscheiden sich geringfügig von herkömmlichen VM-Vorlagen, bestimmte Einstellungen behoben wurden (Generation 2 VM "," UEFI "und" Sicherer Start aktiviert und So weiter) und andere sind nicht verfügbar ist (Mandanten-Anpassung ist beschränkt auf wenige, wählen Sie Eigenschaften des virtuellen Computers) . Um die VM-Vorlage zu erstellen, führen Sie die folgenden Schritte aus:

1. In der **Bibliothek** Arbeitsbereich, klicken Sie auf **VM-Vorlage erstellen** auf der Registerkarte "home" oben.

2. Klicken Sie auf der Seite **Quelle auswählen** auf **Vorhandene VM-Vorlage oder in der Bibliothek gespeicherte virtuelle Festplatte verwenden** und dann auf **Durchsuchen**.

3. Wählen Sie im Fenster, das angezeigt wird, einen vorbereiteten vorlagendatenträger aus der VMM-Bibliothek. Um leichter zu identifizieren, welche Datenträger vorbereitet sind, mit der rechten Maustaste einer Spaltenüberschrift, und aktivieren Sie die **abgeschirmte** Spalte. Klicken Sie auf **OK** dann **Weiter**.

4. Geben Sie einen VM-Vorlagennamen und optional eine Beschreibung ein, und klicken Sie dann auf **Weiter**.

5. Auf der **Hardware konfigurieren** Seite, das die Funktionen des von dieser Vorlage erstellten virtuellen Computer angeben. Stellen Sie sicher, dass mindestens eine Netzwerkkarte verfügbar ist und auf der VM-Vorlage konfiguriert wird. Die einzige Möglichkeit für einen Mandanten für die Verbindung in eine abgeschirmte VM erfolgt über Remote Desktop Connection, Windows-Remoteverwaltung oder andere vorkonfigurierte Remoteverwaltungstools, die über die Netzwerkprotokolle zu arbeiten.

    Falls gewünscht, statische IP-Adresspools in VMM zu nutzen, anstatt einen DHCP-Server auf dem Netzwerk des Mandanten auszuführen, müssen Sie Ihre Mandanten für diese Konfiguration zu warnen. Wenn ein Mandant ihre geschützte Datendatei, die die Datei für die unbeaufsichtigte Installation für die VMM enthält bereitstellt, müssen sie spezielle Platzhalterwerte für die statische IP-Pool-Informationen bereitzustellen. Weitere Informationen zu VMM-Platzhalter in Mandanten für die unbeaufsichtigte Installation-Dateien, finden Sie unter [Erstellen einer Antwortdatei](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file). 

6. Auf der **Configure Operating System** Seite einige Optionen für abgeschirmte VMs, einschließlich der Product Key, Zeitzone und Computername wird von VMM nur anzeigen. Einige sichere Informationen, z. B. das Kennwort und Domäne den Namen des Administrators, von dem Mandanten angegeben ist, über eine geschützte Datendatei (. PDK-Datei). 

    > [!NOTE]
    > Wenn Sie einen Product Key auf dieser Seite angeben möchten, stellen Sie sicher, dass sie für das Betriebssystem auf dem vorlagendatenträger gültig ist. Wenn ein falscher Product Key verwendet wird, schlägt die Erstellung des virtuellen Computers fehl.

Nachdem die Vorlage erstellt wurde, können Mandanten sie verwenden, um neue virtuelle Computer zu erstellen. Sie müssen Sie sicherstellen, dass die VM-Vorlage eine Ressource für die Mandantenadministrator-Benutzerrolle verfügbar ist (in VMM-Benutzerrollen sind der **Einstellungen** Arbeitsbereich).

## <a name="prepare-and-protect-the-vhdx-using-powershell"></a>Vorbereiten Sie und schützen Sie die VHDX mithilfe von PowerShell

Als Alternative zum Ausführen von den Vorlagendatenträger-Assistenten können Sie Ihre vorlagedatenträger und das Zertifikat auf einem Computer mit Remoteserver-Verwaltungstools zu kopieren und ausführen können [schützen-TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps
) zum Prozess den signaturvergabe zu initiieren.
Im folgenden Beispiel wird der Name und Version Informationen gemäß der _TemplateName_ und _Version_ Parameter.
Die VHDX, die Sie, um angeben die `-Path` Typparameter wird mit dem Datenträger für die aktualisierte Vorlage überschrieben werden, daher unbedingt eine Kopie zu erstellen, bevor der Befehl ausgeführt wird.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Certificate $certificate -Path "WindowsServer2019-ShieldedTemplate.vhdx" -TemplateName "Windows Server 2019" -Version 1.0.0.0
```

Ihre vorlagendatenträger kann jetzt zum Bereitstellen geschützter VMs verwendet werden.
Wenn Sie System Center Virtual Machine Manager zur Bereitstellung Ihrer VM verwenden, können Sie jetzt die VHDX auf die VMM-Bibliothek kopieren.

Sie sollten auch die Volume-signaturkatalogs von VHDX zu extrahieren.
Diese Datei wird verwendet, Informationen über das Signaturzertifikat, Datenträgername und Version um VM-Besitzer ermöglichen Ihrer Vorlage verwendet werden soll.
Sie müssen diese Datei in den Assistenten für geschützte Datendateien, autorisieren Sie den Autor der Vorlage im Besitz des Signaturzertifikats, zum Erstellen dieser importieren und zukünftige Vorlage für diese Datenträger.

Um die Volume-signaturkatalogs zu extrahieren, führen Sie den folgenden Befehl in PowerShell aus:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```


## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Erstellen Sie eine geschützte Datendatei](guarded-fabric-tenant-creates-shielding-data.md)

## <a name="see-also"></a>Siehe auch

- [Hosten von Service Provider-Konfigurationsschritte für die überwachten Hosts und abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
