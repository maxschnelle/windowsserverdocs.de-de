---
title: Verwalten von Serverspeicher in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1836682e-c7bb-4dd5-a2b5-6ff032693574
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e0f65dfd25afbd584764d33904ba82e4da4c5443
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-server-storage-in-windows-server-essentials"></a>Verwalten von Serverspeicher in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
   
 Windows Server Essentials können Sie zum Verwalten der gesamten Serverspeicher (einschließlich Festplatten und Speicherplätzen) aus der **Festplatten** Seiten, auf die **Speicher** Dashboard-Registerkarte.  
  
 Die folgenden Abschnitte enthalten Informationen, die Ihnen das Vergrößern des Serverspeichers, verstehen und Verwenden von Speicherplätzen und Verwalten Ihrer Festplatten helfen:  
  
-   [Verwalten von Festplatten mithilfe des Dashboards](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Vergrößern des Speichers auf dem server](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Ausführen von Überprüfungen und Reparaturen auf Festplatten](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_Check)  
  
-   [Formatieren von Festplatten](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Fügen Sie eine neue Festplatte hinzu](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Speicherplätze – Übersicht](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Erstellen eines Speicherplatzes](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_6)  
  
##  <a name="BKMK_1"></a>Verwalten von Festplatten mithilfe des Dashboards  
 Windows Server Essentials können Sie alle Festplatten verwalten, die mit dem Server über das Dashboard verbunden sind. Auf dem Dashboard **Speicher** Registerkarte **Festplatten** zeigt alle Festplatten, die auf dem Server zum Speichern von Daten und serversicherungen verfügbar sind. Der Server überwacht den auf jeder Festplatte verfügbaren Speicherplatz und zeigt eine Warnung, wenn Festplatten-Speicherplatz gering ist. Die **Festplatten** Registerkarte die folgenden Informationen angezeigt:  
  
-   Der Name jeder Festplatte  
  
-   Die Kapazität jeder Festplatte  
  
-   Die Menge des belegten Speicherplatzes auf jeder Festplatte  
  
-   Die Menge an freiem Speicherplatz auf jeder Festplatte  
  
-   Der Status jeder Festplatte; ein leerer Status bedeutet, dass das Laufwerk ordnungsgemäß funktioniert  
  
-   Im Detailbereich, in dem alle speicherstapelinformationen (für Speicherpool, Speicherplatz und Festplatte) angezeigt, wenn die ausgewählte Festplatte auf einem Speicherplatz (anstelle eines physischen Datenträgers) befindet  
  
 Die folgende Tabelle enthält die Aufgaben zur festplattenverwaltung, die in das Dashboard und deren Beschreibungen verfügbar sind. Einige Aufgaben werden nur angezeigt, wenn eine Festplatte ausgewählt ist.  
  
### <a name="available-hard-drive-management-tasks"></a>Verfügbare Aufgaben zur festplattenverwaltung  
  
|Den Namen der Aufgabe|Beschreibung|  
|---------------|-----------------|  
|**Festplatteneigenschaften anzeigen**|Öffnet die *Festplattenname***Eigenschaften** Seite. Diese Aufgabe wird angezeigt, wenn die Festplatte ausgewählt ist. Die **allgemeine** auf der Registerkarte der *Festplattenname* Eigenschaftenseite enthält die folgenden zusätzlichen Aufgaben:<br /><br /> -   **Bereinigung**: ermöglicht Ihnen das Bereinigen nicht verwendeter Dateien auf der Festplatte (diese Aufgabe ist nur verfügbar in Windows Server Essentials).<br />-   **Überprüfen und reparieren**: überprüft die Festplatte auf Dateisystemfehler und versucht, erkannte Fehler automatisch zu reparieren.<br /><br /> Die **Schattenkopien** auf der Registerkarte der *Festplattenname***Eigenschaften** Seite können Sie Schattenkopien aktivieren. Diese Registerkarte zeigt auch das nächste Mal die Schattenkopien geplant ist.|  
|**Verwalten von Speicherplätzen**|**Hinweis:** für Windows Server Essentials dieser Aufgabe wird nur angezeigt, wenn bereits ein Speicherplatz vorhanden ist.<br /><br /> Öffnet die **Speicherplätze** Systemsteuerung, von dem Sie erstellen und Verwalten von Speicherpools und Speicherplätze.|  
|**Erstellen eines Speicherplatzes**|Öffnet den Speicher Speicherplatz Assistenten zum Erstellen eines, dem Sie eine oder mehrere Festplatten zum Erhöhen der Kapazität eines Speicherpools verwenden können.|  
|**Erhöhen der Speicherpoolkapazität**|**Hinweis:** diese Aufgabe ist nur sichtbar, wenn die ausgewählte Festplatte auf einem Speicherplatz befindet.<br /><br /> Öffnet das Erhöhen der Kapazität eines Storage Pool-Assistenten, können Sie eine oder mehrere Festplatten zum Erhöhen der Kapazität eines Speicherpools verwenden.|  
  
