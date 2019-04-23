---
title: Hohen Verfügbarkeit auf die Web-Front RD Web- und Gatewaycomputers hinzufügen
description: Enthält eine schrittweise Anleitung zum Installieren von den RD-Web "und" Gateway-Server in einer RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 11/08/2016
manager: dongill
ms.openlocfilehash: fa09532e0b327b24ebb1c0e155c26c25d1043b63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854601"
---
# <a name="add-high-availability-to-the-rd-web-and-gateway-web-front"></a>Hohen Verfügbarkeit auf die Web-Front RD Web- und Gatewaycomputers hinzufügen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Sie können eine Remote-Remotedesktop-Webzugriff (RD-Webzugriff) und Remotedesktopgateway (RD-Gateway)-Farm, zur Verbesserung der Verfügbarkeit und Skalierung einer Windows Server Remote Desktop Services (RDS)-Bereitstellung bereitstellen. 

Verwenden Sie die folgenden Schritte aus, um das Hinzufügen eines RD-Web- und Gateway-Servers zu einer vorhandenen einfachen Remote Desktop Services-Bereitstellung.  

## <a name="pre-requisites"></a>Voraussetzungen

Einrichten eines Servers als zusätzliche RD-Web und RD-Gateway - fungieren kann dies entweder ein physischer Server oder virtuellen Computer sein. Dies schließt den Server der Beitritt zur Domäne und Aktivieren der Remoteverwaltung.

## <a name="step-1-configure-the-new-server-to-be-part-of-the-rds-environment"></a>Schritt 1: Konfigurieren Sie den neuen Server als Teil der RDS-Umgebung

1. Verbinden Sie mit dem RDMS-Server im Azure-Portal, über Remote Desktop Connection-Client.
2. Fügen Sie den neuen RD-Web- und Gateway-Server zu Server-Manager hinzu:
    1. Starten Sie den Server-Manager, klicken Sie auf **verwalten > Hinzufügen von Servern**.   
    2. Klicken Sie in das Dialogfeld "Server hinzufügen" auf **Jetzt suchen**.   
    3. Wählen Sie den neu erstellten RD Web- und Gatewaycomputers Server (z. B. Contoso-WebGw2) aus, und klicken Sie auf **OK**.
3. Hinzufügen von RD-Web und Gatewayservern zur Bereitstellung  
    1. Server-Manager zu starten.  
    2. Klicken Sie auf **Remote Desktop Services > Übersicht > Bereitstellungsserver > Vorgänge > Hinzufügen von Servern mit Web Access für Remotedesktop-**.   
    3. Wählen Sie den neu erstellten Server (z. B. Contoso-WebGw2), und klicken Sie dann auf **Weiter**.  
    4. Wählen Sie auf der Bestätigungsseite **Remotecomputer neu starten, je nach Bedarf**, und klicken Sie dann auf **hinzufügen**.  
    5. Wiederholen Sie diese Schritte aus, um den RD-Gateway-Server hinzufügen, aber wählen **RD-Gatewayservern** in Schritt b.
4. Installieren Sie Zertifikate für die RD-Gateway-Server neu:
    1.  Klicken Sie im Server-Manager auf dem Server RDMS **Remote Desktop Services > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
    2.  Erweitern Sie **Zertifikate**.  
    3.  Scrollen Sie nach unten zur Tabelle. Klicken Sie auf Remotedesktop **Remotedesktopgateway-Rollendiensts > vorhandenes Zertifikat auswählen.**  
    4.  Klicken Sie auf **wählen Sie ein anderes Zertifikat** und suchen Sie dann den Speicherort des Zertifikats. Z. B. \Contoso-CB1\Certificates). Wählen Sie die Zertifikatdatei für den RD-Web "und" Gateway-Server, die während der die erforderlichen Komponenten (z. B. ContosoRdGwCert) erstellt, und klicken Sie dann auf **öffnen**.  
    5.  Geben Sie das Kennwort für das Zertifikat, wählen **können Sie das Zertifikat dem Zertifikatspeicher "Vertrauenswürdige Stammzertifizierungsstellen" auf den Zielcomputern hinzugefügt werden**, und klicken Sie dann auf **OK**.  
    6.  Klicken Sie auf **Übernehmen**.
    > [!Note] 
    > Sie müssen die TSGateway-Dienst ausgeführt wird, auf jedem Remotedesktopgateway-Server entweder über Server-Manager oder Task-Manager manuell neu starten.
    7.  Wiederholen Sie die Schritte a bis f für den RD-Web Access-Rollendienst.

