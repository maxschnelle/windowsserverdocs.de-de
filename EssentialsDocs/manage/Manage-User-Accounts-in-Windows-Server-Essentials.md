---
title: Verwalten von Benutzerkonten in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 0d115697-532b-48c2-a659-9f889e235326
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 60b37cb2945ca12f03b27a4367edff6eb0fe4746
ms.sourcegitcommit: 34f9577ef32cbdc7ef96040caabc9d83517f9b79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/08/2020
ms.locfileid: "89554483"
---
# <a name="manage-user-accounts-in-windows-server-essentials"></a>Verwalten von Benutzerkonten in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die Seite "Benutzer" des Windows Server Essentials-Dashboards zeigt Informationen und Aufgaben zentral an, die Sie dabei unterstützen, die Benutzerkonten im kleinen Firmennetzwerk zu verwalten. Eine Übersicht über das Benutzer Dashboard finden Sie unter [Übersicht](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)über das Dashboard.


##  <a name="managing-user-accounts"></a><a name="BKMK_ManageAccounts"></a> Verwalten von Benutzerkonten
 Die folgenden Themen enthalten Informationen zur Verwendung des Windows Server Essentials-Dashboards zum Verwalten der Benutzerkonten auf dem Server:

-   [Benutzerkonto hinzufügen](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)

-   [Entfernen von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove)

-   [Anzeigen von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage3)

-   [Ändern des Anzeigenamens für Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage4)

-   [Aktivieren von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage5)

-   [Deaktivieren von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6)

-   [Grundlagen zu Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage7)

-   [Verwalten von Benutzerkonten mithilfe des Dashboards](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)

###  <a name="add-a-user-account"></a><a name="BKMK_Manage1"></a> Benutzerkonto hinzufügen
 Wenn Sie ein Benutzerkonto hinzufügen, kann sich der zugewiesene Benutzer am Netzwerk anmelden, und Sie können dem Benutzer dann die Berechtigung für den Zugriff auf Netzwerkressourcen erteilen, z. B. auf freigegebene Ordner und die Website für den Remotewebzugriff. Windows Server Essentials umfasst den Assistenten zum Hinzufügen von Benutzerkonten, der Ihnen bei folgenden Aufgaben hilft:

-   Bereitstellen eines Namen und Kennworts für das Benutzerkonto.

-   Definieren des Kontos als Administrator oder Standardbenutzer.

-   Auswählen der freigegebenen Ordner, auf die das Benutzerkonto zugreifen kann.

-   Angeben, ob das Benutzerkonto über Remotezugriff auf das Netzwerk verfügt.

-   Auswählen von E-Mail-Optionen, falls zutreffend.

-   Weisen Sie ggf. ein Microsoft Online Services-Konto (als Microsoft 365 Konto in Windows Server Essentials bezeichnet) zu.

-   Zuweisen von Benutzergruppen (nur Windows Server Essentials).

> [!NOTE]
> - Nicht-ASCII-Zeichen werden in Microsoft Azure Active Directory (Azure AD) nicht unterstützt. Verwenden Sie keine nicht-ASCII-Zeichen in Ihrem Kennwort, wenn der Server in Azure AD integriert ist.
>   -   Die E-Mail-Optionen sind nur verfügbar, wenn Sie ein Add-In installieren, das den E-Mail-Dienst bereitstellt.

##### <a name="to-add-a-user-account"></a>So fügen Sie ein Benutzerkonto hinzu

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Klicken Sie im Bereich  **Tasks für Benutzer** auf **Benutzerkonto hinzufügen**. Der Assistent für das Hinzufügen eines Benutzerkontos wird angezeigt.

4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

###  <a name="remove-a-user-account"></a><a name="BKMK_Remove"></a> Entfernen eines Benutzerkontos
 Wenn Sie das Entfernen eines Benutzerkontos vom Server gewählt haben, wird das ausgewählte Konto von einem Assistenten gelöscht. Deshalb können Sie sich nicht länger über das Konto am Netzwerk anmelden oder es für den Zugriff auf eine der Netzwerkressourcen verwenden. Optional können Sie auch die Dateien für das Benutzerkonto zusammen mit dem zu entfernenden Benutzerkonto löschen. Wen das Benutzerkonto nicht dauerhaft gelöscht werden soll, können Sie das Benutzerkonto deaktivieren, anstatt den Zugriff auf Netzwerkressourcen einzustellen.

> [!IMPORTANT]
>  Wenn einem Benutzerkonto ein Microsoft-Onlinekonto zugewiesen ist, wird beim Entfernen des Benutzerkontos auch das Onlinekonto aus Microsoft Online Services entfernt, und die Daten des Benutzers, einschließlich der e-Mails, unterliegen den Daten Aufbewahrungs Richtlinien in Microsoft Online Services. Wenn Sie die Benutzerdaten für ein Onlinekonto bewahren möchten, deaktivieren Sie das Benutzerkonto, anstatt es zu entfernen. Weitere Informationen finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

##### <a name="to-remove-a-user-account"></a>So entfernen Sie ein Benutzerkonto

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Wählen Sie in der Liste der Benutzerkonten das zu entfernende Benutzerkonto aus.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Benutzerkonto entfernen**. Der Assistent zum Löschen eines Benutzerkontos wird angezeigt.

5.  Auf der Seite möchten **Sie die Dateien behalten?** des Assistenten können Sie die Dateien des Benutzers löschen, einschließlich der Sicherungen von Datei Versions Verläufen und des umgeleiteten Ordners für das Benutzerkonto. Lassen Sie das Kontrollkästchen leer, um die Dateien des Benutzers beizubehalten. Nachdem Sie die Auswahl getroffen haben, klicken Sie auf **Weiter**.

6.  Klicken Sie auf **Konto löschen**.

> [!NOTE]
>  Nachdem Sie ein Benutzerkonto entfernt haben, wird das Konto nicht mehr in der Liste der Benutzerkonten angezeigt. Wenn Sie die Dateien löschen möchten, löscht der Server den Ordner des Benutzers dauerhaft aus dem Server Ordner **Benutzer** und aus dem Server Ordner **Sicherungen von Datei** Versions Verläufen.
>
>  Wenn Sie über einen integrierten E-Mail-Anbieter verfügen, wird das E-Mail-Konto, das dem Benutzerkonto zugewiesen ist, ebenfalls entfernt.

