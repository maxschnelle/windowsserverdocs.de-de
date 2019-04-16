---
title: Verwalten von Benutzerkonten in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d115697-532b-48c2-a659-9f889e235326
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 91175836e4453860b17d2655e6a5a831645de410
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-user-accounts-in-windows-server-essentials"></a>Verwalten von Benutzerkonten in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Die Seite "Benutzer" des Windows Server Essentials-Dashboards zeigt Informationen und Aufgaben, mit denen Sie die Benutzerkonten im kleinen Firmennetzwerk verwalten. Eine Übersicht über das Benutzerdashboard finden Sie unter [Dashboardübersicht](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md).  
  
  
##  <a name="BKMK_ManageAccounts"></a>Verwalten von Benutzerkonten  
 Die folgenden Themen enthalten Informationen zur Verwendung von Windows Server Essentials-Dashboards zum Verwalten von Benutzerkonten auf dem Server:  
  
-   [Hinzufügen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)  
  
-   [Entfernen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove)  
  
-   [Anzeigen von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage3)  
  
-   [Ändern des Anzeigenamens für das Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage4)  
  
-   [Aktivieren eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage5)  
  
-   [Deaktivieren eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6)  
  
-   [Grundlagen zu Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage7)  
  
-   [Verwalten von Benutzerkonten, die über das Dashboard](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)  
  
###  <a name="BKMK_Manage1"></a>Hinzufügen eines Benutzerkontos  
 Wenn Sie ein Benutzerkonto hinzufügen, der zugeordnete Benutzer kann mit dem Netzwerk anmelden, und Sie können die Benutzer die Berechtigung zum Zugriff auf Netzwerkressourcen wie z. B. freigegebene Ordner und die Remotewebzugriffs-Website erteilen. Windows Server Essentials umfasst die Add a User Account Wizard, der Ihnen hilft:  
  
-   Geben Sie einen Namen und ein Kennwort für das Benutzerkonto.  
  
-   Definieren Sie das Konto als Administrator oder Standardbenutzer.  
  
-   Wählen Sie aus der freigegebenen Ordner, die das Benutzerkonto zugreifen kann.  
  
-   Geben Sie an, wenn das Benutzerkonto über Remotezugriff auf das Netzwerk verfügt.  
  
-   Aktivieren Sie ggf. die e-Mail-Optionen.  
  
-   Weisen Sie ein Microsoft Online Services-Konto (wie Office 365-Konto in Windows Server Essentials bezeichnet), falls zutreffend.  
  
-   Zuweisen von Benutzergruppen (nur Windows Server Essentials).  
  
> [!NOTE]
>  -   Nicht-ASCII-Zeichen werden in Microsoft Azure Active Directory (Azure AD) nicht unterstützt. Verwenden Sie keine nicht-ASCII-Zeichen in Ihrem Kennwort, nicht, wenn der Server mit Azure AD integriert ist.  
> -   Die e-Mail-Optionen sind nur verfügbar, wenn Sie ein Add-In installieren, die e-Mail-Dienst bereitstellt.  
  
##### <a name="to-add-a-user-account"></a>So fügen Sie ein Benutzerkonto hinzu  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  In der **Benutzeraufgaben** Bereich, klicken Sie auf **Hinzufügen eines Benutzerkontos**. Die Add a User Account Wizard angezeigt wird.  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
###  <a name="BKMK_Remove"></a>Entfernen eines Benutzerkontos  
 Wenn Sie ein Benutzerkonto vom Server entfernen möchten, löscht ein Assistenten das ausgewählte Konto. Aus diesem Grund können Sie das Konto nicht mehr im Netzwerk anmelden oder für den Zugriff auf Netzwerkressourcen verwenden. Optional können Sie auch die Dateien für das Benutzerkonto an gleichzeitig löschen, das Konto zu entfernen. Wenn Sie nicht das Benutzerkonto dauerhaft entfernen möchten, können Sie stattdessen das Benutzerkonto deaktivieren, um den Zugriff auf Netzwerkressourcen zu unterbrechen.  
  
