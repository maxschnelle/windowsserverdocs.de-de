---
title: Netzwerksicherheits-Controller
description: In diesem Thema können Sie Informationen zum Konfigurieren der Sicherheit für die Kommunikation zwischen Netzwerkcontroller und andere Software und Geräte.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab04d3f528beb037988e6390fe85ad9af219266b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller-security"></a>Netzwerksicherheits-Controller

In diesem Thema können Sie Informationen zum Konfigurieren der Sicherheit für die Kommunikation zwischen Netzwerkcontroller und andere Software und Geräte. 

>[!NOTE]
>Eine Übersicht über Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](../technologies/network-controller/network-controller.md).

Die Kommunikationspfade, die Sie sichern können beinhalten die Northbound Datenübertragung auf der Verwaltungsebene, Cluster-Kommunikation zwischen Netzwerkcontroller virtuelle Maschinen \(VMs\) in einem Cluster und die Southbound Kommunikation auf der Ebene der Daten.

1. **Northbound Kommunikation**. Netzwerkcontroller kommuniziert, auf die Verwaltungsebene mit SDN\-fähige Management-Software wie Windows PowerShell und System Center Virtual Machine Manager-\(SCVMM\). Diese Management-Tools bieten Ihnen die Möglichkeit zum Definieren von Netzwerkrichtlinien- und einen Ziel-Status für das Netzwerk zu erstellen, mit denen Sie die tatsächliche Netzwerk-Konfiguration, um die tatsächliche Konfiguration in Parität mit dem Ziel-Zustand zu bringen vergleichen können.

2. **Netzwerk-Controller-Clusterkommunikation**. Wenn Sie als Clusterknoten Netzwerkcontroller drei oder mehr virtuelle Computer konfigurieren, werden diese Knoten miteinander kommunizieren. Diese Kommunikation möglicherweise zu synchronisieren und die Replikation von Daten über den Knoten oder bestimmte Kommunikation zwischen Netzwerkcontroller Dienste ausgerichtet sein.

3.  **Southbound Kommunikation**. Netzwerkcontroller kommuniziert, auf der Ebene der Daten mit SDN-Infrastruktur und anderen Geräten wie Software Load Balancers, Gateways und Hostcomputer. Netzwerkcontroller können Sie konfigurieren und verwalten diese southbound Geräte, sodass sie den Ziel-Zustand verwalten, den Sie für das Netzwerk konfiguriert haben.

## <a name="northbound-communication"></a>Northbound Kommunikation

Netzwerkcontroller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Northbound-Kommunikation. Die folgenden Abschnitte enthalten Informationen zum Konfigurieren dieser Einstellungen.

**Authentifizierung**

Wenn Sie die Authentifizierung für die Netzwerk-Controller Northbound-Kommunikation konfigurieren, können Sie Netzwerkcontroller-Clusterknoten und Verwaltung von Clients zum Überprüfen der Identität des Geräts, mit denen sie kommunizieren.

Netzwerkcontroller unterstützt die folgenden drei Modi der Authentifizierung zwischen Management-Clients und dem Netzwerkcontroller Knoten.

>[!Note]
>Wenn Sie Netzwerkcontroller mit System Center Virtual Machine Manager nur bereitstellen **Kerberos** Modus wird unterstützt.

1. **Kerberos**. Sie können Kerberos-Authentifizierung verwenden, wenn sowohl der Verwaltungsclient, z. B. der Computer mit SCVMM und alle Knoten des Clusters Netzwerkcontroller gehören zu einer Active Directory-Domäne mit Domänenkonten, die für die Authentifizierung verwendet.

2. **X509**. X509 ist Certificate\-basierte Authentifizierung. Sie können X509 Authentifizierung bei der Verwaltung von Clients nicht mit Active Directory-Domäne verbunden sind. Um X509 zu verwenden, müssen Sie Registrieren von Zertifikaten für alle Knoten im Cluster Netzwerkcontroller und Management-Clients, und alle Knoten und Management-Clients müssen Zertifikate gegenseitig vertrauen.

3. **Keine**. Wenn Sie diesen Modus auswählen, werden keine Authentifizierung zwischen Management-Clients und dem Netzwerkcontroller ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und ist nicht für die Verwendung in einer produktionsumgebung empfohlen. 

Sie können den Authentifizierungsmodus für die Northbound-Kommunikation konfigurieren, mit dem Windows PowerShell-Befehl **Installation NetworkController** mit der **ClientAuthentication** Parameter. 

