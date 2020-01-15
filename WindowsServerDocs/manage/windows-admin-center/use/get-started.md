---
title: Jetzt einsteigen –mit Windows Admin Center
description: Jetzt einsteigen –mit Windows Admin Center
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 02/15/2019
ms.openlocfilehash: fc8e6ffa39320cfc73bf3f5bd0a5bc765ded24b4
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950523"
---
# <a name="get-started-with-windows-admin-center"></a>Einstieg in das Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../overview.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows Admin Center auf Windows 10 installiert

> [!IMPORTANT]
> Sie müssen ein Mitglied der lokalen Administrator Gruppe sein, um Windows Admin Center unter Windows 10 verwenden zu können.

### <a name="selecting-a-client-certificate"></a>Auswählen eines Client Zertifikats

Wenn Sie das Windows Admin Center zum ersten Mal unter Windows 10 öffnen, stellen Sie sicher, dass Sie das *Windows Admin Center-Client* Zertifikat auswählen (andernfalls erhalten Sie einen HTTP 403-Fehler, der besagt, dass Sie nicht zu dieser Seite gelangen können).

Wenn Sie in Microsoft Edge aufgefordert werden, dieses Dialogfeld zu erhalten:
 
1. Klicken Sie auf **Weitere Optionen**

    ![](../media/launch-cert-1.png)

2. Wählen Sie das Zertifikat mit der Bezeichnung **Windows Admin Center Client** aus, **und klicken Sie**

    ![](../media/launch-cert-2.png)

3. Stellen Sie sicher, dass **immer Zugriff zulassen** ausgewählt ist, **und klicken Sie**

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>Herstellen einer Verbindung mit verwalteten Knoten und Clustern

Nachdem Sie die Installation des Windows Admin Centers abgeschlossen haben, können Sie über die Haupt Übersichtsseite Server oder Cluster hinzufügen, die verwaltet werden sollen.

 **Fügen Sie einen einzelnen Server oder einen Cluster als verwalteten Knoten hinzu.**

1. Klicken Sie unter **alle Verbindungen**auf **+ Hinzufügen** .

   ![](../media/launch/addserver0.png)

2. Wählen Sie das Hinzufügen eines Servers, Clusters, Windows-PCs oder einer Azure-VM aus:
    
   ![](../media/launch/ChooseConnectionType.png)

3. Geben Sie den Namen des zu verwaltenden Servers oder Clusters ein, und klicken Sie auf **senden**. Der Server oder Cluster wird auf der Übersichtsseite zur Verbindungsliste hinzugefügt.

   ![](../media/launch/addserver2.png)

   **--Oder--**

**Massen Import mehrerer Server**

 1. Wählen Sie auf der Seite **Server Verbindung hinzufügen** die Registerkarte **Server importieren** aus.

    ![](../media/launch/import-servers.png)

 2. Klicken Sie auf **Durchsuchen** , und wählen Sie eine Textdatei aus, die ein Komma oder eine neue durch Trennzeichen getrennte Liste von FQDNs für die Server enthält, die Sie hinzufügen möchten.