> [!IMPORTANT]
>  Wenn ein Benutzerkonto eine Microsoft online ist zugewiesen Konto, wenn Sie das Benutzerkonto entfernen, die online-Konto auch aus Microsoft Online Services entfernt wird und die s Benutzerdaten, einschließlich der e-Mails, unterliegen Datenaufbewahrungsrichtlinien in Microsoft Online Services. Wenn Sie die Benutzerdaten für ein Onlinekonto bewahren möchten, deaktivieren Sie das Benutzerkonto statt es zu entfernen. Weitere Informationen finden Sie unter [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
##### <a name="to-remove-a-user-account"></a>So entfernen Sie ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie entfernen möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Benutzerkonto entfernen**. Das Löschen wird a User Account Wizard angezeigt.  
  
5.  Auf der **möchten Sie die Dateien behalten? ** Seite des Assistenten können Sie die Benutzerdateien s, einschließlich der dateiverlaufssicherungen und des umgeleiteten Ordners für das Benutzerkonto zu löschen. Um den Benutzer s Dateien beibehalten, lassen Sie das Kontrollkästchen leer. Nachdem Sie Ihre Auswahl getroffen haben, klicken Sie auf **Weiter**.  
  
6.  Klicken Sie auf **Konto löschen**.  
  
> [!NOTE]
>  Wenn Sie ein Benutzerkonto entfernen, wird das Konto nicht mehr in der Liste der Benutzerkonten angezeigt. Wenn Sie die Dateien löschen möchten, löscht der Server dauerhaft den Ordner s auf die **Benutzer** Serverordner und aus der **Dateiversionsverläufen** Serverordner.  
>   
>  Wenn Sie einen integrierten e-Mail-Anbieter haben, wird auch die e-Mail-Konto, das dem Benutzerkonto zugewiesen entfernt.  
  
###  <a name="BKMK_Manage3"></a>Anzeigen von Benutzerkonten  
 Die **Benutzer** Abschnitt des Windows Server Essentials-Dashboards zeigt eine Liste der Netzwerkbenutzerkonten. Die Liste enthält auch zusätzliche Informationen zu den einzelnen Konten.  
  
##### <a name="to-view-a-list-of-user-accounts"></a>Zum Anzeigen einer Liste von Benutzerkonten  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Hauptnavigationsleiste auf **Benutzer**.  
  
3.  Das Dashboard zeigt eine aktuelle Liste der Benutzerkonten.  
  
##### <a name="to-view-or-change-properties-for-a-user-account"></a>Zum Anzeigen oder Ändern von Eigenschaften für ein Benutzerkonto  
  
1.  Wählen Sie in der Liste der Benutzerkonten das Konto für das Sie Eigenschaften anzeigen oder ändern möchten.  
  
2.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**. Die **Eigenschaften** Seite für das Benutzerkonto, das angezeigt wird.  
  
3.  Klicken Sie auf eine Registerkarte, um die Eigenschaften für diese Kontofunktion anzuzeigen.  
  
4.  Um die Änderungen zu speichern, die Sie den Eigenschaften des Benutzerkontos vornehmen, klicken Sie auf **übernehmen**.  
  
###  <a name="BKMK_Manage4"></a>Ändern des Anzeigenamens für das Benutzerkonto  
 Der Anzeigename ist der Name, der in der **Namen** Spalte auf den **Benutzer** -Seite des Dashboards. Ändern des Anzeigenamens ändert sich nicht auf den Namen Anmelde- oder -Anmeldung für ein Benutzerkonto aus.  
  
##### <a name="to-change-the-display-name-for-a-user-account"></a>So ändern Sie den Anzeigenamen für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie ändern möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**. Die **Eigenschaften** Seite für das Benutzerkonto, das angezeigt wird.  
  
5.  Auf der **allgemeine** Registerkarte, geben Sie einen neuen **Vorname** und **Nachname** für das Benutzerkonto, und klicken Sie dann auf **OK**.  
  
     Der neue Anzeigename wird in der Liste der Benutzerkonten angezeigt.  
  
###  <a name="BKMK_Manage5"></a>Aktivieren eines Benutzerkontos  
 Wenn Sie ein Benutzerkonto aktivieren, kann der zugewiesene Benutzer auf die Netzwerkressourcen Netzwerk- und melden Sie sich für die das Konto die Berechtigung, z. B. freigegebene Ordner und der Remotewebzugriff-Website besitzt.  
  
> [!NOTE]
>  Sie können nur ein Benutzerkonto aktivieren, die deaktiviert sind. Ein Benutzerkonto kann nicht aktiviert werden, nachdem Sie es vom Server entfernt.  
  
##### <a name="to-activate-a-user-account"></a>Um ein Benutzerkonto zu aktivieren.  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Listenansicht das Benutzerkonto, das Sie aktivieren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Benutzerkonto aktivieren**.  
  
5.  Klicken Sie im Bestätigungsfenster auf **Ja** Aktion zu bestätigen.  
  
> [!NOTE]
>  Nachdem Sie ein Benutzerkonto aktivieren, zeigt der Status für das Konto **Active**. Das Benutzerkonto erhält wieder dieselben Zugriffsrechte, die vor der Deaktivierung des Kontos zugewiesen waren.  
>   
>  Wenn Sie einen integrierten e-Mail-Anbieter haben, wird die e-Mail-Konto, das dem Benutzerkonto zugewiesen ebenfalls aktiviert werden.  
  
###  <a name="BKMK_Manage6"></a>Deaktivieren eines Benutzerkontos  
 Wenn Sie ein Benutzerkonto deaktivieren, wird der Zugriff auf den Server vorübergehend unterbrochen. Aus diesem Grund kann nicht der zugeordnete Benutzer das Konto verwenden, auf Netzwerkressourcen wie die freigegebenen Ordner oder die Remotewebzugriff-Website zugreifen, bis Sie das Konto aktivieren.  
  
 Wenn das Benutzerkonto ein Microsoft-Onlinekonto zugewiesen wurde, wird das Onlinekonto ebenfalls deaktiviert. Der Benutzer kann keine Ressourcen in Office 365 sowie andere Onlinedienste, die Sie abonnieren, aber die s Benutzerdaten, einschließlich der e-Mails, bleiben in Microsoft Online Services verwenden.  
  
> [!NOTE]
>  Sie können nur ein Benutzerkonto deaktivieren, die derzeit aktiv ist.  
  
##### <a name="to-deactivate-a-user-account"></a>So deaktivieren Sie ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Listenansicht das Benutzerkonto, das Sie deaktivieren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Benutzerkonto**.  
  
5.  Klicken Sie im Bestätigungsfenster auf **Ja** Aktion zu bestätigen.  
  
> [!NOTE]
>  Nachdem Sie ein Benutzerkonto deaktivieren, wird der Status für das Konto **inaktiv**.  
>   
>  Wenn Sie einen integrierten e-Mail-Anbieter haben, werden die e-Mail-Konto, das dem Benutzerkonto zugewiesen ebenfalls deaktiviert.  
  
###  <a name="BKMK_Manage7"></a>Grundlagen zu Benutzerkonten  
 Ein Benutzerkonto enthält wichtige Informationen zu Windows Server Essentials, wodurch Benutzer Zugriff auf Informationen, die auf dem Server gespeichert ist, und ermöglicht es einzelnen Benutzern zum Erstellen und verwalten ihre Dateien und Einstellungen. Benutzer können auf alle Computer im Netzwerk anmelden, wenn sie ein Windows Server Essentials-Benutzerkonto und verfügen über Berechtigungen auf einen Computer zugreifen. Benutzerzugriff auf ihre Benutzerkonten mit ihren Benutzernamen und Kennwort.  
  
 Es gibt zwei Haupttypen von Benutzerkonten. Jeder Typ bietet Benutzern einen unterschiedlichen Grad an Kontrolle über den Computer:  
  
-   **Standard** Konten für alltägliche Aufgaben konzipiert sind. Das Standardkonto schützt das Netzwerk durch die verhindert, dass Benutzer Änderungen, die auf andere Benutzer, z. B. Dateien löschen oder Ändern von Einstellungen des Netzwerks auswirkt.  
  
-   **Administrator** Konten bieten die meisten steuerungsmöglichkeiten über ein Computernetzwerk. Weisen Sie den Administrator Kontotyp nur bei Bedarf.  
  
###  <a name="BKMK_Manage8"></a>Verwalten von Benutzerkonten, die über das Dashboard  
 Windows Server Essentials ermöglicht die allgemeine administrative Aufgaben mithilfe von Windows Server Essentials-Dashboard ausführen. Standardmäßig die **Benutzer** Seite des Dashboards enthält zwei Registerkarten **Benutzer** und **Benutzergruppen**.  
  
> [!NOTE]
>  -   Wenn Sie Ihren Server, auf denen Windows Server Essentials in Office 365 ausgeführt wird integrieren, eine neue Registerkarte aufgerufen **Verteilergruppen** hinzugefügt wird der **Benutzer** -Seite des Dashboards.  
> -   In Windows Server Essentials die **Benutzer** Seite des Dashboards enthält nur eine einzelne Registerkarte: **Benutzer**.  
  
 Die **Benutzer** Registerkarte umfasst Folgendes:  
  
-   Eine Liste von Benutzerkonten, die anzeigt:  
  
    -   Der Name des Benutzers.  
  
    -   Der Anmeldename für das Benutzerkonto ein.  
  
    -   Gibt an, ob das Benutzerkonto über die Berechtigung "Zugriff überall" verfügt. An einer beliebigen Stelle Zugriffsberechtigungen für ein Benutzerkonto ist entweder **zugelassene** oder **nicht zulässig,**.  
  
    -   Gibt an, ob der Dateiverlauf für dieses Benutzerkonto von dem Server mit Windows Server Essentials verwaltet wird. Der dateiverlaufsstatus für ein Benutzerkonto ist entweder **verwaltet** oder **nicht verwaltet**.  
  
    -   Die Zugriffsebene, die dem Benutzerkonto zugewiesen ist. Sie können entweder zuweisen **Standardbenutzer** Zugriff oder **Administrator** Zugriff für ein Benutzerkonto.  
  
    -   Der Status des Benutzerkontos. Ein Benutzerkonto kann **Active**, **inaktiv**, oder **unvollständig**.  
  
    -   Wenn der Server mit Office 365 oder Windows Intune integriert ist, wird in Windows Server Essentials Microsoft-Onlinekonto angezeigt.  
  
    -   Wenn der Server mit Microsoft Office 365 integriert ist, wird in Windows Server Essentials der Status des Office 365-Kontos (in Windows Server Essentials als Microsoft-Onlinekonto bezeichnet) für das Benutzerkonto angezeigt.  
  
-   Ein Detailbereich mit zusätzlichen Informationen zum ausgewählten Benutzerkonto.  
  
-   Ein Aufgabenbereich, enthält:  
  
    -   Eine Reihe von administrativen benutzerkontoaufgaben, z. B. anzeigen und Entfernen von Benutzerkonten und Kennwörter ändern.  
  
    -   Aufgaben, mit denen Sie Global festlegen oder Ändern von Einstellungen für alle Benutzerkonten im Netzwerk.  
  
 Die folgende Tabelle beschreibt die verschiedenen benutzerkontoaufgaben, die von der **Benutzer** Registerkarte. Einige Aufgaben sind benutzerkontoabhängig und sie werden nur angezeigt, wenn Sie ein Benutzerkonto in der Liste auswählen.  
  
> [!NOTE]
>  Wenn Sie Office 365 in Windows Server Essentials integrieren, werden weitere Aufgaben verfügbar. Weitere Informationen finden Sie unter [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
### <a name="user-account-tasks-in-the-dashboard"></a>Benutzerkontoaufgaben im Dashboard  
  
|Den Namen der Aufgabe|Beschreibung|  
|---------------|-----------------|  
|Kontoeigenschaften anzeigen|Ermöglicht Ihnen das Anzeigen und Ändern der Eigenschaften des ausgewählten Benutzerkontos ein, und Berechtigungen für den Ordner für das Konto angeben.|  
|Deaktivieren Sie das Benutzerkonto|Ein Benutzerkonto, das deaktiviert ist, kann mit den Netzwerk- oder Netzwerkressourcen wie z. B. freigegebene Ordner oder Drucker anmelden.|  
|Aktivieren Sie das Benutzerkonto|Ein Benutzerkonto, das aktiviert wird mit dem Netzwerk anmelden kann und auf Netzwerkressourcen zugreifen kann gemäß den Kontoberechtigungen.|  
|Benutzerkonto entfernen|Ermöglicht Ihnen das ausgewählte Benutzerkonto zu entfernen.|  
|Ändern Sie das Kennwort des Benutzerkontos|Ermöglicht Ihnen das Netzwerkkennwort für das ausgewählte Benutzerkonto zurückzusetzen.|  
|Hinzufügen eines Benutzerkontos|Startet das Hinzufügen einer Benutzerkonten-Assistenten können Sie ein einzelnes neues Benutzerkonto erstellen, das über Standardbenutzer- oder Administratorzugriff verfügt.|  
|Ein Microsoft-Onlinekonto zuweisen|Der LAN-Benutzerkonto, das aktiviert ist hinzugefügt ein Microsoft-online-Konto.<br /><br /> Diese Aufgabe wird angezeigt, wenn der Server mit Microsoft online Services wie Office 365 integriert ist.|  
|Microsoft-Onlinekonten hinzufügen|Fügt Microsoft-Onlinekonten hinzu und ordnet sie lokalen Netzwerkbenutzerkonten.<br /><br /> Diese Aufgabe wird angezeigt, wenn der Server mit Microsoft online Services wie Office 365 integriert ist.|  
|Kennwortrichtlinie festlegen|Ermöglicht, die Sie zum Ändern der Werte des Kennworts für Ihr Netzwerk Richtlinien.|  
|Microsoft-Onlinekonten importieren|Führt einen Massenimport von Konten von Microsoft-Onlinediensten in das lokale Netzwerk aus.<br /><br /> Diese Aufgabe wird angezeigt, wenn der Server mit Microsoft online Services wie Office 365 integriert ist.|  
|Aktualisieren|Aktualisiert die Registerkarte "Benutzer".<br /><br /> Diese Aufgabe gilt für Windows Server Essentials zur Verfügung.|  
|Dateiverlaufseinstellungen ändern|Ermöglicht das Ändern der Einstellungen für Dateiversionsverlauf, z. B. sicherungshäufigkeit oder Sicherungsdauer.<br /><br /> Diese Aufgabe gilt für Windows Server Essentials zur Verfügung.|  
|Alle Remoteverbindungen exportieren|Erstellt ein. CSV-Format-Datei alle Remoteverbindungen mit dem Server, die in den letzten 30 Tagen aufgetreten sind.|  
  
##  <a name="BKMK_ManageAccess"></a>Verwalten von Kennwörtern und des Zugriffs  
 Die folgenden Themen enthalten Informationen zur Verwendung von Windows Server Essentials-Dashboards zum Verwalten von Benutzerkontokennwörtern und Benutzer der Zugriff auf die freigegebenen Ordner auf dem Server:  
  
-   [Ändern Sie oder Zurücksetzen Sie des Kennworts für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access1)  
  
-   [Was Sie über Kennwortrichtlinien wissen sollten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access3)  
  
-   [Ändern der Kennwortrichtlinie](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access4)  
  
-   [Ebene des Zugriffs auf freigegebene Ordner](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access5)  
  
-   [Behalten Sie bei und verwalten Sie des Zugriffs auf Dateien für entfernte Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access6)  
  
-   [Synchronisieren des DSRM-Kennworts mit dem netzwerkadministratorkennwort](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access7)  
  
-   [Erteilen Sie remotedesktopberechtigung für Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access8)  
  
-   [Ermöglichen Sie Benutzern den Zugriff auf Ressourcen auf dem server](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access9)  
  
-   [RAS-Berechtigungen für ein Benutzerkonto ändern](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access10)  
  
-   [Ändern Sie VPN-Berechtigungen für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access11)  
  
-   [Ändern des Zugriffs auf interne freigegebene Ordner für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access12)  
  
-   [Gewähren Sie Benutzerkonten, eine Remotedesktopsitzung mit ihrem Computer herzustellen.](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access13)  
  
###  <a name="BKMK_Access1"></a>Ändern Sie oder Zurücksetzen Sie des Kennworts für ein Benutzerkonto  
 Gehen Sie folgendermaßen vor, um zu ändern oder Zurücksetzen eines Benutzerkennworts für das Konto.  
  
##### <a name="to-reset-the-password-for-a-user-account"></a>Zum Zurücksetzen des Kennworts für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie zurücksetzen möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **ändern Sie das Kennwort des Benutzerkontos**. Der Änderung Benutzerkonten Kennwort-Assistent wird angezeigt.  
  
5.  Geben Sie ein neues Kennwort für das Benutzerkonto ein, und geben Sie das Kennwort erneut ein, um es zu bestätigen.  
  
6.  Klicken Sie auf **Kennwort ändern**.  
  
7.  Bereitstellen Sie das neue Kennwort für den Benutzer.  
  
    > [!IMPORTANT]
    >  -   Sie können möglicherweise nicht Ihr Kennwort ändern, wenn die Kennwortrichtlinie für Ihr Konto, um eingerichtet ist **Kennwörter niemals ablaufen**.  
    > -   Nicht-ASCII-Zeichen werden in Azure AD nicht unterstützt. Aus diesem Grund, wenn der Server mit Azure AD integriert ist, verwenden Sie keine nicht-ASCII-Zeichen in Ihrem Kennwort.  
    > -   Wenn der Benutzer ein Microsoft-Onlinekonto (in Windows Server Essentials als ein Office 365-Konto "bezeichnet) zugewiesen ist, wird das Kennwort mit dem onlinekontokennwort synchronisiert. Der Benutzer wird das neue Kennwort verwenden, melden Sie sich auf dem Server, oder melden Sie sich bei Office 365. Weitere Informationen finden Sie unter [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
###  <a name="BKMK_Access3"></a>Was Sie über Kennwortrichtlinien wissen sollten  
 Die Kennwortrichtlinie ist ein Satz von Regeln, in denen Benutzer erstellen und verwenden Sie Kennwörter. Die Richtlinie wird verhindert nicht autorisierten Zugriff auf Benutzerdaten und andere Informationen, die auf dem Server gespeichert sind. Die Kennwortrichtlinie wird auf alle Benutzerkonten angewendet, die auf das Netzwerk zugreifen.  
  
 Die Windows Server Essentials-Kennwortrichtlinie besteht aus drei primären Elementen wie folgt:  
  
-   **Kennwortlänge**.  Je länger ein Kennwort ist, desto sicherer ist. Leere Kennwörter sind nicht sicher.  
  
-   **Kennwortkomplexität**.  Komplexe Kennwörter enthalten eine Mischung aus Groß- und Kleinbuchstaben (a-Z, A-Z), basieren Sie Zahlen (0-9) und nicht alphabetischen Zeichen (z. b.!, @, #, _,-). Komplexe Kennwörter sind weniger anfällig für nicht autorisierten Zugriff. Kennwörter, die Benutzernamen, Geburtsdaten oder andere persönliche Informationen enthalten, bieten keine angemessene Sicherheit.  
  
-   **Kennwortalter**.  Windows Server Essentials erfordert, dass Benutzer ihr Kennwort mindestens alle 180 Tage ändern. Optional können Sie Kennwörter nicht ablaufen.  
  
 Zum Implementieren einer Kennwortrichtlinie in Ihrem Computernetzwerk zu vereinfachen, bietet Windows Server Essentials ein einfaches Tool, mit dem Sie festlegen oder Ändern der Kennwortrichtlinie auf eines der folgenden vier vordefinierten Richtlinienprofile:  
  
-   **Unsichere**.  Benutzer können jedes Kennwort angeben, die nicht leer ist.  
  
-   **Mittel**.  Diese Kennwörter müssen mindestens 5 Zeichen enthalten. Ein komplexes Kennwort ist nicht erforderlich.  
  
-   **Mittlere starke**.  Diese Kennwörter müssen mindestens 5 Zeichen enthalten und Buchstaben, Zahlen und Sonderzeichen enthalten.  
  
-   **Starke**.  Diese Kennwörter müssen mindestens 7 Zeichen enthalten und Buchstaben, Zahlen und Sonderzeichen enthalten. Diese Kennwörter sind sicherer, aber schwerer zu merken.  
  
    > [!NOTE]
    >  Kennwörter können nicht den Benutzer oder die e-Mail-Adresse enthalten.  
    >   
    >  Wenn Sie mit Office 365 integrieren, erzwingt die Integration der **starke** Kennwortrichtlinie und aktualisiert die Richtlinie, um die folgenden Anforderungen einzubeziehen:  
    >   
    >  -   Kennwörter müssen 8-16 Zeichen enthalten.  
    > -   Kennwörter können nicht über ein Leerzeichen oder den Namen des Office 365 e-Mail enthalten.  
  
 Standardmäßig wird die Server-Installation die standardmäßige Kennwortrichtlinie auf die **starke** Option.  
  
###  <a name="BKMK_Access4"></a>Ändern der Kennwortrichtlinie  
 Verwenden Sie das folgende Verfahren zum Festlegen oder Ändern der Kennwortrichtlinie auf eine der vier vordefinierten Richtlinienprofile.  
  
##### <a name="to-change-the-password-policy"></a>So ändern Sie die Kennwortrichtlinie  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf **Benutzer**.  
  
2.  In der **Benutzeraufgaben** Bereich, klicken Sie auf **Kennwortrichtlinie festlegen**.  
  
3.  Auf der **Ändern der Kennwortrichtlinie** Bildschirm, legen Sie den Grad der kennwortsicherheit durch Verschieben des Schiebereglers.  
  
     Microsoft empfiehlt, dass Sie die kennwortsicherheit auf **starke**.  
  
    > [!NOTE]
    >  Sie können auch auswählen, als Option **Kennwörter niemals ablaufen**. Diese Einstellung ist weniger sicher und daher nicht empfohlen.  
  
4.  Klicken Sie auf **Richtlinie ändern**.  
  
###  <a name="BKMK_Access5"></a>Ebene des Zugriffs auf freigegebene Ordner  
 Als bewährte Methode sollten Sie die restriktivsten verfügbaren Berechtigungen zuweisen, die weiterhin Benutzer erforderliche Aufgaben ausführen können.  
  
 Sie haben drei zugriffseinstellungen für die freigegebenen Ordner auf dem Server verfügbar:  
  
-   **Lese-/Schreibzugriff**.  Wählen Sie diese Einstellung, wenn Sie möchten, dass das Benutzerkonto die Berechtigung zum Erstellen, ändern und löschen Sie alle Dateien im freigegebenen Ordner.  
  
-   **Schreibgeschützt**.  Wählen Sie diese Einstellung, wenn Sie, dass das Benutzerkonto die Berechtigung für die Dateien im freigegebenen Ordner nur lesen möchten. Benutzerkonten mit schreibgeschützten Zugriff können keine erstellen, ändern oder löschen Sie alle Dateien im freigegebenen Ordner.  
  
-   **Kein Zugriff**.  Wählen Sie diese Einstellung, wenn Sie nicht, dass das Benutzerkonto auf Dateien im freigegebenen Ordner zugreifen möchten.  
  
###  <a name="BKMK_Access6"></a>Behalten Sie bei und verwalten Sie des Zugriffs auf Dateien für entfernte Benutzerkonten  
 Der Netzwerkadministrator kann ein Benutzerkonto entfernen und Auswählen der Benutzer s-Dateien für die zukünftige Verwendung beibehalten. In diesem Szenario kann das entfernte Benutzerkonto nicht mehr mit dem Netzwerk anmelden verwendet werden; die Dateien für den Benutzer werden jedoch in einem freigegebenen Ordner gespeichert werden, der mit einem anderen Benutzer verwendet werden kann.  
  
> [!IMPORTANT]
>  Beachten Sie, dass wenn Sie ein Benutzerkonto, die ein Microsoft-Onlinekonto zugewiesen wurde entfernen, auch das Onlinekonto entfernt wird und die Benutzerdaten, einschließlich der e-Mails, unterliegen den Datenaufbewahrungsrichtlinien in Microsoft Online Services. Um die Benutzerdaten für ein Onlinekonto zu bewahren, deaktivieren Sie das Benutzerkonto statt es zu entfernen. Weitere Informationen finden Sie unter [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
##### <a name="to-remove-a-user-account-but-retain-access-to-the-user-s-files"></a>Zum Entfernen eines Benutzerkontos bewahren aber den Zugriff auf die Dateien des Benutzers s  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie entfernen möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Benutzerkonto entfernen**. Das Löschen wird a User Account Wizard angezeigt.  
  
5.  Auf der **möchten Sie die Dateien behalten? ** Seite, stellen Sie sicher, dass die **löschen Sie die Dateien, einschließlich der dateiverlaufssicherungen und umgeleiteten Ordner für dieses Benutzerkonto** Kontrollkästchen deaktiviert ist, und klicken Sie dann auf **Weiter**.  
  
     Es wird eine Bestätigungsseite Warnung, die das Konto löschen, aber die Dateien behalten.  
  
6.  Klicken Sie auf **Konto löschen** So entfernen Sie das Benutzerkonto.  
  
 Nachdem das Benutzerkonto entfernt wurde, kann der Administrator einem anderen Benutzerkonto den Zugriff auf dem freigegebenen Ordner erteilen.  
  
##### <a name="to-give-a-user-account-permission-to-access-a-shared-folder"></a>Gewähren Sie eine Benutzerkonto die Berechtigung zum Zugriff auf einen freigegebenen Ordner  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Speicher**, und klicken Sie dann auf die **Serverordner** Registerkarte.  
  
3.  Wählen Sie in der Liste der Ordner, der **Benutzer** Ordner.  
  
4.  In der **Benutzeraufgaben** Bereich, klicken Sie auf **öffnen Sie den Ordner**. Windows-Explorer wird geöffnet und zeigt den Inhalt der **Benutzer** Ordner.  
  
5.  Mit der rechten Maustaste in des Ordners für das Benutzerkonto an, die Sie freigeben möchten, und klicken Sie dann auf **Eigenschaften**.  
  
6.  In **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, klicken Sie auf die **Freigabe** Registerkarte, und klicken Sie dann auf **Freigabe**.  
  
7.  In der **Dateifreigabe** Fenster geben, oder wählen Sie den Benutzerkontonamen, mit denen Sie den Ordner frei, und klicken Sie dann auf möchten **hinzufügen**.  
  
8.  Wählen Sie die **Berechtigungsstufe** möchten, dass das Benutzerkonto, und klicken Sie dann auf **Freigabe**.  
  
###  <a name="BKMK_Access7"></a>Synchronisieren des DSRM-Kennworts mit dem netzwerkadministratorkennwort  
 Directory Services-Wiederherstellungsmodus (DSRM) ist eine spezielle Startmethode zum Reparieren oder Wiederherstellen von Active Directory. Das Betriebssystem verwendet die Verzeichnisdienstwiederherstellung für auf dem Computer anmelden, wenn Active Directory fehlschlägt oder wiederhergestellt werden muss. Wenn Ihr netzwerkadministratorkennwort und das DSRM-Kennwort unterscheiden, wird die Verzeichnisdienstwiederherstellung nicht geladen.  
  
 Bei einer sauberen, erstmalige Installation von Windows Server Essentials setzt das Programm das DSRM-Kennwort auf Netzwerk das Kennwort des Administratorkontos, das Sie während des Setups oder in der Antwortdatei für die Migration angeben. Wenn Sie Ihr netzwerkadministratorkennwort (wie in der Regel alle 60 Tage für erhöhte Sicherheit empfohlen) ändern, wird die Änderung des Kennworts nicht an die Verzeichnisdienstwiederherstellung weitergeleitet. Dies führt zu einem kennwortkonflikt. In diesem Fall können Sie die folgenden Lösungen verwenden, manuell oder automatisch synchronisieren Ihrer s netzwerkadministratorkennwort mit dem DSRM-Kennwort.  
  
##### <a name="to-manually-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>So synchronisieren Sie das DSRM-Kennwort mit einem netzwerkadministratorkonto manuell  
  
1.  Führen Sie an einer Eingabeaufforderung `ntdsutil.exe` das Tool "Ntdsutil" zu öffnen.  
  
2.  Geben Sie zum Zurücksetzen des DSRM-Kennworts **Set Dsrm-Kennwort**.  
  
3.  Um das DSRM-Kennwort auf einem Domänencontroller mit dem aktuellen netzwerkadministratorkonto s zu synchronisieren, geben Sie Folgendes ein:  
  
     **Synchronisieren von Domänenkonto** *< aktuelles_netzwerkadministratorkonto >*, und drücken Sie dann die EINGABETASTE.  
  
 Da Sie in regelmäßigen Abständen ändern, werden das Kennwort für das netzwerkadministratorkonto, um sicherzustellen, dass das DSRM-Kennwort ist immer das aktuelle Kennwort des Netzwerkadministrators identisch, es wird empfohlen, dass Sie automatisch eine Aufgabe zu erstellen, synchronisieren Sie das DSRM-Kennwort mit dem netzwerkadministratorkennwort täglich.  
  
##### <a name="to-automatically-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>Um das DSRM-Kennwort mit einem netzwerkadministratorkonto automatisch zu synchronisieren.  
  
1.  Öffnen Sie auf dem Server **Verwaltung**, und doppelklicken Sie dann auf **Aufgabenplanung**.  
  
2.  In der Aufgabenplanung **Aktionen** Bereich, klicken Sie auf **Task erstellen**.  
  
3.  In den **Namen** Textfeld, geben Sie einen Namen für die Aufgabe, z. B. **AutoSync DSRM-Kennwort**, und wählen Sie dann die **mit höchsten Berechtigungen ausführen** Option.  
  
4.  Definieren Sie, wann die Aufgabe ausgeführt werden soll:  
  
    1.  In der **Task erstellen** Dialogfeld, klicken Sie auf die **Trigger** Registerkarte, und klicken Sie dann auf **neu**.  
  
    2.  In der **neuer Trigger** Dialogfeld Wählen Sie die Häufigkeit aus, geben das Wiederholungsintervall an, und wählen Sie eine Startzeit.  
  
        > [!NOTE]
        >  Als bewährte Methode sollten Sie den Task täglich während der Geschäftszeiten ausführen festlegen.  
  
    3.  Klicken Sie auf **OK** um die Änderungen zu speichern und wieder die **Task erstellen** Dialogfeld.  
  
5.  Definieren Sie die Aufgabenaktionen:  
  
    1.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie dann auf **neu**. Die **neue Aktion** Dialogfeld wird angezeigt.  
  
    2.  In der **Aktion** auf **Programm starten**, und wechseln Sie zu **C:\WINDOWS\SYSTEM32\ntdsutil.exe**.  
  
    3.  In der **Argumente hinzufügen**(optional) Text Feld, geben Sie Folgendes ein (Sie müssen die Anführungszeichen einschließen): **Dsrm-Kennwort-Synchronisierung vom Domänenkonto SBS_network_administrator_account Q Q festlegen** , in denen *SBS_network_administrator_account* ist der Name des Administrator s aktuellen Netzwerk.  
  
6.  Klicken Sie auf **OK** zweimal, um die Aufgabe zu speichern und schließen Sie die **Task erstellen** Dialogfeld. Die neue Aufgabe angezeigt wird, der **aktive Tasks** Abschnitt **Taskplan**.  
  
###  <a name="BKMK_Access8"></a>Erteilen Sie remotedesktopberechtigung für Benutzerkonten  
 In der Standardinstallation von Windows Server Essentials verfügen Netzwerkbenutzer nicht über die Berechtigung zum Herstellen einer Remoteverbindung zu Computern oder anderen Ressourcen im Netzwerk.  
  
 Bevor die Netzwerkbenutzer eine Remoteverbindung mit Netzwerkressourcen herstellen können, müssen Sie zunächst "Zugriff überall" einrichten. Nach dem Einrichten von "Zugriff überall" können Benutzer über ein Gerät an einem Ort mit Internetzugang Dateien, Anwendungen und Computer im Unternehmensnetzwerk zugreifen.  
  
 Der "Zugriff überall" den Assistenten zum einrichten können Sie zwei Methoden des Remotezugriffs zu aktivieren:  
  
-   Virtuelles privates Netzwerk (VPN)  
  
-   Remote Web Access  
  
 Wenn Sie den Assistenten ausführen, können Sie auch "Zugriff überall" für alle aktuellen und neu hinzugefügten Benutzerkonten zu ermöglichen.  
  
 Öffnen Sie das Dashboard, um "Zugriff überall" einrichten, **Home** auf **SETUP**, und klicken Sie dann auf **"Zugriff überall" einrichten**.  
  
 Weitere Informationen zu "Zugriff überall" finden Sie unter [Manage Anywhere Access](Manage-Anywhere-Access-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_Access9"></a>Ermöglichen Sie Benutzern den Zugriff auf Ressourcen auf dem server  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials oder Windows Server Essentials oder auf einem Server mit Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials Experience-Rolle.  
  
 Wenn Benutzer Remotezugriff verwenden und/oder über einzelne Benutzerkonten verfügen, klicken Sie nach dem Verbinden eines Computers mit dem Server werden sollen, können Sie neues Netzwerk-Benutzerkonten für die Benutzer die Computer im Netzwerk auf dem Server erstellen mithilfe des Dashboards. Weitere Informationen zum Erstellen eines Benutzerkontos finden Sie unter [Hinzufügen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1). Nach dem Erstellen von Benutzerkonten, müssen Sie das Netzwerk Benutzer Benutzername und Kennwort für die Benutzer des Clientcomputers angeben, damit sie Ressourcen auf dem Server zugreifen können, mit dem Launchpad.  
  
 Für jedes Benutzerkonto, das Sie erstellen können Sie den Zugriff für Folgendes über die Benutzer Eigenschaften festlegen:  
  
-   **Freigegebene Ordner**.  Standardmäßig verfügen Netzwerkadministratoren über **Lese-/Schreibzugriff** über die Berechtigung für alle freigegebenen Ordner und Standardbenutzerkonten **Read-only** Berechtigungen für den Ordner für Unternehmen. Wenn das Medienstreaming aktiviert ist, können Sie Ordnerzugriffsberechtigungen für einzelne Standardbenutzerkonten zuweisen, für die folgenden Ordner freigegebenen: **Musik**, **Bilder**, **TV-Aufzeichnungen**, und **Videos**. Sie können Berechtigungen für Benutzerkonten zum Zugriff auf freigegebene Ordner auf Festlegen der **freigegebene Ordner** auf der Registerkarte Eigenschaften des Benutzerkontos.  
  
-   **Zugriff überall**.  Standardmäßig können Netzwerkadministratoren entweder VPN oder den Remotezugriff auf Serverressourcen zugreifen. Für Standardbenutzerkonten müssen Sie die Berechtigungen für Benutzerkonten festlegen, auf die **"Zugriff überall"** Registerkarte.  
  
-   **Zugriff auf den Computer**.  Standardmäßig können Netzwerkadministratoren auf alle Computer im Netzwerk zugreifen. Allerdings für Standardbenutzerkonten können, legen Sie Berechtigungen für einzelne Benutzerkonten für den Zugriff auf Computer im Netzwerk auf die **Zugriff auf den Computer** auf der Registerkarte Eigenschaften des Benutzerkontos.  
  
##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012-r2"></a>So bearbeiten Sie die Eigenschaften von Benutzerkonten in Windows Server Essentials 2012 R2  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie bearbeiten möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**.  
  
5.  In der **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, gehen Sie folgendermaßen vor:  
  
    1.  Auf der **freigegebene Ordner** Registerkarte, legen Sie die entsprechenden Berechtigungen für jeden freigegebenen Ordner nach Bedarf fest.  
  
    2.  Auf der **"Zugriff überall"** Registerkarte:  
  
        1.  Einen Benutzer eine Verbindung mit dem Server über VPN, Aktivieren der **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen.  
  
        2.  Damit einen Benutzer mithilfe von Remote Web Access eine Verbindung mit dem Server herstellen kann, wählen Sie die **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen** Kontrollkästchen.  
  
    3.  Auf der **Zugriff auf den Computer** Registerkarte, wählen Sie die Netzwerk-Computer, die Benutzer den Zugriff auf werden soll.  
  
##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012"></a>So bearbeiten Sie die Eigenschaften von Benutzerkonten in Windows Server Essentials 2012  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie bearbeiten möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In der **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, gehen Sie folgendermaßen vor:  
  
    1.  Auf der **allgemeine** Registerkarte **Benutzer kann integritätswarnungen für das Netzwerk anzeigen** Wenn das Benutzerkonto, das Netzwerk Integritätsberichte zugreifen muss.  
  
    2.  Auf der **freigegebene Ordner** Registerkarte, legen Sie die entsprechenden Berechtigungen für jeden freigegebenen Ordner nach Bedarf fest.  
  
    3.  Auf der **"Zugriff überall"** Registerkarte:  
  
        1.  Einen Benutzer eine Verbindung mit dem Server über VPN, Aktivieren der **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen.  
  
        2.  Damit einen Benutzer mithilfe von Remote Web Access eine Verbindung mit dem Server herstellen kann, wählen Sie die **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen** Kontrollkästchen.  
  
    4.  Auf der **Zugriff auf den Computer** Registerkarte, wählen Sie die Netzwerk-Computer, die Benutzer den Zugriff auf werden soll.  
  
###  <a name="BKMK_Access10"></a>RAS-Berechtigungen für ein Benutzerkonto ändern  
 Ein Benutzer kann auf dem Server von einem Remotestandort aus über ein virtuelles privates Netzwerk (VPN), Remote Web Access oder andere Webdienstanwendungen Ressourcen zugreifen. Standardmäßig werden RAS-Berechtigungen für Netzwerkbenutzer aktiviert, wenn Sie über das Dashboard "Zugriff überall" in Windows Server Essentials konfigurieren.  
  
##### <a name="to-change-remote-access-permissions-for-a-user-account"></a>So ändern Sie RAS-Berechtigungen für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie ändern möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**. Die **Eigenschaften** Seite für das Benutzerkonto, das angezeigt wird.  
  
5.  Auf der **"Zugriff überall"** Registerkarte, gehen Sie folgendermaßen vor:  
  
    -   Wählen Sie die **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen, um einem Benutzer ermöglichen, mit dem Server über VPN herzustellen.  
  
    -   Wählen Sie die **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen** Kontrollkästchen, um einen Benutzer mithilfe von Remote Web Access eine Verbindung mit dem Server herstellen kann.  
  
6.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
###  <a name="BKMK_Access11"></a>Ändern Sie VPN-Berechtigungen für ein Benutzerkonto  
 Sie können ein virtuelles privates Netzwerk (VPN) verwenden, Windows Server Essentials herstellen und Zugriff auf alle Ressourcen, die auf dem Server gespeichert sind. Dies ist besonders hilfreich, wenn Sie einen Clientcomputer verfügen, der mit Netzwerkkonten eingerichtet ist, die für die Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung verwendet werden können. Alle neu erstellten Benutzerkonten auf dem gehosteten Windows Server Essentials-Server müssen auf dem Client-Computer zum ersten Mal anmelden VPN verwenden.  
  
##### <a name="to-change-vpn-permissions-for-network-users"></a>So ändern Sie die VPN-Berechtigungen für Netzwerkbenutzer  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie Remotezugriff auf den Desktop gewähren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In der **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, klicken Sie auf die **"Zugriff überall"** Registerkarte.  
  
6.  Auf der **"Zugriff überall"** Tab, um einem Benutzer ermöglichen, mit dem Server verbinden, über ein VPN, wählen Sie die **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen.  
  
7.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
###  <a name="BKMK_Access12"></a>Ändern des Zugriffs auf interne freigegebene Ordner für ein Benutzerkonto  
 Sie können den Zugriff auf alle freigegebenen Ordner auf dem Server verwalten, mithilfe der Tasks auf der **Serverordner** Dashboard-Registerkarte. Standardmäßig werden die folgenden Serverordner erstellt, bei der Installation von Windows Server Essentials:  
  
-   **Clientcomputersicherungen**.  Verwendet zum Speichern von Sicherungen des Clientcomputers von Windows Server-Sicherung erstellt. Dieser Serverordner ist nicht freigegeben.  
  
-   **Unternehmen**.  Zum Speichern und Zugriff auf Dokumente, die im Zusammenhang mit Ihrer Organisation von Benutzern im Netzwerk verwendet.  
  
-   **Von dateiversionsverläufen**.  Windows Server Essentials speichert standardmäßig dateisicherungen, die mit dem Dateiversionsverlauf erstellt. Dieser Serverordner ist nicht freigegeben.  
  
-   **Ordnerumleitung**.  Verwendet zum Speichern und Zugreifen auf Ordner, die vom Benutzer im Netzwerk für die ordnerumleitung eingerichtet werden. Dieser Serverordner ist nicht freigegeben.  
  
-   **Musik**.  Zum Speichern und Musikdateien durch Benutzer im Netzwerk zugreifen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.  
  
-   **Bilder**.  Zum Speichern und Bilder von Benutzern im Netzwerk zugreifen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.  
  
-   **TV-Aufzeichnungen**.  Zum Speichern und aufgezeichnete Fernsehsendungen von Netzwerkbenutzern zugreifen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.  
  
-   **Videos**.  Zum Speichern und Videos von Netzwerkbenutzern zugreifen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.  
  
-   **Benutzer**.  Speichern und Zugreifen auf Dateien durch Benutzer im Netzwerk verwendet. Ein Benutzerspezifischer Ordner wird automatisch generiert, der **Benutzer** Serverordner für jedes Netzwerkbenutzerkonto, die Sie erstellen.  
  
##### <a name="to-change-access-to-a-shared-folder-for-a-user-account"></a>So ändern Sie den Zugriff auf einen freigegebenen Ordner für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Navigieren Sie zu, und wählen Sie den Serverordner für den Sie Berechtigungen ändern möchten.  
  
4.  Klicken Sie im Aufgabenbereich auf **Ordnereigenschaften anzeigen**.  
  
5.  In **< FolderName\ > Eigenschaften**, klicken Sie auf **Freigabe**, und wählen Sie die entsprechende Zugriffsebene für die aufgeführten Benutzerkonten aus, und klicken Sie dann auf **übernehmen**.  
  
    > [!NOTE]
    >  Die Freigabeberechtigungen für kann nicht geändert **Dateiversionsverläufen**, **Ordnerumleitung**, und **Benutzer** Serverordner. Die Ordnereigenschaften dieser Serverordner enthalten daher keine **Freigabe** Registerkarte.  
  
###  <a name="BKMK_Access13"></a>Gewähren Sie Benutzerkonten, eine Remotedesktopsitzung mit ihrem Computer herzustellen.  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials oder Windows Server Essentials oder auf einem Server mit Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials Experience-Rolle.  
  
 Der Netzwerkadministrator kann Netzwerkbenutzer Berechtigungen erteilen, mit denen auf den Computern von einem Remotestandort aus zugreifen können.  
  
##### <a name="to-enable-users-to-access-their-network-computers-from-a-remote-location"></a>Damit Benutzer auf den Computern von einem Remotestandort aus zugreifen können  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie für den Remotezugriff auf den Desktop gewähren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In der **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, klicken Sie auf die **Zugriff auf den Computer** Registerkarte.  
  
6.  Wählen Sie die Computer, die Sie möchten, dass dieses Benutzerkonto Remote zugreifen, und klicken Sie auf der Lage **OK**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md)  
  
-   [Herstellen einer Verbindung](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
