---
title: Die Anzahl der laufenden oder konfigurierten virtuellen Computer muss innerhalb unterstützter Grenzwerte liegen.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 9d3c4aa3-8416-46ec-a253-26dc98088d7b
ms.date: 8/16/2016
ms.openlocfilehash: f97ca9ad38bfdeee7e6d543a32f62f7a5344e700
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746825"
---
# <a name="the-number-of-running-or-configured-virtual-machines-must-be-within-supported-limits"></a>Die Anzahl der laufenden oder konfigurierten virtuellen Computer muss innerhalb unterstützter Grenzwerte liegen.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt Kursiv Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Es werden mehr virtuelle Computer ausgeführt oder konfiguriert, als unterstützt werden.*

## <a name="impact"></a>Auswirkung
*Microsoft unterstützt nicht die aktuelle Anzahl der virtuellen Computer, die auf diesem Server ausgeführt oder konfiguriert werden.*

## <a name="resolution"></a>Lösung
*Verschieben Sie mindestens einen virtuellen Computer auf einen anderen Server.*

Ausführliche Informationen zu den maximal unterstützten Konfigurationen für Hyper-v, wie z. b. die Anzahl der aktiven virtuellen Maschinen, finden Sie unter [Planen der Hyper-v-Skalierbarkeit in Windows Server 2016](../plan/plan-hyper-v-scalability-in-windows-server.md).

Wenn Sie einen virtuellen Computer auf einen anderen Server verschieben möchten, können Sie folgende Aktionen ausführen:

- Exportieren Sie die virtuelle Maschine vom aktuellen Server, und importieren Sie Sie dann wie unten beschrieben auf einen neuen Server.
- Führen Sie eine Live Migration durch:
    - Wenn dieser Server zu einem Failovercluster gehört, verwenden Sie die Tools, die mit dem Failoverclustering-Feature bereitgestellt werden. Anweisungen hierzu finden [Sie unter Live Migration, schnell Migration oder Verschieben einer virtuellen Maschine von Knoten zu Knoten](https://go.microsoft.com/fwlink/?LinkID=181519).
    - Wenn es sich um einen eigenständigen Server handelt, finden Sie weitere Informationen unter [Konfigurieren Livemigration und Migrieren von Virtual Machines ohne Failoverclustering](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134199(v=ws.11))

### <a name="to-export-a-virtual-machine"></a>So exportieren Sie einen virtuellen Computer

   > [!IMPORTANT]
   > Wenn der Hyper-v-Host, von dem aus Sie exportieren, zu einer Domäne gehört und Sie die exportierten Dateien an einem Remote Speicherort speichern möchten, muss der Hyper-v-Host für die eingeschränkte Delegierung konfiguriert werden. Bei einem Remote Speicherort kann es sich um einen freigegebenen Netzwerkordner oder einen Ordner auf dem Host handeln, in den Sie importieren. Die eingeschränkte Delegierung ermöglicht dem Computer Konto des Hyper-V-Hosts das Bereitstellen Delegierter Anmelde Informationen für den CIFS-Dienst (Common Internet File System) an den Remote Computer. Anweisungen zum Konfigurieren der eingeschränkten Delegierung finden Sie im Abschnitt befolgen der Anweisungen zum Exportieren und importieren unten.

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.

2.  Klicken Sie im Ergebnisbereich unter **Virtual Machines**mit der rechten Maustaste auf einen virtuellen Computer, und klicken Sie dann auf **exportieren**.

3.  Geben Sie im Dialogfeld **virtuellen Computer exportieren** einen Speicherort mit genügend freiem Speicherplatz zum Speichern aller Ressourcen des virtuellen Computers ein, oder navigieren Sie zu diesem. Wenn Sie einen virtuellen Computer exportieren, werden alle virtuellen Festplatten (VHD-Dateien oder vhdx-Dateien), Prüfpunkte (AVHD-Dateien) und gespeicherte Zustands Dateien, die der virtuellen Maschine zugeordnet sind, in den angegebenen Ordner kopiert.

4.  Klicken Sie auf **Exportieren**.

Importieren Sie die virtuellen Computer nach dem Exportieren der virtuellen Computer auf den anderen Server.

### <a name="to-import-a-virtual-machine-to-another-server"></a>So importieren Sie einen virtuellen Computer auf einen anderen Server

1.  Stellen Sie eine Verbindung mit dem Hyper-v-Server her, und öffnen Sie Hyper-v-Manager.

2.  Klicken Sie im Bereich **Aktion** auf **virtuellen Computer importieren**.

3.  Geben Sie im Dialogfeld **virtuellen Computer importieren** den Speicherort an, an den Sie die virtuelle Maschine exportiert haben. Wenn Sie diesen virtuellen Computer nicht erneut importieren möchten, belassen Sie die Import Einstellungen unverändert.

4.  Klicken Sie auf **Importieren**.

### <a name="to-configure-constrained-delegation"></a>So konfigurieren Sie eingeschränkte Delegierung

Um dieses Verfahren ausführen zu können, ist die Mitgliedschaft in der Gruppe **Domänen Administratoren** erforderlich.

1.  Öffnen Sie auf einem Computer, auf dem das Feature "Active Directory Domain Services Tools" installiert ist, in " **Verwaltung**" **Active Directory Benutzer und Computer**, und navigieren Sie zum Computer Konto des Computers, auf dem Hyper-V ausgeführt wird.

    > [!NOTE]
    > Wenn **Active Directory-Benutzer und -Computer** nicht angezeigt wird, installieren Sie die Tools für die Active Directory-Domänendienste. Anweisungen finden Sie unter [Installieren von Remoteserver-Verwaltungstools für AD DS](https://go.microsoft.com/fwlink/?LinkId=140463) ( https://go.microsoft.com/fwlink/?LinkId=140463) .

2.  Klicken Sie mit der rechten Maustaste auf das Computer Konto des Computers, auf dem Hyper-V ausgeführt wird, und klicken Sie auf **Eigenschaften**.

3.  Klicken Sie auf die Option **Computer bei Delegierungen angegebener Dienste auswählen** auf der Registerkarte **Delegierung**, und wählen Sie dann **Beliebiges Authentifizierungsprotokoll verwenden** aus.

4.  So gestatten Sie dem Hyper-V-Computer Konto das präsentieren von Delegierten Anmelde Informationen für den Remote Computer:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Klicken Sie im Dialogfeld **Dienste hinzufügen** auf **Benutzer oder Computer**, wählen Sie den Remote Computer aus, und klicken Sie dann auf **OK**.

    3.  Wählen Sie in der Liste **verfügbare Dienste** das **CIFS** -Protokoll (auch als SMB-Protokoll (Server Message Block) bezeichnet) aus, und klicken Sie dann auf **Hinzufügen**.