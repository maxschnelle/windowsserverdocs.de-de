---
title: „Konfigurieren und Verwalten des Quorums in einem Failovercluster“
description: Ausführliche Informationen zum Verwalten des Cluster Quorums in einem Windows Server-Failovercluster.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 67ef309bc2a09c5e241d52c747ab800cfde86168
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720532"
---
# <a name="configure-and-manage-quorum"></a>Konfigurieren und Verwalten des Quorums

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Hintergrundinformationen und Schritte zum Konfigurieren und Verwalten des Quorums in einem Windows Server-Failovercluster.

## <a name="understanding-quorum"></a>Grundlegendes zum Quorum

Das Quorum für einen Cluster wird über die Anzahl der Knoten mit Stimmen bestimmt, die Teil der aktiven Clustermitgliedschaft für diesen Cluster sein müssen, um ordnungsgemäß gestartet oder weiterhin ausgeführt werden zu können. Eine ausführlichere Erläuterung finden Sie im Dokument zum Grundlagen des [Cluster-und Pool Quorums](../storage/storage-spaces/understand-quorum.md).

## <a name="quorum-configuration-options"></a>Optionen für die Quorum Konfiguration

Das Quorum Modell in Windows Server ist flexibel. Wenn Sie die Quorum Konfiguration für Ihren Cluster ändern müssen, können Sie den Assistenten zum Konfigurieren des Cluster Quorums oder die Windows PowerShell-Cmdlets für Failovercluster verwenden. Schritte und Überlegungen zur Quorumkonfiguration finden Sie weiter unten in diesem Thema unter [Konfigurieren des Clusterquorums](#configure-the-cluster-quorum).

In der folgenden Tabelle werden die drei Quorumkonfigurationsoptionen aufgelistet, die im Assistenten zum Konfigurieren des Clusterquorums verfügbar sind.

| Option  |BESCHREIBUNG  |
| --------- | ---------|
| „Typische Einstellungen verwenden“, und     |  Der Cluster weist automatisch jedem Knoten eine Stimme zu und verwaltet die Knotenstimmen dynamisch. Sofern es für Ihren Cluster angemessen ist und freigegebener Clusterspeicher zur Verfügung steht, wählt der Cluster einen Datenträgerzeugen aus. Diese Option wird für die meisten Situationen empfohlen, da die Clustersoftware automatisch eine Quorum- und Zeugenkonfiguration auswählt, die die höchste Verfügbarkeit für den Cluster bietet.       |
| „Quorumzeugen hinzufügen oder ändern“     |   Sie können eine Zeugenressource hinzufügen, ändern oder entfernen. Sie können einen Dateifreigabe- oder Datenträgerzeugen konfigurieren. Der Cluster weist automatisch jedem Knoten eine Stimme zu und verwaltet die Knotenstimmen dynamisch.      |
| „Erweiterte Quorumkonfiguration und Zeugenauswahl“     | Wählen Sie diese Option nur aus, wenn für die Konfiguration des Quorums anwendungs- und standortspezifische Anforderungen gelten. Sie können den Quorumzeugen ändern, Knotenstimmen hinzufügen oder entfernen und auswählen, ob der Cluster die Knotenstimmen dynamisch verwalten soll. Standardmäßig werden zu allen Knoten Stimmen zugewiesen, und die Knotenstimmen werden dynamisch verwaltet.        |

In Abhängigkeit von der gewählten Quorumkonfigurationsoption und Ihren spezifischen Einstellungen wird der Cluster in einem der folgenden Quorummodi konfiguriert:

| Mode  | BESCHREIBUNG  |
| --------- | ---------|
| Knotenmehrheit (kein Zeuge)     |   Nur Knoten haben Stimmen. Es wird kein Quorumzeuge konfiguriert. Das Clusterquorum entspricht der Mehrheit der abstimmenden Knoten in der aktiven Clustermitgliedschaft.      |
| Keine Mehrheit mit Zeuge (Datenträger oder Dateifreigabe)     |   Knoten haben Stimmen. Zusätzlich hat ein Quorumzeuge eine Stimme. Das Clusterquorum entspricht der Mehrheit der abstimmenden Knoten in der aktiven Clustermitgliedschaft plus einer Zeugenstimme. Ein Quorumzeuge kann ein festgelegter Datenträgerzeuge oder ein Dateifreigabezeuge sein. 
| Keine Mehrheit (nur Datenträgerzeuge)     | Knoten haben keine Stimmen. Nur ein Datenträgerzeuge hat eine Stimme. <br>Das Clusterquorum wird über den Status des Datenträgerzeugen bestimmt. Im Allgemeinen wird dieser Modus nicht empfohlen und er sollte nicht ausgewählt werden, da er für den Cluster einen einzelnen Fehlerpunkt erzeugt.       |

In den folgenden Unterabschnitten erhalten Sie weitere Informationen zu erweiterten Quorum Konfigurationseinstellungen.

### <a name="witness-configuration"></a>„Zeugenkonfiguration“

Im Allgemeinen sollten die abstimmenden Elemente im Cluster beim Konfigurieren eines Quorums eine ungerade Anzahl ergeben. Wenn der Cluster daher eine gerade Anzahl von abstimmenden Knoten enthält, sollten Sie einen Datenträgerzeugen oder einen Dateifreigabezeugen konfigurieren. Der Cluster ist in der Lage, einen zusätzlichen Knoten inaktiv zu halten. Zudem kann der Cluster durch das Hinzufügen einer Zeugenstimme die Ausführung fortsetzen, wenn die Hälfte der Clusterknoten gleichzeitig ausfällt oder deren Verbindung unterbrochen bzw. getrennt wird.

Ein Datenträgerzeuge wird in der Regel empfohlen, wenn der Datenträger für alle Knoten angezeigt wird. Ein Dateifreigabezeuge wird empfohlen, wenn Sie die Notfallwiederherstellung mit repliziertem Speicher für mehrere Standorte berücksichtigen müssen. Das Konfigurieren eines Datenträgerzeugen mit repliziertem Speicher ist nur möglich, wenn der Speicheranbieter den Lese-/Schreibzugriff auf den replizierten Speicher von allen Standorten aus unterstützt. <strong>*Ein Datenträger Zeuge wird von direkte Speicherplätze nicht unterstützt*</strong>.

Die folgende Tabelle enthält zusätzliche Informationen und Überlegungen zu den Quorumzeugentypen.

| Zeugentyp  | BESCHREIBUNG  | Anforderungen und Empfehlungen  |
| ---------    |---------        |---------                        |
| Datenträgerzeuge     |  <ul><li> Dedizierte LUN, die eine Kopie der Clusterdatenbank speichert</li><li> Besonders für Cluster mit freigegebenem (nicht repliziertem) Speicher geeignet</li>       |  <ul><li>Die Größe der LUN muss mindestens 512 MB betragen</li><li> Muss für die Clusterverwendung dediziert sein und darf keiner Clusterrolle zugewiesen werden</li><li> Muss in den Clusterspeicher einbezogen werden und die Speichervalidierungstests bestehen</li><li> Darf kein Datenträger sein, der ein freigegebenes Clustervolume (CSV) ist</li><li> Einfacher Datenträger mit einzelnem Volume</li><li> Laufwerksbuchstabe ist nicht erforderlich</li><li> Formatierung mit NTFS oder ReFS zulässig</li><li> Kann für die Fehlertoleranz optional mit Hardware-RAID konfiguriert werden</li><li> Sollte von Sicherungen und Antivirenscans ausgeschlossen werden</li><li> Ein Datenträger Zeuge wird mit direkte Speicherplätze nicht unterstützt.</li>|
| Dateifreigabezeuge     | <ul><li>SMB-Dateifreigabe, die auf einem Dateiserver konfiguriert ist, der Windows Server ausführt</li><li> Speichert keine Kopie der Clusterdatenbank</li><li> Verwaltet Clusterinformationen nur in der Datei "witness.log"</li><li> Besonders für Cluster mit repliziertem Speicher für mehrere Standorte geeignet </li>       |  <ul><li>Es sind mindestens 5 MB freier Speicherplatz erforderlich</li><li> Muss dem einzelnen Cluster zugeteilt und nicht zum Speichern von Benutzer- oder Anwendungsdaten verwendet werden</li><li> Schreibberechtigungen müssen für das Computerobjekt für den Clusternamen aktiviert sein</li></ul><br>Nachfolgend sind weitere Überlegungen zu einem Dateiserver aufgeführt, der den Dateifreigabezeugen hostet:<ul><li>Ein einzelner Dateiserver mit Dateifreigabezeugen kann für mehrere Cluster konfiguriert werden.</li><li> Der Dateiserver muss sich an einem Standort befinden, der von der Clusterarbeitsauslastung getrennt ist. Dadurch haben alle Clusterstandorte bei einer Unterbrechung der Netzwerkkommunikation zwischen den Standorten dieselbe Chance, diesen Zwischenfall zu überstehen. Wenn sich der Dateiserver am gleichen Standort befindet, wird der Standort zum primären Standort. Dies ist dann der einzige Standort, der auf die Dateifreigabe zugreifen kann.</li><li> Der Dateiserver kann auf einem virtuellen Computer ausgeführt werden, wenn der virtuelle Computer nicht auf demselben Cluster gehostet wird, der den Dateifreigabezeugen verwendet.</li><li> Der Dateiserver kann auf einem separaten Failovercluster konfiguriert werden, um eine hohe Verfügbarkeit zu bieten. </li>      |
| Cloudzeuge     |  <ul><li>Eine in Azure BLOB Storage gespeicherte Zeugen Datei</li><li> Empfohlen, wenn alle Server im Cluster über eine zuverlässige Internet Verbindung verfügen.</li>      |  Siehe bereitstellen [eines cloudzeugen](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness).       |

### <a name="node-vote-assignment"></a>„Knotenvotumszuweisung“

Als erweiterte Quorum Konfigurationsoption können Sie die Quorum Stimmen auf Knoten Basis zuweisen oder entfernen. Standardmäßig werden allen Knoten Stimmen zugewiesen. Unabhängig von der Stimmenzuweisung funktionieren alle Knoten im Cluster weiterhin. Zudem erhalten sie weiterhin Clusterdatenbankupdates und können Anwendungen hosten.

Möglicherweise möchten Sie die Stimmen von Knoten in bestimmten Notfallwiederherstellungskonfigurationen entfernen. Bei einem Cluster mit mehreren Standorten könnten Sie z. B. Stimmen von den Knoten am Sicherungsstandort entfernen, damit sich diese Knoten nicht auf die Quorumberechnungen auswirken. Diese Konfiguration wird nur für standortübergreifende manuelle Failover empfohlen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Quorumüberlegungen zu Notfallwiederherstellungskonfigurationen](#quorum-considerations-for-disaster-recovery-configurations).

Die konfigurierte Stimme eines Knotens kann durch Überprüfen der allgemeinen **nodeweight** -Eigenschaft des Cluster Knotens mithilfe des Windows PowerShell-Cmdlets [Get-clusternode](https://technet.microsoft.com/library/hh847268.aspx)überprüft werden. Der Wert 0 gibt an, dass für den Knoten keine Quorumstimme konfiguriert ist. Der Wert 1 gibt an, dass die Quorumstimme des Knotens zugewiesen wurde und sie vom Cluster verwaltet wird. Weitere Informationen zur Verwaltung von Knotenstimmen finden Sie unter [Dynamische Quorumverwaltung](#dynamic-quorum-management) in diesem Thema.

Die Stimmenzuweisung für alle Clusterknoten kann mithilfe des Validierungstests **Clusterquorum überprüfen** überprüft werden.

#### <a name="additional-considerations-for-node-vote-assignment"></a>Weitere Überlegungen zur Zuweisung von Knoten Stimmen

  - Die Knotenvotumszuweisung wird nicht empfohlen, um eine ungerade Anzahl von abstimmenden Knoten zu erzwingen. Stattdessen müssen Sie einen Datenträgerzeugen oder einen Dateifreigabezeugen konfigurieren. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Zeugen Konfiguration](#witness-configuration) .
  - Wenn die dynamische Quorumverwaltung aktiviert ist, können die Stimmen nur für Knoten dynamisch zugewiesen oder entfernt werden, die für die Zuweisung von Knotenstimmen konfiguriert sind. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Dynamische Quorumverwaltung](#dynamic-quorum-management).

### <a name="dynamic-quorum-management"></a>„Dynamische Quorumverwaltung“

In Windows Server 2012 können Sie als erweiterte Quorum Konfigurationsoption die dynamische Quorum Verwaltung nach Clustern aktivieren. Weitere Informationen zur Funktionsweise des dynamischen Quorums finden Sie in [dieser Erklärung](../storage/storage-spaces/understand-quorum.md#dynamic-quorum-behavior).

Bei der dynamischen Quorumverwaltung ist es außerdem für Cluster möglich, dass sie auf dem letzten verbleibenden Clusterknoten ausgeführt werden können. Durch die dynamische Anpassung der Anforderungen an die Quorummehrheit kann der Cluster das fortlaufende Herunterfahren von Knoten für einen einzelnen Knoten fortsetzen.

Die vom Cluster zugewiesene dynamische Stimme eines Knotens kann mit der allgemeinen **dynamicweight** -Eigenschaft des Cluster Knotens mithilfe des Windows PowerShell-Cmdlets [Get-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode?view=win10-ps) überprüft werden. Der Wert 0 gibt an, dass der Knoten keine Quorumstimme besitzt. Der Wert 1 gibt an, dass der Knoten eine Quorumstimme besitzt.

Die Stimmenzuweisung für alle Clusterknoten kann mithilfe des Validierungstests **Clusterquorum überprüfen** überprüft werden.

#### <a name="additional-considerations-for-dynamic-quorum-management"></a>Weitere Überlegungen zur dynamischen Quorum Verwaltung

- Die dynamische Quorumverwaltung gestattet es dem Cluster nicht, dass die Mehrheit der abstimmenden Mitglieder gleichzeitig einen Fehler erhält. Damit die Ausführung fortgesetzt werden kann, muss der Cluster beim Herunterfahren eines Clusters oder bei einem Fehler immer über die Quorummehrheit verfügen.

- Falls Sie die Stimme eines Knotens explizit entfernt haben, kann sie vom Cluster nicht dynamisch hinzugefügt oder entfernt werden.
- Wenn direkte Speicherplätze aktiviert ist, kann der Cluster nur zwei Knoten Ausfälle unterstützen. Dies wird im [Abschnitt Pool Quorum](../storage/storage-spaces/understand-quorum.md) ausführlicher erläutert.

## <a name="general-recommendations-for-quorum-configuration"></a>„Allgemeine Empfehlungen zur Quorumkonfiguration“

Die Clustersoftware konfiguriert das Quorum für einen neuen Cluster auf Basis der Anzahl der konfigurierten Knoten und der Verfügbarkeit von freigegebenen Speicher automatisch. Dies ist im Allgemeinen die am besten geeignete Quorumkonfiguration für diesen Cluster. Es ist jedoch eine gute Idee, die Quorumkonfiguration zu überprüfen, nachdem der Cluster erstellt wurde und bevor der Cluster in der Produktionsumgebung eingesetzt wird. Zum Anzeigen der detaillierten Konfiguration des Cluster Quorums können Sie den Konfigurationsüberprüfungs-Assistenten oder das Windows PowerShell-Cmdlet [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) verwenden, um den Test **Quorum Konfiguration** überprüfen auszuführen. In Failovercluster-Manager wird die grundlegende Quorum Konfiguration in den zusammenfassenden Informationen für den ausgewählten Cluster angezeigt. Sie können auch die Informationen zu den Quorum Ressourcen überprüfen, die beim Ausführen des Windows PowerShell-Cmdlets [Get-Clusterquorum](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusterquorum?view=win10-ps) zurückgegeben werden.

Sie können den Test **Quorumkonfiguration überprüfen** jederzeit ausführen, um zu überprüfen, ob die Quorumkonfiguration für Ihren Cluster optimal geeignet ist. Die Testausgabe gibt die optimalen Einstellungen an. Zudem weist die darauf hin, ob eine Änderung an der Quorumkonfiguration empfohlen wird. Wenn eine Änderung empfohlen wird, können Sie die empfohlenen Einstellungen mithilfe des Assistenten zum Konfigurieren des Clusterquorums anwenden.

Ändern Sie die Quorumkonfiguration nicht nachdem der Cluster in der Produktionsumgebung eingesetzt wurde, sofern Sie nicht ermittelt haben, dass die Änderung für Ihren Cluster angemessen ist. In folgenden Situationen können Sie eine Änderung der Quorumkonfiguration erwägen:

- Hinzufügen oder Entfernen von Knoten
- Hinzufügen oder Entfernen von Speicher
- Bei langfristigen Knoten- oder Zeugenfehlern
- Wiederherstellung eines Clusters in einem Notfallwiederherstellungsszenario mit mehreren Standorten

Weitere Informationen zum Überprüfen eines Failoverclusters finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

## <a name="configure-the-cluster-quorum"></a>„Konfigurieren des Clusterquorums“

Sie können die Cluster Quorum Einstellungen mithilfe Failovercluster-Manager oder der Windows PowerShell-Cmdlets für Failovercluster konfigurieren.

> [!IMPORTANT]
> In der Regel ist die Quorumkonfiguration am besten geeignet, die vom Assistenten zum Konfigurieren des Clusterquorums empfohlen wird. Es wird empfohlen, dass Sie die Quorumkonfiguration nur anpassen, wenn Sie ermittelt haben, dass die Änderung für den Cluster angemessen ist. Weitere Informationen finden Sie in diesem Thema unter [Allgemeine Empfehlungen zur Quorumkonfiguration](#general-recommendations-for-quorum-configuration).

### <a name="configure-the-cluster-quorum-settings"></a>Konfigurieren der Clusterquorumeinstellungen

Die erforderlichen Mindestberechtigungen zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** auf den einzelnen Clusterservern oder eine gleichwertige Mitgliedschaft. Das verwendete Konto muss zudem ein Domänenbenutzerkonto sein.

> [!NOTE]
> Sie können die Clusterquorumkonfiguration ändern, ohne den Cluster zu beenden oder die Clusterressourcen offline zu stellen.

### <a name="change-the-quorum-configuration-in-a-failover-cluster-by-using-failover-cluster-manager"></a>Ändern Sie die Quorum Konfiguration in einem Failovercluster, indem Sie Failovercluster-Manager

1. Wählen Sie im Failovercluster-Manager den zu ändernden Cluster aus, oder geben Sie ihn an.
2. Wählen Sie bei ausgewähltem Cluster unter **Aktionen**die Option **Weitere Aktionen**aus, und klicken Sie dann auf **Cluster Quorum Einstellungen konfigurieren**. Der Assistent zum Konfigurieren des Clusterquorums wird angezeigt. Klicken Sie auf **Weiter**.
3. Wählen Sie auf der Seite **Quorumkonfigurationsoption auswählen** eine der drei verfügbaren Konfigurationsoptionen aus, und führen Sie dann die Schritte für diese Option aus. Bevor Sie die Quorumeinstellungen konfigurieren, können Sie Ihre Auswahl überprüfen. Weitere Informationen zu den Optionen finden Sie Untergrund Legendes zu [Quorums](#understanding-quorum)weiter oben in diesem Thema.

    - Um dem Cluster das automatische Zurücksetzen der Quorum Einstellungen zu ermöglichen, die für Ihre aktuelle Cluster Konfiguration optimal sind, wählen Sie **typische Einstellungen verwenden** aus, und schließen Sie dann den Assistenten ab.
    - Um den Quorum Zeugen hinzuzufügen oder zu ändern, wählen Sie **den Quorum Zeugen hinzufügen oder ändern**aus, und führen Sie dann die folgenden Schritte aus. Weitere Informationen und Überlegungen zum Konfigurieren eines Quorumzeugen finden Sie in diesem Thema unter [Zeugenkonfiguration](#witness-configuration).

      1. Wählen Sie auf der Seite **Quorumzeugen auswählen** eine Option zum Konfigurieren eines Datenträgerzeugen oder eines Dateifreigabezeugen aus. Der Assistent zeigt die Zeugenauswahloptionen an, die für Ihren Cluster empfohlen werden.

          > [!NOTE]
          > Sie können auch die Option **Keinen Quorumzeugen konfigurieren** auswählen und dann den Assistenten abschließen. Wenn Sie über eine gerade Anzahl von abstimmenden Knoten in Ihrem Cluster verfügen, ist dies möglicherweise nicht die empfohlene Konfiguration.

      2. Wenn Sie die Option zum Konfigurieren eines Datenträgerzeugen auswählen, wählen Sie auf der Seite **Speicherzeugen konfigurieren** das Speichervolume aus, das Sie als Datenträgerzeugen zuweisen möchten, und schließen Sie dann den Assistenten ab.
      3. Wenn Sie die Option zum Konfigurieren eines Dateifreigabezeugen auswählen, geben Sie auf der Seite **Dateifreigabezeugen konfigurieren** eine Dateifreigabe ein, oder navigieren Sie zu dieser Freigabe, die als Zeugenressource verwendet wird, und schließen Sie dann den Assistenten ab.

    - Um die Einstellungen für die Quorum Verwaltung zu konfigurieren und den Quorum Zeugen hinzuzufügen oder zu ändern, wählen Sie **Erweiterte Quorum Konfiguration und Zeugen Auswahl**aus, und führen Sie dann die folgenden Schritte aus. Weitere Informationen und Überlegungen zu den erweiterten Quorumkonfigurationseinstellungen finden Sie in diesem Thema unter [Knotenvotumszuweisung](#node-vote-assignment) und [Dynamische Quorumverwaltung](#dynamic-quorum-management).

      1. Wählen Sie auf der Seite **Votierungskonfiguration auswählen** eine Option zum Zuweisen von Stimmen zu Knoten aus. Standardmäßig wird allen Knoten eine Stimme zugewiesen. In bestimmten Szenarien können Sie Stimmen jedoch nur zu einer Teilmenge von Knoten zuweisen.

          > [!NOTE]
          > Sie können auch die Option **Keine Knoten** auswählen. Dies wird im Allgemeinen nicht empfohlen, da es den Knoten dadurch nicht gestattet ist, an der Quorumabstimmung teilzunehmen. Zudem erfordert sie die Konfiguration eines Datenträgerzeugen. Der Datenträgerzeuge wird für den Cluster zu einem einzelnen Fehlerpunkt.

      2. Auf der Seite **Quorumverwaltung konfigurieren** können Sie die Option **Die Zuordnung von Knotenvoten kann vom Cluster dynamisch verwaltet werden** aktivieren oder deaktivieren. Durch die Auswahl dieser Option wird die Verfügbarkeit des Clusters im Allgemeinen erhöht. Die Option ist standardmäßig aktiviert, und es wird dringend empfohlen, diese Option nicht zu deaktivieren. Mithilfe dieser Option kann der Cluster in Fehlerszenarien weiterhin ausgeführt werden, die nicht möglich sind, wenn diese Option deaktiviert ist.
      3. Wählen Sie auf der Seite **Quorumzeugen auswählen** eine Option zum Konfigurieren eines Datenträgerzeugen oder eines Dateifreigabezeugen aus. Der Assistent zeigt die Zeugenauswahloptionen an, die für Ihren Cluster empfohlen werden.

          > [!NOTE]
          > Sie können auch die Option **Keinen Quorumzeugen konfigurieren** auswählen und dann den Assistenten abschließen. Wenn Sie über eine gerade Anzahl von abstimmenden Knoten in Ihrem Cluster verfügen, ist dies möglicherweise nicht die empfohlene Konfiguration.

      4. Wenn Sie die Option zum Konfigurieren eines Datenträgerzeugen auswählen, wählen Sie auf der Seite **Speicherzeugen konfigurieren** das Speichervolume aus, das Sie als Datenträgerzeugen zuweisen möchten, und schließen Sie dann den Assistenten ab.
      5. Wenn Sie die Option zum Konfigurieren eines Dateifreigabezeugen auswählen, geben Sie auf der Seite **Dateifreigabezeugen konfigurieren** eine Dateifreigabe ein, oder navigieren Sie zu dieser Freigabe, die als Zeugenressource verwendet wird, und schließen Sie dann den Assistenten ab.

4. Klicken Sie auf **Weiter**. Bestätigen Sie Ihre Auswahl auf der angezeigten Bestätigungsseite, und klicken Sie dann auf **weiter**.

Wenn Sie den Assistenten ausführen und die Seite **Zusammenfassung** angezeigt wird, klicken Sie auf **Bericht anzeigen**, wenn Sie einen Bericht über die vom Assistenten durchgeführten Aufgaben anzeigen möchten. Der neueste Bericht verbleibt im Ordner " <em>systemroot</em>**\\-\\Cluster Berichte** " mit dem Namen " **quorenconfiguration. MHT**".

> [!NOTE]
> Nachdem Sie das Clusterquorum konfiguriert haben, wird empfohlen, dass Sie den Test **Quorumkonfiguration überprüfen** ausführen, um die aktualisierten Quorumeinstellungen zu überprüfen.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

In den folgenden Beispielen wird gezeigt, wie das Cmdlet [Set-Clusterquorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum?view=win10-ps) und andere Windows PowerShell-Cmdlets zum Konfigurieren des Cluster Quorums verwendet werden.

Im folgenden Beispiel wird die Quorumkonfiguration für Cluster *CONTOSO-FC1* in eine Konfiguration mit einfacher Knotenmehrheit ohne Quorumzeugen geändert.

```PowerShell
Set-ClusterQuorum –Cluster CONTOSO-FC1 -NodeMajority
```

Im folgenden Beispiel wird die Quorumkonfiguration auf dem lokalen Cluster in eine Knotenmehrheit mit Zeugenkonfiguration geändert. Die Datenträgerressourcen namens *Cluster Disk 2* wird als Datenträgerzeuge konfiguriert.

```PowerShell
Set-ClusterQuorum -NodeAndDiskMajority "Cluster Disk 2"
```

Im folgenden Beispiel wird die Quorumkonfiguration auf dem lokalen Cluster in eine Knotenmehrheit mit Zeugenkonfiguration geändert. Die Dateifreigabe Ressource mit dem Namen * \\ \\"\deso-FS\\-* Dateifreigabe" ist als Datei frei gaben Zeuge konfiguriert.

```PowerShell
Set-ClusterQuorum -NodeAndFileShareMajority "\\fileserver\fsw"
```

Im folgenden Beispiel wird die Quorumstimme von Knoten *ContosoFCNode1* auf dem lokalen Cluster entfernt.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=0
```

Im folgenden Beispiel wird die Quorumstimme zum Knoten *ContosoFCNode1* auf dem lokalen Cluster hinzugefügt.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=1
```

Im folgenden Beispiel wird die **DynamicQuorum**-Eigenschaft des Clusters *CONTOSO-FC1* aktiviert (wenn diese zuvor deaktiviert war):

```PowerShell
(Get-Cluster CONTOSO-FC1).DynamicQuorum=1
```

## <a name="recover-a-cluster-by-starting-without-quorum"></a>Wiederherstellen eines Clusters durch Starten ohne Quorum

Ein Cluster ohne ausreichende Anzahl von Quorumstimmen wird nicht gestartet. Als ersten Schritt sollten Sie immer die Clusterquorumkonfiguration bestätigen und untersuchen, warum der Cluster das Quorum verloren hat. Dies kann vorkommen, wenn Sie über nicht reagierende Knoten verfügen. Es kann auch auftreten, wenn der primäre Standort bei einem Cluster mit mehreren Standorten nicht erreichbar ist. Nachdem Sie die Hauptursache für den Clusterfehler ermittelt haben, können Sie die in diesem Abschnitt beschriebenen Wiederherstellungsschritte ausführen.

> [!NOTE]
> * Wenn der Clusterdienst aufgrund eines verlorenen Quorums beendet wird, wird Ereignis-ID 1177 im Systemprotokoll angezeigt.
> * Die Ursache für ein verlorenes Clusterquorum muss immer ermittelt werden.
> * Bevorzugt sollte der Knoten oder Quorumzeuge in einen fehlerfreien Status (zum Cluster hinzugefügt) versetzt werden, anstatt den Cluster ohne Zeugen zu starten.

### <a name="force-start-cluster-nodes"></a>Erzwungenes Starten von Clusterknoten

Nachdem Sie ermittelt haben, dass Ihr Cluster nicht wiederhergestellt werden kann, indem Sie die Knoten oder den Quorumzeugen in einen fehlerfreien Status versetzen, ist es erforderlich, den Start des Clusters zu erzwingen. Durch den erzwungenen Start des Clusters werden die Einstellungen Ihrer Clusterquorumkonfiguration außer Kraft gesetzt und der Cluster im Modus **ForceQuorum** gestartet.

Der erzwungene Start eines Clusters ohne Quorum ist möglicherweise besonders hilfreich für Cluster mit mehreren Standorten. Betrachten Sie ein Notfallwiederherstellungsszenario mit einem Cluster, der separat angeordnete primäre Standorte und Sicherungsstandorte, *SiteA* und *SiteB*, enthält. Wenn bei *SiteA* ein ernsthafter Notfall eintritt, könnte es sehr lange dauern, bis der Standort wieder online ist. Sie würden dann für *SiteB* sicherlich erzwingen wollen, dass dieser Standort online gestellt wird, auch wenn er kein Quorum besitzt.

Wenn ein Cluster im **ForceQuorum**-Modus gestartet wird und er ausreichend Quorumstimmen zurückgewonnen hat, verlässt der Cluster automatisch den erzwungenen Status und verhält sich normal. Daher ist es nicht erforderlich, den Cluster erneut normal zu starten. Wenn der Cluster einen Knoten und dann das Quorum verliert, wird er offline gestellt, da er sich nicht mehr im erzwungenen Status befindet. Damit der Cluster wieder online geschaltet werden kann, wenn er nicht über ein Quorum verfügt, muss der Cluster ohne Quorum gestartet werden.

> [!IMPORTANT]
> * Nachdem der Start eines Clusters erzwungen wurde, verfügt der Administrator über die vollständige Kontrolle über den Cluster.
> * Der Cluster verwendet die Clusterkonfiguration auf dem Knoten, auf dem der Start des Clusters erzwungen wurde und repliziert ihn auf alle anderen Knoten, die verfügbar sind.
> * Durch den erzwungenen Start des Clusters ohne Quorum werden alle Quorumkonfigurationseinstellungen ignoriert, während der Cluster im Modus **ForceQuorum** verbleibt. Dies umfasst bestimmte Knotenvotumszuweisungen und Einstellungen für die dynamische Quorumverwaltung.

### <a name="prevent-quorum-on-remaining-cluster-nodes"></a>Verhindern des Quorums auf verbleibenden Clusterknoten

Nachdem Sie den erzwungenen Start des Clusters auf einem Knoten ausgeführt haben, ist es erforderlich, alle verbleibenden Knoten im Cluster mit einer Einstellung zu starten, um das Quorum zu verhindern. Ein Knoten, der mit einer Einstellung gestartet wurde, die das Quorum verhindert, zeigt dem Clusterdienst an, dass die Zuordnung zu einem vorhandenen aktiven Cluster erfolgen soll, anstatt eine neue Clusterinstanz zu erzeugen. Dadurch wird verhindert, dass die verbleibenden Knoten einen unterteilten Cluster bilden, der zwei konkurrierende Instanzen enthält.

Dies ist erforderlich, wenn Sie Ihren Cluster in einigen Notfallwiederherstellungsszenarien mit mehreren Standorten wiederherstellen müssen, nachdem Sie den erzwungenen Start des Clusters an Ihrem Sicherungsstandort, *SiteB*, ausgeführt haben. Um den Cluster mit dem erzwungenen Start am Standort *SiteB* hinzuzufügen, müssen die Knoten am primären Standort, *SiteA*, mit verhindertem Quorum gestartet werden.

> [!IMPORTANT]
> Nach dem erzwungenen Start eines Clusters auf einem Knoten wird empfohlen, dass Sie die verbleibenden Knoten immer mit verhindertem Quorum starten.

So stellen Sie den Cluster mit Failovercluster-Manager wieder her:

1. Wählen Sie im Failovercluster-Manager den wiederherzustellenden Cluster aus, oder geben Sie ihn an.
2. Wählen Sie bei ausgewähltem Cluster unter **Aktionen**die Option **Cluster Start erzwingen**aus.

    Der Failovercluster-Manager erzwingt den Start des Clusters auf allen erreichbaren Knoten. Der Cluster verwendet beim Starten die aktuelle Clusterkonfiguration.

> [!NOTE]
> * Um den Start des Clusters auf einem bestimmten Knoten zu erzwingen, der eine Cluster Konfiguration enthält, die Sie verwenden möchten, müssen Sie die Windows PowerShell-Cmdlets oder entsprechende Befehlszeilen Tools verwenden, die nach diesem Verfahren dargestellt werden. 
> * Wenn Sie den Failover-Manager verwenden, um die Verbindung zu einem Cluster mit erzwungenem Start herzustellen, und Sie die Aktion **Clusterdienst starten** verwenden, um einen Knoten zu starten, dann wird der Knoten automatisch mit der Einstellung gestartet, die das Quorum verhindert.

#### <a name="windows-powershell-equivalent-commands-start-clusternode"></a>Entsprechende Windows PowerShell-Befehle (Start-clusternode)

Im folgenden Beispiel wird gezeigt, wie das **Start-ClusterNode**-Cmdlet verwendet wird, um den Start des Clusters auf dem Knoten *ContosoFCNode1* zu erzwingen.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –FQ
```

Alternativ können Sie den folgenden Befehl lokal auf dem Knoten eingeben:

```PowerShell
Net Start ClusSvc /FQ
```

Im folgenden Beispiel wird gezeigt, wie das **Start-ClusterNode**-Cmdlet verwendet wird, um den Clusterdienst mit dem auf Knoten *ContosoFCNode1* verhinderten Quorum zu starten.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –PQ
```

Alternativ können Sie den folgenden Befehl lokal auf dem Knoten eingeben:

```PowerShell
Net Start ClusSvc /PQ
```

## <a name="quorum-considerations-for-disaster-recovery-configurations"></a>„Quorumüberlegungen zu Notfallwiederherstellungskonfigurationen“

In diesem Abschnitt werden die Merkmale und Quorumkonfigurationen für zwei Clusterkonfigurationen mit mehreren Standorten für Notfallwiederherstellungsbereitstellungen zusammengefasst. Die Anweisungen zur Quorumkonfiguration unterscheiden sich in Abhängigkeit davon, ob für Arbeitsauslastungen zwischen den Standorten ein automatisches oder manuelles Failover erforderlich ist. Ihre Konfiguration hängt normalerweise von den in Ihrer Organisation vorhandenen Vereinbarungen zum Servicelevel (SLAs) ab, um Clusterarbeitsauslastungen bei einem Fehler oder Notfall an einem Standort bereitzustellen und zu unterstützen.

### <a name="automatic-failover"></a>Automatisches Failover

In dieser Konfiguration besteht der Cluster aus zwei oder mehr Standorten, die Clusterrollen hosten können. Wenn an einem Standort ein Fehler auftritt, wird für die anderen Standorte ein automatisches Failover erwartet. Daher muss das Clusterquorum konfiguriert werden, damit ein beliebiger Standort einen vollständigen Standortfehler aushalten kann.

In der folgenden Tabelle sind die Überlegungen und Empfehlungen für diese Konfiguration zusammengefasst.

| Element  | BESCHREIBUNG  |
| ---------| ---------|
| Anzahl von Knotenstimmen pro Standort     | Sollte gleich sein       |
| „Knotenvotumszuweisung“     |  Knotenstimmen sollten nicht entfernt werden, da alle Knoten gleich wichtig sind       |
| „Dynamische Quorumverwaltung“     |   Sollte aktiviert sein      |
| „Zeugenkonfiguration“     |  Es wird ein Dateifreigabezeuge empfohlen, der an einem Standort konfiguriert ist, der sich von Clusterstandorten unterscheidet       |
| Arbeitsauslastungen     |  Arbeitsauslastungen können an einem beliebigen Standort konfiguriert werden       |

#### <a name="additional-considerations-for-automatic-failover"></a>Weitere Überlegungen zum automatischen Failover

- Das Konfigurieren eines Dateifreigabezeugen an einem separaten Standort ist erforderlich, damit jeder Standort die gleichen Überlebenschancen erhält. Weitere Informationen finden Sie in diesem Thema unter [Zeugenkonfiguration](#witness-configuration).

### <a name="manual-failover"></a>Manuelles Failover

In dieser Konfiguration besteht der Cluster aus einem primären Standort, *SiteA*, und einem Sicherungsstandort (Wiederherstellungsstandort), *SiteB*. Clusterrollen werden am Standort *SiteA* gehostet. Wenn auf allen Knoten in *SiteA* ein Fehler auftritt, beendet der Cluster aufgrund der Clusterquorumkonfiguration seine Funktion. In diesem Szenario muss der Administrator ein manuelles Failover für die Clusterdienste zum Standort *SiteB* durchführen und weitere Schritte zum Wiederherstellen des Clusters ausführen.

In der folgenden Tabelle sind die Überlegungen und Empfehlungen für diese Konfiguration zusammengefasst.

| Element   |BESCHREIBUNG  |
| ---------| ---------|
| Anzahl von Knotenstimmen pro Standort     |  <ul><li> Knotenstimmen sollten nicht von Knoten am primären Standort, **SiteA**, entfernt werden.</li><li>Knotenstimmen sollten von Knoten am Sicherungsstandort, **SiteB**, entfernt werden.</li><li>Wenn am Standort **SiteA** ein langfristiger Ausfall eintritt, müssen die Stimmen zu Knoten am Standort **SiteB** zugewiesen werden, um im Rahmen der Wiederherstellung eine Quorummehrheit an diesem Standort zu aktivieren.</li>       |
| „Dynamische Quorumverwaltung“     |  Sollte aktiviert sein       |
| „Zeugenkonfiguration“     |  <ul><li>Konfigurieren eines Zeugen bei ungerader Anzahl der Knoten am Standort **SiteA**</li><li>Wenn ein Zeuge erforderlich ist, konfigurieren Sie entweder einen Dateifreigabezeugen oder einen Datenträgerzeugen, auf den nur Knoten am Standort **SiteA** zugreifen können (gelegentlich als asymmetrischer Datenträgerzeuge bezeichnet).</li>       |
| Arbeitsauslastungen     |  Verwenden bevorzugter Besitzer, damit Arbeitsauslastungen auf Knoten von Standort **SiteA** erhalten bleiben       |

#### <a name="additional-considerations-for-manual-failover"></a>Weitere Überlegungen zum manuellen Failover

- Nur die Knoten am Standort *SiteA* werden anfänglich mit Quorumstimmen konfiguriert. Dies ist erforderlich, um sicherzustellen, dass sich der Status der Knoten am Standort *SiteB* nicht auf das Clusterquorum auswirkt.
- Die Wiederherstellungsschritte können in Abhängigkeit davon abweichen, ob Standort *SiteA* einen temporären oder einen langfristigen Fehler aushält.

## <a name="more-information"></a>Weitere Informationen

* [Failoverclustering](failover-clustering.md)
* [Windows PowerShell-Cmdlets für Failovercluster](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)
* [Grundlegendes zum Cluster-und Pool Quorum](../storage/storage-spaces/understand-quorum.md)