## <a name="step-2-configure-rd-web-and-rd-gateway-properties-on-the-new-server"></a>Schritt 2: Konfigurieren von RD-Web und RD-Gateway-Eigenschaften auf dem neuen server
1. Konfigurieren der Server eine RD-gatewayfarm angehören:
    1.  Klicken Sie im Server-Manager auf dem Server RDMS **alle Server**. Mit der rechten Maustaste eine der Remotedesktop-Gatewayserver, und klicken Sie dann auf **Remotedesktopverbindung**.
    2.  Melden Sie sich an den RD-Gateway-Server unter Verwendung eines Domänenkontos für den Administrator.  
    3.  Klicken Sie im Server-Manager auf dem Remotedesktop-Gatewayserver **Tools > Remotedesktopdienste > Remotedesktopgateway-Manager**.  
    4.  Klicken Sie im Navigationsbereich auf dem lokalen Computer (z. B. Contoso-WebGw1).  
    5.  Klicken Sie auf **Hinzufügen des Remotedesktop-Gatewayserverfarm Mitglieder**.  
    6.  Auf der **Serverfarm** Registerkarte, geben Sie den Namen der einzelnen RD-Gateway-Server, und klicken Sie dann **hinzufügen** und **übernehmen**.  
    7.  Wiederholen Sie Schritte a bis f auf jedes RD-Gatewayserver, so dass sie gegenseitig als RD-Gateway-Server in einer Farm erkennen. Führen Sie besteht kein Problem, wenn es Warnungen angezeigt werden, wie es für die DNS-Verteilung dauern kann.
2. Konfigurieren des Servers als Teil einer Farm Web Access für Remotedesktop. Die folgenden Schritte aus, Konfigurieren der Überprüfung und Entschlüsselungsschlüssel für Computer, um an beiden Standorten RDWeb identisch sein.
    1.  Klicken Sie im Server-Manager auf dem Server RDMS **alle Server**. Mit der rechten Maustaste in der ersten Web Access für Remotedesktop-Servers (z. B. Contoso-WebGw1), und klicken Sie dann auf **Remotedesktopverbindung**.  
    2.  Melden Sie sich die Web Access für Remotedesktop-Server unter Verwendung eines Domänenkontos für den Administrator.  
    3.  Klicken Sie im Server-Manager auf dem Server Web Access für Remotedesktop **Tools > (Internet Information Services, IIS) Manager**.  
    4.  Erweitern Sie im linken Bereich des IIS-Managers die **Server (z. B. Contoso-WebGw1) > Websites > Default Web Site**, und klicken Sie dann auf **RDWeb**.  
    5.  Mit der rechten Maustaste **Computerschlüssel**, und klicken Sie dann auf **Funktion öffnen**.
    6.  Auf der Seite Computerschlüssel in die **Aktionen** wählen Sie im Bereich **Generate Keys**, und klicken Sie dann auf **übernehmen**.
    7.  Kopieren Sie den Validierungsschlüssel (Sie können mit der rechten Maustaste in des Schlüssels, und klicken Sie dann auf **Kopie**.)
    8.  Im IIS-Manager unter **Default Web Site**Option **Feed**, **FeedLogon** und **Seiten** wiederum.
    9. Für die einzelnen:
        1.  Mit der rechten Maustaste **Computerschlüssel**, und klicken Sie dann auf **Funktion öffnen**.
        2.  Deaktivieren Sie für den Validierungsschlüssel **automatisch zur Laufzeit generieren**, und fügen Sie den Schlüssel, die Sie in Schritt g kopiert haben.
    10.  Minimieren Sie das Fenster des Remotedesktop-Verbindung mit diesem RD-Web-Server.  
    11.  Wiederholen Sie die Schritte b bis e für den zweiten Web Access für Remotedesktop-Server, die Ansicht "Feature", der am **Computerschlüssel**.
    12. Deaktivieren Sie für den Validierungsschlüssel **automatisch zur Laufzeit generieren**, und fügen Sie den Schlüssel, die Sie in Schritt g kopiert haben.
    13. Klicken Sie auf **Übernehmen**.
    14. Führen Sie diesen Vorgang für die **RDWeb**, **Feed**, **FeedLogon** und **Seiten** Seiten.
    15. Minimieren Sie das Fenster des Remotedesktop-Verbindung an den zweiten Server mit Web Access für Remotedesktop, und Maximieren Sie das Fenster des Remotedesktop-Verbindung mit der ersten Server mit Web Access für Remotedesktop.  
    16. Wiederholen Sie Schritte g bis n, um den Entschlüsselungsschlüssel zu kopieren.
    17. Wenn Überprüfungsschlüssel und Entschlüsselungsschlüssel unterscheiden sich auf beiden Servern Web Access für Remotedesktop für den **RDWeb**, **Feed**, **FeedLogon** und **Seiten**Seiten, melden Sie sich alle Remotedesktop-Fenster.

