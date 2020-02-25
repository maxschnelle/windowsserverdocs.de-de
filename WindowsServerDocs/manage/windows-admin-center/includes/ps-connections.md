```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to a .csv file
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from a .csv file
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files, and remove any connections that are not explicitly in the imported file using the -prune switch parameter 
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv" -prune
```
### <a name="csv-file-format-for-importing-connections"></a>CSV-Dateiformat zum Importieren von Verbindungen

Das Format der CSV-Datei beginnt mit den vier Überschriften ```"name","type","tags","groupId"```, gefolgt von jeder Verbindung, jeweils in einer neuen Zeile.

**name** ist der FQDN der Verbindung

**type** ist der Verbindungstyp. Für die im Windows Admin Center enthaltenen Standardverbindungen verwendest du eine der folgenden Optionen:

| Verbindungstyp | Verbindungszeichenfolge |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10-PC | msft.sme.connection-type.windows-client |
| Failovercluster | msft.sme.connection-type.cluster |
| Hyperkonvergenter Cluster | msft.sme.connection-type.hyper-converged-cluster |

**tags** werden durch den Pipe-Operator (senkrechter Strich) getrennt.

**groupId** wird für freigegebene Verbindungen verwendet. Verwende den Wert ```global``` in dieser Spalte, um diese Verbindung freizugeben.

> [!NOTE]
> Das Ändern der freigegebenen Verbindungen ist auf Gatewayadministratoren beschränkt. Jeder Benutzer kann PowerShell verwenden, um seine persönliche Verbindungsliste zu ändern.

### <a name="example-csv-file-for-importing-connections"></a>CSV-Beispieldatei zum Importieren von Verbindungen

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>Importieren von RDCman-Verbindungen

Verwende das folgende Skript, um gespeicherte Verbindungen in [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) in eine Datei zu exportieren. Anschließend kannst du die Datei in Windows Admin Center importieren und dabei deine RDCMan-Gruppierungshierarchie mithilfe von Tags erhalten. Probier es aus!

1. Kopiere den folgenden Code, und füge ihn in die PowerShell-Sitzung ein:

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

2. Um eine CSV-Datei zu erstellen, führst du den folgenden Befehl aus:

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. Importiere die resultierende CSV-Datei in Windows Admin Center, und deine gesamte RDCMan-Gruppierungshierarchie wird durch Tags in der Verbindungsliste dargestellt. Details findest du unter [Verwenden von PowerShell zum Importieren oder Exportieren deiner Verbindungen (mit Tags)](#use-powershell-to-import-or-export-your-connections-with-tags).