---
title: Abgeschirmte virtuelle Computer für Mandanten - geschützte Daten erstellen, um eine geschützte VM zu definieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 1245b88a42b80218b5557dc89f2b97b5d0059d44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852541"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>Abgeschirmte virtuelle Computer für Mandanten - geschützte Daten erstellen, um eine geschützte VM zu definieren.

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Eine geschützte Datendatei (auch als Bereitstellungsdatendatei oder PDK-Datei bezeichnet) ist eine verschlüsselte Datei, die ein Mandant oder VM-Besitzer erstellt, um wichtige VM-Konfigurationsinformationen, z.B. Administratorkennwort, RDP und andere identitätsbezogene Zertifikate, Domänenbeitritts-Anmeldeinformationen usw. zu schützen. Dieses Thema enthält Informationen dazu, wie Sie eine geschützte Datendatei zu erstellen. Bevor Sie die Datei erstellen können, Sie müssen Ihre hosting-Anbieter einen vorlagendatenträger entnommen oder erstellen Sie einen vorlagendatenträger, wie im [abgeschirmter VMs für Mandanten – erstellen einen vorlagendatenträger (optional)](guarded-fabric-tenant-creates-template-disk.md).

Eine Liste und ein Diagramm des Inhalts der schutzdatendatei, finden Sie unter [welche Daten Schutz ist und warum dies erforderlich ist?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

> [!IMPORTANT]
> Die Schritte in diesem Abschnitt sollte auf eine Mandanten-VM unter Windows Server 2016 ausgeführt werden. Dieser Computer muss nicht Teil eines geschützten Fabrics (d. h., Sie sollte nicht zur Verwendung eines Host-Überwachungsdienst-Clusters konfiguriert werden).

Zur Vorbereitung auf eine geschützte Datendatei zu erstellen, gehen Sie folgendermaßen vor:

- [Abrufen eines Zertifikats für die Remotedesktopverbindung](#obtain-a-certificate-for-remote-desktop-connection)
- [Erstellen einer Antwortdatei](#create-an-answer-file)
- [Rufen Sie die Volume-Signatur-Katalog-Datei](#get-the-volume-signature-catalog-file)
- [Wählen Sie die vertrauenswürdigen fabrics](#select-trusted-fabrics)

Anschließend können Sie die schutzdatendatei erstellen:

- [Erstellen Sie eine schutzdatendatei und Hinzufügen von Überwachungen](#create-a-shielding-data-file-and-add-guardians)


## <a name="obtain-a-certificate-for-remote-desktop-connection"></a>Abrufen eines Zertifikats für die Remotedesktopverbindung

Da Mandanten nur für die Verbindung mit ihren abgeschirmte VMs über Remotedesktopverbindung oder andere Remoteverwaltungstools können, ist es wichtig sicherzustellen, dass Mandanten überprüfen können sie eine Verbindung mit dem richtigen Endpunkt (das heißt, es ist keinem "Man in the Middle" Abfangen von der Verbindungs).

Eine Möglichkeit, um sicherzustellen, dass Sie mit dem gewünschten Server verbinden, ist zum Installieren und Konfigurieren eines Zertifikats für Remote Desktop Services, um anzuzeigen, wenn Sie eine Verbindung initiieren. Client-Computer mit dem Server überprüft, ob sie das Zertifikat und das Anzeigen einer Warnung vertraut, wenn dies nicht der Fall. Um sicherzustellen, dass der verbindende Client dem Zertifikat vertraut, werden im Allgemeinen die RDP-Zertifikate von des Mandanten PKI ausgegeben. Weitere Informationen zu [Verwenden von Zertifikaten in Remote Desktop Services](https://technet.microsoft.com/library/dn781533.aspx) finden Sie auf TechNet.

<!-- The previous link comes from Windows 2012 R2 content, but as of Sept 2016, there isn't a more recent link that covers the same information. -->

> [!NOTE]
> Wenn Sie eine RDP-Zertifikat in der geschützten Datendatei aufgenommen auswählen möchten, achten Sie darauf, dass Sie ein Platzhalterzertifikat verwenden. Eine geschützte Datendatei kann verwendet werden, um eine unbegrenzte Anzahl von VMs zu erstellen. Da jeder virtuelle Computer das gleiche Zertifikat freigibt, gewährleistet ein Platzhalterzertifikat, dass das Zertifikat gültig ist, unabhängig von der Hostname der VM sein wird.

Wenn Sie abgeschirmte VMs bewerten und nicht noch bereit, um von Ihrer Zertifizierungsstelle ein Zertifikat anzufordern, ein selbstsigniertes Zertifikat auf dem mandantencomputer durch den folgenden Windows PowerShell-Befehl ausführen können (wobei *"contoso.com"*  des Mandanten-Domäne ist):

``` powershell
$rdpCertificate = New-SelfSignedCertificate -DnsName '\*.contoso.com'
$password = ConvertTo-SecureString -AsPlainText 'Password1' -Force
Export-PfxCertificate -Cert $RdpCertificate -FilePath .\rdpCert.pfx -Password $password
```

## <a name="create-an-answer-file"></a>Erstellen einer Antwortdatei

Da in VMM der signierten vorlagendatenträger generalisiert wurde, müssen Mandanten zu einer Antwortdatei an, um geschützten virtuelle Maschinen während der Bereitstellung zu spezialisieren. Die Antwortdatei (oft als "die Datei für die unbeaufsichtigte Installation" bezeichnet) kann den virtuellen Computer für die vorgesehene Rolle konfigurieren – d.h. können Installieren von Windows-Funktionen, registrieren Sie die RDP-Zertifikat, das im vorherigen Schritt erstellt haben und andere benutzerdefinierte Aktionen auszuführen. Es wird auch die erforderlichen Informationen für Windows Setup, einschließlich der Standardadministrator-Kennwort und den Product Key angeben.

Informationen zum Abrufen und Verwenden der **New-ShieldingDataAnswerFile** Funktion zum Generieren einer Antwortdatei (Unattend.xml-Datei) zum Erstellen von abgeschirmten VMs, finden Sie unter [Generieren einer Antwortdatei mit den Neue ShieldingDataAnswerFile Funktion](guarded-fabric-sample-unattend-xml-file.md). Mit der Funktion können Sie leichter eine Antwortdatei generieren, die Auswahloptionen, darunter die folgenden wiedergibt:

- Werden der virtuelle Computer ist mit der Domäne beigetreten, am Ende der Initialisierungsprozess vorgesehen?
- Verwenden eine Volumenlizenz oder ein bestimmter Product Key pro VM Sie?
- Verwenden Sie DHCP oder statischen IP-Adresse?
- Verwenden Sie ein Zertifikat für die Remote Desktop Protocol (RDP), die verwendet wird, um nachzuweisen, dass der virtuelle Computer in Ihrer Organisation gehört?
- Möchten Sie ein Skript am Ende der Initialisierung ausführen?
- Verwenden Sie einen Server Desired State Configuration (DSC) für die weitere Konfiguration?

Antwortdateien verwendet schutzdatendateien werden auf jedem virtuellen Computer erstellt, mit der geschützten Datendatei verwendet. Aus diesem Grund sollten Sie sicherstellen, dass Sie alle VM-spezifische Informationen in der Antwortdatei nicht hart codieren. VMM unterstützt einige Ersatzzeichenfolgen (siehe die folgende Tabelle) in der Datei für die unbeaufsichtigte Installation Spezialisierung Werte behandelt werden, die von virtuellen Computer zum virtuellen Computer ändern kann. Sie sind nicht erforderlich, um diese zu verwenden; jedoch wenn sie vorhanden sind wird VMM diese nutzen.

Wenn Sie eine Datei "Unattend.xml" für abgeschirmte VMs erstellen möchten, beachten Sie die folgenden Einschränkungen:

-   Die Datei für die unbeaufsichtigte Installation muss das Ergebnis auf dem virtuellen Computer wird ausgeschaltet, nachdem es konfiguriert wurde. Dies ist zu wissen, wenn es in den Mandanten melden soll, dass der virtuelle Computer bereitgestellt vollständig und bereit für die Verwendung ist von VMM. VMM wird automatisch den virtuellen Computer wieder einschalten, wenn erkannt wird, dass es während der Bereitstellung deaktiviert wurde.

-   Es wird dringend empfohlen, ein RDP-Zertifikat, um sicherzustellen, dass Sie die VM nach rechts und nicht einem anderen Computer, die für einen Man-in-the-Middle-Angriff konfiguriert verbinden zu konfigurieren.

-   Achten Sie darauf, dass Sie RDP und den entsprechenden Firewall-Regel zu aktivieren, damit Sie den virtuellen Computer zugreifen können, nachdem es konfiguriert wurde. Können keine VMM-Konsole zugreifen, die abgeschirmte VMs, damit Sie RDP für die Verbindung mit Ihrem virtuellen Computer benötigen. Falls, zum Verwalten Ihrer Systeme mit Windows PowerShell-Remoting gewünscht, stellen Sie sicher, dass WinRM aktiviert ist, zu.

-   Die einzige Ersatzzeichenfolgen in abgeschirmte VM-Dateien für die unbeaufsichtigte Installation unterstützt, sind die folgenden:

| Ersetzbare-Element | -Ersatzzeichenfolge |
|-----------|-----------|
| ComputerName        | @ComputerName@      |
| TimeZone            | @TimeZone@          |
| ProductKey          | @ProductKey@        |
| IPAddr4-1           | @IP4Addr-1@         |
| IPAddr6-1           | @IP6Addr-1@         |
| MACAddr-1           | @MACAddr-1@         |
| Prefix-1-1          | @Prefix-1-1@        |
| NextHop-1-1         | @NextHop-1-1@       |
| Prefix-1-2          | @Prefix-1-2@        |
| NextHop-1-2         | @NextHop-1-2@       |

Wenn Sie Ersatzzeichenfolgen verwenden zu können, ist es wichtig, um sicherzustellen, dass die Zeichenfolgen bei der die VM-Bereitstellung aufgefüllt werden. Wenn die Zeichenfolge wie z. B. @ProductKey@ nicht angegeben wird zum Zeitpunkt der Bereitstellung, sodass die &lt;ProductKey&gt; Knoten in die leere Datei für die unbeaufsichtigte, der Spezialisierung Vorgang schlägt fehl, und Sie kann keine Verbindung mit Ihrem virtuellen Computer herstellen.

Beachten Sie, dass nur netzwerkbezogene Ersatzzeichenfolgen am Ende der Tabelle verwendet werden, wenn Sie VMM statische IP-Adresspools nutzen. Ihre hosting-Anbieter sollte in der Lage, Ihnen mitteilen, ob diese Ersatzzeichenfolgen erforderlich sind. Weitere Informationen zu statischen IP-Adressen in VMM-Vorlagen finden Sie in der Dokumentation zu VMM die folgenden:

- [Richtlinien für die IP-Adresspools](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools) 
- [Statische IP-Adresspools im VMM-Fabric einrichten](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

Abschließend ist es wichtig zu beachten, dass der abgeschirmte VM-Bereitstellungsprozess nur das Betriebssystemlaufwerk verschlüsselt wird. Wenn Sie eine abgeschirmte VM mit der eine oder mehrere Datenträger für Daten bereitstellen, wird dringend empfohlen, dass Sie in die mandantendomäne, um die Laufwerke automatisch zu verschlüsseln eines Unattend-Befehl oder einer Gruppenrichtlinien-Einstellung hinzufügen.

## <a name="get-the-volume-signature-catalog-file"></a>Rufen Sie die Volume-Signatur-Katalog-Datei

Geschützte Datendateien enthalten auch Informationen zu den vorlagedatenträgern, dass ein Mandant als vertrauenswürdig eingestuft. Mandanten abrufen, die Datenträgersignaturen aus vertrauenswürdigen vorlagedatenträger in Form von einem Volume Signatur-Katalogdatei (VSC). Diese Signaturen überprüft dann, wenn ein neuer virtueller Computer bereitgestellt wird. Keine der Signaturen in der schutzdatendatei auf den vorlagendatenträger entspricht schlägt beim Versuch, mit dem virtuellen Computer (d.h., es wurde geändert oder ausgetauscht werden, mit einem anderen, potenziell böswilligen Datenträger) bereitgestellt werden, im Rahmen des Bereitstellungsprozesses fehl.

> [!IMPORTANT]
> Während dem VSC bzw. wird sichergestellt, dass ein Datenträger nicht manipuliert wurde, ist es dennoch wichtig für den Mandanten, den Datenträger im vornherein zu vertrauen. Wenn Sie den Mandanten und der vorlagendatenträger erfolgt über Ihr Hoster, stellen einen Test-VM, die mit dieser vorlagendatenträger, und führen Sie Ihre eigenen Tools (Antivirus, Überprüfung auf Sicherheitsrisiken und So weiter), um zu überprüfen, ob den Datenträger befindet, in der Tat in einem Zustand, den Sie vertrauen.

Es gibt zwei Möglichkeiten, dem VSC bzw. der einen vorlagendatenträger abzurufen:

-  Der Hoster (oder der Mandant besitzt Zugriff auf VMM-Mandanten) der VMM-PowerShell-Cmdlets verwendet, um dem VSC bzw. zu speichern, und gibt es für dem Mandanten. Dies kann auf jedem Computer mit der VMM-Konsole installiert und konfiguriert für die Verwaltung der hosting-Fabric VMM-Umgebung durchgeführt werden. Die PowerShell-Cmdlets, dem VSC bzw. gespeichert sind:

        $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"
    
        $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk
    
        $vsc.WriteToFile(".\templateDisk.vsc")

-  Der Mandant hat Zugriff auf die Datenträger-Vorlagendatei. Dies kann der Fall sein, wenn der Mandant einen vorlagendatenträger, die hochgeladen werden, um hosting-Anbieter erstellt oder der Mandant des Hosters vorlagendatenträger herunterladen kann. In diesem Fall würden ohne VMM in der Abbildung, die Mandanten mit dem folgende Cmdlet (mit der Funktion Tools für geschützte VMs Teil der Remoteserver-Verwaltungstools installiert) ausführen:

        Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc

## <a name="select-trusted-fabrics"></a>Wählen Sie die vertrauenswürdigen fabrics

Die letzte Komponente in der schutzdatendatei bezieht sich auf den Besitzer und Überwachungen eines virtuellen Computers. Überwachungen werden verwendet, um zu bestimmen sowohl den Besitzer der einer abgeschirmten VM und die geschützten Fabrics, die auf denen sie zur Ausführung berechtigt ist.

Um ein hosting Fabric zum Ausführen einer abgeschirmten VMs zu autorisieren, müssen Sie der überwachungsmetadaten aus der hosting-Anbieter des Host-Überwachungsdienst abrufen. Häufig stellt Ihnen der hosting-Anbieter mit diesen Metadaten über ihre Verwaltungstools bereit. In einem Unternehmensszenario möglicherweise Sie direkten Zugriff auf die Metadaten selbst abzurufen.

Sie oder Ihre hosting-Anbieter kann der überwachungsmetadaten aus der Host-Überwachungsdienst abrufen, indem Sie eine der folgenden Aktionen ausführen:

-  Rufen Sie der überwachungsmetadaten direkt vom Host-Überwachungsdienst, indem Sie den folgenden Windows PowerShell-Befehl ausführen, oder Sie zur Website navigieren, und speichern die XML-Datei, die angezeigt wird:

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

-  Abrufen der überwachungsmetadaten aus VMM mithilfe der VMM-PowerShell-Cmdlets:

        $relecloudmetadata = Get-SCGuardianConfiguration

        $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8

<!-- Note that the VMM PowerShell cmdlets aren't Windows PowerShell, so "VMM PowerShell" is the correct terminology for them. -->

Abrufen der Überwachungsdienst Metadaten-Dateien für jeden geschützten Fabrics, die Sie autorisieren Sie die abgeschirmten VMs ausgeführt bevor Sie fortfahren möchten.

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>Erstellen Sie eine schutzdatendatei und Hinzufügen von Überwachungen mit dem Assistenten für die Schutzdatendatei

Führen Sie die Schutzdatendatei-Assistenten, um eine geschützte Datendatei (PDK) zu erstellen. Hier wird Sie die RDP-Zertifikat hinzufügen, unattend-Datei, Volume-Signatur-Kataloge, Besitzer-Überwachungsdienst und der heruntergeladenen überwachungsmetadaten, die im vorherigen Schritt abgerufen haben.

1.  Installieren Sie **Remoteserver-Verwaltungstools &gt; Featureverwaltungstools &gt; Tools für geschützte VMs** auf Ihrem Computer mithilfe von Server-Manager oder den folgenden Windows PowerShell-Befehl:

        Install-WindowsFeature RSAT-Shielded-VM-Tools

2.  Öffnen Sie den Assistenten für geschützte Datendateien im Abschnitt "Verwaltung" im Startmenü oder durch die folgende ausführbare Datei ausführen **C:\\Windows\\"System32"\\ShieldingDataFileWizard.exe**.

3.  Verwenden Sie auf der ersten Seite die zweite Datei Auswahlfeld, um einen Speicherort und Namen für die schutzdatendatei auswählen. Normalerweise nennen Sie eine schutzdatendatei nach dem Erstellen die Entität, keine virtuellen Computer besitzt, mit den geschützten Daten (z.B. HR, IT, Finanzen) und die Rolle "arbeitsauslastung", die er ausgeführt wird, (z. B., Dateiserver, Webserver oder sonstige konfiguriert, indem die Datei für die unbeaufsichtigte Installation). Lassen Sie das Optionsfeld aus, legen Sie auf **Schutzdaten für abgeschirmte Vorlagen**.

    > [!NOTE]
    > In den Assistenten für geschützte Datendateien sehen Sie die folgenden beiden Optionen:
    >- **Schutzdaten für abgeschirmte Vorlagen**
    >- **Geschützte Daten für vorhandene virtuelle Computer und Vorlagen nicht geschützte**<br>
    > Die erste Option wird verwendet, wenn es sich bei Erstellen von neuen abgeschirmten VMs aus geschützten Vorlagen. Die zweite Option können Sie geschützte Daten zu erstellen, die beim Konvertieren vorhandener VMs oder das Erstellen von Vorlagen nicht geschützte von VMs abgeschirmten nur verwendet werden können.

    ![Schutz von Daten mit dem Assistenten, der Dateiauswahl](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

       Darüber hinaus müssen Sie auswählen, ob der virtuelle Computer erstellt mithilfe dieser schutzdatendatei wirklich geschützt oder wird im Modus "Verschlüsselung unterstützt" konfiguriert. Weitere Informationen zu diesen beiden Optionen finden Sie unter [gibt die Typen von virtuellen Maschinen, die ein geschütztes Fabric ausführen können?](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run).

    > [!IMPORTANT]
    > Achten Sie mit dem nächsten Schritt definiert werden, den Besitzer Ihre abgeschirmter VMs sowie die Fabrics, die die abgeschirmten VMs werden für die Ausführung auf autorisiert werden.<br>Besitz des **Besitzer Überwachungsdienst** ist erforderlich, um einem vorhandenen geschützten virtuellen Computer aus einem späteren Zeitpunkt ändern **abgeschirmte** zu **Verschlüsselung unterstützt** oder umgekehrt.
    
4.  Ihr Ziel in diesem Schritt umfasst zwei Stufen:

    - Erstellen Sie oder wählen Sie ein Besitzer eines Erziehungsberechtigten, die Sie als Besitzer der VM darstellt

    - Importieren Sie die Überwachung, die Sie aus der hosting-Anbieter heruntergeladen (oder Ihre eigenen) Host-Überwachungsdienst im vorherigen Schritt

    Um einen vorhandenen Besitzer Wächter festzulegen, wählen Sie den entsprechenden Überwachungsdienst aus dem Dropdownmenü aus. In dieser Liste werden nur die Überwachungen auf dem lokalen Computer installiert werden, mit dem privaten Schlüssel intakt angezeigt. Sie können auch Ihren eigenen Überwachungsdienst Besitzer erstellen, indem Sie auswählen **Verwalten lokaler Guardians** in der unteren rechten Ecke, und klicken auf **erstellen** und Abschließen des Assistenten.

    Als Nächstes importieren wir die zuvor heruntergeladene überwachungsmetadaten erneut mit der **Besitzer und Überwachungen** Seite. Wählen Sie **Verwalten lokaler Guardians** aus der unteren rechten Ecke. Verwenden der **importieren** Feature der Überwachungsdienst-Metadatendatei zu importieren. Klicken Sie auf **OK** , nachdem Sie nicht importiert haben, oder alle der erforderlichen Überwachungen hinzugefügt. Benennen Sie als bewährte Methode Guardians nach des hostenden Dienst Anbieter bzw. unternehmensrechenzentrums, die sie darstellen. Wählen Sie abschließend alle Überwachungen, die die Datencentern darstellen, in denen Ihre abgeschirmte VM zur Ausführung berechtigt ist. Sie müssen nicht erneut auswählen, der Besitzer eines Erziehungsberechtigten. Klicken Sie auf **Weiter** wenn fertig gestellt.

    ![Schutz von Daten mit dem Assistenten "," Besitzer "und" Überwachungen](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5.  Klicken Sie auf der Seite Volume-ID-Qualifizierer auf **hinzufügen** einen signierten vorlagendatenträger in der geschützten Datendatei zu autorisieren. Wenn Sie eine VSC im Dialogfeld auswählen, wird Sie angezeigt Informationen zu den Namen des Laufwerks, Version und das Zertifikat, das zum Signieren verwendet wurde. Wiederholen Sie diesen Vorgang für jede vorlagendatenträger, die Sie autorisieren möchten.

6.  Auf der **Spezialisierung Werte** auf **Durchsuchen** Ihrer Datei "Unattend.xml" auswählen, das verwendet wird, um Ihre virtuellen Computer anzugeben.

    Verwenden der **hinzufügen** Schaltfläche am unteren Rand des PDK, die bei der Spezialisierung erforderlich sind, weiteren Dateien hinzugefügt. Angenommen, die für die unbeaufsichtigte Datei eine RDP-Zertifikat auf den virtuellen Computer installiert wird (siehe [Generieren einer Antwortdatei mithilfe der Funktion New-ShieldingDataAnswerFile](guarded-fabric-sample-unattend-xml-file.md)), sollten Sie die Datei RDPCert.pfx Hinzufügen der Unattend-Datei. Beachten Sie, die hier angegebenen Dateien automatisch in "c:" kopiert werden\\Temp\\ auf dem virtuellen Computer, die erstellt wird. Die Datei für die unbeaufsichtigte Installation erwarten, dass die Dateien in diesem Ordner werden, wenn sie anhand des Pfads zu verweisen.

7.  Überprüfen Sie Ihre Auswahl auf der nächsten Seite, und klicken Sie dann auf **generieren**.

8.  Schließen Sie den Assistenten aus, nachdem es abgeschlossen wurde.

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>Erstellen Sie eine schutzdatendatei und Hinzufügen von Überwachungen, die mithilfe von PowerShell

Sie können als Alternative zum Schutzdatendatei-Assistenten ausführen [New-ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps) um eine geschützte Datendatei zu erstellen.

Alle geschützten Datendateien müssen mit dem richtigen Besitzer und den Überwachungsdienst Zertifikate, die abgeschirmten VMs für die Ausführung auf einem geschützten Fabric autorisiert konfiguriert werden.
Sie können überprüfen, ob Sie alle Überwachungen, die lokal mit installiert haben [Get-HgsGuardian](https://docs.microsoft.com/en-us/powershell/module/hgsclient/get-hgsguardian?view=win10-ps). Besitzer Guardians aufweisen private Schlüssel, während Überwachungen für Ihr Rechenzentrum in der Regel nicht der Fall ist.

Wenn Sie ein Besitzer Überwachungsdienst erstellen möchten, führen Sie den folgenden Befehl aus:

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

Dieser Befehl erstellt ein Paar von Signatur-und Verschlüsselungszertifikate im Zertifikatspeicher des lokalen Computers, unter dem Ordner "Abgeschirmte VM lokalen Zertifikate".
Sie benötigen, die besitzerzertifikate und ihre dazugehörigen privaten Schlüssel auf unshield eines virtuellen Computers stellen Sie daher sicher, diese Zertifikate gesichert und vor Diebstahl geschützt.
Ein Angreifer Zugriff auf die besitzerzertifikate können sie Ihre geschützte virtuelle Maschine starten, oder ändern die Sicherheitskonfiguration.

Falls also Überwachungsdienst-Informationen aus einem geschützten Fabric importieren, in dem Ihre VM (Ihre primären Datencenter, Sicherung Rechenzentren, usw.), führen den folgenden Befehl für jede ausgeführt werden soll [Metadatendatei abgerufen werden, von Ihr geschützten Fabrics ](#Select-trusted-fabrics).

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> Wenn Sie selbstsignierte Zertifikate oder Zertifikate registriert-Host-Überwachungsdienst abgelaufen sind, müssen Sie möglicherweise verwenden Sie die `-AllowUntrustedRoot` und/oder `-AllowExpired` Flags mit dem Befehl "Import-HgsGuardian", die sicherheitsüberprüfungen zu umgehen.

Sie müssen auch [erhalten Sie ein Volume-signaturkatalogs](#Get-the-volume-signature-catalog-file) für jeden vorlagendatenträger, die Sie mit diesem schutzdatendatei verwenden möchten und eine [Antwort schutzdatendatei](#Create-an-answer-file) das Betriebssystem ausführen kann seine Spezialisierung Aufgaben automatisch.
Zum Schluss entscheiden Sie, ob Ihr virtueller Computer vollständig abgeschirmt "oder" nur vTPM-fähiger.
Verwendung `-Policy Shielded` für eine vollständig geschützte VM oder `-Policy EncryptionSupported` für eine vTPM VM, die einfachen Konsolen-Verbindungen zulässt und PowerShell Direct aktiviert.

Wenn alles bereit ist, führen Sie den folgenden Befehl zum Erstellen der geschützten Datendatei:

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

Im obigen Befehl werden der Überwachungsdienst, mit dem Namen "Owner" (aus Get-HgsGuardian abgerufen) in Zukunft die Sicherheitskonfiguration des virtuellen Computers zu ändern, während "EAST-US-Rechenzentrum" führen Sie den virtuellen Computer jedoch nicht die Einstellungen ändern können.
Wenn Sie mehr als ein Überwachungsdienst verfügen, separate die Namen der Überwachungen mit Kommas gefallen `'EAST-US Datacenter', 'EMEA Datacenter'`.
Die Volume-ID-Qualifizierer gibt an, ob Sie nur die genaue Version (gleich), der den vorlagendatenträger oder höheren Versionen (GreaterThanOrEquals) sowie vertrauen.
Der Name des Datenträgers und das Signaturzertifikat müssen genau für den Versionsvergleich zum Zeitpunkt der Bereitstellung als übereinstimmen.
Sie können mehrere vorlagendatenträger vertrauen, durch die Bereitstellung einer durch Trennzeichen getrennte Liste von Volume-ID-Qualifizierer auf den `-VolumeIDQualifier` Parameter.
Wenn Sie andere haben Dateien schließlich begleitet die Antwortdatei mit dem virtuellen Computer verwenden, müssen die `-OtherFile` Parameter und geben Sie eine durch Trennzeichen getrennte Liste von Dateipfaden.

Finden Sie in der Cmdlet-Dokumentation für [New-ShieldingDataFile](https://docs.microsoft.com/en-us/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps) und [New-VolumeIDQualifier](https://docs.microsoft.com/en-us/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps) Informationen zu weiteren Möglichkeiten zum Konfigurieren der geschützten Datendatei.

## <a name="see-also"></a>Siehe auch

- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
