---
title: 'Abgeschirmte VMs für Mandanten: Erstellen von Schutz Daten zum Definieren einer abgeschirmten VM'
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 1ae6f881e1bd4b9b317e5622f18958f25f692eec
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71940795"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>Abgeschirmte VMs für Mandanten: Erstellen von Schutz Daten zum Definieren einer abgeschirmten VM

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Eine geschützte Datendatei (auch als Bereitstellungsdatendatei oder PDK-Datei bezeichnet) ist eine verschlüsselte Datei, die ein Mandant oder VM-Besitzer erstellt, um wichtige VM-Konfigurationsinformationen, z.B. Administratorkennwort, RDP und andere identitätsbezogene Zertifikate, Domänenbeitritts-Anmeldeinformationen usw. zu schützen. Dieses Thema enthält Informationen zum Erstellen einer Schutz Datendatei. Bevor Sie die Datei erstellen können, müssen Sie entweder einen Vorlagen Datenträger von Ihrem hostingdienstanbieter abrufen oder einen Vorlagen Datenträger erstellen, wie unter [abgeschirmte VMs für Mandanten: Erstellen eines Vorlagen](guarded-fabric-tenant-creates-template-disk.md)Datenträgers (optional) beschrieben.

Eine Liste und ein Diagramm mit dem Inhalt einer Schutz Datendatei finden [Sie unter Was sind geschützte Daten? und warum ist es erforderlich?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

> [!IMPORTANT]
> Die Schritte in diesem Abschnitt sollten auf einem separaten, vertrauenswürdigen Computer außerhalb des geschützten Fabrics ausgeführt werden. Normalerweise erstellt der VM-Besitzer (Mandant) die geschützten Daten für Ihre VMS, nicht die Fabric-Administratoren.

Führen Sie die folgenden Schritte aus, um eine Schutz Datendatei zu erstellen:

- [Abrufen eines Zertifikats für Remotedesktopverbindung](#optional-obtain-a-certificate-for-remote-desktop-connection)
- [Erstellen einer Antwortdatei](#create-an-answer-file)
- [Get the Volume Signature Catalog file](#get-the-volume-signature-catalog-file)
- [Vertrauenswürdige Fabrics auswählen](#select-trusted-fabrics)

Anschließend können Sie die geschützte Datendatei erstellen:

- [Erstellen einer Schutz Datendatei und Hinzufügen von Betreuern](#create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard)

## <a name="optional-obtain-a-certificate-for-remote-desktop-connection"></a>Optionale Abrufen eines Zertifikats für Remotedesktopverbindung

Da Mandanten nur über Remotedesktopverbindung oder andere Remote Verwaltungs Tools eine Verbindung mit ihren abgeschirmten VMS herstellen können, ist es wichtig sicherzustellen, dass Mandanten sicherstellen können, dass Sie eine Verbindung mit dem richtigen Endpunkt herstellen (d. h. es ist kein "man in der Mitte"). die Verbindung wird abgefangen).

Eine Möglichkeit, um zu überprüfen, ob Sie eine Verbindung mit dem vorgesehenen Server herstellen, ist die Installation und Konfiguration eines Zertifikats, das Remotedesktopdienste beim Initiieren einer Verbindung vorhanden ist. Der Client Computer, der eine Verbindung mit dem Server herstellt, prüft, ob das Zertifikat vertrauenswürdig ist, und zeigt eine Warnung an. Im Allgemeinen werden RDP-Zertifikate von der PKI des Mandanten ausgegeben, um sicherzustellen, dass der Verbindungs Client dem Zertifikat vertraut. Weitere Informationen zur [Verwendung von Zertifikaten in Remotedesktopdienste finden Sie](https://technet.microsoft.com/library/dn781533.aspx) im TechNet.

 Beachten Sie Folgendes, um Sie bei der Entscheidung zu unterstützen, ob Sie ein benutzerdefiniertes RDP-Zertifikat erhalten müssen:

- Wenn Sie nur abgeschirmte VMs in einer Lab-Umgebung testen, benötigen Sie **kein** benutzerdefiniertes RDP-Zertifikat.
- Wenn Ihr virtueller Computer für den Beitritt zu einer Active Directory Domäne konfiguriert ist, wird in der Regel von der Zertifizierungsstelle Ihres Unternehmens automatisch ein Computer Zertifikat ausgestellt und zum Identifizieren des Computers bei RDP-Verbindungen verwendet. Sie benötigen **kein** benutzerdefiniertes RDP-Zertifikat.
- Wenn Ihr virtueller Computer keiner Domäne beigetreten ist, Sie jedoch sicherstellen möchten, dass Sie eine Verbindung mit dem richtigen Computer herstellen, wenn Sie Remotedesktop verwenden, sollten Sie die Verwendung von benutzerdefinierten RDP-Zertifikaten in **Erwägung gezogen** .

> [!TIP]
> Wenn Sie ein RDP-Zertifikat auswählen, das in die geschützte Datendatei aufgenommen werden soll, achten Sie darauf, ein Platzhalter Zertifikat zu verwenden. Eine geschützte Datendatei kann verwendet werden, um eine unbegrenzte Anzahl von VMS zu erstellen. Da jeder virtuelle Computer das gleiche Zertifikat verwendet, wird durch ein Platzhalter Zertifikat sichergestellt, dass das Zertifikat unabhängig vom Hostnamen des virtuellen Computers gültig ist.

## <a name="create-an-answer-file"></a>Erstellen einer Antwortdatei

Da der signierte Vorlagen Datenträger in VMM generalisiert ist, müssen Mandanten eine Antwortdatei bereitstellen, um Ihre abgeschirmten VMs während des Bereitstellungs Prozesses zu spezialisieren. Die Antwortdatei (häufig als Datei für die unbeaufsichtigte Installation bezeichnet) kann den virtuellen Computer für die beabsichtigte Rolle konfigurieren, d. h., er kann Windows-Features installieren, das im vorherigen Schritt erstellte RDP-Zertifikat registrieren und andere benutzerdefinierte Aktionen ausführen. Außerdem werden die erforderlichen Informationen für das Windows-Setup bereitgestellt, einschließlich des Standard Kennworts für den Administrator und Product Key.

Weitere Informationen zum Abrufen und Verwenden der **New-shieldingdataanswer File-** Funktion, um eine Antwortdatei (Unattend. XML-Datei) zum Erstellen von abgeschirmten VMS zu generieren, finden Sie unter [Generieren einer Antwortdatei mithilfe der New-shieldingdatabeantworungsdateifunktion](guarded-fabric-sample-unattend-xml-file.md). Mithilfe der-Funktion können Sie eine Antwortdatei, die die folgenden Optionen widerspiegelt, einfacher generieren:

- Soll der virtuelle Computer am Ende des Initialisierungs Prozesses in eine Domäne aufgenommen werden?
- Verwenden Sie eine Volumenlizenz oder eine bestimmte Product Key pro VM?
- Verwenden Sie DHCP oder eine statische IP-Adresse?
- Verwenden Sie ein benutzerdefiniertes Remotedesktopprotokoll Zertifikat (RDP), das verwendet wird, um nachzuweisen, dass der virtuelle Computer zu Ihrer Organisation gehört?
- Möchten Sie ein Skript am Ende der Initialisierung ausführen?

Antwort Dateien, die in geschützten Datendateien verwendet werden, werden auf allen virtuellen Computern verwendet, die mit dieser Schutz Datendatei erstellt werden. Daher sollten Sie sicherstellen, dass Sie keine VM-spezifischen Informationen in der Antwortdatei hart codieren. VMM unterstützt einige Ersatz Zeichenfolgen (siehe Tabelle unten) in der Datei für die unbeaufsichtigte Installation, um Spezialisierungs Werte zu verarbeiten, die sich möglicherweise von VM zu VM ändern Sie müssen diese nicht verwenden. Wenn Sie jedoch vorhanden sind, werden diese von VMM genutzt.

Beachten Sie beim Erstellen einer Datei "Unattend. xml" für abgeschirmte VMS die folgenden Einschränkungen:

- Wenn Sie VMM zum Verwalten Ihres Rechenzentrums verwenden, muss die Datei für die unbeaufsichtigte Installation nach der Konfiguration des virtuellen Computers ausgeschaltet werden. Auf diese Weise kann VMM wissen, wann dem Mandanten berichtet werden soll, dass die VM bereitgestellt wurde und einsatzbereit ist. Der virtuelle Computer wird von VMM automatisch wieder eingeschaltet, sobald erkannt wird, dass er während der Bereitstellung deaktiviert wurde.

- Stellen Sie sicher, dass Sie RDP und die entsprechende Firewallregel aktivieren, damit Sie nach der Konfiguration auf den virtuellen Computer zugreifen können. Sie können die VMM-Konsole nicht verwenden, um auf abgeschirmte VMS zuzugreifen, sodass Sie RDP benötigen, um eine Verbindung mit Ihrem virtuellen Computer herzustellen. Wenn Sie Ihre Systeme mit Windows PowerShell-Remoting verwalten möchten, müssen Sie auch sicherstellen, dass WinRM ebenfalls aktiviert ist.

- Die einzigen Ersetzungs Zeichenfolgen, die von Dateien für die unbeaufsichtigte Installation geschützter VMS unterstützt werden,

    | Ersetzbares Element | Ersatz Zeichenfolge |
    |-----------|-----------|
    | ComputerName        | @ComputerName@      |
    | Zeitzone            | @TimeZone@          |
    | ProductKey          | @ProductKey@        |
    | IPAddr4-1           | @IP4Addr-1@         |
    | IPAddr6-1           | @IP6Addr-1@         |
    | MACADDR-1           | @MACAddr-1@         |
    | Präfix-1-1          | @Prefix-1-1@        |
    | Nexthop-1-1         | @NextHop-1-1@       |
    | Präfix-1-2          | @Prefix-1-2@        |
    | Nexthop-1-2         | @NextHop-1-2@       |

    Wenn Sie über mehr als eine NIC verfügen, können Sie mehrere Ersatz Zeichenfolgen für die IP-Konfiguration hinzufügen, indem Sie die erste Ziffer erhöhen. Wenn Sie z. b. die IPv4-Adresse, das Subnetz und das Gateway für zwei NICs festlegen möchten, verwenden Sie die folgenden Ersetzungs Zeichenfolgen:

    | Ersatz Zeichenfolge | Beispiel Ersetzung |
    |---------------------|----------------------|
    | @IP4Addr-1@         | 192.168.1.10         |
    | @MACAddr-1@         | Ethernet             |
    | @Prefix-1-1@        | 192.168.1.0/24       |
    | @NextHop-1-1@       | 192.168.1.254        |
    | @IP4Addr-2@         | 10.0.20.30           |
    | @MACAddr-2@         | Ethernet 2           |
    | @Prefix-2-1@        | 10.0.20.0/24         |
    | @NextHop-2-1@       | 10.0.20.1            |

Bei der Verwendung von Ersetzungs Zeichenfolgen müssen Sie sicherstellen, dass die Zeichen folgen während des VM-Bereitstellungs Prozesses aufgefüllt werden. Wenn eine Zeichenfolge wie @ProductKey@ zum Zeitpunkt der Bereitstellung nicht angegeben wird, während der &lt;ProductKey-&gt; Knoten in der Datei für die unbeaufsichtigte Installation leer bleibt, schlägt der Spezialisierungsprozess fehl, und Sie können keine Verbindung mit dem virtuellen Computer herstellen.

Beachten Sie außerdem, dass die netzwerkbezogenen Ersetzungs Zeichenfolgen für das Ende der Tabelle nur verwendet werden, wenn Sie statische VMM-IP-Adress Pools nutzen. Ihr hostingdienstanbieter sollte Ihnen mitteilen können, ob diese Ersetzungs Zeichenfolgen erforderlich sind. Weitere Informationen zu statischen IP-Adressen in VMM-Vorlagen finden Sie in der folgenden Dokumentation in der VMM-Dokumentation:

- [Richtlinien für IP-Adress Pools](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools)
- [Einrichten von statischen IP-Adress Pools im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

Schließlich ist es wichtig zu beachten, dass bei der Bereitstellung der abgeschirmten VM nur das Betriebssystem Laufwerk verschlüsselt wird. Wenn Sie einen abgeschirmten virtuellen Computer mit einem oder mehreren Daten Laufwerken bereitstellen, wird dringend empfohlen, dass Sie einen Unattend-Befehl oder Gruppenrichtlinie Einstellung in der Mandanten Domäne hinzufügen, um die Daten Laufwerke automatisch zu verschlüsseln.

## <a name="get-the-volume-signature-catalog-file"></a>Get the Volume Signature Catalog file

Geschützte Datendateien enthalten auch Informationen zu den Vorlagen Datenträgern, denen ein Mandant vertraut. Mandanten erhalten die Datenträger Signaturen von vertrauenswürdigen Vorlagen Datenträgern in Form einer volumesignatur-Katalog Datei (VSC). Diese Signaturen werden dann überprüft, wenn ein neuer virtueller Computer bereitgestellt wird. Wenn keine der Signaturen in der Schutz Datendatei mit dem Vorlagen Datenträger, der mit dem virtuellen Computer bereitgestellt werden soll, identisch ist (d. h., er wurde geändert oder mit einem anderen, potenziell bösartigen Datenträger ausgetauscht), schlägt der Bereitstellungs Vorgang fehl.

> [!IMPORTANT]
> Während der VSC sicherstellt, dass ein Datenträger nicht manipuliert wurde, ist es weiterhin wichtig, dass der Mandant den Datenträger zunächst als vertrauenswürdig einstuft. Wenn Sie der Mandant sind und der Vorlagen Datenträger von Ihrem Host bereitgestellt wird, stellen Sie einen virtuellen Testcomputer mit diesem Vorlagen Datenträger bereit, und führen Sie eigene Tools (Antivirus, Sicherheitsrisiko Scanner usw.) aus, um zu überprüfen, ob der Datenträger tatsächlich in einem vertrauenswürdigen Zustand ist.

Es gibt zwei Möglichkeiten, den VSC eines Vorlagen Datenträgers abzurufen:

1. Der Host (oder Mandant), wenn der Mandant auf VMM zugreifen kann, verwendet die VMM-PowerShell-Cmdlets zum Speichern des VSC und übergibt ihn an den Mandanten. Dies kann auf einem beliebigen Computer ausgeführt werden, auf dem die VMM-Konsole installiert und konfiguriert ist, um die VMM-Umgebung des hostingfabrics zu verwalten. Die PowerShell-Cmdlets zum Speichern des VSC lauten wie folgt:

    ```powershell
    $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"

    $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk

    $vsc.WriteToFile(".\templateDisk.vsc")
    ```

2. Der Mandant hat Zugriff auf die Vorlagen Datenträger-Datei. Dies kann der Fall sein, wenn der Mandant einen Vorlagen Datenträger erstellt, der auf einen hostingdienstanbieter hochgeladen werden soll, oder wenn der Mandant den Vorlagen Datenträger des gehosteten In diesem Fall würde der Mandant das folgende Cmdlet ausführen (installiert mit dem Feature "abgeschirmte VM-Tools", das Teil Remoteserver-Verwaltungstools ist), ohne dass VMM in der Abbildung dargestellt wird:

    ```powershell
    Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc
    ```

## <a name="select-trusted-fabrics"></a>Vertrauenswürdige Fabrics auswählen

Die letzte Komponente in der Schutz Datendatei bezieht sich auf den Besitzer und die Wächter eines virtuellen Computers. Wächter werden verwendet, um den Besitzer einer abgeschirmten VM und die geschützten Fabrics anzugeben, auf denen Sie zur Laufzeit autorisiert ist.

Zum Autorisieren eines hostinganbieters zum Ausführen einer abgeschirmten VM müssen Sie die Überwachungs Metadaten vom Host-Überwachungsdienst des hostingdienstanbieters abrufen. Häufig stellt der hostingdienstanbieter diese Metadaten über die Verwaltungs Tools bereit. In einem Unternehmens Szenario haben Sie möglicherweise direkten Zugriff, um die Metadaten selbst abzurufen.

Sie oder Ihr hostingdienstanbieter können die Überwachungs Metadaten von HGS abrufen, indem Sie eine der folgenden Aktionen ausführen:

- Rufen Sie die Überwachungs Metadaten direkt von HGS ab, indem Sie den folgenden Windows PowerShell-Befehl ausführen, oder navigieren Sie zur Website, und speichern Sie die angezeigte XML-Datei:

    ```powershell
    Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml
    ```

- Abrufen der Überwachungs Metadaten von VMM mithilfe der VMM-PowerShell-Cmdlets:

    ```powershell
    $relecloudmetadata = Get-SCGuardianConfiguration
    $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8
    ```

Rufen Sie die Überwachungs Metadatendateien für jedes geschützte Fabric ab, für das Sie Ihre abgeschirmten VMS autorisieren möchten, bevor Sie fortfahren.

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>Erstellen einer Schutz Datendatei und Hinzufügen von Betreuern mithilfe des Assistenten zum Schützen von Datendateien

Führen Sie den Assistenten für die Schutz Datendatei aus, um eine Datei mit geschützten Daten (PDK) zu erstellen. Hier fügen Sie das RDP-Zertifikat, die Datei für die unbeaufsichtigte Installation, volumesignaturkataloge, den Besitzer Wächter und die heruntergeladenen Überwachungs Metadaten hinzu, die im vorherigen Schritt abgerufen wurden.

1. Installieren Sie mithilfe Server-Manager oder des folgenden Windows PowerShell-Befehls **Remoteserver-Verwaltungstools &gt; Feature-Verwaltungs Tools &gt; abgeschirmte VM-Tools** auf Ihrem Computer:

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

2. Öffnen Sie den Assistenten zum Schützen von Datendateien über den Abschnitt "Administrator Tools" im Startmenü, oder führen Sie die folgende ausführbare Datei " **C:\\Windows\\System32\\shieldingdatafilewizard. exe**" aus.

3. Verwenden Sie auf der ersten Seite das zweite Feld für die Auswahl von Dateien, um einen Speicherort und Dateinamen für die geschützte Datendatei auszuwählen. Normalerweise würden Sie eine geschützte Datendatei nach der Entität benennen, die virtuelle Computer besitzt, die mit den geschützten Daten (z. b. hr, IT, Finance) erstellt wurden, und die von ihr ausgestellte workloadrolle (z. b. Dateiserver, Webserver oder etwas anderes, das von der Datei für die unbeaufsichtigte Installation konfiguriert wurde). Lassen Sie das Optionsfeld auf **geschützte Daten für geschützte Vorlagen**fest.

    > [!NOTE]
    > Im Assistenten für Schutz Datendateien werden Ihnen die folgenden beiden Optionen angezeigt:
    >- **Geschützte Daten für geschützte Vorlagen**
    >- **Schutz von Daten für vorhandene VMS und nicht abgeschirmte Vorlagen**<br>
    > Die erste Option wird verwendet, wenn neue abgeschirmte VMS aus abgeschirmten Vorlagen erstellt werden. Die zweite Option ermöglicht es Ihnen, geschützte Daten zu erstellen, die nur beim Umrechnen vorhandener virtueller Computer oder beim Erstellen von abgeschirmten VMS aus nicht abgeschirmten Vorlagen verwendet werden können.

    ![Assistent zum Schützen von Datendateien, Dateiauswahl](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

    Außerdem müssen Sie auswählen, ob VMS, die mit dieser Schutz Datendatei erstellt wurden, im Modus "Verschlüsselung unterstützt" wirklich geschützt oder konfiguriert werden. Weitere Informationen zu diesen beiden Optionen finden Sie unter [Was sind die Typen von virtuellen Maschinen, die von einem geschützten Fabric ausgeführt werden können?](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run).

    > [!IMPORTANT]
    > Achten Sie sorgfältig auf den nächsten Schritt, da der Besitzer der abgeschirmten VMS und die Fabrics definiert werden, auf denen Ihre abgeschirmten VMS autorisiert sind.<br>Der Besitz des **Besitzer-Schützers** ist erforderlich, um eine vorhandene abgeschirmte VM später von **abgeschirmt** in **Verschlüsselung unterstützt** oder umgekehrt zu ändern.

4. Ihr Ziel in diesem Schritt besteht darin, das zwei fache zu erreichen:

    - Erstellen oder Auswählen eines Besitzer-Schützers, der Sie als VM-Besitzer darstellt

    - Importieren Sie den Wächter, den Sie im vorherigen Schritt aus dem (oder Ihrem eigenen) hostüberwachungs Dienst des hostinganbieters heruntergeladen haben.

    Um einen vorhandenen Besitzer Wächter festzulegen, wählen Sie im Dropdown Menü den entsprechenden Wächter aus. Nur Wächter, die auf dem lokalen Computer mit den privaten Schlüsseln installiert sind, werden in dieser Liste angezeigt. Sie können auch einen eigenen Besitzer Wächter erstellen, indem Sie in der unteren rechten Ecke **lokale Wächter verwalten** auswählen und auf **Erstellen** klicken, um den Assistenten abzuschließen.

    Als nächstes importieren wir die zuvor heruntergeladenen Wächter-Metadaten auf der Seite **Besitzer und Wächter** . Wählen Sie in der unteren rechten Ecke **lokale Wächter verwalten** aus. Verwenden Sie die **Import** Funktion, um die Datei mit den Überwachungs Metadaten zu importieren. Klicken Sie auf **OK** , nachdem Sie alle erforderlichen Wächter importiert oder eingefügt haben. Als bewährte Vorgehensweise können Sie die Wächter nach dem hostingdienstanbieter oder dem Unternehmens Rechenzentrum benennen. Wählen Sie abschließend alle Wächter aus, die die Daten Center darstellen, in denen Ihre abgeschirmte VM ausgeführt werden soll. Sie müssen den Besitzer Wächter nicht erneut auswählen. Klicken Sie **anschließend auf weiter** .

    ![Schutz Datendatei-Assistent, Besitzer und Wächter](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5. Klicken Sie auf der Seite "Volumen-ID-Qualifizierer" auf **Hinzufügen** , um einen signierten Vorlagen Datenträger in der Wenn Sie im Dialogfeld einen VSC auswählen, werden Informationen über den Namen, die Version und das Zertifikat des Datenträgers angezeigt, der zum Signieren verwendet wurde. Wiederholen Sie diesen Vorgang für jeden zu autorisierende Vorlagen Datenträger.

6. Klicken Sie auf der Seite " **Spezialisierungs Werte** " auf **Durchsuchen** , um die Datei "Unattend. xml" auszuwählen, die für die Spezialisierung ihrer VMS verwendet wird.

    Verwenden Sie die Schaltfläche **Hinzufügen** am unteren Rand, um dem PDK weitere Dateien hinzuzufügen, die während des Spezialisierungs Vorgangs benötigt werden. Wenn die Datei für die unbeaufsichtigte Installation z. b. ein RDP-Zertifikat auf dem virtuellen Computer installiert (wie unter [Generieren einer Antwortdatei mithilfe der New-shieldingdatabeantworungsfile-Funktion](guarded-fabric-sample-unattend-xml-file.md)beschrieben), sollten Sie hier die PFX-Datei des RDP-Zertifikats und das Skript "rdpcertifipteconfig. ps1" hinzufügen. Beachten Sie, dass alle Dateien, die Sie hier angeben, automatisch nach C:\\Temp\\ auf dem virtuellen Computer kopiert werden, der erstellt wird. Die Datei für die unbeaufsichtigte Installation sollte erwarten, dass sich die Dateien in diesem Ordner befinden, wenn Sie über den Pfad referenziert werden.

7. Überprüfen Sie Ihre Auswahl auf der nächsten Seite, und klicken Sie dann auf **generieren**.

8. Schließen Sie den Assistenten, nachdem er abgeschlossen wurde.

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>Erstellen einer Schutz Datendatei und Hinzufügen von Betreuern mithilfe von PowerShell

Als Alternative zum Assistenten zum Schützen von Datendateien können Sie [New-shieldingdatafile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps) ausführen, um eine geschützte Datendatei zu erstellen.

Alle Schutz Datendateien müssen mit den richtigen Besitzer-und Überwachungs Zertifikaten konfiguriert werden, damit Ihre abgeschirmten VMS auf einem geschützten Fabric ausgeführt werden können.
Durch Ausführen von [Get-hgsguardian](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsguardian?view=win10-ps)können Sie überprüfen, ob eine lokale Installation vorhanden ist. Besitzer Wächter verfügen über private Schlüssel, während Wächter für Ihr Rechenzentrum dies in der Regel nicht tun.

Wenn Sie einen Owner-Wächter erstellen müssen, führen Sie den folgenden Befehl aus:

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

Mit diesem Befehl werden ein paar Signierungs-und Verschlüsselungs Zertifikate im Zertifikat Speicher des lokalen Computers unter dem Ordner "geschützte VM local-Zertifikate" erstellt.
Sie benötigen die Besitzer Zertifikate und die zugehörigen privaten Schlüssel, um einen virtuellen Computer zu bereinigen. Stellen Sie also sicher, dass diese Zertifikate gesichert und vor Diebstahl geschützt werden.
Ein Angreifer, der Zugriff auf die Besitzer Zertifikate hat, kann ihn verwenden, um den abgeschirmten virtuellen Computer zu starten oder seine Sicherheitskonfiguration zu ändern.

Wenn Sie Überwachungsinformationen aus einem geschützten Fabric importieren müssen, auf dem Sie den virtuellen Computer (Ihr primäres Daten Center, Sicherungs Datacenter usw.) ausführen möchten, führen Sie den folgenden Befehl für jede [Metadatendatei aus, die von ihren geschützten Fabrics abgerufen](#select-trusted-fabrics)wird.

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> Wenn Sie selbst signierte Zertifikate verwendet haben oder die Zertifikate, die bei HGS registriert sind, abgelaufen sind, müssen Sie möglicherweise die `-AllowUntrustedRoot`-und/oder `-AllowExpired`-Flags mit dem Befehl "Import-hgsguardian" verwenden, um die Sicherheitsüberprüfungen zu umgehen.

Sie müssen auch [einen volumesignaturkatalog](#get-the-volume-signature-catalog-file) für jeden Vorlagen Datenträger abrufen, den Sie mit dieser Schutz Datendatei verwenden möchten, und eine [Antwortdatei](#create-an-answer-file) für die Schutz Daten, damit das Betriebssystem seine Spezialisierungs Aufgaben automatisch ausführen kann.
Entscheiden Sie abschließend, ob Sie möchten, dass Ihr virtueller Computer vollständig abgeschirmt oder nur vtpm aktiviert ist.
Verwenden Sie `-Policy Shielded` für eine vollständig abgeschirmte VM oder `-Policy EncryptionSupported` für eine vtpm-aktivierte VM, die einfache Konsolen Verbindungen und PowerShell Direct zulässt.

Nachdem Sie alles vorbereitet haben, führen Sie den folgenden Befehl aus, um die geschützte Datendatei zu erstellen:

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

> [!TIP]
> Wenn Sie ein benutzerdefiniertes RDP-Zertifikat, SSH-Schlüssel oder andere Dateien verwenden, die in die geschützte Datendatei eingeschlossen werden müssen, verwenden Sie den `-OtherFile`-Parameter, um diese einzuschließen. Sie können eine durch Trennzeichen getrennte Liste mit Dateipfaden angeben, z. b. `-OtherFile "C:\source\myRDPCert.pfx", "C:\source\RDPCertificateConfig.ps1"`

Im obigen Befehl kann der Wächter mit dem Namen "Owner" (abgerufen von Get-hgsguardian) die Sicherheitskonfiguration des virtuellen Computers in Zukunft ändern, während "East-US Datacenter" den virtuellen Computer ausführen, aber seine Einstellungen nicht ändern kann.
Wenn Sie über mehr als einen Wächter verfügen, trennen Sie die Namen der Wächter durch Kommas wie `'EAST-US Datacenter', 'EMEA Datacenter'`.
Der Lautstärke-ID-Qualifizierer gibt an, ob Sie nur der exakten Version (gleich) des Vorlagen Datenträgers oder zukünftigen Versionen (greaterthanorgleich) Vertrauen.
Der Datenträger Name und das Signaturzertifikat müssen exakt mit dem Versionsvergleich übereinstimmen, der zum Zeitpunkt der Bereitstellung berücksichtigt wird.
Sie können mehr als einem Vorlagen Datenträger Vertrauen, indem Sie eine durch Trennzeichen getrennte Liste mit Volumen-ID-Qualifizierern für den `-VolumeIDQualifier`-Parameter
Wenn Sie weitere Dateien haben, die die Antwortdatei mit dem virtuellen Computer begleiten müssen, verwenden Sie den `-OtherFile`-Parameter, und geben Sie eine durch Trennzeichen getrennte Liste mit Dateipfaden an.

Weitere Informationen zu weiteren Möglichkeiten zum Konfigurieren ihrer geschützten Datendatei finden Sie in der Cmdlet-Dokumentation für [New-shieldingdatafile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps) und [New-volumeidqualifizierer](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps) .

## <a name="see-also"></a>Weitere Informationen

- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
