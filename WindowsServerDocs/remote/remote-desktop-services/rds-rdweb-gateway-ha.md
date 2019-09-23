---
title: Hinzufügen von Hochverfügbarkeit zu RD-Web und RD-Gateway (Webfront)
description: Stellt Schritte für die Installation der RD-Web- und RD-Gateway-Server in einer RDS-Bereitstellung bereit.
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
ms.openlocfilehash: 869d47be73a39114ecc05080f8da16f460fb8198
ms.sourcegitcommit: 6423dfa9cecb3b06bdd563cae113c3e80a4ec330
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2019
ms.locfileid: "71105040"
---
# <a name="add-high-availability-to-the-rd-web-and-gateway-web-front"></a>Hinzufügen von Hochverfügbarkeit zu RD-Web und RD-Gateway (Webfront)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016


Sie können eine Web Access für Remotedesktop- (RD Web Access) und Remotedesktopgateway-Farm (RD-Gateway) bereitstellen, um die Verfügbarkeit und Skalierung einer Windows Server-RDS-Bereitstellung (Remotedesktopdienste) zu verbessern. 

Führen Sie die folgenden Schritte aus, um einen RD-Web- und -Gateway-Server zu einer bestehenden einfachen Bereitstellung von Remotedesktopdiensten hinzuzufügen.  

## <a name="pre-requisites"></a>Voraussetzungen

Richten Sie einen Server ein, der als zusätzliches RD-Web und RD-Gateway fungiert. Dies kann entweder ein physischer Server oder ein virtueller Computer sein. Dazu zählt das Hinzufügen des Servers zur Domäne und die Aktivierung der Remoteverwaltung.

## <a name="step-1-configure-the-new-server-to-be-part-of-the-rds-environment"></a>Schritt 1: Konfigurieren des neuen Servers als Komponente der RDS-Umgebung

1. Stellen Sie über den Remotedesktopverbindungs-Client eine Verbindung zum RDMS-Server im Azure-Portal her.
2. Fügen Sie den neuen RD-Web- und -Gateway-Server zum Server-Manager hinzu:
    1. Starten Sie den Server-Manager, und klicken Sie auf **Verwalten > Server hinzufügen**.   
    2. Klicken Sie in das Dialogfeld „Server hinzufügen“ auf **Jetzt suchen**.   
    3. Wählen Sie den neu erstellten RD-Web- und -Gateway-Server (z. B. Contoso-WebGw2) aus, und klicken Sie auf **OK**.
3. Hinzufügen von RD-Web- und -Gateway-Servern zur Bereitstellung  
    1. Starten Sie den Server-Manager.  
    2. Klicken Sie auf **Remotedesktopdienste > Übersicht > Bereitstellungsserver > Aufgaben > RD-Web Access-Server hinzufügen**.   
    3. Wählen Sie den neu erstellten Server aus (z. B. Contoso-WebGw2), und klicken Sie dann auf **Weiter**.  
    4. Wählen Sie auf der Bestätigungsseite **Remotecomputer bei Bedarf neu starten**, und klicken Sie dann auf **Hinzufügen**.  
    5. Wiederholen Sie diese Schritte, um den RD-Gateway-Server hinzuzufügen, wählen Sie aber **RD-Gateway-Server** in Schritt b aus.
4. Installieren Sie die Zertifikate für die RD-Gateway-Server neu:
   1. Klicken Sie im Server-Manager auf dem RDMS-Server auf **Remotedesktopdienste > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
   2. Erweitern Sie **Zertifikate**.  
   3. Scrollen Sie nach unten zur Tabelle. Klicken Sie auf **RD-Gateway-Rollendienst > Vorhandenes Zertifikat auswählen**.  
   4. Klicken Sie auf **Anderes Zertifikat auswählen**, und navigieren Sie dann zum Speicherort des Zertifikats. Beispiel: \Contoso-CB1\Certificates. Wählen Sie die Zertifikatsdatei für den RD-Web- und -Gateway-Server aus, die unter den Voraussetzungen erstellt wurde (z. B. ContosoRdGwCert), und klicken Sie dann auf **Öffnen**.  
   5. Geben Sie das Kennwort für das Zertifikat ein, wählen Sie **Hinzufügen des Zertifikats zum Zertifikatsspeicher der vertrauenswürdigen Stammzertifizierungsstellen auf den Zielcomputern zulassen** aus, und klicken Sie dann auf **OK**.  
   6. Klicken Sie auf **Übernehmen**.
      > [!NOTE] 
      > Möglicherweise müssen Sie den TSGateway-Dienst, der auf jedem RD-Gateway-Server ausgeführt wird, manuell neu starten, entweder über den Server-Manager oder den Task-Manager.
   7. Wiederholen Sie die Schritte a bis f für den RD-Web Access-Rollendienst.

