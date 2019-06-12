---
title: Verwalten von Zertifikaten für die Software Defined Networking
description: Sie können in diesem Thema verwenden, um Informationen zum Verwalten von Zertifikaten für Network Controller Northbound und die Southbound-Kommunikation, beim Bereitstellen von Software-Defined Networking (SDN) in Windows Server 2016 Datacenter.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: d29a98e24b475c38fee61972bf9efbd5a2528974
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446263"
---
# <a name="manage-certificates-for-software-defined-networking"></a>Verwalten von Zertifikaten für die Software Defined Networking

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema erfahren, wie das Verwalten von Zertifikaten für Network Controller Northbound und die Southbound-Kommunikation, beim Bereitstellen von Software Defined Networking \(SDN\) in Windows Server 2016 Datacenter, und Sie werden verwendet, System Center Virtual Machine Manager- \(SCVMM\) als Ihre SDN-Management-Client.

>[!NOTE]
>Übersicht über den Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](../technologies/network-controller/Network-Controller.md).

Wenn Sie Kerberos für die Sicherung der Kommunikation des Netzwerkcontrollers nicht verwenden, können Sie die x. 509-Zertifikate für Authentifizierung, Autorisierung und Verschlüsselung.

SDN in Windows Server 2016 Datacenter unterstützt beide Self\-signiert und Zertifizierungsstelle \(Zertifizierungsstelle\)-x. 509-Zertifikaten. Dieses Thema enthält schrittweise Anweisungen für diese Zertifikate erstellen und diese anwenden zu Network Controller Northbound Kommunikationskanäle mit Verwaltungsclients zu schützen und die Southbound-Kommunikation mit Netzwerkgeräten, z. B. der Software Load Balancer \(SLB\).
.
Bei Verwendung Zertifikat\-basierte Authentifizierung, Sie müssen registrieren, ein Zertifikat auf dem Netzwerkcontroller-Knoten, die auf folgende Weise verwendet wird.

1. Verschlüsseln die Northbound-Kommunikation mit Secure Sockets Layer \(SSL\) zwischen Netzwerkcontroller und Verwaltungsclients, z. B. System Center Virtual Machine Manager.
2. Authentifizierung zwischen dem Netzwerkcontroller-Knoten und Southbound-Geräte und Dienste, wie Hyper-V-Hosts und Software-Lastenausgleichsmodulen \(SLBs\).

## <a name="creating-and-enrolling-an-x509-certificate"></a>Erstellen und registrieren ein x. 509-Zertifikat

Sie können das Erstellen und registrieren Sie entweder ein selbstsigniertes\-signiert oder ein Zertifikat, das von einer Zertifizierungsstelle ausgestellt wurde.

>[!NOTE]
>Wenn Sie SCVMM verwenden, um die Bereitstellung des Netzwerkcontrollers zu verwenden, müssen Sie das x. 509-Zertifikat angeben, das zum Verschlüsseln der Northbound-Kommunikation während der Konfiguration der Netzwerkcontroller-Dienstvorlage verwendet wird.

Konfiguration des Zertifikats muss die folgenden Werte enthalten.

- Der Wert für die **RestEndPoint** Textfeld muss entweder der Controller vollständig qualifizierte Domänenname \(FQDN\) oder IP-Adresse. 
- Die **RestEndPoint** Wert muss der Name des Antragstellers übereinstimmen \(allgemeiner Name, CN\) des x. 509-Zertifikats.

### <a name="creating-a-self-signed-x509-certificate"></a>Erstellen ein selbstsigniertes\-signiertes x. 509-Zertifikat

Sie können ein selbstsigniertes x. 509-Zertifikat erstellen und exportieren Sie es mit dem privaten Schlüssel \(mit einem Kennwort geschützt\) mit folgenden Schritten für einzelne\-Knoten und mehreren\-knotenbereitstellungen des Netzwerkcontrollers .

Beim Erstellen von Self-Service\-selbstsignierten Zertifikaten verwenden, können Sie die folgenden Richtlinien.

