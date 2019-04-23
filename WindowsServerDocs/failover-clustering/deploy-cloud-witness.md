---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: Bereitstellen eines cloudzeugen für einen Failovercluster
ms.prod: windows-server-threshold
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 01/18/2019
description: 'Gewusst wie: Verwenden Sie Microsoft Azure zum Hosten der Zeuge für eine Windows Server Failover Cluster in der Cloud - auch zum Bereitstellen eines Cloudzeugen.'
ms.openlocfilehash: f7e1c84e54f08044a772f06e591588c1add33026
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857981"
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>Bereitstellen eines Cloudzeugen für einen Failovercluster

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Cloudzeuge ist ein Typ von failoverclusterquorum-Zeuge, die Microsoft Azure verwendet wird, um eine Abstimmung auf Quorum eines dateiserverclusters bereitzustellen. Dieses Thema enthält eine Übersicht über die Cloudzeugen-Funktion, die Szenarien, die es unterstützt und Anweisungen zum Konfigurieren eines cloudzeugen für einen Failovercluster.

## <a name="CloudWitnessOverview"></a>Übersicht über die Cloud-Zeugen

Abbildung 1 zeigt eine mit mehreren Standorte stretching Failover Quorumkonfiguration mit Windows Server 2016. In diesem Beispiel (Abbildung 1) gibt es 2 Knoten in 2 Datencentern (Standorten genannt). Beachten Sie, dass es für einen Cluster aus, um mehr als 2 Rechenzentren möglich ist. Darüber hinaus kann jedes Rechenzentrum der Einsatz mehr als 2 Knoten enthalten. Eine typische Quorumkonfiguration in diesem Setup (Automatisches Failover, SLA) bietet jedem Knoten eine Stimme. Eine zusätzliche Stimme an den quorumzeugen übergeben wird, um Cluster ausgeführt wird, auch wenn eine der im Datencenter zu ermöglichen Erfahrungen ein Stromausfalls. Die mathematischen Grundlagen von ist einfach – es 5 insgesamt stimmen und erfordern 3 stimmen für den Cluster für den Betrieb aufrechtzuerhalten.  

![Dateifreigabezeugen in einem dritten separaten Standorten mit 2 Knoten 2 andere](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "Dateifreigabenzeuge")  
**Abbildung 1: Verwenden einen Dateifreigabenzeugen als ein quorumzeuge**  

Bei einem Stromausfall in einem Rechenzentrum gespeichert um die gleiche Möglichkeit für den Cluster in andere Datencenter zu ausgeführt wird, geben empfiehlt es um den quorumzeugen in einen anderen Speicherort als den beiden Rechenzentren zu hosten. Dadurch trennen Sie die in der Regel erfordert eine dritte Möglichkeit Datencenter (Standort) zum Hosten von einem Dateiserver, in dem die Dateifreigabe zugrunde liegt, die als den quorumzeugen (File Share Witness) verwendet wird.  

Die meisten Organisationen verfügen nicht über die eine dritte Datacenter zu trennen, die Dateiserver sichern den Dateifreigabenzeugen hostet. Dies bedeutet, dass Organisationen Hosten in erster Linie den Dateiserver in einem der zwei Rechenzentren, wodurch durch Erweiterung dieses Rechenzentrums im primäre Datencenter. In einem Szenario, Stromausfall im primären Datencenter vorhanden ist, den Cluster fiel aus wie das andere Rechenzentrum nur 2 stimmen die unter die quorummehrheit von 3 stimmen, die erforderlich ist. Für Kunden, die dritte ein separates Datencenter, auf dem Dateiserver gehostet haben, ist es ein Overhead für die hoch verfügbaren Dateiserver sichern den Dateifreigabenzeugen verwalten. Hosten von virtuellen Computern in der öffentlichen Cloud, die den Dateiserver für Dateifreigabenzeugen in Gast-BS ausgeführt haben, wird eines erheblichen Mehraufwands beim sowohl Setup und Wartung.  

Cloudzeuge ist ein neuer Typ von failoverclusterquorum-Zeuge, die Microsoft Azure als Vermittlungspunkt (Abbildung 2) nutzt. Er verwendet Azure Blob Storage, um eine Blobdatei Schreib-/die dann als ein Vermittlungspunkt bei Split-Brain-Auflösung verwendet wird.  

