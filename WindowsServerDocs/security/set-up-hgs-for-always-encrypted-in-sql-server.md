---
title: Einrichten des Host-Überwachungs Diensts für Always Encrypted in SQL Server
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 5d1396f609a425adcd87a41d3469f3aa55774851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402256"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>Einrichten des Host-Überwachungs Diensts für Always Encrypted mit sicheren Enklaven in SQL Server 

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, SQL Server 2019 Preview
 
[Always Encrypted mit sicheren Enklaven](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves) in SQL Server 2019 Preview ist ein Feature, das dazu dient, vertrauliche Berechnungen für vertrauliche Daten zu ermöglichen, die in einer Datenbank gespeichert sind. Der Host-Überwachungsdienst (Host Guardian Service, HGS) spielt eine wichtige Rolle bei der Sicherheit Ihrer Daten, wenn eine für Always Encrypted konfigurierte sichere Enclave eine virtualisierungsbasierte Sicherheits-und Speicher Enclave (VSB) ist. Die Sicherheit einer VSB-Speicher Enclave hängt von der Sicherheit des Windows-Hypervisors und, allgemeiner, von der Sicherheit des Computers ab, auf dem SQL Server gehostet wird. 

Bevor eine Datenbank-Client Anwendung die VSB-Arbeitsspeicher Enclave zulässt, die für Always Encrypted verwendet wurde, um Berechnungen für sensible Daten auszuführen, muss die Anwendung daher eine vertrauenswürdige HGS bestätigen. Der Nachweis bestätigt, dass der Computer, der SQL Server enthält, der die Enclave enthält, den richtigen Status aufweist und als vertrauenswürdig eingestuft werden kann. Im weiteren Verlauf dieses Themas bezeichnen wir den Computer, der die SQL Server hostet, wie den Host Computer.

Es gibt zwei, sich gegenseitig ausschließende Verfahren für die Anwendung: 

- Der Host Schlüssel Nachweis autorisiert einen Host, indem er bestätigt, dass er über einen bekannten und vertrauenswürdigen privaten Schlüssel verfügt. Der Host Schlüssel Nachweis und entweder ein physischer Host Computer oder ein virtueller Computer der Generation 2, auf SQL Server ausgeführt wird, wird für Präproduktionsumgebungen empfohlen.
- Der TPM-Nachweis überprüft Hardware Messungen, um sicherzustellen, dass auf einem Host nur die korrekten Binärdateien und Sicherheitsrichtlinien ausgeführt werden. Der TPM-Nachweis und ein physischer Host Computer (kein virtueller Computer), auf dem SQL Server ausgeführt wird, werden für Produktionsumgebungen empfohlen.

Weitere Informationen über den Host-Überwachungsdienst und dessen Measure finden Sie unter [Übersicht über geschützte Fabric und abgeschirmte VMS](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms). Beachten Sie, dass in den Dokumenten zu abgeschirmten VMS auch die gleichen Schutz-, Architektur-und bewährten Methoden für SQL Server Always Encrypted mit VSB-Enklaven gelten. 

Dieser Artikel unterstützt Sie beim Einrichten von HGS in einer empfohlenen Konfiguration. 

## <a name="prerequisites"></a>Erforderliche Komponenten 

In diesem Abschnitt werden die Voraussetzungen für HGS und Host Computer behandelt. 

### <a name="hgs-servers"></a>HGS-Server

