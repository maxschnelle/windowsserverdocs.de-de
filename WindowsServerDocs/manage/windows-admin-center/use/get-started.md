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
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296652"
---
# Erste Schritte mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## Windows Admin Center auf Windows 10 installiert

> [!IMPORTANT]
> Sie müssen ein Mitglied der lokalen Administratorgruppe verwenden Sie Windows Admin Center auf Windows 10 sein.

### Auswählen eines Clientzertifikats

Beim ersten Öffnen Sie Windows Admin Center auf Windows 10, stellen Sie sicher, dass das *Windows Admin Center-Client* -Zertifikat (andernfalls HTTP 403 Fehlermeldung "kann nicht zu dieser Seite abgerufen" erhalten Sie).

In Microsoft Edge, wenn dieses Dialogfeld angezeigt werden:
 
1. Klicken Sie auf **Weitere Optionen**

    ![](../media/launch-cert-1.png)

2. Wählen Sie das Zertifikat mit der Bezeichnung **Windows Admin Center-Client** , und klicken Sie auf **OK**

    ![](../media/launch-cert-2.png)

3. Stellen Sie sicher, dass **Immer Zugriff erlauben** aktiviert ist, und klicken Sie auf **Zulassen**

    ![](../media/launch-cert-3.png)

## Herstellen einer Verbindung mit verwalteten Knoten und Cluster

Nachdem Sie die Installation von Windows Admin Center abgeschlossen haben, können Sie Servern oder Clustern, von der Haupt-Übersicht verwalten hinzufügen.

 **Fügen Sie einen einzelnen Server oder einem Cluster als verwalteten Knoten hinzu.**

 1. Klicken Sie unter **Alle Verbindungen**auf **+ Hinzufügen** .

    ![](../media/launch/addserver0.png)

 2. Wählen Sie eine Verbindung zum Server, Failovercluster oder Hyper-converged Cluster hinzufügen:
    
    ![](../media/launch/addserver1.png)

 3. Geben Sie den Namen des Servers oder Cluster-zu verwalten, und klicken Sie auf **übermitteln**. Ihre Verbindungsliste auf der Seite "Übersicht" wird den Server oder Cluster hinzugefügt werden.

    ![](../media/launch/addserver2.png)

   **-- ODER --**

**Massenimport mehrere Server importieren**

 1. Wählen Sie die Registerkarte **Import-Server** , auf der Seite **Server-Verbindung hinzufügen** .

    ![](../media/launch/import-servers.png)

 2. Klicken Sie auf **Durchsuchen** , und wählen Sie eine Textdatei, die enthält ein Komma oder eine neue Zeile getrennt, Liste der FQDNs für die Server, die Sie hinzufügen möchten.

    **-- ODER --**

**Hinzufügen von Servern durch Suchen in Active Directory**

 1. Wählen Sie auf der Seite **Server-Verbindung hinzufügen** der Registerkarte " **Suchen in Active Directory** ".

    ![](../media/launch/search-ad.png)

 2. Geben Sie die Suchkriterien, und klicken Sie auf **Suchen**. Platzhalter (*) werden unterstützt.

 3. Nach Abschluss des Suchvorgangs - wählen Sie eine oder mehrere der Ergebnisse, optional fügen Sie Tags hinzu, und klicken Sie auf **Hinzufügen**.

## Authentifizieren Sie mit dem verwalteten Knoten ##

Windows Admin Center unterstützt mehrere Mechanismen für die Authentifizierung mit einem verwalteten Knoten. Einmaliges Anmelden ist die Standardeinstellung.

**Einmaliges Anmelden**

Sie können Ihre aktuellen Windows-Anmeldeinformationen gemacht: authentifizieren mit dem verwalteten Knoten verwenden. Dies ist die Standardeinstellung, und Windows Admin Center versucht das anmelden, wenn Sie einen Server hinzufügen. 

**Einmaliges Anmelden bei der Bereitstellung als Dienst unter Windows Server**

Wenn Sie Windows Admin Center auf Windows Server installiert haben, ist die zusätzliche Konfiguration erforderlich für einmaliges Anmelden.  [Konfigurieren Sie Ihre Umgebung für Delegierungszwecke vertraut](..\configure\user-access-control.md)

**-- ODER --**

**Verwenden Sie zum Angeben von Anmeldeinformationen *Verwalten als***

Klicken Sie unter **Alle Verbindungen**wählen Sie einen Server aus der Liste, und wählen Sie **Verwalten als** die Anmeldeinformationen angeben, die Sie zum Authentifizieren des auf dem verwalteten Knoten verwenden:

![](../media/launch-use-6.png)

Wenn Windows Admin Center im Service-Modus unter Windows Server ausgeführt wird, aber Sie keine Kerberos-Delegierung konfiguriert haben, müssen Sie Ihre Windows-Anmeldeinformationen erneut eingeben:

![](../media/launch-use-7.png)

Sie können die Anmeldeinformationen für alle Verbindungen anwenden, die sie für diese Sitzung bestimmten Browser zwischengespeichert werden. Wenn Sie Ihren Browser erneut laden, müssen Sie Ihre **Verwalten als** Anmeldeinformationen erneut eingeben.

**Lokaler Administrator Password Solution (runden)**

