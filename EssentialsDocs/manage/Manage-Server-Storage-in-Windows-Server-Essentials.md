---
title: Verwalten von Serverspeicher in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 1836682e-c7bb-4dd5-a2b5-6ff032693574
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 0ee5669fc9ae6e1ee4e38065792d3da7611900a4
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87837729"
---
# <a name="manage-server-storage-in-windows-server-essentials"></a>Verwalten von Serverspeicher in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Mit Windows Server Essentials können Sie den gesamten Serverspeicher (einschließlich Festplatten und Speicherplätzen) über die Seiten **Festplatten** auf der Registerkarte **Speicher** des Dashboards verwalten.

 Die folgenden Abschnitte enthalten Informationen, die Ihnen beim Vergrößern des Serverspeichers, Verstehen und Verwenden von Speicherplätzen sowie beim Verwalten Ihrer Festplatten helfen:

-   [Verwalten von Festplatten mithilfe des Dashboards](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_1)

-   [Vergrößern des Speichers auf dem Server](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_2)

-   [Ausführen von Überprüfungen und Reparaturen auf Festplatten](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_Check)

-   [Formatieren von Festplatten](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_3)

-   [Hinzufügen einer neuen Festplatte](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4)

-   [Übersicht über Speicherplätze](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_5)

-   [Speicherplatz erstellen](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_6)

##  <a name="manage-hard-drives-using-the-dashboard"></a><a name="BKMK_1"></a>Verwalten von Festplatten mithilfe des Dashboards
 Windows Server Essentials ermöglicht Ihnen das Verwalten aller Festplatten, die mit dem Server verbunden sind, über das Dashboard. Auf der Registerkarte **Speicher** des Dashboards werden unter **Festplatten** alle Festplatten angezeigt, die auf dem Server zum Speichern von Daten und Serversicherungen verfügbar sind. Der Server überwacht den auf jeder Festplatte verfügbaren Speicherplatz und zeigt eine Warnung an, wenn der Festplattenspeicherplatz nahezu belegt ist. Auf der Registerkarte **Festplatten** werden die folgenden Informationen angezeigt:

- Der Name jeder Festplatte

- Die Kapazität jeder Festplatte

- Der belegte Speicherplatz auf jeder Festplatte

- Der freie Speicherplatz auf jeder Festplatte

- Der Status jeder Festplatte; ein leerer Status bedeutet, dass das Laufwerk ordnungsgemäß funktioniert

- Der Detailbereich, in dem alle Speicherstapelinformationen (für Speicherpool, Speicherplatz und Festplatte) angezeigt werden, wenn sich die ausgewählte Festplatte auf einem Speicherplatz (und nicht auf einem physikalischen Datenträger) befindet

  In der folgenden Tabelle sind die im Dashboard verfügbaren Aufgaben zur Festplattenverwaltung und deren Beschreibungen aufgelistet. Einige der Aufgaben werden nur angezeigt, wenn eine Festplatte ausgewählt ist.

### <a name="available-hard-drive-management-tasks"></a>Verfügbare Aufgaben zur Festplattenverwaltung

|Aufgabenname|BESCHREIBUNG|
|---------------|-----------------|
|**Festplatteneigenschaften anzeigen**|Öffnet die _harddrivename_-**Eigenschaften** Seite. Diese Aufgabe wird angezeigt, wenn die Festplatte ausgewählt ist. Die Registerkarte **Allgemein** der Seite "Eigenschaften von *Festplattenname*" enthält die folgenden zusätzlichen Aufgaben:<br /><br /> -   **Laufwerks Bereinigung**: ermöglicht das Bereinigen nicht verwendeter Dateien auf der Festplatte (diese Aufgabe ist nur in Windows Server Essentials verfügbar).<br />-   **Überprüfen und reparieren**: überprüft die Festplatte auf Dateisystem Fehler und versucht, erkannte Fehler automatisch zu reparieren.<br /><br /> Mithilfe der Registerkarte **Schatten Kopien** der**Eigenschaften** Seite _harddrivename_können Sie Schatten Kopien aktivieren. Diese Registerkarte zeigt auch den Zeitpunkt an, für den die nächste Ausführung von Schattenkopien geplant ist.|
|**Speicherplatz verwalten**|**Hinweis:** Für Windows Server Essentials wird diese Aufgabe nur angezeigt, wenn ein Speicherplatz vorhanden ist.<br /><br /> Öffnet die Systemsteuerung für **Speicherplätze**, von der aus Sie Speicherpools und Speicherplätze erstellen und verwalten können.|
|**Speicherplatz erstellen**|Öffnet den Assistenten zum Erstellen eines Speicherplatzes, der Ihnen die Verwendung einer oder mehrerer Festplatten zum Erhöhen der Kapazität eines Speicherpools ermöglicht.|
|**Speicherpoolkapazität erhöhen**|**Hinweis:** Diese Aufgabe ist nur sichtbar, wenn sich die ausgewählte Festplatte auf einem Speicherplatz befindet.<br /><br /> Öffnet den Assistenten zum Erhöhen der Kapazität eines Speicherpools, der Ihnen die Verwendung einer oder mehrerer Festplatten zum Erhöhen der Kapazität eines Speicherpools ermöglicht.|

