---
title: Hinzufügen eines Remotedesktop-Verbindungsbroker-Servers, um hohe Verfügbarkeit in RDS zu konfigurieren.
description: Erfahren Sie, wie Sie eine Remotedesktop-Verbindungsbroker einer RDS-Bereitstellung für hochverfügbarkeit hinzufügen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e20b4960faac0ef40ad68271fa907394344e9c47
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034428"
---
# <a name="add-the-rd-connection-broker-server-to-the-deployment-and-configure-high-availability"></a>Hinzufügen des Remotedesktop-Verbindungsbrokerservers zur Bereitstellung und Konfigurieren von hoher Verfügbarkeit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Sie können einen Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker)-Cluster zur Verbesserung der Verfügbarkeit und Skalierung der Infrastruktur Remote Desktop Services bereitstellen. 

## <a name="pre-requisites"></a>Voraussetzungen

Einrichten eines Servers als einen zweiten Remotedesktop-Verbindungsbroker - fungieren kann dies entweder auf einem physischen Server oder auf einem virtuellen Computer sein.

Richten Sie eine Datenbank aus, für den Verbindungsbroker. Sie können [Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-get-started/#create-a-new-aure-sql-database) -Instanz oder SQL Server in Ihrer lokalen Umgebung. Wir sprechen über die Verwendung von Azure SQL-unten, aber die Schritte gelten weiterhin für SQL Server. Sie müssen die Verbindungszeichenfolge für die Datenbank zu finden, und stellen Sie sicher, dass Sie den richtigen ODBC-Treiber verfügen.

## <a name="step-1-configure-the-database-for-the-connection-broker"></a>Schritt 1: Konfigurieren Sie die Datenbank für den Verbindungsbroker

1. Suchen die Verbindungszeichenfolge für die Datenbank, die Sie erstellt haben – Sie benötigen sie sowohl die Version des ODBC-Treiber zu identifizieren, Sie benötigen, und später beim Konfigurieren des Verbindungsbrokers selbst (Schritt 3), so speichern Sie die Zeichenfolge Stelle, wo Sie problemlos darauf verweisen können. Hier ist, wie Sie die Verbindungszeichenfolge für Azure SQL suchen:  
    1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen** , und klicken Sie auf die Ressourcengruppe für die Bereitstellung.   
    2. Wählen Sie die SQL-Datenbank, die Sie gerade erstellt, (z. B. CB-DB1 haben).   
    3. Klicken Sie auf **Einstellungen > Eigenschaften > Datenbank-Verbindungszeichenfolgen anzeigen**.   
    4. Kopieren Sie die Verbindungszeichenfolge für **ODBC (umfasst Node.js)** , die wie folgt aussehen sollte:   
      
        Driver = {SQL Server Native Client 13.0}; Server = Tcp:cb-sqls1.database.windows.net,1433; Database = CB-DB1; UID =sqladmin@contoso; PWD = {Your_password_here}; Verschlüsseln = Yes; TrustServerCertificate = Nein; Verbindungstimeout = 30;   
  
    5. Ersetzen Sie "Your_password_here" durch das eigentliche Kennwort ein. Sie müssen diese gesamte Zeichenfolge, mit Ihrem Kennwort enthalten verwenden, beim Verbinden mit der Datenbank. 
2. Installieren Sie den ODBC-Treiber auf der neuen Verbindungsbroker an: 
   1. Wenn Sie einen virtuellen Computer für den Verbindungsbroker verwenden, erstellen Sie eine öffentliche IP-Adresse für den ersten RD Connection Broker. (Sie müssen nur dies tun, wenn die VM RDMS nicht bereits über eine öffentliche IP-Adresse, um die RDP-Verbindungen zulassen verfügt.)
       1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung aus, und klicken Sie dann auf den ersten RD Connection Broker virtuellen Computer (z. B. Contoso-Cb1).
       2. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.
       3. Klicken Sie auf **Einstellungen > IP-Adresse**.
       4. Für **öffentliche IP-Adresse**Option **aktiviert**, und klicken Sie dann auf **IP-Adresse**.
       5. Wenn Sie eine vorhandene öffentliche IP-Adresse, die Sie verwenden möchten verfügen, wählen Sie sie aus der Liste aus. Klicken Sie anderenfalls auf **neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und dann **speichern**.
   2. Verbinden Sie mit dem ersten Remotedesktop-Verbindungsbroker:
       1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung aus, und klicken Sie dann auf den ersten RD Connection Broker virtuellen Computer (z. B. Contoso-Cb1).
       2. Klicken Sie auf **verbinden > Öffnen** den Remotedesktopclient zu öffnen.
       3. Klicken Sie auf dem Client auf **Connect**, und klicken Sie dann auf **verwenden ein anderes Benutzerkonto**. Geben Sie den Benutzernamen und das Kennwort für ein Domänenkonto für Administrator ein.
       4. Klicken Sie auf **Ja** beim des Zertifikats gewarnt.
   3. Herunterladen der [ODBC-Treiber für SQL Server](https://www.microsoft.com/download/confirmation.aspx?id=50420) , die die Version in der ODBC-Verbindungszeichenfolge entspricht. Für die oben genannten Beispielzeichenfolge müssen wir die Version 13-ODBC-Treiber zu installieren.
   4. Kopieren Sie die Datei sqlincli.msi, mit der ersten RD Connection Broker Server.   
   5. Öffnen Sie die sqlincli.msi-Datei, und installieren Sie die native Client.  
   6. Wiederholen Sie die Schritte 1 bis 5 für jede zusätzliche Remotedesktop-Verbindungsbroker (z. B. Contoso-Cb2).
   7. Installieren Sie den ODBC-Treiber auf jedem Server, auf denen den Verbindungsbroker ausgeführt wird.

## <a name="step-2-configure-load-balancing-on-the-rd-connection-brokers"></a>Schritt 2: Konfigurieren Sie den Lastenausgleich für den Remotedesktop-Verbindungsbroker 

Wenn Sie Azure-Infrastruktur verwenden, können Sie erstellen eine [Azure-Lastenausgleich](#create-a-load-balancer); Wenn nicht festgelegt werden kann um oben [DNS-Roundrobin](#configure-dns-round-robin).

### <a name="create-a-load-balancer"></a>Erstellen eines Load Balancers  
1. Erstellen Sie einen Azure Load Balancer   
      1. Im Azure-Portal auf **Durchsuchen > Load Balancer > Add**.   
      2. Geben Sie einen Namen für den neuen Load Balancer (z. B. Hacb) aus.   
      3. Wählen Sie **intern** für die **Schema**, **Virtual Network** für die Bereitstellung (z. B. Contoso-VNet), und die **Subnetz** mit allen Ihre Ressourcen (z. B. "Standard").   
      4. Wählen Sie **statische** für die **IP-Adresszuweisung** , und geben Sie einen **Private IP-Adresse** , nicht gerade verwendet (z. B. 10.0.0.32).   
      5. Wählen Sie das entsprechende **Abonnement**, **Ressourcengruppe** mit allen Ihren Ressourcen und die entsprechenden **Speicherort**.   
      6. Wählen Sie **Erstellen** aus.   
2. Erstellen Sie eine [Test](https://azure.microsoft.com/documentation/articles/load-balancer-custom-probe-overview/) überwachen, welche Server aktiv sind:   
      1. Klicken Sie im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule**, und klicken Sie dann auf den Sie gerade erstellt haben, Load Balancer (z. B. CBLB). Klicken Sie auf **Einstellungen**.   
      2. Klicken Sie auf **Tests > hinzufügen**.   
      3. Geben Sie einen Namen für den Test (z. B. **RDP**) Option **TCP** als die **Protokoll**, geben Sie **3389** für die **Port**, und klicken Sie dann auf **OK**.   
3. Erstellen Sie die Back-End-Adresspool, der den Verbindungsbroker:   
      1. In **Einstellungen**, klicken Sie auf **Back-End-Adresspools > Add**.   
      2. Geben Sie einen Namen (z. B. CBBackendPool), und klicken Sie dann **Hinzufügen eines virtuellen Computers**.  
      3. Wählen Sie eine verfügbarkeitsgruppe (z. B. CbAvSet), und klicken Sie dann auf **OK**.   
      3. Klicken Sie auf **wählen Sie die virtuellen Computer**, wählen Sie die virtuellen Computer aus, und klicken Sie dann auf **auswählen > OK > OK**.   
4. Die RDP-lastenausgleichsregel zu erstellen:   
      1. In **Einstellungen**, klicken Sie auf **Lastenausgleichsregeln**, und klicken Sie dann auf **hinzufügen**.   
      2. Geben Sie einen Namen (z. B. RDP), wählen Sie **TCP** für die **Protokoll**, geben Sie **3389** für beide **Port** und **Back-End-Port** , und klicken Sie auf **OK**.   
5. Fügen Sie einen DNS-Eintrag für den Load Balancer hinzu:   
      1. Verbinden Sie mit dem RDMS Server-Computer (z. B. Contoso-CB1). Sehen Sie sich die [bereiten Sie die RD Connection Broker VM](Prepare-the-RD-Connection-Broker-VM-for-Remote-Desktop.md) Schritte auf, wie Sie eine Verbindung mit dem virtuellen Computer herstellen.   
      2. Klicken Sie im Server-Manager **Tools > DNS**.   
      3. Erweitern Sie im linken Bereich **DNS**, klicken Sie auf dem DNS-Computer, klicken Sie auf **Forward-Lookupzonen**, und klicken Sie dann auf Ihren Domänennamen ein (z.B. "contoso.com"). (Es kann einige Sekunden, die zum Verarbeiten der Abfrage an den DNS-Server Informationen dauern).  
      4. Klicken Sie auf **Aktion > Neuer Host (A oder AAAA)** .   
      9. Geben Sie den Namen (z. B. Hacb) und die zuvor angegebenen IP-Adresse (z. B. 10.0.0.32).   

### <a name="configure-dns-round-robin"></a>Konfigurieren von DNS-Roundrobin  
  
Die folgenden Schritte sind eine Alternative zum Erstellen einer internen Azure Load Balancer.   
  
1. Verbinden Sie mit dem RDMS-Server im Azure-Portal. Mithilfe von Remote Desktop Connection-client   
2. Erstellen Sie DNS-Einträge:   
      1. Klicken Sie im Server-Manager **Tools > DNS**.   
      2. Erweitern Sie im linken Bereich **DNS**, klicken Sie auf dem DNS-Computer, klicken Sie auf **Forward-Lookupzonen**, und klicken Sie dann auf Ihren Domänennamen ein (z.B. "contoso.com"). (Es kann einige Sekunden, die zum Verarbeiten der Abfrage an den DNS-Server Informationen dauern).  
      3. Klicken Sie auf **Aktion** und **neuer Host (A oder AAAA)** .   
      4. Geben Sie die **DNS-Namen** für den Remotedesktop-Verbindungsbroker-cluster (z. B. Hacb), und geben Sie dann die **IP-Adresse** von der ersten RD Connection Broker.   
      5. Wiederholen Sie die Schritte 3 und 4 für jede zusätzliche RD Connection Broker, jede eindeutige IP-Adresse für jeden zusätzlichen Datensatz bereitstellen.


Wenn die IP-Adressen für die beiden virtuellen Computer für Remotedesktop-Verbindungsbroker 10.0.0.8 und 10.0.0.9 sind, würden Sie z. B. zwei DNS-Hosteinträge erstellen:
 - Hostname: hacb.contoso.com, IP-Adresse: 10.0.0.8
 - Hostname: hacb.contoso.com, IP-Adresse: 10.0.0.9

## <a name="step-3-configure-the-connection-brokers-for-high-availability"></a>Schritt 3: Konfigurieren der Verbindungsbroker für hohe Verfügbarkeit

1. Fügen Sie dem neuen Remotedesktop-Verbindungsbroker-Server zu Server-Manager hinzu:
   1. Klicken Sie im Server-Manager **verwalten > Hinzufügen von Servern**.
   2. Klicken Sie auf **Jetzt suchen**.
   3. Klicken Sie auf den neu erstellten RD Connection Broker Server (z. B. Contoso-Cb2), und klicken Sie auf **OK**.
2. Konfigurieren von hochverfügbarkeit für den Remotedesktop-Verbindungsbroker:
   1. Klicken Sie im Server-Manager **Remote Desktop Services > Übersicht über die**.
   2. Mit der rechten Maustaste **RD Connection Broker**, und klicken Sie dann auf **hohe Verfügbarkeit konfigurieren**.
   3. Seite mit dem Assistenten, bis Sie auf den Typ-Konfigurationsabschnitt. Wählen Sie **Shared-Datenbankserver**, und klicken Sie dann auf **Weiter**.
   4. Geben Sie den DNS-Namen für den Remotedesktop-Verbindungsbroker-Cluster aus.
   5. Geben Sie die Verbindungszeichenfolge für die SQL-Datenbank, und klicken Sie dann die Seite mit dem Assistenten zum Herstellen von hochverfügbarkeit.
3. Hinzufügen der neuen Remotedesktop-Verbindungsbroker zur Bereitstellung
   1. Klicken Sie im Server-Manager **Remote Desktop Services > Übersicht über die**.
   2. Mit der rechten Maustaste den Remotedesktop-Verbindungsbroker, und klicken Sie dann auf **hinzufügen Remotedesktop-Verbindungsbrokerserver**.
   3. Die Seite über den Assistenten, bis Sie zur Auswahl der Server zu erhalten, und wählen den neu erstellten RD Connection Broker Server (z. B. Contoso-CB2).
   4. Führen Sie den Assistenten unter Verwendung der Standardwerte.
4. Konfigurieren von vertrauenswürdigen Zertifikaten auf Remotedesktop-Verbindungsbroker-Servern und Clients.

