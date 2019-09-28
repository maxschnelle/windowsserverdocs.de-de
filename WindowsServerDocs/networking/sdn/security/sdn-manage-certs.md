---
title: Verwalten von Zertifikaten für Software-Defined Networking
description: In diesem Thema erfahren Sie, wie Sie bei der Bereitstellung von Software-Defined Networking (SDN) in Windows Server 2016 Datacenter die Zertifikate für die Kommunikation zwischen dem Netzwerk Controller und der Southbound-Kommunikation verwalten.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: b1cff080630c68ee8c4b7f0904f8fd0978330edc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405987"
---
# <a name="manage-certificates-for-software-defined-networking"></a>Verwalten von Zertifikaten für Software-Defined Networking

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie bei der Bereitstellung von Software-Defined Networking \(-Sdn\) in Windows Server 2016 Datacenter die Zertifikate für den Netzwerk Controller in der Northbound-und der Southbound-Kommunikation verwalten, und Sie verwenden System Zentrieren \(Sie Virtual Machine Manager SCVMM\) als Sdn-Verwaltungs Client.

>[!NOTE]
>Eine Übersicht über den Netzwerk Controller finden Sie unter [Netzwerk Controller](../technologies/network-controller/Network-Controller.md).

Wenn Sie Kerberos nicht zum Sichern der Netzwerk Controller Kommunikation verwenden, können Sie X. 509-Zertifikate für Authentifizierung, Autorisierung und Verschlüsselung verwenden.

Der Sdn in Windows Server 2016 Datacenter unterstützt\-die von der \(Zertifizierungs\)Stelle signierten X. 509-Zertifikate. Dieses Thema enthält Schritt-für-Schritt-Anleitungen zum Erstellen dieser Zertifikate und zum Anwenden dieser Zertifikate, um Kanäle für die Kommunikation mit dem Netzwerk Controller mit Verwaltungs Clients und die intranetgebundene Kommunikation mit Netzwerkgeräten, z. b. der Software Load Balancer \(SLB\).
.
Wenn Sie die Zertifikat\-basierte Authentifizierung verwenden, müssen Sie ein Zertifikat auf den Netzwerk Controller Knoten registrieren, die wie folgt verwendet werden.

1. Verschlüsseln der Northbound-Kommunikation mit \(Secure Sockets Layer\) SSL zwischen Netzwerk Controller Knoten und Verwaltungs Clients, z. b. System Center Virtual Machine Manager.
2. Authentifizierung zwischen Netzwerk Controller Knoten und in der Mitte befindlichen Geräten und Diensten, z. b. Hyper-V-Hosts \(und Software\)Lastenausgleichs-SLB.

## <a name="creating-and-enrolling-an-x509-certificate"></a>Erstellen und Anmelden eines X. 509-Zertifikats

Sie können entweder ein selbst\-signiertes Zertifikat oder ein Zertifikat, das von einer Zertifizierungsstelle ausgestellt wurde, erstellen und registrieren.

>[!NOTE]
>Wenn Sie SCVMM zur Bereitstellung des Netzwerk Controllers verwenden, müssen Sie das X. 509-Zertifikat angeben, das bei der Konfiguration der Netzwerk Controller-Dienst Vorlage zum Verschlüsseln der Northbound-Kommunikation verwendet wird.

Die Zertifikat Konfiguration muss die folgenden Werte enthalten.

- Der Wert für das Textfeld **restendpoint** muss entweder der voll qualifizierte Domänen Name \(-FQDN\) oder die IP-Adresse des Netzwerk Controllers sein. 
- Der **restendpoint** -Wert muss mit dem Antrags \(Teller Namen Common Name\) , CN des X. 509-Zertifikats identisch sein.

### <a name="creating-a-self-signed-x509-certificate"></a>Erstellen eines selbst\-signierten X. 509-Zertifikats

Sie können ein selbst signiertes X. 509-Zertifikat erstellen und es mit dem privaten Schlüssel \(exportieren, der mit\) einem Kennwort geschützt ist,\-indem Sie die\-folgenden Schritte für die bereit Stellungen einzelner Knoten und mehrerer Knoten des Netzwerk Controllers ausführen. .

Wenn Sie selbst\-signierte Zertifikate erstellen, können Sie die folgenden Richtlinien verwenden:

