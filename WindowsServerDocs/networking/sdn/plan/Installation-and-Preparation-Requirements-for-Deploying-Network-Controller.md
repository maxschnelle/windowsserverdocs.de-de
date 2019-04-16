---
title: Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller
description: In diesem Thema können Sie Ihrem Datencenter Netzwerkcontroller Bereitstellung vorzubereiten.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c50a2167a894871ea76fb96523c19531100648ce
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="installation-and-preparation-requirements-for-deploying-network-controller"></a>Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Ihrem Datencenter Netzwerkcontroller Bereitstellung vorzubereiten.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema ist die folgende Netzwerk-Controller-Dokumentation verfügbar.  
> 
> - [Netzwerkcontroller](../technologies/network-controller/Network-Controller.md)
> - [Netzwerk-Controller mit hoher Verfügbarkeit](../technologies/network-controller/network-controller-high-availability.md)
> - [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [Installieren Sie die Netzwerk-Controller-Serverrolle mit Server-Manager](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)  

Es folgen die Installation, Software und anderen Anforderungen und zur Vorbereitung Maßnahmen ergreifen müssen vor der Bereitstellung von Netzwerkcontroller.

## <a name="installation-requirements"></a>Anforderungen für die Installation

Im folgenden werden die Installationsanforderungen für Netzwerkcontroller.

- Zur Bereitstellung von Windows Server 2016 können Sie Netzwerkcontroller auf einem oder mehreren Computern, einen oder mehrere virtuelle Maschinen oder eine Kombination von Computern und virtuellen Maschinen bereitstellen. Alle virtuellen Maschinen und Computern im Netzwerk-Controller-Knoten geplant müssen Windows Server 2016 Datacenter Edition ausgeführt werden.

## <a name="software-requirements"></a>Anforderungen der Clientsoftware

Bereitstellung von Domänencontrollern erfordert eine oder mehrere Computer oder virtuelle Maschinen, die als Netzwerk-Controller und einem Computer dienen oder virtuellen Computer als einen Verwaltungsclient für den Netzwerkcontroller dienen soll. Diese Computer oder virtuelle Computer müssen die folgenden Betriebssysteme ausführen.  

- Alle Computer oder virtuellen Computer (VM) auf dem Sie Netzwerkcontroller installieren, muss die Datacenter-Edition von Windows Server 2016 ausgeführt werden.  
  
- Das Management Client-Computer oder virtuellen Computer für den Netzwerkcontroller muss Windows 8, Windows 8.1 oder Windows 10 ausgeführt werden.  
  
## <a name="additional-requirements"></a>Zusätzliche Anforderungen

Folgendes sind zusätzliche Schritte müssen Sie vor dem Bereitstellen des Netzwerkcontrollers ausführen.
  
### <a name="configure-security-groups"></a>Konfigurieren von Sicherheitsgruppen
  
Wenn die Computer oder VMs für Netzwerkcontroller und den Verwaltungsclient Domäne befinden, konfigurieren Sie die folgenden Sicherheitsgruppen für die Kerberos-Authentifizierung.

- Erstellen einer Sicherheitsgruppe ein, und fügen Sie alle Benutzer, die die Berechtigung zum Konfigurieren von Netzwerk-Controller hinzu. Erstellen Sie z. B. eine Gruppe namens **Controller Netzwerkadministratoren**. Alle Benutzer, die Sie dieser Gruppe hinzufügen. Außerdem muss die Mitglieder der **Domänenbenutzer** Gruppe in Active Directory-Benutzer und -Computer.  
  
    > [!NOTE]  
    > Weitere Informationen zum Erstellen einer gruppenverwaltetes in Active Directory-Benutzer und -Computer finden Sie unter [Erstellen einer neuen Gruppe](https://technet.microsoft.com/en-us/library/cc783256(v=ws.10).aspx).  

- Erstellen Sie eine Sicherheitsgruppe, und fügen Sie alle Benutzer, die über die Berechtigung zum Konfigurieren und verwalten das Netzwerk mithilfe von Netzwerkcontroller hinzu.  Z. B. erstellen eine neue Gruppe namens **Controller Netzwerkbenutzer**. Alle Benutzer, die Sie in die neue Gruppe hinzufügen. Außerdem muss die Mitglieder der **Domänenbenutzer** Gruppe in Active Directory-Benutzer und -Computer. Alle Netzwerk-Controller-Konfiguration und Verwaltung wird mit Representational State Transfer \(REST\) ausgeführt.

### <a name="configure-log-file-locations-if-needed"></a>Konfigurieren Sie Speicherorte der Protokolldateien, ggf.

Sie können die Debugprotokolle Netzwerkcontroller auf die Netzwerk-Controller-Computer oder virtuellen Computer oder auf einer Remotedateifreigabe speichern. Wenn die Protokolle in einer Remotedateifreigabe gespeichert werden soll, stellen Sie sicher, dass die Freigabe von Netzwerkcontroller zugänglich ist.

### <a name="configure-dynamic-dns-registration-for-network-controller"></a>Konfigurieren von dynamischen DNS-Registrierung für den Netzwerkcontroller
  
Sie können dem Netzwerkcontroller Clusterknoten im selben Subnetz oder in unterschiedlichen Subnetzen bereitstellen. 

>[!NOTE]
>Wenn die Netzwerk-Controller-Knoten im gleichen Subnetz befinden, müssen Sie die Netzwerk-Controller REST IP-Adresse bereitstellen, beim Konfigurieren von dynamischen DNS-Registrierung für den Netzwerkcontroller. Wenn die Knoten in unterschiedlichen Subnetzen befinden, müssen Sie den Netzwerk-Controller REST DNS-Namen angeben, beim Konfigurieren der dynamischen DNS-Registrierung.

Wenn Sie Netzwerkcontroller Knoten in unterschiedlichen Subnetzen befinden, müssen Sie die folgende zusätzliche DNS-Konfiguration ausführen:

- Erstellen Sie einen DNS-Namen für den Netzwerkcontroller während des Bereitstellungsprozesses

- Konfigurieren Sie dynamische DNS-Updates für die Netzwerk-Controller DNS-Namen auf dem DNS-server

- Beschränken Sie das dynamische DNS-Updates nur Knoten Netzwerkcontroller

Sie können die folgenden Verfahren konfigurieren Sie dynamische DNS-Updates und dynamische Aktualisieren von dem Netzwerkcontroller Eintrag verwenden.

> [!NOTE]
> Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritte ausführen.
  
#### <a name="to-allow-dns-dynamic-updates-for-a-zone"></a>Um dynamische DNS-Updates für eine Zone zu ermöglichen.

1. Öffnen Sie die DNS-Manager.

2. Klicken Sie in der Konsolenstruktur mit der rechten Maustaste der entsprechenden Zone, und klicken Sie dann auf **Eigenschaften**. Der Zone **Eigenschaften** Dialogfeld wird geöffnet.

3. Auf der **allgemeine** Registerkarte, stellen Sie sicher, dass der Zonentyp entweder **primären** oder **Active Directory-integrierte**.

4. In **dynamische Updates**, überprüfen Sie, ob **nur sichere** ausgewählt ist. Wenn es nicht aktiviert ist, ändern Sie den Wert der **dynamische Updates** auf **nur sichere**, und klicken Sie dann auf **OK**.

#### <a name="to-configure-dns-zone-security-permissions-for-network-controller-nodes"></a>So konfigurieren Sie DNS-Zone Sicherheitsberechtigungen für die Netzwerk-Controller-Knoten

1.  Öffnen Sie die DNS-Manager.

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste der entsprechenden Zone, und klicken Sie dann auf **Eigenschaften**. Der Zone **Eigenschaften** Dialogfeld wird geöffnet.

3.  Klicken Sie auf die **Security** Registerkarte, und klicken Sie dann auf **erweitert**. Die **Advanced Security Settings** Dialogfeld wird geöffnet.

4. In **Advanced Security Settings**, klicken Sie auf **hinzufügen**. Die **Berechtigungseintrag** Dialogfeld wird geöffnet.
  
5. Klicken Sie auf **Prinzipal auswählen**. Die **Benutzer, Computer, Dienstkonto oder Gruppe** Dialogfeld wird geöffnet.

6. In der **Benutzer, Computer, Dienstkonto oder Gruppe** Dialogfeld, klicken Sie auf **Objekttypen**. Die **Objekttypen** Dialogfeld wird geöffnet. 

7. In **Objekttypen**Option **Computer**, und klicken Sie dann auf **OK**.

8. In der **Benutzer, Computer, Dienstkonto oder Gruppe** Dialogfeld Geben Sie den NetBIOS-Namen von einem der Knoten Netzwerkcontroller in Ihrer Bereitstellung, und klicken Sie dann auf **OK**.

9. In **Berechtigungseintrag**, stellen Sie sicher, dass den Wert der **Typ** ist **zulassen**, und der Wert der **gilt für** ist **dieses Objekt und alle untergeordneten Objekte**.
  
10. Wählen Sie unter Berechtigungen **alle Eigenschaften schreiben** und **löschen**, und klicken Sie dann auf **OK**.

11. Wiederholen Sie die Schritte **5** über **10** für alle Computer und virtuellen Maschinen im Cluster Netzwerkcontroller.

Weitere Informationen finden Sie unter [Planen einer Software definiert Netzwerkinfrastruktur](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure).
