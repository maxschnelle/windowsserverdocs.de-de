---
title: Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell
description: Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zum Bereitstellen des Netzwerkcontrollers auf eine oder mehrere Computer oder virtuellen Computern (VMs), die Windows Server 2016 ausgeführt werden.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2448d381-55aa-4c14-997a-202c537c6727
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 31c1579dc840f6f4eb805ac4e10f51192a6b4c99
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816191"
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zur Bereitstellung des Netzwerkcontrollers unter eine oder mehrere virtuelle Computer (VMs), die Windows Server 2016 ausgeführt werden.

>[!IMPORTANT]
>Stellen Sie keine der Serverrolle "Netzwerkcontroller" auf physischen Hosts ausgeführt werden. Sie müssen die Netzwerkcontroller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen des Netzwerkcontrollers \(VM\) , die auf einem Hyper-V-Host installiert ist. Nach der Installation des Netzwerkcontrollers auf virtuellen Computern für drei verschiedene Hyper\-V-Hosts müssen Sie die Hyper aktivieren\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts mit dem Netzwerkcontroller der Windows PowerShell-Befehl **New-NetworkControllerServer**. Auf diese Weise aktivieren Sie den SDN-Softwarelastenausgleich-Funktion. Weitere Informationen finden Sie unter [New-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Dieses Thema enthält die folgenden Abschnitte:

- [Installieren Sie die Netzwerkcontroller-Serverrolle](#bkmk_role)

- [Konfigurieren Sie den Netzwerkcontroller-cluster](#bkmk_configure)

- [Konfigurieren Sie die Netzwerkcontroller-Anwendung](#bkmk_app)

- [Network Controller bereitstellungsüberprüfung](#bkmk_validation)

- [Zusätzliche Windows PowerShell-Befehle für den Netzwerkcontroller](#bkmk_ps)

- [Beispielskript für den Netzwerkcontroller-Konfiguration](#bkmk_script)

- [Schritte nach der Bereitstellung für nicht-Kerberos-Bereitstellungen](#bkmk_nonkerb)

## <a name="install-the-network-controller-server-role"></a>Installieren Sie die Netzwerkcontroller-Serverrolle

Sie können dieses Verfahren verwenden, um die Netzwerkcontroller-Serverrolle auf einem virtuellen Computer zu installieren \(VM\).

>[!IMPORTANT]
>Stellen Sie keine der Serverrolle "Netzwerkcontroller" auf physischen Hosts ausgeführt werden. Sie müssen die Netzwerkcontroller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen des Netzwerkcontrollers \(VM\) , die auf einem Hyper-V-Host installiert ist. Nach der Installation des Netzwerkcontrollers auf virtuellen Computern für drei verschiedene Hyper\-V-Hosts müssen Sie die Hyper aktivieren\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts für den Netzwerkcontroller. Auf diese Weise aktivieren Sie den SDN-Softwarelastenausgleich-Funktion.

Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  

>[!NOTE]
>Sollten Sie Server-Manager anstelle von Windows PowerShell verwenden, installieren den Netzwerkcontroller, finden Sie unter [installieren Sie die Netzwerkcontroller-Serverrolle, die mithilfe des Server-Manager](https://technet.microsoft.com/library/mt403348.aspx)

Zum Installieren des Netzwerkcontrollers mithilfe von Windows PowerShell Geben Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

Installation des Netzwerkcontrollers erfordert, dass Sie den Computer neu starten. Zu diesem Zweck geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.

`Restart-Computer`

## <a name="configure-the-network-controller-cluster"></a>Konfigurieren Sie den Netzwerkcontroller-cluster

Der Netzwerkcontroller-Cluster bietet hohe Verfügbarkeit und Skalierbarkeit für die Netzwerkcontroller-Anwendung, die Sie nach Erstellung des Clusters konfigurieren können, und die auf dem Cluster gehostet wird.

>[!NOTE]
>Sie können die Schritte in den folgenden Abschnitten ausführen entweder direkt auf dem virtuellen Computer, in dem Sie Netzwerk-Controller installiert, oder Sie können Remote Server Administration Tools für Windows Server 2016 verwenden, um die Prozeduren auf einem Remotecomputer auszuführen, die ausgeführt wird WindowsServer 2016 oder Windows 10. Außerdem wird die Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe sein, um dieses Verfahren auszuführen. Wenn der Computer oder virtuellen Computer, auf dem Netzwerkcontroller installiert, zu einer Domäne angehört, muss Ihr Benutzerkonto Mitglied der **Domänenbenutzer**.

Sie können einen Netzwerkcontroller-Cluster erstellen, indem Sie ein Node-Objekt das Erstellen und Konfigurieren des Clusters.

### <a name="create-a-node-object"></a>Erstellen Sie ein Node-Objekt

Sie müssen eine Node-Objekt für jeden virtuellen Computer zu erstellen, die dem Netzwerkcontroller-Cluster angehört.

Um eine Node-Objekt zu erstellen, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

Die folgende Tabelle enthält Beschreibungen für jeden Parameter der **New-NetworkControllerNodeObject** Befehl.

|Parameter|Beschreibung|
|-------------|---------------|
|Name|Die **Namen** Parameter gibt den benutzerfreundlichen Namen des Servers, der dem Cluster hinzufügen möchten.|
|Server|Die **Server** Parameter gibt an, den Hostnamen, vollständig qualifizierten Domänennamen (FQDN) oder IP-Adresse des Servers, der mit dem Cluster hinzufügen möchten. Für die Domäne eingebundenen Computern ist der FQDN erforderlich.|
|FaultDomain|Die **FaultDomain** Parameter gibt an, die Fehlerdomäne für den Server, die Sie mit dem Cluster hinzufügen. Dieser Parameter definiert die Server, die zur gleichen Zeit wie der Server, die Sie mit dem Cluster hinzufügen, Fehler auftreten können. Dieser Fehler möglicherweise weil gemeinsame physische Abhängigkeiten wie Stromversorgung und Netzwerk-Quellen. Fehlerdomänen stellen in der Regel dar, Hierarchien, die im Zusammenhang mit diesen gemeinsam genutzten Abhängigkeiten, mehr Server, die wahrscheinlich von einem höheren Punkt in der Domänenstruktur Fehler ausführen. Während der Laufzeit Netzwerkcontroller berücksichtigt die Fehlerdomänen im Cluster und versucht, die dem Netzwerkcontroller-Dienste verteilen, damit sie sich in separaten Fehlerdomänen befinden. Dieser Vorgang hilft, bei einem Ausfall einer Fehlerdomäne, stellen Sie sicher, dass die Verfügbarkeit des Diensts und seinen Zustand nicht beeinträchtigt wird. Fehlerdomänen werden in einem hierarchischen Format angegeben. Zum Beispiel: "Fd: / DC1/Rack1/Host1", wobei DC1 den Namen des Rechenzentrums, Rack 1 der Name der Rack ist und "host1" ist der Name des Hosts, in dem der Knoten platziert wird.|
|RestInterface|Die **RestInterface** Parameter gibt den Namen der Schnittstelle auf dem Knoten, auf denen die Kommunikation Representational State Transfer (REST) beendet wird. Diese Schnittstelle für den Netzwerkcontroller empfängt die Northbound-API-Anforderungen von Verwaltungsebene des Netzwerks.|
|NodeCertificate|Die **NodeCertificate** Parameter gibt an, das Zertifikat, das dem Netzwerkcontroller für die Computerauthentifizierung verwendet. Das Zertifikat ist erforderlich, wenn Sie zertifikatbasierte Authentifizierung für die Kommunikation innerhalb des Clusters verwenden. das Zertifikat wird auch für die Verschlüsselung des Datenverkehrs zwischen dem Netzwerkcontroller-Diensten verwendet werden. Antragstellername des Zertifikats muss der DNS-Name des Knotens identisch sein.|

### <a name="configure-the-cluster"></a>Konfigurieren Sie den cluster

Um den Cluster zu konfigurieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

Die folgende Tabelle enthält Beschreibungen für jeden Parameter der **Install-NetworkControllerCluster** Befehl.
  
|Parameter|Beschreibung|
|-------------|---------------|
|ClusterAuthentication|Die **ClusterAuthentication** Parameter gibt den Authentifizierungstyp an, die zum Sichern der Kommunikation zwischen Knoten verwendet und wird auch für die Verschlüsselung des Datenverkehrs zwischen dem Netzwerkcontroller-Dienste verwendet. Die unterstützten Werte sind **Kerberos**, **X509** und **keine**. Kerberos-Authentifizierung wird verwendet, Domänenkonten und kann nur verwendet werden, wenn die Netzwerkcontroller-Knoten der Domäne beigetreten sind. Wenn Sie X509-basierte Authentifizierung angeben, müssen Sie ein Zertifikat in das Objekt NetworkControllerNode bereitstellen. Darüber hinaus müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|ManagementSecurityGroup|Die **ManagementSecurityGroup** Parameter gibt den Namen der Sicherheitsgruppe, die Benutzer enthält, die den Verwaltungs-Cmdlets von einem Remotecomputer ausgeführt werden dürfen. Dies ist nur anwendbar, wenn ClusterAuthentication Kerberos ist. Sie müssen eine Domänensicherheitsgruppe und nicht um eine Sicherheitsgruppe angeben, auf dem lokalen Computer.|
|Knoten|Die **Knoten** Parameter gibt die Liste der Netzwerkcontroller-Knoten, das Sie erstellt die **New-NetworkControllerNodeObject** Befehl.|
|DiagnosticLogLocation|Die **DiagnosticLogLocation** Parameter gibt den Speicherort, in dem die Diagnoseprotokolle regelmäßig hochgeladen werden. Wenn Sie einen Wert für diesen Parameter nicht angeben, werden die Protokolle lokal auf jedem Knoten gespeichert. Protokolle werden in den Ordner % systemdrive%\Windows\tracing\SDNDiagnostics lokal gespeichert. Clusterprotokolle werden in den Ordner %systemdrive%\ProgramData\Microsoft\Service Fabric\log\Traces lokal gespeichert.|
|LogLocationCredential|Die **LogLocationCredential** Parameter gibt an, die Anmeldeinformationen, die für den Zugriff auf den freigegebenen Speicherort, in dem die Protokolle gespeichert werden, müssen.|
|CredentialEncryptionCertificate|Die **CredentialEncryptionCertificate** Parameter gibt an, das Zertifikat, das dem Netzwerkcontroller verwendet wird, um die Anmeldeinformationen zu verschlüsseln, die verwendet werden, auf dem Netzwerkcontroller-Binärdateien und die  **LogLocationCredential**angegeben. Das Zertifikat muss auf allen Knoten des Netzwerkcontrollers vor dem Ausführen dieses Befehls bereitgestellt werden, und das gleiche Zertifikat muss auf allen Knoten eines Clusters registriert werden. Verwenden diesen Parameter zum Netzwerkcontroller-Binärdateien und-Protokolle zu schützen, wird in produktionsumgebungen empfohlen. Ohne diesen Parameter die Anmeldeinformationen werden in Klartext gespeichert und können von nicht autorisierten Benutzern missbraucht werden.|
|Credential|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **Anmeldeinformationen** Parameter gibt ein Benutzerkonto mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer.|
|CertificateThumbprint|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **CertificateThumbprint** Parameter gibt an, digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer.|
|UseSSL|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **UseSSL** Parameter gibt an, die Secure Sockets Layer (SSL)-Protokoll, das zum Herstellen einer Verbindung mit dem Remotecomputer verwendet wird. Standardmäßig wird SSL nicht verwendet.|
|ComputerName|Die **ComputerName** Parameter gibt den Netzwerkcontroller-Knoten, die auf dem dieser Befehl ausgeführt wird. Wenn Sie einen Wert für diesen Parameter nicht angeben, wird der lokale Computer standardmäßig verwendet.|
|LogSizeLimitInMBs|Dieser Parameter gibt die maximale Protokollgröße in MB, die Netzwerkcontroller gespeichert werden können. Protokolle werden in einer kreisförmigen Weise gespeichert. Wenn DiagnosticLogLocation angegeben wird, ist der Standardwert dieses Parameters 40 GB. Wenn DiagnosticLogLocation nicht angegeben wird, die Protokolle werden auf den Knoten für den Netzwerkcontroller gespeichert, und der Standardwert dieses Parameters ist 15 GB.|
|LogTimeLimitInDays|Dieser Parameter gibt die maximale Anzahl Dauer in Tagen, für die die Protokolle gespeichert werden. Protokolle werden in einer kreisförmigen Weise gespeichert. Der Standardwert dieses Parameters beträgt 3 Tage.|

## <a name="configure-the-network-controller-application"></a>Konfigurieren Sie die Netzwerkcontroller-Anwendung
Um die Netzwerkcontroller-Anwendung zu konfigurieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

Die folgende Tabelle enthält Beschreibungen für jeden Parameter der **Install-NetworkController** Befehl.

|Parameter|Beschreibung|
|-------------|---------------|
|ClientAuthentication|Die **ClientAuthentication** Parameter gibt den Authentifizierungstyp, der zum Sichern der Kommunikation zwischen REST und dem Netzwerkcontroller verwendet wird. Die unterstützten Werte sind **Kerberos**, **X509** und **keine**. Kerberos-Authentifizierung wird verwendet, Domänenkonten und kann nur verwendet werden, wenn die Netzwerkcontroller-Knoten der Domäne beigetreten sind. Wenn Sie X509-basierte Authentifizierung angeben, müssen Sie ein Zertifikat in das Objekt NetworkControllerNode bereitstellen. Darüber hinaus müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|Knoten|Die **Knoten** Parameter gibt die Liste der Netzwerkcontroller-Knoten, das Sie erstellt die **New-NetworkControllerNodeObject** Befehl.|
|ClientCertificateThumbprint|Dieser Parameter ist erforderlich, nur, wenn Sie zertifikatbasierte Authentifizierung für den Netzwerkcontroller-Clients verwenden. Die **ClientCertificateThumbprint** Parameter gibt den Fingerabdruck des Zertifikats, das Clients auf die Northbound-Ebene registriert ist.|
|ServerCertificate|Die **ServerCertificate** Parameter gibt an, das Zertifikat, das dem Netzwerkcontroller verwendet wird, um für Clients ihre Identität nachzuweisen. Das Serverzertifikat muss Zertifizierungszweck der Serverauthentifizierung in Enhanced Key Usage-Erweiterungen enthalten und muss für den Netzwerkcontroller ausgestellt werden, von einer Zertifizierungsstelle, die von Clients als vertrauenswürdig eingestuft wird.|
|RESTIPAddress|Sie müssen sich nicht an einen Wert für **RESTIPAddress** mit einer einzelnen knotenbereitstellung des Netzwerkcontrollers. Für Bereitstellungen mit mehreren Knoten die **RESTIPAddress** Parameter gibt die IP-Adresse des REST-Endpunkts in CIDR-Notation an. Z. B. 192.168.1.10/24. Der Wert der Antragstellername des **ServerCertificate** muss aufgelöst werden auf den Wert des der **RESTIPAddress** Parameter. Dieser Parameter muss für alle Netzwerkcontroller-Bereitstellungen mit mehreren Knoten angegeben werden, wenn alle Knoten im gleichen Subnetz befinden. Wenn der Knoten in unterschiedlichen Subnetzen befinden, müssen Sie verwenden die **RestName** Parameter anstelle von **RESTIPAddress**.|
|RestName|Sie müssen sich nicht an einen Wert für **RestName** mit einer einzelnen knotenbereitstellung des Netzwerkcontrollers. Nur dann geben Sie einen Wert für **RestName** ist, wenn die Bereitstellung mehrerer Knoten Knoten verfügen, die in unterschiedlichen Subnetzen befinden. Für Bereitstellungen mit mehreren Knoten die **RestName** Parameter gibt den FQDN für den Netzwerkcontroller-Cluster.|
|ClientSecurityGroup|Die **ClientSecurityGroup** Parameter gibt den Namen der Active Directory-Sicherheitsgruppe, deren Mitglieder sind die Netzwerkcontroller-Clients. Dieser Parameter ist nur bei Verwendung von Kerberos-Authentifizierung für erforderlich **ClientAuthentication**. Die Sicherheitsgruppe darf die Konten, die von denen aus die REST-APIs zugegriffen werden, und Sie erstellen die Sicherheitsgruppe und Hinzufügen von Mitgliedern vor dem Ausführen dieses Befehls müssen.|
|Credential|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **Anmeldeinformationen** Parameter gibt ein Benutzerkonto mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer.|
|CertificateThumbprint|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **CertificateThumbprint** Parameter gibt an, digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer.|
|UseSSL|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **UseSSL** Parameter gibt an, die Secure Sockets Layer (SSL)-Protokoll, das zum Herstellen einer Verbindung mit dem Remotecomputer verwendet wird. Standardmäßig wird SSL nicht verwendet.|

Nach Abschluss die Konfiguration der Netzwerkcontroller-Anwendung ist die Bereitstellung des Netzwerkcontrollers abgeschlossen.

## <a name="network-controller-deployment-validation"></a>Network Controller bereitstellungsüberprüfung

Zum Überprüfen der Bereitstellung des Netzwerkcontrollers können Sie Anmeldeinformationen und den Netzwerkcontroller hinzufügen und die Anmeldeinformationen abrufen.

Bei Verwendung von Kerberos als der ClientAuthentication-Mechanismus, Mitgliedschaft in der **ClientSecurityGroup** , die Sie erstellt, ist die mindestvoraussetzung, um dieses Verfahren auszuführen.

**Vorgehensweise:**

1.  Auf einem Clientcomputer, wenn Sie Kerberos als ClientAuthentication Mechanismus verwenden, melden Sie sich mit einem Benutzerkonto, das Mitglied ist Ihre **ClientSecurityGroup**.

2. Öffnen Sie Windows PowerShell, geben Sie die folgenden Befehle zum Hinzufügen von Anmeldeinformationen für den Netzwerkcontroller, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. Um die Anmeldeinformationen abzurufen, die Sie für den Netzwerkcontroller hinzugefügt haben, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. Überprüfen Sie die Befehlsausgabe die sollte der folgenden Beispielausgabe ähneln.

    ```
    Tags                   :
    ResourceRef     : /credentials/cred1
    CreatedTime    : 1/1/0001 12:00:00 AM
    InstanceId        : e16ffe62-a701-4d31-915e-7234d4bc5a18
    Etag                  : W/"1ec59631-607f-4d3e-ac78-94b0822f3a9d"
    ResourceMetadata :
    ResourceId       : cred1
    Properties       : Microsoft.Windows.NetworkController.CredentialProperties
    ```

    > [!NOTE]
    > Beim Ausführen der **Get-NetworkControllerCredential** Befehl, und Sie können die Ausgabe des Befehls zu einer Variablen zuweisen, indem Sie mit dem Punktoperator, um die Eigenschaften von Anmeldeinformationen anzuzeigen. Beispiel: $cred. Eigenschaften.

## <a name="additional-windows-powershell-commands-for-network-controller"></a>Zusätzliche Windows PowerShell-Befehle für den Netzwerkcontroller

Nachdem Sie den Netzwerkcontroller bereitgestellt haben, können Sie Windows PowerShell-Befehle verwalten und ändern Sie Ihre Bereitstellung. Es folgen einige der Änderungen, die Sie für Ihre Bereitstellung vornehmen können.

- Ändern Sie den Netzwerkcontroller Knoten-Cluster und Anwendungseinstellungen

- Entfernen Sie die Netzwerkcontroller-Cluster und Anwendung

- Verwalten Sie die Netzwerkcontroller-Clusterknoten, einschließlich hinzufügen, entfernen, aktivieren und Deaktivieren von Knoten.

Die folgende Tabelle enthält, dass die Syntax für die Windows PowerShell-Befehle, die Sie für diese Aufgaben verwenden können.

|Aufgabe|Befehl|Syntax|
|--------|-------|----------|
|Ändern Sie den Netzwerkcontroller-Clustereinstellungen|Set-NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Ändern Sie den Netzwerkcontroller-Anwendungseinstellungen|Set-NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|Ändern der Einstellungen für den Netzwerkcontroller-Knotens|Set-NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Ändern der diagnoseeinstellungen für den Netzwerkcontroller|Set-NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen Sie die Netzwerkcontroller-Anwendung|Uninstall-NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen Sie den Netzwerkcontroller-cluster|Uninstall-NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Hinzufügen eines Knotens mit dem Netzwerkcontroller-cluster|Add-NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|Deaktivieren Sie einen Netzwerkcontroller-Clusterknoten|Disable-NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Aktivieren Sie einen Netzwerkcontroller-Clusterknoten|Enable-NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Entfernen Sie einen Netzwerkcontroller-Knoten aus einem cluster|Remove-NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>Windows PowerShell-Befehle für den Netzwerkcontroller befinden sich in der TechNet-Bibliothek unter [Network Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).

## <a name="sample-network-controller-configuration-script"></a>Beispielskript für den Netzwerkcontroller-Konfiguration

Das folgende Beispielskript für die Konfiguration zeigt, wie erstellen Sie einen Netzwerkcontroller-Cluster mit mehreren Knoten, und installieren Sie die Netzwerkcontroller-Anwendung. Darüber hinaus wählt die Variable $cert ein Zertifikat aus dem lokalen Computer-Zertifikatspeicher, der die Zeichenfolge "networkController.contoso.com" der Subject-Namen entspricht.

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="post-deployment-steps-for-non-kerberos-deployments"></a>Schritte nach der Bereitstellung für nicht-Kerberos-Bereitstellungen

Wenn Sie mit der Bereitstellung des Netzwerkcontrollers nicht Kerberos verwenden, müssen Sie Zertifikate bereitstellen.

Weitere Informationen finden Sie unter [Schritte nach der Bereitstellung für den Netzwerkcontroller](../technologies/network-controller/post-deploy-steps-nc.md).


