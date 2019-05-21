---
title: Erste Schritte mit Windows Admin Center
description: Erste Schritte mit Windows Admin Center
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/15/2019
ms.openlocfilehash: f4fd9f69e75ed80bbdb345b4041c2337c65ec2e6
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2019
ms.locfileid: "63742549"
---
# <a name="get-started-with-windows-admin-center"></a>Erste Schritte mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows Admin Center installiert unter Windows 10

> [!IMPORTANT]
> Sie müssen ein Mitglied der lokalen Gruppe Administratoren Windows Admin Center auf Windows 10 verwenden werden.

### <a name="selecting-a-client-certificate"></a>Ein Clientzertifikat auswählen

Beim ersten Öffnen Sie Windows Admin Center unter Windows 10, achten Sie darauf, wählen Sie die *Windows Admin Center Client* Zertifikat (Andernfalls erhalten Sie einen HTTP 403-Fehler, die aufgrund unzureichender "kann nicht auf diese Seite gelangen").

In Microsoft Edge, wenn Sie dieses Dialogfeld dazu aufgefordert werden:
 
1. Klicken Sie auf **Weitere Optionen**

    ![](../media/launch-cert-1.png)

2. Wählen Sie das Zertifikat mit der Bezeichnung **Windows Admin Center Client** , und klicken Sie auf **OK**

    ![](../media/launch-cert-2.png)

3. Stellen Sie sicher, dass **Always Allow Access** ausgewählt ist, und klicken Sie auf **zulassen**

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>Herstellen einer Verbindung mit den verwalteten Knoten und Cluster

Nachdem Sie die Installation von Windows Admin Center abgeschlossen haben, können Sie Server oder Cluster, von der hauptübersichtsseite verwalten hinzufügen.

 **Fügen Sie einem einzelnen Server oder Cluster als verwalteten Knoten hinzu.**

 1. Klicken Sie auf **+ hinzufügen** unter **alle Verbindungen**.

    ![](../media/launch/addserver0.png)

 2. Wählen Sie eine Verbindung zum Server, Failovercluster oder Hyper-Converged Cluster hinzufügen:
    
    ![](../media/launch/addserver1.png)

 3. Geben Sie den Namen des Servers oder -Cluster zu verwalten, und klicken Sie auf **senden**. Der Server oder Cluster werden Ihre Liste der auf der Seite "Übersicht" hinzugefügt werden.

    ![](../media/launch/addserver2.png)

   **-- OR --**

**Massenimport mehrere Server**

 1. Auf der **Serververbindung hinzufügen** Seite die **Importserver** Registerkarte.

    ![](../media/launch/import-servers.png)

 2. Klicken Sie auf **Durchsuchen** und wählen Sie eine Textdatei, die ein Komma enthält, oder neue Zeile getrennte Liste von FQDNs für die Server, die Sie hinzufügen möchten.

    **-- OR --**

**Fügen Sie Server hinzu, indem das Durchsuchen von Active Directory**

 1. Auf der **Serververbindung hinzufügen** Seite die **Durchsuchen von Active Directory** Registerkarte.

    ![](../media/launch/search-ad.png)

 2. Geben Sie die Suchkriterien ein, und klicken Sie auf **Suche**. Platzhalter (*) werden unterstützt.

 3. Nachdem die Suche abgeschlossen ist: Wählen Sie eine oder mehrere der Ergebnisse, optional Tags hinzufügen und klicken Sie auf **hinzufügen**.

## <a name="authenticate-with-the-managed-node"></a>Authentifizieren Sie sich mit den verwalteten Knoten ##

Windows Admin Center unterstützt mehrere Mechanismen für die Authentifizierung mit einem verwalteten Knoten. Einmaliges Anmelden ist die Standardeinstellung.

**Einmaliges Anmelden**

Sie können Ihre aktuellen Windows-Anmeldeinformationen verwenden, für die Authentifizierung mit den verwalteten Knoten. Dies ist die Standardeinstellung, und Windows Admin Center die Anmeldung versucht, wenn Sie einen Server hinzufügen. 

**Einmaliges Anmelden bei der Bereitstellung als Dienst unter Windows Server**

Wenn Sie Windows Admin Center unter Windows Server installiert haben, ist zusätzliche Konfiguration für einmaliges Anmelden erforderlich.  [Konfigurieren Sie Ihre Umgebung für die Delegierung](..\configure\user-access-control.md)

**-- OR --**

**Verwendung *verwalten als* beim Angeben von Anmeldeinformationen**

Klicken Sie unter **alle Verbindungen**, wählen Sie einen Server aus der Liste, und wählen Sie **verwalten als** um die Anmeldeinformationen anzugeben, die Sie verwenden den verwalteten Knoten zu authentifizieren:

![](../media/launch-use-6.png)

Wenn Windows Admin Center im Dienstmodus unter Windows Server ausgeführt wird, aber Sie verfügen nicht über die Kerberos-Delegierung konfiguriert, müssen Sie Ihre Windows-Anmeldeinformationen erneut eingeben:

![](../media/launch-use-7.png)

Sie können die Anmeldeinformationen an alle Verbindungen anwenden, die sie für diese bestimmte Browsersitzung zwischengespeichert werden. Wenn Sie Ihren Browser neu laden, müssen Sie erneut eingeben Ihrer **verwalten als** Anmeldeinformationen.

**Local Administrator Password Solution (LAPS)**

