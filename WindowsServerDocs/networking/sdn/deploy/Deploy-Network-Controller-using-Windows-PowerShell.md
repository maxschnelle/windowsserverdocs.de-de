---
title: Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell
description: Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zur Bereitstellung von Netzwerk Controllern auf einem oder mehreren Computern oder virtuellen Computern (VMS), auf denen Windows Server 2016 ausgeführt wird.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2448d381-55aa-4c14-997a-202c537c6727
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 294466ef70a9ffc230953b48bb292938be519eac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406116"
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell zur Bereitstellung des Netzwerk Controllers auf mindestens einem virtuellen Computer (Virtual Machines, VMS), auf dem Windows Server 2016 ausgeführt wird.

>[!IMPORTANT]
>Stellen Sie die Netzwerk Controller-Server Rolle nicht auf physischen Hosts bereit. Zum Bereitstellen des Netzwerk Controllers müssen Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Hyper-v-Computer \(VM-\) installieren, der auf einem Hyper-v-Host installiert ist. Nachdem Sie den Netzwerk Controller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für Software-Defined Networking \(Sdn\) aktivieren, indem Sie die Hosts mithilfe des Windows PowerShell-Befehls **New-networkcontrollerserver**dem Netzwerk Controller hinzufügen. Auf diese Weise aktivieren Sie die Load Balancer der Sdn-Software. Weitere Informationen finden Sie unter [New-networkcontrollerserver](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Dieses Thema enthält die folgenden Abschnitte:

- [Installieren der Server Rolle "Netzwerk Controller"](#install-the-network-controller-server-role)

- [Konfigurieren des Netzwerk Controller Clusters](#configure-the-network-controller-cluster)

- [Konfigurieren der Netzwerk Controller Anwendung](#configure-the-network-controller-application)

- [Überprüfung der Netzwerk Controller Bereitstellung](#network-controller-deployment-validation)

- [Zusätzliche Windows PowerShell-Befehle für den Netzwerk Controller](#additional-windows-powershell-commands-for-network-controller)

- [Beispiel für ein Netzwerk Controller-Konfigurationsskript](#sample-network-controller-configuration-script)

- [Schritte nach der Bereitstellung für nicht-Kerberos-bereit Stellungen](#post-deployment-steps-for-non-kerberos-deployments)

## <a name="install-the-network-controller-server-role"></a>Installieren der Server Rolle "Netzwerk Controller"

Mit diesem Verfahren können Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Computer \(VM-\)installieren.

>[!IMPORTANT]
>Stellen Sie die Netzwerk Controller-Server Rolle nicht auf physischen Hosts bereit. Zum Bereitstellen des Netzwerk Controllers müssen Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Hyper-v-Computer \(VM-\) installieren, der auf einem Hyper-v-Host installiert ist. Nachdem Sie den Netzwerk Controller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für Software-Defined Networking \(Sdn-\) aktivieren, indem Sie die Hosts dem Netzwerk Controller hinzufügen. Auf diese Weise aktivieren Sie die Load Balancer der Sdn-Software.

Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  

>[!NOTE]
>Wenn Sie zum Installieren von Netzwerk Controllern Server-Manager anstelle von Windows PowerShell verwenden möchten, finden Sie weitere Informationen unter [Installieren der Netzwerk Controller-Server Rolle mithilfe Server-Manager](https://technet.microsoft.com/library/mt403348.aspx)

Um den Netzwerk Controller mithilfe von Windows PowerShell zu installieren, geben Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

Die Installation des Netzwerk Controllers erfordert, dass Sie den Computer neu starten. Geben Sie hierzu den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

`Restart-Computer`

## <a name="configure-the-network-controller-cluster"></a>Konfigurieren des Netzwerk Controller Clusters

Der Netzwerk Controller Cluster bietet Hochverfügbarkeit und Skalierbarkeit für die Netzwerk Controller Anwendung, die Sie nach dem Erstellen des Clusters konfigurieren können, und die auf dem Cluster gehostet wird.

>[!NOTE]
>Sie können die Verfahren in den folgenden Abschnitten entweder direkt auf dem virtuellen Computer durchführen, auf dem Sie den Netzwerk Controller installiert haben, oder Sie können die Remoteserver-Verwaltungstools für Windows Server 2016 verwenden, um die Prozeduren auf einem Remote Computer auszuführen, auf dem ausgeführt wird. entweder Windows Server 2016 oder Windows 10. Außerdem müssen Sie mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können. Wenn der Computer oder der virtuelle Computer, auf dem Sie den Netzwerk Controller installiert haben, einer Domäne angehört, muss Ihr Benutzerkonto Mitglied der **Domäne "Benutzer**" sein.

Sie können einen Netzwerk Controller Cluster erstellen, indem Sie ein Node-Objekt erstellen und dann den Cluster konfigurieren.

### <a name="create-a-node-object"></a>Erstellen eines Node-Objekts

Sie müssen ein Knoten Objekt für jeden virtuellen Computer erstellen, der Mitglied des Netzwerk Controller Clusters ist.

Geben Sie zum Erstellen eines Knoten Objekts den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

In der folgenden Tabelle finden Sie Beschreibungen zu den einzelnen Parametern des **New-networkcontrollernodebug Object-** Befehls.

|Parameter|Beschreibung|
|-------------|---------------|
|Name|Der **Name** -Parameter gibt den anzeigen amen des Servers an, den Sie dem Cluster hinzufügen möchten.|
|Server|Der **Server** Parameter gibt den Hostnamen, den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) oder die IP-Adresse des Servers an, den Sie dem Cluster hinzufügen möchten. Für in die Domäne eingebundenen Computern ist ein voll qualifizierter Domänen Name erforderlich.|
|FaultDomain|Der Parameter " **fehlerdomain** " gibt die Fehler Domäne für den Server an, den Sie dem Cluster hinzufügen. Dieser Parameter definiert die Server, bei denen möglicherweise ein Fehler auftritt, und zwar mit dem Server, den Sie dem Cluster hinzufügen. Dieser Fehler kann auf freigegebene physische Abhängigkeiten wie z. b. Stromversorgung und Netzwerk Quellen zurückzuführen sein. Fehler Domänen stellen in der Regel Hierarchien dar, die sich auf diese freigegebenen Abhängigkeiten beziehen, wobei es wahrscheinlich ist, dass mehr Server von einem höheren Punkt in der Fehler Domänen Struktur fehlschlagen. Während der Laufzeit berücksichtigt der Netzwerk Controller die Fehler Domänen im Cluster und versucht, die Netzwerk Controller Dienste so zu verteilen, dass Sie sich in separaten Fehler Domänen befinden. Dadurch wird sichergestellt, dass bei einem Ausfall einer Fehler Domäne die Verfügbarkeit dieses dienstants und seines Zustands nicht beeinträchtigt wird. Fehler Domänen werden in einem hierarchischen Format angegeben. Beispiel: "FD:/DC1/Rack1/host1", wobei DC1 der Datacenter-Name ist, Rack1 der Rack-Name und host1 ist der Name des Hosts, auf dem der Knoten platziert wird.|
|Restinterface|Der **restinterface** -Parameter gibt den Namen der Schnittstelle auf dem Knoten an, in dem die Kommunikation mit dem Representational State Transfer (Rest) beendet wird. Diese Netzwerk Controller Schnittstelle empfängt Northbound-API-Anforderungen von der Verwaltungsebene des Netzwerks.|
|NoDebug-Zertifikat|Der **NoDebug Certificate** -Parameter gibt das Zertifikat an, das vom Netzwerk Controller für die Computer Authentifizierung verwendet wird. Das Zertifikat ist erforderlich, wenn Sie die Zertifikat basierte Authentifizierung für die Kommunikation innerhalb des Clusters verwenden. das Zertifikat wird auch für die Verschlüsselung des Datenverkehrs zwischen den Netzwerk Controller Diensten verwendet. Der Antragsteller Name des Zertifikats muss mit dem DNS-Namen des Knotens identisch sein.|

### <a name="configure-the-cluster"></a>Konfigurieren des Clusters

Um den Cluster zu konfigurieren, geben Sie an der Windows PowerShell-Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

In der folgenden Tabelle finden Sie Beschreibungen der einzelnen Parameter des Befehls **install-networkcontrollercluster** .
  
|Parameter|Beschreibung|
|-------------|---------------|
|Clusterauthentication|Der **clusterauthentication** -Parameter gibt den Authentifizierungstyp an, der zum Sichern der Kommunikation zwischen Knoten verwendet wird, und wird auch für die Verschlüsselung des Datenverkehrs zwischen den Netzwerk Controller Diensten verwendet. Die unterstützten Werte sind **Kerberos**, **X509** und **None**. Die Kerberos-Authentifizierung verwendet Domänen Konten und kann nur verwendet werden, wenn die Netzwerk Controller Knoten in eine Domäne angeschlossen sind. Wenn Sie die X509-basierte Authentifizierung angeben, müssen Sie im Network controllernode-Objekt ein Zertifikat bereitstellen. Außerdem müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|Managementsecuritygroup|Der **managementsecuritygroup** -Parameter gibt den Namen der Sicherheitsgruppe an, die Benutzer enthält, die die Verwaltungs-Cmdlets von einem Remote Computer ausführen dürfen. Dies gilt nur, wenn "clusterauthentication" Kerberos ist. Sie müssen eine Domänen Sicherheitsgruppe und keine Sicherheitsgruppe auf dem lokalen Computer angeben.|
|Knoten|Der **Node** -Parameter gibt die Liste der Netzwerk Controller Knoten an, die Sie mit dem Befehl **New-networkcontrollernodebug Object** erstellt haben.|
|Diagnosticlogloation|Der **diagnosticlogloation** -Parameter gibt den Freigabe Speicherort an, an dem die Diagnoseprotokolle regelmäßig hochgeladen werden. Wenn Sie keinen Wert für diesen Parameter angeben, werden die Protokolle lokal auf jedem Knoten gespeichert. Protokolle werden lokal im Ordner%SystemDrive%\windows\tracing\sdndiagnosticsgespeichert. Cluster Protokolle werden lokal im Ordner%SystemDrive%\programdata\microsoft\service fabric\log\tracesgespeichert.|
|Loglocationcredential|Der **loglocationcredential** -Parameter gibt die Anmelde Informationen an, die für den Zugriff auf den Freigabe Speicherort erforderlich sind, an dem die Protokolle gespeichert werden.|
|"Kredentialverschlüsselungscertificate"|Der Parameter " **fidentialverschlüsseltioncertificate** " gibt das Zertifikat an, mit dem der Netzwerk Controller die Anmelde Informationen verschlüsselt, die für den Zugriff auf die Binärdateien des Netzwerk Controllers verwendet werden, und " **loglocationcredential**", sofern angegeben. Das Zertifikat muss auf allen Netzwerk Controller Knoten bereitgestellt werden, bevor Sie diesen Befehl ausführen. das Zertifikat muss auf allen Cluster Knoten registriert werden. Die Verwendung dieses Parameters zum Schützen der Binärdateien und Protokolle von Netzwerk Controllern wird in Produktionsumgebungen empfohlen. Ohne diesen Parameter werden die Anmelde Informationen als Klartext gespeichert und können von jedem nicht autorisierten Benutzer missbraucht werden.|
|Credential|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der **Credential** -Parameter gibt ein Benutzerkonto an, das über die Berechtigung zum Ausführen dieses Befehls auf dem Bereitstellungs Zielcomputer verfügt.|
|CertificateThumbprint|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der " **certifikatethumbprint** "-Parameter gibt das digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos an, das über die Berechtigung zum Ausführen dieses Befehls auf dem Bereitstellungs Zielcomputer verfügt.|
|UseSSL|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der **Parameter "** -Parameter" gibt das Secure Sockets Layer (SSL)-Protokoll an, das verwendet wird, um eine Verbindung mit dem Remote Computer herzustellen. Standardmäßig wird SSL nicht verwendet.|
|ComputerName|Der **Computername** -Parameter gibt den Netzwerk Controller Knoten an, auf dem dieser Befehl ausgeführt wird. Wenn Sie für diesen Parameter keinen Wert angeben, wird standardmäßig der lokale Computer verwendet.|
|Logsizelimitinmsb|Dieser Parameter gibt die maximale Protokoll Größe in MB an, die der Netzwerk Controller speichern kann. Protokolle werden zirkulär gespeichert. Wenn diagnosticloglokation bereitgestellt wird, ist der Standardwert dieses Parameters 40 GB. Wenn diagnosticloglokation nicht angegeben wird, werden die Protokolle auf den Netzwerk Controller Knoten gespeichert, und der Standardwert dieses Parameters ist 15 GB.|
|Logtimelimitindays|Dieser Parameter gibt das Dauer Limit in Tagen an, in dem die Protokolle gespeichert werden. Protokolle werden zirkulär gespeichert. Der Standardwert dieses Parameters ist 3 Tage.|

## <a name="configure-the-network-controller-application"></a>Konfigurieren der Netzwerk Controller Anwendung
Geben Sie zum Konfigurieren der Netzwerk Controller Anwendung den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

In der folgenden Tabelle finden Sie Beschreibungen der einzelnen Parameter des Befehls **install-networkcontroller** .

|Parameter|Beschreibung|
|-------------|---------------|
|ClientAuthentication|Der **clientauthentication** -Parameter gibt den Authentifizierungstyp an, der zum Sichern der Kommunikation zwischen Rest und Netzwerk Controller verwendet wird. Die unterstützten Werte sind **Kerberos**, **X509** und **None**. Die Kerberos-Authentifizierung verwendet Domänen Konten und kann nur verwendet werden, wenn die Netzwerk Controller Knoten in eine Domäne angeschlossen sind. Wenn Sie die X509-basierte Authentifizierung angeben, müssen Sie im Network controllernode-Objekt ein Zertifikat bereitstellen. Außerdem müssen Sie das Zertifikat manuell bereitstellen, bevor Sie diesen Befehl ausführen.|
|Knoten|Der **Node** -Parameter gibt die Liste der Netzwerk Controller Knoten an, die Sie mit dem Befehl **New-networkcontrollernodebug Object** erstellt haben.|
|Clientcertifialisiethumschlag-Print|Dieser Parameter ist nur erforderlich, wenn Sie die Zertifikat basierte Authentifizierung für Netzwerk Controller Clients verwenden. Der **clientcertifikatethüberbprint** -Parameter gibt den Fingerabdruck des Zertifikats an, das für Clients in der Northbound-Ebene registriert wird.|
|ServerCertificate|Der **Server Certificate** -Parameter gibt das Zertifikat an, das der Netzwerk Controller verwendet, um seine Identität für Clients zu beweisen. Das Serverzertifikat muss den Zweck der Server Authentifizierung in Erweiterungen für erweiterte Schlüssel Verwendung enthalten und muss von einer Zertifizierungsstelle, die von Clients als vertrauenswürdig eingestuft wird, an den Netzwerk Controller ausgegeben werden.|
|Restipaddress|Es ist nicht erforderlich, einen Wert für **restipaddress** mit einer einzelnen Knoten Bereitstellung des Netzwerk Controllers anzugeben. Bei bereit Stellungen mit mehreren Knoten gibt der **restipaddress** -Parameter die IP-Adresse des Rest-Endpunkts in CIDR-Notation an. Beispiel: 192.168.1.10/24. Der Wert des Antragsteller namens von **Server Certificate** muss in den Wert des Parameters **restipaddress aufgelöst werden** . Dieser Parameter muss für alle Netzwerk Controller Bereitstellungen mit mehreren Knoten angegeben werden, wenn sich alle Knoten im gleichen Subnetz befinden. Wenn sich Knoten in unterschiedlichen Subnetzen befinden, müssen Sie anstelle von **restipaddress**den **restname** -Parameter verwenden.|
|Restname|Es ist nicht erforderlich, einen Wert für **restname** mit einer einzelnen Knoten Bereitstellung des Netzwerk Controllers anzugeben. Sie müssen nur dann einen Wert für **restname** angeben, wenn bereit Stellungen mit mehreren Knoten über Knoten verfügen, die sich in unterschiedlichen Subnetzen befinden. Bei bereit Stellungen mit mehreren Knoten gibt der **restname** -Parameter den voll qualifizierten Domänen Namen (FQDN) des Netzwerk Controller Clusters an.|
|Clientsecuritygroup|Der Parameter " **clientsecuritygroup** " gibt den Namen der Active Directory Sicherheitsgruppe an, deren Mitgliedernetzwerk Controller Clients sind. Dieser Parameter ist nur erforderlich, wenn Sie die Kerberos-Authentifizierung für die **Client Authentifizierung**verwenden. Die Sicherheitsgruppe muss die Konten enthalten, von denen aus auf die Rest-APIs zugegriffen wird. Sie müssen die Sicherheitsgruppe erstellen und Mitglieder hinzufügen, bevor Sie diesen Befehl ausführen.|
|Credential|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der **Credential** -Parameter gibt ein Benutzerkonto an, das über die Berechtigung zum Ausführen dieses Befehls auf dem Bereitstellungs Zielcomputer verfügt.|
|CertificateThumbprint|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der " **certifikatethumbprint** "-Parameter gibt das digitale Zertifikat für öffentliche Schlüssel (X509) eines Benutzerkontos an, das über die Berechtigung zum Ausführen dieses Befehls auf dem Bereitstellungs Zielcomputer verfügt.|
|UseSSL|Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Computer ausführen. Der **Parameter "** -Parameter" gibt das Secure Sockets Layer (SSL)-Protokoll an, das verwendet wird, um eine Verbindung mit dem Remote Computer herzustellen. Standardmäßig wird SSL nicht verwendet.|

Nachdem Sie die Konfiguration der Netzwerk Controller Anwendung fertiggestellt haben, ist die Bereitstellung des Netzwerk Controllers fertiggestellt.

## <a name="network-controller-deployment-validation"></a>Überprüfung der Netzwerk Controller Bereitstellung

Zum Überprüfen der Bereitstellung des Netzwerk Controllers können Sie dem Netzwerk Controller Anmelde Informationen hinzufügen und dann die Anmelde Informationen abrufen.

Wenn Sie Kerberos als clientauthentication-Mechanismus verwenden, ist die Mitgliedschaft in der von Ihnen erstellten **clientsecuritygroup** mindestens erforderlich, um dieses Verfahren auszuführen.

**Dringlichkeit**

1.  Wenn Sie Kerberos als clientauthentication-Mechanismus verwenden, melden Sie sich mit einem Benutzerkonto, das Mitglied Ihrer **clientsecuritygroup**ist, auf einem Client Computer an.

2. Öffnen Sie Windows PowerShell, geben Sie die folgenden Befehle ein, um dem Netzwerk Controller Anmelde Informationen hinzuzufügen, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. Zum Abrufen der Anmelde Informationen, die Sie dem Netzwerk Controller hinzugefügt haben, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie Werte für jeden Parameter hinzufügen, die für Ihre Bereitstellung geeignet sind.

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. Überprüfen Sie die Befehlsausgabe, die der folgenden Beispielausgabe ähneln sollte.

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
    > Wenn Sie den Befehl **Get-networkcontrollercredential** ausführen, können Sie die Ausgabe des Befehls einer Variablen zuweisen, indem Sie den Punkt Operator verwenden, um die Eigenschaften der Anmelde Informationen aufzulisten. Beispielsweise $cred. Eigenschaften.

## <a name="additional-windows-powershell-commands-for-network-controller"></a>Zusätzliche Windows PowerShell-Befehle für den Netzwerk Controller

Nachdem Sie den Netzwerk Controller bereitgestellt haben, können Sie Windows PowerShell-Befehle verwenden, um die Bereitstellung zu verwalten und zu ändern. Im folgenden finden Sie einige der Änderungen, die Sie an der Bereitstellung vornehmen können.

- Ändern der Einstellungen für den Netzwerk Controller Knoten, den Cluster und die Anwendung

- Entfernen des Netzwerk Controller Clusters und der Anwendung

- Verwalten von Netzwerk Controller-Cluster Knoten, einschließlich hinzufügen, entfernen, aktivieren und Deaktivieren von Knoten.

In der folgenden Tabelle ist die Syntax für Windows PowerShell-Befehle enthalten, die Sie zum Ausführen dieser Aufgaben verwenden können.

|Aufgabe|Befehl|Syntax|
|--------|-------|----------|
|Ändern der Netzwerk Controller-Cluster Einstellungen|Set-networkcontrollercluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Ändern der Anwendungseinstellungen für Netzwerk Controller|Set-networkcontroller|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|Einstellungen für Netzwerk Controller Knoten ändern|Set-networkcontrollernode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Ändern der Diagnose Einstellungen für den Netzwerk Controller|Set-networkcontrollerdiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen der Netzwerk Controller Anwendung|Deinstallieren von networkcontroller|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|Entfernen des Netzwerk Controller Clusters|Deinstallieren von networkcontrollercluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|Hinzufügen eines Knotens zum Netzwerk Controller Cluster|Add-networkcontrollernode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|Deaktivieren eines Netzwerk Controller-Cluster Knotens|Deaktivieren Sie "-networkcontrollernode".|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Aktivieren eines Netzwerk Controller-Cluster Knotens|Enable-networkcontrollernode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|Entfernen eines Netzwerk Controller Knotens aus einem Cluster|Remove-networkcontrollernode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>Windows PowerShell-Befehle für Netzwerk Controller befinden sich in der TechNet-Bibliothek unter [Network Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).

## <a name="sample-network-controller-configuration-script"></a>Beispiel für ein Netzwerk Controller-Konfigurationsskript

Das folgende Beispiel Konfigurationsskript zeigt, wie ein Netzwerk Controller Cluster mit mehreren Knoten erstellt und die Netzwerk Controller Anwendung installiert wird. Außerdem wählt die $CERT Variable ein Zertifikat aus dem Zertifikat Speicher des lokalen Computers aus, das mit der Betreffnamen-Zeichenfolge "networkController.contoso.com" übereinstimmt.

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="post-deployment-steps-for-non-kerberos-deployments"></a>Schritte nach der Bereitstellung für nicht-Kerberos-bereit Stellungen

Wenn Sie Kerberos nicht bei der Bereitstellung des Netzwerk Controllers verwenden, müssen Sie Zertifikate bereitstellen.

Weitere Informationen finden Sie unter [Schritte nach der Bereitstellung für den Netzwerk Controller](../technologies/network-controller/post-deploy-steps-nc.md).