## <a name="step-2-configure-rd-web-and-rd-gateway-properties-on-the-new-server"></a>Schritt 2: Konfigurieren der RD-Web- und RD-Gateway-Eigenschaften auf dem neuen Server
1. Konfigurieren des Servers als Komponente einer RD-Gateway-Farm:
    1.  Klicken Sie im Server-Manager auf dem RDMS-Server auf **Alle Server**. Klicken Sie mit der rechten Maustaste auf einen der RD-Gateway-Server, und klicken Sie dann auf **Remotedesktopverbindung**.
    2.  Melden Sie sich mit einem Domänenadministrationskonto am RD-Gateway-Server an.  
    3.  Klicken Sie im Server-Manager auf dem RD-Gateway-Server auf **Tools > Remotedesktopdienste > RD-Gateway-Manager**.  
    4.  Klicken Sie im Navigationsbereich auf den lokalen Computer (z. B. Contoso-WebGw1).  
    5.  Klicken Sie auf **Mitglieder der RD-Gateway-Serverfarm hinzufügen**.  
    6.  Geben Sie auf der Registerkarte **Serverfarm** den Namen der einzelnen RD-Gateway-Server ein, und klicken Sie dann auf **Hinzufügen** und **Übernehmen**.  
    7.  Wiederholen Sie die Schritte a bis f auf den einzelnen RD-Gateway-Servern, damit sie sich gegenseitig als RD-Gateway-Server in einer Farm erkennen. Lassen Sie sich nicht verunsichern, wenn Warnungen angezeigt werden, da es einige Zeit dauern kann, bis die DNS-Einstellungen verbreitet sind.
2. Konfigurieren des Servers als Komponente einer RD-Web Access-Farm: Die folgenden Schritte konfigurieren die Schlüssel der Validierungs- und Entschlüsselungscomputer so, dass sie auf beiden RDWeb-Websites identisch sind.
    1.  Klicken Sie im Server-Manager auf dem RDMS-Server auf **Alle Server**. Klicken Sie mit der rechten Maustaste auf den ersten RD-Web Access-Server (z. B. Contoso-WebGw1) und dann auf **Remotedesktopverbindung**.  
    2.  Melden Sie sich mit einem Domänenadministrationskonto am RD-Web Access-Server an.  
    3.  Klicken Sie im Server-Manager auf dem RD-Web Access-Server auf **Tools > Internetinformationsdienste-Manager (IIS)** .  
    4.  Erweitern Sie im linken Bereich von IIS-Manager den **Server (z. B. Contoso-WebGw1) > Websites > Standardwebsite**, und klicken Sie dann auf **RDWeb**.  
    5.  Klicken Sie mit der rechten Maustaste auf **Computerschlüssel**, und klicken Sie dann auf **Feature öffnen**.
    6.  Wählen Sie auf der Seite „Computerschlüssel“ im Bereich **Aktionen** die Option **Schlüssel generieren** aus, und klicken Sie dann auf **Übernehmen**.
    7.  Kopieren Sie den Validierungsschlüssel (Sie können mit der rechten Maustaste auf den Schlüssel und dann auf **Kopieren** klicken).
    8.  Wählen Sie im IIS-Manager unter **Standardwebsite** nacheinander **Feed**, **FeedLogon** und **Seiten** aus.
    9. Gehen Sie jeweils wie folgt vor:
        1.  Klicken Sie mit der rechten Maustaste auf **Computerschlüssel**, und klicken Sie dann auf **Feature öffnen**.
        2.  Deaktivieren Sie für den Validierungsschlüssel **Automatisch zur Laufzeit generieren**, und fügen Sie dann den Schlüssel ein, den Sie in Schritt g kopiert haben.
    10.  Minimieren Sie das Fenster der RD-Verbindung auf diesen RD-Webserver.  
    11.  Wiederholen Sie die Schritte b bis e für den zweiten RD-Web Access-Server und beenden Sie die Schritte bei der Featureansicht von **Computerschlüssel**.
    12. Deaktivieren Sie für den Validierungsschlüssel **Automatisch zur Laufzeit generieren**, und fügen Sie dann den Schlüssel ein, den Sie in Schritt g kopiert haben.
    13. Klicken Sie auf **Übernehmen**.
    14. Schließen Sie diesen Prozess für die Seiten **RDWeb**, **Feed**, **FeedLogon** und **Seiten** ab.
    15. Minimieren Sie das Fenster für die RD-Verbindung auf den zweiten RD-Web Access-Server, und maximieren Sie dann das Fenster für die RD-Verbindung auf den ersten RD-Web Access-Server.  
    16. Wiederholen Sie die Schritte g bis n, um den Entschlüsselungsschlüssel zu kopieren.
    17. Wenn Validierungsschlüssel und Entschlüsselungsschlüssel auf beiden RD-Web Access-Servern für die Seiten **RDWeb**, **Feed**, **FeedLogon** und **Seiten** identisch sind, melden Sie sich von allen Fenstern für RD-Verbindungen ab.