> [!Note]
> Die CSV-Datei, die durch den [Export ihrer Verbindungen mit PowerShell](#use-powershell-to-import-or-export-your-connections-with-tags) erstellt wurde, enthält neben den Servernamen zusätzliche Informationen, die mit dieser Import Methode nicht kompatibel sind.

  **--Oder--**

**Hinzufügen von Servern durchsuchen Active Directory**

 1. Wählen Sie auf der Seite **Server Verbindung hinzufügen** die Registerkarte **Active Directory suchen** aus.

    ![](../media/launch/search-ad.png)

 2. Geben Sie Suchkriterien ein, und klicken Sie auf **Suchen**. Platzhalter (*) werden unterstützt.

 3. Wenn die Suche abgeschlossen ist, wählen Sie mindestens eines der Ergebnisse aus, und fügen Sie optional Tags hinzu, und klicken Sie auf **Hinzufügen**.

## <a name="authenticate-with-the-managed-node"></a>Authentifizieren mit dem verwalteten Knoten ##

Das Windows Admin Center unterstützt mehrere Mechanismen zum Authentifizieren mit einem verwalteten Knoten. Das einmalige Anmelden ist die Standardeinstellung.

**Einmaliges Anmelden**

Sie können Ihre aktuellen Windows-Anmelde Informationen verwenden, um sich mit dem verwalteten Knoten zu authentifizieren. Dies ist die Standardeinstellung, und das Windows Admin Center versucht, sich anzumelden, wenn Sie einen Server hinzufügen. 

**Einmaliges Anmelden bei Bereitstellung als Dienst unter Windows Server**

Wenn Sie Windows Admin Center auf Windows Server installiert haben, ist für Single Sign-on zusätzliche Konfiguration erforderlich.  [Konfigurieren Ihrer Umgebung für die Delegierung](../configure/user-access-control.md)

**--Oder--**

**Verwenden von *Manage as* zum Angeben von Anmelde Informationen**

Wählen Sie unter **alle Verbindungen**einen Server aus der Liste aus, und wählen Sie **verwalten als** aus, um die Anmelde Informationen anzugeben, die Sie für die Authentifizierung beim verwalteten Knoten verwenden werden:

![](../media/launch-use-6.png)

Wenn Windows Admin Center im Dienst Modus unter Windows Server ausgeführt wird, aber keine Kerberos-Delegierung konfiguriert ist, müssen Sie Ihre Windows-Anmelde Informationen erneut eingeben:

![](../media/launch-use-7.png)

Sie können die Anmelde Informationen auf alle Verbindungen anwenden, wodurch Sie für die jeweilige Browsersitzung zwischengespeichert werden. Wenn Sie Ihren Browser neu laden, müssen Sie Ihre **Manage als** Anmelde Informationen erneut eingeben.

**Lokale Administrator Kenn Wort Lösung (Runden)**

Wenn Ihre Umgebung [runden](https://technet.microsoft.com/mt227395.aspx)verwendet und Sie Windows Admin Center auf Ihrem Windows 10-PC installiert haben, können Sie die Runden-Anmelde Informationen verwenden, um sich mit dem verwalteten Knoten zu authentifizieren. **Wenn Sie dieses Szenario verwenden, geben Sie uns** [Feedback](https://aka.ms/WACFeedback).

## <a name="using-tags-to-organize-your-connections"></a>Verwenden von Tags zum Organisieren von Verbindungen

Sie können Tags verwenden, um verwandte Server in der Verbindungsliste zu identifizieren und zu filtern.  Dies ermöglicht es Ihnen, eine Teilmenge der Server in der Verbindungsliste anzuzeigen.  Dies ist besonders nützlich, wenn Sie über viele Verbindungen verfügen.

### <a name="edit-tags"></a>Tags bearbeiten

* Wählen Sie in der Liste "alle Verbindungen" einen Server oder mehrere Server aus.
* Klicken Sie unter **alle Verbindungen**auf **Tags bearbeiten** .

![](../media/launch/tags-5.png)

Im Bereich " **Verbindungs Tags bearbeiten** " können Sie Tags Ihrer ausgewählten Verbindung (en) ändern, hinzufügen oder entfernen:

* Zum Hinzufügen eines neuen Tags zu den ausgewählten Verbindungen Wählen Sie **Tag hinzufügen** aus, und geben Sie den Tagnamen ein, den Sie verwenden möchten.

* Aktivieren Sie das Kontrollkästchen neben dem Tagnamen, den Sie anwenden möchten, um die ausgewählten Verbindungen mit einem vorhandenen Tagnamen zu markieren.

* Wenn Sie ein Tag aus allen ausgewählten Verbindungen entfernen möchten, deaktivieren Sie das Kontrollkästchen neben dem Tag, das Sie entfernen möchten.

* Wenn ein Tag auf eine Teilmenge der ausgewählten Verbindungen angewendet wird, wird das Kontrollkästchen in einem Zwischenzustand angezeigt. Sie können auf das Kontrollkästchen klicken, um es zu überprüfen und das Tag auf alle ausgewählten Verbindungen anzuwenden. Sie können auch auf das Kontrollkästchen klicken, um es zu deaktivieren und das Tag aus allen ausgewählten Verbindungen zu entfernen

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>Verbindungen nach Tag filtern

Nachdem Tags zu einer oder mehreren Serververbindungen hinzugefügt wurden, können Sie die Tags in der Verbindungsliste anzeigen und die Verbindungsliste nach Tags filtern.

* Um nach einem Tag zu filtern, wählen Sie das Filter Symbol neben dem Suchfeld aus.
![](../media/launch/tags-7.png)
* Sie können "or", "and" oder "Not" auswählen, um das Filter Verhalten der ausgewählten Tags zu ändern.
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>Verwenden von PowerShell zum Importieren oder Exportieren deiner Verbindungen (mit Tags)

[!INCLUDE [ps-connections](../includes/ps-connections.md)]

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Anzeigen von im Windows Admin Center verwendeten PowerShell-Skripts

Nachdem Sie eine Verbindung mit einem Server, einem Cluster oder einem PC hergestellt haben, können Sie sich die PowerShell-Skripts ansehen, die die im Windows Admin Center verfügbaren UI-Aktionen unterliegen. Klicken Sie in einem Tool in der oberen Anwendungsleiste auf das PowerShell-Symbol. Wählen Sie in der Dropdown Liste den gewünschten Befehl aus, um zum entsprechenden PowerShell-Skript zu navigieren.

![](../media/launch/showscript.png)
