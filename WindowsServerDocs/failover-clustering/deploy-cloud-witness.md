---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: Bereitstellen eines cloudzeugen für einen Failovercluster
ms.prod: windows-server
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 01/18/2019
description: In diesem Abschnitt wird erläutert, wie Sie den Zeugen für einen Windows Server-Failovercluster in der Cloud hosten und wie Sie einen cloudzeugen bereitstellen. Microsoft Azure
ms.openlocfilehash: 1f38a1a436cfced8637b743817dc1b3d150f7fa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369880"
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>Bereitstellen eines Cloudzeugen für einen Failovercluster

> Gilt für: Windows Server 2019, Windows Server 2016

Der cloudzeuge ist ein Failovercluster-Quorum Zeugen, der Microsoft Azure verwendet, um eine Stimme für das Cluster Quorum bereitzustellen. Dieses Thema enthält eine Übersicht über die Cloud-Zeugen Funktion, die unterstützten Szenarien sowie Anweisungen zum Konfigurieren eines cloudzeugen für einen Failovercluster.

## <a name="CloudWitnessOverview"></a>Cloud-Zeugen Übersicht

Abbildung 1 zeigt eine Konfiguration eines Failoverclusters mit mehreren Standorten mit Windows Server 2016. In dieser Beispielkonfiguration (Abbildung 1) gibt es zwei Knoten in zwei Rechenzentren (als Standorte bezeichnet). Beachten Sie, dass sich ein Cluster über mehr als 2 Rechenzentren erstrecken kann. Außerdem kann jedes Rechenzentrum mehr als zwei Knoten aufweisen. Durch eine typische Cluster Quorum Konfiguration in diesem Setup (automatisches Failover-SLA) erhält jeder Knoten eine Stimme. Der Quorum Zeuge erhält eine zusätzliche Stimme, damit der Cluster weiterhin ausgeführt werden kann, selbst wenn eines der Rechenzentren einen Stromausfall hat. Die Mathematik ist einfach: Es sind insgesamt 5 Stimmen vorhanden, und Sie benötigen 3 Stimmen, damit der Cluster weiterhin ausgeführt wird.  

![Dateifreigabe Zeuge an einem dritten separaten Standort mit 2 Knoten in 2 anderen Standorten](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "Dateifreigabe Zeuge")  
**Abbildung 1: Verwenden eines Dateifreigabe Zeugen als Quorum Zeugen**  

Bei einem Stromausfall in einem Rechenzentrum wird empfohlen, den Quorum Zeugen an einem anderen Speicherort als den beiden Rechenzentren zu hosten, um dem Cluster in einem anderen Rechenzentrum die gleiche Chance zu geben. Dies bedeutet in der Regel, dass ein drittes separates Daten Center (Standort) zum Hosten eines Dateiservers erforderlich ist, der die Dateifreigabe unterstützt, die als Quorum Zeuge (Dateifreigabe Zeuge) verwendet wird.  

Die meisten Organisationen verfügen über kein drittes separates Daten Center, das den Datei Server hostet, der den Dateifreigabe Zeugen unterstützt. Dies bedeutet, dass Unternehmen in erster Linie den Datei Server in einem der beiden Rechenzentren hosten, die durch Erweiterung dieses Rechenzentrum zum primären Daten Center machen. In einem Szenario, in dem ein Stromausfall im primären Daten Center auftritt, würde der Cluster ausfallen, da das andere Daten Center nur 2 Stimmen aufweisen würde, was unter dem Quorum der Mehrheit von 3 Stimmen liegt. Für Kunden, die über ein drittes separates Daten Center verfügen, um den Dateiserver zu hosten, ist es ein zusätzlicher Aufwand, den hoch verfügbaren Dateiserver zu verwalten, der den Datei frei gaben Zeugen unterstützt. Das Hosting von virtuellen Computern in den Public Cloud, auf denen der Datei Server für den Dateifreigabe Zeugen im Gast Betriebssystem ausgeführt wird, ist ein erheblicher Aufwand in Bezug auf die Einrichtung & Wartung.  

Der cloudzeuge ist ein neuer Failovercluster-Quorum Zeugen, der Microsoft Azure als Schiedsrichter Punkt nutzt (Abbildung 2). Es verwendet Azure BLOB Storage, um eine BLOB-Datei zu lesen und zu schreiben, die dann als Schlichtungs Punkt bei der Auflösung von Split Brain verwendet wird.  