- Sie können die IP-Adresse der Netzwerk-Controller-REST-Endpunkt für den DNS-Name-Parameter -, aber dies wird nicht empfohlen, da sie erfordert, dass die Netzwerkcontroller-Knoten alle in einem einzelnen Management-Subnetz befinden \(z. B. auf einem einzelnen Rack\)
- Der DNS-Namen, die Sie angeben, werden für mehrere knotenbereitstellungen für NC-, den FQDN des Clusters Network Controller \(DNS-Host-A-Datensätze werden automatisch erstellt.\) 
- Für Bereitstellungen für einzelne Knoten Netzwerkcontroller kann der DNS-Namen des Netzwerkcontrollers, Hostname, gefolgt von den vollständigen Domänennamen sein.

#### <a name="multiple-node"></a>Mehrere Knoten

Sie können die [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell-Befehl erstellen Sie ein selbstsigniertes\-signiertes Zertifikat.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**Beispiel für die Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>Einzelner Knoten

Sie können die [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell-Befehl erstellen Sie ein selbstsigniertes\-signiertes Zertifikat.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**Beispiel für die Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>Erstellen eine Zertifizierungsstelle\-signiertes x. 509-Zertifikat

Um ein Zertifikat von einer Zertifizierungsstelle zu erstellen, Sie müssen bereits bereitgestellt haben eine Public Key-Infrastruktur \(PKI\) mit Active Directory Certificate Services \(AD CS\). 

>[!NOTE]
>Sie können Drittanbieter-Zertifizierungsstellen oder Tools wie Openssl, verwenden, um ein Zertifikat zur Verwendung mit Netzwerkcontroller, zu erstellen, aber die Anweisungen in diesem Thema an AD CS spezifisch sind. Um zu erfahren, wie Sie eine Drittanbieter-Zertifizierungsstelle oder ein Tool verwenden, finden Sie in der Dokumentation für die Software, die Sie verwenden.

Erstellen ein Zertifikat mit einer Zertifizierungsstelle enthält die folgenden Schritte aus.

1. Sie oder Ihre Organisation Domäne oder Sicherheitsadministrator wird die Zertifikatvorlage konfiguriert.
2. Sie oder Ihre Organisation Network Controller-Administratoren oder SCVMM-Administrator fordert bei der Zertifizierungsstelle ein neues Zertifikat.

#### <a name="certificate-configuration-requirements"></a>Zertifikatanforderungen für die Konfiguration

Während Sie im nächsten Schritt eine Zertifikatvorlage konfigurieren, stellen Sie sicher, dass die Vorlage, die Sie konfigurieren die folgenden erforderlichen Elemente enthält.

1. Antragstellername des Zertifikats muss den FQDN des Hyper-V-Host sein.
2. Das Zertifikat muss im persönlichen Speicher lokalen Computers abgelegt werden (Meine – Cert: \localmachine\my)
3. Das Zertifikat muss beide Server-Authentifizierung verfügen (EKU: 1.3.6.1.5.5.7.3.1) und die Clientauthentifizierung (EKU: 1.3.6.1.5.5.7.3.2) Richtlinien für die Anwendungen.

>[!NOTE]
>Wenn das Personal \(Meine – Cert: \localmachine\my\) Zertifikatspeicher auf dem Hyper\-V-Host hat mehr als ein x. 509-Zertifikat mit Betreff Name (CN) wie der Host vollständig qualifizierten Domänennamens \(FQDN\), Stellen Sie sicher, dass das Zertifikat, das von SDN verwendet werden, eine zusätzliche benutzerdefinierte Enhanced Key Usage-Eigenschaft mit der OID 1.3.6.1.4.1.311.95.1.1.1 verfügt. Andernfalls funktioniert die Kommunikation zwischen Netzwerkcontroller und dem Host möglicherweise nicht.

#### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage
  
>[!NOTE]
>Bevor Sie dieses Verfahren durchführen, prüfen Sie die zertifikatanforderungen und verfügbaren Zertifikatvorlagen in der Verwaltungskonsole für Zertifikatvorlagen. Sie können entweder eine vorhandene Vorlage ändern oder erstellen Sie ein Duplikat einer vorhandenen Vorlage und dann die Kopie der Vorlage ändern. Erstellen eine Kopie einer vorhandenen Vorlage wird empfohlen.

1. Klicken Sie auf dem Server, auf dem AD CS, im Server-Manager installiert ist auf **Tools**, und klicken Sie dann auf **Zertifizierungsstelle**. Die Microsoft-Verwaltungskonsole \(MMC\) wird geöffnet. 
2. Doppelklicken Sie in der MMC auf den Zertifizierungsstellennamen, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **verwalten**.
3. Die Zertifikatvorlagenkonsole wird geöffnet. Alle Zertifikatvorlagen werden im Detailbereich angezeigt.
4. Klicken Sie im Detailbereich auf die Vorlage, die Sie duplizieren möchten.
5.  Klicken Sie auf die **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Die Vorlage **Eigenschaften** Dialogfeld wird geöffnet.
6.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Antragstellername** auf **Geben Sie in der Anforderung**. \(Diese Einstellung ist für die Netzwerk-Controller-SSL-Zertifikate erforderlich.\)
7.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Anforderungsverarbeitung** sicher, dass **privatem Schlüssel zulassen zu exportierenden** ausgewählt ist. Stellen Sie außerdem sicher, dass die **Signatur- und verschlüsselungselemente** Zweck ausgewählt ist.
8.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Erweiterungen** Registerkarte **Schlüsselverwendung**, und klicken Sie dann auf **bearbeiten**.
9.  In **Signatur**, sicher, dass **digitale Signatur** ausgewählt ist.
10.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Erweiterungen** Registerkarte **Anwendungsrichtlinien**, und klicken Sie dann auf **bearbeiten**.
11.  In **Anwendungsrichtlinien**, sicher, dass **Clientauthentifizierung** und **Serverauthentifizierung** aufgeführt sind.
12.  Speichern Sie die Kopie der Zertifikatvorlage durch einen eindeutigen Namen, z. B. **Netzwerkcontroller Vorlage**.

#### <a name="to-request-a-certificate-from-the-ca"></a>Von der Zertifizierungsstelle ein Zertifikat anfordern

Sie können das Zertifikate-Snap-in zum Anfordern von Zertifikaten verwenden. Sie können jede Art von Zertifikat anfordern, die vorkonfiguriert und zur Verfügung gestellt, von einem Administrator der Zertifizierungsstelle, die die Anforderung verarbeitet wurde.

**Benutzer** oder lokale **Administratoren** mindestens Mitglied der Gruppe zum Durchführen dieses Verfahrens erforderlich ist.

1. Öffnen Sie das Zertifikate-Snap-in für einen Computer an.
2. Klicken Sie in der Konsolenstruktur auf **Zertifikate \(lokalen Computer\)** . Wählen Sie die **persönliche** Zertifikatspeicher.
3. Auf der **Aktion** , zeigen Sie auf ** alle Aufgaben<strong>, und klicken Sie dann auf ** Neues Zertifikat anfordern</strong> zum Starten des Assistenten für die Registrierung von Zertifikaten. Klicken Sie auf **Weiter**.
4. Wählen Sie die **von Ihrem Administrator konfiguriert** Certificate Enrollment-Richtlinie, und klicken Sie auf **Weiter**.
5. Wählen Sie die **Active Directory-Registrierungsrichtlinie** \(basierend auf der ZS-Vorlage, die Sie im vorherigen Abschnitt konfiguriert\).
6. Erweitern Sie die **Details** aus und konfigurieren Sie die folgenden Elemente.
   1. Sicherstellen, dass **Schlüsselverwendung** enthält die beiden <strong>digitale Signatur ** und ** Schlüsselverschlüsselung</strong>.
   2. Sicherstellen, dass **Anwendungsrichtlinien** enthält die beiden **Serverauthentifizierung** \(1.3.6.1.5.5.7.3.1\) und **Clientauthentifizierung** \(1.3.6.1.5.5.7.3.2\).
7. Klicken Sie auf **Eigenschaften**.
8. Auf der **Betreff** Registerkarte **Antragstellername**im **Typ**Option **allgemeiner Name**. Geben Sie in "Wert" **Network Controller-REST-Endpunkt**.
9. Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.
10. Klicken Sie auf **Registrieren**.

Das Zertifikate-MMC klicken Sie auf dem persönlichen Speicher, um das Zertifikat anzuzeigen, die, das Sie von der Zertifizierungsstelle registriert haben.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>Exportieren und kopieren das Zertifikat in der SCVMM-Bibliothek

Nach dem Erstellen entweder ein selbstsigniertes\-signiert oder von einer Zertifizierungsstelle\-signiertes Zertifikat verwenden, müssen Sie das Zertifikat mit dem privaten Schlüssel exportieren \(im PFX-Format\) und ohne den privaten Schlüssel \(im Base64-CER-Format\) aus dem Zertifikate-Snap-in. 

Dann müssen Sie die beiden exportierten Dateien zum Kopieren der **ServerCertificate.cr** und **"nccertificate.CR"** Ordnern, die Sie angegeben haben, die zum Zeitpunkt beim Importieren der Dienstvorlage NC.

1. Öffnen Sie das Zertifikate-Snap-in (certlm.msc), und suchen Sie das Zertifikat im persönlichen Zertifikatspeicher für den lokalen Computer.
2. Rechts\-klicken Sie auf das Zertifikat, klicken Sie auf **alle Aufgaben**, und klicken Sie dann auf **exportieren**. Der Zertifikatexport-Assistent wird geöffnet. Klicken Sie auf **Weiter**.
3. Wählen Sie **Ja**, exportieren Sie die Option für private Schlüssel, klicken Sie auf **Weiter**.
4. Wählen Sie **privater Informationsaustausch – PKCS #12 (. PFX)** und übernehmen Sie die Standardeinstellung **alle Zertifikate im Zertifizierungspfad einbeziehen** Wenn möglich.
5. Weisen Sie dem Benutzer/Gruppen und ein Kennwort für das Zertifikat, das Sie exportieren, klicken Sie auf **Weiter**.
6. Klicken Sie auf der Seite zu exportierende Datei durchsuchen Sie den Pfad, in dem Sie die exportierte Datei speichern möchten, und geben sie einen Namen.
7. Exportieren Sie außerdem das Zertifikat im. CER-Format. Hinweis: Zu exportieren. CER-Format, deaktivieren Sie die "Ja", Option für private Schlüssel zu exportieren.
8. Kopieren der. PFX zu dem Ordner "ServerCertificate.cr".
9. Kopieren der. CER-Datei in den Ordner "nccertificate.CR".

Wenn Sie fertig sind, aktualisieren Sie diese Ordner in der SCVMM-Bibliothek, und stellen Sie sicher, dass Sie diese Zertifikate kopiert haben. Setzen Sie die Netzwerkkonfiguration für die Vorlage von Controller-Dienst und die Bereitstellung.

## <a name="authenticating-southbound-devices-and-services"></a>Authentifizieren von Southbound-Geräten und Diensten 

Die Controller-Netzwerkkommunikation mit Hosts und Geräte für SLB MUX verwendet Zertifikate zur Authentifizierung an. Kommunikation mit den Hosts ist über OVSDB-Protokoll, während der Kommunikation mit der SLB MUX-Geräte über das WCF-Protokoll ist.

### <a name="hyper-v-host-communication-with-network-controller"></a>Hyper-V-Host-Kommunikation mit Netzwerkcontroller

Für die Kommunikation mit den Hyper-V-Hosts über OVSDB muss Netzwerkcontroller ein Zertifikat auf dem Hostcomputer bereitstellen. In der Standardeinstellung SCVMM übernimmt das SSL-Zertifikat konfiguriert werden, auf dem Netzwerkcontroller und wird für die southbound-Kommunikation mit den Hosts verwendet.

Dies ist der Grund, warum das SSL-Zertifikat der konfigurierten Clientauthentifizierungs-EKU aufweisen muss. Dieses Zertifikat wird auf "Server" REST konfiguriert Ressource \(Hyper-V-Hosts werden in den Netzwerkcontroller wie ein Server-Ressource dargestellt\), und können angezeigt werden, mit dem Windows PowerShell-Befehl  **Get-NetworkControllerServer**.

Es folgt ein teilbeispiel des Servers REST-Ressource.

      "resourceId": "host31.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "host31.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

Bei der gegenseitigen Authentifizierung benötigen des Hyper-V-Hosts außerdem ein Zertifikat für die Kommunikation mit Netzwerkcontroller. 

Sie können das Zertifikat von einer Zertifizierungsstelle registrieren \(Zertifizierungsstelle\). Wenn das Zertifikat einer Zertifizierungsstelle, die basierend auf dem Hostcomputer nicht gefunden wird, kann SCVMM erstellt ein selbstsigniertes Zertifikat und wird auf dem Hostcomputer bereitgestellt.

Netzwerkcontroller und die Hyper-V-Host-Zertifikate müssen gegenseitig vertrauen. Stammzertifikat für das Hyper-V-hostzertifikat muss vorliegen, in der Netzwerk-Controller vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer (und umgekehrt). 

Bei der Verwendung von Self-Service\-selbstsignierten Zertifikaten, SCVMM wird sichergestellt, dass die erforderlichen Zertifikate im Speicher Vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer vorhanden sind. 

Wenn Sie Zertifizierungsstellen basierende Zertifikate für die Hyper-V-Hosts verwenden, müssen Sie sicherstellen, dass die Zertifizierungsstellen-Stammzertifikat für den Netzwerkcontroller vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer vorhanden ist.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>Software Load Balancer-MUX-Kommunikation mit Netzwerkcontroller

Den Software Load Balancer-Multiplexer \(MUX\) und Netzwerkcontroller kommunizieren über das WCF-Protokoll, das mithilfe von Zertifikaten für die Authentifizierung.

In der Standardeinstellung SCVMM übernimmt das SSL-Zertifikat auf dem Netzwerkcontroller konfiguriert und verwendet es für die southbound-Kommunikation mit den Geräten MUX-Instanz. Dieses Zertifikat wird auf der "NetworkControllerLoadBalancerMux" konfiguriert, dass REST-Ressourcen und können angezeigt werden, indem Sie Ausführung des Powershell-Cmdlets **Get-NetworkControllerLoadBalancerMux**.

Beispiel für MUX-REST-Ressource \(teilweise\):

      "resourceId": "slbmux1.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "slbmux1.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

Bei der gegenseitigen Authentifizierung müssen Sie auch ein Zertifikat verfügen, auf den SLB MUX-Geräten. Dieses Zertifikat wird automatisch von SCVMM konfiguriert, beim Bereitstellen von Software Load Balancer mit SCVMM.

>[!IMPORTANT]
>Auf dem Host und die SLB-Knoten, es ist wichtig, dass der Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen keines Zertifikat enthält, der "ausgestellt" entspricht nicht der "Ausgestellt von". In diesem Fall schlägt die Kommunikation zwischen Netzwerkcontroller und die southbound-Gerät.

Netzwerkcontroller und der SLB MUX-Zertifikate müssen vertrauenswürdig sein miteinander \(Stammzertifikat der SLB MUX-Zertifikat muss in den Speicher vertrauenswürdiger Stammzertifizierungsstellen des Netzwerkcontrollers-Computer vorhanden sein und umgekehrt\). Bei der Verwendung von Self-Service\-selbstsignierten Zertifikaten, SCVMM stellt sicher, dass die erforderlichen Zertifikate vorhanden, in der in der vertrauenswürdigen Stammzertifizierungsstellen für den lokalen Computer zu speichern.



