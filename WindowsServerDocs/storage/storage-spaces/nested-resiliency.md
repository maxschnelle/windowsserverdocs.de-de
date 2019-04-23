---
title: Geschachtelte resilienz für "direkte Speicherplätze"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dansimp
ms.technology: storagespaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2018
ms.openlocfilehash: 206d5d19ec55774f9055e7265d4c87d276c60590
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879571"
---
# <a name="nested-resiliency-for-storage-spaces-direct"></a>Geschachtelte resilienz für "direkte Speicherplätze"

> Gilt für: Windows Server 2019

Geschachtelte resilienz ist eine neue Funktion von ["direkte Speicherplätze"](storage-spaces-direct-overview.md) in Windows Server-2019, die es einem zwei-Server-Cluster ermöglicht standhalten Hardwareausfällen mehrere zur selben Zeit ohne Verlust der speicherverfügbarkeit, sodass Benutzer, apps und virtuelle Computer weiterhin ohne Unterbrechung ausgeführt werden. In diesem Thema wird erläutert, wie es funktioniert, bietet eine schrittweise Anleitung für den Einstieg und Antworten die am häufigsten gestellten Fragen.

## <a name="prerequisites"></a>Vorraussetzungen

### <a name="green-checkmark-iconmedianested-resiliencysupportedpng-consider-nested-resiliency-if"></a>![Grünes Häkchen-Symbol.](media/nested-resiliency/supported.png) Betrachten Sie geschachtelte resilienz, wenn:

- Ihren Cluster wird Windows Server-2019. und
- Der Cluster enthält genau 2 Server-Knoten

### <a name="red-x-iconmedianested-resiliencyunsupportedpng-you-cant-use-nested-resiliency-if"></a>![Rotes X-Symbol.](media/nested-resiliency/unsupported.png) Sie können keine geschachtelten resilienz verwenden, wenn:

- Ihren Cluster wird Windows Server 2016. oder
- Der Cluster enthält 3 oder mehr Server-Knoten

## <a name="why-nested-resiliency"></a>Warum geschachtelte resilienz

Volumes, die geschachtelte resilienz verwenden zu können **online und zugänglich bleiben, selbst wenn mehrere Hardwareausfällen zur gleichen Zeit**, im Gegensatz zum klassischen Bereitstellungsmodell [Wege-Spiegelung](storage-spaces-fault-tolerance.md) resilienz. Wenn zwei Laufwerke zur gleichen Zeit ausfallen, oder wenn ein Server ausfällt und ein Laufwerk ausfällt, bleiben Volumes, die geschachtelte resilienz verwenden z. B. online und zugänglich ist. Für hyperkonvergenten Infrastruktur erhöht dies die Betriebszeit für apps und virtuellen Computern; für Datei-Server-Workloads bedeutet dies, dass Benutzer einen unterbrechungsfreien Zugriff auf ihre Dateien nutzen.

![Speicherverfügbarkeit](media/nested-resiliency/storage-availability.png)

