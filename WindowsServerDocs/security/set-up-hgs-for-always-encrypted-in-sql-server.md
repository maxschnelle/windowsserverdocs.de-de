---
title: Einrichten von Host-Überwachungsdienst für Always Encrypted in SQL Server
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 2f800dfa01077287f8200dd8abea0be899776683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866691"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>Einrichten von Host-Überwachungsdienst für Always Encrypted mit sicheren Enclaves in SQL Server 

>Gilt für: Windows Server (Halbjährlicher Kanal), Windows Server-2019, SQL Server-2019-Vorschau
 
[Always Encrypted mit sicheren Enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves) in SQL Server-2019 Preview ist ein Feature, um vertrauliche Berechnungen in einer Datenbank gespeicherte sensible Daten zu aktivieren. Die Host Guardian Service (HGS) spielt eine wichtige Rolle bei, wie Sie Ihre Daten schützen, wenn eine sichere Enclave, konfiguriert für Always Encrypted, eine Arbeitsspeicher-Enclave virtualisierungsbasierte Sicherheit (VBS) ist. Die Sicherheit eine VBS-Arbeitsspeicher-Enclave hängt davon ab, die Sicherheit der Windows-Hypervisor und breiter, die Sicherheit des Computers, der SQL Server hostet. 

Bevor eine Datenbank-Clientanwendung die von der VBS-Arbeitsspeicher-Enclave für Always Encrypted verwendet werden, um Berechnungen auszuführen, auf sensible Daten erlaubt werden, muss die Anwendung daher mit einem vertrauenswürdigen Host-Überwachungsdienst bestätigen. Nachweis stellt den Computer mit SQL Server, die die Enclave enthält, befindet sich im richtigen Zustand und vertrauenswürdig. Für den Rest dieses Themas werden wir auf dem Computer mit SQL Server als einfach auf dem Host-Computer verweisen.

Es gibt zwei sich gegenseitig ausschließende Möglichkeiten für die Anwendung bestätigen: 

- Schlüsselnachweis Host autorisiert einen Host von Beweisen sie einen bekannten und vertrauenswürdigen privaten Schlüssel besitzt. Host-schlüsselnachweis und einem physischen Hostcomputer oder einen virtuellen Computer der Generation 2, Ausführen von SQL Server wird für Umgebungen vor der Produktion empfohlen.
- TPM-Nachweis überprüft die Hardware-Messungen, um sicherzustellen, dass es sich bei ein Host ausgeführt wird, nur die richtigen Binärdateien und Sicherheitsrichtlinien. TPM-Nachweis und einem physischen Host-Computer (nicht auf einem virtuellen Computer), die mit SQL Server wird für produktionsumgebungen empfohlen.

Weitere Informationen über die Host-Überwachungsdienst und was sie messen kann, finden Sie unter [überwachten Fabric und abgeschirmte VMs Overview](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms). Beachten Sie, dass auch die Dokumente über abgeschirmte VMs sprechen, die gleichen Schutzmaßnahmen, die Architektur und die bewährten Methoden für die SQL Server Always Encrypted mithilfe von VBS Enclaves gelten. 

Dieser Artikel hilft beim Einrichten eines Host-Überwachungsdienst in eine empfohlene Konfiguration. 

## <a name="prerequisites"></a>Vorraussetzungen 

Dieser Abschnitt behandelt die Voraussetzungen für die Host-Überwachungsdienst und Computer gehostet. 

### <a name="hgs-servers"></a>HGS-Servern

