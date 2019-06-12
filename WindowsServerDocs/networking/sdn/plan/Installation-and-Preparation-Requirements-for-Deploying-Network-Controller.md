---
title: Anforderungen für die Bereitstellung des Netzwerkcontrollers
description: Vorbereiten Sie Ihres Datencenters für die Bereitstellung des Netzwerkcontrollers, die eine oder mehrere Computer oder virtuelle Computer und einem einzigen Computer oder VM erforderlich ist. Bevor Sie den Netzwerkcontroller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Speicherorte der Protokolldateien (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: pashort
author: shortpatti
ms.date: 08/10/2018
ms.openlocfilehash: 51ba991397a7c35ee0198f8e75c67b2f99b7c7bc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446315"
---
# <a name="requirements-for-deploying-network-controller"></a>Anforderungen für die Bereitstellung des Netzwerkcontrollers

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Vorbereiten Sie Ihres Datencenters für die Bereitstellung des Netzwerkcontrollers, die eine oder mehrere Computer oder virtuelle Computer und einem einzigen Computer oder VM erforderlich ist. Bevor Sie den Netzwerkcontroller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Speicherorte der Protokolldateien (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.


## <a name="network-controller-requirements"></a>Controller-netzwerkanforderungen

Bereitstellung des Netzwerkcontrollers erfordert eine oder mehrere Computer oder virtuelle Computer, dienen als Netzwerkcontroller und einen Computer, oder VM als einen Verwaltungsclient für den Netzwerkcontroller verwendet werden. 

- Alle VMs und Computer, die als Knoten für den Netzwerkcontroller geplant müssen Windows Server 2016 Datacenter Edition ausgeführt werden. 
- Alle Computer oder virtuellen Computer (VM) auf dem Sie den Netzwerkcontroller installieren, muss die Datacenter-Edition von Windows Server 2016 ausgeführt werden. 
- Dem Management-Client-Computer oder virtuellen Computer für den Netzwerkcontroller muss Windows 10 ausgeführt werden. 


## <a name="configuration-requirements"></a>Konfigurationsanforderungen

Vor der Bereitstellung des Netzwerkcontrollers, müssen Sie die Sicherheitsgruppen, die Speicherorte der Protokolldateien (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.

### <a name="step-1-configure-your-security-groups"></a>Schritt 1 Konfigurieren von Sicherheitsgruppen

Zunächst zu tun ist, zwei Sicherheitsgruppen für die Kerberos-Authentifizierung zu erstellen. 

Sie erstellen Sie Gruppen für Benutzer mit Berechtigung zum: 

1. Konfigurieren Sie den Netzwerkcontroller<p>Sie können diese Gruppe von Netzwerk-Controller-Administratoren, z. B. benennen. 
2.  Konfigurieren Sie und verwalten Sie des Netzwerks mithilfe des Netzwerkcontrollers<p>Sie können z. B. Netzwerkcontroller-Benutzer, dieser Gruppe benennen. Verwenden Sie zum Konfigurieren und verwalten den Netzwerkcontroller Representational State Transfer (REST).

>[!NOTE]
>Alle Benutzer, die Sie hinzufügen müssen der Gruppe "Domänenbenutzer" in Active Directory-Benutzer und-Computer angehören.

### <a name="step-2-configure-log-file-locations-if-needed"></a>Schritt 2 Konfigurieren von Speicherorten von Protokolldateien bei Bedarf

Als Nächstes zu tun ist, die Dateispeicherorte zum Speichern von Netzwerkcontroller-Debug-Protokolle auf dem Netzwerkcontroller-Computer oder virtuellen Computer oder auf einer Remotedateifreigabe zu konfigurieren. 

>[!NOTE]
>Wenn Sie die Protokolle in einer Remotedateifreigabe speichern, stellen Sie sicher, dass die Freigabe über den Netzwerkcontroller zugänglich ist.


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>Schritt 3 Dynamische DNS-Registrierung für den Netzwerkcontroller konfigurieren

Schließlich ist als Nächstes tun möchten die Netzwerkcontroller-Clusterknoten, auf dem gleichen Subnetz oder unterschiedlichen Subnetzen bereitstellen. 


|         Situation         |                                                                                                                                                         Folge                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Im gleichen Subnetz  |                                                                                                                                Sie müssen die Netzwerk-Controller-REST-IP-Adresse angeben.                                                                                                                                 |
| In unterschiedlichen Subnetzen | Sie müssen den Netzwerk-Controller-REST-DNS-Namen angeben, die Sie während der Bereitstellung zu erstellen. Sie müssen auch die folgenden Schritte ausführen:<ul><li>Konfigurieren Sie auf dem DNS-Server dynamische DNS-Updates für den Network Controller DNS-Namen ein.</li><li>Beschränken Sie die dynamische DNS-Updates auf nur die Netzwerkcontroller-Knoten an.</li></ul> |

---

> [!NOTE]
> Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe sein, um diese Schritte ausführen.

1. Können Sie dynamische DNS-Updates für eine Zone an.

   a. Öffnen Sie den DNS-Manager, in der Konsolenstruktur mit der Maustaste der entsprechenden Zone, und klicken Sie dann auf **Eigenschaften**. 

   b. Auf der **allgemeine** Registerkarte, stellen Sie sicher, dass der Zonentyp entweder **primären** oder **Active Directory-integrierte**.

   c. In **dynamische Updates**, überprüfen Sie, ob **nur sichere** ausgewählt ist, und klicken Sie dann auf **OK**.

2. Konfigurieren von DNS-Zone Sicherheitsberechtigungen für den Netzwerkcontroller-Knoten

   a.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Erweitert**. 

   b. In **Advanced Security Settings**, klicken Sie auf **hinzufügen**. 

   c. Klicken Sie auf **Prinzipal auswählen**. 

   d. In der **Select User, Computer, Dienstkonto oder Gruppe** Dialogfeld klicken Sie auf **Objekttypen**. 

   e. In **Objekttypen**Option **Computer**, und klicken Sie dann auf **OK**.

   f. In der **Select User, Computer, Dienstkonto oder Gruppe** Dialogfeld Geben Sie den NetBIOS-Namen von einem der Knoten den Netzwerkcontroller in Ihrer Bereitstellung, und klicken Sie dann auf **OK**.

   g. In **Berechtigungseintrag**, überprüfen Sie die folgenden Werte:

      - **Typ** = zulassen
      - **Gilt für** = dieses Objekt und alle untergeordneten Objekte

   h. In **Berechtigungen**Option **alle Eigenschaften schreiben** und **löschen**, und klicken Sie dann auf **OK**.

3. Wiederholen Sie die für alle Computer und virtuellen Computern im Cluster den Netzwerkcontroller.

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>Schritt 4 Konfigurieren Sie Service Principal Name ein, wenn mithilfe von Kerberos-Authentifizierung

Wenn Netzwerkcontroller für die Kommunikation mit dem Management-Clients die Kerberos-Authentifizierung verwendet wird, müssen Sie einen Namen (SPN) für den Netzwerkcontroller in Active Directory konfigurieren. Der Netzwerkcontroller konfiguriert automatisch den SPN an. Alles, was Sie tun müssen ist, erteilen Sie Berechtigungen für die Netzwerkcontroller-Computer den SPN zu registrieren. Weitere Informationen finden Sie unter [Konfigurieren von Dienstprinzipalnamen (SPN)](https://docs.microsoft.com/windows-server/networking/sdn/security/kerberos-with-spn#configure-service-principal-names-spn).

## <a name="deployment-options"></a>Bereitstellungsoptionen

### <a name="network-controller-deployment"></a>Bereitstellung des Netzwerkcontrollers

Das Setup ist hoch verfügbar, mit drei Netzwerkcontroller-Knoten, die auf virtuellen Computern konfiguriert. Außerdem wird dargestellt zwei Mandanten mit dem Mandanten 2 im virtuellen Netzwerk in zwei virtuelle Subnetze unterteilt ist, um eine Webebene und eine Datenbankebene zu simulieren.  

![Planen der SDN-NC](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>Netzwerkcontroller und Software laden die Bereitstellung von Lastenausgleich

Für hohe Verfügbarkeit zu erzielen müssen Sie zwei oder mehr SLB/MUX-Knoten vorhanden sind.

![Planen der SDN-NC](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>Netzwerkcontroller, Softwarelastenausgleich und RAS-Gateway-Bereitstellung

Es gibt drei Gateway-VMs. zwei sind aktiv, und eine ist redundant.

![Planen der SDN-NC](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  



Für TP5-basierte bereitstellungsautomatisierung muss es sich bei der Active Directory verfügbar und aus diesen Subnetzen erreichbar sein. Weitere Informationen zu Active Directory finden Sie unter [Active Directory Domain Services Overview](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview).  

>[!IMPORTANT] 
>Wenn Sie mithilfe von VMM bereitgestellt haben, vergewissern Sie sich mit dem Ihre Infrastruktur-VMs (SQL-Server für VMM-Server, AD/DNS, usw.) nicht auf den vier Hosts, die in den Diagrammen gezeigten gehostet werden.  


## <a name="next-steps"></a>Nächste Schritte
[Planen eine Software-Defined Networking-Infrastruktur](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure).

## <a name="related-topics"></a>Verwandte Themen
- [Netzwerkcontroller](../technologies/network-controller/Network-Controller.md) 
- [Hohe Netzwerkverfügbarkeit für Controller](../technologies/network-controller/network-controller-high-availability.md) 
- [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)   
- [Installieren der Serverrolle „Netzwerkcontroller“ mit Server-Manager](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)   