## <a name="step-3-configure-load-balancing-for-the-rd-web-and-rd-gateway-servers"></a>Schritt 3: Konfigurieren des Lastenausgleichs für die RD-Web und RD-Gateway-Server

Wenn Sie Azure-Infrastruktur verwenden, können Sie einen Azure Load Balancer erstellen; Wenn dies nicht der Fall ist, können Sie einen separaten Hardware oder Software Load Balancer einrichten. Der Lastenausgleich Schlüssel ist, sodass Datenverkehr gleichmäßig verteilt die langlebigen Verbindungen über Remote Desktop-Clients über das RD-Gateway, auf die Server, dass Benutzer ihre Workloads ausgeführt werden soll.

> [!Note] 
> Wenn der vorherige Server ausgeführt wird, RD-Web und RD-Gateway hinter einem externen Load Balancer bereits eingerichtet wurde, fahren Sie zum Schritt 4, wählen Sie den vorhandenen Back-End-Pool, und fügen den neuen Server für den Pool.

1.  Erstellen Sie einen Azure Load Balancer:  
    1.  Im Azure-Portal auf **Durchsuchen > Load Balancer > Add**.  
    2.  Geben Sie einen Namen ein, z. B. **WebGwLB**.  
    3.  Wählen Sie **öffentliche** für die **Schema**, **öffentliche IP-Adresse**, und ein **öffentliche IP-Adresse**. Sie können wählen Sie eine vorhandene öffentliche IP-Adresse oder einen neuen erstellen. 
    4.  Wählen Sie das entsprechende **Abonnement**, **Ressourcengruppe**, und **Speicherort**.
    5.  Klicken Sie auf **Erstellen**.  
2. Erstellen Sie eine [Test](https://azure.microsoft.com/documentation/articles/load-balancer-custom-probe-overview/) überwachen, welche Server aktiv sind:  
    1.  Im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule**., den Load Balancer erstellte z. B. WebGwLB und Einstellungen  
    2.  Klicken Sie auf **Tests > hinzufügen**.  
    3.  Geben Sie einen Namen ein, z. B. **HTTPS**, für den Test. Wählen Sie **TCP** als die **Protokoll**, und geben Sie **443** für die **Port**, klicken Sie dann auf **OK**.   
3.  Erstellen Sie die HTTPS- und UDP-lastenausgleichsregeln:  
    1.  In **Einstellungen**, klicken Sie auf **Lastenausgleichsregeln**.  
    2.  Wählen Sie **hinzufügen** für die **-HTTPS-Regel**.  
    3.  Geben Sie einen Namen für die Regel ein, z. B. HTTPS, und wählen Sie **TCP** für die **Protokoll**. Geben Sie **443** für beide **Port** und **Back-End-Port**, und klicken Sie auf **OK**.  
    4.  In **Lastenausgleichsregeln**, klicken Sie auf **hinzufügen** für die **UDP-Regel**.  
    5.  Geben Sie einen Namen für die Regel ein, z. B. **UDP**, und wählen Sie **UDP** für die **Protokoll**. Geben Sie **3391** für beide **Port** und **Back-End-Port**, und klicken Sie auf **OK**.  
4. Erstellen Sie die Back-End-Adresspool für die RD-Web und RD-Gateway-Server:
      1. In **Einstellungen**, klicken Sie auf **Back-End-Adresspools > Add**.   
      2. Geben Sie einen Namen (z. B. **WebGwBackendPool**), klicken Sie dann auf **Hinzufügen eines virtuellen Computers**.  
      3. Wählen Sie eine verfügbarkeitsgruppe (z. B. WebGwAvSet), und klicken Sie dann auf **OK**.   
      4. Klicken Sie auf **wählen Sie die virtuellen Computer**, wählen Sie die virtuellen Computer aus, und klicken Sie dann auf **auswählen > OK > OK**.
