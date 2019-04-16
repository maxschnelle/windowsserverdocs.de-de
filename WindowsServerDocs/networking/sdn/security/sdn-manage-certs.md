---
title: Verwalten von Zertifikaten für Software-Networking Defined
description: Sie können in diesem Thema verwenden, finden Sie Informationen zum Verwalten von Zertifikaten für die Netzwerk-Controller Northbound und Southbound Kommunikation, bei der Bereitstellung von Software Defined Networking (SDN) in Windows Server2016 Datacenter.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3036de9161cabc2f3a85a1d3b2ce7739f0ff6bd3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-certificates-for-software-defined-networking"></a>Verwalten von Zertifikaten für Software-Networking Defined

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema finden Sie Informationen zum Verwalten von Zertifikaten für Netzwerk-Controller Northbound und Southbound Kommunikation, wenn Sie die Software Defined Networking \(SDN\) in Windows Server2016 Datacenter bereitstellen und Sie System Center Virtual Machine Manager-\(SCVMM\) als Ihre SDN-Verwaltungsclient verwenden verwenden.

>[!NOTE]
>Übersicht über Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](../technologies/network-controller/Network-Controller.md).

Wenn Sie Kerberos nicht zum Sichern der Kommunikation Netzwerkcontroller verwenden, können Sie die x. 509-Zertifikate für Authentifizierung, Autorisierung und Verschlüsselung.

In Windows Server2016 Datacenter SDN unterstützt sowohl mit deren Hilfe signiert und Zertifizierungsstelle \ (CA\)-signierte x. 509-Zertifikate. Dieses Thema enthält eine schrittweise Anleitung zum Erstellen dieser Zertifikate und diese anwenden zum Sichern von Netzwerk-Controller Northbound Kommunikationskanäle mit Management-Clients und für die Southbound-Kommunikation mit Netzwerkgeräten, z.B. die Software Load Balancers \(SLB\).
.
Wenn Sie Certificate\-basierte Authentifizierung verwenden, müssen Sie ein Zertifikat auf dem Netzwerkcontroller Knoten registrieren, die auf folgende Weise verwendet wird.

1. Verschlüsseln der Northbound Kommunikation mit Secure Sockets Layer-\(SSL\) zwischen Netzwerkcontroller Knoten und Management-Clients, z.B. System Center Virtual Machine Manager.
2. Authentifizierung zwischen Knoten Netzwerkcontroller und Southbound Geräte und Dienste, z.B. Hyper-V-Hosts und Software Load Balancers \(SLBs\).

## <a name="creating-and-enrolling-an-x509-certificate"></a>Erstellen und registrieren ein x. 509-Zertifikat

Sie erstellen und Registrieren einer deren Hilfe signiertes Zertifikat oder ein Zertifikat, das von einer Zertifizierungsstelle ausgestellt wurde.

>[!NOTE]
>Wenn Sie zum Bereitstellen von Netzwerkcontroller SCVMM verwenden, müssen Sie das x. 509-Zertifikat angeben, das zum Verschlüsseln der Northbound Kommunikation während der Konfiguration der Netzwerk-Controller-Dienstvorlage verwendet wird.

Die Konfiguration des Zertifikats muss die folgenden Werte enthalten.

- Der Wert für die **RestEndPoint** Textfeld muss die \(FQDN\) Network Controller vollqualifizierter Domänenname oder IP-Adresse sein. 
- Die **RestEndPoint** Wert muss der Name des Antragstellers entsprechen \ (Common Name, CN\) des x. 509-Zertifikats.

### <a name="creating-a-self-signed-x509-certificate"></a>Erstellen eines signierten mit deren Hilfe x. 509-Zertifikats

Sie können ein selbstsigniertes x. 509-Zertifikat zu erstellen und es mit dem privaten Schlüssel exportieren \ (mit einer Password\ geschützt) folgende Schrittefür die Singlethread-Knoten und Listenfeld Bereitstellung von Netzwerk-Controller.

