---
title: Erstellen eines Datenträgers für eine geschützte Windows-VM-Vorlage
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 9c8b84e8-1f5a-47a1-83ca-b1dbd801cb0b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/29/2019
ms.openlocfilehash: 686fd2ed5969d191240bbd726f1d759e9974f08a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386679"
---
# <a name="create-a-windows-shielded-vm-template-disk"></a>Erstellen eines Datenträgers für eine geschützte Windows-VM-Vorlage

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wie bei regulären virtuellen Computern können Sie eine VM-Vorlage erstellen (z. b. eine [VM-Vorlage in Virtual Machine Manager (VMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-library-add-vm-templates)), damit Mandanten und Administratoren mithilfe eines Vorlagen Datenträgers problemlos neue VMS im Fabric bereitstellen können. Da abgeschirmte VMS sicherheitsrelevante Ressourcen sind, sind zusätzliche Schritte erforderlich, um eine VM-Vorlage zu erstellen, die Schutz unterstützt. In diesem Thema werden die Schritte zum Erstellen eines geschützten Vorlagen Datenträgers und einer VM-Vorlage in VMM behandelt.

Informationen dazu, wie sich dieses Thema in den Gesamtprozess der Bereitstellung von abgeschirmten VMS einfügt, finden Sie unter [Hosten von Dienstanbietern Konfigurationsschritte für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="prepare-an-operating-system-vhdx"></a>Vorbereiten einer vhdx-Betriebssystem Datei

Bereiten Sie zuerst einen Betriebssystem Datenträger vor, den Sie dann mit dem Assistenten zum Erstellen einer abgeschirmten Vorlage ausführen Dieser Datenträger wird als Betriebssystem Datenträger in den virtuellen Computern Ihres Mandanten verwendet. Zum Erstellen dieses Datenträgers können Sie beliebige vorhandene Tools verwenden, z. b. Microsoft Desktop Image Service Manager (Mage), oder Sie können manuell einen virtuellen Computer mit einer leeren vhdx einrichten und das Betriebssystem auf diesem Datenträger installieren. Beim Einrichten des Datenträgers müssen die folgenden Anforderungen erfüllt werden, die für die Generation 2 und/oder abgeschirmte VMS spezifisch sind: 

| Anforderung für vhdx | Grund |
|-----------|----|
|Muss ein GPT-Datenträger (GUID-Partitionstabelle) sein. | Erforderlich für virtuelle Computer der Generation 2 zur Unterstützung von UEFI|
|Der Datenträgertyp muss Standard und nicht **dynamisch** **sein.** <br>Hinweis: Dies bezieht sich auf den Typ des logischen Datenträgers, nicht auf das von Hyper-V unterstützte "dynamisch erweiterbare" vhdx-Feature. | BitLocker unterstützt keine dynamischen Datenträger.|
|Der Datenträger verfügt über mindestens zwei Partitionen. Eine Partition muss das Laufwerk enthalten, auf dem Windows installiert ist. Dies ist das Laufwerk, das von BitLocker verschlüsselt wird. Die andere Partition ist die aktive Partition, die den Bootloader enthält und unverschlüsselt bleibt, damit der Computer gestartet werden kann.|Für BitLocker erforderlich|
|Dateisystem ist NTFS | Für BitLocker erforderlich|
|Das auf der vhdx installierte Betriebssystem ist einer der folgenden:<br>-Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 <br>-Windows 10, Windows 8.1, Windows 8| Erforderlich zur Unterstützung virtueller Maschinen der Generation 2 und der Microsoft-Vorlage für den sicheren Start|
|Das Betriebssystem muss generalisiert sein (führen Sie "syspree. exe" aus). | Die Vorlagen Bereitstellung umfasst spezialisierte VMs für die Arbeitsauslastung eines bestimmten Mandanten.| 

> [!NOTE]
> Wenn Sie VMM verwenden, kopieren Sie den Vorlagen Datenträger in dieser Phase nicht in die VMM-Bibliothek. 

## <a name="run-windows-update-on-the-template-operating-system"></a>Ausführen von Windows Update auf dem Vorlagen Betriebssystem

Vergewissern Sie sich auf dem Vorlagen Datenträger, dass alle aktuellen Windows-Updates auf dem Betriebssystem installiert sind. Kürzlich veröffentlichte Updates verbessern die Zuverlässigkeit des End-to-End-Schutz Vorgangs. Dies ist ein Prozess, der möglicherweise nicht abgeschlossen wird, wenn das Vorlagen Betriebssystem nicht auf dem neuesten Stand ist.

## <a name="prepare-and-protect-the-vhdx-with-the-template-disk-wizard"></a>Vorbereiten und schützen der vhdx-Datei mit dem Vorlagen Datenträger-Assistenten

Um einen Vorlagen Datenträger mit abgeschirmten VMS zu verwenden, muss der Datenträger mithilfe des Assistenten für die Datenträger Erstellung für abgeschirmte Vorlagen mit BitLocker vorbereitet und verschlüsselt werden. Dieser Assistent generiert einen Hash für den Datenträger und fügt ihn einem volumesignaturkatalog (VSC) hinzu. Der VSC wird mit einem von Ihnen angegebenen Zertifikat signiert und während des Bereitstellungs Prozesses verwendet, um sicherzustellen, dass der Datenträger, der für einen Mandanten bereitgestellt wird, nicht geändert oder durch einen Datenträger ersetzt wurde, dem der Mandant nicht vertraut. Schließlich wird BitLocker auf dem Betriebssystem des Datenträgers installiert (sofern es noch nicht vorhanden ist), um den Datenträger für die Verschlüsselung während der VM-Bereitstellung vorzubereiten.

> [!NOTE]
> Der Vorlagen Datenträger-Assistent ändert den Vorlagen Datenträger, den Sie direkt angeben. Sie sollten eine Kopie der ungeschützten vhdx-Datei erstellen, bevor Sie den Assistenten ausführen, um die Datenträger zu einem späteren Zeitpunkt zu aktualisieren. Sie können einen Datenträger, der mit dem Vorlagen Datenträger-Assistenten geschützt wurde, nicht ändern.

Führen Sie die folgenden Schritte auf einem Computer aus, auf dem Windows Server 2016 ausgeführt wird (es muss sich nicht um einen überwachten Host oder VMM-Server handeln):

1. Kopieren Sie die in [Vorbereiten einer Betriebssystem-vhdx](#prepare-an-operating-system-vhdx) erstellte generalisierte vhdx auf den Server, sofern diese nicht bereits vorhanden ist.

2. Um den Server lokal zu verwalten, installieren Sie das Feature der **abgeschirmten VM-Tools** von **Remoteserver-Verwaltungstools** auf dem Server.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
        
    Sie können den Server auch über einen Client Computer verwalten, auf dem Sie die [Windows 10-Remoteserver-Verwaltungstools](https://www.microsoft.com/en-us/download/details.aspx?id=45520)installiert haben.

3. Abrufen oder Erstellen eines Zertifikats zum Signieren des VSC für die vhdx-Datei, die als Vorlagen Datenträger für neue abgeschirmte VMS verwendet wird. Details zu diesem Zertifikat werden den Mandanten angezeigt, wenn Sie Ihre geschützten Datendateien erstellen und die Datenträger autorisierst, denen Sie vertrauen. Daher ist es wichtig, dass Sie dieses Zertifikat von einer Zertifizierungsstelle abrufen, die von Ihnen und ihren Mandanten als nicht vertrauenswürdig eingestuft wird. In Unternehmens Szenarios, in denen Sie sowohl der Host als auch der Mandant sind, sollten Sie das Zertifikat aus Ihrer PKI ausgeben.

    Wenn Sie eine Testumgebung einrichten und nur ein selbst signiertes Zertifikat verwenden möchten, um den Vorlagen Datenträger vorzubereiten, führen Sie einen Befehl aus, der dem folgenden ähnelt:

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. Starten Sie den Vorlagen Datenträger- **Assistenten** im Ordner " **Verwaltung** " im Startmenü, oder geben Sie " **templatediskwizard. exe** " an einer Eingabeaufforderung ein.

5. Klicken Sie auf der Seite **Zertifikat** auf **Durchsuchen** , um eine Liste mit Zertifikaten anzuzeigen. Wählen Sie das Zertifikat aus, mit dem die Datenträger Vorlage vorbereitet werden soll. Klicken Sie auf **OK** und dann auf **Weiter**.

6. Klicken Sie auf der Seite virtueller Datenträger auf **Durchsuchen** , um das vhdx auszuwählen, das Sie vorbereitet haben, und klicken Sie dann auf **weiter**.

7. Geben Sie auf der Seite Signatur Katalog einen anzeigen **Amen** und eine **Version** des Datenträgers an. Diese Felder sind vorhanden, damit Sie den Datenträger nach der Vorbereitung identifizieren können.

    Beispielsweise können Sie für den Datenträger Namen _WS2016_ und für **Version**, _1.0.0.0_ eingeben.

8. Überprüfen Sie Ihre Auswahl auf der Seite Einstellungen überprüfen des Assistenten. Wenn Sie auf **generieren**klicken, aktiviert der Assistent BitLocker auf dem Vorlagen Datenträger, berechnet den Hash des Datenträgers und erstellt den volumensignaturkatalog, der in den vhdx-Metadaten gespeichert ist.

    Warten Sie, bis der Vorbereitungs Vorgang abgeschlossen ist, bevor Sie versuchen, den Vorlagen Datenträger zu starten Der Vorgang kann je nach Größe des Datenträgers einige Zeit in Anspruch nehmen.

    > [!IMPORTANT]
    > Vorlagen Datenträger können nur mit dem sicheren geschützten VM-Bereitstellungs Prozess verwendet werden.
    > Der Versuch, einen regulären virtuellen Computer mit einem Vorlagen Datenträger zu starten, führt wahrscheinlich zu einem Fehler beim Abbrechen (blauer Bildschirm) und wird nicht unterstützt.

9. Auf der Seite **Zusammenfassung** werden Informationen zur Datenträger Vorlage, zum Zertifikat, das zum Signieren des VSC und zum Aussteller des Zertifikats verwendet wird, angezeigt. Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

Wenn Sie VMM verwenden, führen Sie die Schritte in den restlichen Abschnitten in diesem Thema aus, um einen Vorlagen Datenträger in eine geschützte VM-Vorlage in VMM einzubinden. 

## <a name="copy-the-template-disk-to-the-vmm-library"></a>Kopieren Sie den Vorlagen Datenträger in die VMM-Bibliothek

Wenn Sie VMM verwenden, müssen Sie nach dem Erstellen eines Vorlagen Datenträgers diese Datei in eine VMM-Bibliotheks Freigabe kopieren, damit Hosts den Datenträger herunterladen und verwenden können, wenn Sie neue VMs bereitstellen. Verwenden Sie das folgende Verfahren, um den Vorlagen Datenträger in die VMM-Bibliothek zu kopieren und dann die Bibliothek zu aktualisieren.

1. Kopieren Sie die vhdx-Datei in den Ordner der VMM-Bibliotheks Freigabe. Wenn Sie die VMM-Standardkonfiguration verwendet haben, kopieren Sie den Vorlagen _Datenträger in \\ @ no__t-2\MSSCVMMLibrary\VHDs_.

2. Aktualisieren Sie den Bibliothek Server. Öffnen Sie den Arbeitsbereich **Bibliothek** , erweitern Sie **Bibliothek Server**, klicken Sie mit der rechten Maustaste auf den Bibliothek Server, den Sie aktualisieren möchten, und klicken Sie auf **Aktualisieren**.

3. Als Nächstes stellen Sie VMM Informationen zum Betriebssystem bereit, das auf dem Vorlagen Datenträger installiert ist:

    a. Suchen Sie den neu importierten Vorlagen Datenträger auf dem Bibliothek Server im Arbeitsbereich **Bibliothek** .

    b. Klicken Sie mit der rechten Maustaste auf den Datenträger und dann auf **Eigenschaften**.

    c. Erweitern Sie unter **Betriebssystem**die Liste, und wählen Sie das Betriebssystem aus, das auf dem Datenträger installiert ist. Die Auswahl eines Betriebssystems weist VMM darauf hin, dass die vhdx nicht leer ist.

    d. Klicken Sie auf **OK**.

Das kleine Schild Symbol neben dem Namen des Datenträgers bezeichnet den Datenträger als vorbereiteten Vorlagen Datenträger für geschützte VMS. Sie können auch mit der rechten Maustaste auf die Spaltenüberschriften klicken und die **geschützte** Spalte umschalten, um eine Textdarstellung anzuzeigen, die angibt, ob ein Datenträger für reguläre oder abgeschirmte VM-bereit Stellungen vorgesehen ist.

![Vorlage für abgeschirmte VM-Vorlage](../media/Guarded-Fabric-Shielded-VM/shielded-vm-template-disk.png)

## <a name="create-the-shielded-vm-template-in-vmm-using-the-prepared-template-disk"></a>Erstellen der abgeschirmten VM-Vorlage in VMM mithilfe des vorbereiteten Vorlagen Datenträgers

Mit einem vorbereiteten Vorlagen Datenträger in der VMM-Bibliothek können Sie eine VM-Vorlage für abgeschirmte VMS erstellen. VM-Vorlagen für abgeschirmte VMS unterscheiden sich geringfügig von herkömmlichen VM-Vorlagen dahin, dass bestimmte Einstellungen fest sind (VM der Generation 2, UEFI und sicherer Start aktiviert usw.) und andere nicht verfügbar sind (die Anpassung der Mandanten ist auf einige wenige, SELECT-Eigenschaften der VM beschränkt). . Führen Sie die folgenden Schritte aus, um die VM-Vorlage zu erstellen:

1. Klicken Sie im Arbeitsbereich **Bibliothek** oben auf der Registerkarte Start auf **VM-Vorlage erstellen** .

2. Klicken Sie auf der Seite **Quelle auswählen** auf **Vorhandene VM-Vorlage oder in der Bibliothek gespeicherte virtuelle Festplatte verwenden** und dann auf **Durchsuchen**.

3. Wählen Sie im angezeigten Fenster einen vorbereiteten Vorlagen Datenträger aus der VMM-Bibliothek aus. Um leichter festzustellen, welche Datenträger vorbereitet werden, klicken Sie mit der rechten Maustaste auf einen Spaltenheader, und aktivieren Sie die **geschützte** Spalte. Klicken Sie auf **OK** und dann **weiter**.

4. Geben Sie einen VM-Vorlagen Namen und optional eine Beschreibung ein, und klicken Sie dann auf **weiter**.

5. Geben Sie auf der Seite **Hardware konfigurieren** die Funktionen der virtuellen Computer an, die aus dieser Vorlage erstellt wurden. Stellen Sie sicher, dass mindestens eine NIC für die VM-Vorlage verfügbar und konfiguriert ist. Die einzige Möglichkeit für einen Mandanten, eine Verbindung mit einer abgeschirmten VM herzustellen, ist die Remotedesktopverbindung, Windows-Remoteverwaltung oder anderen vorkonfigurierten Remote Verwaltungs Tools, die über Netzwerkprotokolle arbeiten.

    Wenn Sie statische IP-Pools in VMM nutzen möchten, anstatt einen DHCP-Server im Mandanten Netzwerk ausführen zu müssen, müssen Sie Ihre Mandanten für diese Konfiguration benachrichtigen. Wenn ein Mandant seine Schutz Datendatei bereitstellt, die die Datei für die unbeaufsichtigte Installation für VMM enthält, muss er spezielle Platzhalter Werte für die Informationen des statischen IP-Pools angeben. Weitere Informationen zu VMM-Platzhaltern in Dateien für die unbeaufsichtigte Installation von Mandanten finden Sie unter [Erstellen einer Antwortdatei](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file). 

6. Auf der Seite **Betriebs System konfigurieren** werden von VMM nur einige Optionen für abgeschirmte VMS angezeigt, einschließlich der Product Key, der Zeitzone und des Computer namens. Einige sichere Informationen, z. b. das Administrator Kennwort und der Domänen Name, werden vom Mandanten über eine geschützte Datendatei () angegeben. PDK-Datei). 

    > [!NOTE]
    > Wenn Sie einen Product Key auf dieser Seite angeben, stellen Sie sicher, dass er für das Betriebssystem auf dem Vorlagen Datenträger gültig ist. Wenn eine falsche Product Key verwendet wird, tritt bei der VM-Erstellung ein Fehler auf.

Nachdem die Vorlage erstellt wurde, können Mandanten Sie zum Erstellen neuer virtueller Maschinen verwenden. Sie müssen überprüfen, ob es sich bei der VM-Vorlage um eine der für die Mandantenadministrator-Benutzerrolle verfügbaren Ressourcen handelt (in VMM befinden sich Benutzer Rollen im Arbeitsbereich " **Einstellungen** ").

## <a name="prepare-and-protect-the-vhdx-using-powershell"></a>Vorbereiten und schützen der vhdx-Datei mithilfe von PowerShell

Als Alternative zum Ausführen des Assistenten für Vorlagen Datenträger können Sie den Vorlagen Datenträger und das Zertifikat auf einen Computer kopieren, auf dem RSAT ausgeführt wird, und [protect-templatedisk @ no__t-1 ausführen, um den Signatur Prozess zu initiieren.
Im folgenden Beispiel werden der Name und die Versionsinformationen verwendet, die von den Parametern _templatename_ und _Version_ angegeben werden.
Die vhdx-Datei, die Sie für den Parameter "`-Path`" bereitstellen, wird mit dem aktualisierten Vorlagen Datenträger überschrieben. Achten Sie daher darauf, dass Sie vor dem Ausführen des Befehls

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Certificate $certificate -Path "WindowsServer2019-ShieldedTemplate.vhdx" -TemplateName "Windows Server 2019" -Version 1.0.0.0
```

Der Vorlagen Datenträger kann jetzt zum Bereitstellen von abgeschirmten VMS verwendet werden.
Wenn Sie System Center Virtual Machine Manager zum Bereitstellen Ihrer VM verwenden, können Sie jetzt die vhdx-Datei in die VMM-Bibliothek kopieren.

Möglicherweise möchten Sie auch den volumesignaturkatalog aus der vhdx-Datei extrahieren.
Diese Datei wird verwendet, um Informationen über das Signaturzertifikat, den Datenträger Namen und die Version für die VM-Besitzer bereitzustellen, die Ihre Vorlage verwenden möchten.
Sie müssen diese Datei in den Assistenten für die Schutz Datendatei importieren, um Sie zu autorisieren, den Vorlagen Autor im Besitz des Signatur Zertifikats, um diesen und zukünftige Vorlagen Datenträger zu erstellen.

Führen Sie den folgenden Befehl in PowerShell aus, um den volumesignaturkatalog zu extrahieren:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```


## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Erstellen einer Schutz Datendatei](guarded-fabric-tenant-creates-shielding-data.md)

## <a name="see-also"></a>Siehe auch

- [Konfigurationsschritte des hostingdienstanbieters für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