##  <a name="BKMK_2"></a>Vergrößern des Speichers auf dem server  
 Um den Speicher auf dem Server zu erhöhen, können Sie eine zusätzliche interne Festplatte zum Server hinzufügen. Um die zusätzliche interne Festplatte hinzufügen möchten, müssen Sie Herunterfahren des Servers, die interne Festplatte hinzufügen und dann den Server neu starten. Sie müssen nicht den Server Herunterfahren, wenn die Festplatte an den SCSI-Controller angeschlossen ist. In diesem Fall kann die Festplatte angeschlossen werden während der Server ausgeführt wird.  
  
 Je nachdem, ob die Festplatte hinzugefügt werden formatiert ist führen Sie eine der folgenden:  
  
-   **Formatiert** Wenn die interne Festplatte mit NTFS oder ReFS formatiert ist, der Server einen Laufwerkbuchstaben weist und die Festplatte wird auf der **Festplatten** Registerkarte. Sie können jetzt erstellen oder Verschieben von Serverordnern auf der neuen Festplatte.  
  
-   **Nicht formatiert** , wenn die interne Festplatte nicht formatiert ist, wird die folgende Warnung angezeigt: mindestens eine unformatierte Festplatte mit dem Server verbunden sind. Verwenden Sie das folgende Verfahren zum Formatieren der Festplatte.  
  
#### <a name="to-format-the-hard-disk"></a>Zum Formatieren der Festplatte  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf das Warnungssymbol zum Starten der **Alert Viewer** in Windows Server Essentials oder die **Überwachung der Integrität** Registerkarte in Windows Server Essentials.  
  
3.  In der **Alert Viewer** oder **Überwachung der Integrität** Registerkarte auf die Warnung, und klicken Sie dann im Aufgabenbereich auf **Problem behandeln**.  
  
4.  Folgen Sie den Anweisungen zum Hinzufügen eines neuen Hard Drive-Assistenten abschließen.  
  
###  <a name="BKMK_Clean"></a>Bereinigen der Festplatte  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf **Speicher**, und klicken Sie dann auf **Festplatten**.  
  
3.  In der **Festplatten** Abschnitt, wählen Sie den Laufwerkbuchstaben an, die auf die neu hinzugefügten Festplatte, und klicken Sie im Aufgabenbereich zugewiesen wurde, klicken Sie auf **Festplatteneigenschaften anzeigen**.  
  
4.  In **< Driveletter\ > Eigenschaften**auf die **allgemeine** auf **Bereinigung**.  
  
##  <a name="BKMK_Check"></a>Ausführen von Überprüfungen und Reparaturen auf Festplatten  
 Die Festplatten überprüfen und Reparieren Prozess prüft die Integrität des Dateisystems auf den Festplatten gespeichert. Ausführung einer **Chkdsk** Prozess auf dem Datenträger, die in die Sicherungsdateien gespeichert sind. Die folgende Warnung Problem aufgelöst werden kann, durch Ausführen einer Überprüfung und Reparatur auf den Festplatten:  
  
-   Eine oder mehrere Festplatten in Server-Sicherung müssen überprüft werden.  
  