Diese Vorgehensweise hat bedeutende Vorteile:
1. Nutzt Microsoft Azure (kein drittes separates Rechenzentrum erforderlich).  
2. Verwendet standardmäßig verfügbare Azure BLOB Storage (kein zusätzlicher Wartungsaufwand für in Public Cloud gehostete virtuelle Maschinen).  
3. Dasselbe Azure Storage Konto kann für mehrere Cluster verwendet werden (eine BLOB-Datei pro Cluster; eindeutige Cluster-ID, die als BLOB-Dateiname verwendet wird).  
4. Sehr niedriger $cost zum Speicherkonto (sehr kleine Daten, die pro BLOB-Datei geschrieben werden, BLOB-Dateien werden nur einmal aktualisiert, wenn sich der Status der Cluster Knoten ändert).  
5. Integrierter cloudzeugen-Ressourcentyp.  

![Diagramm, das einen gestreckten Cluster mit mehreren Standorten mit dem cloudzeugen als Quorum Zeugen veranschaulicht](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**Abbildung 2: Stretch-Cluster mit mehreren Standorten mit dem cloudzeugen als Quorum Zeugen**  

Wie in Abbildung 2 dargestellt, gibt es keine dritte separate Site, die erforderlich ist. Der cloudzeuge erhält, wie jeder andere Quorum Zeuge, eine Stimme und kann an Quorum Berechnungen teilnehmen.  

## <a name="CloudWitnessSupportedScenarios"></a>Cloudzeuge: unterstützte Szenarien für einen einzelnen Zeugen Typen
Wenn Sie über eine failoverclusterbereitstellung verfügen, bei der alle Knoten das Internet erreichen können (durch Erweiterung von Azure), empfiehlt es sich, einen cloudzeugen als Quorum Zeugen Ressource zu konfigurieren.  

Folgende Szenarien werden von einem cloudzeugen als Quorum Zeuge unterstützt:  
- Die Notfall Wiederherstellung streckten Cluster mit mehreren Standorten (siehe Abbildung 2).  
- Failovercluster ohne freigegebenen Speicher (SQL Always on usw.).  
- Failovercluster, die in einem Gast Betriebssystem ausgeführt werden, das in Microsoft Azure Rolle für virtuelle Computer (oder anderen Public Cloud) gehostet wird  
- Failovercluster, die innerhalb des Gast Betriebssystems von Virtual Machines in privaten Clouds gehostet werden.
- Speicher Cluster mit oder ohne freigegebenen Speicher, z. b. Datei Server Cluster mit horizontaler Skalierung.  
- Kleine Zweigstellen Cluster (auch Cluster mit zwei Knoten)  

Ab Windows Server 2012 R2 empfiehlt es sich, immer einen Zeugen zu konfigurieren, da der Cluster die Zeugen Stimme automatisch verwaltet und die Knoten mit dynamischem Quorum Stimmen.  

## <a name="CloudWitnessSetUp"></a>Einrichten eines cloudzeugen für einen Cluster
Führen Sie die folgenden Schritte aus, um einen cloudzeugen als Quorum Zeugen für Ihren Cluster einzurichten:
1. Erstellen Sie ein Azure Storage Konto, das als cloudzeuge verwendet werden soll.
2. Konfigurieren Sie den cloudzeugen als Quorum Zeugen für Ihren Cluster.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>Erstellen Sie ein Azure Storage Konto, das als cloudzeuge verwendet werden soll.

In diesem Abschnitt wird beschrieben, wie Sie ein Speicherkonto erstellen und Endpunkt-URLs und Zugriffsschlüssel für dieses Konto anzeigen und kopieren.

Zum Konfigurieren des cloudzeugen müssen Sie über ein gültiges Azure Storage Konto verfügen, das zum Speichern der BLOB-Datei verwendet werden kann. Der cloudzeuge erstellt einen bekannten Container **MSFT-Cloud-Witness** unter dem Microsoft-Speicherkonto. Der cloudzeuge schreibt eine einzelne BLOB-Datei mit der entsprechenden eindeutigen Cluster-ID, die als Dateiname der BLOB-Datei in diesem **MSFT-Cloud-Witness-** Container verwendet wird. Dies bedeutet, dass Sie das gleiche Microsoft Azure Storage Konto verwenden können, um einen cloudzeugen für mehrere verschiedene Cluster zu konfigurieren.

Wenn Sie das gleiche Azure Storage Konto für die Konfiguration eines cloudzeugen für mehrere verschiedene Cluster verwenden, wird automatisch ein einzelner **MSFT-Cloud-Witness-** Container erstellt. Dieser Container enthält eine BLOB-Datei pro Cluster.

### <a name="to-create-an-azure-storage-account"></a>So erstellen Sie ein Azure-Speicherkonto

1. Melden Sie sich beim [Azure-Portal](http://portal.azure.com)an.
2. Wählen Sie im Menü "Hub" die Option Neu > Daten und Speicher > Speicherkonto aus.
3. Gehen Sie auf der Seite Speicherkonto erstellen folgendermaßen vor:
    1. Geben Sie einen Namen für Ihr Speicherkonto ein.
    <br>Speicherkonto Namen müssen zwischen 3 und 24 Zeichen lang sein und dürfen nur Ziffern und Kleinbuchstaben enthalten. Der Name des Speicher Kontos muss auch innerhalb von Azure eindeutig sein.
        
    2. Wählen Sie unter **Kontoart**die Option **Allgemein**aus.
    <br>Sie können kein BLOB Storage-Konto für einen cloudzeugen verwenden.
    3. Wählen Sie für **Leistung**die Option **Standard**aus.
    <br>Azure Storage Premium kann nicht für einen cloudzeugen verwendet werden.
    2. Wählen Sie unter **Replikation**die Option **lokal redundanter Speicher (LRS)** aus.
    <br>Failoverclustering verwendet die BLOB-Datei als Schiedsrichter Punkt. Dies erfordert einige Konsistenz Garantien beim Lesen der Daten. Daher müssen Sie für den **Replikationstyp** den **lokal redundanten Speicher** auswählen.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>Anzeigen und Kopieren von Speicherzugriffs Schlüsseln für Ihr Azure Storage Konto

Wenn Sie ein Microsoft Azure Storage Konto erstellen, ist es zwei Zugriffs Schlüsseln zugeordnet, die automatisch generiert werden: primärer Zugriffsschlüssel und sekundärer Zugriffsschlüssel. Verwenden Sie für die erstmalige Erstellung eines cloudzeugen den **primären Zugriffsschlüssel**. Es gibt keine Einschränkung hinsichtlich des Schlüssels, der für den cloudzeugen verwendet werden soll.  

#### <a name="to-view-and-copy-storage-access-keys"></a>So können Sie Speicherzugriffs Schlüssel anzeigen und kopieren

Navigieren Sie im Azure-Portal zu Ihrem Speicherkonto, klicken Sie auf **alle Einstellungen** , und klicken Sie dann auf **Zugriffsschlüssel** , um Ihre Konto Zugriffsschlüssel anzuzeigen, zu kopieren und neu zu generieren. Das Blatt Zugriffsschlüssel enthält auch vorkonfigurierte Verbindungs Zeichenfolgen, die ihre primären und sekundären Schlüssel verwenden, die Sie zur Verwendung in Ihren Anwendungen kopieren können (siehe Abbildung 4).

![Momentaufnahme des Dialog Felds Zugriffsschlüssel verwalten in Microsoft Azure](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**Abbildung 4: Speicherzugriffs Schlüssel**

### <a name="view-and-copy-endpoint-url-links"></a>Anzeigen und Kopieren von Endpunkt-URL-Links  
Wenn Sie ein Speicherkonto erstellen, werden die folgenden URLs im folgenden Format generiert: `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

Der cloudzeuge verwendet immer **BLOB** als Speichertyp. Azure verwendet **. Core.Windows.net** als Endpunkt. Wenn Sie einen cloudzeugen konfigurieren, ist es möglich, ihn gemäß Ihrem Szenario mit einem anderen Endpunkt zu konfigurieren (z. b. Microsoft Azure Rechenzentrum in China einen anderen Endpunkt).  

> [!NOTE]  
> Die Endpunkt-URL wird automatisch von der Cloud-Zeugen Ressource generiert, und für die URL ist kein zusätzlicher Konfigurationsschritt erforderlich.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>So können Sie Endpunkt-URL-Links anzeigen und kopieren
Navigieren Sie im Azure-Portal zu Ihrem Speicherkonto, klicken Sie auf **alle Einstellungen** , und klicken Sie dann auf **Eigenschaften** , um Ihre Endpunkt-URLs anzuzeigen und zu kopieren (siehe Abbildung 5).  

![Momentaufnahme der cloudzeugen-Endpunkt Verknüpfungen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**Abbildung 5: Verknüpfungen der Cloud-Zeugen Endpunkt-URL**

Weitere Informationen zum Erstellen und Verwalten von Azure Storage Konten finden Sie unter [Informationen zu Azure Storage Konten](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/) .

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>Konfigurieren des cloudzeugen als Quorum Zeugen für Ihren Cluster
Die cloudzeugen Konfiguration ist innerhalb des vorhandenen Quorum Konfigurationsassistenten, der in die Failovercluster-Manager integriert ist, gut integriert.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>So konfigurieren Sie einen cloudzeugen als Quorum Zeugen
1. Starten Sie Failovercluster-Manager.
2. Klicken Sie mit der rechten Maustaste auf den Cluster, > **Weitere Aktionen** -> **Konfigurieren der Cluster Quorum Einstellungen** (siehe Abbildung 6). Der Assistent zum Konfigurieren des Cluster Quorums wird gestartet.  
    ![Momentaufnahme des Menü Pfads zu den Einstellungen für den Systempfad des-Clusters in der Failovercluster-Manager-Benutzeroberfläche](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png) **Abbildung 6. Cluster Quorum Einstellungen**

3. Wählen Sie auf der Seite **Quorum Konfigurationen auswählen** **die Option Quorum Zeugen auswählen** (siehe Abbildung 7).  

    ![Momentaufnahme des Options Felds "quotrum Witness" im Clusterquorum-Assistenten](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **Abbildung 7: Wählen Sie die Quorum Konfiguration aus.**

4. Wählen Sie auf der Seite **Quorum Zeugen auswählen** die Option **cloudzeuge konfigurieren** (siehe Abbildung 8).  

    ![Momentaufnahme des entsprechenden Options Felds, um einen cloudzeugen auszuwählen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **Abbildung 8. Wählen Sie den Quorum Zeugen aus.**  

5. Geben Sie auf der Seite **Cloud-Zeuge konfigurieren** die folgenden Informationen ein:  
   1. (Erforderlicher Parameter) Azure Storage Kontoname.  
   2. (Erforderlicher Parameter) Zugriffsschlüssel, der dem Speicherkonto entspricht.  
       1. Wenn Sie zum ersten Mal erstellen, verwenden Sie den primären Zugriffsschlüssel (siehe Abbildung 5).  
       2. Wenn Sie den primären Zugriffsschlüssel rotieren, verwenden Sie den sekundären Zugriffsschlüssel (siehe Abbildung 5).  
   3. (Optionaler Parameter) Wenn Sie beabsichtigen, einen anderen Azure-Dienst Endpunkt (z. b. den Microsoft Azure-Dienst in China) zu verwenden, aktualisieren Sie den Endpunkt Servernamen.  

      ![Momentaufnahme des cloudzeugen-Konfigurations Bereichs im Assistenten für Cluster Quorum](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
      **Abbildung 9: Konfigurieren des cloudzeugen**

6. Nach erfolgreicher Konfiguration des cloudzeugen können Sie die neu erstellte Zeugen Ressource im Failovercluster-Manager-Snap-in anzeigen (siehe Abbildung 10).

    ![erfolgreiche Konfiguration des cloudzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png)  
    **Abbildung 10: erfolgreiche Konfiguration des cloudzeugen**

### <a name="configuring-cloud-witness-using-powershell"></a>Konfigurieren eines cloudzeugen mithilfe von PowerShell  
Der vorhandene PowerShell-Befehl "Set-Clusterquorum" verfügt über neue zusätzliche Parameter, die dem cloudzeugen entsprechen.  

Sie können den cloudzeugen mit dem [`Set-ClusterQuorum`](https://technet.microsoft.com/library/ee461013.aspx) folgenden PowerShell-Befehl konfigurieren:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

Für den Fall, dass Sie einen anderen Endpunkt (selten) verwenden müssen:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>Überlegungen zu Azure Storage Konten mit dem cloudzeugen  
Beachten Sie Folgendes, wenn Sie einen cloudzeugen als Quorum Zeugen für Ihren Failovercluster konfigurieren:
* Anstatt den Zugriffsschlüssel zu speichern, generiert und speichert der Failovercluster ein SAS-Token (Shared Access Security).  
* Das generierte SAS-Token ist gültig, solange der Zugriffsschlüssel gültig ist. Wenn Sie den primären Zugriffsschlüssel rotieren, ist es wichtig, zuerst den cloudzeugen (auf allen Clustern, die dieses Speicherkonto verwenden) mit dem sekundären Zugriffsschlüssel zu aktualisieren, bevor Sie den primären Zugriffsschlüssel erneut generieren.  
* Der cloudzeuge verwendet die HTTPS-Rest-Schnittstelle des Azure Storage Konto Diensts. Dies bedeutet, dass der HTTPS-Port auf allen Cluster Knoten geöffnet sein muss.

### <a name="proxy-considerations-with-cloud-witness"></a>Überlegungen zum Proxy mit dem cloudzeugen  
Der cloudzeuge verwendet HTTPS (Standardport 443), um die Kommunikation mit dem Azure-BLOB-Dienst herzustellen. Stellen Sie sicher, dass der HTTPS-Port über den Netzwerk Proxy zugänglich ist

## <a name="see-also"></a>Weitere Informationen
- [Neues beim Failoverclustering unter Windows Server](whats-new-in-failover-clustering.md)
