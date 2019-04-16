---
title: Verwalten von Serverordnern in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 090cf1b8-7b9b-48b9-ae85-b98477b8d7cc
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e1f3640f21b95acafa850b2204cd52f9c0f324e5
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-server-folders-in-windows-server-essentials"></a>Verwalten von Serverordnern in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Als Serveradministrator können Sie den Zugriff auf alle Serverordner (bekannt als freigegebene Ordner, wenn über das Launchpad, den Remotewebzugriff, My Server-app für Windows Phone oder My Server-app für Windows 8) auf dem Server verwalten, mithilfe der Tasks auf der **Serverordner** Registerkarte des Dashboards, sodass Benutzern unterschiedliche Zugriffsebenen für eine Vielzahl von Dateien.  
  
 Die folgenden Themen enthalten Informationen, mit deren Hilfe Sie verstehen, erstellen und Verwalten von Serverordnern:  
  
-   [Verwalten von Serverordnern über das Dashboard](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Verwalten des Zugriffs auf Serverordner](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Hinzufügen oder Verschieben von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Fügen Sie fehlender Serverordner hinzu](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Grundlagen zu freigegebenen Ordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Grundlagen zu Schattenkopien](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Shadow)  
  
##  <a name="BKMK_2"></a>Verwalten von Serverordnern über das Dashboard  
 Windows Server Essentials ermöglicht es, allgemeine Verwaltungsaufgaben auszuführen, über das Dashboard. Die **Serverordner** -Seite des Dashboards bietet Folgendes:  
  
-   Eine Liste der Serverordner, die anzeigt:  
  
    -   Der Name des Ordners  
  
    -   Eine Beschreibung des Ordners  
  
    -   Der Speicherort des Ordners  
  
    -   Die Menge des freien Speicherplatzes, der am Speicherort Ordners verfügbar ist  
  
    -   Kurze Statusinformationen zu allen Aufgaben, die auf den Ordner ausgeführt werden; die **Status** Feld ist leer, wenn der Ordner fehlerfrei ist und keine Aufgaben ausgeführt werden  
  
-   Ein Detailbereich, der zusätzliche Informationen zu einem ausgewählten Ordner bereitstellen können  
  
-   Ein Aufgabenbereich, der eine Reihe von Verwaltungsaufgaben im Zusammenhang mit Ordner enthält  
  
 Die folgende Tabelle beschreibt die verschiedenen Ordneraufgaben, die auf Windows Server Essentials-Dashboard verfügbar sind. Die meisten Aufgaben sind ordnerabhängig und sie werden nur angezeigt, wenn Sie einen Ordner in der Liste auswählen.  
  
### <a name="server-folder-tasks-on-the-dashboard"></a>Tasks für Serverordner auf dem Dashboard  
  
|Den Namen der Aufgabe|Beschreibung|  
|---------------|-----------------|  
|Öffnen Sie den Ordner|Zeigt den Inhalt des ausgewählten Ordners im Datei-Explorer (in früheren Versionen von Windows auch Windows-Explorer genannt).|  
|Löschen Sie den Ordner|Können Sie eine vom Benutzer erstellten Ordners zu löschen. Diese Aufgabe ist nicht verfügbar für die Standardordner, die Server-Installation erstellt.|  
|Verschieben Sie den Ordner|Öffnet einen Assistenten, der Sie die Ordner an einen neuen Speicherort zu verschieben können.|  
|Beenden Sie den Ordner freigeben|Beendet die Freigabe des ausgewählten Ordners, jedoch nicht gelöscht. Wenn der Ordner nicht mehr freigegeben ist, wird es nicht im Dashboard angezeigt. Diese Aufgabe ist nicht verfügbar für die Standardordner, die Server-Installation erstellt.|  
|Ordnereigenschaften anzeigen|Zeigt die Eigenschaften für einen ausgewählten Ordner ein, und ermöglicht es Ihnen:<br /><br /> – Ändern Sie den Namen der Benutzer erstellten Ordners.<br /><br /> – Ändern Sie die Beschreibung für einen ausgewählten Ordner.<br /><br /> -Zeigen Sie die Größe des Ordners.<br /><br /> – Öffnen Sie den ausgewählten Ordner im Datei-Explorer.<br /><br /> -Geben Sie Berechtigungen für Benutzerkonten Zugriff für einen ausgewählten Ordner.<br /><br /> -Blenden Sie einen ausgewählten Ordner Remote Web Access und Webdienst-Anwendungen.<br /><br /> -Ordnerkontingente anzugeben.|  
|Hinzufügen eines Ordners|Hilft Ihnen beim Erstellen eines neuen Serverordners und weisen die Zugriffsebene für jedes Benutzerkonto.|  
|Grundlagen zu Serverordnern|Öffnet ein Hilfethema im Internet, die die Verwendung und die Funktionen von Serverordnern beschrieben.|  
  
