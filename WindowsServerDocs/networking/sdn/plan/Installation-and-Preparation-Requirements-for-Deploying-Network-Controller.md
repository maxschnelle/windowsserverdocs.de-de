---
title: Anforderungen für die Bereitstellung des Netzwerk Controllers
description: Bereiten Sie Ihr Daten Center auf die Bereitstellung des Netzwerk Controllers vor, für die mindestens ein Computer oder ein virtueller Computer und ein Computer oder ein virtueller Computer erforderlich ist. Bevor Sie den Netzwerk Controller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Protokolldatei Speicherorte (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.
manager: grcusanz
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/10/2018
ms.openlocfilehash: 051518873bd028e8b1253b9bf7cb17dcff344d0d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996602"
---
# <a name="requirements-for-deploying-network-controller"></a>Anforderungen für die Bereitstellung des Netzwerk Controllers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Bereiten Sie Ihr Daten Center auf die Bereitstellung des Netzwerk Controllers vor, für die mindestens ein Computer oder ein virtueller Computer und ein Computer oder ein virtueller Computer erforderlich ist. Bevor Sie den Netzwerk Controller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Protokolldatei Speicherorte (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.


## <a name="network-controller-requirements"></a>Anforderungen an den Netzwerk Controller

Die Bereitstellung des Netzwerk Controllers erfordert mindestens einen Computer oder virtuelle Computer, die als Netzwerk Controller fungieren, sowie einen Computer oder einen virtuellen Computer, der als Verwaltungs Client für den Netzwerk Controller fungieren soll.

- Auf allen VMS und Computern, die als Netzwerk Controller Knoten geplant sind, muss Windows Server 2016 Datacenter Edition ausgeführt werden.
- Auf jedem Computer oder virtuellen Computer (VM), auf dem Sie den Netzwerk Controller installieren, muss die Datacenter Edition von Windows Server 2016 ausgeführt werden.
- Auf dem Verwaltungs Client Computer oder der VM für den Netzwerk Controller muss Windows 10 ausgeführt werden.


## <a name="configuration-requirements"></a>Konfigurationsanforderungen

Vor der Bereitstellung des Netzwerk Controllers müssen Sie die Sicherheitsgruppen, die Protokolldatei Speicherorte (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.

### <a name="step-1-configure-your-security-groups"></a>Schritt 1: Sicherheitsgruppen konfigurieren

Als erstes erstellen Sie zwei Sicherheitsgruppen für die Kerberos-Authentifizierung.

Sie erstellen Gruppen für Benutzer, die über die folgenden Berechtigungen verfügen:

1. Netzwerk Controller konfigurieren<p>Sie können dieser Gruppe beispielsweise Netzwerk Controller-Administratoren benennen.
2.  Konfigurieren und Verwalten des Netzwerks mithilfe des Netzwerk Controllers<p>Beispielsweise können Sie dieser Gruppe Netzwerk Controller Benutzer benennen. Verwenden Sie Representational State Transfer (Rest), um den Netzwerk Controller zu konfigurieren und zu verwalten.

>[!NOTE]
>Alle Benutzer, die Sie hinzufügen, müssen Mitglied der Gruppe "Domänen Benutzer" in Active Directory Benutzer und Computer sein.

### <a name="step-2-configure-log-file-locations-if-needed"></a>Schritt 2: Protokolldatei Speicherorte bei Bedarf konfigurieren

Als Nächstes konfigurieren Sie die Dateispeicher Orte für die Speicherung von Netzwerk Controller-Debugprotokollen entweder auf dem Netzwerk Controller Computer, auf dem virtuellen Computer oder auf einer Remote Dateifreigabe.

>[!NOTE]
>Wenn Sie die Protokolle in einer Remote Dateifreigabe speichern, stellen Sie sicher, dass die Freigabe vom Netzwerk Controller aus zugänglich ist.


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>Schritt 3: Konfigurieren der dynamischen DNS-Registrierung für den Netzwerk Controller

Schließlich möchten Sie als nächstes Netzwerk Controller-Cluster Knoten im gleichen Subnetz oder in anderen Subnetzen bereitstellen.


|         Situation         |                                                                                                                                                         Folge                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Im gleichen Subnetz:  |                                                                                                                                Sie müssen die Rest-IP-Adresse des Netzwerk Controllers angeben.                                                                                                                                 |
| In unterschiedlichen Subnetzen | Sie müssen den Rest-DNS-Namen des Netzwerk Controllers angeben, den Sie während des Bereitstellungs Vorgangs erstellen. Sie müssen auch die folgenden Schritte ausführen:<ul><li>Konfigurieren Sie dynamische DNS-Updates für den DNS-Namen des Netzwerk Controllers auf dem DNS-Server.</li><li>Beschränken Sie die dynamischen DNS-Updates nur auf Netzwerk Controller Knoten.</li></ul> |

---

> [!NOTE]
> Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

1. Dynamische DNS-Updates für eine Zone zulassen.

   a. Öffnen Sie den DNS-Manager, und klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die entsprechende Zone, und klicken Sie dann auf **Eigenschaften**.

   b. Überprüfen Sie auf der Registerkarte **Allgemein** , ob der Zonentyp entweder **primär** oder **Active Directory integriert**ist.

   c. Vergewissern Sie sich unter **dynamische Updates**, dass **Secure only** ausgewählt ist, und klicken Sie dann auf **OK**.

2. Konfigurieren von DNS-Zonen Sicherheits Berechtigungen für Netzwerk Controller Knoten

   a.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Erweitert**.

   b. Klicken Sie unter **Erweiterte Sicherheitseinstellungen**auf **Hinzufügen**.

   c. Klicken Sie auf **Prinzipal auswählen**.

   d. Klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konto oder Gruppe auswählen** auf **Objekttypen**.

   e. Wählen Sie unter **Objekttypen**die Option **Computer**aus, und klicken Sie dann auf **OK**.

   f. Geben Sie im Dialogfeld **Benutzer, Computer, Dienst Konto oder Gruppe auswählen** den NetBIOS-Namen eines der Netzwerk Controller Knoten in der Bereitstellung ein, und klicken Sie dann auf **OK**.

   g. Überprüfen Sie unter **Berechtigungs Eintrag**die folgenden Werte:

      - **Typ** = zulassen
      - **Gilt für** = dieses Objekt und alle untergeordneten Objekte

   h. Wählen Sie unter **Berechtigungen**die Option **alle Eigenschaften schreiben** und **Löschen**aus, und klicken Sie dann auf **OK**.

3. Wiederholen Sie diesen Vorgang für alle Computer und VMS im Netzwerk Controller Cluster.

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>Schritt 4. Konfigurieren des Dienst Prinzipal namens bei Verwendung der Kerberos-basierten Authentifizierung

Wenn der Netzwerk Controller die Kerberos-basierte Authentifizierung für die Kommunikation mit Verwaltungs Clients verwendet, müssen Sie einen Dienst Prinzipal Namen (SPN) für den Netzwerk Controller in Active Directory konfigurieren. Der SPN wird vom Netzwerk Controller automatisch konfiguriert. Sie müssen lediglich Berechtigungen für die Netzwerk Controller Computer bereitstellen, um den SPN zu registrieren und zu ändern. Weitere Informationen finden Sie unter [Konfigurieren von Dienst Prinzipal Namen (SPN)](../security/kerberos-with-spn.md#configure-service-principal-names-spn).

## <a name="deployment-options"></a>Bereitstellungsoptionen

### <a name="network-controller-deployment"></a>Netzwerk Controller-Bereitstellung

Das Setup ist mit drei Netzwerk Controller Knoten hoch verfügbar, die auf virtuellen Maschinen konfiguriert sind. Außerdem werden zwei Mandanten mit dem virtuellen Netzwerk von Mandant 2 in zwei virtuelle Subnetze unterteilt, um eine webeebene und eine Datenbankebene zu simulieren.

![SDN-NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>Bereitstellung von Netzwerk Controllern und Software Lastenausgleich

Für hohe Verfügbarkeit gibt es zwei oder mehr SLB/MUX-Knoten.

![SDN-NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>Bereitstellung von Netzwerk Controllern, Software Load Balancer und RAS-Gateways

Es gibt drei virtuelle Gateway-Computer: zwei sind aktiv, und eine ist redundant.

![SDN-NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)

>[!IMPORTANT]
>Wenn Sie mithilfe von VMM bereitstellen, stellen Sie sicher, dass die virtuellen Computer der Infrastruktur (VMM-Server, AD/DNS, SQL Server usw.) nicht auf einem der vier in den Diagrammen angezeigten Hosts gehostet werden.


## <a name="next-steps"></a>Nächste Schritte
[Planen Sie eine Software definierte Netzwerkinfrastruktur](./plan-a-software-defined-network-infrastructure.md).

## <a name="related-topics"></a>Verwandte Themen
- [Netzwerkcontroller](../technologies/network-controller/Network-Controller.md)
- [Hohe Verfügbarkeit des Netzwerk Controllers](../technologies/network-controller/network-controller-high-availability.md)
- [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
- [Installieren der Serverrolle „Netzwerkcontroller“ mit Server-Manager](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)