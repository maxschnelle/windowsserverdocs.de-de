---
title: Hinzufügen eines RD-Verbindungsbrokerservers zum Konfigurieren der Hochverfügbarkeit in RDS
description: Erfahren Sie, wie Sie einen RD-Verbindungsbroker zu einer RDS-Bereitstellung für Hochverfügbarkeit hinzufügen können.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 6e7e70b8adfcba78e50757be671d38f4d62c99db
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958702"
---
# <a name="add-the-rd-connection-broker-server-to-the-deployment-and-configure-high-availability"></a>Hinzufügen des Remotedesktop-Verbindungsbrokerservers zur Bereitstellung und Konfigurieren von hoher Verfügbarkeit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Sie können einen Remotedesktop-Verbindungsbrokercluster bereitstellen, um die Verfügbarkeit und Skalierbarkeit Ihrer Remotedesktopdienste-Infrastruktur zu verbessern. 

## <a name="pre-requisites"></a>Voraussetzungen

Richten Sie einen Server ein, der als zweiter RD-Verbindungsbroker fungiert. Dies kann entweder ein physischer Server oder ein virtueller Computer sein.

Richten Sie eine Datenbank für den Verbindungsbroker ein. Sie können die [Azure SQL-Datenbank](/azure/azure-sql/database/single-database-create-quickstart#create-a-new-aure-sql-database)-Instanz oder SQL Server in Ihrer lokalen Umgebung verwenden. Im Folgenden wird über die Verwendung von Azure SQL gesprochen, aber die Schritte gelten weiterhin für SQL Server. Sie müssen die Verbindungszeichenfolge für die Datenbank finden und sicherstellen, dass Sie über den richtigen ODBC-Treiber verfügen.

## <a name="step-1-configure-the-database-for-the-connection-broker"></a>Schritt 1: Konfigurieren der Datenbank für den Verbindungsbroker

1. Suchen Sie die Verbindungszeichenfolge für die von Ihnen erstellte Datenbank. Sie benötigen sie sowohl zur Identifizierung der benötigten Version des ODBC-Treibers als auch später, wenn Sie den Verbindungsbroker selbst konfigurieren (Schritt 3). Speichern Sie die Zeichenfolge also an einem Ort, auf den Sie problemlos verweisen können. So finden Sie die Verbindungszeichenfolge für Azure SQL  
    1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, und klicken Sie dann auf die Ressourcengruppe für die Bereitstellung.   
    2. Wählen Sie die SQL-Datenbank aus, die Sie gerade erstellt haben (z. B. CB-DB1).   
    3. Klicken Sie auf **Einstellungen** > **Eigenschaften** > **Datenbankverbindungszeichenfolgen anzeigen**.   
    4. Kopieren Sie die Verbindungszeichenfolge für **ODBC (enthält Node.js)** , die wie folgt aussehen sollte:   
      
        ```
        Driver={SQL Server Native Client 13.0};Server=tcp:cb-sqls1.database.windows.net,1433;Database=CB-DB1;Uid=sqladmin@contoso;Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
        ```
  
    5. Ersetzen Sie „your_password_here“ durch das aktuelle Kennwort. Sie verwenden diese gesamte Zeichenfolge mit Ihrem einbezogenen Kennwort, wenn Sie eine Verbindung mit der Datenbank herstellen. 
2. Installieren Sie den ODBC-Treiber für den neuen Verbindungsbroker: 
   1. Wenn Sie einen virtuellen Computer für den Verbindungsbroker verwenden, erstellen Sie eine öffentliche IP-Adresse für den ersten RD-Verbindungsbroker. (Dies ist nur erforderlich, wenn der virtuelle RDMS-Computer noch keine öffentliche IP-Adresse hat, um RDP-Verbindungen zu ermöglichen.)
       1. Klicken Sie im Azure-Portal auf **Durchsuchen** > **Ressourcengruppen**, dann auf die Ressourcengruppe für die Bereitstellung, und klicken Sie anschließend auf den ersten virtuellen Computer des RD-Verbindungsbrokers (Beispiel: Contoso-Cb1).
       2. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.
       3. Klicken Sie auf **Einstellungen > IP-Adresse**.
       4. Wählen Sie für **Öffentliche IP-Adresse** die Option **Aktiviert** aus, und klicken Sie dann auf **IP-Adresse**.
       5. Wenn Sie über eine vorhandene öffentliche IP-Adresse verfügen, die Sie verwenden möchten, wählen Sie sie in der Liste aus. Klicken Sie andernfalls auf **Neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und dann auf **Speichern**.
   2. Stellen Sie eine Verbindung mit dem ersten RD-Verbindungsbroker her:
       1. Klicken Sie im Azure-Portal auf **Durchsuchen** > **Ressourcengruppen**, dann auf die Ressourcengruppe für die Bereitstellung, und klicken Sie anschließend auf den ersten virtuellen Computer des RD-Verbindungsbrokers (Beispiel: Contoso-Cb1).
       2. Klicken Sie auf **Verbinden > Öffnen**, um den Remotedesktopclient zu öffnen.
       3. Klicken Sie auf dem Client auf **Verbinden** und dann auf **Anderes Benutzerkonto verwenden**. Geben Sie den Benutzernamen und das Kennwort für ein Domänenadministratorkonto ein.
       4. Klicken Sie in der Zertifikatwarnung auf **Ja**.
   3. Laden Sie den [ODBC-Treiber für SQL Server](https://www.microsoft.com/download/confirmation.aspx?id=50420) herunter, der der Version in der ODBC-Verbindungszeichenfolge entspricht. Für die obige Beispielzeichenfolge müssen wir den ODBC-Treiber der Version 13 installieren.
   4. Kopieren Sie die Datei „sqlincli.msi“ auf den ersten RD-Verbindungsbrokerserver.   
   5. Öffnen Sie die Datei „sqlincli.msi“, und installieren Sie den nativen Client.  
   6. Wiederholen Sie die Schritte 1-5 für jeden weiteren RD-Verbindungsbroker (z. B. Contoso-Cb2).
   7. Installieren Sie den ODBC-Treiber auf jedem Server, auf dem der Verbindungsbroker ausgeführt wird.

## <a name="step-2-configure-load-balancing-on-the-rd-connection-brokers"></a>Schritt 2: Konfigurieren des Lastenausgleichs auf den RD-Verbindungsbrokern 

Wenn Sie die Azure-Infrastruktur verwenden, können Sie einen [Azure Load Balancer](#create-a-load-balancer) erstellen. Andernfalls können Sie [DNS-Round-Robin](#configure-dns-round-robin) einrichten.

### <a name="create-a-load-balancer"></a>Erstellen eines Lastenausgleichs  
1. Erstellen eines Azure Load Balancers   
      1. Klicken Sie im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule > Hinzufügen**.   
      2. Geben Sie einen Namen für den neuen Lastenausgleich ein (z. B. hacb).   
      3. Wählen Sie **Intern** für das **Schema**, **Virtuelles Netzwerk** für Ihre Bereitstellung (z. B. Contoso-VNet) und das **Subnetz** mit all Ihren Ressourcen (z. B. Standard) aus.   
      4. Wählen Sie **Statisch** für die **IP-Adressvergabe** aus, und geben Sie eine **Private IP-Adresse** ein, die derzeit nicht verwendet wird (z. B. 10.0.0.32).   
      5. Wählen Sie das entsprechende **Abonnement**, die **Ressourcengruppe** mit allen Ihren Ressourcen und den entsprechenden **Speicherort** aus.   
      6. Wählen Sie **Erstellen** aus.   
2. Erstellen Sie einen [Test](/azure/load-balancer/load-balancer-custom-probe-overview), um zu überwachen, welche Server aktiv sind:   
      1. Klicken Sie im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule**, und klicken Sie dann auf den Lastenausgleich, den Sie soeben erstellt haben (z. B. CBLB). Klicken Sie auf **Einstellungen**.   
      2. Klicken Sie auf **Tests > Hinzufügen**.   
      3. Geben Sie einen Namen für den Test ein (z. B. **RDP**), wählen Sie **TCP** als **Protokoll** aus, geben Sie **3389** für den **Port** ein, und klicken Sie dann auf **OK**.   
3. Erstellen Sie den Back-End-Pool des Verbindungsbrokers:   
      1. Klicken Sie unter **Einstellungen** auf **Back-End-Adresspools > Hinzufügen**.   
      2. Geben Sie einen Namen ein (z. B. CBBackendPool), und klicken Sie dann auf **Virtuellen Computer hinzufügen**.  
      3. Wählen Sie eine Verfügbarkeitsgruppe (z. B. CbAvSet) aus, und klicken Sie dann auf **OK**.   
      3. Klicken Sie auf **Virtuelle Computer auswählen**, wählen Sie die einzelnen virtuellen Computer aus, und klicken Sie dann auf **Auswählen > OK > OK**.   
4. Erstellen Sie die RDP-Lastenausgleichsregel:   
      1. Klicken Sie unter **Einstellungen** auf **Lastenausgleichsregeln**, und klicken Sie dann auf **Hinzufügen**.   
      2. Geben Sie einen Namen ein (z. B. RDP), wählen Sie **TCP** als **Protokoll** aus, geben Sie **3389** für den **Port** und **Back-End-Port** ein, und klicken Sie dann auf **OK**.   
5. Fügen Sie einen DNS-Eintrag für den Lastenausgleich hinzu:   
      1. Stellen Sie eine Verbindung mit dem virtuellen Computer des RDMS-Servers her (z. B. Contoso-CB1). Informationen zu den Schritten zum Herstellen der Verbindung mit dem virtuellen Computer finden Sie unter [Vorbereiten des virtuellen Computers des RD-Verbindungsbrokers](./rds-prepare-vms.md).   
      2. Klicken Sie im Server-Manager auf **Extras > DNS**.   
      3. Erweitern Sie im linken Bereich **DNS**, klicken Sie auf den DNS-Computer, klicken Sie auf **Forward-Lookupzonen**, und klicken Sie dann auf Ihren Domänennamen (z. B. Contoso.com). (Es kann einige Sekunden dauern, bis die Abfrage an den DNS-Server für die Informationen bearbeitet wurde.)  
      4. Klicken Sie auf **Aktion > Neuer Host (A oder AAAA)** .   
      9. Geben Sie den Namen (z. B. hacb) und die zuvor angegebene IP-Adresse (z. B. 10.0.0.32) ein.   

### <a name="configure-dns-round-robin"></a>Konfigurieren von DNS-Round-Robin  
  
Die folgenden Schritte sind eine Alternative zur Erstellung eines internen Azure Load Balancers.   
  
1. Stellen Sie eine Verbindung mit dem RDMS-Server im Azure-Portal her. Mit dem Remotedesktopverbindungs-Client   
2. Erstellen von DNS-Einträgen:   
      1. Klicken Sie im Server-Manager auf **Extras > DNS**.   
      2. Erweitern Sie im linken Bereich **DNS**, klicken Sie auf den DNS-Computer, klicken Sie auf **Forward-Lookupzonen**, und klicken Sie dann auf Ihren Domänennamen (z. B. Contoso.com). (Es kann einige Sekunden dauern, bis die Abfrage an den DNS-Server für die Informationen bearbeitet wurde.)  
      3. Klicken Sie auf **Aktion** und **Neuer Host (A oder AAAA)** .   
      4. Geben Sie den **DNS-Namen** für den RD-Verbindungsbrokercluster (z. B. hacb) und dann die **IP-Adresse** des ersten RD-Verbindungsbrokers ein.   
      5. Wiederholen Sie die Schritte 3-4 für jeden weiteren RD Verbindungsbroker, und geben Sie jede eindeutige IP-Adresse für jeden zusätzlichen Eintrag an.


Wenn z. B. die IP-Adressen für die beiden virtuellen Computer des RD-Verbindungsbrokers 10.0.0.8 und 10.0.0.9 sind, würden Sie zwei DNS-Hosteinträge erstellen:
 - Hostname: hacb.contoso.com, IP-Adresse: 10.0.0.8
 - Hostname: hacb.contoso.com, IP-Adresse: 10.0.0.9

## <a name="step-3-configure-the-connection-brokers-for-high-availability"></a>Schritt 3: Konfigurieren des Verbindungsbrokers für Hochverfügbarkeit

1. Fügen Sie den neuen RD-Verbindungsbrokerserver zum Server-Manager hinzu:
   1. Klicken Sie im Server-Manager auf **Verwalten > Server hinzufügen**.
   2. Klicken Sie auf **Jetzt suchen**.
   3. Klicken Sie auf den neu erstellten RD-Verbindungsbrokerserver (z. B. Contoso-Cb2) und dann auf **OK**.
2. Konfigurieren Sie die Hochverfügbarkeit für den RD-Verbindungsbroker:
   1. Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht**.
   2. Klicken Sie mit der rechten Maustaste auf **RD-Verbindungsbroker**, und klicken Sie dann auf **Hochverfügbarkeit konfigurieren**.
   3. Navigieren Sie durch den Assistenten, bis Sie zum Abschnitt „Konfigurationstyp“ gelangen. Wählen Sie **Freigegebener Datenbankserver** aus, und klicken Sie dann auf **Weiter**.
   4. Geben Sie den DNS-Namen für den RD-Verbindungsbrokercluster ein.
   5. Geben Sie die Verbindungszeichenfolge für die SQL-Datenbank ein, und navigieren Sie dann durch den Assistenten, um die Hochverfügbarkeit einzurichten.
3. Hinzufügen des neuen RD-Verbindungsbrokers zur Bereitstellung
   1. Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht**.
   2. Klicken Sie mit der rechten Maustaste auf den RD-Verbindungsbroker, und klicken Sie dann auf **RD-Verbindungsbrokerserver hinzufügen**.
   3. Navigieren Sie durch den Assistenten, bis Sie zur Serverauswahl gelangen, und wählen Sie dann den neu erstellten RD-Verbindungsbrokerserver (z. B. Contoso-CB2) aus.
   4. Schließen Sie den Assistenten ab, und übernehmen Sie die Standardwerte.
4. Konfigurieren Sie vertrauenswürdige Zertifikate auf Servern und Clients des RD-Verbindungsbrokers.
