---
title: Netzwerkcontroller-Sicherheit
description: In diesem Thema erfahren Sie, wie Sie die Sicherheit für die gesamte Kommunikation zwischen Netzwerk Controller und anderer Software und Geräte konfigurieren.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 54a8b9490fdf83d04c6b69fa88f4e8beca4f703a
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259065"
---
# <a name="secure-the-network-controller"></a>Sichern des Netzwerk-Controllers

In diesem Thema erfahren Sie, wie Sie die Sicherheit für die gesamte Kommunikation zwischen [Netzwerk Controller](../technologies/network-controller/network-controller.md) und anderer Software und Geräte konfigurieren. 

Die Kommunikations Pfade, die Sie sichern können, umfassen die Northbound-Kommunikation auf der Verwaltungsebene, die Cluster Kommunikation zwischen virtuellen Netzwerken des Netzwerk Controllers \(virtuellen Computern\) in einem Cluster und die Kommunikation mit der Datenebene auf der Datenebene.

1. **Northbound-Kommunikation**. Der Netzwerk Controller kommuniziert auf der Verwaltungsebene mit Sdn-\-fähigen Verwaltungssoftware wie Windows PowerShell und System Center Virtual Machine Manager \(SCVMM-\). Diese Verwaltungs Tools bieten Ihnen die Möglichkeit, Netzwerk Richtlinien zu definieren und einen Ziel Status für das Netzwerk zu erstellen, mit dem Sie die tatsächliche Netzwerkkonfiguration vergleichen können, um die tatsächliche Konfiguration mit dem Ziel Status in Parität zu bringen.

2. **Netzwerk Controller-Cluster Kommunikation**. Wenn Sie drei oder mehr VMS als Netzwerk Controller-Cluster Knoten konfigurieren, kommunizieren diese Knoten miteinander. Diese Kommunikation kann sich auf die Synchronisierung und Replikation von Daten über Knoten hinweg oder eine bestimmte Kommunikation zwischen den Netzwerk Controller Diensten beziehen.

3.  **Southbound-Kommunikation**. Der Netzwerk Controller kommuniziert auf der Datenebene mit der Sdn-Infrastruktur und anderen Geräten wie Software Load Balancer, Gateways und Host Computern. Sie können den Netzwerk Controller verwenden, um diese Southbound-Geräte so zu konfigurieren und zu verwalten, dass Sie den Ziel Status behalten, den Sie für das Netzwerk konfiguriert haben.


## <a name="northbound-communication"></a>Northbound-Kommunikation

Der Netzwerk Controller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Northbound-Kommunikation. In den folgenden Abschnitten finden Sie Informationen zum Konfigurieren dieser Sicherheitseinstellungen.

### <a name="authentication"></a>Authentifizierung

Wenn Sie die Authentifizierung für die Kommunikation zwischen Netzwerk Controller und Verbindung konfigurieren, können Sie Netzwerk Controller-Cluster Knoten und Verwaltungs Clients die Identität des Geräts, mit dem Sie kommunizieren, überprüfen.

Der Netzwerk Controller unterstützt die folgenden drei Authentifizierungs Modi zwischen Verwaltungs Clients und Netzwerk Controller Knoten.

>[!Note]
>Wenn Sie einen Netzwerk Controller mit System Center Virtual Machine Manager bereitstellen, wird nur der **Kerberos** -Modus unterstützt.

1. **Kerberos**. Verwenden Sie die Kerberos-Authentifizierung, wenn Sie sowohl den Verwaltungs Client als auch alle Cluster Knoten des Netzwerk Controllers einer Active Directory Domäne beitreten. Die Active Directory Domäne muss über Domänen Konten verfügen, die zur Authentifizierung verwendet werden.

2. **X509**. Verwenden Sie X509 für die Zertifikat\-basierte Authentifizierung für Verwaltungs Clients, die nicht mit einer Active Directory Domäne verknüpft sind. Sie müssen Zertifikate für alle Cluster Knoten und Verwaltungs Clients von Netzwerk Controller registrieren. Außerdem müssen alle Knoten und Verwaltungs Clients die Zertifikate der anderen Knoten als vertrauenswürdig einstufen.

3. **Keine**. Verwenden Sie keine zu Testzwecken in einer Testumgebung und daher nicht für die Verwendung in einer Produktionsumgebung. Wenn Sie diesen Modus auswählen, wird keine Authentifizierung zwischen Knoten und Verwaltungs Clients durchgeführt.