###  <a name="view-user-accounts"></a><a name="BKMK_Manage3"></a> Anzeigen von Benutzerkonten
 Der Abschnitt **Benutzer** des Windows Server Essentials-Dashboards zeigt eine Liste der Netzwerkbenutzerkonten an. Die Liste enthält auch zusätzliche Informationen zu den einzelnen Konten.

##### <a name="to-view-a-list-of-user-accounts"></a>So zeigen Sie eine Liste von Benutzerkonten an

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Hauptnavigationsleiste auf **Benutzer**.

3.  Das Dashboard zeigt eine aktuelle Liste von Benutzerkonten an.

##### <a name="to-view-or-change-properties-for-a-user-account"></a>So zeigen Sie Eigenschaften eines Benutzerkontos an oder ändern diese

1.  Wählen Sie in der Liste der Benutzerkonten das Konto aus, für das Sie Eigenschaften anzeigen oder ändern möchten.

2.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Konto Eigenschaften anzeigen**. Die Seite **Eigenschaften** für das Benutzerkonto wird angezeigt.

3.  Klicken Sie auf eine Registerkarte, um die Eigenschaften für diese Kontofunktion anzuzeigen.

4.  Um die Änderungen zu speichern, die Sie an den Eigenschaften des Benutzerkontos vorgenommen haben, klicken Sie auf **Übernehmen**.

###  <a name="change-the-display-name-for-the-user-account"></a><a name="BKMK_Manage4"></a> Ändern Sie den anzeigen Amen für das Benutzerkonto.
 Der Anzeigename ist der Name, der in der Spalte **Name** auf der Seite **Benutzer** des Dashboards angezeigt wird. Durch die Änderung des Anzeigenamens ändert sich nicht der Name für die Anmeldung an einem Benutzerkonto.

##### <a name="to-change-the-display-name-for-a-user-account"></a>So ändern Sie den Anzeigenamen für Benutzerkonten

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Wählen Sie in der Liste von Benutzerkonten das Benutzerkonto aus, das Sie ändern möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Konto Eigenschaften anzeigen**. Die Seite **Eigenschaften** für das Benutzerkonto wird angezeigt.

5.  Geben Sie auf der Registerkarte **Allgemein** einen neuen **Vornamen** und **Nachnamen** für das Benutzerkonto ein, und klicken Sie dann auf **OK**.

     Der neue Anzeigename wird in der Liste der Benutzerkonten angezeigt.

###  <a name="activate-a-user-account"></a><a name="BKMK_Manage5"></a> Aktivieren eines Benutzerkontos
 Wenn Sie ein Benutzerkonto aktivieren, kann sich der zugeordnete Benutzer am Netzwerk anmelden und auf Netzwerkressourcen zugreifen, für die das Konto über die entsprechende Berechtigung verfügt, z. B. freigegebene Ordner und die Website für den Remotewebzugriff.

> [!NOTE]
>  Sie können nur Benutzerkonten aktivieren, die deaktiviert sind. Ein Benutzerkonto kann nicht aktiviert werden, nachdem es vom Server entfernt wurde.

##### <a name="to-activate-a-user-account"></a>So aktivieren Sie ein Benutzerkonto

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Wählen Sie in der Listenansicht das zu aktivierende Benutzerkonto aus.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Benutzerkonto aktivieren**.

5.  Klicken Sie im Bestätigungsfenster auf **Ja**, um die Aktion zu bestätigen.

> [!NOTE]
>  Nachdem Sie ein Benutzerkonto aktiviert haben, wird als Status für das Konto **Aktiv** angezeigt. Das Benutzerkonto erhält wieder dieselben Zugriffsrechte, die vor der Deaktivierung des Kontos zugewiesen waren.
>
>  Wenn Sie über einen integrierten E-Mail-Anbieter verfügen, wird das E-Mail-Konto, das dem Benutzerkonto zugewiesen ist, ebenfalls aktiviert.

###  <a name="deactivate-a-user-account"></a><a name="BKMK_Manage6"></a> Deaktivieren eines Benutzerkontos
 Wenn Sie ein Benutzerkonto deaktivieren, wird der Zugriff des Kontos auf den Server vorübergehend unterbrochen. Daher kann der zugeordnete Benutzer das Konto nicht für den Zugriff auf die Netzwerkressourcen wie die freigegebenen Ordner oder die Website für den Remotewebzugriff verwendet werden, bis Sie das Konto aktivieren.

 Wenn dem Benutzerkonto ein Microsoft-Onlinekonto zugeordnet ist, wird das Onlinekonto ebenfalls deaktiviert. Der Benutzer kann keine Ressourcen in Microsoft 365 und anderen Onlinedienste verwenden, die Sie abonnieren, aber die Daten des Benutzers, einschließlich der e-Mails, bleiben in Microsoft Online Services erhalten.

> [!NOTE]
>  Sie können nur Benutzerkonten deaktivieren, die derzeit aktiviert sind.

##### <a name="to-deactivate-a-user-account"></a>So deaktivieren Sie ein Benutzerkonto

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Wählen Sie in der Listenansicht das zu deaktivierende Benutzerkonto aus.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Benutzerkonto deaktivieren**.

5.  Klicken Sie im Bestätigungsfenster auf **Ja**, um die Aktion zu bestätigen.

> [!NOTE]
>  Nachdem Sie ein Benutzerkonto deaktiviert haben, wird als Status für das Konto **Aktiv** angezeigt.
>
>  Wenn Sie über einen integrierten E-Mail-Anbieter verfügen, wird das E-Mail-Konto, das dem Benutzerkonto zugewiesen ist, ebenfalls deaktiviert.

###  <a name="understand-user-accounts"></a><a name="BKMK_Manage7"></a> Grundlegendes zu Benutzerkonten
 Ein Benutzerkonto stellt wichtige Informationen zu Windows Server Essentials bereit, wodurch Benutzer Zugriff auf Informationen erhalten können, die auf dem Server gespeichert werden. Zudem wird es einzelnen Benutzern ermöglicht, ihre Dateien und Einstellungen zu erstellen und zu verwalten. Benutzer können sich auf beliebigen Computern im Netzwerk anmelden, wenn sie ein Benutzerkonto für Windows Server Essentials besitzen und über Zugriffsrechte für einen Computer verfügen. Benutzer greifen mithilfe ihres Benutzernamens und des zugehörigen Kennworts auf ihr Benutzerkonto zu.

 Es gibt zwei hauptsächliche Benutzerkontotypen. Die einzelnen Typen weisen den Benutzern jeweils einen anderen Grad an Kontrolle für den Computer zu:

-   **Standardkonten** sind für die tägliche Arbeit am Computer konzipiert. Das Standardkonto schützt das Netzwerk, indem Benutzer daran gehindert werden Änderungen vorzunehmen, die sich auf andere Benutzer auswirken, z. B. Dateien löschen oder Netzwerkeinstellungen ändern.

-   **Administratorkonten** bieten die umfassendsten Kontrollmöglichkeiten über ein Computernetzwerk. Administratorkonten sollten nur zugewiesen werden, wenn dies wirklich erforderlich ist.

###  <a name="manage-user-accounts-using-the-dashboard"></a><a name="BKMK_Manage8"></a> Verwalten von Benutzerkonten mithilfe des Dashboards
 Windows Server Essentials ermöglicht es, die allgemeinen administrativen Aufgaben mithilfe des Windows Server Essentials-Dashboard auszuführen. Standardmäßig umfasst die Seite **Benutzer** des Dashboards zwei Registerkarten: **Benutzer** und **Benutzergruppen**.

> [!NOTE]
> - Wenn Sie Ihren Server, auf dem Windows Server Essentials ausgeführt wird, mit Microsoft 365 integrieren, wird auch eine neue Registerkarte mit der Bezeichnung **Verteiler Gruppen** auf der Seite **Benutzer** des Dashboards hinzugefügt.
>   -   In Windows Server Essentials enthält die Seite " **Benutzer** " des Dashboards nur eine einzelne Registerkarte: **Benutzer**.

 Die Registerkarte **Benutzer** enthält Folgendes:

- Eine Liste von Benutzerkonten, in der Folgendes angezeigt wird:

  -   Der Name des Benutzers.

  -   Der Anmeldename für das Benutzerkonto.

  -   Ob das Benutzerkonto über die Berechtigung "Zugriff überall" verfügt. Die Berechtigung "Zugriff überall" für ein Benutzerkonto bedeutet entweder **Zulässig** oder **Nicht zulässig**.

  -   Ob der Dateiverlauf für dieses Benutzerkonto von dem Server verwaltet wird, der Windows Server Essentials ausführt. Der Dateiverlaufsstatus für ein Benutzerkonto ist entweder **Verwaltet** oder **Nicht verwaltet**.

  -   Die Zugriffsebene, die dem Benutzerkonto zugewiesen wird. Sie können entweder **Standardbenutzer** oder **Administrator** für den Umfang des Zugriffs auf ein Benutzerkonto zuweisen.

  -   Der Benutzerkontostatus. Ein Benutzerkonto kann **Aktiv**, **Inaktiv** oder **Unvollständig** sein.

  -   Wenn der Server in Windows Server Essentials in Microsoft 365 oder Windows InTune integriert ist, wird das Microsoft-Onlinekonto angezeigt.

  -   Wenn der Server in Windows Server Essentials in Microsoft 365 integriert ist, wird der Status des Kontos (in Windows Server Essentials als Microsoft-Onlinekonto bezeichnet) für das Benutzerkonto angezeigt.

- Ein Detailbereich mit zusätzlichen Informationen zum ausgewählten Benutzerkonto.

- Ein Aufgabenbereich, der Folgendes enthält:

  -   Eine Reihe von Verwaltungsaufgaben für das Benutzerkonto, z. B. Benutzerkonten anzeigen und entfernen oder Kennwörter ändern.

  -   Aufgaben, die es Ihnen gestatten, Einstellungen für alle Benutzerkonten im Netzwerk global festzulegen oder zu ändern.

  In der folgenden Tabelle werden die verschiedenen Benutzerkonto Aufgaben beschrieben, die auf der Registerkarte **Benutzer** verfügbar sind. Einige Aufgaben sind Benutzerkonto spezifisch und nur sichtbar, wenn Sie ein Benutzerkonto in der Liste auswählen.

> [!NOTE]
>  Wenn Sie Microsoft 365 in Windows Server Essentials integrieren, werden weitere Aufgaben zur Verfügung gestellt. Weitere Informationen finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

### <a name="user-account-tasks-in-the-dashboard"></a>Benutzerkontoaufgaben im Dashboard

|Aufgabenname|BESCHREIBUNG|
|---------------|-----------------|
|Kontoeigenschaften anzeigen|Gestattet es Ihnen, die Eigenschaften des ausgewählten Benutzerkontos anzuzeigen und zu ändern sowie die Berechtigungen für den Ordnerzugriff für das Konto anzugeben.|
|Benutzerkonto deaktivieren|Ein deaktiviertes Benutzerkonto kann sich nicht am Netzwerk anmelden oder auf die Netzwerkressourcen zugreifen, z. B. auf die freigegebenen Ordner oder Drucker.|
|Benutzerkonto aktivieren|Ein aktiviertes Benutzerkonto kann sich am Netzwerk anmelden und gemäß der definierten Kontoberechtigungen auf Netzwerkressourcen zugreifen.|
|Benutzerkonto entfernen|Ermöglicht es Ihnen, das ausgewählte Benutzerkonto zu entfernen.|
|Benutzerkontokennwort ändern|Ermöglicht es Ihnen, das Netzwerkkennwort für das ausgewählte Benutzerkonto zurückzusetzen.|
|Benutzerkonto hinzufügen|Startet den Assistenten zum Hinzufügen eines Benutzerkontos, mit dem Sie ein einzelnes neues Benutzerkonto erstellen können, das entweder über Standardbenutzer- oder Administratorzugriff verfügt.|
|Microsoft-Onlinekonto zuweisen|Fügt ein Microsoft-Onlinekonto zum ausgewählten lokalen Netzwerkbenutzerkonto hinzu.<br /><br /> Diese Aufgabe wird angezeigt, wenn Ihr Server in Microsoft Onlinedienste integriert ist, z. b. Microsoft 365.|
|Microsoft-Onlinekonten hinzufügen|Fügt Microsoft-Onlinekonten hinzu und ordnet sie lokalen Netzwerkbenutzerkonten zu.<br /><br /> Diese Aufgabe wird angezeigt, wenn Ihr Server in Microsoft Onlinedienste integriert ist, z. b. Microsoft 365.|
|Kennwortrichtlinie festlegen|Ermöglicht es Ihnen, die Werte der Kennwortrichtlinien für Ihr Netzwerk zu ändern.|
|Microsoft-Onlinekonten importieren|Führt einen Massenimport von Konten von Microsoft-Onlinediensten in das lokale Netzwerk aus.<br /><br /> Diese Aufgabe wird angezeigt, wenn Ihr Server in Microsoft Onlinedienste integriert ist, z. b. Microsoft 365.|
|Aktualisieren|Aktualisiert die Registerkarte "Benutzer".<br /><br /> Diese Aufgabe gilt für Windows Server Essentials.|
|Dateiverlaufseinstellungen ändern|Ermöglicht es Ihnen, die Einstellungen für den Dateiverlauf zu ändern, z. B. Sicherungshäufigkeit oder Sicherungsdauer.<br /><br /> Diese Aufgabe gilt für Windows Server Essentials.|
|Alle Remoteverbindungen exportieren|Erstellt für alle Remoteverbindungen zum Server, die in den letzten 30 Tagen hergestellt wurden, eine Datei im CSV-Format.|

