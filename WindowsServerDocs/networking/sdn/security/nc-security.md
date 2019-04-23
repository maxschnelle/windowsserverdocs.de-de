---
title: Netzwerkcontroller-Sicherheit
description: Sie können in diesem Thema erfahren, wie Sie zum Konfigurieren der Sicherheit für die gesamte Kommunikation zwischen Netzwerkcontroller und andere Software und Geräte verwenden.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: fccd6ee1ba734d72629264bd5b3bb7d93ddcdb70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884761"
---
# <a name="secure-the-network-controller"></a>Sichern des Netzwerk-Controllers

In diesem Thema erfahren Sie, wie Sie zum Konfigurieren der Sicherheit für die gesamte Kommunikation zwischen [Netzwerkcontroller](../technologies/network-controller/network-controller.md) und andere Software und alle Geräte. 

Die Kommunikationspfade, die Sie sichern können, umfassen Northbound-Kommunikation auf der Verwaltungsebene, die Kommunikation zwischen Netzwerkcontroller-VMs des Clusters \(VMs\) in einem Cluster und die Southbound-Kommunikation für die Daten Ebene.

1. **Northbound-Kommunikation**. Netzwerkcontroller kommuniziert, auf der Verwaltungsebene mit SDN\-kann Verwaltungssoftware wie Windows PowerShell und System Center Virtual Machine Manager- \(SCVMM\). Diese Management-Tools bieten Ihnen die Möglichkeit zum Definieren von Netzwerkrichtlinien- und einen Ziel-Status für das Netzwerk zu erstellen, mit dem Sie die tatsächliche Netzwerk-Konfiguration, um die tatsächliche Konfiguration in Übereinstimmung mit den Zielzustand bringen vergleichen können.

2. **Cluster-Netzwerkkommunikation Controller**. Wenn Sie mindestens drei virtuelle Computer als Clusterknoten für den Netzwerkcontroller konfigurieren, werden diese Knoten miteinander kommunizieren. Diese Kommunikation kann mit Synchronisierung und Replikation von Daten über Knoten oder eine bestimmte Kommunikation zwischen Netzwerkcontroller-Diensten zusammen.

3.  **Southbound-Kommunikation**. Netzwerkcontroller kommuniziert, auf die Datenebene mit SDN-Infrastruktur und anderen Geräten wie Software-Lastenausgleichsmodule, Gateways und Hostcomputer. Sie können den Netzwerkcontroller verwenden, konfigurieren und verwalten die southbound-Geräte, sodass sie den Zielzustand verwalten, den Sie für das Netzwerk konfiguriert haben.


## <a name="northbound-communication"></a>Northbound-Kommunikation

Netzwerkcontroller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Northbound-Kommunikation. Die folgenden Abschnitte enthalten Informationen dazu, wie Sie diese Sicherheitseinstellungen konfigurieren.

### <a name="authentication"></a>Authentifizierung

Wenn Sie die Authentifizierung für Network Controller Northbound-Kommunikation konfigurieren, können Sie den Netzwerkcontroller-Clusterknoten und Verwaltungsclients zum Überprüfen der Identität des Geräts, mit denen sie kommunizieren.

Netzwerkcontroller unterstützt die folgenden drei Modi der Authentifizierung zwischen Management-Clients und dem Netzwerkcontroller-Knoten.

>[!Note]
>Bei der Bereitstellung des Netzwerkcontrollers mit System Center Virtual Machine Manager nur **Kerberos** -Modus wird unterstützt.

1. **Kerberos**. Verwenden Sie Kerberos-Authentifizierung aus, wenn sowohl der Management-Client als auch alle Netzwerkcontroller-Clusterknoten in einer Active Directory-Domäne einbinden. Active Directory-Domäne müssen Domänenkonten, die für die Authentifizierung verwendet.

2. **X509**. Verwenden Sie X509 für Zertifikat\-basierende Authentifizierung für Management-Clients, die nicht mit Active Directory-Domäne verknüpft. Sie müssen Zertifikate für alle Netzwerkcontroller-Clusterknoten und Verwaltungsclients registrieren. Darüber hinaus müssen alle Knoten und Verwaltungsclients voneinander Zertifikate vertrauen.

3. **Keine**. Verwenden Sie keine für das Testen in einer testumgebung zu Testzwecken und daher nicht empfohlen, für die Verwendung in einer produktionsumgebung. Wenn Sie diesen Modus auswählen, besteht keine Authentifizierung zwischen Knoten und Verwaltungsclients ausgeführt.