Der Nachteil besteht darin, geschachtelte resilienz hat **senken Kapazitätseffizienz als klassische-Wege-Spiegelung**, d. h. man etwas weniger Speicherplatz verwendet werden. Weitere Informationen finden Sie unter den [Kapazitätseffizienz](#capacity-efficiency) Abschnitt weiter unten.

## <a name="how-it-works"></a>Funktionsweise

### <a name="inspiration-raid-51"></a>Inspiration: RAID 5+1

RAID 5 + 1 ist eine eingerichtete Form von verteiltem Speicher resilienz, die hilfreiche Hintergrund verstehen geschachtelte Blick auf resilienz bereitstellen. RAID 5 + 1, auf jedem Server, lokale resilienz wird von RAID-5, bereitgestellt oder *einmaliges Parität*, um Schutz vor dem Verlust von einem einzelnen Laufwerk. Anschließend weitere resilienz von RAID-1, bereitgestellt wird oder *Wege-Spiegelung*, zwischen den beiden Servern zum Schutz gegen den Verlust von einem Server.

![RAID 5+1](media/nested-resiliency/raid-51.png)

### <a name="two-new-resiliency-options"></a>Zwei neue resilienzoptionen

"Direkte Speicherplätze" in Windows Server-2019 bietet zwei neue resilienzoptionen, die in der Software, ohne spezielle RAID-Hardware implementiert:

- **Geschachtelte-Wege-Spiegelung.** Klicken Sie auf jedem Server lokalen Stabilität wird durch zwei-Wege-Spiegelung bereitgestellt, und klicken Sie dann weitere resilienz vom Wege-Spiegelung zwischen den beiden Servern bereitgestellt wird. Es ist im Wesentlichen eine vier-Wege-Spiegelung, zwei Kopien auf jedem Server. Geschachtelte-Wege-Spiegelung bietet kompromisslosen Leistung: die Schreibvorgänge erfolgen, um alle Kopien, und Lesevorgänge, die aus einer Kopie stammen.

  ![Geschachtelte-Wege-Spiegelung](media/nested-resiliency/nested-two-way-mirror.png)

- **Geschachtelte Mirror-beschleunigte Parität.** Kombinieren geschachtelte Wege-Spiegelung, aus der oben genannten mit geschachtelten Parität. Auf jedem Server, lokale Flexibilität in Bezug auf die meisten Daten wird durch einzelne bereitgestellt [bitweise Parität arithmetische](storage-spaces-fault-tolerance.md#parity), mit Ausnahme der neuen aktuellen Schreibvorgänge, die zwei-Wege-Spiegelung verwenden. Klicken Sie dann weitere Flexibilität in Bezug auf alle Daten erfolgt über zwei-Wege-Spiegelung zwischen den Servern. Weitere Informationen zur Spiegelung wie beschleunigte Parität finden Sie unter [Mirror-beschleunigte Parität](https://docs.microsoft.com/windows-server/storage/refs/mirror-accelerated-parity).

  ![Geschachtelte Mirror-beschleunigte Parität](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="capacity-efficiency"></a>Kapazität Effizienz

Kapazität Effizienz ist das Verhältnis des freien Speicherplatzes auf [Volume Speicherbedarf](plan-volumes.md#choosing-the-size-of-volumes). Es wird beschrieben, die Kapazität Aufwand auf resilienz zurückzuführen, und richten sich nach der gewählten resilienz. Als einfaches Beispiel ist das Speichern von Daten ohne resilienz Auslastung von 100 % effizient (1 TB Daten dauert bis zu 1 TB physischen Speicherkapazität), ist bei der zwei-Wege-Spiegelung 50 % effizient (1 TB Daten dauert bis zu 2 TB physischen Speicherkapazität) aus.

- **Geschachtelte-Wege-Spiegelung** schreibt Sie vier Kopien aller Daten, zum Speichern von 1 TB an Daten, d. h. Sie 4 TB physischen Speicher benötigen. Aufgrund seiner Einfachheit attraktiv ist zwar geschachtelte Wege-Spiegelung des Kapazitätseffizienz von 25 % der niedrigste einer Option resilienz in "direkte Speicherplätze".

- **Geschachtelte Mirror-beschleunigte Parität** erzielt höhere Kapazitätseffizienz, ca. 35-40 %, von denen zwei Faktoren abhängt: die Anzahl der Kapazität Laufwerke in jedem Server, und die Kombination aus Spiegelung und Parität, die Sie, für das Volume angeben. Diese Tabelle bietet eine Suche für häufig verwendete Konfigurationen:

  | Kapazitätslaufwerke pro server | 10 %-Spiegelung | 20 % Spiegel | 30 % Spiegel |
  |----------------------------|------------|------------|------------|
  | 4                          | 35.7%      | 34.1%      | 32.6%      |
  | 5                          | 37.7%      | 35.7%      | 33.9%      |
  | 6                          | 39.1%      | 36.8%      | 34.7%      |
  | 7+                         | 40.0%      | 37.5%      | 35.3%      |

  > [!NOTE]
  > **Wenn Sie neugierig sind, ist hier ein Beispiel für die vollständige Mathematik.** Angenommen Sie, wir haben sechs Kapazität Laufwerke in jeder der beiden Server und ein 100-GB-Volume umfasst 10 GB der Spiegelung und Parität 90 GB erstellt werden soll. Server-Local-Wege-Spiegelung 50,0 % effizient, d. h. die 10 GB Spiegeln von Daten dauert 20 GB zum Speichern auf jedem Server. Auf beiden Servern gespiegelt wird, wird der gesamte Speicherbedarf 40 GB. Server-Local-einzelparität, wird in diesem Fall 5/6 = 83.3 % effizient, d. h. die 90 GB der Paritätsdaten dauert 108 GB auf jedem Server zu speichern. Auf beiden Servern gespiegelt wird, wird der gesamte Speicherbedarf 216 GB. Der gesamte Speicherbedarf ist also [(10 GB/50,0 %) + (90 GB / 83.3 %)] x 2 = 256 GB, für die 39.1 % insgesamt Kapazitätseffizienz.

Beachten Sie, dass die Kapazitätseffizienz klassischer zwei-Wege-Spiegelung (ca. 50 %) und geschachtelte Mirror-beschleunigte Parität (bis zu 40 %) sind nicht sehr unterschiedlich. Die etwas niedrigere Kapazitätseffizienz möglicherweise je nach Ihren Anforderungen lohnt die beachtliche speicherverfügbarkeit. Sie auswählen resilienz pro Volume, sodass Sie klassische-Wege-Spiegelung-Volumes auf demselben Cluster und die geschachtelten resilienz mischen können.

![Tradeoff](media/nested-resiliency/tradeoff.png)

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Sie können vertraute Speicher-Cmdlets in PowerShell verwenden, zum Erstellen von Volumes mit geschachtelten resilienz.

### <a name="step-1-create-storage-tier-templates"></a>Schritt 1: Erstellen von Vorlagen für Storage-Ebene

Erstellen Sie zunächst neue Speicher-Tier-Vorlagen, die mithilfe der `New-StorageTier` Cmdlet. Müssen Sie nur einmal tun, und klicken Sie dann jedes neues Volume, die, das Sie erstellen, diese Vorlage verweisen kann. Geben Sie die `-MediaType` Ihren Laufwerken, Kapazität und optional die `-FriendlyName` Ihrer Wahl. Ändern Sie die anderen Parameter nicht.

Wenn die Kapazität Festplattenlaufwerken (HDD) werden, starten Sie PowerShell als Administrator, und führen Sie aus:

```PowerShell 
# For mirror
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedMirror -ResiliencySettingName Mirror -MediaType HDD -NumberOfDataCopies 4

# For parity
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedParity -ResiliencySettingName Parity -MediaType HDD -NumberOfDataCopies 2 -PhysicalDiskRedundancy 1 -NumberOfGroups 1 -FaultDomainAwareness StorageScaleUnit -ColumnIsolation PhysicalDisk 
``` 

Wenn die Kapazität Solid State Drives (SSD) werden, legen Sie die `-MediaType` zu `SSD` stattdessen. Ändern Sie die anderen Parameter nicht.

> [!TIP]
> Überprüfen Sie die Ebenen wurde erfolgreich erstellt, mit `Get-StorageTier`.

### <a name="step-2-create-volumes"></a>Schritt 2: Erstellen von Volumes

Erstellen Sie dann auf neue Volumes, die mit der `New-Volume` Cmdlet.

#### <a name="nested-two-way-mirror"></a>Geschachtelte-Wege-Spiegelung

Um geschachtelte-Wege-Spiegelung zu verwenden, verweisen die `NestedMirror` Ebene Vorlage, und geben Sie die Größe. Zum Beispiel:

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume01 -StorageTierFriendlyNames NestedMirror -StorageTierSizes 500GB
```

#### <a name="nested-mirror-accelerated-parity"></a>Geschachtelte Mirror-beschleunigte Parität

Um geschachtelte Mirror-beschleunigte Parität verwenden, verweisen auf beide die `NestedMirror` und `NestedParity` Ebene Vorlagen, und geben Sie zwei Größen, eine für jeden Teil des Volumes (spiegeln zunächst Parität Sekunde). Z. B. um ein 500-GB-Volume zu erstellen, die 20 % geschachtelte-Wege-Spiegelung und 80 % ist geschachtelt Parität ausführen:

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume02 -StorageTierFriendlyNames NestedMirror, NestedParity -StorageTierSizes 100GB, 400GB
```

### <a name="step-3-continue-in-windows-admin-center"></a>Schritt 3: In Windows Admin Center fortfahren

Volumes, die geschachtelte resilienz zu verwenden, werden in [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) mit klar Bezeichnungen, wie im folgenden Screenshot dargestellt. Nachdem sie erstellt haben, können Sie verwalten und Überwachen mithilfe von Windows Admin Center wie alle anderen Volumes in "direkte Speicherplätze".

![](media/nested-resiliency/windows-admin-center.png)

### <a name="optional-extend-to-cache-drives"></a>Optional: Erweitern Sie auf Cachelaufwerke

Mit den Standardeinstellungen schützt geschachtelte resilienz gegen den Verlust von mehrere Laufwerke von Kapazität zur gleichen Zeit, oder einen Server und ein Laufwerk mit der Kapazität zur gleichen Zeit. Um diesen Schutz zu erweitern [Zwischenspeichern Laufwerke](understand-the-cache.md) verfügt über eine zusätzliche Aspekte berücksichtigt werden: Da Cachelaufwerken häufig lesen bereitstellen *und Schreiben von* Zwischenspeicherung für *mehrere* Laufwerke Kapazität , ist die einzige Möglichkeit, um sicherzustellen, dass Sie den Verlust von einem Cachelaufwerk tolerieren können, wenn der andere Server ausgefallen ist nicht einfach Schreibvorgänge zwischengespeichert, aber, die Leistung auswirkt.

Dieses Problem zu beheben, bietet "direkte Speicherplätze" die Option deaktiviert automatisch die Schreibcache bei einem Server in einem zwei-Server-Cluster nicht verfügbar ist, und klicken Sie dann erneut aktivieren Schreibcache, sobald der Server wieder verfügbar ist. Um routinemäßigen Neustarts ohne Auswirkungen auf die Leistung zu ermöglichen, Schreiben Sie, dass das caching deaktiviert ist nicht, bis der Server für 30 Minuten verfügbar ist.

Um dieses Verhalten festzulegen (optional) starten Sie PowerShell als Administrator, und führen Sie aus:

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.NestedResiliency.DisableWriteCacheOnNodeDown.Enabled" -Value "True"
```

Um ein festgelegter `True`, das Cacheverhalten ist:

| Situation                       | Das Verhalten des Caches                           | Tolerieren von Cache-Laufwerk verloren gehen kann? |
|---------------------------------|------------------------------------------|--------------------------------|
| Beide Server einrichten                 | Cachelese- und-Schreibvorgänge, volle Leistung | Ja                            |
| Server nicht verfügbar, die ersten 30 Minuten   | Cachelese- und-Schreibvorgänge, volle Leistung | Nein (vorübergehend)               |
| Nach der ersten 30 Minuten          | Vom Cache verarbeitete Lesevorgänge, die Leistung beeinträchtigt   | Ja                            |

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="can-i-convert-an-existing-volume-between-two-way-mirror-and-nested-resiliency"></a>Kann ich ein vorhandenes Volume Wege-Spiegelung und geschachtelte ausfallsicherheit konvertieren?

Nein, nicht Volumes zwischen resilienztypen konvertiert werden. Entscheiden Sie bei neuen Bereitstellungen auf Windows Server-2019 vorher die beste resilienztyp Ihren Anforderungen entspricht. Wenn Sie von Windows Server 2016 aktualisieren, können Sie neue Volumes mit geschachtelten resilienz erstellen, migrieren Sie Ihre Daten und löschen Sie dann auf die älteren Volumes.

### <a name="can-i-use-nested-resiliency-with-multiple-types-of-capacity-drives"></a>Kann ich geschachtelte resilienz mit mehreren Arten von Kapazität Laufwerke verwenden?

Ja, geben Sie einfach die `-MediaType` entsprechend jeder Ebene bei der [Schritt 1](#step-1-create-storage-tier-templates) oben. Z. B. mit NVMe, SSD und HDD im selben Cluster die NVMe bietet Cache während der letzten beiden Kapazität bereitstellen: Legen Sie die `NestedMirror` -Tarif in `-MediaType SSD` und `NestedParity` -Tarif in `-MediaType HDD`. Beachten Sie in diesem Fall, dass Kapazität paritätseffizienz hängt die Anzahl der HDD-Laufwerke nur benötigen Sie mindestens 4 davon pro Server.

### <a name="can-i-use-nested-resiliency-with-3-or-more-servers"></a>Kann ich geschachtelte resilienz mit 3 oder mehr Server verwenden?

Nein, nur verwenden Sie geschachtelter resilienz Wenn Ihr Cluster genau 2 Server enthält.

### <a name="how-many-drives-do-i-need-to-use-nested-resiliency"></a>Wie viele Laufwerke muss ich zur Verwendung von geschachtelten resilienz?

Die minimale Anzahl von Laufwerken, die für "direkte Speicherplätze" erforderlich sind, ist 4 Kapazität Laufwerke pro Serverknoten, plus 2 Cachelaufwerken pro Serverknoten (sofern vorhanden). Dies ist nicht von Windows Server 2016. Es gibt keine zusätzlichen Anforderungen für die geschachtelte resilienz, und die Empfehlung für Reservekapazität bleibt unverändert.

### <a name="does-nested-resiliency-change-how-drive-replacement-works"></a>Ändert geschachtelte resilienz die Funktionsweise von Laufwerk ersetzt?

Nein.

### <a name="does-nested-resiliency-change-how-server-node-replacement-works"></a>Ändert geschachtelte resilienz die Funktionsweise von Knoten ersetzen des Servers?

Nein. Um einen Serverknoten sowie deren Laufwerke zu ersetzen, führen Sie in dieser Reihenfolge:

1. Die Laufwerke auf dem Server für ausgehende abkoppeln
2. Fügen Sie den neuen Server, die Laufwerke, auf den cluster
3. Der Speicherpool wird ausgeglichen.
4. Entfernen Sie den Server für ausgehende sowie deren Laufwerke

Weitere Informationen finden Sie die [Entfernen von Servern](remove-servers.md) Thema.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Verstehen der Fehlertoleranz in "direkte Speicherplätze"](storage-spaces-fault-tolerance.md)
- [Planen von Volumes im "direkte Speicherplätze"](plan-volumes.md)
- [Erstellen Sie Volumes im "direkte Speicherplätze"](create-volumes.md)
