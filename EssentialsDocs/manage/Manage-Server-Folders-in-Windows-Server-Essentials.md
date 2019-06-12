---
title: Verwalten der Serverordner in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: 0c46d19f4f172786e0ffe7f3b9dd7ac1d8f4fcf0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433203"
---
# <a name="manage-server-folders-in-windows-server-essentials"></a>Verwalten der Serverordner in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Als Serveradministrator, können Sie den Zugriff auf alle Serverordner (bekannt als freigegebenen Ordner, wenn über das Launchpad, Remote Web Access, My Server-app für Windows Phone oder My Server-app für Windows 8) auf dem Server verwalten, mithilfe der Tasks auf der  **Serverordner** Registerkarte des Dashboards, sodass Benutzern unterschiedliche Zugriffsebenen für eine Vielzahl von Dateien.  
  
 Die folgenden Themen enthalten Informationen, die Ihnen dabei helfen, das Erstellen und Verwalten der Serverordner zu verstehen:  
  
-   [Verwalten von Serverordnern über das Dashboard](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Verwalten des Zugriffs auf Serverordner](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Hinzufügen oder Verschieben von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Fügen Sie fehlender Serverordner hinzu](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Grundlagen zu freigegebenen Ordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Grundlagen zu Schattenkopien](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Shadow)  
  
##  <a name="BKMK_2"></a> Verwalten von Serverordnern über das Dashboard  
 Windows Server Essentials ermöglicht die Ausführung allgemeiner administrativer Aufgaben über das Dashboard. Die Seite **Serverordner** des Dashboards bietet Folgendes:  
  
- Eine Liste der Serverordner, in der Folgendes angezeigt wird:  
  
  -   Der Name des Ordners.  
  
  -   Eine Beschreibung des Ordners.  
  
  -   Der Speicherort des Ordners.  
  
  -   Die Menge des freien Speicherplatzes, die am Speicherort des Ordners verfügbar ist.  
  
  -   Kurze Statusinformationen zu allen Aufgaben, die für den Ordner ausgeführt werden. Das Feld **Status** ist leer, wenn der Ordner fehlerfrei ist und keine Aufgaben ausgeführt werden.  
  
- Ein Detailbereich, der möglicherweise zusätzliche Informationen zu einem ausgewählten Ordner bietet.  
  
- Ein Aufgabenbereich, der eine Reihe von auf den Ordner bezogenen administrativen Aufgaben enthält.  
  
  Die folgende Tabelle beschreibt die verschiedenen Ordneraufgaben, die auf dem Windows Server Essentials-Dashboard verfügbar sind. Die meisten Aufgaben sind ordnerabhängig und sie werden nur angezeigt, wenn Sie einen Ordner in der Liste auswählen.  
  
### <a name="server-folder-tasks-on-the-dashboard"></a>Serverordneraufgaben auf dem Dashboard  
  
|Aufgabenname|Beschreibung|  
|---------------|-----------------|  
|Ordner öffnen|Zeigt den Inhalt des ausgewählten Ordners im Datei-Explorer (wird in früheren Versionen von Windows auch Windows-Explorer genannt) an.|  
|Ordner löschen|Ermöglicht das Löschen eines vom Benutzer erstellten Ordners. Diese Aufgabe ist für Standardordner nicht verfügbar, die über die Serverinstallation erstellt werden.|  
|Ordner verschieben|Öffnet einen Assistenten, der Sie beim Verschieben eines Serverordners an einen neuen Speicherort unterstützt.|  
|Freigabe des Ordners beenden|Beendet die Freigabe des ausgewählten Ordners, löscht ihn jedoch nicht. Wenn der Ordner nicht mehr freigegeben ist, wird er nicht mehr auf dem Dashboard angezeigt. Diese Aufgabe ist für Standardordner nicht verfügbar, die über die Serverinstallation erstellt werden.|  
|Ordnereigenschaften anzeigen|Zeigt die Eigenschaften für einen ausgewählten Ordner an, und ermöglicht Ihnen Folgendes:<br /><br /> -Ändern Sie der Name des Benutzer erstellten Ordners.<br /><br /> – Ändern Sie die Beschreibung für einen ausgewählten Ordner ein.<br /><br /> – Die Größe des Ordners anzeigen.<br /><br /> – Öffnen Sie den ausgewählten Ordner im Datei-Explorer.<br /><br /> -Geben Sie den Zugriff für Benutzerkontoberechtigungen für einen ausgewählten Ordner.<br /><br /> -Blenden Sie aus, einen ausgewählten Ordner Remote Web Access und Webdienst-Anwendungen.<br /><br /> -Ordnerkontingente anzugeben.|  
|Hinzufügen von Ordnern|Unterstützt Sie bei der Erstellung eines neuen Serverordners und der Zuweisung der Zugriffsebene, die für die jeweiligen Benutzerkonten zulässig sind.|  
|Grundlagen zu Serverordnern|Öffnet ein Hilfethema im Internet, in dem Verwendung und Funktionen von Serverordnern beschrieben sind.|  
  