##  <a name="managing-passwords-and-access"></a><a name="BKMK_ManageAccess"></a> Verwalten von Kenn Wörtern und Zugriff
 Die folgenden Themen enthalten Informationen zur Verwendung des Windows Server Essentials-Dashboards zum Verwalten von Benutzerkontokennwörtern und für den Benutzerzugriff auf freigegebene Ordner auf dem Server:

-   [Ändern oder Zurücksetzen des Kennworts für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access1)

-   [Wissenswertes zu Kennwortrichtlinien](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access3)

-   [Ändern der Kennwortrichtlinie](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access4)

-   [Zugriffsebene für freigegebene Ordner](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access5)

-   [Erhalten und Verwalten des Zugriffs auf Dateien für entfernte Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access6)

-   [Synchronisieren des DSRM-Kennworts mit dem Netzwerkadministratorkennwort](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access7)

-   [Erteilen der Remotedesktopberechtigung für Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access8)

-   [Ermöglichen des Ressourcenzugriffs für Benutzer auf dem Server](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access9)

-   [Ändern der RAS-Berechtigungen für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access10)

-   [Ändern der Berechtigungen für virtuelle private Netzwerke für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access11)

-   [Ändern des Zugriffs auf interne freigegebene Ordner für ein Benutzerkonto](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access12)

-   [Es Benutzerkonten gewähren, eine Remotedesktopsitzung für ihre Computer einzurichten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access13)

###  <a name="change-or-reset-the-password-for-a-user-account"></a><a name="BKMK_Access1"></a> Ändern oder Zurücksetzen des Kennworts für ein Benutzerkonto
 Gehen Sie folgendermaßen vor, um ein Benutzerkontokennwort zu ändern oder zurückzusetzen.

##### <a name="to-reset-the-password-for-a-user-account"></a>So setzen Sie das Kennwort für ein Benutzerkonto zurück

1. Öffnen Sie das Windows Server Essentials-Dashboard.

2. Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3. Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto aus, das Sie zurücksetzen möchten.

4. Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Benutzerkonto Kennwort ändern**. Der Assistent zum Ändern des Benutzerkontokennworts wird angezeigt.

5. Geben Sie ein neues Kennwort für das Benutzerkonto ein, und geben Sie das Kennwort anschließend erneut ein, um es zu bestätigen.

6. Klicken Sie auf **Kennwort ändern**.

7. Stellen Sie das neue Kennwort für die Benutzer bereit.

   > [!IMPORTANT]
   > - Möglicherweise können Sie Ihr Kennwort nicht ändern, wenn die Kennwortrichtlinie für Ihr Konto auf **Kennwörter laufen nicht ab** festgelegt wurde.
   >   -   Nicht-ASCII-Zeichen werden in Azure AD nicht unterstützt. Wenn Ihr Server in Azure AD integriert ist, sollten Sie daher keine nicht-ASCII-Zeichen in Ihrem Kennwort verwenden.
   >   -   Wenn dem Benutzer ein Microsoft-Onlinekonto (in Windows Server Essentials als Microsoft 365-Konto bekannt) zugewiesen ist, wird das Kennwort mit dem Onlinekonto Kennwort synchronisiert. Der Benutzer verwendet das neue Kennwort, um sich beim Server anzumelden oder sich bei Microsoft 365 anzumelden. Weitere Informationen finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

###  <a name="what-you-should-know-about-password-policies"></a><a name="BKMK_Access3"></a> Was Sie über Kenn Wort Richtlinien wissen sollten
 Die Kennwortrichtlinie besteht aus einer Reihe von Regeln, die festlegen, wie Benutzer Kennwörter entsprechend erstellen und verwenden. Die Richtlinie hilft dabei den nicht berechtigten Zugriff auf Benutzerdaten und andere Informationen zu vermeiden, die auf dem Server gespeichert werden. Die Kennwortrichtlinie wird auf alle Benutzerkonten angewendet, die auf das Netzwerk zugreifen.

 Die Kennwortrichtlinie von Windows Server Essentials besteht wie folgt aus drei primären Elementen:

- **Kennwortlänge**  Je länger ein Kennwort, desto sicherer ist es. Leere Kennwörter sind nicht sicher.