- Sie können die IP-Adresse des Netzwerk Controller-Rest-Endpunkts für den DnsName-Parameter verwenden. Dies wird jedoch nicht empfohlen, da es erforderlich ist, dass sich die Netzwerk Controller Knoten alle \(innerhalb eines einzelnen Verwaltungssubnetzes befinden, z. b. in einem einzigen Rack.\)
- Bei bereit Stellungen mit mehreren Knoten NC wird der von Ihnen angegebene DNS-Name zum FQDN des DNS-Hosts des Netzwerk \(Controller Clusters. A-Einträge werden automatisch erstellt.\) 
- Bei Netzwerk Controller Bereitstellungen mit einem einzelnen Knoten kann der DNS-Name der Hostname des Netzwerk Controllers gefolgt vom vollständigen Domänen Namen sein.

#### <a name="multiple-node"></a>Mehrere Knoten

Sie können den Windows PowerShell-Befehl " [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) " verwenden,\-um ein selbst signiertes Zertifikat zu erstellen.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**Beispiel Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>Einzelner Knoten

Sie können den Windows PowerShell-Befehl " [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) " verwenden,\-um ein selbst signiertes Zertifikat zu erstellen.

**Syntax**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**Beispiel Verwendung**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>Erstellen eines X\-. 509-Zertifikats mit einer Zertifizierungsstelle

Wenn Sie ein Zertifikat mit einer Zertifizierungsstelle erstellen möchten, müssen Sie bereits eine Public Key- \(Infrastruktur-\) PKI mit Active Directory \(AD CS\)-Zertifikat Diensten bereitgestellt haben. 

>[!NOTE]
>Sie können ZS oder Tools von Drittanbietern, wie z. b. OpenSSL, verwenden, um ein Zertifikat für die Verwendung mit dem Netzwerk Controller zu erstellen. die Anweisungen in diesem Thema beziehen sich jedoch speziell auf AD CS. Informationen zur Verwendung einer Drittanbieter-Zertifizierungsstelle oder eines Drittanbieters finden Sie in der Dokumentation für die von Ihnen verwendete Software.

Das Erstellen eines Zertifikats mit einer Zertifizierungsstelle umfasst die folgenden Schritte.

1. Die Zertifikat Vorlage wird von Ihnen oder von Ihrer Organisation konfiguriert.
2. Der Netzwerk Controller Administrator oder der SCVMM-Administrator Ihres Unternehmens fordert von der Zertifizierungsstelle ein neues Zertifikat an.

#### <a name="certificate-configuration-requirements"></a>Anforderungen an die Zertifikat Konfiguration

Beim Konfigurieren einer Zertifikat Vorlage im nächsten Schritt müssen Sie sicherstellen, dass die konfigurierten Vorlagen die folgenden erforderlichen Elemente enthalten.

1. Der Antragsteller Name des Zertifikats muss der voll qualifizierte Name des Hyper-V-Hosts sein.
2. Das Zertifikat muss sich im persönlichen Speicher des lokalen Computers befinden (My – CERT: \ LocalMachine\MY).
3. Das Zertifikat muss über eine Server Authentifizierung verfügen (EKU: 1.3.6.1.5.5.7.3.1) und Client Authentifizierung (EKU: 1.3.6.1.5.5.7.3.2) Anwendungsrichtlinien.

>[!NOTE]
>Wenn der persönliche \(My – CERT: \ LocalMachine\MY\) Certificate Store auf dem Hyper\--V-Host mehr als ein X. 509-Zertifikat mit dem Antragsteller Namen (CN) als voll qualifizierter \(Domänen Namen\)-FQDN des Hosts aufweist, Stellen Sie sicher, dass das Zertifikat, das von Sdn verwendet wird, über eine zusätzliche benutzerdefinierte erweiterte Schlüssel Verwendungs Eigenschaft mit dem OID 1.3.6.1.4.1.311.95.1.1.1 verfügt. Andernfalls funktioniert die Kommunikation zwischen dem Netzwerk Controller und dem Host möglicherweise nicht.

#### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage
  
