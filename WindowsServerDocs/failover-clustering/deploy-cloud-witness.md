---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: "Bereitstellen eines cloudzeugen für einen Failovercluster"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 10/2/2017
description: "Wie Sie Microsoft Azure zum Hosten der Zeugendatenträger für einen Windows Server-Failovercluster in der Cloud - aka zum Bereitstellen eines Cloudzeugen."
ms.openlocfilehash: 564c6668fcc80a8bd1531c05c142996689de8154
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>Bereitstellen eines Cloudzeugen für einen Failovercluster

> Gilt für: gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Cloudzeuge ist ein neuer Typ von Failoverclusterquorum-Zeuge, der in Windows Server2016 eingeführt wird. Dieses Thema enthält eine Übersicht über die Cloudzeugen-Funktion, die Szenarien, die sie unterstützt und Anweisungen zur Vorgehensweise beim Konfigurieren eines cloudzeugen für einen Failovercluster, auf denen Windows Server2016 ausgeführt wird.

## <a name="CloudWitnessOverview"></a>Übersicht über die Cloud-Zeugen

Abbildung1 zeigt eine Multisite gestreckte Failover Quorumkonfiguration mit Windows Server2016. In diesem Beispiel (Abbildung1) gibt es 2 Knoten in 2 Rechenzentren (bezeichnet als Standorte). Beachten Sie, dass es für einen Cluster mit mehr als 2 Rechenzentren Bildschirme möglich ist. Darüber hinaus kann jedes Datencenter mehr als 2 Knoten verfügen. Eine typische Quorumkonfiguration in Setup (automatische Failover SLA) bietet jedem Knoten eine Stimme. Eine zusätzliche stimme den quorumzeugen zugewiesen wird, um Cluster ausgeführt wird, auch wenn eine der im Datencenter zu ermöglichen Benutzern einen Stromausfall. Math ist einfach: 5 insgesamt stimmen vorhanden sind, und benötigen Sie 3 stimmen für den Cluster ausführen zu lassen.  

![File Share Witness in einer dritten separaten Standort mit 2 Knoten 2 anderen Standorten](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "File Share Witness")  
**Abbildung1: Verwenden eines Dateifreigabezeugen als quorumzeugen**  

Bei einem Stromausfall in einem Datencenter hier gleich Gelegenheit für den Cluster in anderen Datacenter ausgeführt wird, lassen empfiehlt es sich um den quorumzeugen in einem anderen Speicherort als den beiden Datencentern zu hosten. Dies trennen Sie die in der Regel bedeutet, erfordern eine dritte Datacenter (Standort) zum Hosten von einem Dateiserver, die die Dateifreigabe zusammensetzt, als den quorumzeugen (File Share Witness) verwendet wird.  

Die meisten Organisationen haben keinen dritten Datacenter trennen, das Sichern der File Share Witness Dateiserver gehostet wird. Dies bedeutet, dass Organisationen Hosten in erster Linie den Dateiserver in einem der beiden Datencentern, wodurch durch die Erweiterung Datencenter im primäre Datencenter. In einem Szenario liegt der Stromausfalls im primären Datencenter, der Cluster würde ausfallen als andere Datencenter nur 2 stimmen unter die quorummehrheit von 3 stimmen erforderlich ist. Für die Kunden, die dritte separaten Datencenter zum Hosten der Dateiserver verfügen, ist es ein Aufwand beim Verwalten der hoch verfügbaren Dateiserver Dateifreigabezeugen sichern. Hosten von virtuellen Computern in der öffentlichen Cloud, die den Dateiserver für File Share Witness im Gastbetriebssystem ausgeführt haben, wird einem erheblichen Mehraufwand in Bezug auf die Einrichtung und Wartung.  

Cloudzeuge ist ein neuer Typ von Failoverclusterquorum-Zeuge, der Microsoft Azure als Vermittlungspunkt (Abbildung2) nutzt. Azure BLOB-Speicher verwendet, um ein BLOB-Datei Schreib- oder der dann als ein Vermittlungspunkt bei einem Split-Brain-Lösung verwendet wird.  