Weitere Informationen finden Sie unter den folgenden Themen. 

- [Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**Autorisierung**

Wenn Sie die Autorisierung für die Netzwerk-Controller Northbound-Kommunikation konfigurieren, können Sie Netzwerkcontroller Clusterknoten und Verwaltung von Clients zu überprüfen, ob das Gerät, mit dem sie kommunizieren, vertrauenswürdig ist und verfügt über die Berechtigung zur Teilnahme an der Kommunikation.

Für jede der Authentifizierungsmodi, die vom Netzwerk-Controller unterstützt wird werden die folgenden Autorisierungsmethoden verwendet.

1.  **Kerberos**. Wenn Sie die Kerberos-Authentifizierung-Methode verwenden, definieren Sie die Benutzer und Computer, die autorisiert sind, um die Kommunikation mit Netzwerkcontroller durch Erstellen einer Sicherheitsgruppe in Active Directory, und klicken Sie dann die autorisierte Benutzer und Computer zur Gruppe hinzufügen. Sie können konfigurieren, Netzwerk-Controller, um die Sicherheitsgruppe für die Autorisierung mithilfe der **ClientSecurityGroup** -Parameter von der **Installation NetworkController** Windows PowerShell-Befehl. Nach der Installation von Netzwerkcontroller können Sie die Sicherheitsgruppe ändern, indem Sie mit der [Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller) Befehl mit dem Parameter **- ClientSecurityGroup**. Wenn Sie SCVMM verwenden, müssen Sie die Sicherheitsgruppe als Parameter während der Bereitstellung bereitstellen.

2.  **X509**. Sie verwenden die X509 Authentifizierungsmethode Netzwerkcontroller nur Anforderungen von Management-Clients, deren zertifikatfingerabdrücke ist, dass Netzwerkcontroller bekannt, akzeptiert. Sie können diese Fingerabdrücke konfigurieren, mit der **ClientCertificateThumbprint** -Parameter von der **Installation NetworkController** Windows PowerShell-Befehl. Sie können andere Client-Fingerabdrücke zu einem beliebigen Zeitpunkt hinzufügen, mit der **Set-NetworkController** Befehl.

3.  **Keine**. Wenn Sie diesen Modus auswählen, werden keine Autorisierung für Kommunikationsversuche zwischen Management-Clients und dem Netzwerkcontroller Knoten ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und ist nicht für die Verwendung in einer produktionsumgebung empfohlen. 

Weitere Informationen finden Sie unter den folgenden Themen. 

- [Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**Verschlüsselung**

Northbound Kommunikation wird Secure Sockets Layer-\(SSL\) verwendet, um einen verschlüsselten Kanal zwischen Management-Clients und dem Netzwerkcontroller Knoten zu erstellen. SSL-Verschlüsselung für die Northbound-Kommunikation umfasst die folgenden Anforderungen.

- Alle Netzwerkcontroller-Knoten müssen identische Zertifikate verfügen, die die Serverauthentifizierung und Clientauthentifizierung Zwecke Enhanced Key Usage \(EKU\) Erweiterungen enthält. 

- Der URI, mit der Management-Clients die Kommunikation mit Netzwerkcontroller muss der Name des Zertifikatantragstellers. Der Antragstellername des Zertifikats muss den vollständig qualifizierten Domänennamen (FQDN) oder die IP-Adresse der Netzwerk-Controller-REST-Endpunkt enthalten.

- Netzwerkcontroller-Knoten in verschiedenen Subnetzen befinden, muss der Antragstellername des ihre Zertifikate werden identisch mit dem Wert, den Sie verwenden die **RestName** -Parameter in der **Installation NetworkController** Windows PowerShell-Befehl. 

- Das SSL-Zertifikat muss von allen Management-Clients vertrauenswürdig sein.

### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL-Zertifikat-Registrierung und Konfiguration

Sie müssen das SSL-Zertifikat auf dem Netzwerkcontroller Knoten manuell registrieren.

Nachdem das Zertifikat registriert wurde, können Sie Netzwerkcontroller zur Verwendung des Zertifikats mit Konfigurieren der **- ServerCertificate** -Parameter von der **Installation NetworkController** Windows PowerShell-Befehl. Wenn Sie Netzwerkcontroller bereits installiert haben, können Sie die Konfiguration zu einem beliebigen Zeitpunkt aktualisieren, mithilfe der **Set-NetworkController** Befehl.

>[!NOTE]
>Wenn Sie SCVMM verwenden, müssen Sie das Zertifikat als Bibliothekressource hinzufügen. Weitere Informationen finden Sie unter [richten Sie ein SDN-Netzwerkcontroller in der VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

## <a name="network-controller-cluster-communication"></a>Netzwerk-Controller-Clusterkommunikation

Netzwerkcontroller unterstützt die Authentifizierung, Autorisierung und Verschlüsselung für die Kommunikation zwischen Netzwerkcontroller Knoten. Die Kommunikation erfolgt über [Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) und TCP.

Können Sie konfigurieren diesen Modus mit der **ClusterAuthentication** -Parameter von der **Installation NetworkControllerCluster** Windows PowerShell-Befehl. 

Weitere Informationen finden Sie unter [Installation NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster).

**Authentifizierung**

Wenn Sie die Authentifizierung für die Netzwerk-Controller-Clusterkommunikation konfigurieren, können Sie Netzwerkcontroller Clusterknoten zum Überprüfen der Identität der anderen Knoten, mit denen sie kommunizieren.

Netzwerkcontroller unterstützt die folgenden drei Modi der Authentifizierung zwischen Netzwerkcontroller Knoten.

>[!NOTE]
>Wenn Sie Netzwerkcontroller bereitstellen, nur mithilfe von SCVMM **Kerberos** Modus wird unterstützt.

1. **Kerberos**. Sie können die Kerberos-Authentifizierung verwenden, wenn alle Knoten des Clusters Netzwerkcontroller mit Domänenkonten, die für die Authentifizierung mit einer Active Directory-Domäne verknüpft werden.

2. **X509**. X509 ist Certificate\-basierte Authentifizierung. Sie können X509 Authentifizierung Netzwerkcontroller Clusterknoten Active Directory-Domäne angeschlossen sind. Um X509 zu verwenden, müssen Sie Registrieren von Zertifikaten für alle Knoten des Clusters Netzwerkcontroller, und alle Knoten müssen die Zertifikate vertrauen. Darüber hinaus muss der Antragstellername des Zertifikats, das auf jedem Knoten registriert ist identisch mit dem DNS-Namen des Knotens.

3. **Keine**. Wenn Sie diesen Modus auswählen, werden keine Authentifizierung zwischen Netzwerkcontroller Knoten ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und ist nicht für die Verwendung in einer produktionsumgebung empfohlen.

**Autorisierung**

Wenn Sie die Autorisierung für die Controller-Clusterkommunikation konfiguriert haben, können Sie Netzwerkcontroller Clusterknoten, stellen Sie sicher, dass die Knoten mit denen sie kommunizieren sind vertrauenswürdig sind und über die Berechtigung zur Teilnahme an der Kommunikation.

Für jede der Authentifizierungsmodi, die vom Netzwerk-Controller unterstützt wird werden die folgenden Autorisierungsmethoden verwendet.

1. **Kerberos**. Controller Netzwerkknoten akzeptieren Kommunikation nur Anforderungen von anderen Netzwerkcontroller Computerkonten. Können Sie diese Konten konfigurieren, bei der Bereitstellung von Netzwerkcontroller mithilfe der **Namen** -Parameter von der [neu NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell-Befehl.

2. **X509**. Controller Netzwerkknoten akzeptieren Kommunikation nur Anforderungen von anderen Netzwerkcontroller Computerkonten. Können Sie diese Konten konfigurieren, bei der Bereitstellung von Netzwerkcontroller mithilfe der **Namen** -Parameter von der [neu NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell-Befehl.

3. **Keine**. Wenn Sie diesen Modus auswählen, werden keine Autorisierung zwischen Netzwerkcontroller Knoten ausgeführt. Dieser Modus wird nur zu Testzwecken bereitgestellt und ist nicht für die Verwendung in einer produktionsumgebung empfohlen.

**Verschlüsselung**

Kommunikation zwischen Netzwerkcontroller Knoten wird mithilfe von Verschlüsselung auf Transportebene WCF verschlüsselt. Diese Form der Verschlüsselung wird verwendet, wenn die Authentifizierung und Autorisierung Methoden entweder die Kerberos- oder X509 sind Zertifikate. Weitere Informationen finden Sie unter den folgenden Themen.

- [Vorgehensweise: Sichern ein Diensts mit Windows-Anmeldeinformationen](https://msdn.microsoft.com/library/ms734673.aspx)
- [Vorgehensweise: Sichern ein Diensts mit x. 509-Zertifikate](https://msdn.microsoft.com/library/ms788968.aspx).

## <a name="southbound-communication"></a>Southbound Kommunikation

Netzwerkcontroller interagiert mit unterschiedlichen Arten von Geräten für die Southbound-Kommunikation. Diese Interaktionen verwenden andere Protokolle. Aus diesem Grund stehen verschiedene Anforderungen für Authentifizierung, Autorisierung und Verschlüsselung abhängig vom Typ des Geräts und das Protokoll von Netzwerkcontroller verwendet, um die Kommunikation mit dem Gerät.

In der folgende Tabelle enthält Informationen zu dem Netzwerkcontroller Interaktion mit den verschiedenen southbound-Geräten.

| Southbound Gerät bzw. eines Diensts | Protokoll              | Authentifizierung verwendet    |
|---------------------------|-----------------------|------------------------|
| Softwarelastenausgleich    | WCF (MUX), TCP (Host) | Zertifikate           |
| Firewall                  | OVSDB                 | Zertifikate           |
| Gateway                   | WinRM                 | Kerberos, Zertifikate |
| Virtuelle Netzwerke        | OVSDB, WCF            | Zertifikate           |
| Benutzerdefinierte routing      | OVSDB                 | Zertifikate           |

Für jedes dieser Protokolle wird der Kommunikationsmechanismus im folgenden Abschnitt beschrieben.

**Authentifizierung**

Für die Southbound-Kommunikation werden die folgenden Protokolle und Authentifizierungsmethoden verwendet.

1. **WCF/TCP/OVSDB**. Die Authentifizierung erfolgt für diese Protokolle mit X509 Zertifikate. Netzwerkcontroller und dem Peer \(SLB\) Lastenausgleich Multiplexer \ (MUX\) / Hostcomputer vorhanden, die Zertifikate für die gegenseitige Authentifizierung. Jedes Zertifikat muss von den Remotepeer vertrauenswürdig sein.

    Für die southbound-Authentifizierung können Sie dasselbe SSL-Zertifikat, das so konfiguriert ist, für die Verschlüsselung der Kommunikation mit der Northbound-Clients. Sie müssen auch ein Zertifikat auf den SLB MUX und Hostgeräten konfigurieren. Antragstellername des Zertifikats muss mit dem DNS-Namen des Geräts.

2. **WinRM**. Für dieses Protokoll erfolgt die Authentifizierung mithilfe von Kerberos \ (für die Domäne Machines\) und unter Verwendung von Zertifikaten \ (für Domänenmitglieder verknüpften Machines\).

**Autorisierung**

Für die Southbound-Kommunikation werden die folgenden Protokolle und die Autorisierungsmethoden verwendet.

1. **WCF/TCP**. Für diese Protokolle Autorisierung der Antragstellername des die Peer-Entität basiert. Netzwerkcontroller speichert den Peer-DNS-Gerätenamen, und es für die Autorisierung verwendet werden. Dieser DNS-Name muss der Antragstellername des Geräts im Zertifikat übereinstimmen. Netzwerkcontroller Zertifikat muss entsprechend den Netzwerk-Controller DNS-Namen, die auf dem peergerät gespeicherten übereinstimmen.

2. **WinRM**. Wenn Kerberos verwendet wird, muss das Clientkonto von WinRM in einer vordefinierten Gruppe in Active Directory oder in der lokalen Administratorgruppe auf dem Server vorhanden sein. Wenn Zertifikate verwendet werden, stellt der Client ein Zertifikat mit dem Server, dass der Server autorisiert mithilfe des Betreff Name/Ausstellers, und der Server ein zugeordnetes Benutzerkonto verwendet Authentifizierung durchführen.

3.  **OVSDB**. Es gibt keine Genehmigung für dieses Protokoll.

**Verschlüsselung**

Für die Southbound-Kommunikation werden die folgenden Verschlüsselungsmethoden für Protokolle verwendet.

1. **WCF/TCP/OVSDB**. Für diese Protokolle wird die Verschlüsselung über das Zertifikat, das registriert ist auf dem Client oder Server ausgeführt.

2. **WinRM**. WinRM-Datenverkehr wird standardmäßig unter Verwendung des Kerberos-Security Support Provider verschlüsselt \(SSP\). Sie können zusätzliche Verschlüsselung in Form von SSL auf dem WinRM-Server konfigurieren.