#### <a name="to-check-and-repair-hard-drives"></a>Um zu überprüfen und Reparieren von Laufwerken  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Serverordner und Festplatten**, und klicken Sie dann auf **Festplatten**.  
  
3.  Wählen Sie die Festplatte, die der Fehler angezeigt wird, und wählen Sie dann **Festplatteneigenschaften anzeigen**.  
  
4.  Auf der **überprüfen und reparieren** auf **überprüfen und reparieren**.  
  
##  <a name="BKMK_3"></a>Formatieren von Festplatten  
 Wenn eine unformatierte interne Festplatte auf dem Server erkannt wird, führt eine integritätswarnung den Benutzer durch den Prozess der formatieren. Hinzufügen eines neuen Festplatte Laufwerk Assistenten führt Sie durch die Formatierung der Festplatte und können Sie die Festplatte in einem der folgenden Methoden konfigurieren:  
  
1.  Die Festplatte formatieren und automatisch ein Laufwerk darauf erstellen. Wenn Sie diese Option auswählen, wenn der Assistent abgeschlossen ist, wird eine logische Festplatte mit dem NTFS-Dateisystem formatierte erstellt.  
  
2.  Die Festplatte formatieren und für die Server-Sicherung einrichten. Wenn Sie diese Option auswählen, der Server-Sicherung-Assistent wird gestartet und führt Sie durch die Serversicherungskonfiguration.  
  
3.  Wenn eine Speicherplatz Datenspeicher-t vorhanden sind, verwenden Sie die neue Festplatte zum Erstellen eines Speicherplatzes. Sie benötigen mindestens zwei Festplatten, um einen Speicherplatz zu erstellen.  
  
4.  Wenn bereits ein Speicherplatz vorhanden ist, verwenden Sie die neue Festplatte zum Erhöhen der Kapazität eines Speicherpools. Diese Option wird nur angezeigt, wenn ein Speicherplatz auf dem Server erstellt ist. Wenn Sie diese Option auswählen, wird der Assistent diese Festplatte zum Speicherpool hinzufügen.  
  
##  <a name="BKMK_4"></a>Fügen Sie eine neue Festplatte hinzu  
 Wenn Sie eine neue Festplatte an einen Server mit Windows Server Essentials anschließen, können Sie folgende Schritte ausführen:  
  
-   [Verwenden Sie die neue Festplatte zum Speichern von Serverordnern](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4a)  
  
-   [Verwenden Sie die neue Festplatte zum Speichern von serversicherungen](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4b)  
  
-   [Verwenden Sie die neue Festplatte zum Erhöhen der Speicherpoolkapazität](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c)  
  
###  <a name="BKMK_4a"></a>Verwenden Sie die neue Festplatte zum Speichern von Serverordnern  
 Verwendung die neue Festplatte zum Speichern von Serverordnern können Sie einen neuen Serverordner auf der Festplatte hinzufügen oder verschieben einen vorhandenen Serverordner auf der Festplatte.  
  
##### <a name="to-store-server-folders"></a>Zum Speichern von Serverordnern  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf die **Speicher** Registerkarte, und klicken Sie dann auf **Serverordner**.  
  
3.  In der **Tasks für Serverordner** Bereich, führen Sie einen der folgenden:  
  
    1.  Klicken Sie auf einen Serverordner hinzufügen, **fügen Sie einen Ordner**.  
  
    2.  Um einen Ordner zu verschieben, wählen Sie den Ordner, die Sie verwenden möchten, auf die neue Festplatte verschieben, und klicken Sie dann auf **Verschieben eines Serverordners**.  
  
    > [!NOTE]
    >  Wenn Sie auf die Festplatte durchsuchen und wählen Sie ihn als Speicherort für Serverordner, ohne einen Ordner zu erstellen, wird die folgende Fehlermeldung angezeigt: **ein Stammverzeichnis (z. B. C:\\, D:\\) kann nicht als Serverordner hinzugefügt werden. Erstellen Sie einen neuen Ordner oder wählen Sie eine vorhandene unter dem Stammverzeichnis und versuchen Sie es dann erneut**. Um diesen Fehler zu beheben, erstellen Sie einen neuen Ordner in der neu hinzugefügten Festplatte, und wählen Sie dann den neuen Ordner als Speicherort für Serverordner.  
  