##  <a name="increase-storage-on-the-server"></a><a name="BKMK_2"></a>Vergrößern des Speichers auf dem Server
 Um den Speicher auf dem Server zu vergrößern, können Sie eine zusätzliche interne Festplatte zum Server hinzufügen. Zum Hinzufügen der zusätzlichen internen Festplatte müssen Sie den Server herunterfahren, die interne Festplatte hinzufügen und dann den Server neu starten. Wenn die Festplatte an den SCSI-Controller angeschlossen ist, müssen Sie den Server nicht herunterfahren. In diesem Fall kann die Festplatte bei aktivem Server angeschlossen werden.

 Je nachdem, ob die hinzuzufügende Festplatte formatiert ist, führen Sie eine der folgenden Aktionen aus:

-   **Formatiert** Wenn die interne Festplatte mit NTFS oder Refs formatiert ist, weist Sie dem Server einen Laufwerk Buchstaben zu, und die Festplatte wird auf der Registerkarte **Festplatten** angezeigt. Sie können nun Server Ordner auf der neuen Festplatte erstellen oder verschieben.

-   **Nicht formatiert** Wenn die interne Festplatte nicht formatiert ist, wird die folgende Warnung angezeigt: Mindestens eine unformatierte Festplatte ist mit dem Server verbunden. Verwenden Sie das folgende Verfahren, um die Festplatte zu formatieren.

#### <a name="to-format-the-hard-disk"></a>Formatieren der Festplatte

1.  Öffnen Sie das Dashboard.

2.  Klicken Sie im Navigationsbereich auf das Warnsymbol, um die Meldungs Anzeige in Windows Server Essentials **oder die Register** Karte System **Überwachung** in Windows Server Essentials zu starten.

3.  Klicken Sie in der**** Meldungsanzeige oder auf der Registerkarte **Systemüberwachung** auf die Warnung, und klicken Sie dann im Aufgabenbereich auf **Problem behandeln**.

4.  Befolgen Sie die Anweisungen, um den Assistenten zum Hinzufügen einer neuen Festplatte abzuschließen.

###  <a name="to-clean-up-the-hard-drive"></a><a name="BKMK_Clean"></a>So bereinigen Sie die Festplatte

1.  Öffnen Sie das Dashboard.

2.  Klicken Sie im Navigationsbereich auf **Speicher** und dann auf **Festplatten**.

3.  Wählen Sie im Abschnitt **Festplatten** den Laufwerkbuchstaben aus, der der neu hinzugefügten Festplatte zugewiesen wurde, und klicken Sie im Aufgabenbereich auf **Festplatteneigenschaften anzeigen**.

4.  Klicken Sie in **<DriveLetter- \> Eigenschaften**auf der Registerkarte **Allgemein** auf **Laufwerks Bereinigung**.

##  <a name="perform-checks-and-repairs-on-hard-drives"></a><a name="BKMK_Check"></a>Ausführen von Überprüfungen und Reparaturen auf Festplatten
 Mit dem Überprüfungs- und Reparaturprozess für Festplatten wird die Integrität des auf den Festplatten gespeicherten Dateisystems sichergestellt. Es wird ein **chkdsk**-Prozess auf dem Volume ausgeführt, auf dem die Sicherungsdateien gespeichert sind. Die folgende Warnung kann durch Ausführen einer Überprüfung und Reparatur auf den Festplatten behoben werden:

-   Mindestens eine Festplatte in der Serversicherung muss überprüft werden.

#### <a name="to-check-and-repair-hard-drives"></a>Überprüfen und Reparieren von Laufwerken

1.  Öffnen Sie das Dashboard.

2.  Klicken Sie auf **Serverordner und Festplatten** und dann auf **Festplatten**.

3.  Wählen Sie die Festplatte aus, für die der Fehler angezeigt wird, und wählen Sie dann **Festplatteneigenschaften anzeigen** aus.

4.  Klicken Sie auf der Registerkarte **Überprüfen und reparieren** auf **Überprüfen und reparieren**.

##  <a name="format-hard-drives"></a><a name="BKMK_3"></a>Formatieren von Festplatten
 Wenn eine unformatierte interne Festplatte auf dem Server erkannt wird, wird der Benutzer durch eine Integritätswarnung durch den Formatierungsprozess geführt. Der Assistent zum Hinzufügen einer neuen Festplatte führt Sie durch das Formatieren der Festplatte und ermöglicht Ihnen das Konfigurieren der Festplatte auf eine der folgenden Arten:

1.  Festplatte formatieren und automatisch ein Laufwerk darauf erstellen. Wenn Sie diese Option auswählen, haben Sie nach Abschluss des Assistenten eine logische Festplatte erstellt, die mit dem NTFS-Dateisystem formatiert ist.

2.  Die Festplatte formatieren und für die Serversicherung einrichten. Wenn Sie diese Option auswählen, wird der Assistent zum Einrichten der Serversicherung gestartet und führt Sie durch die Serversicherungskonfiguration.

3.  Wenn kein Speicherplatz vorhanden ist, verwenden Sie die neue Festplatte, um einen Speicherplatz zu erstellen. Sie benötigen mindestens zwei Festplatten, um einen Speicherplatz zu erstellen.

4.  Wenn bereits ein Speicherplatz vorhanden ist, verwenden Sie die neue Festplatte, um die Kapazität eines Speicherpools zu erhöhen. Diese Option wird nur angezeigt, wenn bereits ein Speicherplatz auf dem Server erstellt ist. Wenn Sie diese Option auswählen, fügt der Assistent diese Festplatte zum Speicherpool hinzu.

##  <a name="add-a-new-hard-drive"></a><a name="BKMK_4"></a>Neue Festplatte hinzufügen
 Wenn Sie eine neue Festplatte an einen Server mit Windows Server Essentials anschließen, haben Sie folgende Möglichkeiten:

-   [Verwenden der neuen Festplatte zum Speichern von Serverordnern](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4a)

-   [Verwenden der neuen Festplatte zum Speichern von Serversicherungen](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4b)

-   [Verwenden der neuen Festplatte zum Erhöhen der Speicherpoolkapazität](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c)

###  <a name="use-the-new-hard-drive-to-store-server-folders"></a><a name="BKMK_4a"></a>Verwenden der neuen Festplatte zum Speichern von Server Ordnern
 Wenn Sie die neue Festplatte zum Speichern von Serverordnern verwenden möchten, können Sie einen neuen Serverordner zur Festplatte hinzufügen oder einen vorhandenen Serverordner auf die Festplatte verschieben.

##### <a name="to-store-server-folders"></a>Speichern von Serverordnern

1. Öffnen Sie das Dashboard.

2. Klicken Sie auf die Registerkarte **SPEICHER** und anschließend auf **Serverordner**.

3. Führen Sie im Bereich **Tasks für Serverordner** einen der folgenden Schritte aus:

   1.  Zum Hinzufügen eines Serverordners klicken Sie auf **Ordner hinzufügen**.

   2.  Zum Verschieben eines Serverordners wählen Sie den Ordner aus, den Sie auf die neue Festplatte verschieben möchten, und klicken Sie dann auf **Ordner verschieben**.

   > [!NOTE]
   >  Wenn Sie die Festplatte suchen und als Speicherort des Server Ordners auswählen, ohne einen Ordner zu erstellen, wird die folgende Fehlermeldung angezeigt: **ein Stammverzeichnis (z \\ . b. C:, D: \\ ) kann nicht als Server Ordner hinzugefügt werden. Erstellen Sie einen neuen Ordner, oder wählen Sie einen vorhandenen Ordner unter dem Stammverzeichnis aus, und wiederholen Sie dann den**Vorgang. Um diesen Fehler zu beheben, erstellen Sie einen neuen Ordner auf der neu hinzugefügten Festplatte, und wählen Sie dann den neuen Ordner als Speicherort für Serverordner aus.