>[!NOTE]
>Bevor Sie dieses Verfahren ausführen, sollten Sie die Zertifikat Anforderungen und die verfügbaren Zertifikat Vorlagen in der Zertifikat Vorlagen Konsole überprüfen. Sie können entweder eine vorhandene Vorlage ändern oder ein Duplikat einer vorhandenen Vorlage erstellen und dann die Kopie der Vorlage ändern. Es wird empfohlen, eine Kopie einer vorhandenen Vorlage zu erstellen.

1. Klicken Sie auf dem **Server, auf**dem AD CS installiert ist, in Server-Manager auf Extras, und klicken Sie dann auf **Zertifizierungs**Stelle. Die Microsoft Management Console \(-MMC\) der Zertifizierungsstelle wird geöffnet. 
2. Doppelklicken Sie in der MMC auf den Zertifizierungsstellen Namen, klicken Sie mit der rechten Maustaste auf **Zertifikat Vorlagen**, und klicken Sie dann auf **Verwalten**.
3. Die Konsole Zertifikat Vorlagen wird geöffnet. Alle Zertifikat Vorlagen werden im Bereich Details angezeigt.
4. Klicken Sie im Detailbereich auf die Vorlage, die Sie duplizieren möchten.
5.  Klicken Sie auf das Menü **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Das Dialogfeld Vorlagen **Eigenschaften** wird geöffnet.
6.  Klicken Sie im Dialogfeld Vorlagen **Eigenschaften** auf der Registerkarte Antragsteller **Name** **in der Anforderung auf bereit**stellen. \(Diese Einstellung ist für SSL-Zertifikate des Netzwerk Controllers erforderlich.\)
7.  Vergewissern Sie sich, dass im Dialogfeld Vorlagen **Eigenschaften** auf der Registerkarte **Anforderungs Verarbeitung** die Option **Exportieren von privatem Schlüssel zulassen** aktiviert ist. Stellen Sie außerdem sicher, dass die **Signatur und der Verschlüsselungs** Zweck ausgewählt sind.
8.  Wählen Sie im Dialogfeld Vorlagen **Eigenschaften** auf der Registerkarte **Erweiterungen** die Option **Schlüssel Verwendung**aus, und klicken Sie dann auf **Bearbeiten**.
9.  Stellen Sie sicher, dass unter **Signatur**die Option **digitale Signatur** ausgewählt ist.
10.  Wählen Sie im Dialogfeld Vorlagen **Eigenschaften** auf der Registerkarte **Erweiterungen** die Option **Anwendungsrichtlinien**aus, und klicken Sie dann auf **Bearbeiten**.
11.  Stellen Sie in **Anwendungsrichtlinien**sicher, dass **Client Authentifizierung** und **Server Authentifizierung** aufgeführt sind.
12.  Speichern Sie die Kopie der Zertifikat Vorlage mit einem eindeutigen Namen, z. b. **Netzwerk Controller Vorlage**.

#### <a name="to-request-a-certificate-from-the-ca"></a>So fordern Sie ein Zertifikat von der Zertifizierungsstelle an

Sie können das Zertifikate-Snap-in verwenden, um Zertifikate anzufordern. Sie können einen beliebigen Zertifikattyp anfordern, der von einem Administrator der Zertifizierungsstelle, die die Zertifikat Anforderung verarbeitet, vorkonfiguriert und verfügbar gemacht wurde.

**Benutzer** oder lokale **Administratoren** sind die mindestens erforderliche Gruppenmitgliedschaft, um dieses Verfahren abzuschließen.