##  <a name="BKMK_1"></a>Verwalten des Zugriffs auf Serverordner  
 Windows Server Essentials können Sie Dateien mithilfe von Serverordnern auf den Clientcomputern an einem zentralen Ort speichern. Speichern von Dateien in Serverordnern wird sichergestellt, dass Ihre Dateien an einem Speicherort befinden, die immer auf sichere Weise auf jedem Client zugegriffen werden kann.  
  
 Verwendung von Serverordnern zum Speichern der Dateien können Sie die folgenden Schritte ausführen:  
  
-   Sichern Sie den Serverordner mithilfe von Server-Sicherung und Wiederherstellung um vor totalen Serverausfällen zu schützen.  
  
-   Zugriff auf Dateien, die mit einem Internetbrowser über Remotezugriff oder über die My Server-apps für Windows Phone und Windows 8 auf den Serverordner von einem beliebigen Speicherort gespeichert sind.  
  
-   Zugriff auf den neuen Serverordner von beliebigen Clientcomputern.  
  
 Sie können den Zugriff auf alle Serverordner auf dem Server verwalten, mithilfe der Tasks auf der **Serverordner** Dashboard-Registerkarte. Die folgende Tabelle enthält die Serverordner, die standardmäßig bei der Installation von Windows Server Essentials oder Medienstreaming aktivieren, auf dem Server erstellt werden.  
  
|Serverordnername|Beschreibung|  
|------------------------|-----------------|  
|Clientcomputersicherungen|Standardmäßig erstellt Windows Server Essentials Client-Sicherungen, die in diesem Ordner gespeichert sind. Die Einstellungen für Clientcomputersicherungen können vom Netzwerkadministrator geändert werden.|  
|Unternehmen|Zum Speichern und Zugriff auf Dokumente, die im Zusammenhang mit Ihrer Organisation von Benutzern im Netzwerk verwendet.|  
|Sicherungen von Dateiversionsverläufen|Windows Server Essentials verwendet standardmäßig den Dateiversionsverlauf zum Erstellen von dateisicherungen, die in diesem Ordner gespeichert sind. Diese Einstellungen für Dateiversionsverlauf können von Netzwerkadministratoren geändert werden.|  
|Ordnerumleitung|Verwendet zum Speichern und Zugreifen auf Ordner, die vom Benutzer im Netzwerk für die ordnerumleitung eingerichtet werden.|  
|Benutzer|Speichern und Zugreifen auf Dateien durch Benutzer im Netzwerk verwendet. Ein Benutzerspezifischer Ordner wird automatisch generiert, der **Benutzer** Serverordner für jedes Netzwerkbenutzerkonto, die Sie erstellen.|  
|Musik|Zum Speichern und Musikdateien durch Benutzer im Netzwerk zugreifen. Dieser Ordner ist verfügbar, wenn Sie die Medienfreigabe aktivieren.|  
|Bilder|Zum Speichern und Abrufen von Bilddateien von Netzwerkbenutzern verwendet. Dieser Ordner ist verfügbar, wenn Sie die Medienfreigabe aktivieren.|  
|Aufgezeichnete Fernsehsendungen|Zum Speichern und aufgezeichnete Fernsehsendungen von Netzwerkbenutzern zugreifen. Dieser Ordner ist verfügbar, wenn Sie die Medienfreigabe aktivieren.|  
|Videos|Zum Speichern und Videodateien von Netzwerkbenutzern zugreifen. Dieser Ordner ist verfügbar, wenn Sie die Medienfreigabe aktivieren.|  
  
 Zum Ausblenden oder Festlegen von Berechtigungen für Serverordner oder zu ändern, finden Sie unter den folgenden Verfahren:  
  
-   [Ausblenden von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Hide)  
  
-   [Festlegen von Berechtigungen für Serverordner](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Perms)  
  
-   [Anzeigen oder Ändern von serverordnereigenschaften](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_10)  
  
###  <a name="BKMK_Hide"></a>Ausblenden von Serverordnern  
 Als Netzwerkadministrator können Sie eines dieser Serverordner ausblenden und verhindern, dass sie auf dem Remote Web Access-Website oder Web Services-Anwendungen (z. B. My Server) angezeigt werden.  
  