4.  Führen Sie die Anweisungen, um den Assistenten zu beenden.  
  
 Weitere Informationen zum Verschieben von Serverordnern finden Sie unter [hinzufügen oder Verschieben eines Serverordners](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).  
  
###  <a name="BKMK_4b"></a>Verwenden Sie die neue Festplatte zum Speichern von serversicherungen  
 Sie können die neu hinzugefügte Festplatte zum Speichern von serversicherungen verwenden.  
  
##### <a name="to-store-server-backups"></a>Zum Speichern von serversicherungen  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf die **Geräte** Registerkarte, wählen Sie den Server aus dem Listenbereich aus, und führen Sie dann im Aufgabenbereich eine der folgenden:  
  
    1.  Wenn der Server-Sicherung nicht auf dem Server konfiguriert ist, klicken Sie auf **Serversicherung einrichten**.  
  
    2.  Wenn der Server-Sicherung auf dem Server konfiguriert ist, klicken Sie auf **Anpassen der Serversicherung**.  
  
     Der Server-Sicherung-Assistent wird angezeigt.  
  
3.  In der **Sicherungsziel auswählen** Seite, die neue Festplatte als Sicherungsziel auswählen.  
  
4.  Führen Sie die Anweisungen, um den Assistenten zu beenden.  
  
###  <a name="BKMK_4c"></a>Verwenden Sie die neue Festplatte zum Erhöhen der Speicherpoolkapazität  
 Wenn die Speicherpoolkapazität gering ist, erhalten Sie eine Warnung, die besagt, dass Sie die Speicherpoolkapazität erhöhen können, durch das Hinzufügen einer neuen Festplatte zum Speicherpool mit dem das Erhöhen der Kapazität eines Storage Pool-Assistenten.  
  
> [!NOTE]
>  Sie können dieses Verfahren ausführen, nur dann, wenn Sie einen Speicherpool auf dem Server erstellt.  
  
##### <a name="to-increase-storage-pool-capacity"></a>Erhöhen der Speicherpoolkapazität  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf die **Speicher** Registerkarte, und klicken Sie dann auf **Festplatten**.  
  
3.  Wählen Sie das Laufwerk, das ein geringer Kapazität.  
  
4.  Wählen Sie im Aufgabenbereich **Speicherpoolkapazität**. Das Erhöhen der Kapazität ein Speicher-Pool-Assistent wird angezeigt.  
  
5.  Führen Sie die Anweisungen, um den Assistenten zu beenden.  
  
##  <a name="BKMK_5"></a>Speicherplätze – Übersicht  
 Mit Speicherplätzen können Sie gruppieren Datenträger zusammen in einem Speicherpool. Sie können dann Pool-Kapazität verwenden, zum Erstellen von Speicherplätzen. Speicherplätze sind virtuelle Laufwerke, die auf die **Festplatten** Dashboard-Registerkarte. Können Speicherplätze wie jedes andere Laufwerk, sodass es einfach mit Dateien arbeiten. Wenn der Pool-Kapazität erschöpft ist, können Sie große Speicherplätze erstellen und weitere Laufwerke zum Speicherpool hinzufügen. Wenn Sie zwei oder mehr Datenträger im Speicherpool verfügen, können Sie Speicherplätze erstellen, durch eine zwei-Wege-Spiegelung, die von einem Laufwerksfehler nicht beeinträchtigt sind? oder sogar den Ausfall von zwei Laufwerken? Wenn Sie einen drei-Wege-spiegelspeicherplatz erstellen.  
  
 Um einen Speicherplatz zu erstellen, müssen Sie, lediglich ein oder mehrere zusätzliche Laufwerke darüber hinaus auf das Laufwerk, auf dem Windows installiert ist. Diese Laufwerke können interne oder externe Festplatten und solid State-Laufwerke werden. Sie können eine Vielzahl von Laufwerkstypen mit Speicherplätzen, einschließlich USB-, SATA- und SAS-Laufwerke verwenden.  
  
