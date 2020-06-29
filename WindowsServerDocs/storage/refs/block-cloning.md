---
ms.assetid: fd427da3-3869-428f-bf2a-56c4b7d99b40
title: Block-Clone-Vorgänge auf ReFS
author: gawatu
ms.author: gawatu
manager: gawatu
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-file-systems
ms.openlocfilehash: c74e8744c22e2be174c1f1297e0472e5f32e1fe8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475407"
---
# <a name="block-cloning-on-refs"></a>Block-Clone-Vorgänge auf ReFS

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Block-Clone-Vorgänge weisen das Dateisystem an, den Bytewert von Dateien im Namen einer Anwendung zu kopieren, bei der die Zieldatei entweder der Ausgangsdatei gleicht oder nicht. Kopiervorgänge sind leider sehr kostspielig, da sie teure Lese- und Schreibvorgänge für die zugrunde liegenden, physischen Daten auslösen.

Block-Clone-Vorgänge auf ReFS führen jedoch Kopien als kostengünstige Metadatenvorgänge aus, anstatt Lese- und Schreibvorgänge auf Dateidaten durchzuführen. ReFS ermöglicht mehreren Dateien, die gleichen logischen Cluster (physische Speicherorte auf einem Datenträger) zu teilen, wodurch Kopiervorgänge nur einer Region der Datei auf einem separaten physischen Speicherort zugeordnet werden müssen und der teure, physische Vorgang zu einem schnellen logischen Vorgang konvertiert wird. Dadurch werden Kopien schneller erstellt und es wird weniger E/A im zugrunde liegenden Speicher generiert. Diese Verbesserung ist auch von Vorteil für Virtualisierungs-Workloads, da VHDX-Prüfpunkt-Mergevorgängen bei der Verwendung von Block-Clone-Vorgängen erheblich beschleunigt werden. Da mehrere Dateien die gleichen logischen Cluster teilen können, werden identische Daten physisch nicht mehrmals gespeichert, was die Speicherkapazität verbessert.

## <a name="how-it-works"></a>Funktionsweise

Block-Clone-Vorgänge auf ReFS konvertieren eine Dateidatenoperation in einen Metadatenvorgang. Um diese Optimierung vorzunehmen, führt ReFS Referenzzähler in die Metadaten für die kopierten Regionen ein. Diese Referenzzähler zeichnen die Anzahl der eindeutigen Dateiregionen auf, die die gleichen physischen Regionen aufweisen. Dadurch können mehrere Dateien die gleichen physischen Daten gemeinsam nutzen:

![Das Anzeigen der Referenzzähler wird aktualisiert, wenn mehrere Dateien auf die gleiche Region verweisen](media/ref-count-example.gif)

Durch das Beibehalten der Referenzzähler für jeden logischen Cluster behält ReFS die Isolation zwischen Dateien bei: Schreibvorgänge auf freigegebene Regionen lösen einen Zuordnungsmechanismus der Schreibvorgänge aus, wobei ReFS dem eingehenden Schreibvorgang eine neue Region zuordnet. Dieser Mechanismus bewahrt die Integrität der freigegebenen logischen Cluster.

### <a name="example"></a>Beispiel
Angenommen, es gibt zwei Dateien: X und Y, wobei jede Datei aus drei Bereichen besteht und jede Region auf getrennte logische Cluster verweist.

![Zwei Dateien, die jeweils drei unterschiedliche Regionen aufweisen, die alle auf Regionen mit der Referenzzahl 1 hinweisen.](media/block-clone-1.png)

Angenommen eine Anwendung erteilt einen Block-Clone-Vorgang von Datei X für Datei Y, bei dem die Regionen A und B auf den Versatz von Bereich E kopiert werden. Dies würde folgenden Dateisystemstatus ergeben:

![Referenzzähler zeigt für die blockierte geklonte Regionen „2” an](media/block-clone-2.png)

Dieser Dateisystemstatus zeigt eine erfolgreiche Duplizierung der Block-Clone-Region an. Da ReFS diesen Kopiervorgang nur beim Update von VCN- auf LCN-Zuordnungen durchführt, werden keine physischen Daten gelesen und die physischen Daten in der Datei Y werden nicht überschrieben. Datei X und Datei Y teilen jetzt logische Cluster, was durch die Referenzzähler in der Tabelle dargestellt wird. Da keine Daten physisch kopiert wurde, reduziert ReFS den Kapazitätsverbrauch auf dem Volume.

Angenommen die Anwendung versucht Region A der Datei X zu überschreiben. ReFS dupliziert den gemeinsamen Bereich, aktualisiert die Referenzzähler dementsprechend und führt den eingehenden Schreibvorgang auf die neu duplizierte Region aus. Dadurch wird sichergestellt, dass die Isolation zwischen den Dateien beibehalten wird.

![Die Isolation wird durch das Schreiben auf die neue Region G und das Aktualisieren der Referenzzähler beibehalten](media/block-clone-3.png)

Nach dem Ändern des Schreibvorgangs wird Region B weiterhin von beide Dateien verwendet. Falls Region A größer als ein Cluster wäre, würde nur der geänderte Cluster dupliziert und der verbleibende Teil würde freigegeben.


## <a name="functionality-restrictions-and-remarks"></a>Einschränkungen der Funktion und Hinweise
- Die Quell- und Zielregion muss an einer Cluster-Begrenzung beginnen und enden.
- Die geklonte Region muss kleiner als 4 GB lang sein.
- Die maximale Anzahl von Datei Regionen, die derselben physischen Region zugeordnet werden können, ist 8175.
- Die Zielregion darf nicht über das Ende der Datei erweitert werden. Falls die Anwendung das Ziel mit geklonten Daten erweitern möchte, müssen sie zuerst [SetEndOfFile](https://msdn.microsoft.com/library/windows/desktop/aa365531(v=vs.85).aspx) aufrufen.
- Wenn sich die Quell- und Zielregionen in derselben Datei befinden, dürfen diese nicht überlappen. (Die Anwendung kann möglicherweise durch Aufteilen des Block-Clone-Vorgangs in mehrere Block-Clone-Vorgänge ausgeführt werden, wenn diese nicht überlappen).
- Die Quell- und Zieldateien müssen sich auf demselben Volume ReFS befinden.
- Die Quell- und Zieldateien müssen die gleichen [Integrity Streams](https://msdn.microsoft.com/library/windows/desktop/gg258117(v=vs.85).aspx)-Einstellungen aufweisen.
- Hat die Quelldatei eine geringe Datendichte, muss die Zieldatei ebenfalls eine geringe Datendichte aufweisen.
- Der Block-Clone-Vorgang durchbricht die Shared Opportunistic Sperrfunktion (auch bekannt als [Level 2 Opportunistic Locks](https://msdn.microsoft.com/library/windows/desktop/aa365713(v=vs.85).aspx)).
- Das ReFS-Volume muss mit Windows Server 2016 formatiert worden sein und wenn Failoverclustering verwendet wird muss die Clustering-Funktionsebene Windows Server 2016 oder höher zum Zeitpunkt der Formatierung verwendet haben.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [ReFS – Übersicht](refs-overview.md)
-   [ReFS Integrity Streams](integrity-streams.md)
-   [Übersicht über direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)
-   [DUPLICATE_EXTENTS_DATA](https://msdn.microsoft.com/library/windows/desktop/mt590821(v=vs.85).aspx)
-   [FSCTL_DUPLICATE_EXTENTS_TO_FILE](https://msdn.microsoft.com/library/windows/desktop/mt590823(v=vs.85).aspx)