- 1 bis 3-Server-Host-Überwachungsdiensts ausführen. 

  >[!NOTE]
  >Nur 1 HGS-Server ist für eine Test- oder präproduktionsumgebung-Umgebung erforderlich.

  Diese Server sollten sorgfältig geschützt werden, da sie steuern, welche Computer von Always Encrypted mit sicheren Enclaves SQL Server-Instanzen ausgeführt werden können. 
  Es wird empfohlen, dass verschiedene Administratoren den Host-Überwachungsdienst-Cluster zu verwalten und der Host-Überwachungsdienst auf physischer Hardware isoliert vom Rest der Infrastruktur oder in separaten virtualisierungsfabrics oder Azure-Abonnements ausführen.

  - Windows Server 2019 Standard oder Datacenter Edition.
  - 2 CPUs
  - 8GB RAM
  - 100GB Speicher

  Verwenden Sie entweder die [langfristigen Wartungskanal (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) oder [Halbjährlicher Kanal](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel). 
  Zum Registrieren und Windows Server Insider Preview heruntergeladen haben, finden Sie unter [erste Schritte mit der Windows-Insider-Programm](https://insider.windows.com/for-business-getting-started-server/).

- Wählen Sie einen Namen für die neue Active Directory-Gesamtstruktur, die durch den Host-Überwachungsdienst erstellt. 
  Host-Überwachungsdienst sollte nicht mit Ihrer vorhandenen Unternehmensdomäne verknüpft werden und verschiedene Administratoren verwalten müssen.   

- Firewall- und Routingregeln für eingehender HTTP-Datenverkehr (TCP 80) oder HTTPS (TCP-Port 443)-Datenverkehr auf den Host-Überwachungsdienst-Knoten aus zu ermöglichen: 

  - Der Computer mit SQL Server
  - Die Computer, die Datenbank-Clientanwendungen (z. B. Webserver), die Datenbank Abfragen und Verwenden von Always Encrypted mit sicheren Enclaves ausgeführt wird. 

### <a name="sql-server-host-machines"></a>SQL Server-Hostcomputern

- Ihre SQL Server-Instanz sollte auf einem Computer ausführen, die die folgenden Anforderungen erfüllt:

  - Windows: 
    - Windows 10 Enterprise, Version 1809  
    - Windows-Server 2019 Datacenter (Halbjährlicher Kanal), Version 1809
    - Windows Server 2019 Datacenter
  - Physischer Computer für die Produktion oder einen virtuellen Computer der Generation 2 zu Testzwecken (Beachten Sie, dass Azure VMs der Generation 2 nicht unterstützt)
  - Allgemeine Anforderungen aufgelistet in [Hardware- und Softwareanforderungen für die Installation von SQL Server](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017).   

  Verwenden Sie entweder die [langfristigen Wartungskanal (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) oder [Halbjährlicher Kanal](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel). 
  Zum Registrieren und Windows Server Insider Preview heruntergeladen haben, finden Sie unter [erste Schritte mit der Windows-Insider-Programm](https://insider.windows.com/for-business-getting-started-server/).

- Anforderungen für den ausgewählten nachweismodus spezifisch:
  - **TPM-Modus** ist die stärkste nachweismodus und verwendet ein Trusted Platform Module (TPM) kryptografisch überprüfen, dass der Hostcomputer in Ihrem Rechenzentrum (mit einer eindeutigen ID in jede TPM), ausgeführt wird, vertrauenswürdige Hardware und Firmware bekannt sind (verwenden eine TPM-Baseline), Konfigurationen und trustworthy Kernel und Code im Benutzermodus (mithilfe von Windows Defender Application Control) ausführen. Die folgende Hardware ist erforderlich, um TPM-Modus verwenden zu können: 
    - TPM 2.0-Modul installiert und aktiviert 
    - Sicherer Start mit der Richtlinie für die Microsoft sicherer Start aktiviert (Aktivieren Sie nicht 3. Richtlinie für die Zertifizierungsstelle für sicheren Start oder benutzerdefinierten Richtlinien)
    - UNTERSTÜTZT (Intel VT-d oder AMD IOV), um direct Memory Access Angriffe zu verhindern 

  - **Wichtige Hostmodus** verwendet ein asymmetrisches Schlüsselpaar (ähnlich wie SSH-Schlüssel) zur Identifizierung und Autorisierung von Hostcomputern, die SQL Server ausführen möchten. Dieser Modus ist leichter einzurichten und verfügt nicht über alle hardwareanforderungen für bestimmte, jedoch wird nicht überprüft werden, die Software oder Firmware, die auf den Hostcomputern ausführen.  

Um festzustellen, ob das TPM kompatibel ist, führen Sie die folgenden Befehle auf dem Hostcomputer, in dem Sie SQL-Server, die von Always Encrypted mit sicheren Enclaves ausführen möchten. "2.0" müssen in der Liste der unterstützten SpecVersions und TPM-Nachweis können angezeigt werden:

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>Richten Sie den ersten Knoten für den Host-Überwachungsdienst 

Host-Überwachungsdienst gibt es in einer hoch verfügbaren Konfiguration mit einem Cluster mit 3 Knoten. Es wird empfohlen, dass Sie einen Knoten vollständig einrichten vor dem Hinzufügen weiterer Knoten. 

Führen Sie die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus.

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   Für Always Encrypted mit sicheren Enclaves führen die Hostcomputer, auf denen SQL Server und Computer, die ausgeführt Datenbank-Clientanwendungen, die beide benötigen, wenden Sie sich an der Host-Überwachungsdienst bietet jedoch nur auf die Hostcomputern Nachweis erforderlich.

4. Nach dem Neustart des Computers-Host-Überwachungsdienst installiert werden, und der Server werden sich auch auf einem Domänencontroller mit konfiguriertem Active Directory. 
   Während der Active Directory-Konfiguration wird das lokale Computerkonto für den Administrator der Domänen-Admins-Gruppe hinzugefügt, und nur ein Mitglied dieser Gruppe zu einem Domänencontroller anmelden können.
   Melden Sie sich mit dem Domänenadministratorkonto (z. B. administrator@bastion.local oder bastion.local\administrator), oder erstellen Sie ein anderes-Admins-Domänenadministratorkonto für melden Sie sich, und klicken Sie dann die Attestation-Dienst zu konfigurieren.
   Sie benötigen, wählen Sie die TPM oder das Host-schlüsselnachweis und führen Sie den entsprechenden Befehl. 
   Geben Sie für die HgsServiceName das DNN, das Sie ausgewählt haben.

   Für TPM-Modus:
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   Für den Host-Schlüssel-Modus:
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. Stellen Sie sicher, dass die DNS-Namen Ihrer neuen Domänenmitglieder von Host-Überwachungsdienst auflösen, indem Sie eine Weiterleitung von Ihre Unternehmens-DNS-Server mit dem neuen Host-Überwachungsdienst-Domänencontroller einrichten die Hostcomputer, auf denen SQL Server ausgeführt werden. Wenn Sie Windows Server-DNS verwenden, können Sie eine bedingte Weiterleitung einrichten, indem Sie die folgenden Befehle auf einem DNS-Server in Ihrer Organisation in einer PowerShell-Konsole mit erhöhten Rechten ausführen. Ersetzen Sie den Namen und Adressen in der Windows PowerShell-Syntax finden Sie unten nach Bedarf für Ihre Umgebung. Weitere HGS-Knoten hinzugefügt haben, führen Sie diesen Befehl erneut aus, um sie als Masterserver hinzuzufügen.

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>Richten Sie zusätzliche HGS-Knoten für produktionsbereitstellungen

Um Knoten zum Cluster hinzuzufügen, führen Sie die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus. 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. Legen Sie die DNS-Clientauflösung an Ihrem primären Host-Überwachungsdienst-Server verweisen, damit sie Ihr HGS-Domänennamen auflösen kann. Wenn Sie Server mit Desktopdarstellung verwenden, möglich dies in der Netzwerk- und Freigabecenter. Auf Server Core aufweist, können Sie die **sconfig.exe** tool, 8, option oder **Set-DnsClientServerAddress** zum Festlegen der DNS-Adresse. 

3. Als Nächstes werden wir diesen Server zu einem Domänencontroller heraufstufen. Sie benötigen Domänenadministrator-Anmeldeinformationen, um diese Aufgabe abzuschließen, und werden aufgefordert, ein Verzeichnisdienst-Wiederherstellungsmodus-Kennwort eingeben, nach Ausführung des Befehls. 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>Konfigurieren von Host-Überwachungsdienst für HTTPS 

In der Standardeinstellung beim Initialisieren des HGS-Servers wird die IIS-Websites für die nur für HTTP-Kommunikation konfiguriert.

>[!NOTE]
>Konfigurieren von HTTPS mit einem bekannten und vertrauenswürdigen HGS-Serverzertifikat ist erforderlich, um Man-in-the-Middle-Angriffe zu verhindern, und es wird daher für produktionsbereitstellungen empfohlen.

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

>[!NOTE]
>Für Always Encrypted mit sicheren Enclaves das SSL-Zertifikat muss auf beiden Hostcomputern vertrauenswürdig sein, auf denen SQL Server ausgeführt und Computer, die Datenbank-Clientanwendungen ausgeführt kontaktieren müssen, Host-Überwachungsdienst. 

## <a name="collect-attestation-info-from-the-host-machines"></a>Erfassen Sie Nachweis Informationen von den Hostcomputern

Nachdem der Host-Überwachungsdienst eingerichtet ist, muss sie mit Informationen zum Identitätsnachweis aus Ihrem Hostcomputer konfiguriert werden, damit dieser weiß, welche Computer autorisiert werden soll, vertrauliche Berechnungen, die mit Always Encrypted und VBS sichere Enclaves ausgeführt. Diese Schritte hängen von der nachweismodus, die Sie verwenden. 

### <a name="collect-tpm-attestation-artifacts"></a>Sammeln von TPM-Nachweis-Artefakte 

Wenn Sie TPM-Modus verwenden, führen Sie die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten für jeden Hostcomputer für die Unterstützung für den Nachweis installieren und erfassen die Informationen, die Sie mit der Host-Überwachungsdienst registrieren müssen. 

1. Um den Host-Überwachungsdienst-Client auf dem Hostcomputer installieren, installieren Sie die überwachte Host-Funktion, die auch die Hyper-V installiert wird. 
   Während Sie keine virtuellen Computer auf diesem Computer ausführen, muss der Hypervisor die virtualisierungsbasierte Sicherheitsfeatures zu aktivieren, die VBS Enclaves zu isolieren.

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Neustarten des Computers bei der Aufforderung zum Abschließen der Installation von Hyper-V 
3. Erstellen Sie eine codeintegritätsrichtlinie um einzuschränken, welche Software auf dem System ausgeführt werden kann. 
   Jede Windows Defender Application Control-Richtlinie ist ausreichend. 
   Wenn Sie nur Microsoft-Software auf dem Server ausführen, werden die folgenden Befehle schnell eine Richtlinie für Sie erstellen. 
   Die Richtlinie wird im Überwachungsmodus, d. h., protokolliert ein Ereignis zu nicht autorisierten Code, sondern wird nicht verhindert, dass ausgeführt wird.  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Windows Defender Application Control verfügt über zahlreiche Features, um eine Vielzahl von Sicherheit Postures abzudecken. 
   Wenn Sie nicht-Microsoft-Software zulassen, oder passen Sie die Standardrichtlinie, Se müssen die [Handbuch für die Bereitstellung von Windows Defender Application Control](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).   


4. Stellen Sie sicher, dass die virtualisierungsbasierte Sicherheit auf dem Computer mit dem folgenden Befehl ausgeführt wird. 
   Sie wissen, dass VBS ausgeführt wird, wenn das DeviceGuardSecurityServicesRunning-Feld "HypervisorEnforcedCodeIntegrity" darin aufgeführt ist. 
   Wenn er nicht ausgeführt wird, laden Sie die [Device Guard Systemupdate-Vorbereitungstool](https://www.microsoft.com/download/details.aspx?id=53337) , und führen Sie "DG_Readiness.ps1-HVCI - aktivieren" aktivieren.  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```
5. Sammeln Sie die TPM-ID und der Baseline an:

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. Kopieren Sie die XML-Tcglog und Binärdateien aus C:\artifacts, mit dem HGS-Server.
7. Wenn dies der erste TPM-Host, die, den Sie an den Host-Überwachungsdienst-Server hinzufügen ist, müssen Sie die vertrauenswürdigen TPM-Stammzertifikate auf jedem Host-Überwachungsdienst-Server zu installieren. 
   Führen Sie die [Anleitungen in der Dokumentation für die Host-Überwachungsdienst](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates) zum Ausführen dieses Schritts.
8. Autorisieren Sie diesen Host einen Nachweis erbringen, auf dem Server-Host-Überwachungsdienst. 
   Die unten angegebenen Skripts wird davon ausgegangen werden, die 3-Dateien auf C:\temp auf dem Host-Überwachungsdienst-Server kopiert wurden und Name des Servers "ServerA" ist. 
   Passen Sie die Pfade und den Namen Ihrer eigenen Umgebung entsprechend. 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```
9. Ihren erste Server kann jetzt bestätigen! 
   Führen Sie den folgenden Befehl mitteilen, wo Sie bestätigen (Änderung der DNS-Name, der von Ihrem Host-Überwachungsdienst-Cluster, in der Regel den Namen des Host-Überwachungsdienst-Diensts mit dem Host-Überwachungsdienst-Domänennamen kombiniert verwendet wird) ist, auf dem Hostcomputer. 
   Wenn Sie eine HostUnreachable-Fehlermeldung erhalten, stellen Sie sicher, können Sie beheben und die DNS-Namen der HGS-Server zu pingen. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. Das Ergebnis des Befehls oben sollte angezeigt werden, AttestationStatus = erfolgreich. Wenn dies nicht der Fall ist, finden Sie unter [Nachweis Fehler](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures) Anleitungen dazu, wie Sie den Fehler zu beheben.   
11. Wiederholen Sie die Schritte 1 bis 10 für jeden Hostcomputer. 
    Wenn Sie dieselbe Hardware verwenden, müssen Sie nicht um eine neue Baseline oder codeintegritätsrichtlinie für jeden Computer zu erfassen. 
    Die Baseline aus Ihren ersten Server behandelt alle identisch konfigurierter Computer aus, und die codeintegritätsrichtlinie kann wiederverwendet werden über mehrere Computer hinweg, sofern Microsoft-Software, die nur-Software auf dem Computer ist.

### <a name="collecting-host-keys"></a>Sammeln von Host-Schlüssel 

>[!NOTE] 
>Host-schlüsselnachweis wird nur für die Verwendung in testumgebungen empfohlen. TPM-Nachweis gewährleistet die stärksten VBS Enclaves verarbeiten Ihre sensiblen Daten in SQL Server vertrauenswürdigen Code ausgeführt werden, und die Computer mit den empfohlenen Einstellungen konfiguriert werden. 

Wenn Sie Host-Überwachungsdienst in den schlüsselnachweis Hostmodus einrichten möchten, müssen Sie generieren und Schlüssel von jedem Hostcomputer erfassen, und registrieren Sie ihn beim Host-Überwachungsdienst. 

1. Installieren Sie die überwachte Host-Funktion, die auch die Hyper-V installiert wird, rufen Sie den Host-Überwachungsdienst-Client auf dem Hostcomputer installiert. 
   Während Sie keine virtuellen Computer auf diesem Computer ausführen, muss der Hypervisor die virtualisierungsbasierte Sicherheitsfeatures zu aktivieren, die von der VBS Enclaves zu isolieren, die Always Encrypted-Abfragen ausführen. 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Neustarten des Computers bei der Aufforderung zum Abschließen der Installation von Hyper-V
3. Generieren Sie einen eindeutigen Host-Schlüssel und exportieren Sie den resultierenden öffentlichen Schlüssel in eine Datei. 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   Alternativ können Sie einen Fingerabdruck angeben, wenn Sie Ihr eigenes Zertifikat verwenden möchten. 
   Dies kann nützlich sein, wenn ein Zertifikat auf mehreren Computern freigeben, oder verwenden ein Zertifikat an einem TPM noch ein HSM gebunden werden soll. Hier ist ein Beispiel zum Erstellen eines TPM-Bound-Zertifikats (der verhindert, dass der private Schlüssel gestohlen und auf einem anderen Computer verwendet und erfordert nur ein TPM 1.2):

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. Kopieren Sie den Hostschlüssel auf dem Host-Überwachungsdienst. 
5. Registrieren Sie den Hostschlüssel mit einem beliebigen Host-Überwachungsdienst Knoten mit relevanten Namen und den Pfad für Ihre Umgebung: 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. Ihren erste Server kann jetzt bestätigen! 
   Führen Sie den folgenden Befehl mitteilen, wo Sie bestätigen (Änderung der DNS-Name, der von Ihrem Host-Überwachungsdienst-Cluster, in der Regel den Namen des Host-Überwachungsdienst-Diensts mit dem Host-Überwachungsdienst-Domänennamen kombiniert verwendet wird) ist, auf dem Hostcomputer. 
   Wenn Sie eine HostUnreachable-Fehlermeldung erhalten, stellen Sie sicher, können Sie beheben und die DNS-Namen der HGS-Server zu pingen.    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. Das Ergebnis des Befehls oben sollte angezeigt werden, AttestationStatus = erfolgreich. 
   Wenn Sie eine HostUnreachable-Fehlermeldung erhalten, bedeutet dies, dass es sich bei der Hostcomputer nicht mit Host-Überwachungsdienst kommunizieren kann. 
   Stellen Sie sicher, dass die DNS-Auflösung zwischen dem Host-Computer und die Host-Überwachungsdienst-Server eingerichtet ist und Sie die Server pingen können. 
   Ein UnauthorizedHost-Fehler weist darauf hin, dass der öffentliche Schlüssel mit dem HGS-Server – wiederholen Sie die Schritte 4 und 5 zum Beheben des Fehlers nicht registriert wurde. 
   Wenn alle anderen Versuche fehlschlagen, führen Sie Clear-HgsClientHostKey, und wiederholen Sie Schritte 3 bis 6 aus.   

8. Wiederholen Sie die Schritte 1 bis 7 für jeden Server, auf denen SQL Server Always Encrypted mithilfe von VBS Enclaves ausgeführt wird.     