1. Öffnen Sie das Zertifikat-Snap-in für einen Computer.
2. Klicken Sie in der Konsolen Struktur **auf \(Zertifikate lokaler\)Computer**. Wählen Sie den **persönlichen** Zertifikat Speicher aus.
3. Zeigen Sie im Menü **Aktion** auf * * alle Aufgaben<strong>, und klicken Sie dann auf * * neues Zertifikat anfordern</strong> , um den Zertifikatregistrierungs-Assistenten zu starten. Klicken Sie auf **Weiter**.
4. Wählen Sie die von Ihrer Administrator Zertifikat-Registrierungs Richtlinie **konfigurierte aus** , und klicken Sie auf **weiter**.
5. Wählen Sie die **Active Directory Registrierungs Richtlinie** \(basierend auf der Zertifizierungsstellen Vorlage aus, die Sie im vorherigen\)Abschnitt konfiguriert haben.
6. Erweitern Sie den Abschnitt **Details** , und konfigurieren Sie die folgenden Elemente:
   1. Stellen Sie sicher, dass die **Schlüssel Verwendung** sowohl <strong>Digital Signature * * als auch * * Key-Chiffrierung</strong>umfasst.
   2. Stellen Sie sicher, dass die **Anwendungsrichtlinien** sowohl\) **Server Authentifizierung** \(1.3.6.1.5.5.7.3.1 als\)auch **Client Authentifizierung** \(1.3.6.1.5.5.7.3.2 enthalten.
7. Klicken Sie auf **Eigenschaften**.
8. Wählen Sie **auf der Register** Karte Antragsteller unter Antragsteller **Name**unter **Typ**den **Namen allgemeiner Name**aus. Geben Sie unter Wert den **Netzwerk Controller-Rest-Endpunkt**an.
9. Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.
10. Klicken Sie auf **Registrieren**.

Klicken Sie im MMC-Zertifikat auf den persönlichen Speicher, um das Zertifikat anzuzeigen, das Sie von der Zertifizierungsstelle angemeldet haben.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>Exportieren und Kopieren des Zertifikats in die SCVMM-Bibliothek

Nachdem Sie ein selbst\-signiertes\-oder ein von der Zertifizierungsstelle signiertes Zertifikat erstellt haben, müssen Sie \(das Zertifikat mit dem privaten\) Schlüssel im PFX- \(Format und ohne den privaten Schlüssel im Base-64. CER-Formatexportieren.\) über das Snap-in "Zertifikate". 

Sie müssen dann die beiden exportierten Dateien in die Ordner **ServerCertificate.CR** und **NCCertificate.CR** kopieren, die Sie beim Importieren der NC-Dienst Vorlage angegeben haben.

1. Öffnen Sie das Zertifikate-Snap-in (certlm. msc), und suchen Sie das Zertifikat im persönlichen Zertifikat Speicher des lokalen Computers.
2. Klicken\-Sie mit der rechten Maustaste auf das Zertifikat, klicken Sie auf **Alle Tasks**und dann auf **exportieren**. Der Zertifikatexport-Assistent wird geöffnet. Klicken Sie auf **Weiter**.
3. Wählen Sie **Ja**, privaten Schlüssel exportieren aus, und klicken Sie auf **weiter**.
4. Wählen Sie privater **Informationsaustausch-PKCS #12 () aus. PFX)** , und übernehmen Sie die Standardeinstellung, um nach Möglichkeit **alle Zertifikate im Zertifizierungspfad einzubeziehen** .
5. Weisen Sie die Benutzer/Gruppen und ein Kennwort für das Zertifikat zu, das Sie exportieren, und klicken Sie auf **weiter**.
6. Suchen Sie auf der Seite zu exportierende Datei den Speicherort, an dem Sie die exportierte Datei platzieren möchten, und benennen Sie Sie.
7. Exportieren Sie das Zertifikat auch in. CER-Format. Hinweis: Zum Exportieren in. CER-Format, deaktivieren Sie die Option Ja, privaten Schlüssel exportieren.
8. Kopieren Sie die. PFX zum Ordner ServerCertificate.CR.
9. Kopieren Sie die. CER-Datei in den Ordner NCCertificate.CR.

Wenn Sie diese Schritte abgeschlossen haben, aktualisieren Sie diese Ordner in der SCVMM-Bibliothek, und stellen Sie sicher, dass diese Zertifikate kopiert wurden. Fahren Sie mit der Konfiguration und Bereitstellung der Netzwerk Controller-Dienst Vorlage fort.

## <a name="authenticating-southbound-devices-and-services"></a>Authentifizieren von Southbound-Geräten und-Diensten 

Die Netzwerk Controller Kommunikation mit Hosts und SLB-MUX-Geräten verwendet Zertifikate für die Authentifizierung. Die Kommunikation mit den Hosts erfolgt über das ovsdb-Protokoll, während die Kommunikation mit den SLB MUX-Geräten über das WCF-Protokoll erfolgt.

### <a name="hyper-v-host-communication-with-network-controller"></a>Kommunikation mit dem Hyper-V-Host mit dem Netzwerk Controller

Für die Kommunikation mit den Hyper-V-Hosts über ovsdb muss der Netzwerk Controller ein Zertifikat für die Host Computer präsentieren. Standardmäßig übernimmt SCVMM das auf dem Netzwerk Controller konfigurierte SSL-Zertifikat und verwendet es für die Kommunikation mit den Hosts in der Southbound-Kommunikation.

Dies ist der Grund, warum für das SSL-Zertifikat die Clientauthentifizierungs-EKU konfiguriert sein muss. Dieses Zertifikat wird auf der Rest-Ressource \("Servers" konfiguriert. Hyper-V-Hosts werden im Netzwerk Controller als Server Ressource\)dargestellt und können durch Ausführen des Windows PowerShell-Befehls " **Get-networkcontrollerserver" angezeigt werden.** .

Im folgenden finden Sie ein Beispiel für die Rest-Ressource des Servers.

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

Für die gegenseitige Authentifizierung muss der Hyper-V-Host auch über ein Zertifikat für die Kommunikation mit dem Netzwerk Controller verfügen. 

Sie können das Zertifikat von einer Zertifizierungsstellen-Zertifizierungs \(\)Stelle anmelden. Wenn auf dem Host Computer kein ZS-basiertes Zertifikat gefunden wird, wird von SCVMM ein selbst signiertes Zertifikat erstellt und auf dem Host Computer bereitgestellt.

Der Netzwerk Controller und die Hyper-V-Host Zertifikate müssen einander als vertrauenswürdig eingestuft werden. Das Stamm Zertifikat des Hyper-V-Host Zertifikats muss im Speicher für vertrauenswürdige Stamm Zertifizierungsstellen des Netzwerk Controllers für den lokalen Computer vorhanden sein und umgekehrt. 

Wenn Sie selbst\-signierte Zertifikate verwenden, stellt SCVMM sicher, dass die erforderlichen Zertifikate im Speicher der vertrauenswürdigen Stamm Zertifizierungsstellen für den lokalen Computer vorhanden sind. 

Wenn Sie auf Zertifizierungsstellen basierende Zertifikate für die Hyper-V-Hosts verwenden, müssen Sie sicherstellen, dass das Stamm Zertifikat der Zertifizierungsstelle im Speicher vertrauenswürdiger Stamm Zertifizierungsstellen für den lokalen Computer vorhanden ist.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>Software Load Balancer MUX-Kommunikation mit dem Netzwerk Controller

Die Software Load Balancer Multiplexor \(MUX\) und der Netzwerk Controller kommunizieren über das WCF-Protokoll mithilfe von Zertifikaten für die Authentifizierung.

Standardmäßig übernimmt SCVMM das auf dem Netzwerk Controller konfigurierte SSL-Zertifikat und verwendet es für die Kommunikation mit den MUX-Geräten in der Southbound-Kommunikation. Dieses Zertifikat wird für die Rest-Ressource "networkcontrollerloadbalancermux" konfiguriert und kann durch Ausführen des PowerShell-Cmdlets " **Get-networkcontrollerloadbalancermux**" angezeigt werden.

Beispiel für eine partielle \(\)MUX-Rest-Ressource:

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

Für die gegenseitige Authentifizierung müssen Sie auch über ein Zertifikat auf den SLB MUX-Geräten verfügen. Dieses Zertifikat wird automatisch von SCVMM konfiguriert, wenn Sie den Software Load Balancer mithilfe von SCVMM bereitstellen.

>[!IMPORTANT]
>Auf dem Host-und dem SLB-Knoten ist es wichtig, dass der Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen kein Zertifikat enthält, bei dem "ausgestellt für" nicht mit "ausgestellt von" identisch ist. In diesem Fall tritt ein Fehler bei der Kommunikation zwischen dem Netzwerk Controller und dem Southbound-Gerät auf.

Netzwerk Controller und SLB-MUX-Zertifikate müssen voneinander \(als vertrauenswürdig eingestuft werden\). das Stamm Zertifikat des SLB MUX-Zertifikats muss im Speicher für vertrauenswürdige Stamm Zertifizierungsstellen des Netzwerk Controller Computers vorhanden sein und umgekehrt. Wenn Sie selbst\-signierte Zertifikate verwenden, stellt SCVMM sicher, dass die erforderlichen Zertifikate im Speicher Vertrauenswürdige Stamm Zertifizierungsstellen für den lokalen Computer vorhanden sind.