> [!NOTE]
>  Sie muss ein Netzwerkadministrator, um dieses Verfahren ausführen zu können.  
  
##### <a name="to-hide-server-folders-from-being-displayed-in-remote-web-access"></a>Ausblenden von Serverordnern in Remotewebzugriff angezeigt wird  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< ServerFolder\ > Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< FolderName\ > Eigenschaften**, klicken Sie auf **Freigabe**Option **Ausblenden dieser Ordner Remote Web Access und Webdienst Applications**, und klicken Sie dann auf **übernehmen**.  
  
###  <a name="BKMK_Perms"></a>Festlegen von Berechtigungen für Serverordner  
 Für jeden zusätzlichen Serverordner, die Sie mithilfe des Dashboards auf dem Server hinzufügen, können Sie drei unterschiedliche zugriffseinstellungen Einstellungen auswählen:  
  
-   **Lese-/Schreibzugriff**  
  
     Wählen Sie diese Einstellung, wenn Sie diese Person erstellen, ändern und löschen Sie alle Dateien im Serverordner zulassen möchten.  
  
-   **Schreibgeschützt**  
  
     Wählen Sie diese Einstellung, wenn Sie zulassen, diese Person nur Dateien im Serverordner zu lesen möchten. Benutzer mit schreibgeschütztem Zugriff können nicht erstellen, ändern oder löschen Sie alle Dateien im Serverordner.  
  
-   **Kein Zugriff**  
  
     Wählen Sie diese Einstellung, wenn Sie nicht, dass diese Person auf Dateien im Serverordner zugreifen möchten.  
  
> [!IMPORTANT]
>  Die Berechtigungen, die in den Ordnereigenschaften angezeigt werden darstellen, nur die Benutzer, die über das Dashboard verwaltet werden. Sie führen Sie keine Benutzerberechtigungen wie Gruppen oder Dienstkonten, oder enthalten alle Berechtigungen, die möglicherweise über andere systemeigene Tools für den Ordner festgelegt werden, oder Benutzer, die nicht über das Dashboard hinzugefügt wurden.  
  
> [!NOTE]
>  Sie muss ein Netzwerkadministrator, um dieses Verfahren ausführen zu können.  
  
##### <a name="to-set-permissions-to-server-folders-on-the-server"></a>Festlegen von Berechtigungen für Serverordner auf dem server  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< ServerFolder\ > Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< FolderName\ > Eigenschaften**, klicken Sie auf **Freigabe**, und wählen Sie die entsprechende Zugriffsebene für die aufgeführten Benutzerkonten aus, und klicken Sie dann auf **übernehmen**.  
  
> [!NOTE]
>  Standardmäßig, wenn Sie ein Benutzerkonto mit dem Netzwerk hinzufügen ein Unterordner erstellt für den Benutzer durch die **Benutzer** Ordner auf dem Server. Der Unterordner kann nur für den Benutzer oder der Administrator von einem Computer im Netzwerk zugegriffen werden. Die Berechtigungen festgelegt sind, für die einzelnen Unterordner unter **Benutzer**, sodass es keine allgemeine Zugriffsberechtigungen für die auf der obersten Ebene **Benutzer** Ordner.  
  
> [!NOTE]
>  Die Freigabeberechtigungen für kann nicht geändert die **Dateiversionsverläufen**, **Ordnerumleitung**, und **Benutzer** Serverordner. Die Ordnereigenschaften dieser Serverordner enthalten daher keine **Freigabe** Registerkarte.  
  
###  <a name="BKMK_10"></a>Anzeigen oder Ändern von serverordnereigenschaften  
 Sie können den serverordnernamen seine Beschreibung ändern und definieren, welche Benutzerkonten Zugriff auf einen Serverordner haben über die **Ordnereigenschaften anzeigen** Aufgabe auf den **Serverordner** Dashboard-Registerkarte.  
  
> [!NOTE]
>  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle können Sie auch Ordnerkontingent ändern.  
  
##### <a name="to-view-or-modify-folder-properties"></a>Anzeigen oder Ändern der Eigenschaften des Ordners  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< ServerFolder\ > Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< Foldername\ > Eigenschaften**auf die **allgemeine** Registerkarte, anzeigen oder ändern Sie den Namen und die Beschreibung des Serverordners.  
  
    > [!NOTE]
    >  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle können Sie auch Ordnerkontingent ändern, die eine Warnmeldung ausgibt, wenn ein Serverordner seine angegebene Größe erreicht hat.  
  