##  <a name="BKMK_1"></a> Verwalten des Zugriffs auf Serverordner  
 Mithilfe von Windows Server Essentials können Sie Dateien, die sich auf Ihren Clientcomputern befinden, mithilfe von Serverordnern an einem zentralen Speicherort speichern. Durch das Speichern der Dateien in Serverordnern wird sichergestellt, dass sich Ihre Dateien immer an einem Speicherort befinden, auf den von jedem Client aus immer auf sichere Weise zugegriffen werden kann.  
  
 Die Verwendung von Serverordnern zum Speichern von Dateien bietet folgende Möglichkeiten:  
  
- Serverordner mithilfe der Serversicherung und -wiederherstellung sichern, um vor totalen Serverausfällen zu schützen.  
  
- Zugriff auf Dateien, die im Serverordner gespeichert werden, von beliebigen Standorten aus mit Internetbrowser und Remotewebzugriff, oder über die App für eigene Server für Windows Phone und Windows 8.  
  
- Zugriff auf den neuen Serverordner von beliebigen Clientcomputern aus.  
  
  Sie können den Zugriff auf Serverordner auf dem Server mithilfe der Tasks auf der Registerkarte **Serverordner** des Dashboards verwalten. Die folgende Tabelle enthält die Serverordner, die standardmäßig bei der Installation von Windows Server Essentials oder bei der Aktivierung des Medienstreamings auf dem Server erstellt werden.  
  
|Serverordnername|Beschreibung|  
|------------------------|-----------------|  
|Clientcomputersicherungen|Windows Server Essentials erstellt standardmäßig Clientcomputersicherungen, die in diesem Ordner gespeichert werden. Die Einstellungen für Clientcomputersicherungen können vom Netzwerkadministrator geändert werden.|  
|Firma|Darin werden Dokumente von Netzwerkbenutzern gespeichert und abgerufen, die sich auf das Unternehmen beziehen.|  
|Sicherungen von Dateiversionsverläufen|Windows Server Essentials verwendet Dateiversionsverläufe standardmäßig zum Erstellen von Dateisicherungen, die in diesem Ordner gespeichert werden. Diese Einstellungen für Dateiversionsverläufe können von Netzwerkadministratoren geändert werden.|  
|Ordnerumleitung|Darin werden Ordner gespeichert und abgerufen, die von Netzwerkbenutzern für die Ordnerumleitung eingerichtet wurden.|  
|Benutzer|Darin werden Dateien von Netzwerkbenutzern gespeichert und abgerufen. Ein benutzerspezifischer Ordner wird automatisch im Serverordner **Benutzer** für jedes Netzwerkbenutzerkonto generiert, das Sie erstellen.|  
|Musik|Darin werden Musikdateien von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.|  
|Bilder|Darin werden Bilddateien von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.|  
|TV-Aufzeichnungen|Darin werden aufgezeichnete Fernsehsendungen von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.|  
|Videos|Darin werden Videodateien von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.|  
  
 Die folgenden Verfahren bieten Informationen zum Ausblenden oder Festlegen von Berechtigungen für Serverordner oder zum Ändern von Serverordnereigenschaften:  
  
-   [Ausblenden von Serverordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Hide)  
  
-   [Festlegen von Berechtigungen für Serverordner](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_Perms)  
  
-   [Anzeigen oder Ändern von serverordnereigenschaften](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_10)  
  
###  <a name="BKMK_Hide"></a> Ausblenden von Serverordnern  
 Als Netzwerkadministrator können Sie jeden dieser Serverordner ausblenden und dadurch verhindern, dass sie auf der Website für den Remotewebzugriff oder in den Webdienstanwendungen (wie "Eigener Server") angezeigt werden.  
  
> [!NOTE]
>  Sie müssen Netzwerkadministrator sein, um dieses Verfahren ausführen zu können.  
  
##### <a name="to-hide-server-folders-from-being-displayed-in-remote-web-access"></a>So blenden Sie Serverordner von der Anzeige für den Remotewebzugriff aus  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner aus, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< Serverordner\> Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< Ordnername\> Eigenschaften**, klicken Sie auf **Freigabe**Option **diesen Ordner Remote Web Access und Webdienst-Anwendungen ausblenden**, und klicken Sie dann auf **Anwenden**.  
  