4. Folgen Sie den Anweisungen, um den Assistenten zu beenden.

   Weitere Informationen zum Verschieben von Serverordnern finden Sie unter [Add or move a server folder](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).

###  <a name="use-the-new-hard-drive-to-store-server-backups"></a><a name="BKMK_4b"></a>Verwenden der neuen Festplatte zum Speichern von Server Sicherungen
 Sie können die neu hinzugefügte Festplatte zum Speichern von Serversicherungen verwenden.

##### <a name="to-store-server-backups"></a>Speichern von Serversicherungen

1. Öffnen Sie das Dashboard.

2. Klicken Sie auf die Registerkarte **Geräte**, wählen Sie den Server aus dem Listenbereich aus, und führen Sie dann im Aufgabenbereich eine der folgenden Aktionen aus:

   1. Wenn die Serversicherung nicht auf dem Server konfiguriert ist, klicken Sie auf **Serversicherung einrichten**.

   2. Wenn die Serversicherung auf dem Server konfiguriert ist, klicken Sie auf **Serversicherung anpassen**.

      Der Assistent zum Einrichten der Serversicherung wird angezeigt.

3. Wählen Sie auf der Seite **Sicherungsziel auswählen** die neue Festplatte als Sicherungsziel aus.

4. Folgen Sie den Anweisungen, um den Assistenten zu beenden.

###  <a name="use-the-new-hard-drive-to-increase-storage-pool-capacity"></a><a name="BKMK_4c"></a>Verwenden der neuen Festplatte zum Erhöhen der Speicherpool Kapazität
 Wenn die Speicherpoolkapazität gering ist, wird Ihnen eine Warnung angezeigt, die besagt, dass Sie die Speicherpoolkapazität erhöhen können, indem Sie mithilfe des Assistenten zum Erhöhen der Kapazität eines Speicherpools eine neue Festplatte zum Speicherpool hinzufügen.

> [!NOTE]
>  Sie können dieses Verfahren nur ausführen, wenn Sie einen Speicherpool auf dem Server erstellt haben.

##### <a name="to-increase-storage-pool-capacity"></a>Erhöhen der Speicherpoolkapazität

1.  Öffnen Sie das Dashboard.

2.  Klicken Sie auf die Registerkarte **Speicher** und anschließend auf **Festplatten**.

3.  Wählen Sie die Festplatte mit geringer Kapazität aus.

4.  Wählen Sie im Aufgabenbereich die Option **Speicherpoolkapazität erhöhen** aus. Der Assistent zum Erhöhen der Kapazität eines Speicherpools wird angezeigt.

5.  Folgen Sie den Anweisungen, um den Assistenten zu beenden.

##  <a name="storage-spaces-overview"></a><a name="BKMK_5"></a>Übersicht über Speicherplätze
 Mithilfe von Speicherplätzen können Sie Datenträger in einem Speicherpool zu Gruppen zusammenfassen. Dann können Sie Poolkapazität zum Erstellen von Speicherplätzen verwenden. Speicherplätze sind virtuelle Laufwerke, die auf der Registerkarte **Festplatten** des Dashboards angezeigt werden. Sie können Speicherplätze wie jedes andere Laufwerk verwenden, sodass Sie problemlos mit Dateien arbeiten können. Wenn die Poolkapazität nur noch gering ist, können Sie große Speicherplätze erstellen und weitere Laufwerke zum Speicherpool hinzufügen. Wenn Sie über zwei oder mehr Datenträger im Speicherpool verfügen, können Sie Speicherplätze mit einer zwei-Wege-Spiegelung erstellen, die nicht von einem Laufwerks Ausfall betroffen ist? oder sogar den Ausfall von zwei Laufwerken?, wenn Sie einen drei-Wege-Spiegelungs Speicherplatz erstellen.

 Zum Erstellen eines Speicherplatzes benötigen Sie lediglich ein oder mehrere Laufwerke zusätzlich zu dem, auf dem Windows installiert ist. Bei diesen Laufwerken kann es sich um interne oder externe Festplatten oder Festkörperlaufwerke handeln. Sie können eine Vielzahl von Laufwerkstypen für Speicherplätze verwenden, einschließlich USB-, SATA- und SAS-Laufwerke.