- **Kennwortkomplexität**  Komplexe Kennwörter enthalten eine Mischung aus Groß- und Kleinbuchstaben (a-z, A-Z), Basiszahlen (0-9) und nicht alphabetischen Zeichen (z. B. !,@,#,_,-). Komplexe Kennwörter sind weniger anfällig für unberechtigte Zugriffe. Kennwörter, die Benutzernamen, Geburtsdaten oder andere persönliche Informationen enthalten, bieten keine geeignete Sicherheit.

- **Kennwortalter**  Windows Server Essentials erfordert, dass Benutzer ihr Kennwort mindestens alle 180 Tage ändern. Optional können Sie auswählen, dass Kennwörter nicht ablaufen.

  Um die Implementierung einer Kennwortrichtlinie in Ihrem Computernetzwerk zu vereinfachen, bietet Windows Server Essentials ein einfaches Tool, mit dem die Kennwortrichtlinie auf eines der folgenden vier vordefinierten Richtlinienprofile festgelegt oder in eines dieser Profile geändert werden kann:

- **Unsicher**  Benutzer können ein beliebiges nicht leeres Kennwort angeben.

- **Mittel**  Diese Kennwörter müssen mindestens fünf Zeichen enthalten. Ein komplexes Kennwort ist nicht erforderlich.

- **Mittelstark**  Diese Kennwörter müssen mindestens fünf Zeichen enthalten und dabei Buchstaben, Zahlen und Zeichen einbeziehen.

- **Sicher**  Diese Kennwörter müssen mindestens sieben Zeichen enthalten und dabei Buchstaben, Zahlen und Zeichen einbeziehen. Diese Kennwörter sind sicherer, aber schwerer zu merken.

  > [!NOTE]
  >  Kennwörter dürfen weder den Benutzernamen noch die E-Mail-Adresse enthalten.
  >
  >  Wenn Sie in Microsoft 365 integrieren, erzwingt die-Integration die Richtlinie für sichere **Kenn Wörter und** aktualisiert die Richtlinie so, dass die folgenden Anforderungen erfüllt sind:
  >
  > - Kenn Wörter müssen 8 16 Zeichen enthalten.
  >   -   Kenn Wörter dürfen kein Leerzeichen oder den Microsoft 365 e-Mail-Namen enthalten.

  Bei der Serverinstallation wird die Standardkennwortrichtlinie standardmäßig auf die Option **Sicher** festgelegt.

###  <a name="change-the-password-policy"></a><a name="BKMK_Access4"></a> Ändern der Kenn Wort Richtlinie
 Verwenden Sie das folgende Verfahren zum Festlegen oder Ändern der Kennwortrichtlinie auf bzw. in eines der vier vordefinierten Richtlinienprofile.

##### <a name="to-change-the-password-policy"></a>So ändern Sie die Kennwortrichtlinie

1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf **Benutzer**.

2.  Klicken Sie im Bereich **Tasks für Benutzer** auf **Kennwortrichtlinie festlegen**.

3.  Legen Sie auf dem Bildschirm **Kennwortrichtlinie ändern** den Grad der Kennwortsicherheit über den Schieberegler fest.

     Microsoft empfiehlt, für die Kennwortsicherheit **Sicher** festzulegen.

    > [!NOTE]
    >  Optional können Sie auch **Kennwörter laufen nicht** auswählen. Diese Einstellung ist weniger sicher und wird somit nicht empfohlen.

4.  Klicken Sie auf **Richtlinie ändern**.

###  <a name="level-of-access-to-shared-folders"></a><a name="BKMK_Access5"></a> Zugriffsebene für freigegebene Ordner
 Als bewährte Methode sollten Sie die restriktivsten verfügbaren Berechtigungen zuweisen, die es den Benutzern weiterhin gestatten, die erforderlichen Aufgaben auszuführen.

 Für die freigegebenen Ordner auf dem Server sind drei Zugriffseinstellungen verfügbar:

-   **Lesen/Schreiben**  Wählen Sie diese Einstellung aus, wenn Sie es der Benutzerkontoberechtigung gestatten möchten, Dateien in den freigegebenen Ordnern zu erstellen, zu ändern und zu löschen.

-   **Schreibgeschützt**  Wählen Sie diese Einstellung aus, wenn Sie es der Benutzerkontoberechtigung nur gestatten möchten, Dateien in den freigegebenen Ordnern zu lesen. Benutzerkonten mit schreibgeschützten Zugriff können keine Dateien im freigegebenen Ordner erstellen, ändern oder löschen.

-   **Kein Zugriff**  Wählen Sie diese Einstellung aus, wenn das Benutzerkonto nicht auf Dateien im freigegebenen Ordner zugreifen können soll.

###  <a name="retain-and-manage-access-to-files-for-removed-user-accounts"></a><a name="BKMK_Access6"></a> Beibehalten und Verwalten des Zugriffs auf Dateien für entfernte Benutzerkonten
 Der Netzwerkadministrator kann ein Benutzerkonto entfernen und auswählen, dass die Dateien des Benutzers zur zukünftigen Verwendung aufbewahrt werden. In diesem Szenario kann das entfernte Benutzerkonto nicht mehr für die Anmeldung am Netzwerk verwendet werden. Die Dateien für diesen Benutzer werden jedoch in einem freigegebenen Ordner gespeichert, der mit einem anderen Benutzer gemeinsam verwendet werden kann.

> [!IMPORTANT]
>  Beachten Sie, dass beim Entfernen eines Benutzerkontos mit zugewiesenem Microsoft-Onlinekonto, dieses Onlinekonto ebenfalls entfernt wird, und die Benutzerdaten, einschließlich E-Mails, unterliegen den Datenaufbewahrungsrichtlinien in Microsoft Online Services. Um die Benutzerdaten für ein Onlinekonto zu bewahren, deaktivieren Sie das Benutzerkonto, anstatt es zu entfernen. Weitere Informationen finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

##### <a name="to-remove-a-user-account-but-retain-access-to-the-users-files"></a>So entfernen Sie ein Benutzerkonto, behalten aber den Zugriff auf die Dateien des Benutzers bei

1. Öffnen Sie das Windows Server Essentials-Dashboard.

2. Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3. Wählen Sie in der Liste der Benutzerkonten das zu entfernende Benutzerkonto aus.

4. Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Benutzerkonto entfernen**. Der Assistent zum Löschen eines Benutzerkontos wird angezeigt.

5. Stellen Sie auf der Seite **Möchten Sie die Dateien behalten?** sicher, dass das Kontrollkästchen **Dateien (samt Sicherungen des Dateiversionsverlaufs und umgeleitetem Ordner) für das Benutzerkonto löschen** deaktiviert ist, und klicken Sie dann auf **Weiter**.

    Es wird eine Bestätigungsseite mit einer Warnung angezeigt, dass Sie das Konto löschen, aber die Dateien behalten.

6. Klicken Sie auf **Konto löschen**, um das Benutzerkonto zu löschen.

   Nachdem das Benutzerkonto entfernt wurde, kann der Administrator einem anderen Benutzerkonto den Zugriff auf den freigegebenen Ordner erteilen.

##### <a name="to-give-a-user-account-permission-to-access-a-shared-folder"></a>So erteilen Sie einem Benutzerkonto die Berechtigung für den Zugriff auf einen freigegebenen Ordner

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Speicher**, und klicken Sie dann auf die Registerkarte **Serverordner**.

3.  Wählen Sie in der Liste der Ordner den Ordner **Benutzer** aus.

4.  Klicken Sie im Bereich **Tasks für Benutzer** auf **Ordner öffnen**. Windows-Explorer wird geöffnet und zeigt den Inhalt des Ordners **Benutzer** an.

5.  Klicken Sie mit der rechten Maustaste auf den Ordner für das Benutzerkonto, das Sie freigeben möchten, und klicken Sie dann auf **Eigenschaften**.

6.  Klicken Sie in **<Benutzerkonto \> Eigenschaften**auf die Registerkarte **Freigabe** , und klicken Sie dann auf **Freigeben**.

7.  Geben Sie in das Fenster **Dateifreigabe** den Benutzerkontonamen ein oder wählen Sie einen Namen aus, für den der Ordner freigegeben werden soll, und klicken Sie dann auf **Hinzufügen**.

8.  Wählen Sie die **Berechtigungsstufe** aus, über die das Benutzerkonto verfügen soll, und klicken Sie dann auf **Freigeben**.

###  <a name="synchronize-the-dsrm-password-with-the-network-administrator-password"></a><a name="BKMK_Access7"></a> Synchronisieren des DSRM-Kennworts mit dem Netzwerkadministrator Kennwort
 Die Verzeichnisdienstwiederherstellung (Directory Services Restore Mode, DSRM) ist eine spezielle Startmethode zum Reparieren oder Wiederherstellen von Active Directory. Das Betriebssystem verwendet die Verzeichnisdienstwiederherstellung für die Anmeldung auf dem Computer, falls Active Directory fehlschlägt oder wiederhergestellt werden muss. Wenn sich Ihr Netzwerkadministratorkennwort und das Kennwort für die Verzeichnisdienstwiederherstellung unterscheiden, wird die Verzeichnisdienstwiederherstellung nicht geladen.

 Während einer reinen Erstinstallation von Windows Server Essentials legt das Programm das DSRM-Kennwort auf das Kennwort für das Netzwerkadministratorkonto fest, das Sie während des Setups oder in der Antwortdatei für die Migration angeben. Wenn Sie Ihr Netzwerkadministratorkennwort ändern (es wird empfohlen, dies alle 60 Tage vorzunehmen, um die Serversicherheit zu erhöhen), die Kennwortänderung nicht an die Verzeichnisdienstwiederherstellung weitergeleitet. Dies führt zu einem Kennwortkonflikt. In diesem Fall können Sie die folgenden Lösungen verwenden, um das Kennwort Ihres Netzwerkadministrators manuell oder automatisch mit dem DSRM-Kennwort zu synchronisieren.

##### <a name="to-manually-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>So synchronisieren Sie das DSRM-Kennwort mit einem Netzwerkadministratorkonto

1. Führen Sie an einer Eingabeaufforderung `ntdsutil.exe` aus, um das Tool "ntdsutil" zu öffnen.

2. Geben Sie zum Zurücksetzen des DSRM-Kennworts **set dsrm password** ein.

3. Um das DSRM-Kennwort auf einem Domänen Controller mit dem aktuellen Netzwerkadministrator Konto zu synchronisieren, geben Sie Folgendes ein:

    **sync from domain account** *<aktuelles_Netzwerkadministratorkonto>*. Drücken Sie dann die EINGABETASTE.

   Da Sie das Kennwort für das Netzwerkadministratorkonto in regelmäßigen Abständen ändern, um sicherzustellen, dass das DSRM-Kennwort immer dem aktuellen Kennwort des Netzwerkadministrators entspricht, empfiehlt es sich, einen Zeitplantask zu planen, um das DSRM-Kennwort automatisch täglich mit dem Netzwerkadministratorkennwort zu synchronisieren.

##### <a name="to-automatically-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>So synchronisieren Sie das DSRM-Kennwort automatisch mit einem Netzwerkadministratorkonto

1.  Öffnen Sie auf dem Server **Verwaltung**, und doppelklicken Sie dann auf **Taskplaner**.

2.  Klicken Sie im Taskplaner im Bereich **Aktionen** auf **Task erstellen**.

3.  Geben Sie in das Textfeld **Name** einen Namen für die Task ein, z. B. **AutoSync DSRM-Kennwort**, und wählen Sie dann die Option **Mit höchsten Berechtigungen ausführen** aus.

4.  Legen Sie fest, wann die Task ausgeführt werden soll:

    1.  Klicken Sie im Dialogfeld **Task erstellen** auf die Registerkarte **Trigger** ein, und klicken Sie auf **Neu**.

    2.  Wählen Sie im Dialogfeld **Neuer Trigger** die Häufigkeit aus, geben Sie das Wiederholungsintervall an, und wählen Sie dann eine Startzeit aus.

        > [!NOTE]
        >  Als bewährte Methode sollten Sie die Task täglich außerhalb der Geschäftszeiten ausführen lassen.

    3.  Klicken Sie auf **OK**, um die Änderungen zu speichern und zum Dialogfeld **Task erstellen** zurückzukehren.

5.  Definieren Sie die folgenden Taskaktionen:

    1.  Klicken Sie auf die Registerkarte **Aktionen**, und klicken Sie dann auf **Neu**. Das Dialogfeld **Neue Aktion** wird angezeigt.

    2.  Klicken Sie in der Liste **Aktion** auf **Programm starten**, und navigieren Sie dann zu **C:\WINDOWS\SYSTEM32\ntdsutil.exe**.

    3.  Geben Sie im Textfeld **Argumente hinzufügen**(optional) Folgendes ein (Sie müssen die Anführungszeichen einschließen): **legen Sie die DSRM-Kenn Wort Synchronisierung über das Domänen Konto SBS_network_administrator_account q q fest** , wobei *SBS_network_administrator_account* den Kontonamen des aktuellen Netzwerkadministrators darstellt.

6.  Klicken Sie zweimal auf **OK**, um die Task zu speichern und das Dialogfeld **Task erstellen** zu schließen. Die neue Task wird im Abschnitt **Aktive Tasks** des **Taskplaners** angezeigt.

###  <a name="give-user-accounts-remote-desktop-permission"></a><a name="BKMK_Access8"></a> Erteilen der Remote Desktop Berechtigung für Benutzerkonten
 Bei der Standardinstallation von Windows Server Essentials verfügen Netzwerkbenutzer nicht über die Berechtigung zum Herstellen einer Remoteverbindung zu Computern oder anderen Ressourcen im Netzwerk.

 Bevor die Netzwerkbenutzer eine Remoteverbindung mit Netzwerkressourcen herstellen können, müssen Sie zuerst die Option "Zugriff überall" einrichten. Nachdem Sie die Option "Zugriff überall" eingerichtet haben, können die Benutzer über ein Gerät an einem beliebigen Standort mit Internetverbindung auf Dateien, Anwendungen und Computer im Unternehmensnetzwerk zugreifen.

 Der Assistent zum Einrichten von "Zugriff überall" gestattet es Ihnen, zwei Methoden für den Remotezugriff zu aktivieren:

- Ein virtuelles privates Netzwerk (VPN)

- Remotewebzugriff

  Wenn Sie den Assistenten ausführen, können Sie auch auswählen, dass für alle aktuellen und neu hinzugefügten Benutzerkonten der "Zugriff überall" gestattet ist.

  Öffnen Sie zum Einrichten von "Zugriff überall" die Seite **Start** des Dashboards, klicken Sie auf **SETUP**, und klicken Sie dann auf **"Zugriff überall" einrichten**.

  Weitere Informationen zu "Zugriff überall" finden Sie unter Verwalten von "Zugriff [überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)".

###  <a name="enable-users-to-access-resources-on-the-server"></a><a name="BKMK_Access9"></a> Benutzern den Zugriff auf Ressourcen auf dem Server ermöglichen
  Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials oder Windows Server Essentials ausgeführt wird, oder für einen Server mit Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials-Rolle.

 Wenn Benutzer den Remotezugriff verwenden und/oder über einzelne Benutzerkonten verfügen sollen, können Sie nach dem Herstellen einer Verbindung zwischen einem Computer und dem Server über das Dashboard neue Netzwerkbenutzerkonten für die Benutzer des an das Netzwerk angeschlossenen Computers auf dem Server erstellen. Weitere Informationen zum Erstellen von Benutzerkonten finden Sie unter [Hinzufügen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1). Nachdem Sie die Benutzerkonten erstellt haben, müssen Sie die Informationen zum Netzwerkbenutzernamen und dem zugehörigen Kennwort für die Benutzer des Clientcomputers bereitstellen, damit diese mithilfe des Launchpads auf die Ressourcen auf dem Server zugreifen können.

 Für jedes erstellte Benutzerkonto können Sie den Zugriff auf Folgendes über die Benutzerkontoeigenschaften festlegen:

-   **Freigegebene Ordner**  Standardmäßig verfügen Netzwerkadministratoren über die Berechtigung **Lesen/Schreiben** für alle freigegebenen Ordner, und Standardbenutzerkonten weisen die Berechtigung **Schreibgeschützt** für den Unternehmensordner auf. Wenn das Medienstreaming aktiviert ist, können Sie Ordnerzugriffsberechtigungen für einzelne Standardbenutzerkonten für die folgenden freigegebenen Ordner zuweisen: **Musik**, **Bilder**, **TV-Aufzeichnungen**und **Videos**. Sie können Berechtigung für Benutzerkonten für den Zugriff auf freigegebene Ordner auf der Registerkarte **Freigegebene Ordner** der Benutzerkontoeigenschaften festlegen.

-   **Zugriff überall**  Standardmäßig können Netzwerkadministratoren entweder VPN oder den Remotewebzugriff für den Zugriff auf Serverrollen verwenden. Für Standardbenutzerkonten müssen Sie Benutzerkontoberechtigungen auf der Registerkarte **Zugriff überall** festlegen.

-   **Computerzugriff**  Standardmäßig können Netzwerkadministratoren auf alle Computer im Netzwerk zugreifen. Für Standardbenutzerkonten können Sie jedoch einzelne Benutzerkontoberechtigungen für den Zugriff auf Computer im Netzwerk auf der Registerkarte **Computerzugriff** der Benutzerkontoeigenschaften festlegen.

##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012-r2"></a>So bearbeiten Sie die Eigenschaften von Benutzerkonten in Windows Server Essentials 2012 R2

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.

3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto aus, das Sie bearbeiten möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Konto Eigenschaften anzeigen**.

5.  Gehen Sie in den ** \> Eigenschaften des<Benutzerkontos**wie folgt vor:

    1.  Legen Sie auf der Registerkarte **Freigegebene Ordner** die entsprechenden Berechtigungen für die einzelnen freigegebenen Ordner fest.

    2.  Auf der Registerkarte **Zugriff überall**:

        1.  Um dem Benutzer die Berechtigung zu gehören, eine Verbindung zum Server über VPN herzustellen, aktivieren Sie das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**.

        2.  Um einem Benutzer die Herstellung einer Verbindung zum Server über den Remotewebzugriff zu erlauben, aktivieren Sie das Kontrollkästchen **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.

    3.  Wählen Sie auf der Registerkarte **Computerzugriff** die Netzwerkcomputer aus, auf die die Benutzer zugreifen können sollen.

##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012"></a>So bearbeiten Sie die Eigenschaften von Benutzerkonten in Windows Server Essentials 2012

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.

3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto aus, das Sie bearbeiten möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Eigenschaften**.

5.  Gehen Sie in den ** \> Eigenschaften des<Benutzerkontos**wie folgt vor:

    1.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Benutzer kann Integritätswarnungen für das Netzwerk anzeigen** aus, wenn das Benutzerkonto auf die Berichte zur Netzwerkintegrität zugreifen können muss.

    2.  Legen Sie auf der Registerkarte **Freigegebene Ordner** die entsprechenden Berechtigungen für die einzelnen freigegebenen Ordner fest.

    3.  Auf der Registerkarte **Zugriff überall**:

        1.  Um dem Benutzer die Berechtigung zu gehören, eine Verbindung zum Server über VPN herzustellen, aktivieren Sie das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**.

        2.  Um einem Benutzer die Herstellung einer Verbindung zum Server über den Remotewebzugriff zu erlauben, aktivieren Sie das Kontrollkästchen **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.

    4.  Wählen Sie auf der Registerkarte **Computerzugriff** die Netzwerkcomputer aus, auf die die Benutzer zugreifen können sollen.

###  <a name="change-remote-access-permissions-for-a-user-account"></a><a name="BKMK_Access10"></a> Ändern der Remote Zugriffsberechtigungen für ein Benutzerkonto
 Ein Benutzer kann von einem Remotestandort aus über ein VPN, den Remotewebzugriff oder andere Webdienstanwendungen auf Ressourcen zugreifen, die sich auf dem Server befinden. Standardmäßig werden die Remotezugriffsberechtigungen für Netzwerkbenutzer aktiviert, wenn Sie die Option "Zugriff überall" in Windows Server Essentials über das Dashboard konfigurieren.

##### <a name="to-change-remote-access-permissions-for-a-user-account"></a>So ändern Sie die Remotezugriffsberechtigungen für ein Benutzerkonto

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Wählen Sie in der Liste von Benutzerkonten das Benutzerkonto aus, das Sie ändern möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Konto Eigenschaften anzeigen**. Die Seite **Eigenschaften** für das Benutzerkonto wird angezeigt.

5.  Gehen Sie auf der Registerkarte **Zugriff überall** in folgender Weise vor:

    -   Aktivieren Sie das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**, um es Benutzern zu gestatten, die Verbindung zum Server über ein VPN herzustellen.

    -   Aktivieren Sie das Kontrollkästchen **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**, um es Benutzern zu gestatten, die Verbindung zum Server über Remotewebzugriff herzustellen.

6.  Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.

###  <a name="change-virtual-private-network-permissions-for-a-user-account"></a><a name="BKMK_Access11"></a> Ändern der Berechtigungen für virtuelle private Netzwerke für ein Benutzerkonto
 Sie können die Verbindung über ein virtuelles privates Netzwerk (VPN) mit Windows Server Essentials herstellen und auf die Ressourcen zugreifen, die auf dem Server gespeichert sind. Dies ist besonders dann nützlich, wenn auf Ihrem Clientcomputer Netzwerkkonten eingerichtet sind, die verwendet werden können, um eine Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung herzustellen. Alle auf dem gehosteten Windows Server Essentials-Server neu erstellten Benutzerkonten müssen bei der ersten Anmeldung am Clientcomputer VPN verwenden.

##### <a name="to-change-vpn-permissions-for-network-users"></a>So ändern Sie die VPN-Berechtigungen für Netzwerkbenutzer

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.

3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto aus, dem Sie den Remotezugriff auf den Desktop gewähren möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Eigenschaften**.

5.  Klicken Sie in den ** \> Eigenschaften des<Benutzerkontos**auf die Registerkarte **Zugriff überall** .

6.  Aktivieren Sie auf der Registerkarte **Zugriff überall** das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**, um es Benutzern zu gestatten, die Verbindung zum Server über ein VPN herzustellen.

7.  Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.

###  <a name="change-access-to-internal-shared-folders-for-a-user-account"></a><a name="BKMK_Access12"></a> Ändern des Zugriffs auf interne freigegebene Ordner für ein Benutzerkonto
 Sie können den Zugriff auf freigegebene Ordner auf dem Server mithilfe der Tasks auf der Registerkarte **Serverordner** des Dashboards verwalten. Standardmäßig werden die folgenden Serverordner erstellt, wenn Sie Windows Server Essentials installieren:

-   **Clientcomputersicherungen**  Darin werden Clientcomputersicherungen gespeichert, die von der Windows Server-Sicherung erstellt wurden. Dieser Serverordner wird nicht freigegeben.

-   **Firma**  Darin werden Dokumente von Netzwerkbenutzern gespeichert und abgerufen, die sich auf das Unternehmen beziehen.

-   **Sicherungen von Dateiversionsverläufen**  Windows Server Essentials speichert standardmäßig Dateisicherungen, die über den Dateiversionsverlauf erstellt wurden. Dieser Serverordner wird nicht freigegeben.

-   **Ordnerumleitung**  Darin werden Ordner gespeichert und abgerufen, die von Netzwerkbenutzern für die Ordnerumleitung eingerichtet wurden. Dieser Serverordner wird nicht freigegeben.

-   **Musik**  Darin werden Musikdateien von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.

-   **Bilder**  Darin werden Bilder von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.

-   **TV-Aufzeichnungen**  Darin werden aufgezeichnete Fernsehsendungen von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.

-   **Videos**  Darin werden Videos von Netzwerkbenutzern gespeichert und abgerufen. Dieser Ordner wird erstellt, wenn Sie die Medienfreigabe aktivieren.

-   **Benutzer**  Darin werden Dateien von Netzwerkbenutzern gespeichert und abgerufen. Ein benutzerspezifischer Ordner wird automatisch im Serverordner **Benutzer** für jedes Netzwerkbenutzerkonto generiert, das Sie erstellen.

##### <a name="to-change-access-to-a-shared-folder-for-a-user-account"></a>So ändern Sie den Zugriff auf einen freigegebenen Ordner für ein Benutzerkonto

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf **SPEICHER** und anschließend auf **Serverordner**.

3.  Navigieren Sie zum Serverordner, für den Sie die Berechtigungen ändern möchten, und wählen Sie ihn aus.

4.  Klicken Sie im Aufgabenbereich auf **Ordnereigenschaften anzeigen**.

5.  Klicken Sie in **<FolderName- \> Eigenschaften**auf **Freigabe**, **Wählen Sie die**entsprechende Benutzer Zugriffsebene für die aufgeführten Benutzerkonten aus, und klicken Sie dann auf übernehmen.

    > [!NOTE]
    >  Die Freigabeberechtigungen für die Serverordner **Sicherungen von Dateiversionsverläufen**, **Ordnerumleitung** und **Benutzer** können nicht geändert werden. Die Ordnereigenschaften dieser Serverordner enthalten daher keine Registerkarte für **Freigabe**.

###  <a name="allow-user-accounts-to-establish-a-remote-desktop-session-to-their-computer"></a><a name="BKMK_Access13"></a> Zulassen, dass Benutzerkonten eine Remote Desktop Sitzung mit Ihrem Computer einrichten
  Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials oder Windows Server Essentials ausgeführt wird, oder für einen Server mit Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials-Rolle.

 Der Netzwerkadministrator kann Netzwerkbenutzern Berechtigungen erteilen, die es ihnen ermöglichen, von einem Remotestandort aus auf ihre Netzwerkcomputer zuzugreifen.

##### <a name="to-enable-users-to-access-their-network-computers-from-a-remote-location"></a>So ermöglichen Sie Benutzern von einem Remotestandort aus den Zugriff auf ihre Netzwerkcomputer

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.

3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto aus, dem Sie den Remotezugriff auf den Desktop gewähren möchten.

4.  Klicken Sie im Bereich ** \> Aufgaben des<Benutzerkontos** auf **Eigenschaften**.

5.  Klicken Sie in den ** \> Eigenschaften des<Benutzerkontos**auf die Registerkarte **Computer Zugriff** .

6.  Wählen Sie die Computer aus, auf die dieses Benutzerkonto remote zugreifen können soll, und klicken Sie dann auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md)

-   [Verbindung herstellen](../use/Get-Connected-in-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