###  <a name="BKMK_Perms"></a> Festlegen von Berechtigungen für Serverordner  
 Für jeden zusätzlichen Serverordner, den Sie mithilfe des Dashboards auf dem Server hinzufügen, können Sie drei unterschiedliche Zugriffseinstellungen Einstellungen auswählen:  
  
-   **Lese-/Schreibzugriff**  
  
     Wählen Sie diese Einstellung aus, wenn Sie es der Person gestatten möchten, Dateien im Serverordner zu erstellen, zu ändern und zu löschen.  
  
-   **Read-only**  
  
     Wählen Sie diese Einstellung aus, wenn Sie es der nur Person gestatten möchten, Dateien im Serverordner zu lesen. Benutzer mit schreibgeschützten Zugriff können keine Dateien im Serverordner erstellen, ändern oder löschen.  
  
-   **Kein Zugriff**  
  
     Wählen Sie diese Einstellung aus, wenn die Person nicht auf Dateien im Serverordner zugreifen können soll.  
  
> [!IMPORTANT]
>  Die Berechtigungen, die in den Ordnereigenschaften angezeigt werden, stellen nur Benutzer dar, die über das Dashboard verwaltet werden. Sie beziehen keine Benutzerberechtigungen wie Gruppen oder Dienstkonten ein. Sie beziehen auch keine Berechtigungen ein, die möglicherweise über andere systemeigene Tools für den Ordner festgelegt werden. Auch nicht über das Dashboard hinzugefügte Benutzer werden nicht einbezogen.  
  
> [!NOTE]
>  Sie müssen Netzwerkadministrator sein, um dieses Verfahren ausführen zu können.  
  
##### <a name="to-set-permissions-to-server-folders-on-the-server"></a>So legen Sie Berechtigungen für Serverordner auf dem Server fest  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner aus, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< Serverordner\> Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< Ordnername\> Eigenschaften**, klicken Sie auf **Freigabe**, und wählen Sie die entsprechende Zugriffsebene für die aufgeführten Benutzerkonten aus, und klicken Sie dann auf **übernehmen**.  
  
> [!NOTE]
>  Wenn Sie ein Benutzerkonto zum Netzwerk hinzufügen wird standardmäßig ein Unterordner für den Benutzer unter dem Ordner **Benutzer** auf dem Server erstellt. Nur der Benutzer oder der Administrator kann über einen Netzwerkcomputer auf den Unterordner zugreifen. Die Berechtigungen für die einzelnen Unterordner werden unter **Benutzer**festgelegt, sodass es keine allgemeine Zugriffsberechtigungen für den Ordner **Benutzer** der obersten Ebene gibt.  
  
> [!NOTE]
>  Die Freigabeberechtigungen für die Serverordner **Sicherungen von Dateiversionsverläufen**, **Ordnerumleitung**und **Benutzer** können nicht geändert werden. Die Ordnereigenschaften dieser Serverordner enthalten daher keine Registerkarte für **Freigabe**.  
  
###  <a name="BKMK_10"></a> Anzeigen oder Ändern von serverordnereigenschaften  
 Sie können den Serverordnernamen und seine Beschreibung ändern und über die Aufgabe **Ordnereigenschaften anzeigen** auf der Registerkarte **Serverordner** des Dashboards festlegen, welche Benutzerkonten Zugriff auf einen Serverordner erhalten.  
  
> [!NOTE]
>  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle können Sie auch Ordnerkontingent ändern.  
  
##### <a name="to-view-or-modify-folder-properties"></a>So zeigen Sie Ordnereigenschaften an oder ändern diese  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.  
  
3.  Wählen Sie in der Listenansicht die Serverordner aus, deren Eigenschaften Sie anzeigen oder ändern möchten.  
  
4.  In der **< Serverordner\> Aufgaben** Bereich, klicken Sie auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< Ordnername\> Eigenschaften**auf die **allgemeine** Registerkarte, anzeigen oder ändern Sie den Namen und die Beschreibung des Serverordners.  
  
    > [!NOTE]
    >  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle können Sie auch Ordnerkontingent ändern, die eine Warnmeldung ausgibt, wenn ein Serverordner seine angegebene Größe erreicht hat.  
  