##  <a name="BKMK_5"></a>Hinzufügen oder Verschieben von Serverordnern  
 Sie können **Weitere Serverordner hinzufügen** zum Speichern der Dateien auf dem Server als auch die standardmäßigen Serverordner, die während des Setups erstellt werden. Sie können Serverordner auf dem primären Server oder einem Mitgliedsserver unter Windows Server Essentials hinzufügen.  
  
 Können Sie **Verschieben von Serverordnern** , befindet sich auf dem primären Server mit Windows Server Essentials und wird angezeigt, auf die **Serverordner** Registerkarte im Dashboard auf eine andere Festplatte bei Bedarf mithilfe des Assistenten wechseln. Sie können einen Serverordner an eine andere Festplatte Speicherort Adresse verschieben, wenn:  
  
-   Die Datenfestplatte verfügt nicht mehr genügend Speicherplatz zum Speichern von Daten.  
  
-   Sie möchten den Standardspeicherort zu ändern. Sollten Sie für eine schnellere verschieben den Serverordner verschieben, während es keine Daten enthalten ist.  
  
-   Sie möchten die vorhandene Festplatte entfernen, ohne dass die Serverordner, die sich darauf befinden.  
  
 Bevor Sie den Ordner verschieben, stellen Sie Folgendes sicher:  
  
-   Stellen Sie sicher, dass Sie den Server gesichert haben.  
  
-   Stellen Sie sicher, dass alle Clientsicherungen beendet werden und nicht aktiv, wenn Sie den Client Computer Backup-Ordner verschieben möchten. Während der Client Computer Backup-Ordner verschieben, wird der Server in der Lage keine Clientcomputer sichern, bis der Ordner vollständig verschoben wurde.  
  
-   Stellen Sie sicher, dass der Server keine kritischen Systemvorgänge ausführt. Es wird empfohlen, dass Sie alle Updates oder Sicherungen, die in Bearbeitung sind, bevor Sie beginnen von einem Ordner verschieben oder dieser Vorgang kann länger dauern.  
  
-   Keine der Dateien in den zu verschiebenden Ordner wird zurzeit verwendet. Sie werden nicht auf den Serverordner zugreifen, während dieser verschoben wird.  
  
 Verschieben eines Ordners von NTFS zu ReFS wird nicht unterstützt, wenn die Dateien in den Serverordnern die folgenden Technologien implementieren:  
  
-   Alternative Datenströme  
  
-   Objekt-IDs  
  
-   Kurznamen (8.3-Namen)  
  
-   Komprimierung  
  
-   EFS-Verschlüsselung  
  
-   Transaktions-NTFS, TxF (eingeführt in Windows Vista)  
  
-   Dateien mit geringer Datendichte  
  
-   Feste links  
  
-   Erweiterte Attribute  
  
-   Kontingente  
  
###  <a name="BKMK_6"></a>Wo hinzufügen oder Verschieben von Serverordnern  
 Sie sollten in der Regel hinzufügen oder verschieben Serverordner auf Festplatten, die die maximale Menge an freiem Speicherplatz verfügen. Vermeiden Sie wenn möglich hinzufügen oder verschieben einen freigegebenen Ordner auf das Systemlaufwerk (z. B. "c:"), wie es sofort der erforderlichen Festplattenspeicher dauern kann, die für das Betriebssystem und seine Updates erforderlich ist. Vermeiden Sie außerdem hinzufügen oder Verschieben von Serverordnern auf einer externen Festplatte, da sie ganz einfach getrennt werden können und daher möglicherweise nicht auf Ihre Dateien zugreifen. Stattdessen wird empfohlen, dass Sie den Ordner auf einem internen Laufwerk erstellen.  
  
 Ein Serverordner kann nicht hinzugefügt oder in den folgenden Speicherorten verschoben werden und führt zu einem Fehler, wenn einer dieser Speicherorte für oder Verschieben von Serverordnern ausgewählt ist:  
  
-   Eine Festplatte, die nicht mit dem Dateisystem NTFS oder ReFS formatiert ist  
  
-   Ordner "% windir%"  
  
-   Ein zugeordnetes Netzwerklaufwerk  
  
-   Einen Ordner mit einem freigegebenen Ordner  
  
-   Eine Festplatte, die befinden sich **Gerät mit Wechselmedien**  
  
-   Ein Stammverzeichnis einer Festplatte (z. B. C:\\, D:\\, E:\\)  
  
-   Ein Unterordner eines vorhandenen freigegebenen Ordners  
  