## <a name="step-3-configure-load-balancing-for-the-rd-web-and-rd-gateway-servers"></a>Schritt 3: Konfigurieren des Lastenausgleichs für die RD-Web- und RD-Gateway-Server

Wenn Sie die Azure-Infrastruktur verwenden, können Sie einen externen Azure Load Balancer erstellen. Andernfalls können Sie einen separaten Hard- oder Softwarelastenausgleich einrichten. Der Lastenausgleich ist entscheidend, damit der Datenverkehr gleichmäßig auf die langlebigen Verbindungen von Remotedesktopclients über das RD-Gateway zu den Servern verteilt wird, auf denen die Benutzer ihre Workloads ausführen.

> [!NOTE] 
> Wenn Ihr früherer Server mit RD-Web und RD-Gateway bereits hinter einem externen Lastenausgleich eingerichtet war, fahren Sie mit Schritt 4 fort, wählen Sie den vorhandenen Back-End-Pool aus, und fügen Sie den neuen Server dem Pool hinzu.

1.  Erstellen Sie einen Azure Load Balancer:  
    1.  Klicken Sie im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule > Hinzufügen**.  
    2.  Geben Sie einen Namen ein, z. B. **WebGwLB**.  
    3.  Wähle **Öffentlich** für das **Schema** aus.
    4.  Wähle unter **Öffentliche IP-Adresse** die Option **Öffentliche IP-Adresse auswählen** aus, und wähle dann eine vorhandene öffentliche IP-Adresse aus, oder erstelle eine neue.
    5.  Wählen Sie das entsprechende **Abonnement**, eine **Ressourcengruppe** und einen **Speicherort** aus.
    6.  Klicken Sie auf **Erstellen**.  
2. Erstellen Sie einen [Test](https://azure.microsoft.com/documentation/articles/load-balancer-custom-probe-overview/), um zu überwachen, welche Server aktiv sind:  
    1.  Wähle im Azure-Portal die Option **Durchsuchen** > **Lastensaugleiche** aus, und wähle dann den Lastenausgleich aus, den du im vorherigen Schritt erstellt hast.
    2.  Wähle **Alle Einstellungen** > **Tests** > **Hinzufügen** aus.  
    3.  Geben Sie einen Namen, z. B. **HTTPS**, für den Test ein. Wählen Sie **TCP** als **Protokoll** aus, und geben Sie **443** für den **Port** ein. Klicken Sie anschließend auf **OK**.   
3.  Erstellen Sie die HTTPS- und UDP-Lastenausgleichsregeln:  
    1.  Klicken Sie unter **Einstellungen** auf **Lastenausgleichsregeln**.  
    2.  Wählen Sie **Hinzufügen** für die **HTTPS-Regel** aus.  
    3.  Geben Sie einen Namen für die Regel ein, z. B. HTTPS, und wählen Sie **TCP** für das **Protokoll** aus. Geben Sie **443** für **Port** und **Back-End-Port** ein, und klicken Sie auf **OK**.  
    4.  Klicken Sie in **Lastenausgleichsregeln** auf **Hinzufügen** für die **UDP-Regel**.  
    5.  Geben Sie einen Namen für die Regel ein, z. B. **UDP**, und wählen Sie **UDP** für das **Protokoll** aus. Geben Sie **3391** für **Port** und **Back-End-Port** ein, und klicken Sie auf **OK**.  
4. Erstellen Sie den Back-End-Pool für die RD-Web- und RD-Gateway-Server:
      1. Klicken Sie unter **Einstellungen** auf **Back-End-Adresspools > Hinzufügen**.   
      2. Geben Sie einen Namen ein (z. B. **WebGwBackendPool**), und klicken Sie dann auf **Virtuellen Computer hinzufügen**.  
      3. Wählen Sie eine Verfügbarkeitsgruppe (z. B. WebGwAvSet) aus, und klicken Sie dann auf **OK**.   
      4. Klicken Sie auf **Virtuelle Computer auswählen**, wählen Sie die einzelnen virtuellen Computer aus, und klicken Sie dann auf **Auswählen > OK > OK**.