Wenn Sie mit deren Hilfe signierte Zertifikate erstellen, können Sie die folgenden Richtlinien.

- Sie können die IP-Adresse der Netzwerk-Controller-REST-Endpunkt für den DNS-Name-Parameter -, aber dies wird nicht empfohlen, da sie erfordert, dass die Netzwerk-Controller-Knoten alle in einem einzigen Management-Subnetz befinden \ (z.B. auf einem einzelnen Rack\)
- Für mehrere Knoten NC-Bereitstellungen, der DNS-Namen, den Sie angeben, werden den FQDN des Clusters Controller Netzwerk \ (DNS-Host-A-Datensätze werden automatisch erstellt. \) 
- Für die einzelnen Knoten Netzwerkcontroller Bereitstellungen kann der DNS-Name der Netzwerkcontroller Hostnamen gefolgt von dem Domänennamen sein.

#### <a name="multiple-node"></a>Mehrere Knoten

Sie können die [New-SelfSignedCertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell-Befehl zum Erstellen eines Zertifikats mit deren Hilfe signiert.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**Beispiel für die Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>Einem einzelnen Knoten

Sie können die [New-SelfSignedCertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell-Befehl zum Erstellen eines Zertifikats mit deren Hilfe signiert.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**Beispiel für die Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>Erstellen eines CA\ signierte x. 509-Zertifikats

Um ein Zertifikat einer Zertifizierungsstelle mit erstellen, müssen Sie bereits eine Public Key-Infrastruktur \(PKI\) mit Active Directory Certificate Services \(AD CS\) bereitgestellt. 

>[!NOTE]
>Drittanbieter-Zertifizierungsstellen oder Tools, z.B. Openssl, können ein Zertifikat für die Verwendung mit Netzwerkcontroller, erstellen, aber die Anweisungen in diesem Thema für AD CS spezifisch sind. Um erfahren Sie, wie Sie eine Drittanbieter-Zertifizierungsstelle oder ein Tool verwenden, finden Sie in der Dokumentation für die Software, die Sie verwenden.

Erstellen ein Zertifikat mit einer Zertifizierungsstelle umfasst die folgenden Schritteaus.

1. Sie oder Ihre Domäne oder Organisation Sicherheitsadministrator konfiguriert die Zertifikatvorlage
2. Sie oder Ihre Organisation Controller Netzwerkadministrator oder SCVMM-Administrator fordert ein neues Zertifikat von der Zertifizierungsstelle.

#### <a name="certificate-configuration-requirements"></a>Konfiguration von Zertifikatanforderungen

Während Sie im nächsten Schritteine Zertifikatvorlage konfigurieren, stellen Sie sicher, dass die Vorlage, die Sie konfigurieren die folgenden erforderlichen Elemente enthält.

1. Der Antragstellername des Zertifikats muss den FQDN des Hyper-V-Host sein.
2. Das Zertifikat muss im persönlichen Speicher lokalen Computers platziert werden (Meine – Cert: \localmachine\my)
3. Das Zertifikat muss sowohl Serverauthentifizierung enthalten (EKU: 1.3.6.1.5.5.7.3.1) und Client-Authentifizierung (EKU: 1.3.6.1.5.5.7.3.2) Anwendungsrichtlinien.

>[!NOTE]
>Wenn der persönliche \ (Meine – Cert: \localmachine\my\) Zertifikat Store auf dem Hyper\-V-Host hat mehr als ein x. 509 certificate mit Betreff Name (CN) wie des Hosts \(FQDN\) Fully Qualified Domain Name, stellen Sie sicher, dass das Zertifikat, das von SDN verwendet werden, eine zusätzliche benutzerdefinierte Enhanced Key Usage-Eigenschaft mit der OID 1.3.6.1.4.1.311.95.1.1.1 verfügt. Andernfalls funktioniert die Kommunikation zwischen Netzwerkcontroller und dem Host möglicherweise nicht.

#### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage
  
>[!NOTE]
>Bevor Sie dieses Verfahren ausführen, sollten Sie die Zertifikatanforderungen und die verfügbaren Zertifikatvorlagen in die Zertifikatvorlagenkonsole überprüfen. Sie können entweder eine vorhandene Vorlage ändern oder erstellen Sie ein Duplikat einer vorhandenen Vorlage und ändern Sie Ihre Kopie der Vorlage. Wird empfohlen, eine Kopie einer vorhandenen Vorlage erstellen.

1. Klicken Sie auf dem Server, auf dem AD CS wird, wird im Server-Manager installiert, auf **Tools**, und klicken Sie dann auf **Zertifizierungsstelle**. Die Microsoft-Verwaltungskonsole \(MMC\) wird geöffnet. 
2. Doppelklicken Sie in der MMC auf den Namen der Zertifizierungsstelle, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **verwalten**.
3. Die Zertifikatvorlagenkonsole wird geöffnet. Alle Zertifikatvorlagen werden im Detailbereich angezeigt.
4. Klicken Sie im Detailbereich auf die Vorlage, die Sie duplizieren möchten.
5.  Klicken Sie auf die **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Die Vorlage **Eigenschaften** Dialogfeld wird geöffnet.
6.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Antragstellername** auf **Geben Sie in der Anforderung**. \ (Diese Einstellung ist für die Controller-SSL-Zertifikate erforderlich. \)
7.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Anforderungsverarbeitung** sicher, dass der **Exportieren von privatem Schlüssel zulassen** ausgewählt ist. Außerdem sicherstellen, dass die **Signatur und Verschlüsselung** Zweck ausgewählt ist.
8.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Erweiterungen** Registerkarte **Schlüsselverwendung**, und klicken Sie dann auf **bearbeiten**.
9.  In **Signatur**, stellen Sie sicher, dass **digitale Signatur** ausgewählt ist.
10.  In der Vorlage **Eigenschaften** Dialogfeld auf die **Erweiterungen** Registerkarte **Anwendungsrichtlinien**, und klicken Sie dann auf **bearbeiten**.
11.  In **Anwendungsrichtlinien**, stellen Sie sicher, dass **Clientauthentifizierung** und **Serverauthentifizierung** aufgeführt sind.
12.  Speichern Sie die Kopie der Zertifikatvorlage mit einem eindeutigen Namen, z.B. **Netzwerkcontroller Vorlage**.

#### <a name="to-request-a-certificate-from-the-ca"></a>Von der Zertifizierungsstelle ein Zertifikat anfordern

Sie können das Zertifikate-Snap-In zum Anfordern von Zertifikaten verwenden. Sie können jede Art von Zertifikat anfordern, die vorkonfiguriert und zur Verfügung gestellt, durch den Administrator der Zertifizierungsstelle, die die Anforderung verarbeitet wurde.

**Benutzer** oder lokalen **Administratoren** mindestens Mitglied der Gruppe zum Durchführen dieses Verfahrens erforderlich ist.

1. Öffnen Sie die Zertifikate-Snap-In für einen Computer.
2. Klicken Sie in der Konsolenstruktur auf **Zertifikate \(Local Computer\)**. Wählen Sie die **persönliche** Zertifikatspeicher.
3. Auf der **Aktion** auf ** alle Aufgaben **, und klicken Sie dann auf **neues Zertifikat anfordern** auf den Zertifikatregistrierungs-Assistenten zu starten. Klicken Sie auf **Weiter**.
4. Wählen Sie die **vom Administrator konfiguriert** Zertifikatregistrierungsrichtlinie und klicken Sie auf **Weiter**.
5. Wählen Sie die **Active Directory-Registrierungsrichtlinie** \ (basierend auf der CA-Vorlage, die Sie in der vorherigen Section\ konfiguriert).
6. Erweitern Sie die **Details** Abschnitt, und konfigurieren Sie die folgenden Elemente.
    1. Stellen Sie sicher, dass **Schlüssel Nutzung** beinhaltet ** digitale Signatur ** und **Schlüsselverschlüsselung**.
    2. Stellen Sie sicher, dass **Anwendungsrichtlinien** beinhaltet **Serverauthentifizierung** \(1.3.6.1.5.5.7.3.1\) und **Clientauthentifizierung** \(1.3.6.1.5.5.7.3.2\).
7. Klicken Sie auf **Eigenschaften**.
8. Auf der **Betreff** Registerkarte **Antragstellername**im **Typ**Option **allgemeiner Name**. Geben Sie im Feld Wert **Netzwerk-Controller-REST-Endpunkt**.
9. Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.
10. Klicken Sie auf **registrieren**.

Klicken Sie in der MMC-Zertifikate auf den persönlichen Speicher des Zertifikats anzeigen, die Sie von der Zertifizierungsstelle registriert haben.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>Exportieren und kopieren das Zertifikat in der SCVMM-Bibliothek

Nach dem Erstellen eines Zertifikats signiert mit deren Hilfe oder CA\ angemeldet haben, müssen Sie das Zertifikat mit dem privaten Schlüssel exportieren \(in.pfx Format\) und ohne den privaten Schlüssel \ (in Base64-CER-Format) in das Zertifikate-Snap-In. 

Sie müssen die beiden exportierten Dateien zum Kopieren der **ServerCertificate.cr** und **NCCertificate.cr** Ordner, die Sie zu dem Zeitpunkt angegeben beim Importieren von der Dienstvorlage NC.

1. Öffnen Sie das Zertifikate-Snap-In (certlm.msc), und suchen Sie das Zertifikat in den persönlichen Zertifikatspeicher des lokalen Computers.
2. Klicken Sie mit der rechten Maustaste auf das Zertifikat auf **alle Aufgaben**, und klicken Sie dann auf **exportieren**. Der Zertifikatexport-Assistent wird geöffnet. Klicken Sie auf **Weiter**.
3. Wählen Sie **Ja**, exportieren Sie die Option für private Schlüssel, klicken Sie auf **Weiter**.
4. Wählen Sie **privater Informationsaustausch – PKCS 12 (.PFX)** und akzeptieren Sie die Standardeinstellung, **, alle Zertifikate im Zertifizierungspfad einbeziehen** Wenn möglich.
5. Weisen Sie dem Benutzer/Gruppen und ein Kennwort für das Zertifikat, das Sie exportieren, klicken Sie auf **Weiter**.
6. Durchsuchen Sie auf der Seite zu exportieren den Pfad, in dem die exportierte Datei erstellt werden soll, und geben sie einen Namen.
7. Auf ähnliche Weise Exportieren des Zertifikats in. CER-Format. Hinweis: Um zu exportieren. CER-Format, deaktivieren Sie die Option Ja, exportieren die Option für private Schlüssel.
8. Kopieren der. PFX in den Ordner ServerCertificate.cr.
9. Kopieren der. CER-Datei in den Ordner NCCertificate.cr.

Wenn Sie fertig sind, aktualisieren Sie diese Ordner in der Bibliothek SCVMM, und stellen Sie sicher, dass Sie diese Zertifikate kopiert haben. Fahren Sie mit der Netzwerkdienst Controller-Vorlagenkonfiguration und Bereitstellung.

## <a name="authenticating-southbound-devices-and-services"></a>Authentifizieren von Southbound-Geräten und Diensten 

Die Controller-Netzwerkkommunikation mit Hosts und SLB MUX-Geräten werden Zertifikate für die Authentifizierung verwendet. Kommunikation mit den Hosts ist über OVSDB Protokoll, während die Kommunikation mit den SLB MUX-Geräten über das WCF-Protokoll ist.

### <a name="hyper-v-host-communication-with-network-controller"></a>Hyper-V-Host-Kommunikation mit Netzwerkcontroller

Für die Kommunikation mit der Hyper-V-Hosts über OVSDB muss Netzwerkcontroller ein Zertifikat auf dem Hostcomputer an. In der Standardeinstellung SCVMM wählt das SSL-Zertifikat auf dem Controller Netzwerk konfiguriert und für die southbound-Kommunikation mit den Hosts verwendet.

Dies ist der Grund, warum das SSL-Zertifikat der Client konfiguriert EKU für Serverauthentifizierung muss. Dieses Zertifikat wird auf "Server" REST konfiguriert Ressource \ (Hyper-V-Hosts sind im Netzwerkcontroller als ein Server Resource\ dargestellt) und können mit dem Windows PowerShell-Befehl angezeigt werden **Get-NetworkControllerServer**.

Es folgt ein Beispiel für Teil des Servers REST-Ressource.

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

Hyper-V-Host muss auch ein Zertifikat zur Kommunikation mit Netzwerkcontroller verfügen, für die gegenseitige Authentifizierung. 

Sie können das Zertifikat von einer Zertifizierungsstelle \(CA\) registrieren. Wenn ein Zertifizierungsstellenzertifikat basierend auf dem Hostcomputer nicht gefunden wird, wird SCVMM erstellt ein selbstsigniertes Zertifikat und stellt es auf dem Hostcomputer.

Netzwerkcontroller und die Hyper-V-Host-Zertifikate müssen jeweils anderen vertrauenswürdig sein. Das Hyper-V-Host-Zertifikat Stammzertifikats muss in vorhanden sein, die Netzwerk-Controller vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer (und umgekehrt) zu speichern. 

Wenn Sie mit deren Hilfe signierte Zertifikate verwenden, gewährleistet SCVMM, dass die erforderlichen Zertifikate im Speicher vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer vorhanden sind. 

Wenn Sie basierende Zertifizierungsstellenzertifikate für die Hyper-V-Hosts verwenden, müssen Sie sicherstellen, dass das Stammzertifikat der Zertifizierungsstelle auf dem Netzwerkcontroller vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer vorhanden ist.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>Software Load Balancer MUX-Kommunikation mit Netzwerkcontroller

Die Software Load Balancer Multiplexor \(MUX\) und Netzwerkcontroller kommunizieren über das Protokoll WCF mithilfe von Zertifikaten für die Authentifizierung.

In der Standardeinstellung SCVMM wählt das SSL-Zertifikat auf dem Controller Netzwerk konfiguriert und für die southbound-Kommunikation mit den Mux-Geräten verwendet. Dieses Zertifikat wird auf die "NetworkControllerLoadBalancerMux" konfiguriert, die Ressource zu positionieren und können durch Ausführen des PowerShell-Cmdlets angezeigt werden **Get-NetworkControllerLoadBalancerMux**.

Beispiel für die Ressource \(partial\) MUX-REST:

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

Für die gegenseitige Authentifizierung müssen Sie auch ein Zertifikat auf den Geräten SLB MUX verfügen. Dieses Zertifikat wird von SCVMM automatisch konfiguriert, bei der Bereitstellung von Software Load Balancers mit SCVMM.

>[!IMPORTANT]
>Auf dem Host und SLB Knoten, es ist wichtig, dass keine Zertifikate in der Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen enthalten ist "ausgestellt" ist nicht identisch mit "Ausgestellt von". In diesem Fall schlägt die Kommunikation zwischen Netzwerkcontroller und dem southbound-Gerät.

Netzwerkcontroller und dem SLB MUX-Zertifikate müssen als vertrauenswürdig festgelegt sein jeweils anderen \ (das SLB MUX-Zertifikat Stammzertifikats muss auf dem Computer Netzwerkcontroller vertrauenswürdige Stammzertifizierungsstellen speichern und umgekehrt Versa\ vorhanden sein). Wenn Sie mit deren Hilfe signierte Zertifikate verwenden, SCVMM wird sichergestellt, dass die erforderlichen Zertifikate vorhanden, in der in den Speicher vertrauenswürdiger Stammzertifizierungsstellen für den lokalen Computer zu speichern.