Sie können den Authentifizierungsmodus für die Northbound-Kommunikation konfigurieren, indem Sie den Windows PowerShell **[-Befehl install-networkcontroller](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** mit dem _clientauthentication_ -Parameter verwenden. 


### <a name="authorization"></a>Autorisierung

Wenn Sie die Autorisierung für die Kommunikation zwischen Netzwerk Controller und Verbindung konfigurieren, können Sie Netzwerk Controller-Cluster Knoten und-Verwaltungs Clients überprüfen, ob das Gerät, mit dem Sie kommunizieren, vertrauenswürdig ist und über die Berechtigung zur Teilnahme an der ssy.

Verwenden Sie die folgenden Autorisierungs Methoden für jeden Authentifizierungsmodus, der vom Netzwerk Controller unterstützt wird.

1.  **Kerberos**. Wenn Sie die Kerberos-Authentifizierungsmethode verwenden, definieren Sie die Benutzer und Computer, die für die Kommunikation mit dem Netzwerk Controller autorisiert sind, indem Sie eine Sicherheitsgruppe in Active Directory erstellen und dann die autorisierten Benutzer und Computer der Gruppe hinzufügen. Sie können den Netzwerk Controller so konfigurieren, dass die Sicherheitsgruppe für die Autorisierung verwendet wird. verwenden Sie dazu den _clientsecuritygroup_ -Parameter des Windows PowerShell-Befehls **[install-networkcontroller](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** . Nachdem Sie den Netzwerk Controller installiert haben, können Sie die Sicherheitsgruppe ändern, indem Sie den Befehl **[Set-networkcontroller](https://docs.microsoft.com/powershell/module/networkcontroller/Set-NetworkController)** mit dem Parameter _-clientsecuritygroup_verwenden. Wenn Sie SCVMM verwenden, müssen Sie die Sicherheitsgruppe während der Bereitstellung als Parameter bereitstellen.

2.  **X509**. Wenn Sie die X509-Authentifizierungsmethode verwenden, akzeptiert der Netzwerk Controller nur Anforderungen von Verwaltungs Clients, deren Zertifikat Fingerabdrücke dem Netzwerk Controller bekannt sind. Sie können diese Fingerabdrücke mithilfe des Parameters _clientcertifigatethrebprint_ des Windows PowerShell **[-Befehls Install-networkcontroller](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** konfigurieren. Sie können jederzeit mit dem Befehl **[Set-networkcontroller](https://docs.microsoft.com/powershell/module/networkcontroller/Set-NetworkController)** weitere Client Fingerabdrücke hinzufügen.

3.  **Keine**. Wenn Sie diesen Modus auswählen, wird keine Authentifizierung zwischen Knoten und Verwaltungs Clients durchgeführt. Verwenden Sie keine zu Testzwecken in einer Testumgebung und daher nicht für die Verwendung in einer Produktionsumgebung. 


### <a name="encryption"></a>Verschlüsselung

Die Northbound-Kommunikation verwendet Secure Sockets Layer \(SSL-\), um zwischen Verwaltungs Clients und Netzwerk Controller Knoten einen verschlüsselten Kanal zu erstellen. Die SSL-Verschlüsselung für die Northbound-Kommunikation umfasst die folgenden Anforderungen:

- Alle Netzwerk Controller Knoten müssen über ein identisches Zertifikat verfügen, das die Server Authentifizierung und Client Authentifizierung unter Erweiterte Schlüssel Verwendung \(EKU-\) Erweiterungen umfasst. 

- Der von Verwaltungs Clients für die Kommunikation mit dem Netzwerk Controller verwendete URI muss der Antragsteller Name des Zertifikats sein. Der Antragsteller Name des Zertifikats muss entweder den voll qualifizierten Domänen Namen (FQDN) oder die IP-Adresse des Netzwerk Controller-Rest-Endpunkts enthalten.

- Wenn sich Netzwerk Controller Knoten in unterschiedlichen Subnetzen befinden, muss der Antragsteller Name seiner Zertifikate mit dem Wert identisch sein, der für den _restname_ -Parameter im Windows PowerShell-Befehl **install-networkcontroller** verwendet wird. 

- Alle Verwaltungs Clients müssen dem SSL-Zertifikat vertrauen.


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL-Zertifikat Registrierung und-Konfiguration

Sie müssen das SSL-Zertifikat auf den Netzwerk Controller Knoten manuell registrieren.

Nachdem das Zertifikat registriert wurde, können Sie den Netzwerk Controller so konfigurieren, dass das Zertifikat mit dem Parameter **-serverCertificate** des Windows PowerShell-Befehls **install-networkcontroller** verwendet wird. Wenn Sie den Netzwerk Controller bereits installiert haben, können Sie die Konfiguration jederzeit mithilfe des Befehls **Set-networkcontroller** aktualisieren.

>[!NOTE]
>Wenn Sie SCVMM verwenden, müssen Sie das Zertifikat als Bibliotheks Ressource hinzufügen. Weitere Informationen finden Sie unter [Einrichten eines Sdn-Netzwerk Controllers im VMM-Fabric](https://docs.microsoft.com/system-center/vmm/sdn-controller).

## <a name="network-controller-cluster-communication"></a>Netzwerk Controller-Cluster Kommunikation

Der Netzwerk Controller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Kommunikation zwischen Netzwerk Controller Knoten. Die Kommunikation erfolgt über [Windows Communication Foundation](https://docs.microsoft.com/dotnet/framework/wcf/whats-wcf) \(WCF\) und TCP.

Sie können diesen Modus mit dem Parameter " **clusterauthentication** " des Windows PowerShell-Befehls " **install-networkcontrollercluster** " konfigurieren. 

Weitere Informationen finden Sie unter [install-networkcontrollercluster](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontrollercluster).

### <a name="authentication"></a>Authentifizierung

Wenn Sie die Authentifizierung für die Netzwerk Controller-Cluster Kommunikation konfigurieren, können Sie den Netzwerk Controller-Cluster Knoten die Identität der anderen Knoten überprüfen, mit denen Sie kommunizieren.

Der Netzwerk Controller unterstützt die folgenden drei Authentifizierungs Modi zwischen Netzwerk Controller Knoten.

>[!NOTE]
>Wenn Sie den Netzwerk Controller mithilfe von SCVMM bereitstellen, wird nur der **Kerberos** -Modus unterstützt.

1. **Kerberos**. Sie können die Kerberos-Authentifizierung verwenden, wenn alle Netzwerk Controller-Cluster Knoten mit einer Active Directory Domäne verknüpft sind, mit Domänen Konten, die für die Authentifizierung verwendet werden.

2. **X509**. X509 ist Zertifikat\-basierte Authentifizierung. Sie können die X509-Authentifizierung verwenden, wenn Netzwerk Controller-Cluster Knoten nicht mit einer Active Directory Domäne verknüpft sind. Zur Verwendung von X509 müssen Sie Zertifikate für alle Cluster Knoten des Netzwerk Controllers registrieren, und alle Knoten müssen den Zertifikaten vertrauen. Außerdem muss der Antragsteller Name des Zertifikats, das für jeden Knoten registriert ist, mit dem DNS-Namen des Knotens identisch sein.

3. **Keine**. Wenn Sie diesen Modus auswählen, wird keine Authentifizierung zwischen den Netzwerk Controller Knoten durchgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und wird nicht für die Verwendung in einer Produktionsumgebung empfohlen.

### <a name="authorization"></a>Autorisierung

Wenn Sie die Autorisierung für die Netzwerk Controller-Cluster Kommunikation konfigurieren, können Sie die Netzwerk Controller-Cluster Knoten überprüfen, ob die Knoten, mit denen Sie kommunizieren, vertrauenswürdig sind und über die Berechtigung zur Teilnahme an der Kommunikation verfügen.

Für jeden Authentifizierungsmodus, der vom Netzwerk Controller unterstützt wird, werden die folgenden Autorisierungs Methoden verwendet.

1. **Kerberos**. Netzwerk Controller Knoten akzeptieren Kommunikationsanforderungen nur von anderen Netzwerk Controller-Computer Konten. Sie können diese Konten konfigurieren, wenn Sie den Netzwerk Controller mit dem **Name** -Parameter des Windows PowerShell-Befehls [New-networkcontrollernodeobject](https://docs.microsoft.com/powershell/module/networkcontroller/new-networkcontrollernodeobject) bereitstellen.

2. **X509**. Netzwerk Controller Knoten akzeptieren Kommunikationsanforderungen nur von anderen Netzwerk Controller-Computer Konten. Sie können diese Konten konfigurieren, wenn Sie den Netzwerk Controller mit dem **Name** -Parameter des Windows PowerShell-Befehls [New-networkcontrollernodeobject](https://docs.microsoft.com/powershell/module/networkcontroller/new-networkcontrollernodeobject) bereitstellen.

3. **Keine**. Wenn Sie diesen Modus auswählen, wird keine Autorisierung zwischen den Netzwerk Controller Knoten durchgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und wird nicht für die Verwendung in einer Produktionsumgebung empfohlen.

### <a name="encryption"></a>Verschlüsselung

Die Kommunikation zwischen den Netzwerk Controller Knoten wird mithilfe der WCF-Transport Schicht Verschlüsselung verschlüsselt. Diese Art der Verschlüsselung wird verwendet, wenn die Authentifizierungs-und Autorisierungs Methoden entweder Kerberos-oder X509-Zertifikate sind. Weitere Informationen finden Sie in den folgenden Themen.

- [Vorgehensweise: Sichern eines Dienstes mit Windows-Anmeldeinformationen](https://docs.microsoft.com/dotnet/framework/wcf/how-to-secure-a-service-with-windows-credentials)
- Vorgehens [Weise: Sichern eines Dienstanbieter mit X. 509-Zertifikaten](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-secure-a-service-with-an-x-509-certificate).

## <a name="southbound-communication"></a>Southbound-Kommunikation

Der Netzwerk Controller interagiert mit verschiedenen Gerätetypen für die Southbound-Kommunikation. Für diese Interaktionen werden unterschiedliche Protokolle verwendet. Aus diesem Grund gibt es verschiedene Anforderungen für Authentifizierung, Autorisierung und Verschlüsselung, je nach Gerätetyp und Protokoll, die vom Netzwerk Controller für die Kommunikation mit dem Gerät verwendet werden.

In der folgenden Tabelle finden Sie Informationen zur Interaktion von Netzwerk Controllern mit unterschiedlichen Southbound-Geräten.

| Southbound-Gerät/-Dienst | Protokoll              | Verwendete Authentifizierung    |
|---------------------------|-----------------------|------------------------|
| Softwarelastenausgleich    | WCF (MUX), TCP (Host) | Zertifikate           |
| Firewall                  | Ovsdb                 | Zertifikate           |
| Gateway                   | WinRM                 | Kerberos, Zertifikate |
| Virtuelle Netzwerke        | ovsdb, WCF            | Zertifikate           |
| Benutzerdefiniertes Routing      | Ovsdb                 | Zertifikate           |

Der Kommunikationsmechanismus wird für jedes dieser Protokolle im folgenden Abschnitt beschrieben.

### <a name="authentication"></a>Authentifizierung

Bei der Southbound-Kommunikation werden die folgenden Protokolle und Authentifizierungsmethoden verwendet.

1. **WCF/TCP/ovsdb**. Für diese Protokolle erfolgt die Authentifizierung mithilfe von X509-Zertifikaten. Sowohl der Netzwerk Controller als auch der Peer Software Lastenausgleich \(SLB\) Multiplexer \(MUX\)/Host Computer stellen ihre Zertifikate für die gegenseitige Authentifizierung zur Verfügung. Jedem Zertifikat muss vom Remotepeer vertraut werden.

    Bei der Southbound-Authentifizierung können Sie das gleiche SSL-Zertifikat verwenden, das für die Verschlüsselung der Kommunikation mit den Northbound-Clients konfiguriert ist. Außerdem müssen Sie ein Zertifikat auf den SLB MUX-und Host Geräten konfigurieren. Der Antragsteller Name des Zertifikats muss mit dem DNS-Namen des Geräts identisch sein.

2. **WinRM**. Für dieses Protokoll wird die Authentifizierung mithilfe von Kerberos-\(für in die Domäne eingebundenen Computern\) und mithilfe von Zertifikaten \(für Computer, die nicht der Domäne beigetreten sind\).

### <a name="authorization"></a>Autorisierung

Bei der Southbound-Kommunikation werden die folgenden Protokolle und Autorisierungs Methoden verwendet.

1. **WCF/TCP**. Für diese Protokolle basiert die Autorisierung auf dem Antragsteller Namen der Peer Entität. Der Netzwerk Controller speichert den DNS-Namen des Peer Geräts und verwendet ihn zur Autorisierung. Dieser DNS-Name muss mit dem Antragsteller Namen des Geräts im Zertifikat identisch sein. Ebenso muss das Netzwerk Controller Zertifikat mit dem DNS-Namen des Netzwerk Controllers identisch sein, der auf dem Peer Gerät gespeichert ist.

2. **WinRM**. Wenn Kerberos verwendet wird, muss das WinRM-Client Konto in einer vordefinierten Gruppe in Active Directory oder in der lokalen Gruppe Administratoren auf dem Server vorhanden sein. Wenn Zertifikate verwendet werden, stellt der Client dem Server, den der Server autorisiert, ein Zertifikat mit dem Antragsteller Namen/Aussteller und der Server verwendet ein zugeordnetes Benutzerkonto, um die Authentifizierung durchzuführen.

3.  **Ovsdb**. Für dieses Protokoll wird keine Autorisierung bereitgestellt.

### <a name="encryption"></a>Verschlüsselung

Für die Southbound-Kommunikation werden die folgenden Verschlüsselungsmethoden für Protokolle verwendet.

1. **WCF/TCP/ovsdb**. Für diese Protokolle wird die Verschlüsselung mithilfe des Zertifikats ausgeführt, das auf dem Client oder auf dem Server registriert ist.

2. **WinRM**. Der WinRM-Datenverkehr wird standardmäßig mithilfe der Kerberos-Security Support Provider \(SSP-\)verschlüsselt. Sie können zusätzliche Verschlüsselung auf dem WinRM-Server in Form von SSL konfigurieren.