-   Ein Mitgliedsserver unter Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle  
  
### <a name="steps-to-add-or-move-a-server-folder"></a>Schritte zum Hinzufügen oder Verschieben von Serverordnern  
  
> [!NOTE]
>  Sie müssen ein Serveradministrator zum Abschließen dieser Verfahren sein.  
  
##### <a name="to-add-a-server-folder"></a>So fügen Sie einen Serverordner hinzu  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  In **Tasks für Serverordner**, klicken Sie auf **fügen Sie einen Ordner**. Dies startet den Assistenten zum Ordner hinzufügen.  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
    > [!NOTE]
    >  -   Wenn Sie mithilfe der Schaltfläche "Durchsuchen", geben Sie den Speicherort des Ordners für einen bestimmten Ordner navigieren, wird der Ordner, dem Sie navigiert sind als Serverordner hinzugefügt.  
    > -   Sie können definieren, welche Serverordner über Remotewebzugriff zugegriffen werden können. Weitere Informationen finden Sie unter [Verwalten des Zugriffs auf Serverordner](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_1).  
  
##### <a name="to-move-a-server-folder"></a>So verschieben Sie einen Serverordner  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Wählen Sie in der Liste der Serverordner den Ordner, den Sie verschieben möchten.  
  
4.  Klicken Sie im Bereich Aufgaben auf **verschieben Sie den Ordner**.  
  
5.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
##  <a name="BKMK_9"></a>Fügen Sie fehlender Serverordner hinzu  
 Wenn der Server erkennt, dass ein vordefinierter Serverordner? Unternehmen, Benutzer, Clientcomputersicherungen, Dateiversionsverläufen oder Ordnerumleitung? nicht mehr freigegeben ist (für aus irgendeinem Grund oder ein anderes), wird eine Warnung generiert, um den Benutzer zum Beheben dieses Problems zu unterstützen. Es wird empfohlen, dass Sie versuchen, und stellen Sie den Ordner über Server-Sicherung wieder her. Wenn der Server nicht gesichert wurde, wählen Sie den fehlenden Ordner und klicken Sie dann auf **fehlenden Ordner neu erstellen** so konfigurieren Sie den Speicherort des Serverordners neu.  
  
> [!NOTE]
>  Nur vordefinierte Ordner? Unternehmen, Benutzer, Clientcomputersicherungen, Dateiversionsverläufen oder Ordnerumleitung? neu erstellt werden können. Benutzer erstellte Serverordner und Medien Serverordner können nicht neu erstellt werden.  
  
 Nach dem Wiederherstellen oder fehlenden Ordner neu erstellen, es sollte nicht mehr als aufgeführt **fehlt**.  
  
 Informationen zum Wiederherstellen von Dateien aus serversicherungen finden Sie im Abschnitt Weitere Informationen zum Wiederherstellen von Dateien und Ordner unter dem Thema [Manage Backup and Restore](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_11"></a>Grundlagen zu freigegebenen Ordnern  
 Es gibt mehrere Möglichkeiten, die die freigegebenen Ordner auf Windows Server Essentials von einem Gerät zugreifen können, die mit dem Server verbunden ist. Weitere Informationen finden Sie im Thema [Use Shared Folders](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_Shadow"></a>Grundlagen zu Schattenkopien  
 Mit Schattenkopien von Servern können Benutzer freigegebene Dateien und Ordner anzeigen, sie zu Zeitpunkten in der Vergangenheit vorhanden waren. Zugreifen auf vorherige Versionen von Dateien oder Schattenkopien sind hilfreich, da Benutzer können:  
  
1.  **Wiederherstellen von versehentlich gelöschten Dateien**. Wenn Sie eine Datei versehentlich löschen, können Sie eine frühere Version öffnen und an einem sicheren Speicherort zu kopieren.  
  
2.  **Wiederherstellen von versehentlich überschriebenen Dateien**. Wenn Sie eine Datei versehentlich überschreiben, können Sie eine vorherige Version der Datei wiederherstellen. (Die Anzahl der Versionen hängt wie viele Momentaufnahmen Sie erstellt haben.)  
  
3.  **Vergleichen der Versionen einer Datei während der Arbeit**. Frühere Versionen können Sie überprüfen, was zwischen Versionen einer Datei geändert hat.  
  
 Um Schattenkopien, von einem Clientcomputer aus zu verwenden, mit der rechten Maustaste in eines freigegebenen Serverordner, und wählen Sie **vorherige Version wiederherstellen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Serverspeicher](Manage-Server-Storage-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