Sie können den Authentifizierungsmodus für die Northbound-Kommunikation konfigurieren, mit dem Windows PowerShell-Befehl **[Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** mit der _ClientAuthentication_ Parameter. 


### <a name="authorization"></a>Autorisierung

Wenn Sie Authorization für Network Controller Northbound-Kommunikation konfigurieren, können Sie Netzwerkcontroller-Clusterknoten und Verwaltungsclients, um sicherzustellen, dass das Gerät sie mit dem kommunizieren vertrauenswürdigen und verfügt über die Berechtigung zur Teilnahme an der die Kommunikation.

Verwenden Sie die folgenden Autorisierungsmethoden für die einzelnen die Authentifizierungsmodi, die vom Netzwerkcontroller unterstützt.

1.  **Kerberos**. Wenn Sie die Kerberos-Authentifizierung-Methode verwenden, definieren Sie die Benutzer und Computer berechtigt, die Kommunikation mit Netzwerkcontroller durch Erstellen einer Sicherheitsgruppe in Active Directory, und klicken Sie dann die autorisierten Benutzer und Computer zur Gruppe hinzufügen. Netzwerkcontroller, um die Sicherheitsgruppe für die Autorisierung mit konfigurierbaren der _ClientSecurityGroup_ Parameter, der die **[Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell-Befehl. Nach der Installation der Netzwerkcontroller können Sie die Sicherheitsgruppe ändern, indem Sie mit der **[Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** Befehl mit dem Parameter _- ClientSecurityGroup_ . Wenn Sie SCVMM zu verwenden, müssen Sie der Sicherheitsgruppe "als Parameter während der Bereitstellung bereitstellen.

2.  **X509**. Bei Verwendung der X509 Authentifizierungsmethode Netzwerkcontroller nur Anforderungen von Management-Clients, deren Fingerabdrücke für clusterzertifikat, dass der Netzwerkcontroller bekannt ist, akzeptiert. Sie können diese Fingerabdrücke konfigurieren, mit der _ClientCertificateThumbprint_ Parameter der **[Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell-Befehl. Sie können jederzeit andere Client-Fingerabdrücke hinzufügen, mit der **[Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** Befehl.

3.  **Keine**. Wenn Sie diesen Modus auswählen, besteht keine Authentifizierung zwischen Knoten und Verwaltungsclients ausgeführt. Verwenden Sie keine für das Testen in einer testumgebung zu Testzwecken und daher nicht empfohlen, für die Verwendung in einer produktionsumgebung. 


### <a name="encryption"></a>Verschlüsselung

Northbound-Kommunikation verwendet, Secure Sockets Layer \(SSL\) einen verschlüsselten Kanal zwischen Management-Clients und dem Netzwerkcontroller-Knoten zu erstellen. SSL-Verschlüsselung für die Northbound-Kommunikation umfasst die folgenden Anforderungen:

- Alle Netzwerkcontroller-Knoten müssen identische Zertifikate, die erweiterte Schlüsselverwendung der Serverauthentifizierung und Clientauthentifizierung Zwecke einschließt \(EKU\) Erweiterungen. 

- Der URI von Verwaltungsclients verwendet werden, um die Kommunikation mit Netzwerkcontroller muss es sich um Antragstellername des Zertifikats sein. Antragstellername des Zertifikats muss entweder den vollständig qualifizierten Domänennamen (FQDN) oder die IP-Adresse der Netzwerk-Controller-REST-Endpunkt enthalten.

- Netzwerkcontroller-Knoten in unterschiedlichen Subnetzen befinden, der Antragstellernamen der Zertifikate muss identisch sein als der Wert für die _RestName_ Parameter in der **Install-NetworkController** Windows PowerShell-Befehl. 

- Alle Management-Clients muss das SSL-Zertifikat vertrauen.


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL-Zertifikat-Registrierung und Konfiguration

Sie müssen das SSL-Zertifikat auf dem Netzwerkcontroller-Knoten manuell registrieren.

Nachdem das Zertifikat registriert ist, können Sie konfigurieren, dass Netzwerkcontroller zur Verwendung des Zertifikats mit der **- ServerCertificate** Parameter der **Install-NetworkController** Windows PowerShell-Befehl . Wenn Sie den Netzwerkcontroller bereits installiert haben, können Sie die Konfiguration jederzeit aktualisieren, mit der **Set-NetworkController** Befehl.

>[!NOTE]
>Wenn Sie SCVMM verwenden, müssen Sie das Zertifikat als eine Bibliothekressource hinzufügen. Weitere Informationen finden Sie unter [richten Sie eine SDN-Netzwerkcontroller im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

## <a name="network-controller-cluster-communication"></a>Die Controller-Cluster-Netzwerkkommunikation

Netzwerkcontroller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Kommunikation zwischen Netzwerkcontroller-Knoten. Die Kommunikation erfolgt über [Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) und TCP.

Sie können konfigurieren, dass dieser Modus mit der **ClusterAuthentication** Parameter, der die **Install-NetworkControllerCluster** Windows PowerShell-Befehl. 

Weitere Informationen finden Sie unter [Install-NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster).

### <a name="authentication"></a>Authentifizierung

Wenn Sie die Authentifizierung für die Kommunikation der Cluster von Network Controller konfigurieren, können Sie den Netzwerkcontroller-Clusterknoten zum Überprüfen der Identität von den anderen Knoten, mit denen sie kommunizieren.

Netzwerkcontroller unterstützt die folgenden drei Modi der Authentifizierung zwischen dem Netzwerkcontroller-Knoten.

>[!NOTE]
>Wenn die Bereitstellung des Netzwerkcontrollers mithilfe von SCVMM nur **Kerberos** -Modus wird unterstützt.

1. **Kerberos**. Sie können die Kerberos-Authentifizierung verwenden, wenn alle Netzwerkcontroller-Clusterknoten mit Domänenkonten, die für die Authentifizierung mit einer Active Directory-Domäne verknüpft sind.

2. **X509**. X509 ist Zertifikat\--basierte Authentifizierung. Sie können die X509-Authentifizierung, wenn der Netzwerkcontroller-Clusterknoten nicht zu einer Active Directory-Domäne verknüpft sind. Um X509 verwenden zu können, müssen Sie Registrieren von Zertifikaten für alle Netzwerkcontroller-Clusterknoten, und alle Knoten müssen die Zertifikate vertrauen. Darüber hinaus muss der Antragstellername des Zertifikats, das auf jedem Knoten registriert ist identisch mit den DNS-Namen des Knotens.

3. **Keine**. Wenn Sie diesen Modus auswählen, besteht keine Authentifizierung zwischen dem Netzwerkcontroller-Knoten ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und wird für die Verwendung in einer produktionsumgebung nicht empfohlen.

### <a name="authorization"></a>Autorisierung

Wenn Sie Authorization für Netzwerk-Controller-Clusterkommunikation konfiguriert haben, können Sie den Netzwerkcontroller-Clusterknoten an, stellen Sie sicher, dass die Knoten, mit denen sie kommunizieren, vertrauenswürdig sind und über die Berechtigung zur Teilnahme an der Kommunikation.

Für jeden die Authentifizierungsmodi, die vom Netzwerkcontroller unterstützt werden die folgenden Autorisierungsmethoden verwendet.

1. **Kerberos**. Netzwerkcontrollerknoten akzeptieren die nur kommunikationsanforderungen von anderen Netzwerkcontroller-Computerkonten. Können Sie diese Konten konfigurieren, bei der Bereitstellung des Netzwerkcontrollers mithilfe der **Namen** Parameter, der die [New-NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell-Befehl.

2. **X509**. Netzwerkcontrollerknoten akzeptieren die nur kommunikationsanforderungen von anderen Netzwerkcontroller-Computerkonten. Können Sie diese Konten konfigurieren, bei der Bereitstellung des Netzwerkcontrollers mithilfe der **Namen** Parameter, der die [New-NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell-Befehl.

3. **Keine**. Wenn Sie diesen Modus auswählen, steht keine Autorisierung, die zwischen dem Netzwerkcontroller-Knoten ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und wird für die Verwendung in einer produktionsumgebung nicht empfohlen.

### <a name="encryption"></a>Verschlüsselung

Kommunikation zwischen Netzwerkcontroller-Knoten werden mithilfe von WCF-Transport-Verschlüsselung auf Geräteebene verschlüsselt. Diese Form der Verschlüsselung wird verwendet, wenn die Authentifizierung und Autorisierung Methoden entweder "Kerberos" oder "X509 sind Zertifikate. Weitere Informationen finden Sie in den folgenden Themen.

- [So wird es gemacht: Sichern eines Diensts mit Windows-Anmeldeinformationen](https://msdn.microsoft.com/library/ms734673.aspx)
- [So wird es gemacht: Sichern eines Diensts mit x. 509-Zertifikaten](https://msdn.microsoft.com/library/ms788968.aspx).

## <a name="southbound-communication"></a>Southbound-Kommunikation

Netzwerkcontroller interagiert mit verschiedenen Arten von Geräten für die Southbound-Kommunikation. Diese Interaktionen verwenden verschiedene Protokolle. Aus diesem Grund stehen Ihnen unterschiedliche Anforderungen an die Authentifizierung, Autorisierung und Verschlüsselung abhängig von den Typ des Geräts und das Protokoll, das vom Netzwerkcontroller für die Kommunikation mit dem Gerät verwendet.

Die folgende Tabelle enthält Informationen über den Netzwerkcontroller-Interaktion mit verschiedenen southbound-Geräten.

| Southbound Device-Dienst | Protokoll              | Authentifizierung verwendet    |
|---------------------------|-----------------------|------------------------|
| Softwarelastenausgleich    | WCF (MUX), TCP (Host) | Zertifikate           |
| Firewall                  | OVSDB                 | Zertifikate           |
| Gateway                   | WinRM                 | Kerberos, Zertifikate |
| Virtuelle Netzwerke        | OVSDB, WCF            | Zertifikate           |
| Benutzerdefiniertes routing      | OVSDB                 | Zertifikate           |

Für jedes dieser Protokolle wird der Kommunikationsmechanismus im folgenden Abschnitt beschrieben.

### <a name="authentication"></a>Authentifizierung

Für die Southbound-Kommunikation werden die folgenden Protokolle und die Authentifizierungsmethoden verwendet.

1. **WCF/TCP/OVSDB**. Für diese Protokolle, Authentifizierung erfolgt über X509 Zertifikate. Sowohl auf dem Netzwerkcontroller und dem Peer, der den Softwarelastenausgleich \(SLB\) Multiplexer \(MUX \) /Hostcomputer stellen ihre Zertifikate miteinander für die gegenseitige Authentifizierung. Jedes Zertifikat muss vom Remotepeer vertrauenswürdig sein.

    Für die southbound-Authentifizierung können Sie dasselbe SSL-Zertifikat konfiguriert ist, die für die Verschlüsselung der Kommunikation mit der Northbound-Clients verwenden. Sie müssen auch ein Zertifikat auf den SLB MUX und die Hostgeräten konfigurieren. Antragstellername des Zertifikats muss identisch mit den DNS-Namen des Geräts.

2. **WinRM**. Für dieses Protokoll, erfolgt die Authentifizierung über Kerberos \(für die Domäne eingebundenen Computern\) und mithilfe von Zertifikaten \(für nicht in die Domäne eingebundenen Computern\).

### <a name="authorization"></a>Autorisierung

Für die Southbound-Kommunikation werden die folgenden Protokolle und Autorisierungsmethoden verwendet.

1. **WCF-TCP**. Für diese Protokolle basiert die Autorisierung in den Betreffnamen der peerentität. Netzwerkcontroller speichert den Peer-DNS-Gerätenamen und wird für die Autorisierung verwendet. Dieser DNS-Name muss der Antragstellername des Geräts im Zertifikat übereinstimmen. Ebenso müssen die Netzwerkcontroller-Zertifikat den Network Controller DNS-Namen, die auf dem peergerät gespeicherten übereinstimmen.

2. **WinRM**. Wenn Kerberos verwendet wird, muss das Clientkonto von WinRM in einer vordefinierten Gruppe in Active Directory oder in der lokalen Administratorgruppe auf dem Server vorhanden sein. Wenn Zertifikate verwendet werden, stellt der Client ein Zertifikat für den Server, auf der Server autorisiert, mit dem Namen Antragsteller/Aussteller- und der Server ein zugeordnetes Benutzerkonto verwendet, um die Authentifizierung durchzuführen.

3.  **OVSDB**. Es gibt keine Autorisierung für dieses Protokoll bereitgestellt.

### <a name="encryption"></a>Verschlüsselung

Für die Southbound-Kommunikation werden die folgenden Verschlüsselungsmethoden für Protokolle verwendet.

1. **WCF/TCP/OVSDB**. Für diese Protokolle wird die Verschlüsselung unter Verwendung des Zertifikats, das registriert wird auf dem Client oder Server ausgeführt.

2. **WinRM**. WinRM-Datenverkehr wird verschlüsselt, werden standardmäßig mithilfe von Kerberos-Security Support Provider \(SSP\). Sie können zusätzliche Verschlüsselung in Form von SSL auf dem WinRM-Server konfigurieren.