> [!NOTE]
>  Wenn Sie Speicherplätze auf einem Server konfigurieren, auf dem Windows Server Essentials ausgeführt wird, können Sie mit der Option **Daten bereinigen** keine Werkseinstellungen zurücksetzen. Um dieses Problem zu umgehen, entfernen Sie zunächst die Speicherplätze, und führen Sie dann eine Wiederherstellung der Herstellerstandards mit der Option **Daten bereinigen** aus.

 Weitere Informationen zu Speicherplätzen finden Sie unter [Häufig gestellte Fragen zu Speicherplätzen](/windows-server/storage/storage-spaces/storage-spaces-direct-faq).

##  <a name="create-a-storage-space"></a><a name="BKMK_6"></a>Erstellen eines Speicherplatzes
 Wenn Sie mit Speicherplätzen auf einem Server arbeiten möchten, müssen die folgenden Mindestanforderungen erfüllt sein:

-   Der Server mit Windows Server Essentials muss mit zusätzlichen physischen Laufwerken (nicht nur dem Startlaufwerk) verbunden sein, auf den Laufwerken dürfen keine Volumes gehostet sein und sie müssen eine Mindestkapazität von 10 GB aufweisen. Zum Erstellen eines Speicherpools ist ein physisches Laufwerk erforderlich; mindestens zwei physische Laufwerke werden benötigt, um einen robusten Spiegelspeicherplatz zu erstellen.

-   Mindestens zwei physische Laufwerke sind erforderlich, um einen Speicherplatz mit Resilienz durch Parität oder Zwei-Wege-Spiegelung zu erstellen.

> [!NOTE]
>  Wenn Sie Speicherplätze auf einem Server konfigurieren, auf dem Windows Server Essentials ausgeführt wird, können Sie mit der Option **Daten bereinigen** keine Werkseinstellungen zurücksetzen. Um dieses Problem zu umgehen, entfernen Sie zunächst die Speicherplätze, und führen Sie dann eine Wiederherstellung der Herstellerstandards mit der Option **Daten bereinigen** aus.

#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>So erstellen Sie einen Speicherplatz in Windows Server Essentials

1. Fügen Sie alle Laufwerke, die Sie mithilfe von Speicherplätzen in einer Gruppe zusammenfassen möchten, zum Server mit Windows Server Essentials hinzu oder stellen Sie eine Verbindung her.

2. Klicken Sie auf dem Dashboard auf **Erweitert: Speicherplatz verwalten**.

3. Klicken Sie auf **Neuen Pool und Speicherplatz erstellen**.

4. Wählen Sie die Laufwerke aus, die Sie zu dem neuen Speicherplatz hinzufügen möchten, und klicken Sie dann auf **Pool erstellen**.

5. Weisen Sie dem Laufwerk einen Namen und einen Buchstaben zu, und wählen Sie dann ein Layout. Mithilfe von **Zwei-Wege-Spiegelung**, **Drei-Wege-Spiegelung** und **Parität** können Sie die Dateien am Speicherplatz bei Laufwerkfehlern schützen.

6. Geben Sie die maximale Größe an, die der Speicherplatz erreichen kann, und klicken Sie dann auf **Speicherplatz erstellen**.

   In Windows Server Essentials können Sie einen bidirektionalen gespiegelten Speicherplatz erstellen, indem Sie den Assistenten zum Erstellen eines Speicherplatzes aus dem Dashboard verwenden.

#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>So erstellen Sie einen Speicherplatz in Windows Server Essentials

1. Fügen Sie alle Laufwerke, die Sie mithilfe von Speicherplätzen in einer Gruppe zusammenfassen möchten, zum Server mit Windows Server Essentials hinzu oder stellen Sie eine Verbindung her.

2. Klicken Sie auf dem Dashboard auf **Speicherplatz verwalten**. Der Assistent zum Erstellen eines Speicherplatzes wird angezeigt.

3. Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

   Informationen zum Erhöhen der Speicherpoolkapazität finden Sie unter [Use the new hard drive to increase storage pool capacity](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c).

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)