##  <a name="BKMK_5"></a> Hinzufügen oder Verschieben von Serverordnern  
 Sie können **weitere Serverordner hinzufügen** , um Ihre Dateien auf dem Server zu speichern, anstatt nur die Standardserverordner zu verwenden, die beim Setup erstellt werden. Sie können Serverordner entweder auf dem primären oder einem Mitgliedsserver hinzufügen, auf denen Windows Server Essentials ausgeführt wird.  
  
 Sie können einen **Serverordner**, der sich auf dem primären Server befindet, auf dem Windows Server Essentials ausgeführt wird, und auf der Registerkarte **Serverordner** des Dashboards angezeigt wird, bei Bedarf mithilfe des Assistenten zum Verschieben von Ordnern auf eine andere Festplatte verschieben. Unter den folgenden Bedingungen können Sie einen Serverordner an eine andere Speicheradresse auf der Festplatte verschieben:  
  
- Die Datenfestplatte verfügt nicht mehr über ausreichend Speicherplatz zum Speichern der Daten.  
  
- Sie möchten den Standardspeicherort ändern. Erwägen Sie, den Serverordner zu verschieben, wenn dieser keine Daten enthält, um den Vorgang zu beschleunigen.  
  
- Sie möchten die vorhandene Festplatte entfernen, ohne die Serverordner zu verlieren, die sich darauf befinden.  
  
  Stellen Sie Folgendes sicher, bevor Sie den Ordner verschieben:  
  
- Stellen Sie sicher, dass Sie den Server gesichert haben.  
  
- Stellen Sie sicher, dass alle Clientsicherungen beendet werden und nicht aktiv sind, wenn Sie den Ordner für die Clientcomputersicherung verschieben möchten. Beim Verschieben des Ordners für die Clientcomputersicherung kann der Server keine Clientcomputer sichern, bis der Ordner vollständig verschoben wurde.  
  
- Stellen Sie sicher, dass der Server keine kritischen Systemvorgänge ausführt. Es wird empfohlen, alle aktiven Updates oder Sicherungen abzuschließen, bevor Sie eine Ordnerverschiebung starten. Andernfalls kann es länger dauern, bis der Vorgang abgeschlossen ist.  
  
- Keine der Dateien im zu verschiebenden Ordner wird verwendet. Sie können nicht auf den Serverordner zugreifen, während dieser verschoben wird.  
  
  Das Verschieben von Ordnern von NTFS zu ReFS wird nicht unterstützt, wenn die Dateien in den Serverordnern die folgenden Technologien implementieren:  
  
- Alternative Datenströme  
  
- Objekt-IDs  
  
- Kurznamen (8.3-Namensformat)  
  
- Komprimierung  
  
- EFS-Verschlüsselung  
  
- Transaktionales NTFS, TxF (wurde mit Windows Vista eingeführt)  
  
- Dateien mit geringer Datendichte  
  
- Feste Links  
  
- Erweiterte Attribute  
  
- Kontingente  
  
###  <a name="BKMK_6"></a> Wo hinzufügen oder Verschieben von Serverordnern  
 In der Regel sollten Sie Serverordner auf Festplatten hinzufügen oder verschieben, die über die maximale Größe an freiem Speicherplatz verfügen. Vermeiden Sie nach Möglichkeit das Hinzufügen oder Verschieben eines freigegebenen Ordners zum Systemlaufwerk (z. B. "C:"), da dadurch dann möglicherweise der erforderliche Speicherplatz fehlt, der für das Betriebssystem und seine Updates erforderlich ist. Vermeiden Sie außerdem das Hinzufügen oder Verschieben von Serverordnern auf externe Festplatten, da die Verbindung zu ihnen ganz einfach getrennt werden kann. In diesem Fall können Sie dann nicht mehr auf Ihre Dateien zugreifen. Stattdessen wird empfohlen, den Ordner auf einem internen Laufwerk zu erstellen.  
  
 Ein Serverordner kann nicht zu den folgenden Speicherorten hinzugefügt oder an diese verschoben werden. Wenn einer dieser Speicherorte für das Hinzufügen oder Verschieben von Serverordnern ausgewählt wird, führt dies zu einem Fehler:  
  
-   Eine Festplatte, die nicht mit dem Dateisystem NTFS oder ReFS formatiert ist  
  
-   Der Ordner "%windir%"  
  
-   Ein zugeordnetes Netzwerklaufwerk  
  
-   Ein Ordner, der einen freigegebenen Ordner enthält  
  
-   Eine Festplatte, die sich unter einem **Gerät mit Wechselmedium**befindet  
  
-   Ein Stammverzeichnis einer Festplatte (z. B. "c:"\\, "d:"\\, "e:"\\)  
  
-   Ein Unterordner eines vorhandenen freigegebenen Ordners  
  
-   Ein Mitgliedsserver unter Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle  
  
### <a name="steps-to-add-or-move-a-server-folder"></a>Schritte zum Hinzufügen oder Verschieben von Serverordnern  
  
