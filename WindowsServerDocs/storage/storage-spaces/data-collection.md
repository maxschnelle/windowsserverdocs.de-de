---
title: Sammeln von Diagnosedaten mit "direkte Speicherplätze"
description: Grundlegendes zu Storage Spaces direkte Tools zur Datensammlung, mit konkrete Beispiele führen und deren Verwendung.
keywords: Speicherplätze "," Datensammlung "," Problembehandlung "," ereigniskanäle, Get-SDDCDiagnosticInfo
ms.assetid: ''
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.localizationpriority: ''
ms.openlocfilehash: 51cf96fb462b68f2ba01d49642a858430c71e9f5
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469604"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>Sammeln von Diagnosedaten mit "direkte Speicherplätze"

> Gilt für: Windows Server 2019, Windows Server 2016

Es gibt verschiedene Diagnosetools, die zum Erfassen der Daten erforderlich, um die Problembehandlung von "direkte Speicherplätze" und Failover-Cluster verwendet werden können. In diesem Artikel konzentrieren wir uns auf **Get-SDDCDiagnosticInfo** -ein eine Touch-Tool, das alle relevanten Informationen, denen Sie Ihrem Cluster diagnostizieren können erfasst werden.

Angegeben, die die Protokolle und andere Informationen, die **Get-SDDCDiagnosticInfo** Dichte, die Informationen zur Problembehandlung unten werden für die Problembehandlung der erweiterten zu beheben, wurde eskaliert und, die möglicherweise, hilfreich sind sind die Daten an Microsoft gesendet werden, für die Selektierung erforderlich.

## <a name="installing-get-sddcdiagnosticinfo"></a>Installieren von Get-SDDCDiagnosticInfo

Die **Get-SDDCDiagnosticInfo** PowerShell-Cmdlet (Alias) **Get-PCStorageDiagnosticInfo**, zuvor bekannt als **Test-StorageHealth**) dienen zum Sammeln von Protokollen, und führen Sie integritätsprüfungen für Failover-Clusterunterstützung (Cluster, Ressourcen, Netzwerke, Knoten), Speicherplätze () Physische Datenträger, Gehäuse, virtuelle Datenträger), Cluster Shared Volumes, SMB-Dateifreigaben und Datendeduplizierung. 

Es gibt zwei Methoden zum Installieren des Skripts, die beide sind unten sind.

### <a name="powershell-gallery"></a>PowerShell-Katalog

Die [PowerShell-Katalog](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo) ist eine Momentaufnahme des GitHub-Repositorys. Beachten Sie, dass Elemente aus dem PowerShell-Katalog installiert die neueste Version des PowerShellGet-Moduls, die in Windows 10, im Windows Management Framework (WMF) 5.0 oder in der MSI-basierten Installer (für PowerShell 3 und 4) verfügbar ist.

Sie können das Modul installieren, mit dem folgenden Befehl in PowerShell mit Administratorrechten aus:

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
```

Um das Modul zu aktualisieren, führen Sie den folgenden Befehl in PowerShell aus:

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

Die [GitHub-Repository](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/) ist die aktuelle Version des Moduls, da wir hier kontinuierlich durchlaufen werden. Um das Modul von GitHub zu installieren, laden Sie das aktuelle Modul aus der [Archiv](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip) und extrahieren Sie das Verzeichnis PrivateCloud.DiagnosticInfo der richtige PowerShell-Module-Pfad, auf die von ```$env:PSModulePath```

``` PowerShell
# Allowing Tls12 and Tls11 -- e.g. github now requires Tls12
# If this is not set, the Invoke-WebRequest fails with "The request was aborted: Could not create SSL/TLS secure channel."
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$module = 'PrivateCloud.DiagnosticInfo'
Invoke-WebRequest -Uri https://github.com/PowerShell/$module/archive/master.zip -OutFile $env:TEMP\master.zip
Expand-Archive -Path $env:TEMP\master.zip -DestinationPath $env:TEMP -Force
if (Test-Path $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module) {
    rm -Recurse $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module -ErrorAction Stop
    Remove-Module $module -ErrorAction SilentlyContinue
} else {
    Import-Module $module -ErrorAction SilentlyContinue
} 
if (-not ($m = Get-Module $module -ErrorAction SilentlyContinue)) {
    $md = "$env:ProgramFiles\WindowsPowerShell\Modules"
} else {
    $md = (gi $m.ModuleBase -ErrorAction SilentlyContinue).PsParentPath
    Remove-Module $module -ErrorAction SilentlyContinue
    rm -Recurse $m.ModuleBase -ErrorAction Stop
}
cp -Recurse $env:TEMP\$module-master\$module $md -Force -ErrorAction Stop
rm -Recurse $env:TEMP\$module-master,$env:TEMP\master.zip
Import-Module $module -Force