Es gibt bedeutende Vorteile der dieser Ansatz:
1. Nutzt Microsoft Azure (es muss für den dritten separaten Rechenzentrum).  
2. Verwendet standard verfügbaren Azure Blob Storage (keine zusätzlichen Wartungsaufwand für virtuelle Computer in der öffentlichen Cloud gehostet).  
3. Gleiche Azure Storage-Konto kann für mehrere Cluster (einen Blob-Datei pro Cluster, Cluster eindeutige Id als Blob-Dateiname) verwendet werden.  
4. Sehr niedrig laufenden $cost in das Speicherkonto (sehr kleine Daten geschrieben pro Blob-Datei, BLOB-Datei aktualisiert wird, nur einmal Wenn Clusterknoten Zustand ändert).  
5. Integrierte Cloudzeugen Ressourcentyp.  

![Diagramm zur Veranschaulichung eines gestreckten Multisite-Clusters mit Cloudzeugen als quorumzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**Abbildung 2: Stretched Cluster mit mehreren Standorten mit Cloudzeugen als quorumzeugen**  

Wie in Abbildung 2 gezeigt, besteht keine dritten separaten Standort, der erforderlich ist. Cloudzeuge erhält wie jeder andere quorumzeuge ein Votum und quorumberechnung teilnehmen kann.  

## <a name="CloudWitnessSupportedScenarios"></a>Cloudzeuge: Unterstützte Szenarien für die einzelnen zeugentyp
Wenn Sie eine Bereitstellung Failovercluster verfügen, in dem alle Knoten im Internet (durch Erweiterung von Azure) erreichen, wird empfohlen, dass Sie einen Cloudzeugen als Ihr Quorum Zeugenressource konfigurieren.  

Einige der Szenarien, die unterstützt werden verwenden Cloudzeugen als quorumzeugen lauten wie folgt:  
- Wiederherstellung im Notfall gestreckt Multisite-Cluster (siehe Abbildung 2).  
- Failovercluster ohne freigegebenen Speicher (SQL immer auf usw.).  
- Failover-Cluster ausgeführt, die innerhalb des Gastbetriebssystems, die in Microsoft Azure-VM-Rolle (oder jeder anderen öffentlichen Cloud) gehostet wird.  
- Failovercluster, die Ausführung im Betriebssystem des virtuellen Gastcomputern, die in privaten Clouds gehostet werden.
- Speicher-Cluster mit oder ohne freigegebenen Speicher, z. B. Dateiservercluster mit horizontaler.  
- Kleine Zweigstellen-Clustern (auch 2-Knoten-Cluster)  

Ab Windows Server 2012 R2, wird es empfohlen, immer einen Zeugen zu konfigurieren, wie der Cluster automatisch die zeugenstimme verwaltet und stimmen die Knoten mit dynamisches Quorum.  

## <a name="CloudWitnessSetUp"></a> Richten Sie einen Cloudzeugen für einen cluster
Um einen Cloudzeugen als quorumzeugen für Ihren Cluster einzurichten, führen Sie die folgenden Schritte aus:
1. Erstellen Sie ein Azure Storage-Konto als einen Cloudzeugen verwenden
2. Konfigurieren Sie den Cloudzeugen als quorumzeugen für Ihren Cluster ein.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>Erstellen Sie ein Azure Storage-Konto als einen Cloudzeugen verwenden

Dieser Abschnitt beschreibt das Erstellen von eines Storage-Konto "und" Ansicht "und" Kopie-Endpunkts-URLs und Zugriffsschlüssel für dieses Konto.

Um Cloudzeugen zu konfigurieren, benötigen Sie ein gültiges Azure Storage-Konto die verwendet werden kann, um die Blob-Datei (verwendet für die Vermittlung) zu speichern. Cloudzeuge erstellt einen bekannten Container **Msft-cloudzeugen** in der Microsoft Storage-Konto. Cloud Witness Schreibvorgänge eine einzelne Blob-Datei mit den entsprechenden cluster, die eindeutige ID wie der Dateiname der BLOB-Datei unter diesem **Msft-cloudzeugen** Container. Dies bedeutet, dass Sie die gleiche Microsoft Azure Storage-Konto verwenden können, so konfigurieren Sie einen Cloudzeugen für mehrere unterschiedliche Cluster.

Wenn Sie das gleiche Azure Storage-Konto verwenden, für die Konfiguration von Cloud-Zeuge für mehrere verschiedene-Cluster eine einzelne **Msft-cloudzeugen** Container wird automatisch erstellt. Dieser Container enthält eine-Blob-Datei pro Cluster.

### <a name="to-create-an-azure-storage-account"></a>Azure Storage-Konto erstellen

1. Melden Sie sich bei der [Azure-Portal](http://portal.azure.com).
2. Klicken Sie im Menü "Hub" Option Neu -> Daten + Speicher-Storage-Konto >.
3. Die Seite eine Storage-Konto erstellen führen Sie folgende Schritte aus:
    1. Geben Sie einen Namen für Ihr Speicherkonto aus.
    <br>Speicherkontonamen müssen zwischen 3 und 24 Zeichen lang sein und darf nur Zahlen und Kleinbuchstaben enthalten. Der Name des Speicherkontos muss auch innerhalb von Azure eindeutig sein.
        
    2. Für **Kontoart**Option **allgemeiner**.
    <br>Sie können keine Blob-Speicherkonten für einen Cloudzeugen verwenden.
    3. Für **Leistung**Option **Standard**.
    <br>Sie können keine Azure Storage Premium für einen Cloudzeugen verwenden.
    2. Für **Replikation**Option **lokal redundanter Speicher (LRS)** .
    <br>Failover-Clusterunterstützung wird die Blob-Datei als Vermittlungspunkt, erfordert einige Konsistenzgarantien beim Lesen der Daten verwendet. Deshalb müssen Sie auswählen **lokal redundanter Speicher** für **Replikation** Typ.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>Anzeigen und Kopieren von speicherzugriffsschlüssel für Ihr Azure-Speicherkonto

Wenn Sie ein Microsoft Azure Storage-Konto erstellen, ist es zwei Zugriffsschlüssel, die automatisch generiert werden – primärer Zugriffsschlüssel und sekundären Zugriffsschlüssel zugeordnet. Verwenden Sie für die Erstellung eines ersten Cloud Zeugen, dem **primärer Zugriffsschlüssel**. Es gibt keine Einschränkung in Bezug auf die Schlüssel für Cloudzeugen.  

#### <a name="to-view-and-copy-storage-access-keys"></a>Zum Anzeigen und Kopieren von speicherzugriffsschlüsseln

Navigieren Sie im Azure-Portal zu Ihrem Speicherkonto, klicken Sie auf **alle Einstellungen** , und klicken Sie dann auf **Zugriffsschlüssel** zum Anzeigen, kopieren und den Zugriffsschlüssel für Ihr Konto. Das Blatt "Zugriffsschlüssel" enthält auch vorkonfigurierte Verbindungszeichenfolgen, die mit Ihrem primären und sekundären Schlüssel, die Sie kopieren können Verwendung in Ihren Anwendungen (siehe Abbildung 4).

![Überblick über das Dialogfeld "Zugriffsschlüssel verwalten" in Microsoft Azure](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**Abbildung 4: Speicherzugriffsschlüssel**

### <a name="view-and-copy-endpoint-url-links"></a>Zeigen Sie an und kopieren Sie die Endpunkt-URL-Links  
Wenn Sie ein Speicherkonto erstellen, werden die folgenden URLs im Format generiert: `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

Cloudzeuge verwendet immer **Blob** als Speichertyp. Azure verwendet **. core.windows.net** als Endpunkt. Wenn Sie Cloudzeugen zu konfigurieren, ist es möglich, dass Sie ihn mit einem anderen Endpunkt gemäß Ihrem Szenario konfigurieren (Microsoft Azure-Datencenter in China hat z. B. einen anderen Endpunkt).  

> [!NOTE]  
> Die Endpunkt-URL von Cloudzeugen Ressource wird automatisch generiert und ist kein zusätzlicher Schritt der Konfiguration für die URL erforderlich.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>Zum Anzeigen und kopieren die Endpunkt-URL-links
Navigieren Sie im Azure-Portal zu Ihrem Speicherkonto, klicken Sie auf **alle Einstellungen** , und klicken Sie dann auf **Eigenschaften** anzeigen und kopieren die Endpunkt-URLs (siehe Abbildung 5).  

![Momentaufnahme der Cloudzeugen Endpunkt links](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**Abbildung 5: Cloud-Zeuge Endpunkt-URL-links**

Weitere Informationen zum Erstellen und Verwalten von Azure Storage-Konten finden Sie unter [Informationen zu Azure-Speicherkonten](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>Konfigurieren von Cloudzeugen als quorumzeugen für Ihren cluster
Cloud-zeugenkonfiguration ist gut integrierten in den vorhandenen Quorum-Konfigurations-Assistenten in der Failovercluster-Manager erstellt.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>Um Cloudzeugen als Quorumzeugen konfigurieren
1. Failovercluster-Manager zu starten.
2. Mit der rechten Maustaste, der der Cluster -> **Weitere Aktionen** -> **Clusterquorumeinstellungen konfigurieren** (siehe Abbildung 6). Dadurch wird der Konfigurieren von Cluster-Quorum-Assistent gestartet.  
    ![Momentaufnahme des Pfades Menü Clusterquorumeinstellungen konfigurieren, in der Failovercluster-Manager-UI](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png) **Abbildung 6. Cluster-Quorum-Einstellungen**

3. Auf der **Quorumkonfigurationen wählen** Seite **quorumzeugen auswählen** (siehe Abbildung 7).  

    ![Momentaufnahme "Auswählen der Zeuge Quotrum" Optionsfeld in der Cluster-Quorum-Assistent](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **Abbildung 7. Wählen Sie die Quorumkonfiguration**

4. Auf der **Quorumzeuge auswählen** Seite **konfigurieren ein cloudzeugen** (siehe Abbildung 8).  

    ![Überblick über das entsprechende Optionsfeld, wählen Sie einen cloudzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **Abbildung 8. Quorumzeugen auswählen**  

5. Auf der **Cloudzeugen konfigurieren** geben die folgende Informationen:  
    1. (Erforderliche Parameter) Azure-Speicherkontos ein.  
    2. (Erforderliche Parameter) Der Zugriffsschlüssel für das Speicherkonto an.  
        1. Wenn Sie zum ersten Mal erstellen, verwenden Sie die Primary Access Key (siehe Abbildung 5)  
        2. Verwenden Sie beim Rotieren von den primären Zugriffsschlüssel sekundären Zugriffsschlüssel (siehe Abbildung 5)  
    3. (Optionaler Parameter) Wenn Sie einen anderen Azure-Dienst-Endpunkt (z. B. die Microsoft Azure-Dienst in China) verwenden möchten, aktualisieren Sie dann den Servernamen für den Endpunkt.  

    ![Überblick über Cloudzeuge Konfigurationsbereich in der Cluster-Quorum-Assistent](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
    **Abbildung 9: Konfigurieren Sie Ihre Cloudzeugen**

6. Nach einer erfolgreichen Konfiguration des Cloudzeugen, sehen Sie die neu erstellte Zeugenressource im Failovercluster-Manager-Snap-in (siehe Abbildung 10).

    ![Bei der Konfiguration des Cloudzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png)  
    **Abbildung 10: Bei der Konfiguration des Cloudzeugen**

### <a name="configuring-cloud-witness-using-powershell"></a>Konfigurieren von Cloudzeugen mithilfe von PowerShell  
Der vorhandene Set-ClusterQuorum-PowerShell-Befehl verfügt über neue zusätzliche Parameter für Cloudzeugen.  

Sie können konfigurieren, Cloudzeugen mithilfe der [ `Set-ClusterQuorum` ](https://technet.microsoft.com/library/ee461013.aspx) den folgenden PowerShell-Befehl:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

Im Fall müssen Sie einen anderen Endpunkt (selten vorkommenden) zu verwenden:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>Überlegungen zum von Azure Storage-Konto mit Cloudzeugen  
Wenn Sie einen Cloudzeugen als quorumzeugen für Ihren Failovercluster konfigurieren möchten, beachten Sie Folgendes ein:
* Anstatt zu speichern, den Zugriffsschlüssel, den Failovercluster generiert und eine Shared Access-Sicherheit (SAS) Tokens sicher zu speichern.  
* Das generierte SAS-Token ist gültig, solange die Zugriffstaste gültig bleibt. Wenn Sie den primären Zugriffsschlüssel zu drehen, ist es wichtig, zuerst mit den sekundären Zugriffsschlüssel des Cloudzeugen (in allen Ihren Clustern, die dieses Speicherkonto verwenden) aktualisieren, vor dem erneuten Generieren des primären Zugriffsschlüssels.  
* Cloudzeuge verwendet HTTPS-REST-Schnittstelle des Diensts Azure Storage-Konto. Dies bedeutet, dass den HTTPS-Port auf allen Clusterknoten geöffnet sein muss.

### <a name="proxy-considerations-with-cloud-witness"></a>Proxy-Überlegungen zu Cloudzeugen  
Cloudzeuge verwendet HTTPS (standardmäßig Port 443), um die Kommunikation mit Azure Blob-Dienst herstellen. Stellen Sie sicher, dass HTTPS-Port über das Netzwerk Proxy möglich ist.

## <a name="see-also"></a>Siehe auch
- [Neues beim Failoverclustering in WindowsServer](whats-new-in-failover-clustering.md)
