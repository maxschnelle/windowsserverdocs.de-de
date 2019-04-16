---
title: Konfigurieren Sie und verwalten Sie des Quorums in einem Failovercluster
description: Ausführliche Informationen zum Verwalten des Clusterquorums in einem Windows Server-Failovercluster.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 21f99362205e0a6aa90ebd26cef8f3a779bdc1dc
ms.sourcegitcommit: 28dc7c7f1e44fee7ab2112228af329a9ce0e02ba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2019
ms.locfileid: "9023996"
---
# Konfigurieren und Verwalten des Quorums

>Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema enthält Hintergrundinformationen und Schritte zum Konfigurieren und Verwalten des Quorums in einem Windows Server-Failovercluster.

## Grundlegendes zu quorum

Das Quorum für einen Cluster wird durch die Anzahl der Abstimmungsschaltflächen Elemente bestimmt, die Teil des aktiven Cluster-Mitgliedschaft für diesen Cluster ordnungsgemäß gestartet oder ausgeführt werden muss. Eine ausführlichere Erklärung finden Sie unter der [Cluster und Pool Quorum Doc verstehen](../storage/storage-spaces/understand-quorum.md).

## Quorumkonfigurationsoptionen

Das Quorummodell in Windows Server ist flexibel. Wenn Sie die Quorumkonfiguration für Ihren Cluster ändern müssen, können Sie den Assistenten zum Konfigurieren des Clusterquorums oder Failover Cluster Windows PowerShell-Cmdlets verwenden. Schritte und Überlegungen zum Konfigurieren des Quorums finden Sie unter [konfigurieren das Clusterquorum](#configure-the-cluster-quorum) später in diesem Thema.

Die folgende Tabelle enthält die drei Quorumkonfigurationsoptionen, die in den Assistenten zum Konfigurieren des Clusterquorums verfügbar sind.

<table>
<thead>
<tr class="header">
<th>Option</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Verwenden Sie die Standardeinstellungen</td>
<td>Der Cluster weist automatisch eine Stimme zu jedem Knoten und dynamisch verwaltet die Knoten stimmen. Wenn sie eignet sich für den Cluster und freigegebenen Speicher verfügbar ist, wählt des Clusters einen Datenträger Zeugen. Diese Option wird in den meisten Fällen empfohlen, da die Clustersoftware wählt automatisch eine Quorum und Zeugen Konfiguration enthält, die die höchste Verfügbarkeit für den Cluster.</td>
</tr>
<tr class="even">
<td>Hinzufügen oder Ändern der quorumzeugen</td>
<td>Sie können hinzufügen, ändern oder Entfernen einer Zeugenressource. Sie können einen Datei Freigabe oder Datenträger-Zeugen konfigurieren. Der Cluster weist automatisch eine Stimme zu jedem Knoten und dynamisch verwaltet die Knoten stimmen.</td>
</tr>
<tr class="odd">
<td>Erweiterte Quorumkonfiguration und Zeugen Auswahl</td>
<td>Sie sollten diese Option nur, wenn Sie für die Konfiguration des Quorums anwendungsspezifische oder standortspezifische benötigen. Sie können die quorumzeugen ändern, hinzufügen oder entfernen Knoten wurde, und wählen Sie, ob der Cluster dynamisch Knoten stimmen verwaltet. Standardmäßig wurde auf alle Knoten zugewiesen sind, und die Knoten stimmen dynamisch verwaltet werden.</td>
</tr>
</tbody>
</table>

Je nach der Konfiguration Quorumoption, die Sie auswählen und bestimmten Einstellungen, wird der Cluster in einem der folgenden Quorummodi konfiguriert werden:

<table>
<thead>
<tr class="header">
<th>Modus</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Knotenmehrheit (keine Zeugen)</td>
<td>Nur Knoten haben wurde. Es ist keine quorumzeugen konfiguriert. Das Clusterquorum ist die Mehrzahl der Abstimmungsschaltflächen Knoten in der aktiven Cluster-Mitgliedschaft.</td>
</tr>
<tr class="even">
<td>Knotenmehrheit mit Zeugen (oder Freigabe)</td>
<td>Knoten haben wurde. Darüber hinaus hat ein Clusterquorums hören. Das Clusterquorum ist die Mehrzahl der Abstimmungsschaltflächen Knoten in der aktiven Cluster-Mitgliedschaft sowie Zeugen hören.<br />
<br />
Ein Clusterquorums kann es sich um einen Zeugen festgelegten Datenträger oder eine festgelegte dateifreigabezeugen sein.</td>
</tr>
<tr class="odd">
<td>Keine Mehrheit (nur Datenträger Zeugen)</td>
<td>Keine Knoten haben wurde. Nur ein Datenträger-Zeuge verfügt über eine Stimme. Das Clusterquorum wird durch den Status des Datenträgers Zeugen bestimmt.<br />
<br />
Cluster hat Quorum, wenn ein Knoten verfügbar und Kommunikation mit einem bestimmten Datenträger im Cluster ist. In der Regel in diesem Modus wird nicht empfohlen, und es sollte nicht ausgewählt werden, da es sich um eine zentrale Anlaufstelle für Fehler für den Cluster erstellt.</td>
</tr>
</tbody>
</table>

In den folgenden Unterabschnitten erhalten Sie weitere Informationen zu erweiterten Quorum-Konfigurationseinstellungen.

### Zeugenkonfiguration

Bei der Konfiguration der ein Quorum werden im Allgemeinen sollten die Abstimmungsschaltflächen Elemente im Cluster eine ungerade Anzahl. Aus diesem Grund Cluster eine gerade Zahl von Knoten Abstimmung enthält, sollten Sie einen Datenträger Zeugen oder einen dateifreigabezeugen konfigurieren. Cluster ist ein zusätzlichen Knoten nach unten weiterhin möglich. Darüber hinaus kann die Abstimmung Zeugen Hinzufügen des Clusters weiter ausgeführt werden, wenn die Hälfte die Clusterknoten gleichzeitig abstürzt oder getrennt werden.

Ein Datenträger-Zeuge wird empfohlen, wenn alle Knoten den Datenträger angezeigt wird. Eine dateifreigabezeugen wird empfohlen, wenn Sie für mehrere Standorte Wiederherstellung mit replizierten Speichers zu berücksichtigen müssen. Konfigurieren einen Datenträger Zeugen mit replizierten Speichers ist nur möglich, wenn der Speicheranbieter Lese-/ Schreibzugriff von allen Websites zu replizierten Speichers unterstützt. <strong>*Ein Datenträger-Zeuge wird nicht unterstützt, mit "direkte Speicherplätze"*</strong>.

Die folgende Tabelle enthält weitere Informationen und Hinweise zu den Quorum Zeugen.

<table>
<thead>
<tr class="header">
<th>Zeugen-Typ</th>
<th>Beschreibung</th>
<th>Anforderungen und Empfehlungen</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Datenträger-Zeugen</td>
<td>- Dedizierte LUNs, in dem eine Kopie der Clusterdatenbank gespeichert.<br />
- Besonders nützlich für Cluster mit freigegebenem (nicht replizierten) Speicher</td>
<td>- Größe des LUNs muss mindestens 512 MB sein.<br />
- Für die Verwendung im Cluster zu nicht zu einer gruppierten Rolle zugewiesen werden muss<br />
- Muss in gruppierten Speicher und übergeben Sie Speicher Validierungstests enthalten sein<br />
- Ein Datenträger nicht möglich, die einem Cluster Shared Volumes (CSV)<br />
- Basisdatenträger mit einem einzigen volume<br />
- Muss nicht unbedingt einen Laufwerkbuchstaben haben.<br />
- Kann mit NTFS oder ReFS formatiert werden<br />
- Kann optional mit Hardware-RAID für Fehlertoleranz konfiguriert werden<br />
- Sollte von Sicherungen und Antivirusscans ausgeschlossen werden<br />
- Ein Datenträger-Zeuge wird mit "direkte Speicherplätze" nicht unterstützt.</td>
</tr>
<tr class="even">
<td>Dateifreigabezeugen</td>
<td>- SMB-Dateifreigabe, die auf einem Dateiserver unter Windows Server konfiguriert ist<br />
- Eine Kopie der Clusterdatenbank werden nicht gespeichert werden.<br />
- Verwaltet die Clusterinformationen nur in einer Datei witness.log<br />
- Besonders nützlich für die für mehrere Standorte Cluster mit replizierten Speichers</td>
<td>- Benötigen Sie mindestens 5 MB Speicherplatz frei<br />
- Für die einzelnen Cluster zu nicht verwendet, um den Benutzer oder die Anwendung Daten gespeichert werden muss<br />
- Schreibberechtigungen müssen für das Computerobjekt für den Namen des Clusters aktiviert haben<br />
<br />
Im folgenden finden Sie weitere Überlegungen zu einem Dateiserver, der die dateifreigabezeugen hostet:<br />
<br />
- Ein einzelner Dateiserver kann mit Datei Freigabe Zeugen für mehrere Cluster konfiguriert werden.<br />
- Der Dateiserver muss auf eine Website, die unabhängig von der Workload Cluster ist. Dadurch können gleiche Chancen für alle Cluster-Website, um noch vorhanden sind, wenn der Standort-zu-Standort Netzwerkkommunikation nicht mehr auffindbar ist. Wenn der Dateiserver auf der gleichen Website ist, die Website wird des primären Standorts, und es ist die einzige Website, die die Dateifreigabe zugreifen kann.<br />
- Der Dateiserver kann auf einem virtuellen Computer ausführen, wenn der virtuelle Computer nicht im gleichen Cluster gehostet wird, die die dateifreigabezeugen verwendet.<br />
- Für hohe Verfügbarkeit kann der Dateiserver auf einem separaten Failovercluster konfiguriert werden.</td>
</tr>

<tr class-"odd">
<td>Cloudzeuge</td>
<td>- Eine Zeugen-Datei, die in Azure Blob-Speicher gespeichert<br>
-Empfohlen, alle Server im Cluster eine zuverlässige Verbindung mit dem Internet haben.</td>
<td>Finden Sie unter <a href="https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness">Bereitstellen eines cloudzeugen</a>.</td>
<td>
</td>
</tr>

</tbody>
</table>

### Knoten Abstimmung Zuordnung

Erweiterte Quorum Konfiguration Möglichkeit können Sie zuweisen oder Entfernen von Quorum stimmen auf pro Knoten. Standardmäßig werden alle Knoten wurde zugewiesen. Unabhängig von der Stimme Zuweisung alle Knoten weiterhin funktionieren im Cluster, Cluster-Datenbankupdates erhalten, und Anwendungen hosten können.

Möglicherweise möchten stimmen von Knoten in bestimmten Notfall Recovery-Konfigurationen zu entfernen. Beispielsweise können in einem Cluster mit mehreren Standorten Sie stimmen von Knoten in einer Sicherung Website entfernen, damit diese Knoten quorumberechnung nicht beeinträchtigen. Diese Konfiguration wird nur für manuelles Failover zwischen Standorten empfohlen. Weitere Informationen finden Sie [Quorum für Notfall Recovery-Konfigurationen](#quorum-considerations-for-disaster-recovery-configurations) später in diesem Thema.

Die konfigurierte Abstimmung eines Knotens kann durch die allgemeine **NodeWeight** -Eigenschaft der Clusterknoten mithilfe der Windows PowerShell-Cmdlet [Get-ClusterNode](http://technet.microsoft.com/library/hh847268.aspx)Nachschlagen überprüft werden. Ein Wert von 0 gibt an, dass der Knoten nicht Quorum Abstimmung konfiguriert ist. Der Wert 1 gibt an, dass die Abstimmung Quorum des Knotens zugewiesen ist, und es wird vom Cluster verwaltet. Weitere Informationen zur Verwaltung von Knoten stimmen finden Sie weiter unten in diesem Thema [dynamische Quorum Management](#dynamic-quorum-management) .

Die Zuordnung des stimmen Sie für alle Clusterknoten kann mithilfe der Überprüfung **Clusterquorum überprüfen** überprüft werden.

#### Weitere Überlegungen für Knoten Abstimmung Zuordnung

  - Knoten Abstimmung Zuordnung wird nicht empfohlen, um eine ungerade Anzahl von Abstimmungsschaltflächen Knoten zu erzwingen. Stattdessen sollten Sie einen Datenträger Zeugen oder dateifreigabezeugen konfigurieren. Weitere Informationen finden Sie weiter unten in diesem Thema [zeugenkonfiguration](#witness-configuration) .
  - Wenn dynamische Quorum Management aktiviert ist, können nur die Knoten, die konfiguriert sind, um Knoten stimmen zugewiesen haben ihre Stimme zugewiesen oder dynamisch entfernt haben. Weitere Informationen finden Sie weiter unten in diesem Thema [dynamische Quorum Management](#dynamic-quorum-management) .

### Dynamische Quorum management

In Windows Server 2012 können als eine erweiterte Konfiguration Quorumoption, Sie zum Aktivieren der dynamischen Quorum Verwaltung durch Cluster. Weitere Details dazu, wie dynamische Quorum funktioniert finden Sie in [Diese Erklärung](../storage/storage-spaces/understand-quorum.md#dynamic-quorum-behavior).

Dynamische Quorum Management ist es auch möglich, dass ein Cluster auf dem letzten verbleibenden Clusterknoten ausgeführt. Durch dynamisch anpassen Anforderung an die meisten Quorum, kann der Cluster sequenzielle Knoten Herunterfahren des Systems auf einen einzelnen Knoten tolerieren.

Die Cluster-zugewiesen dynamische Abstimmung eines Knotens kann mit der allgemeinen **DynamicWeight** -Eigenschaft des Clusterknotens mithilfe der Windows PowerShell-Cmdlet [Get-ClusterNode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode?view=win10-ps) überprüft werden. Ein Wert von 0 gibt an, dass der Knoten nicht Abstimmung Quorum verfügt. Der Wert 1 gibt an, dass der Knoten Abstimmung Quorum verfügt.

Die Zuordnung des stimmen Sie für alle Clusterknoten kann mithilfe der Überprüfung **Clusterquorum überprüfen** überprüft werden.

#### Weitere Überlegungen für die dynamische Quorum-Verwaltung

- Dynamische Quorum Management lässt sich nicht auf den Cluster das gleichzeitigen Ausfall eines Mehrheit Abstimmungsschaltflächen Mitglieder weiterhin aus. Um weiter ausgeführt muss der Cluster immer Mehrheit Quorum zum Zeitpunkt der Knoten Herunterfahren oder Fehler verfügen.

- Wenn Sie die Abstimmung eines Knotens explizit entfernt haben, nicht dynamisch Cluster hinzufügen oder entfernen diese Stimme.
- Wenn "direkte Speicherplätze" aktiviert ist, kann der Cluster nur zwei Knotenfehler unterstützen. Dies ist mehr im [Pool Quorum Abschnitt](../storage/storage-spaces/understand-quorum.md#poolQuorum) erläutert.

## Allgemeine Empfehlungen für die Quorumkonfiguration

Die Clustersoftware konfiguriert automatisch das Quorum für einen neuen Cluster, basierend auf der Anzahl der Knoten konfiguriert und die Verfügbarkeit von freigegebenem Speicher. Dies ist in der Regel am besten geeigneten Quorumkonfiguration für diesen Cluster. Allerdings ist es sinnvoll, die Quorumkonfiguration überprüfen Sie nach der Erstellung des Clusters vor dem Cluster in der Produktion platzieren. Um die detaillierte Cluster Quorumkonfiguration anzuzeigen, können Sie Sie verwenden überprüfen Konfigurationsassistenten oder des [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) Windows PowerShell-Cmdlets zum Ausführen des Tests **Quorumkonfiguration überprüfen** . Im Failovercluster-Manager, die grundlegende Quorumkonfiguration wird angezeigt, in der zusammenfassende Informationen für den ausgewählten Cluster oder Sie können prüfen, die Informationen über Quorumressourcen, die zurückgibt, wenn Sie die [Get-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusterquorum?view=win10-ps) Windows PowerShell ausführen Cmdlet.

Zu einem beliebigen Zeitpunkt können Sie dem Test **Quorumkonfiguration überprüfen** , um zu überprüfen ausführen, dass die Quorumkonfiguration für den Cluster optimal ist. Die Test-Ausgabe gibt an, ob eine Änderung der Quorumkonfiguration wird empfohlen, und die Einstellungen, die eine optimale sind. Wenn eine Änderung empfohlen wird, können Sie den Assistenten zum Konfigurieren des Clusterquorums verwenden, um die empfohlenen Einstellungen anzuwenden.

Nachdem der Cluster in der Produktion wird, ändern Sie es sei denn, Sie festgestellt haben, dass die Änderung für den Cluster geeignet ist nicht Quorumkonfiguration. Möglicherweise möchten überlegen, ob die Quorumkonfiguration in folgenden Fällen:

- Hinzufügen oder Entfernen von Knoten
- Hinzufügen oder Entfernen von Speicher
- Ein Long-term Knoten oder Zeugen-Fehler
- Wiederherstellen von einem Cluster in einem Szenario zur Wiederherstellung für mehrere Standorte nach

Weitere Informationen dazu Überprüfen eines Failoverclusters finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

## Konfigurieren Sie das Clusterquorum

Sie können die Cluster-Quorum-Einstellungen konfigurieren, mithilfe des Failovercluster-Manager oder Failover Cluster Windows PowerShell-Cmdlets.

>[!IMPORTANT]
>Es empfiehlt sich in der Regel die Quorumkonfiguration zu verwenden, die durch den Assistenten zum Konfigurieren des Clusterquorums empfohlen wird. Es wird empfohlen, die Quorumkonfiguration anpassen, nur dann, wenn Sie festgestellt haben, dass die Änderung für den Cluster geeignet ist. Weitere Informationen finden Sie in diesem Thema [Allgemeine Empfehlungen für die Quorumkonfiguration](#general-recommendations-for-quorum-configuration) .

### Konfigurieren Sie die Cluster-Quorum-Einstellungen

Mitgliedschaft in der lokalen Gruppe **Administratoren** auf jedem Cluster-Server oder entspricht, ist die minimalen Berechtigungen zum Ausführen dieser Schritte erforderlich sind. Darüber hinaus muss das Konto, mit denen Sie ein Domänenbenutzerkonto sein.

>[!NOTE]
>Sie können die Cluster-Quorumkonfiguration ändern, ohne eine Unterbrechung der Cluster oder Notizen Clusterressourcen offline.

### Ändern Sie die Quorumkonfiguration in einem Failovercluster mithilfe des Failovercluster-Manager

1. Wählen Sie im Failovercluster-Manager, oder geben Sie den Cluster, den Sie ändern möchten.
2. Klicken Sie mit dem Cluster ausgewählt haben, klicken Sie unter **Aktionen** **Mehr**Aktionen Sie, und wählen Sie dann **Aktionsbereich**. Der Assistenten zum Konfigurieren des Clusterquorums wird angezeigt. Wählen Sie **Weiter** aus.
3. Klicken Sie auf der Seite **Quorum Configuration Option auswählen** wählen Sie eine der drei Konfigurationsoptionen, und führen Sie die Schritte für diese Option. Bevor Sie die Quorum-Einstellungen konfigurieren, können Sie Ihre Auswahl überprüfen. Weitere Informationen zu den Optionen finden Sie in der [Übersicht über des Quorums in einem Failovercluster](#overview-of-the-quorum-in-a-failover-cluster), weiter oben in diesem Thema.

    - Damit können den Cluster automatisch zurückgesetzt, die Quorum-Einstellungen, die für die aktuelle Clusterkonfiguration optimal sind, wählen Sie **typische verwenden** , und schließen Sie den Assistenten ab.
    - Klicken Sie zum Hinzufügen oder ändern die quorumzeugen, wählen Sie **Hinzufügen oder Ändern der quorumzeugen**, und führen Sie die folgenden Schritte. Weitere Informationen und Hinweise zum Konfigurieren eines Clusterquorums finden Sie unter [zeugenkonfiguration](#witness-configuration) weiter oben in diesem Thema.

      1. Wählen Sie auf der Seite **Quorumzeugen wählen Sie** eine Option, um einen Datenträger Zeugen oder einen dateifreigabezeugen zu konfigurieren. Der Assistent gibt an, Zeugen Auswahloptionen, die für den Cluster empfohlen werden.

          >[!NOTE]
          >Sie können auch auswählen **ein Clusterquorums nicht konfigurieren** , und schließen Sie den Assistenten ab. Wenn Sie eine gerade Zahl von Knoten im Cluster abstimmen haben, kann dies nicht empfohlene Konfiguration sein.

      2. Wenn Sie die Option so konfigurieren Sie einen Zeugen Datenträger auf der Seite **Konfigurieren Speicher Zeugen** wählen Sie das Speichervolume, das Sie als Zeugen Datenträger zuweisen möchten, und führen Sie den Assistenten.
      3. Wenn Sie die Option so konfigurieren Sie einen dateifreigabezeugen auf der Seite **Dateifreigabe-konfigurieren** oder navigieren Sie eine Dateifreigabe, die als Zeugenressource verwendet werden, und schließen Sie den Assistenten ab.

    - Um Quorum Management-Einstellungen zu konfigurieren und hinzufügen oder ändern die quorumzeugen, wählen Sie **Erweiterte Quorumkonfiguration und Zeugen Auswahl**, und führen Sie die folgenden Schritte. Informationen und Hinweise Einstellungen für die erweiterte Quorum-Konfiguration finden Sie unter [Knoten Zuweisung abstimmen](#node-vote-assignment) und [dynamische Quorum Management](#dynamic-quorum-management) weiter oben in diesem Thema.

      1. Wählen Sie eine Option zum Knoten stimmen zuweisen, auf der Seite **Abstimmung Konfiguration auswählen** . Standardmäßig werden alle Knoten Abstimmung zugewiesen. Allerdings können für bestimmte Szenarien, Sie stimmen nur eine Teilmenge der Knoten zuweisen.

          >[!NOTE]
          >Sie können auch **Keine Knoten**auswählen. Dies ist im Allgemeinen nicht empfohlen, da ermöglicht keine Knoten zur Teilnahme Quorum Abstimmung und erfordert einen Datenträger Zeugen konfigurieren. Diese Datenträger Zeugen wird der einzelnen Fehlerpunkt für den Cluster.

      2. Auf der Seite **Quorum Management konfigurieren** können Sie aktivieren oder deaktivieren die Option **stimmen zulassen Cluster-zu-dynamisch die Zuweisung von Knoten zu verwalten** . Im Allgemeinen ist diese Option erhöht die Verfügbarkeit des Clusters. Die Option ist standardmäßig aktiviert, und es wird dringend empfohlen, diese Option nicht zu deaktivieren. Diese Option ermöglicht dem Cluster weiterhin ausgeführt, die in Szenarien, die nicht möglich sind, wenn diese Option deaktiviert ist.
      3. Wählen Sie auf der Seite **Quorumzeugen wählen Sie** eine Option, um einen Datenträger Zeugen oder einen dateifreigabezeugen zu konfigurieren. Der Assistent gibt an, Zeugen Auswahloptionen, die für den Cluster empfohlen werden.

          >[!NOTE]
          >Sie können auch auswählen **ein Clusterquorums nicht konfigurieren**, und schließen Sie den Assistenten ab. Wenn Sie eine gerade Zahl von Knoten im Cluster abstimmen haben, kann dies nicht empfohlene Konfiguration sein.

      4. Wenn Sie die Option so konfigurieren Sie einen Zeugen Datenträger auf der Seite **Konfigurieren Speicher Zeugen** wählen Sie das Speichervolume, das Sie als Zeugen Datenträger zuweisen möchten, und führen Sie den Assistenten.
      5. Wenn Sie die Option so konfigurieren Sie einen dateifreigabezeugen auf der Seite **Dateifreigabe-konfigurieren** oder navigieren Sie eine Dateifreigabe, die als Zeugenressource verwendet werden, und schließen Sie den Assistenten ab.

4. Wählen Sie **Weiter** aus. Bestätigen Sie Ihre Auswahl auf der Seite "Bestätigung", die angezeigt wird, und wählen Sie dann **Weiter**.

Nachdem der Assistent ausgeführt wird, und der Seite " **Zusammenfassung** " angezeigt wird, wenn Sie einen Bericht über die Aufgaben anzeigen, die vom Assistenten ausgeführten möchten, wählen Sie **Bericht anzeigen**. Der letzte Bericht bleibt in der *Systemroot *** \\Cluster\\Reports** Ordner mit dem Namen **QuorumConfiguration.mht**.

>[!NOTE]
>Nachdem Sie das Clusterquorum konfiguriert haben, empfehlen wir, dass Sie den Test **Quorumkonfiguration überprüfen** , um zu überprüfen, die aktualisierte Quorum-Einstellungen ausführen.

### Entsprechende Windows PowerShell-Befehle

Die folgenden Beispiele zeigen, wie Sie das Cmdlet " [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum?view=win10-ps) " und andere Windows PowerShell-Cmdlets verwenden, um das Clusterquorum konfigurieren.

Im folgenden Beispiel wird die Quorumkonfiguration auf Cluster *CONTOSO FC1* zu einer einfachen Knoten Mehrheit-Konfiguration mit keine quorumzeugen.

```PowerShell
Set-ClusterQuorum –Cluster CONTOSO-FC1 -NodeMajority
```

Im folgenden Beispiel wird die Quorumkonfiguration auf dem lokalen Cluster auf der Mehrzahl der Knoten mit zeugenkonfiguration. Die Ressource mit dem Namen ' *Cluster Disk 2* ist als Zeugen Datenträger konfiguriert.

```PowerShell
Set-ClusterQuorum -NodeAndDiskMajority "Cluster Disk 2"
```

Im folgenden Beispiel wird die Quorumkonfiguration auf dem lokalen Cluster auf der Mehrzahl der Knoten mit zeugenkonfiguration. Die Dateifreigabe-Ressource mit dem Namen *\\\CONTOSO-FS\\fsw* ist als ein dateifreigabezeugen konfiguriert.

```PowerShell
Set-ClusterQuorum -NodeAndFileShareMajority "\\fileserver\fsw"
```

Im folgende Beispiel wird die Abstimmung Quorum vom Knoten *ContosoFCNode1* auf dem lokalen Cluster entfernt.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=0
```

Im folgende Beispiel hinzugefügt Knoten *ContosoFCNode1* auf dem lokalen Cluster die Quorum Abstimmung.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=1
```

Im folgende Beispiel ermöglicht die **DynamicQuorum** -Eigenschaft des Clusters *CONTOSO FC1* (Wenn sie zuvor deaktiviert wurde):

```PowerShell
(Get-Cluster CONTOSO-FC1).DynamicQuorum=1
```

## Wiederherstellen eines Clusters ohne Quorum starten

Ein Cluster, der nicht über genügend stimmen Quorum verfügt, wird nicht gestartet. Als ersten Schritt sollten Sie die Cluster-Quorumkonfiguration bestätigen und untersuchen, warum der Cluster nicht mehr Quorum verfügt. Dies kann passieren, wenn Sie Knoten verfügen, die nicht mehr reagiert oder des primären Standorts nicht in einem Cluster für mehrere Standorte erreichbar ist. Nachdem Sie die Ursache des Fehlers Cluster identifiziert haben, können Sie die in diesem Abschnitt beschriebenen Schritte zur Wiederherstellung.

>[!NOTE]
> * Wenn der Cluster-Dienst wird beendet, da Quorum nicht mehr auffindbar ist, wird die Ereignis-ID 1177 im Systemprotokoll angezeigt.
> * Es ist immer erforderlich, um festzustellen, warum das Clusterquorum verloren gegangen sind.
> * Es wird immer empfohlen, einen Zeugen Knoten oder Quorums in einem fehlerfreien Zustand (Verknüpfen des Clusters) und nicht des Clusters ohne Quorum anzuzeigen.

### Force starten Clusterknoten

Nachdem Sie feststellen, dass den Cluster durch das Hinzufügen von Knoten oder quorumzeugen in einem fehlerfreien Zustand behoben werden kann, wird die erzwingen die Cluster-zu-start erforderlich. Erzwingen die Cluster-zu starten, überschreibt Cluster-Einstellungen für die Konfiguration der Quorum und beginnt mit den Cluster **ForceQuorum** -Modus.

Erzwingen von einem Cluster zu starten, wenn es kein Quorum vorhanden ist möglicherweise in einem Cluster für mehrere Standorte besonders nützlich. Sollten Sie ein Szenario zur Wiederherstellung nach mit einem Cluster, der separat sich primären und backup-Websites, *Standort* und *Standort b*enthält. Wenn Katastrophenfall Originalversion am *Standort*vorhanden ist, kann es sehr viel Zeit für die Website wieder online geschaltet dauern. Sie möchten wahrscheinlich erzwingen *Standort b* online geschaltet werden, obwohl es kein Quorum vorhanden ist.

Wenn ein Cluster in **ForceQuorum** -Modus gestartet wird, nachdem es wieder ist ausreichend Quorum stimmen, Cluster verlässt automatisch die erzwungene Zustand und es verhält sich normal. Daher ist es nicht erforderlich, um dem Cluster erneut normal gestartet. Wenn Cluster eines Knotens verliert, und es Quorum verliert, wird es offline geschaltet erneut, da es sich nicht mehr im erzwungenen Zustand ist. Um es wieder online geschaltet, wenn sie keinen Quorum hat erfordert erzwingen den Cluster das Quorum, startet.

>[!IMPORTANT]
>* Nach ein Cluster erzwingen, die gestartet wird, wird der Administrator vollständige Kontrolle über den Cluster.
>* Der Cluster die Cluster-Konfiguration auf dem Knoten verwendet, in dem Cluster erzwingen, die gestartet wird, und wird auf allen Knoten, die verfügbar sind repliziert.
>* Wenn Sie die Cluster-zu-ohne Quorum gestartet werden, werden alle Einstellungen für die Konfiguration von Quorum ignoriert, während des Clusters im **ForceQuorum** Modus bleibt. Dazu gehören bestimmte Knoten stimmen Sie Aufgaben und Einstellungen für die dynamische Quorum Management.

### Verhindern, dass Quorums auf den verbleibenden Knoten

Nachdem Sie haben Schritte Force Cluster auf einem Knoten ist es erforderlich, alle verbleibenden Knoten im Cluster mit einer Einstellung, um zu verhindern, dass Quorum zu starten. Gibt an, ein Knoten Schritte mit einer Einstellung, die das Quorum verhindert den Cluster-Dienst auf einem bestehenden ausgeführten Cluster anstelle von bilden eine neue Clusterinstanz beitreten. Dadurch wird verhindert, dass die verbleibenden Knoten bilden einen geteilten Cluster mit zwei konkurrierenden Instanzen.

Dies notwendig ist die Sicherung Website, *Standort b*Cluster Schritte müssen Sie Ihre Cluster in einigen für mehrere Standorte Notfallwiederherstellungsszenarien wiederherstellen, nachdem Sie Force haben. So verknüpfen Sie die Kraft Cluster *Standort b*, Knoten im primären Standort, *Standort*zu machen, müssen mit das Quorum verhindert gestartet werden.

>[!IMPORTANT]
>Nach ein Cluster erzwingen, die auf einem Knoten gestartet wird, wird empfohlen, dass Sie immer die verbleibenden Knoten mit des Quorums verhindert, dass gestartet.

Dies sind die der Cluster mit Failovercluster-Manager wiederhergestellt werden:

1. Wählen Sie im Failovercluster-Manager, oder geben Sie den Cluster, die, den Sie wiederherstellen möchten.
2. Wählen Sie mit dem Cluster ausgewählt haben, klicken Sie unter **Aktionen** **Force Cluster starten**.

    Failovercluster-Manager-Force beginnt die Cluster auf allen Knoten, die erreichbar sind. Der Cluster verwendet die aktuelle Clusterkonfiguration beim Starten.

>[!NOTE]
>* Damit wird die Cluster-zu-starten Sie auf einem bestimmten Knoten mit einer Cluster-Konfiguration, die Sie verwenden möchten, müssen Sie die Windows PowerShell-Cmdlets oder den Befehlszeilentools verwenden, wie nach diesem Verfahren dargestellt. 
> * Wenn Sie Failovercluster-Manager verwenden, um zu einem Cluster herzustellen, Force gestartet ist, und Sie die **Cluster-Dienst starten** Aktion zum Starten eines Knotens, der Knoten automatisch mit der Einstellung gestartet wird, die das Quorum verhindert.

#### Entsprechende Windows PowerShell-Befehle (Start-Clusternode)

Im folgenden Beispiel wird veranschaulicht, wie auf die **Start-ClusterNode** -Cmdlet verwenden, um Erzwingen der Startseite Cluster auf den Knoten *ContosoFCNode1*.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –FQ
```

Alternativ können Sie den folgenden Befehl lokal auf dem Knoten eingeben:

```PowerShell
Net Start ClusSvc /FQ
```

Das folgende Beispiel zeigt, wie Sie die **Start-ClusterNode** -Cmdlet verwenden, um mit der Quorum verhindert, dass auf den Knoten *ContosoFCNode1*starten.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –PQ
```

Alternativ können Sie den folgenden Befehl lokal auf dem Knoten eingeben:

```PowerShell
Net Start ClusSvc /PQ
```

## Quorum Überlegungen für Notfall Recovery-Konfigurationen

Dieser Abschnitt enthält die Merkmale und Quorumkonfigurationen für zwei für mehrere Standorte Clusterkonfigurationen im Notfall Recovery Bereitstellungen. Die Quorum Konfigurationsrichtlinien unterscheiden sich je nach, wenn Sie automatische Failover oder manuelles Failover für Workloads zwischen den Websites benötigen. In der Regel hängt die Konfiguration der Service Level Agreements (Agreement, SLA), die in Ihrer Organisation bereitstellen und unterstützen gruppierte Arbeitslasten bei einem Ausfall des Notfall an einem Standort vorhanden sind.

### Automatische failover

Bei dieser Konfiguration besteht aus der Cluster zwei oder mehr Sites, die clusterrollen hosten können. Bei einem an jedem beliebigen Standort Fehler, erscheinen die clusterrollen automatisch die verbleibenden Standorte Failover zu. Aus diesem Grund muss das Clusterquorum konfiguriert werden, damit eine Website mit einer vollständigen Ausfall des Standorts verarbeiten kann.

Die folgende Tabelle enthält eine Zusammenfassung Überlegungen und Empfehlungen für diese Konfiguration.

<table>
<thead>
<tr class="header">
<th>Element</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Anzahl von Knoten stimmen pro Standort</td>
<td>Sollte gleich sein</td>
</tr>
<tr class="even">
<td>Knoten Abstimmung Zuordnung</td>
<td>Knoten stimmen sollte nicht entfernt werden, da alle Knoten ebenso wichtig sind.</td>
</tr>
<tr class="odd">
<td>Dynamische Quorum management</td>
<td>Muss aktiviert sein.</td>
</tr>
<tr class="even">
<td>Zeugenkonfiguration</td>
<td>Dateifreigabezeugen wird empfohlen, in einer Website, die aus der Cluster-Websites ist konfiguriert,</td>
</tr>
<tr class="odd">
<td>Workloads</td>
<td>Workloads können auf alle Websites konfiguriert werden</td>
</tr>
</tbody>
</table>

#### Weitere Überlegungen für die automatische failover

- Konfigurieren des dateifreigabezeugen in einer separaten Website ist erforderlich, um jede Website gleich überleben können. Weitere Informationen finden Sie weiter oben in diesem Thema [zeugenkonfiguration](#witness-configuration) .

### Manuelles failover

In dieser Konfiguration umfasst den Cluster einen primären Standort, *Standort*und eine Sicherung (Wiederherstellung)-Website, *Standort b*. Clusterrollen werden auf *Standort*gehostet. Aufgrund der Clusterkonfiguration Quorum tritt ein Fehler auf allen Knoten im *Standort*, funktioniert der Cluster. In diesem Szenario muss der Administrator manuell ein Failover Cluster-Dienste auf *Standort b* und zusätzliche Schritte zum Wiederherstellen des Clusters ausführen.

Die folgende Tabelle enthält eine Zusammenfassung Überlegungen und Empfehlungen für diese Konfiguration.

<table>
<thead>
<tr class="header">
<th>Element</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Anzahl von Knoten stimmen pro Standort</td>
<td>Kann unterschiedlich sein</td>
</tr>
<tr class="even">
<td>Knoten Abstimmung Zuordnung</td>
<td>- Knoten stimmen sollte nicht entfernt werden, von Knoten am primären Standort, <em>Standort</em><br />
- Knoten stimmen sollte von Knoten am Standort backup entfernt werden <em>Standort b</em><br />
- Ein Long-term Ausfall erfolgt am <em>Standort</em>, stimmen Knoten am zugewiesen werden müssen <em>Standort b</em> Quorum Mehrzahl an diesem Standort im Rahmen der Wiederherstellung aktivieren</td>
</tr>
<tr class="odd">
<td>Dynamische Quorum management</td>
<td>Muss aktiviert sein.</td>
</tr>
<tr class="even">
<td>Zeugenkonfiguration</td>
<td>- Konfigurieren Sie einen Zeugen liegt eine gerade Zahl von Knoten am <em>Standort</em><br />
- Wenn ein Zeuge erforderlich ist, konfigurieren Sie einen dateifreigabezeugen oder einen Datenträger Zeugen, die nur auf Knoten in zugegriffen werden kann <em>Standort</em> (auch als eine asymmetrische Datenträger Zeugen bezeichnet)</td>
</tr>
<tr class="odd">
<td>Workloads</td>
<td>Verwenden Sie weiterhin Arbeitslasten auf Knoten am bevorzugten Besitzer <em>Standort</em></td>
</tr>
</tbody>
</table>

#### Weitere Überlegungen für manuelles failover

- Nur die Knoten am *Standort* werden anfänglich mit Quorum stimmen konfiguriert. Dies ist erforderlich, um sicherzustellen, dass der Zustand der Knoten am *Standort b* nicht das Clusterquorum auswirkt.
- Schritte zur Wiederherstellung können je nach variieren, wenn *Standort* ein temporärer Fehler oder Long-term Fehler Sicherstellung.

## Weitere Informationen

* [Failoverclusterunterstützung](failover-clustering.md)
* [Failover Cluster Windows PowerShell-cmdlets](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)
* [Grundlegendes zu-Cluster und Pool Quorum](../storage/storage-spaces/understand-quorum.md)