> [!NOTE]
>  Wenn Sie Speicherplätze auf einem Server unter Windows Server Essentials konfigurieren, ist nicht möglich Herstellerstandards mit der **Daten bereinigen** Option. Dieses Problem zu umgehen, entfernen Sie zuerst mithilfe von Speicherplätzen und führen Sie dann die Herstellerstandards mit ist die **Daten bereinigen** Option.  
  
 Weitere Informationen zu Speicherplätzen finden Sie unter [Storage Spaces häufig gestellte Fragen (FAQ)](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).  
  
##  <a name="BKMK_6"></a>Erstellen eines Speicherplatzes  
 Um die Arbeit mit Speicherplätzen auf Server beginnen, müssen die folgenden Mindestanforderungen erfüllt sein:  
  
-   Der Server mit Windows Server Essentials muss mit zusätzlichen physischen Laufwerken (nicht nur dem Startlaufwerk) verbunden sein, die Laufwerke müssen keine Volumes gehostet und müssen eine Mindestkapazität von 10 GB haben. Erstellen eines Speicherpools ist ein physisches Laufwerk erforderlich; mindestens zwei physische Laufwerke ist erforderlich, um einen robusten spiegelspeicherplatz zu erstellen.  
  
-   Mindestens zwei physische Laufwerke sind erforderlich, um einen Speicherplatz mit resilienz durch Parität oder zwei-Wege-Spiegelung zu erstellen.  
  
> [!NOTE]
>  Wenn Sie Speicherplätze auf einem Server unter Windows Server Essentials konfigurieren, ist nicht möglich Herstellerstandards mit der **Daten bereinigen** Option. Dieses Problem zu umgehen, entfernen Sie zuerst mithilfe von Speicherplätzen und führen Sie dann die Herstellerstandards mit ist die **Daten bereinigen** Option.  
  
#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>Zum Erstellen eines Speicherplatzes in Windows Server Essentials  
  
1.  Fügen Sie hinzu, oder Verbinden Sie die Laufwerke, die Sie mit dem Server mit Windows Server Essentials Speicherplätzen gruppieren möchten.  
  
2.  Klicken Sie auf dem Dashboard auf **erweitert: Speicherplatz verwalten**.  
  
3.  Klicken Sie auf **erstellen einen neuen Pool und Speicherplatz**.  
  
4.  Wählen Sie die Laufwerke, die Sie verwenden möchten, auf dem neuen Speicherplatz hinzufügen, und klicken Sie dann auf **-Pool erstellen**.  
  
5.  Weisen Sie dem Laufwerk einen Namen und einen Buchstaben aus, und wählen Sie dann ein Layout. **Zwei-Wege-Spiegelung**, **drei-Wege-Spiegelung**, und **Parität** schützen die Dateien am Speicherplatz vor Laufwerksfehlern.  
  
6.  Geben Sie die maximale Größe des Speicherplatzes erreichen kann, und klicken Sie dann auf **Speicherplatz erstellen**.  
  
 In Windows Server Essentials können Sie einen bidirektionalen gespiegelten Speicherplatz mit dem Speicherplatz Assistent zum Erstellen eines über das Dashboard.  
  
#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>Zum Erstellen eines Speicherplatzes in Windows Server Essentials  
  
1.  Fügen Sie hinzu, oder Verbinden Sie die Laufwerke, die Sie mit dem Server mit Windows Server Essentials Speicherplätzen gruppieren möchten.  
  
2.  Klicken Sie auf dem Dashboard auf **Verwalten von Speicherplätzen**. Erstellen, den einer Speicherplatz-Assistent wird angezeigt.  
  
3.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
 Informationen zum Erhöhen der Speicherpoolkapazität finden Sie unter [verwenden Sie die neue Festplatte zum Erhöhen der Speicherpoolkapazität](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