- 1-3-Server zum Ausführen von HGS. 

  > [!NOTE]
  > Für eine Test-oder Präproduktionsumgebung ist nur ein HGS-Server erforderlich.

  Diese Server sollten sorgfältig geschützt werden, da Sie steuern, welche Computer Ihre SQL Server Instanzen mithilfe Always Encrypted mit sicheren Enklaven ausführen können. 
  Es wird empfohlen, dass verschiedene Administratoren den HGS-Cluster verwalten und die HGS auf physischer Hardware ausführen, die von der restlichen Infrastruktur oder in separaten virtualisierungsfabrics oder Azure-Abonnements isoliert ist.

  - Windows Server 2019 Standard oder Datacenter Edition.
  - 2 CPUs
  - 8 GB RAM
  - 100 GB Speicher

  Sie können entweder den [langfristigen Wartungs Kanal (Long-Term Service Channel, LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) oder den [halbjährlichen Kanal](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)verwenden. 
  Informationen zum Registrieren und Herunterladen der Windows Server Insider-Vorschau finden Sie unter [Getting Started with the Windows Insider Program](https://insider.windows.com/for-business-getting-started-server/).

- Wählen Sie einen Namen für die neue Active Directory-Gesamtstruktur aus, die vom Host-Überwachungsdienst erstellt wurde. 
  HGS sollten nicht mit Ihrer vorhandenen Unternehmens Domäne verknüpft werden und sollten über separate Administratoren verfügen, die Sie verwalten.   

- Firewall-und Routing Regeln zum Zulassen von eingehendem http-(TCP 80) oder HTTPS-Datenverkehr (TCP 443) auf den Host-Überwachungsdienst Knoten von: 

  - Computer, auf denen ausgeführt wird SQL Server
  - Die Computer, auf denen Daten Bank Client Anwendungen (z. b. Webserver) ausgeführt werden, die Datenbankabfragen ausgeben und Always Encrypted mit sicheren Enklaven verwenden. 

### <a name="sql-server-host-machines"></a>SQL Server Host Computer

- Die SQL Server Instanz sollte auf einem Computer ausgeführt werden, der die folgenden Anforderungen erfüllt:

  - Windows: 
    - Windows 10 Enterprise, Version 1809  
    - Windows Server 2019 Datacenter (halbjährlicher Kanal), Version 1809
    - Windows Server 2019 Datacenter
  - Physischer Computer für die Produktion oder ein virtueller Computer der Generation 2 zu Testzwecken (Beachten Sie, dass Azure VMS der Generation 2 nicht unterstützt)
  - Allgemeine Anforderungen, die unter [Hardware-und Software Anforderungen für die Installation von SQL Server](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017)aufgeführt sind.   

  Sie können entweder den [langfristigen Wartungs Kanal (Long-Term Service Channel, LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) oder den [halbjährlichen Kanal](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)verwenden. 
  Informationen zum Registrieren und Herunterladen der Windows Server Insider-Vorschau finden Sie unter [Getting Started with the Windows Insider Program](https://insider.windows.com/for-business-getting-started-server/).

- Spezifische Anforderungen für den ausgewählten Nachweis Modus:
  - Der **TPM-Modus** ist der stärkste Nachweis Modus und verwendet eine Trusted Platform Module (TPM), um kryptografisch zu überprüfen, ob Ihre Host Computer Ihrem Rechenzentrum bekannt sind (mit einer eindeutigen ID von jedem TPM), und führen Sie vertrauenswürdige Hardware und Firmware aus. Konfigurationen (mithilfe einer TPM-Baseline) und Ausführen von vertrauenswürdigem Kernel-und Benutzermoduscode (mithilfe der Windows Defender-Anwendungssteuerung). Die folgende Hardware ist erforderlich, um den TPM-Modus zu verwenden: 
    - TPM 2,0-Modul installiert und aktiviert 
    - Sicherer Start aktiviert mit der Microsoft-Richtlinie für den sicheren Start (aktivieren Sie nicht die Richtlinie für den sicheren Start von Drittanbietern oder benutzerdefinierte Richtlinien)
    - IOMMU (Intel VT-d oder AMD IOV), um Angriffe auf den direkten Speicherzugriff zu verhindern 

  - Der **Host Schlüssel Modus** verwendet ein asymmetrisches Schlüsselpaar (ähnlich wie SSH-Schlüssel), um Host Computer zu identifizieren und zu autorisieren, die SQL Server ausführen möchten. Dieser Modus ist leichter einzurichten und verfügt nicht über bestimmte Hardwareanforderungen, sondern überprüft nicht die auf den Host Computern laufende Software oder Firmware.  

Um zu überprüfen, ob das TPM kompatibel ist, führen Sie die folgenden Befehle auf dem Host Computer aus, auf dem Sie SQL Server mithilfe Always Encrypted mit sicheren Enklaven ausführen möchten. "2,0" muss in der Liste der unterstützten specversions angezeigt werden, damit Sie den TPM-Nachweis verwenden können:

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>Einrichten des ersten HGS-Knotens 

Der Host-Überwachungsdienst arbeitet mit einem Cluster mit drei Knoten in einer hoch Verfügbarkeits Konfiguration. Es wird empfohlen, dass Sie einen Knoten vollständig einrichten, bevor Sie weitere Knoten hinzufügen. 

Führen Sie alle folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus.

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   Für Always Encrypted mit sicheren Enklaven müssen auf den Host Computern, auf denen SQL Server ausgeführt wird, und auf Computern, auf denen Daten Bank Client Anwendungen ausgeführt werden, HGS kontaktiert werden, obwohl nur für die Host Computer ein Nachweis erforderlich ist.

4. Nachdem der Computer neu gestartet wurde, wird HGS installiert, und der Server ist auch ein Domänen Controller, auf dem Active Directory konfiguriert sind. 
   Während der Active Directory Konfiguration wird das Administrator Konto für den lokalen Computer der Gruppe "Domänen-Admins" hinzugefügt, und nur Mitglieder dieser Gruppe können sich bei einem Domänen Controller anmelden.
   Melden Sie sich mit dem Domänen Administrator Konto (z administrator@bastion.local . b. "geschützten. local\administrator") an, oder erstellen Sie ein weiteres Domänen Administrator Konto für die Anmeldung, und konfigurieren Sie dann den Nachweis Dienst.
   Sie müssen den TPM-oder Host Schlüssel Nachweis auswählen und den entsprechenden Befehl ausführen. 
   Geben Sie für hgsservicename den gewählten DNN an.

   Für den TPM-Modus:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   Für den Host Schlüssel Modus:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. Stellen Sie sicher, dass die Host Computer, auf denen SQL Server ausgeführt wird, die DNS-Namen der neuen Mitglieder der HGS-Domäne auflösen können, indem Sie eine Weiterleitung von ihren Unternehmens-DNS-Servern an den neuen HGS-Domänen Controller richten. Wenn Sie Windows Server-DNS verwenden, können Sie eine bedingte Weiterleitung einrichten, indem Sie die folgenden Befehle in einer PowerShell-Konsole mit erhöhten Rechten auf einem DNS-Server in Ihrer Organisation ausführen. Ersetzen Sie die Namen und Adressen in der folgenden Windows PowerShell-Syntax nach Bedarf für Ihre Umgebung. Nachdem Sie weitere HGS-Knoten hinzugefügt haben, führen Sie diesen Befehl erneut aus, um Sie als Master Server hinzuzufügen.

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>Einrichten zusätzlicher HGS-Knoten für Produktions Bereitstellungen

Um dem Cluster Knoten hinzuzufügen, führen Sie die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus. 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. Legen Sie fest, dass der DNS-Client Konflikt Löser auf Ihren primären HGS-Server verweist, damit der HGS-Domänen Name aufgelöst werden kann. Wenn Sie Server mit Desktop Darstellung verwenden, können Sie dies im Netzwerk-und Freigabe Center durchführen. Unter Server Core können Sie das **SCONFIG. exe** -Tool, Option 8 oder **Set-dnsclientserveraddress** verwenden, um die DNS-Adresse festzulegen. 

3. Als nächstes Stufen wir diesen Server zu einem Domänen Controller herauf. Sie benötigen Domänen Administrator-Anmelde Informationen, um diese Aufgabe abzuschließen, und werden nach dem Ausführen des Befehls aufgefordert, ein Kennwort für den Verzeichnisdienst-Reparatur Modus einzugeben. 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>Konfigurieren von HGS für HTTPS 

Wenn Sie den HGS-Server initialisieren, werden die IIS-Websites standardmäßig für die HTTP-Kommunikation konfiguriert.

> [!NOTE]
> Das Konfigurieren von HTTPS mithilfe eines bekannten und vertrauenswürdigen HGS-Serverzertifikats ist erforderlich, um man-in-the-Middle-Angriffe zu verhindern, und wird daher für Produktions Bereitstellungen empfohlen.

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

> [!NOTE]
> Für Always Encrypted mit sicheren Enklaven muss das SSL-Zertifikat auf beiden Host Computern, auf denen SQL Server ausgeführt wird, als vertrauenswürdig eingestuft werden, und Computer, auf denen Daten Bank Client Anwendungen ausgeführt werden, müssen HGS kontaktieren. 

## <a name="collect-attestation-info-from-the-host-machines"></a>Sammeln von Nachweis Informationen von den Host Computern

Sobald HGS eingerichtet ist, muss Sie mit Nachweis Informationen von Ihren Host Computern konfiguriert werden, damit Sie wissen, welche Computer autorisiert werden müssen, vertrauliche Berechnungen mithilfe Always Encrypted und sicheren enkennungen von VB auszuführen. Diese Schritte unterscheiden sich je nach verwendeter Nachweis Modus. 

### <a name="collect-tpm-attestation-artifacts"></a>Sammeln von TPM-Nachweis Artefakten 

Wenn Sie den TPM-Modus verwenden, führen Sie auf jedem Host Computer die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus, um die Unterstützung für den Nachweis zu installieren und die Informationen zu sammeln, die Sie für die Registrierung beim Host-Überwachungsdienst benötigen. 

1. Installieren Sie zum Installieren des HGS-Clients auf dem Host Computer die Funktion des überwachten Hosts, auf der auch Hyper-V installiert wird. 
   Obwohl Sie keine VMs auf diesem Computer ausführen, ist der Hypervisor erforderlich, um virtualisierungsbasierte Sicherheitsfeatures zu aktivieren, die VSB-Enklaven isolieren.

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Starten Sie den Computer neu, wenn Sie aufgefordert werden, die Installation von Hyper-V abzuschließen. 
3. Erstellen Sie eine Code Integritätsrichtlinie, um einzuschränken, welche Software auf dem System ausgeführt werden kann. 
   Eine beliebige Windows Defender-Anwendungs Steuerungs Richtlinie ist ausreichend. 
   Wenn Sie nur Microsoft-Software auf dem Server ausführen, können Sie mit den folgenden Befehlen schnell eine Richtlinie erstellen. 
   Die Richtlinie befindet sich im Überwachungsmodus. Dies bedeutet, dass ein Ereignis über nicht autorisierten Code protokolliert, aber nicht ausgeführt wird.  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Die Windows Defender-Anwendungssteuerung verfügt über zahlreiche Funktionen, die eine Vielzahl von Sicherheitsfunktionen abdecken. 
   Wenn Sie nicht-Microsoft-Software zulassen oder die Standard Richtlinie anpassen müssen, können Sie das [Bereitstellungs Handbuch für die Windows Defender-Anwendungssteuerung](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)nutzen.   


4. Überprüfen Sie mit dem folgenden Befehl, ob die virtualisierungsbasierte Sicherheit auf dem Computer ausgeführt wird. 
   Sie werden feststellen, dass VSB ausgeführt wird, wenn im Feld deviceguardsecurityservicesrunning der Wert "hypervisorenforcedcodeintegrity" aufgeführt ist. 
   Wenn er nicht ausgeführt wird, laden Sie das [Device Guard Readiness-Tool](https://www.microsoft.com/download/details.aspx?id=53337) herunter, und führen Sie "DG_Readiness. ps1-enable-hvci" aus, um es zu aktivieren.  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```

5. Erfassen Sie den TPM-Bezeichner und die Baseline:

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. Kopieren Sie die Dateien XML, tcglog und bin aus c:\artefakte auf Ihren HGS-Server.
7. Wenn dies der erste TPM-Host ist, den Sie dem HGS-Server hinzufügen, müssen Sie die vertrauenswürdigen TPM-Stamm Zertifikate auf jedem HGS-Server installieren. 
   Befolgen Sie die [Anweisungen in der HGS-Dokumentation](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates) , um diesen Schritt abzuschließen.
8. Autorisieren Sie den Host auf dem HGS-Server für den Nachweis. 
   In den folgenden Skripts wird davon ausgegangen, dass die drei Dateien auf dem HGS-Server nach "c:\temp" kopiert und der Computername des Servers "ServerA" lautet. 
   Passen Sie die Pfade und Namen so an, dass Sie Ihrer eigenen Umgebung entsprechen. 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```

9. Der erste Server ist nun bereit für das bestätigen! 
   Führen Sie auf dem Host Computer den folgenden Befehl aus, um ihm mitzuteilen, wo es zu bestätigen ist (ändern Sie den DNS-Namen in den des HGS-Clusters. in der Regel verwenden Sie den HGS-Dienstnamen in Kombination mit dem HGS-Domänen Namen). 
   Wenn Sie den Fehler "hostnicht erreichbar" erhalten, stellen Sie sicher, dass Sie die DNS-Namen Ihrer HGS-Server auflösen und pingen können. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. Das Ergebnis des obigen Befehls sollte anzeigen, dass attestationstatus = erfolgreich war. Wenn dies nicht der Fall ist, finden Sie unter Nachweis [Fehler](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures) Hinweise zum Beheben des Fehlers.   
11. Wiederholen Sie die Schritte 1-10 für jeden Host Computer. 
    Wenn Sie identische Hardware verwenden, müssen Sie keine neue Baseline oder CI-Richtlinie für jeden Computer erfassen. 
    Die Baseline Ihres ersten Servers deckt alle identisch konfigurierten Computer ab, und die CI-Richtlinie kann über mehrere Computer hinweg wieder verwendet werden, solange die Microsoft-Software die einzige Software auf dem Computer ist.

### <a name="collecting-host-keys"></a>Erfassen von Host Schlüsseln 

> [!NOTE] 
> Der Host Schlüssel Nachweis wird nur für die Verwendung in Testumgebungen empfohlen. Der TPM-Nachweis bietet die stärksten Zusicherungen, dass VB die Verarbeitung Ihrer sensiblen Daten auf SQL Server die den vertrauenswürdigen Code ausführen und die Computer mit den empfohlenen Sicherheitseinstellungen konfiguriert werden. 

Wenn Sie das Einrichten von HGS im Host Schlüssel Nachweis Modus ausgewählt haben, müssen Sie Schlüssel von jedem Host Computer generieren und erfassen und diese beim Host-Überwachungsdienst registrieren. 

1. Wenn Sie den HGS-Client auf Ihrem Host Computer installieren möchten, installieren Sie die Funktion des überwachten Hosts, auf der auch Hyper-V installiert wird. 
   Obwohl Sie keine virtuellen Computer auf diesem Computer ausführen, ist der Hypervisor erforderlich, um die virtualisierungsbasierten Sicherheitsfeatures zu aktivieren, die die VSB-enves isolieren, die Always Encrypted-Abfragen ausgeführt werden. 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Starten Sie den Computer neu, wenn Sie aufgefordert werden, die Installation von Hyper-V abzuschließen.
3. Generieren eines eindeutigen Host Schlüssels und Exportieren des resultierenden öffentlichen Schlüssels in eine Datei. 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   Alternativ können Sie einen Fingerabdruck angeben, wenn Sie Ihr eigenes Zertifikat verwenden möchten. 
   Dies kann hilfreich sein, wenn Sie ein Zertifikat für mehrere Computer freigeben möchten, oder wenn Sie ein Zertifikat verwenden möchten, das an ein TPM oder ein HSM gebunden ist. Hier ist ein Beispiel für das Erstellen eines TPM-gebundenen Zertifikats (das verhindert, dass der private Schlüssel gestohlen und auf einem anderen Computer verwendet wird und nur ein TPM 1,2 erforderlich ist):

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. Kopieren Sie den Host Schlüssel in den Host-Überwachungsdienst. 
5. Registrieren Sie den Host Schlüssel mit einem beliebigen HGS-Knoten, und verwenden Sie dabei einen relevanten Namen und Pfad für Ihre Umgebung: 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. Der erste Server ist nun bereit für das bestätigen! 
   Führen Sie auf dem Host Computer den folgenden Befehl aus, um ihm mitzuteilen, wo es zu bestätigen ist (ändern Sie den DNS-Namen in den des HGS-Clusters. in der Regel verwenden Sie den HGS-Dienstnamen in Kombination mit dem HGS-Domänen Namen). 
   Wenn Sie den Fehler "hostnicht erreichbar" erhalten, stellen Sie sicher, dass Sie die DNS-Namen Ihrer HGS-Server auflösen und pingen können.    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. Das Ergebnis des obigen Befehls sollte anzeigen, dass attestationstatus = erfolgreich war. 
   Wenn Sie den Fehler "hostnicht erreichbar" erhalten, bedeutet dies, dass der Host Computer nicht mit HGS kommunizieren kann. 
   Stellen Sie sicher, dass die DNS-Auflösung zwischen dem Host Computer und den HGS-Servern eingerichtet ist und Sie einen Ping für die Server durchsetzen können. 
   Ein unauthorizedhost-Fehler zeigt an, dass der öffentliche Schlüssel nicht beim HGS-Server registriert wurde – wiederholen Sie die Schritte 4 und 5, um den Fehler zu beheben. 
   Wenn alle anderen Fehler ausfallen, führen Sie Clear-hgsclienthostkey aus, und wiederholen Sie die Schritte 3-6.   

8. Wiederholen Sie die Schritte 1-7 für jeden Server, der SQL Server Always Encrypted mithilfe von VSB-Enklaven ausgeführt wird.     