Wenn in Ihrer Umgebung verwendet [LAPS](https://technet.microsoft.com/mt227395.aspx), können Sie LAPS-Anmeldeinformationen für die Authentifizierung mit den verwalteten Knoten. **Wenn Sie dieses Szenario verwenden, wenden Sie** [Feedback geben](http://aka.ms/WACFeedback).

## <a name="using-tags-to-organize-your-connections"></a>Verwenden von Tags zum Organisieren von Verbindungen

Sie können Tags verwenden, zu erkennen und Filtern verwandter Server in der Verbindungsliste Ihrer.  Dadurch können Sie eine Teilmenge Ihrer Server in der Liste angezeigt.  Dies ist besonders nützlich, wenn Sie die Anzahl von Verbindungen verfügen.

### <a name="edit-tags"></a>Bearbeiten von tags

* Wählen Sie eine oder mehrere Server in der Liste alle Verbindungen
* Klicken Sie unter **alle Verbindungen**, klicken Sie auf **Tags bearbeiten**

![](../media/launch/tags-5.png)

Die **Verbindung Tags bearbeiten** Bereich können Sie sich ändern, hinzufügen oder Entfernen von Tags in Ihrem ausgewählten Verbindung(en) angezeigt:

* Wählen Sie zum Hinzufügen eines neuen Tags auf Ihre ausgewählten Verbindung(en) **Tag hinzufügen** , und geben Sie den Namen des Tags, Sie verwenden möchten.

* Aktivieren Sie das Kontrollkästchen neben den Namen des Tags, die, den Sie anwenden möchten, um die ausgewählten Verbindungen mit einem vorhandenen Tagnamen zu markieren.

* Deaktivieren Sie das Kontrollkästchen neben dem Tag, die, das Sie entfernen möchten, um ein Tag aus allen ausgewählten Verbindungen zu entfernen.

* Wenn ein Tag auf eine Teilmenge der ausgewählten Verbindungen angewendet wird, wird das Kontrollkästchen in einem zwischengelagerten Zustand angezeigt. Sie können das Kontrollkästchen, um es überprüfen und wenden das Tag für alle ausgewählten Verbindungen oder klicken erneut, um es deaktivieren und entfernen Sie das Tag von allen ausgewählten Verbindungen klicken.

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>Filtern von Verbindungen nach tag

Nachdem der Server-Verbindungen für eine oder mehrere Tags hinzugefügt haben, können Sie zeigen Sie die Tags in der Verbindungsliste und die Verbindungsliste nach Tags filtern.

* Wählen Sie das Symbol "Filter" neben dem Suchfeld zum Filtern nach einem Tag.
![](../media/launch/tags-7.png)
* Sie können auswählen, "or", "und" oder "not", um das Verhalten der ausgewählten Tags zu ändern.
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>Verwenden von PowerShell zum Importieren oder Exportieren von Verbindungen (mit Tags)

> Gilt für: Windows Admin Center – Vorschau

Windows Admin Center Preview umfasst ein PowerShell-Modul zum Importieren oder exportieren Ihre Verbindungsliste.

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### <a name="csv-file-format-for-importing-connections"></a>CSV-Dateiformat für das Importieren von Verbindungen

Das Format der CSV-Datei beginnt mit den vier Überschriften ```"name","type","tags","groupId"```, gefolgt von den einzelnen Verbindungen in einer neuen Zeile.

**Namen** ist der FQDN der Verbindung

**Typ** ist der Verbindungstyp. Für die standardverbindungen in Windows Admin Center enthalten verwenden Sie eine der folgenden:

| Verbindungstyp | Verbindungszeichenfolge |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10-PCs | msft.sme.connection-type.windows-client |
| Failovercluster | msft.sme.connection-type.cluster |
| Hyperkonvergenten Cluster | msft.sme.connection-type.hyper-converged-cluster |

**Tags** sind senkrechte Striche getrennte.

**GroupId** für freigegebene Verbindungen verwendet. Verwenden Sie den Wert ```global``` in dieser Spalte, damit diese gemeinsam genutzte Verbindung.

### <a name="example-csv-file-for-importing-connections"></a>Beispiel-CSV-Datei für das Importieren von Verbindungen

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>Importieren von RDCman Verbindungen

Verwenden Sie das folgende Skript, um gespeicherte Verbindungen in exportieren [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) in eine Datei. Sie können dann die Datei in Windows Admin Center, importieren, verwalten Ihre RDCMan Gruppierungshierarchie mithilfe von Tags. Probieren Sie es aus!

1. Kopieren Sie den folgenden Code in der PowerShell-Sitzung:

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

2. Zum Erstellen einer. CSV-Datei den folgenden Befehl ausführen:

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. Importieren Sie das resultierende. CSV-Datei in Windows Admin Center und Ihre RDCMan Gruppierungshierarchie wird mithilfe von Tags in der Verbindungsliste dargestellt. Weitere Informationen finden Sie unter [mithilfe von PowerShell zum Importieren oder Exportieren von Verbindungen (mit Tags)](#use-powershell-to-import-or-export-your-connections-with-tags).

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Anzeigen von PowerShell-Skripts, die in Windows Admin Center verwendet werden.

Sobald Sie mit einem Server, Cluster oder einem PC verbunden haben, können Sie die PowerShell-Skripts diese Leistung die UI-Aktionen verfügbar in Windows Admin Center ansehen. Klicken Sie in einem Tool auf das Symbol "PowerShell" in der oberen Leiste. Wählen Sie einen Befehl von Interesse sind, aus der Dropdownliste aus, um zum entsprechenden PowerShell-Skript zu navigieren.

![](../media/launch/showscript.png)