``` 

Verschieben Sie Wenn Sie dieses Modul in einem offline-Cluster abrufen müssen, laden die ZIP-Datei, es auf Ihre Ziel-Serverknoten, und installieren Sie das Modul.

## <a name="gathering-logs"></a>Sammeln von Protokollen

Nachdem Sie die Kanäle für Ereignisse aktiviert und den Installationsvorgang abgeschlossen haben, können das Get-SDDCDiagnosticInfo-PowerShell-Cmdlet im Modul Sie zum Abrufen:

- Berichte, auf die Integrität des Netzwerkspeichers sowie Informationen zu fehlerhaften Komponenten
- Berichte, die Speicherkapazität von Pool, Volumen und dedupliziertes volume
- Ereignisprotokoll für alle Knoten des Clusters und eine Zusammenfassung Fehlerbericht

Davon ausgehen, dass der speichercluster der Name enthält *"CLUS01".*

Für einen Remotespeicher-Cluster ausgeführt wird:

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

Zum Ausführen von lokal auf die gruppierten Knoten "Speicher" aus:

``` PowerShell
Get-SDDCDiagnosticInfo
```

Um Ergebnisse in einem angegebenen Ordner zu speichern:

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

Hier ist ein Beispiel für diesen auf einem echten Cluster Fall:

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

Wie Sie sehen können, werden Skripts Überprüfung des aktuellen Status des Clusters auch durchführen.

![Data Collection-Powershell-screenshot](media/data-collection/CollectData.png)

Wie Sie sehen können, werden alle Daten in SDDCDiagTemp Ordner geschrieben.

![Daten im Datei-Explorer-screenshot](media/data-collection/CollectDataFolder.png)

Nachdem das Skript abgeschlossen ist, wird es in Ihrem Benutzerverzeichnis ZIP erstellt.

![Daten-Zip im Powershell-screenshot](media/data-collection/CollectDataResult.png)

Lassen Sie uns einen Bericht generieren, in eine Textdatei

```PowerShell
#find the latest diagnostic zip in UserProfile
    $DiagZip=(get-childitem $env:USERPROFILE | where Name -like HealthTest*.zip)
    $LatestDiagPath=($DiagZip | sort lastwritetime | select -First 1).FullName
#expand to temp directory
    New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
    Expand-Archive -Path $LatestDiagPath -DestinationPath D:\SDDCDiagTemp -Force
#generate report and save to text file
    $report=Show-SddcDiagnosticReport -Path D:\SDDCDiagTemp
    $report | out-file d:\SDDCReport.txt
    
```

Zu Referenzzwecken ist hier ein Link zu der [Beispielbericht](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt) und [Beispiel-Zip](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP).

Sehen Sie sich dieses in Windows Admin Center (Version 1812 oder höher), navigieren zu der *Diagnose* Registerkarte. Wie Sie im folgenden Screenshot sehen, können Sie 

- Installieren von Tools für die Diagnose
- Aktualisieren sie die (falls sie veraltet sind) 
- Planen der täglichen Diagnose ausgeführt wird (Diese weisen eine mit geringen Auswirkungen auf Ihr System, in der Regel < 5 Minuten im Hintergrund und wird nicht mehr als 500 MB in Ihrem Cluster dauern)
- Ansicht gesammelt zuvor Diagnoseinformationen, weisen Sie ihm unterstützen, oder selbst eine Analyse durchführen sollen.

![Screenshot der WAC](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>Ausgabe von Get-SDDCDiagnosticInfo

Im folgenden werden die Dateien, die in der ZIP-Ausgabe von Get-SDDCDiagnosticInfo enthalten.

### <a name="health-summary-report"></a>Zusammenfassender Integritätsbericht

Zusammenfassender Integritätsbericht wird als gespeichert:
- 0_CloudHealthSummary.log

Diese Datei wird generiert, nachdem Analyse aller Daten erfasst und eine kurze Zusammenfassung Ihres Systems bereitstellen soll. Es enthält:

- Systeminformationen
- Übersicht über das Storage-Integrität (Anzahl von Knoten einrichten, Ressourcen online sind, freigegebene Clustervolumes online, fehlerhafter Komponenten usw.).
- Informationen zu fehlerhaften Komponenten (Clusterressourcen, die offline, fehlerhaften oder ausstehenden online sind.)
- Firmware- und Treiberversionen-Informationen
- Pool, die physischen Datenträger und volumedetails
- Speicherleistung (Leistung, die Leistungsindikatoren erfasst werden)

In diesem Bericht wird ständig aktualisiert wird, um weitere nützliche Informationen enthalten. Die neuesten Informationen finden Sie unter den [GitHub README](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md).

### <a name="logs-and-xml-files"></a>Protokolle und XML-Dateien

Das Skript führt verschiedene Protokolldateien Sammeln von Skripts und speichert die Ausgabe als XML-Dateien. Wir sammeln Protokolle für Cluster und die Integrität, Systeminformationen (MSInfo32), ungefilterten-Ereignisprotokolle (Failover-Clusterunterstützung, Dis Diagnose, hyper-V, Speicherplätze und mehr) und Storage Diagnoseinformationen (Betriebsprotokolle). Die neuesten Informationen, auf welche Informationen gesammelt werden, finden Sie unter den [GitHub README (was wir erfassen)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include).

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>Nutzen Sie die XML-Dateien aus Get-PCStorageDiagnosticInfo
Sie können die Daten aus der XML-Dateien bereitgestellt, die in von gesammelten Daten nutzen die **Get-PCStorageDiagnosticInfo** Cmdlet. Diese Dateien enthalten Informationen zu den virtuellen Datenträger, physischen Datenträgern, grundlegende Informationen und andere PowerShell-bezogene Ausgaben. 

Um die Ergebnisse der Ausgaben anzuzeigen, öffnen Sie ein PowerShell-Fenster, und führen Sie die folgenden Schritte aus. 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>Was Sie als Nächstes zu erwarten?
Viele Verbesserungen und neue Cmdlets zur Integrität des SDDC-System zu analysieren.
Feedback zu was Sie anzeigen, indem Sie mögliche Probleme möchten [hier](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues). Darüber hinaus können Sie nützliche Änderungen am Skript, durch die Übermittlung beitragen eine [Pull-Anforderung](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls).