Wenn Ihre Umgebung [runden](https://technet.microsoft.com/mt227395.aspx)verwendet, können Sie runden Anmeldeinformationen verwenden, um mit dem verwalteten Knoten zu authentifizieren. **Wenn Sie dieses Szenario verwenden** [Feedback bereitstellen](http://aka.ms/WACFeedback).

## Verwendung von Tags für Ihre Verbindungen zu organisieren.

Sie können Tags verwenden, zu identifizieren und verwandte Servern in Ihre Verbindungsliste zu filtern.  Dadurch können Sie eine Teilmenge der Server in der Verbindungsliste anzuzeigen.  Dies ist besonders hilfreich, wenn Sie viele Verbindungen verfügen.

### Bearbeiten von tags

* Wählen Sie eine oder mehrere Server in der Liste alle Verbindungen
* Klicken Sie unter **Alle Verbindungen**auf **Tags bearbeiten**

![](../media/launch/tags-5.png)

Der Bereich **Verbindung-Tags bearbeiten** können Sie ändern, hinzufügen oder Entfernen von Tags aus der ausgewählten Verbindung(en):

* Um ein neues Tag Ihre ausgewählten Verbindung(en) hinzuzufügen, wählen Sie **Tag hinzufügen** , und geben Sie den Tagnamen, die, den Sie verwenden möchten.

* Um die ausgewählten Verbindungen mit einem vorhandenen Tagnamen zu markieren, aktivieren Sie das Kontrollkästchen neben dem Tagnamen, die, den Sie anwenden möchten.

* Um ein Tag aus alle ausgewählten Verbindungen zu entfernen, deaktivieren Sie das Kontrollkästchen neben dem Tag, das Sie entfernen möchten.

* Wenn ein Tag auf eine Teilmenge der ausgewählten Verbindungen angewendet wird, wird das Kontrollkästchen in einem unbestimmten Zustand angezeigt. Sie können das Kontrollkästchen, damit Probieren Sie es und wenden das Tag mit allen ausgewählten-Verbindungen, oder klicken erneut, um es deaktivieren und entfernen Sie das Tag aus allen ausgewählten Verbindungen klicken.

![](../media/launch/tags-6.png)

### Filter-Verbindungen von tag

Nachdem ein oder mehrere Server-Verbindungen Tags hinzugefügt haben, können Sie die Tags auf der Verbindungsliste anzeigen und Filtern Sie die Verbindungsliste von Tags.

* Wählen Sie zum Filtern von einem Tag das Filtersymbol neben das Suchfeld ein.
![](../media/launch/tags-7.png)
* Wählen Sie "oder", "und" oder "nicht", um das Filterverhalten ausgewählten Tags zu ändern.
![](../media/launch/tags-8.png)

## Verwenden von PowerShell zum Importieren oder exportieren die Verbindungen (mit Tags)

> Gilt für: Windows Admin Center Vorschau

Windows Admin Center – Vorschau enthält ein PowerShell-Modul zum Importieren oder Exportieren der Verbindungsliste.

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### CSV-Datei-Format für den Import von Verbindungen

Das Format der CSV-Datei beginnt mit der vier Überschriften ```"name","type","tags","groupId"```, gefolgt von jede Verbindung in einer neuen Zeile.

**Name** ist der vollqualifizierte Domänenname der Verbindung

**Typ** ist den Verbindungstyp. Für die Standard-Verbindungen mit Windows Admin Center enthalten verwenden Sie eine der folgenden:

| Verbindungstyp | Verbindungszeichenfolge |
|------|-------------------------------|
| Windows Server | msft.SME.Connection type.server |
| Windows 10-PC | msft.SME.Connection-type.windows-client |
| Failovercluster | msft.SME.Connection type.cluster |
| Zusammengeführte Cluster | msft.SME.Connection type.hyper zusammengeführt cluster |

**Tags** werden durch umgekehrten Schrägstrich.

**GroupId** wird für gemeinsam genutzte Verbindungen verwendet. Verwenden Sie den Wert ```global``` in dieser Spalte, dies eine gemeinsame Verbindung herzustellen.

### Beispiel-CSV-Datei für den Import von Verbindungen

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## Importieren von RDCman-Verbindungen

Verwenden Sie das folgende Skript, um die gespeicherte Verbindungen in [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) in eine Datei zu exportieren. Sie können dann die Datei in Windows Admin Center importieren, verwalten Ihre RDCMan Gruppierungshierarchie mithilfe von Tags umgesetzt. Probieren Sie es aus!

1. Kopieren Sie und fügen Sie den folgenden Code in der PowerShell-Sitzung:

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

2. Zum Erstellen einer. CSV-Datei, führen Sie den folgenden Befehl aus:

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. Importieren Sie das resultierende. CSV-Datei in Windows Admin Center und der von RDCMan-Gruppierungshierarchie wird durch Tags in der Verbindungsliste dargestellt werden. Weitere Informationen finden Sie unter [Verwenden von PowerShell zum Importieren oder exportieren die Verbindungen (mit Tags)](#use-powershell-to-import-or-export-your-connections-with-tags).

## Anzeigen von PowerShell-Skripts, die in Windows Admin Center verwendet

Sobald Sie mit Servern, Cluster oder PC verbunden haben, können Sie die PowerShell-Skripts die Leistung der UI-Aktionen verfügbar im Windows Admin Center anzeigen. Klicken Sie in einem Tool auf das PowerShell-Symbol in der oberen Leiste. Wählen Sie einen Befehl von Interesse sind, aus der Dropdownliste aus, um das entsprechende PowerShell-Skript zu navigieren.

![](../media/launch/showscript.png)