---
title: Einstieg in das Windows Admin Center
description: Einstieg in das Windows Admin Center
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 02/15/2019
ms.openlocfilehash: 68b5c7b2c5bc8e93d653514b2664d96b97b07a9e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406842"
---
# <a name="get-started-with-windows-admin-center"></a>Einstieg in das Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

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

2. Sie können einen Server, einen Failovercluster oder eine hyperkonvergierte Cluster Verbindung hinzufügen:
    
   ![](../media/launch/addserver1.png)

3. Geben Sie den Namen des zu verwaltenden Servers oder Clusters ein, und klicken Sie auf **senden**. Der Server oder Cluster wird auf der Übersichtsseite zur Verbindungsliste hinzugefügt.

   ![](../media/launch/addserver2.png)

   **--ODER--**

**Massen Import mehrerer Server**

 1. Wählen Sie auf der Seite **Server Verbindung hinzufügen** die Registerkarte **Server importieren** aus.

    ![](../media/launch/import-servers.png)

 2. Klicken Sie auf **Durchsuchen** , und wählen Sie eine Textdatei aus, die ein Komma oder eine neue durch Trennzeichen getrennte Liste von FQDNs für die Server enthält, die Sie hinzufügen möchten.

> [!Note]
> Die CSV-Datei, die durch den [Export ihrer Verbindungen mit PowerShell](#use-powershell-to-import-or-export-your-connections-with-tags) erstellt wurde, enthält neben den Servernamen zusätzliche Informationen, die mit dieser Import Methode nicht kompatibel sind.

  **--ODER--**

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

Wenn Sie Windows Admin Center auf Windows Server installiert haben, ist für das einmalige Anmelden eine zusätzliche Konfiguration erforderlich.  [Konfigurieren Ihrer Umgebung für die Delegierung](../configure/user-access-control.md)

**--ODER--**

**Verwenden von *Manage as* zum Angeben von Anmelde Informationen**

Wählen Sie unter **alle Verbindungen**einen Server aus der Liste aus, und wählen Sie **verwalten als** aus, um die Anmelde Informationen anzugeben, die Sie für die Authentifizierung beim verwalteten Knoten verwenden werden:

![](../media/launch-use-6.png)

Wenn Windows Admin Center im Dienst Modus unter Windows Server ausgeführt wird, aber keine Kerberos-Delegierung konfiguriert ist, müssen Sie Ihre Windows-Anmelde Informationen erneut eingeben:

![](../media/launch-use-7.png)

Sie können die Anmelde Informationen auf alle Verbindungen anwenden, wodurch Sie für die jeweilige Browsersitzung zwischengespeichert werden. Wenn Sie Ihren Browser neu laden, müssen Sie Ihre **Manage als** Anmelde Informationen erneut eingeben.

**Lokale Administrator Kenn Wort Lösung (Runden)**

Wenn Ihre Umgebung [runden](https://technet.microsoft.com/mt227395.aspx)verwendet und Sie Windows Admin Center auf Ihrem Windows 10-PC installiert haben, können Sie die Runden-Anmelde Informationen verwenden, um sich mit dem verwalteten Knoten zu authentifizieren. **Wenn Sie dieses Szenario verwenden, bitte** [geben](http://aka.ms/WACFeedback)Sie uns Feedback.

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

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>Verwenden von PowerShell zum Importieren oder Exportieren von Verbindungen (mit Tags)

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### <a name="csv-file-format-for-importing-connections"></a>CSV-Dateiformat zum Importieren von Verbindungen

Das Format der CSV-Datei beginnt mit den vier über ```"name","type","tags","groupId"```Schriften, gefolgt von jeder Verbindung in einer neuen Zeile.

**Name** ist der voll qualifizierte Name der Verbindung.

**Typ** ist der Verbindungstyp. Für die im Windows Admin Center enthaltenen Standardverbindungen verwenden Sie eine der folgenden Aktionen:

| Verbindungstyp | Verbindungszeichenfolge |
|------|-------------------------------|
| Windows Server | msft. SME. Connection-Type. Server |
| Windows 10-PC | msft. SME. Connection-Type. Windows-Client |
| Failovercluster | msft. SME. Connection-Type. Cluster |
| Hyperkonvergierter Cluster | msft. SME. Connection-Type. hyperkonvergierter Cluster |

**Tags** sind per Pipe getrennt.

**GroupID** wird für freigegebene Verbindungen verwendet. Verwenden Sie den ```global``` Wert in dieser Spalte, um eine freigegebene Verbindung herzustellen.

### <a name="example-csv-file-for-importing-connections"></a>Beispiel-CSV-Datei zum Importieren von Verbindungen

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>Importieren von rdcman-Verbindungen

Verwenden Sie das folgende Skript, um gespeicherte Verbindungen in [rdcman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) in eine Datei zu exportieren. Anschließend können Sie die Datei in das Windows Admin Center importieren und dabei die rdcman-Gruppierungs Hierarchie mithilfe von Tags verwalten. Probieren Sie es aus!

1. Kopieren Sie den folgenden Code, und fügen Sie ihn in die PowerShell-Sitzung ein:

   ```powershell
   #Helper function for RdgToWacCsv
   function AddServers {
    param (
    [Parameter(Mandatory = $true)]
    [Xml.XmlLinkedNode]
    $node,
    [Parameter()]
    [String[]]
    $tags,
    [Parameter(Mandatory = $true)]
    [String]
    $csvPath
    )
    if ($node.LocalName -eq 'server') {
        $serverName = $node.properties.name
        $tagString = $tags -join "|"
        Add-Content -Path $csvPath -Value ('"'+ $serverName + '","msft.sme.connection-type.server","'+ $tagString +'"')
    } 
    elseif ($node.LocalName -eq 'group' -or $node.LocalName -eq 'file') {
        $groupName = $node.properties.name
        $tags+=$groupName
        $currNode = $node.properties.NextSibling
        while ($currNode) {
            AddServers -node $currNode -tags $tags -csvPath $csvPath
            $currNode = $currNode.NextSibling
        }
    } 
    else {
        # Node type isn't relevant to tagging or adding connections in WAC
    }
    return
   }

   <#
   .SYNOPSIS
   Convert an .rdg file from Remote Desktop Connection Manager into a .csv that can be imported into Windows Admin Center, maintaining groups via server tags. This will not modify the existing .rdg file and will create a new .csv file

    .DESCRIPTION
    This converts an .rdg file into a .csv that can be imported into Windows Admin Center.

    .PARAMETER RDGfilepath
    The path of the .rdg file to be converted. This file will not be modified, only read.

    .PARAMETER CSVdirectory
    Optional. The directory you wish to export the new .csv file. If not provided, the new file is created in the same directory as the .rdg file.

    .EXAMPLE
    C:\PS> RdgToWacCsv -RDGfilepath "rdcmangroup.rdg"
    #>
   function RdgToWacCsv {
    param(
        [Parameter(Mandatory = $true)]
        [String]
        $RDGfilepath,
        [Parameter(Mandatory = $false)]
        [String]
        $CSVdirectory
    )
    [xml]$RDGfile = Get-Content -Path $RDGfilepath
    $node = $RDGfile.RDCMan.file
    if (!$CSVdirectory){
        $csvPath = [System.IO.Path]::GetDirectoryName($RDGfilepath) + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    } else {
        $csvPath = $CSVdirectory + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    }
    New-item -Path $csvPath
    Add-Content -Path $csvPath -Value '"name","type","tags"'
    AddServers -node $node -csvPath $csvPath
    Write-Host "Converted $RDGfilepath `nOutput: $csvPath"
   }
   ```

2. Um einen zu erstellen. CSV-Datei, führen Sie den folgenden Befehl aus:

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. Importieren Sie das resultierende. CSV-Datei in in Windows Admin Center, und die gesamte rdcman-Gruppierungs Hierarchie wird durch Tags in der Verbindungsliste dargestellt. Weitere Informationen finden [Sie unter Verwenden von PowerShell zum Importieren oder Exportieren von Verbindungen (mit Tags)](#use-powershell-to-import-or-export-your-connections-with-tags).

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Anzeigen von im Windows Admin Center verwendeten PowerShell-Skripts

Nachdem Sie eine Verbindung mit einem Server, einem Cluster oder einem PC hergestellt haben, können Sie sich die PowerShell-Skripts ansehen, die die im Windows Admin Center verfügbaren UI-Aktionen unterliegen. Klicken Sie in einem Tool in der oberen Anwendungsleiste auf das PowerShell-Symbol. Wählen Sie in der Dropdown Liste den gewünschten Befehl aus, um zum entsprechenden PowerShell-Skript zu navigieren.

![](../media/launch/showscript.png)