Es gibt wichtige Vorteile der dieser Ansatz:
1. Nutzt Microsoft Azure (keine Notwendigkeit für Dritte separate Datacenter).  
2. Verwendet standardmäßige verfügbaren Azure BLOB-Speicher (keine zusätzlichen Verwaltungsaufwand von virtuellen Maschinen, die in öffentlichen Cloud gehostet).  
3. Dieselbe Azure-Speicherkonto kann für mehrere Cluster (ein Blobdatei pro Cluster; Cluster eindeutige ID, die als BLOB--Dateiname) verwendet werden.  
4. Nur noch sehr wenig laufende $cost für das Storage-Konto (sehr kleinen Daten geschrieben pro BLOB-Datei, BLOB-Datei aktualisiert wird, nur einmal Wenn Clusterknoten-Zustand ändert).  
5. Integrierte Cloudzeugen Ressourcentyp.  

![Diagramm zur Veranschaulichung eines gestreckten Multisite-Clusters mit Cloudzeugen als quorumzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**Abbildung2: Gestreckt Multisite-Cluster mit Cloudzeugen als quorumzeugen**  

Wie in Abbildung2 gezeigt, besteht keine Dritter separater Standort, der erforderlich ist. Cloudzeuge, wie jeder andere quorumzeuge eine Stimme ruft und quorumberechnungen beteiligt sein kann.  

## <a name="CloudWitnessSupportedScenarios"></a>Cloudzeuge: Unterstützte Szenarien für die einzelnen quorumzeugen-Typ
Wenn Sie eine Bereitstellung Failovercluster verfügen, in denen alle Knoten im Internet (durch die Erweiterung von Azure) erreichen, wird empfohlen, als Ihre Zeugenressource Quorum eines Cloudzeugen zu konfigurieren.  

Einige Szenarien, die unterstützt werden nutzen Cloudzeugen als quorumzeugen lauten wie folgt:  
- Wiederherstellung gestreckt Multisite-Cluster (siehe Abbildung2).  
- Failovercluster ohne freigegebenen Speicher (SQL immer auf usw.).  
- Failovercluster in Microsoft Azure Virtual Machine-Rolle (oder eine beliebige andere öffentliche Cloud) gehostet Gastbetriebssystem ausgeführt.  
- Failovercluster in Gast OS des gehosteten virtuellen Computer in privaten Clouds ausgeführt.
- Speicher zu einem Cluster mit oder ohne freigegebenen Speicher, wie z.B. das Dateiservercluster mit horizontaler Skalierung.  
- Kleine Zweigstellen-Clustern (auch 2-Knoten-Cluster)  

Ab Windows Server2012 R2, wird empfohlen, einen Zeugen immer zu konfigurieren, wie der Cluster automatisch die zeugenstimme verwaltet und stimmen Sie die Knoten mit dynamische Quorum.  

## <a name="CloudWitnessSetUp"></a>Einrichten eines Cloudzeugen für einen Cluster
Führen Sie zum Einrichten eines Cloudzeugen als quorumzeugen für Ihren Cluster die folgenden Schritteaus:
1. Erstellen Sie ein Azure-Speicherkonto als eines Cloudzeugen verwenden
2. Konfigurieren Sie den Cloudzeugen als quorumzeugen für Ihren Cluster.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>Erstellen Sie ein Azure-Speicherkonto als eines Cloudzeugen verwenden

Dieser Abschnittbeschreibt die Vorgehensweise beim Erstellen einer Speicher und anzeigen und kopieren URLs und Zugriffstasten für dieses Konto.

Um Cloudzeugen zu konfigurieren, müssen Sie ein gültiges Azure Storage-Konto verfügen, die zum Speichern der Blobdatei (für die Vermittlung verwendet) verwendet werden kann. Cloudzeuge erstellt einen bekannten Container **Msft cloudzeugen** unter dem Konto des Microsoft-Speicher. Cloud Witness schreibt eine einzelnes Blob-Datei mit entsprechenden Cluster die eindeutige ID, die als des Dateinamen der BLOB-Datei unter diesem **Msft cloudzeugen** Container. Dies bedeutet, dass Sie das gleiche Microsoft Azure-Speicherkonto zum Konfigurieren eines Cloudzeugen für mehrere unterschiedliche Cluster verwenden können.

Wenn Sie das gleiche Azure Storage-Konto verwenden, für die Konfiguration von Cloudzeugen für mehrere unterschiedliche Cluster eine einzelne **Msft cloudzeugen** Container wird automatisch erstellt. Dieser Container enthält ein Blob-Datei pro Cluster.

### <a name="to-create-an-azure-storage-account"></a>Zum Erstellen eines Azure Storage-Kontos

1. Melden Sie sich an den [Azure-Portal](http://portal.azure.com).
2. Klicken Sie im Menü "Hub" Wählen Sie neue Daten -> + Speicher-Speicherkonto >.
3. Führen Sie folgende Schritteaus, in der Seite eine Speicher-Konto erstellen:
    1. Geben Sie einen Namen für das Speicherkonto.
    <br>Speicher-Kontonamen müssen zwischen 3 und 24 Zeichen lang sein und darf Zahlen und nur Kleinbuchstaben enthalten. Der Kontoname Speicher muss auch in Azure eindeutig sein.
        
    2. Für **Konto Kind**Option **allgemeine**.
    <br>Sie können kein Blob-Speicher-Konto für einen Cloudzeugen verwenden.
    3. Für **Leistung**Option **Standard**.
    <br>Sie können nicht Azure Premium-Speicher für einen Cloudzeugen verwenden.
    2. Für **Replikation**Option **lokal redundante Speicher (LRS)**.
    <br>Failover-Clusterunterstützung verwendet die Blobdatei als Vermittlungspunkt, die einige der Anwendungskonsistenz erforderlich ist, wenn die Daten lesen. Wählen Sie hierfür **lokal redundante Speicher** für **Replikation** geben.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>Anzeigen und Kopieren von Zugriffstasten Speicher für das Azure-Speicherkonto

Wenn Sie ein Microsoft Azure Storage-Konto erstellen, ist es zwei Zugriffstasten, die automatisch generierten - Zugriffstaste primären und sekundären Zugriffstaste zugeordnet. Verwenden Sie für die Erstellung eines ersten von Cloudzeugen, die **primären Zugriffstaste**. Es besteht keine Einschränkung in Bezug auf die Schlüssel für Cloudzeugen.  

#### <a name="to-view-and-copy-storage-access-keys"></a>Anzeigen und kopieren die Zugriffstasten für Speicher

Navigieren Sie im Azure-Portal auf das Speicherkonto, klicken Sie auf **alle Einstellungen**, und klicken Sie dann auf **Zugriffstasten** zum Anzeigen von kopieren und müssen Sie Ihr Konto Zugriffstasten. Der Zugriffstasten Blade enthält auch vorkonfigurierte Verbindungszeichenfolgen, die mit Ihrem primären und sekundären Schlüsseln, die Sie kopieren können die Verwendung in Ihrer Anwendung (siehe Abbildung4).

![Übersicht über das Dialogfeld "verwalten" in Microsoft Azure](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**Abbildung4: Speicher-Zugriffstasten**

### <a name="view-and-copy-endpoint-url-links"></a>Zeigen Sie an und kopieren Sie die Endpunkt-URL-Links  
Wenn Sie ein Speicherkonto erstellen, werden die folgenden URLs im Format generiert: `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

Cloudzeuge verwendet immer **Blob** als Speichertyp. Azure verwendet **. core.windows.net** als Endpunkt. Wenn Sie Cloudzeugen zu konfigurieren, ist es möglich, dass Sie es mit einem anderen Endpunkt gemäß Ihrem Szenario konfigurieren (z.B. Microsoft Azure-Datencenter in China für einen anderen Endpunkt hat).  

> [!NOTE]  
> Die Endpunkt-URL wird von Cloud-Zeugenressource automatisch erstellt, und es ist kein zusätzlicher Schrittder Konfiguration für die URL erforderlich.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>Anzeigen und kopieren die Endpunkt-URL-links
Navigieren Sie im Azure-Portal auf das Speicherkonto, klicken Sie auf **alle Einstellungen**, und klicken Sie dann auf **Eigenschaften** anzeigen und kopieren die Endpunkt-URLs (siehe Abbildung5).  

![Momentaufnahme der Cloudzeugen Endpunkt links](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**Abbildung5: Cloudzeugen Endpunkt-URL-links**

Weitere Informationen zum Erstellen und Verwalten von Azure Storage-Konten finden Sie unter [zu Azure Storage-Konten](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>Konfigurieren von Cloudzeugen als quorumzeugen für Ihren Cluster
Cloud-zeugenkonfiguration ist gut integrierte innerhalb des vorhandenen Quorum-Konfigurations-Assistenten in den Failovercluster-Manager integriert.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>Cloudzeugen als Quorumzeugen konfigurieren
1. Failovercluster-Manager zu starten.
2. Mit der rechten Maustaste die Cluster -> **Weitere Aktionen** -> **Clusterquorumeinstellungen konfigurieren** (siehe Abbildung6). Konfigurieren Sie Cluster-Quorum-Assistent wird gestartet.  
    ![Momentaufnahme des Pfads Menü zur Configue Cluster-Quorum-Einstellungen in der Failovercluster-Manager-UI](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png)**Abbildung6. Cluster-Quorum-Einstellungen**

3. Auf der **Quorumkonfigurationen wählen** Seite **wählen Sie den quorumzeugen** (siehe Abbildung7).  

    ![Momentaufnahme von "select Quotrum Zeugen" Optionsfeld in die Cluster-Quorum-Assistent](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **Abbildung7. Wählen Sie die Quorumkonfiguration**

4. Auf der **Quorumzeugen auswählen** Seite **konfigurieren ein cloudzeugen** (siehe Abbildung8).  

    ![Übersicht über das entsprechende Optionsfeld ein cloudzeugen auswählen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **Abbildung8. Wählen Sie den Quorumzeugen**  

5. Auf der **Cloudzeugen konfigurieren** Seite, geben Sie die folgende Informationen:  
    1. (erforderlicher Parameter) Name des Azure-Speicher.  
    2. (erforderlicher Parameter) Tastenkombination für das Speicherkonto.  
        1. Beim Erstellen von zum ersten Mal primären Zugriffstaste verwenden (siehe Abbildung5)  
        2. Bei der primären Zugriffstaste zu drehen, verwenden Sie sekundäre Zugriffstaste (siehe Abbildung5)  
    3. (optionaler Parameter) Wenn Sie einen anderen Azure-Endpunkt (z.B. die Microsoft Azure-Dienst in China) verwenden möchten, klicken Sie dann aktualisieren Sie den Namen des Servers Endpunkts.  

    ![Übersicht über den Konfigurationsbereich Cloudzeugen in die Cluster-Quorum-Assistent](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
    **Abbildung9: Konfigurieren der Cloudzeugen**

6. Nach der erfolgreichen Konfiguration der Cloudzeugen, sehen Sie die neu erstellte Zeugenressource in den Failovercluster-Manager-Snap-In (siehe Abbildung10).

    ![Bei der Konfiguration des Cloudzeugen](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png)  
    **Abbildung10: Bei der Konfiguration des Cloudzeugen**

### <a name="configuring-cloud-witness-using-powershell"></a>Konfigurieren von Cloudzeugen mithilfe von PowerShell  
Die vorhandene Set-ClusterQuorum-PowerShell-Befehl hat neue zusätzliche Parameter für Cloudzeugen.  

Sie können konfigurieren, Cloudzeugen mithilfe der [`Set-ClusterQuorum`](https://technet.microsoft.com/library/ee461013.aspx)folgenden PowerShell-Befehl:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

Im Fall müssen Sie einen anderen Endpunkt (selten) verwenden:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>Azure Storage-Konto zu Cloudzeugen  
Beim Konfigurieren eines Cloudzeugen als quorumzeugen für den Failovercluster die folgenden Punkte:
* Anstatt die Zugriffstaste, den Failovercluster generiert und ein Token Shared Access-Sicherheit (SAS) sicher zu speichern.  
* Der generierte SAS-Token ist gültig, solange die Zugriffstaste gültig bleibt. Bei der primären Zugriffstaste zu drehen, ist es wichtig, zuerst den Cloudzeugen (in allen den Clustern, die diesem Storage-Konto verwenden) mit der sekundären Zugriffstaste vor dem erneuten Generieren von der primären Zugriffstaste aktualisiert.  
* Cloudzeuge verwendet HTTPS-REST-Schnittstelle des Diensts Azure-Speicherkonto. Dies bedeutet, dass den HTTPS-Port auf allen Clusterknoten geöffnet sein muss.

### <a name="proxy-considerations-with-cloud-witness"></a>Proxy zu Cloudzeugen  
Cloudzeuge verwendet HTTPS (standardmäßig Port 443), um die Kommunikation mit Azure BLOB-Dienst herstellen. Stellen Sie sicher, dass HTTPS-Port über Netzwerk-Proxy möglich ist.

## <a name="see-also"></a>Siehe auch
- [Neues beim Failoverclustering in Windows Server](whats-new-in-failover-clustering.md)