> [!NOTE]
>  Sie müssen Serveradministrator sein, um diese Verfahren auszuführen zu können.  
  
##### <a name="to-add-a-server-folder"></a>So fügen Sie einen Serverordner hinzu  
  
1. Öffnen Sie das Dashboard.  
  
2. Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.  
  
3. Klicken Sie in **Tasks für Serverordner** auf **Ordner hinzufügen**. Dadurch wird das Assistent zum Hinzufügen von Ordnern gestartet.  
  
4. Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
   > [!NOTE]
   > - Wenn Sie mithilfe der Schaltfläche "Durchsuchen" zum Angeben des Speicherorts des Serverordners zu einem bestimmten Ordner navigieren, wird der Ordner, zu dem Sie navigiert sind, als Serverordner hinzugefügt.  
   >   -   Sie können festlegen, auf welche Serverordner über Remotewebzugriff zugegriffen werden kann. Weitere Informationen finden Sie unter [Manage access to server folders](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_1).  
  
##### <a name="to-move-a-server-folder"></a>So verschieben Sie einen Serverordner  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.  
  
3.  Wählen Sie aus der Liste der Serverordner den Ordner aus, den Sie verschieben möchten.  
  
4.  Klicken Sie im Aufgabenbereich auf **Ordner verschieben**.  
  
5.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
##  <a name="BKMK_9"></a> Fügen Sie fehlender Serverordner hinzu  
 Wenn der Server erkennt, dass ein vordefinierter Serverordner? Unternehmen, Benutzer, Clientcomputersicherungen, Sicherungen von Dateiversionsverläufen oder Ordnerumleitung? nicht mehr freigegeben ist (für aus irgendeinem Grund oder einen anderen), wird eine Warnung generiert, um den Benutzer zum Beheben dieses Problems anzuleiten. Versuchen Sie nach Möglichkeit, den Ordner aus einer Serversicherung wiederherzustellen. Wenn der Server jedoch nicht gesichert wurde, wählen Sie den fehlenden Ordner aus, und klicken Sie dann auf **Fehlenden Ordner neu erstellen**, um den Speicherort des Serverordners neu zu konfigurieren.  
  
> [!NOTE]
>  Nur vordefinierte Ordner? Unternehmen, Benutzer, Clientcomputersicherungen, Sicherungen von Dateiversionsverläufen oder Ordnerumleitung? erstellt werden können. Von Benutzern erstellte Serverordner und Medienserverordner können nicht neu erstellt werden.  
  
 Nach dem Wiederherstellen oder erneuten Erstellen des fehlenden Ordners, sollte er nicht länger als **Fehlt** aufgelistet werden.  
  
 Informationen zum Wiederherstellen von Dateien aus serversicherungen finden Sie im Abschnitt erfahren Sie mehr Informationen zum Wiederherstellen von Dateien und Ordner unter dem Thema [Manage Backup and Restore](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_11"></a> Grundlagen zu freigegebenen Ordnern  
 Es gibt mehrere Möglichkeiten, in Windows Server Essentials über ein Gerät, das mit dem Server verbunden ist, auf die freigegebenen Ordner zuzugreifen. Weitere Informationen finden Sie im Thema [Use Shared Folders](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_Shadow"></a> Grundlagen zu Schattenkopien  
 Mit Schattenkopien von Servern können Benutzer freigegebene Dateien und Ordner anzeigen, wie sie zu einem bestimmten Zeitpunkt in der Vergangenheit vorhanden waren. Der Zugriff auf frühere Versionen von Dateien oder Schattenkopien sind hilfreich, da Benutzer die folgenden Möglichkeiten haben:  
  
1. **Wiederherstellen von versehentlich gelöschten Dateien**. Wenn Sie eine Datei versehentlich löschen, können Sie eine frühere Version öffnen und diese an einen sicheren Speicherort kopieren.  
  
2. **Wiederherstellen von versehentlich überschriebenen Dateien**. Wenn Sie eine Datei versehentlich überschreiben, können Sie eine frühere Version der Datei wiederherstellen. (Die Anzahl der Versionen hängt davon ab, wie viele Momentaufnahmen Sie erstellt haben.)  
  
3. **Vergleichen der Versionen einer Datei während der Arbeit**. Sie können früheren Versionen verwenden, wenn Sie überprüfen möchten, welche Änderungen sich zwischen verschiedenen Versionen einer Datei ergeben haben.  
  
   Um Schattenkopien zu verwenden, klicken Sie über einen Clientcomputer mit der rechten Maustaste auf einen freigegebenen Serverordner und wählen **Vorherige Version wiederherstellen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Serverspeicher](Manage-Server-Storage-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
