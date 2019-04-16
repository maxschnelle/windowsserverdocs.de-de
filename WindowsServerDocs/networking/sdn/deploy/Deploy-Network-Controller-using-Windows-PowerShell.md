---
title: Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell
description: Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zur Bereitstellung von Netzwerk-Controller auf einem oder mehreren Computern oder virtuellen Computern (VMs), auf denen Windows Server2016 ausgeführt werden.
manager: brianlic
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
ms.openlocfilehash: cfd06662f317381fb77bf31db5ed60c2489ff871
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zur Bereitstellung von Netzwerkcontroller auf einem oder mehreren virtuellen Computern (VMs), auf denen Windows Server2016 ausgeführt werden.

>[!IMPORTANT]
>Stellen Sie die Serverrolle "Netzwerkcontroller" auf physischen Hosts nicht. Sie müssen die Netzwerk-Controller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen von Netzwerkcontroller \(VM\), die auf einem Hyper-V-Host installiert ist. Nachdem Sie Netzwerkcontroller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts des Netzwerkcontrollers mithilfe von Windows PowerShell-Befehl aktivieren **neu NetworkControllerServer**. Auf diese Weise aktivieren Sie das Lastenausgleichsmodul für SDN-Software funktioniert. Weitere Informationen finden Sie unter [neu NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Dieses Thema enthält die folgenden Abschnitte.

- [Installieren der Serverrolle Netzwerkcontroller](#bkmk_role)

- [Konfigurieren Sie den Cluster Netzwerkcontroller](#bkmk_configure)

- [Konfigurieren Sie die Netzwerk-Controller-Anwendung](#bkmk_app)

- [Netzwerk-Controller-bereitstellungsüberprüfung](#bkmk_validation)

- [Zusätzliche Windows PowerShell-Befehle für den Netzwerkcontroller](#bkmk_ps)

- [Beispielskript für Netzwerk-Controller-Konfiguration](#bkmk_script)

- [Nach der Post-Deployment Schrittefür Nicht-Kerberos-Bereitstellungen](#bkmk_nonkerb)

## <a name="bkmk_role"></a>Installieren der Serverrolle Netzwerkcontroller

Verwenden Sie dieses Verfahren, um die Netzwerk-Controller-Serverrolle auf einem virtuellen Computer installieren \(VM\).

>[!IMPORTANT]
>Stellen Sie die Serverrolle "Netzwerkcontroller" auf physischen Hosts nicht. Sie müssen die Netzwerk-Controller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen von Netzwerkcontroller \(VM\), die auf einem Hyper-V-Host installiert ist. Nachdem Sie Netzwerkcontroller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts Netzwerkcontroller aktivieren. Auf diese Weise aktivieren Sie das Lastenausgleichsmodul für SDN-Software funktioniert.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  

>[!NOTE]
>Wenn Sie möchten, verwenden Sie Server-Manager anstelle von Windows PowerShell zum Installieren von Netzwerkcontroller finden Sie unter [die Netzwerk-Controller-Serverrolle mit Server-Manager installieren](https://technet.microsoft.com/library/mt403348.aspx)

Um Netzwerkcontroller mithilfe von Windows PowerShell zu installieren, geben Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

Installation des Netzwerkcontroller erfordert, dass Sie den Computer neu starten. Hierzu geben Sie folgenden Befehl, und drücken Sie dann die EINGABETASTE.

`Restart-Computer`

## <a name="bkmk_configure"></a>Konfigurieren Sie den Cluster Netzwerkcontroller

Netzwerkcontroller Cluster bietet hohe Verfügbarkeit und Skalierbarkeit für die Netzwerkcontroller-Anwendung, die Sie nach dem Erstellen des Clusters konfigurieren und die auf dem Cluster gehostet wird.

>[!NOTE]
>Sie können den Verfahren in den folgenden Abschnitten ausführen entweder direkt auf dem virtuellen Computer, in dem Sie Netzwerkcontroller installiert, oder Sie können Remote Server Administration Tools für Windows Server2016 verwenden, um die Verfahren auf einem Remotecomputer ausführen, auf denen Windows Server2016 oder Windows10 ausgeführt wird. Darüber hinaus Mitglied der Gruppe **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen. Wenn der Computer oder virtuellen Computer auf dem Netzwerkcontroller installiert zu einer Domäne angehört, muss Ihr Benutzerkonto Mitglied der **Domänenbenutzer**.

Erstellen Sie einen Cluster Netzwerkcontroller, durch ein Node-Objekt erstellen und konfigurieren Cluster.

### <a name="create-a-node-object"></a>Erstellen Sie ein Knotenobjekt

Sie müssen ein Node-Objekt für jeden virtuellen Computer zu erstellen, die Mitglied des Clusters Netzwerkcontroller ist.

Um ein Node-Objekt zu erstellen, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

Die folgende Tabelle enthält eine Beschreibung für jeden Parameter, der die **neu NetworkControllerNodeObject** Befehl.

|Parameter|Beschreibung|
|-------------|---------------|
|Name|Die **Namen** Parameter gibt den Anzeigenamen des Servers, die Sie dem Cluster hinzufügen möchten.|
|Server|Die **Server** Parameter gibt den Hostnamen, vollständig qualifizierten Domänennamen (FQDN) oder IP-Adresse des Servers, die Sie dem Cluster hinzufügen möchten. Für die Domäne eingebundene Computer ist ein FQDN erforderlich.|
|FaultDomain|Die **FaultDomain** Parameter gibt an, die Fehler bei der Domäne für den Server, die Sie dem Cluster hinzufügen. Dieser Parameter definiert die Server, die zur gleichen Zeit wie der Server, die Sie dem Cluster hinzufügen, Fehler auftreten können. Dieser Fehler kann auf freigegebenen physischen Abhängigkeiten wie Strom oder Netzwerke Quellen zurückzuführen sein. Fehlerdomänen stellen in der Regel Hierarchien, die im Zusammenhang mit diesen freigegebenen Abhängigkeiten, mit wahrscheinlich von einem höheren Punkt in der Struktur von Domäne Fehlertoleranz zusammen nicht mehr Server dar. Während der Laufzeit Netzwerkcontroller berücksichtigt die Fehlerdomänen im Cluster und versucht, die Netzwerk-Controller-Dienste zu verteilen, damit sie in separaten Fehlerdomänen sind. So können Sie bei einem Ausfall einer beliebigen Domäne eine Fehlertoleranz sicherstellen, dass die Verfügbarkeit dieses Diensts und den Zustand nicht gefährdet ist. Fehlerdomänen sind in einem hierarchischen Format angegeben. Beispiel: "Fd: / DC1/Rack 1/Host1", wobei DC1 die Datacenter-Name, Rack 1 der Name des Rack ist und Host1 der Name des Hosts ist, wo sich der Knoten befindet.|
|RestInterface|Die **RestInterface** Parameter gibt den Namen der Schnittstelle auf dem Knoten, in denen die Kommunikation Representational State Transfer (REST) wird beendet. Diese Schnittstelle Netzwerkcontroller erhält die Northbound-API-Anfragen von Verwaltungsebene für das Netzwerk.|
|NodeCertificate|Die **NodeCertificate** Parameter gibt an, das Zertifikat, das Netzwerk-Controller für Authentifizierung verwendet wird. Das Zertifikat ist erforderlich, wenn Sie zertifikatbasierte Authentifizierung für die Kommunikation innerhalb des Clusters verwenden. das Zertifikat wird auch für die Verschlüsselung von Datenverkehr zwischen Netzwerk-Controller-Diensten verwendet. Antragstellername des Zertifikats muss mit dem DNS-Namen des Knotens.|

### <a name="configure-the-cluster"></a>Konfigurieren Sie den Cluster

Um den Cluster zu konfigurieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

Die folgende Tabelle enthält eine Beschreibung für jeden Parameter, der die **Installation NetworkControllerCluster** Befehl.
  
|Parameter|Beschreibung|
|-------------|---------------|
|ClusterAuthentication|Die **ClusterAuthentication** Parameter gibt den Authentifizierungstyp an, die zum Sichern der Kommunikation zwischen Knoten verwendet und wird auch für die Verschlüsselung von Datenverkehr zwischen Netzwerk-Controller-Diensten verwendet. Die unterstützten Werte sind **Kerberos**, **X509** und **keine**. Kerberos-Authentifizierung Domänenkonten verwendet und kann nur verwendet werden, wenn die Netzwerk-Controller-Knoten eine Domäne eingebunden sind. Wenn Sie X509-basierte Authentifizierung angeben, müssen Sie ein Zertifikat für das Objekt NetworkControllerNode bereitstellen. Darüber hinaus müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|ManagementSecurityGroup|Die **ManagementSecurityGroup** Parameter gibt den Namen der Sicherheitsgruppe ein, die Benutzer enthält, die die Cmdlets für die Verwaltung von einem Remotecomputer ausgeführt werden dürfen. Dies gilt nur, wenn ClusterAuthentication Kerberos ist. Sie müssen eine Domänensicherheitsgruppe und nicht in eine Sicherheitsgruppe angeben, auf dem lokalen Computer.|
|Knoten|Die **Knoten** Parameter gibt die Liste der Netzwerk-Controller-Knoten, die mit der Erstellung der **neu NetworkControllerNodeObject** Befehl.|
|DiagnosticLogLocation|Die **DiagnosticLogLocation** Parameter gibt den Speicherort der Freigabe, in denen die Diagnoseprotokolle werden in regelmäßigen Abständen hochgeladen. Wenn Sie einen Wert für diesen Parameter nicht angeben, werden die Protokolle auf jedem Knoten lokal gespeichert. Protokolle werden in den Ordner % systemdrive%\Windows\tracing\SDNDiagnostics lokal gespeichert. Clusterprotokolle werden in den Ordner %systemdrive%\ProgramData\Microsoft\Service Fabric\log\Traces lokal gespeichert.|
|LogLocationCredential|Die **LogLocationCredential** Parameter gibt die Anmeldeinformationen an, die für den Zugriff auf den freigegebenen Speicherort, in dem die Protokolle gespeichert werden, erforderlich sind.|
|CredentialEncryptionCertificate|Die **CredentialEncryptionCertificate** Parameter gibt an, das Zertifikat, das Netzwerkcontroller verwendet, um die Anmeldeinformationen zu verschlüsseln, die auf dem Netzwerkcontroller Binärdateien verwendet werden und die **LogLocationCredential**, sofern angegeben. Das Zertifikat muss auf allen Knoten Netzwerkcontroller vor dem Ausführen dieses Befehls bereitgestellt werden, und das gleiche Zertifikat muss auf allen Knoten eines Clusters registriert werden. In Produktionsumgebungen wird empfohlen, verwenden diesen Parameter zum Schutz von Netzwerkcontroller Binärdateien und Protokolle. Ohne diesen Parameter werden die Anmeldeinformationen werden in Klartext gespeichert und können von einem nicht autorisierten Benutzer missbraucht werden.|
|Anmeldeinformationen|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **Credential** Parameter gibt ein Benutzerkonto mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer an.|
|CertificateThumbprint|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **CertificateThumbprint** Parameter gibt das digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer an.|
|UseSSL|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **UseSSL** Parameter gibt das Secure Sockets Layer (SSL)-Protokoll, das Herstellen eine Verbindung mit dem Remotecomputer verwendet wird. Standardmäßig wird SSL nicht verwendet.|
|ComputerName|Die **ComputerName** Parameter gibt den Netzwerk-Controller-Knoten auf dem dieser Befehl ausgeführt wird. Wenn Sie einen Wert für diesen Parameter nicht angeben, wird der lokale Computer standardmäßig verwendet.|
|LogSizeLimitInMBs|Dieser Parameter gibt die maximale Protokollgröße in MB, die Netzwerk-Controller gespeichert werden können. Protokolle werden in Round gespeichert. Wenn DiagnosticLogLocation bereitgestellt wird, ist der Standardwert für diesen Parameter 40GB. Wenn DiagnosticLogLocation nicht angegeben ist, werden die Protokolle auf den Knoten Netzwerkcontroller gespeichert, und der Standardwert für diesen Parameter ist 15GB.|
|LogTimeLimitInDays|Dieser Parameter gibt den Grenzwert Dauer in Tagen, für die die Protokolle gespeichert werden. Protokolle werden in Round gespeichert. Der Standardwert für diesen Parameter ist 3Tage.|

## <a name="bkmk_app"></a>Konfigurieren Sie die Netzwerk-Controller-Anwendung
Um die Netzwerk-Controller-Anwendung zu konfigurieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

Die folgende Tabelle enthält eine Beschreibung für jeden Parameter, der die **Installation NetworkController** Befehl.

|Parameter|Beschreibung|
|-------------|---------------|
|ClientAuthentication|Die **ClientAuthentication** Parameter gibt den Authentifizierungstyp, der zum Sichern der Kommunikation zwischen REST und Netzwerkcontroller verwendet wird. Die unterstützten Werte sind **Kerberos**, **X509** und **keine**. Kerberos-Authentifizierung Domänenkonten verwendet und kann nur verwendet werden, wenn die Netzwerk-Controller-Knoten eine Domäne eingebunden sind. Wenn Sie X509-basierte Authentifizierung angeben, müssen Sie ein Zertifikat für das Objekt NetworkControllerNode bereitstellen. Darüber hinaus müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|Knoten|Die **Knoten** Parameter gibt die Liste der Netzwerk-Controller-Knoten, die mit der Erstellung der **neu NetworkControllerNodeObject** Befehl.|
|ClientCertificateThumbprint|Dieser Parameter ist erforderlich, nur, wenn Sie zertifikatbasierte Authentifizierung für Clients Netzwerkcontroller verwenden. Die **ClientCertificateThumbprint** -Parameter gibt den Fingerabdruck des Zertifikats, das für Clients in der Northbound-Ebene registriert ist.|
|ServerCertificate|Die **ServerCertificate** Parameter gibt an, das Zertifikat, das dem Netzwerkcontroller wird verwendet, um seine Identität gegenüber Clients nach. Das Serverzertifikat muss Serverauthentifizierung Enhanced Key Usage Erweiterungen enthalten und muss auf dem Netzwerkcontroller ausgestellt werden, von einer Zertifizierungsstelle, die von den Clients als vertrauenswürdig eingestuft wird.|
|RESTIPAddress|Sie müssen keine Angabe eines Werts für **RESTIPAddress** mit einer einzelnen Knoten Bereitstellung von Netzwerk-Controller. Für Bereitstellungen mit mehreren Knoten der **RESTIPAddress** Parameter gibt die IP-Adresse der REST-Endpunkt in CIDR-Notation an. Beispiel: 192.168.1.10/24. Der Antragstellername Wert der **ServerCertificate** auf den Wert des korrigiert die **RESTIPAddress** Parameter. Dieser Parameter muss für alle Bereitstellungen für mehrere Knoten Netzwerkcontroller angegeben werden, wenn alle Knoten im gleichen Subnetz befinden. Wenn der Knoten in unterschiedlichen Subnetzen befinden, können Sie mit der **RestName** Parameter anstelle von **RESTIPAddress**.|
|RestName|Sie müssen keine Angabe eines Werts für **RestName** mit einer einzelnen Knoten Bereitstellung von Netzwerk-Controller. Nur dann geben Sie einen Wert für **RestName** ist bei Bereitstellungen mit mehreren Knoten Knoten verfügen, die in unterschiedlichen Subnetzen befinden. Für Bereitstellungen mit mehreren Knoten der **RestName** -Parameter gibt den FQDN für den Netzwerkcontroller Cluster an.|
|ClientSecurityGroup|Die **ClientSecurityGroup** Parameter gibt den Namen der Active Directory-Sicherheitsgruppe, deren Mitglieder Netzwerkcontroller-Clients sind. Dieser Parameter ist erforderlich, nur, wenn Sie Kerberos-Authentifizierung für **ClientAuthentication**. Die Sicherheitsgruppe dürfen die Konten, die über die REST-APIs aufgerufen werden, und müssen Sie die Sicherheitsgruppe erstellen und Hinzufügen von Mitgliedern vor dem Ausführen dieses Befehls.|
|Anmeldeinformationen|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **Credential** Parameter gibt ein Benutzerkonto mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer an.|
|CertificateThumbprint|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **CertificateThumbprint** Parameter gibt das digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos mit der Berechtigung zum Ausführen dieses Befehls auf dem Zielcomputer an.|
|UseSSL|Dieser Parameter ist erforderlich, nur dann, wenn Sie diesen Befehl von einem Remotecomputer ausgeführt werden. Die **UseSSL** Parameter gibt das Secure Sockets Layer (SSL)-Protokoll, das Herstellen eine Verbindung mit dem Remotecomputer verwendet wird. Standardmäßig wird SSL nicht verwendet.|

Nach Abschluss der Konfiguration der Netzwerk-Controller-Anwendung ist die Bereitstellung von Netzwerkcontroller abgeschlossen.

## <a name="bkmk_validation"></a>Netzwerk-Controller-bereitstellungsüberprüfung

Zum Überprüfen der Bereitstellung von Netzwerkcontroller können Sie Netzwerkcontroller von Anmeldeinformationen hinzu und rufen dann die Anmeldeinformationen.

Bei Verwendung von Kerberos ClientAuthentication Mechanismus für die Mitgliedschaft in der **ClientSecurityGroup** erstellten ist mindestens erforderlich, um dieses Verfahren auszuführen.

#### <a name="to-validate-deployment-of-network-controller"></a>Überprüfen der Bereitstellung von Netzwerkcontroller

1.  Auf einem Clientcomputer bei Verwendung von Kerberos als Mechanismus ClientAuthentication melden Sie sich mit einem Benutzerkonto, das Mitglied ist Ihre **ClientSecurityGroup**.

2. Öffnen Sie Windows PowerShell, geben Sie die folgenden Befehle Netzwerkcontroller einen Satz von Anmeldeinformationen hinzu, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. Rufen Sie die Anmeldeinformationen, die Sie Netzwerkcontroller hinzugefügt, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. Überprüfen Sie die Befehlsausgabe die folgende Beispielausgabe ähnlich sein sollten.

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
    > Beim Ausführen der **Get-NetworkControllerCredential** Befehl, Sie können die Ausgabe des Befehls zu einer Variablen zuweisen, mithilfe des Punktoperators zum Auflisten der Eigenschaften der Anmeldeinformationen. Beispielsweise $cred. Eigenschaften.

## <a name="bkmk_ps"></a>Zusätzliche Windows PowerShell-Befehle für den Netzwerkcontroller

Nach der Bereitstellung von Netzwerkcontroller können Sie Windows PowerShell-Befehle zum Verwalten und Ihre Bereitstellung zu ändern. Nachfolgend sind einige der Änderungen, die Sie für Ihre Bereitstellung vornehmen können.

- Ändern Sie Netzwerkcontroller Knoten-Cluster und App-Einstellungen

- Entfernen Sie die Netzwerk-Controller-Cluster und die Anwendung

- Netzwerkcontroller Clusterknoten, einschließlich hinzufügen, entfernen, aktivieren und Deaktivieren von Knoten zu verwalten.

Die folgende Tabelle enthält die Syntax für Windows PowerShell-Befehle, die Sie verwenden können, um diese Aufgaben ausführen.

|Aufgabe|Befehl|Syntax|
|--------|-------|----------|
|Netzwerkcontroller-Clustereinstellungen ändern|Set-NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Netzwerkcontroller-App-Einstellungen ändern|Set-NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|Netzwerkcontroller knoteneinstellungen ändern|Set-NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Netzwerkcontroller-Diagnose-Einstellungen ändern|Set-NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen Sie die Netzwerk-Controller-Anwendung|Uninstall-NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen Sie die Netzwerk-Controller-Cluster|Uninstall-NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Hinzufügen eines Knotens zum Cluster Netzwerkcontroller|Add-NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|Deaktivieren eines Clusterknotens Netzwerkcontroller|Disable-NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Aktivieren eines Clusterknotens Netzwerkcontroller|Enable-NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Entfernen eines Knotens Netzwerkcontroller aus einem Cluster|Remove-NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>Windows PowerShell-Befehle für den Netzwerkcontroller befinden sich in der TechNet-Bibliothek unter [Network Controller Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).

## <a name="bkmk_script"></a>Beispielskript für Netzwerk-Controller-Konfiguration

Das folgende Beispielskript Configuration veranschaulicht, wie einen Cluster mit mehreren Knoten Netzwerkcontroller erstellen und installieren Sie die Netzwerk-Controller-Anwendung. Darüber hinaus wählt die $cert-Variable ein Zertifikat aus dem Speicher des lokalen Computers Zertifikate, der Namenszeichenfolge Betreff "networkController.contoso.com" entspricht.

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="bkmk_nonkerb"></a>Nach der Bereitstellung Schrittefür nicht - Kerberos-Bereitstellungen

Wenn Sie mit der Bereitstellung Netzwerkcontroller Kerberos nicht verwenden, müssen Sie Zertifikate bereitstellen.

Weitere Informationen finden Sie unter [Schrittenach der Bereitstellung für den Netzwerkcontroller](../technologies/network-controller/post-deploy-steps-nc.md).


