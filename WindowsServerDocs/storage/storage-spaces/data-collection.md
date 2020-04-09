---
title: Sammeln von Diagnosedaten mit direkte Speicherplätze
description: Grundlegendes zu direkte Speicherplätze Tools für die Datensammlung, mit speziellen Beispielen, wie diese ausgeführt und verwendet werden.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.openlocfilehash: 75a74017f48b357dd029b062a7ce06775836bd0a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858963"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>Sammeln von Diagnosedaten mit direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

Es gibt verschiedene Diagnosetools, die verwendet werden können, um die für die Problembehandlung von direkte Speicherplätze und Failoverclustern erforderlichen Daten zu erfassen. In diesem Artikel konzentrieren wir uns auf " **Get-sddcdiagnosticinfo** ": ein eingabetool, das alle relevanten Informationen sammelt, um Sie bei der Diagnose Ihres Clusters zu unterstützen.

Da die Protokolle und andere Informationen, die " **Get-sddcdiagnosticinfo** " aufweisen, dicht sind, sind die Informationen zur Problembehandlung, die nachstehend beschrieben werden, hilfreich bei der Behebung erweiterter Probleme, die eskaliert wurden und möglicherweise erfordern, dass Daten für die Auslagerung an Microsoft gesendet werden.

## <a name="installing-get-sddcdiagnosticinfo"></a>Installieren von "Get-sddcdiagnosticinfo"

Das PowerShell-Cmdlet **Get-sddcdiagnosticinfo** (auch bekannt als **Get-pcstoragediagnosticinfo**, früher als **Test-storagehealth**bezeichnet) kann verwendet werden, um Protokolle für Failoverclustering (Cluster, Ressourcen, Netzwerke, Knoten), Speicherplätze (physische Datenträger, Gehäuse, virtuelle Datenträger), freigegebene Clustervolumes, SMB-Dateifreigaben und Deduplizierung zu erfassen und auszuführen. 

Es gibt zwei Methoden zum Installieren des Skripts, von denen beide nachfolgend beschrieben werden.

### <a name="powershell-gallery"></a>PowerShell-Katalog

Der [PowerShell-Katalog](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo) ist eine Momentaufnahme des GitHub-Repository. Beachten Sie, dass die Installation von Elementen aus dem PowerShell-Katalog die neueste Version des PowerShellGet-Moduls erfordert, das in Windows 10, in Windows Management Framework (WMF) 5,0 oder im MSI-basierten Installationsprogramm (für PowerShell 3 und 4) verfügbar ist.

Während dieses Vorgangs wird auch die neueste Version der [Microsoft-Netzwerk Diagnosetools](https://www.powershellgallery.com/packages/MSFT.Network.Diag) installiert, da Get-sddcdiagnosticinfo auf diese Weise basiert. Dieses Manifest-Modul enthält das Tool für die Netzwerk Diagnose und-Problembehandlung, das von der Produktgruppe Microsoft Core Networking bei Microsoft verwaltet wird.

Sie können das-Modul installieren, indem Sie den folgenden Befehl in PowerShell mit Administratorrechten ausführen:

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
Install-Module -Name MSFT.Network.Diag
```

Führen Sie den folgenden Befehl in PowerShell aus, um das Modul zu aktualisieren:

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

Das [GitHub](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/) -Repository ist die aktuellste Version des Moduls, da wir hier ständig Iteration durchlaufen. Um das Modul aus GitHub zu installieren, laden Sie das neueste Modul aus dem [Archiv](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip) herunter, und extrahieren Sie das Verzeichnis privatecloud. diagnosticinfo in den richtigen PowerShell-Modul Pfad, auf den ```$env:PSModulePath```

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

Wenn Sie dieses Modul in einem Offline Cluster herunterladen müssen, laden Sie die ZIP-Datei herunter, verschieben Sie Sie auf den Zielserver Knoten, und installieren Sie das Modul.

## <a name="gathering-logs"></a>Protokolle werden gesammelt.

Nachdem Sie Ereignis Kanäle aktiviert und den Installationsvorgang abgeschlossen haben, können Sie das PowerShell-Cmdlet Get-sddcdiagnosticinfo im-Modul verwenden, um Folgendes zu erhalten:

- Berichte über die Speicher Integrität sowie Details zu fehlerhaften Komponenten
- Berichte zur Speicherkapazität nach Pool, Volume und dedupliziertes Volume
- Ereignisprotokolle von allen Cluster Knoten und einen Zusammenfassungs Fehlerbericht

Angenommen, Ihr Speicher Cluster hat den Namen *"CLUS01".*

So führen Sie einen Remote Speicher Cluster aus:

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

So führen Sie lokal auf einem Cluster Speicher Knoten aus:

``` PowerShell
Get-SDDCDiagnosticInfo
```

So speichern Sie Ergebnisse in einem angegebenen Ordner:

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

Im folgenden finden Sie ein Beispiel dafür, wie dies in einem echten Cluster aussieht:

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

Wie Sie sehen können, führt das Skript auch die Überprüfung des aktuellen Cluster Status durch.

![Screenshot der Data Collection PowerShell](media/data-collection/CollectData.png)

Wie Sie sehen können, werden alle Daten in den Ordner sddcdiagtemp geschrieben.

![Screenshot der Daten im Datei-Explorer](media/data-collection/CollectDataFolder.png)

Nachdem das Skript abgeschlossen wurde, wird die ZIP-Datei in Ihrem Benutzerverzeichnis erstellt.

![Screenshot: Data zip in PowerShell](media/data-collection/CollectDataResult.png)

Erstellen Sie einen Bericht in einer Textdatei.

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

Im folgenden finden Sie einen Link zum [Beispiel Bericht](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt) und zum [Beispiel ZIP](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP).

Um dies im Windows Admin Center (Version 1812 oder höher) anzuzeigen, navigieren Sie zur Registerkarte *Diagnose* . Wie Sie im folgenden Screenshot sehen, können Sie 

- Installieren von Diagnosetools
- Aktualisieren Sie Sie (wenn Sie veraltet sind). 
- Planen Sie tägliche Diagnose Ausführungen (Dies hat eine geringe Auswirkung auf Ihr System, nehmen Sie in der Regel < fünf Minuten im Hintergrund in Anspruch, und es werden nicht mehr als 500 MB in Ihrem Cluster benötigt)
- Zeigen Sie die zuvor gesammelten Diagnoseinformationen an, wenn Sie Sie benötigen, um Sie selbst zu unterstützen oder zu analysieren.

![Bildschirm Abbildung von WAC Diagnostics](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>Ausgabe von "Get-sddcdiagnosticinfo"

Im folgenden finden Sie die Dateien, die in der ZIP-Ausgabe von Get-sddcdiagnosticinfo enthalten sind.

### <a name="health-summary-report"></a>Integritäts Zusammenfassungs Bericht

Der Integritäts Zusammenfassungs Bericht wird gespeichert unter:
- 0_CloudHealthSummary. log

Diese Datei wird generiert, nachdem Sie alle gesammelten Daten verarbeitet und eine kurze Zusammenfassung Ihres Systems bereitgestellt haben. Die Datei enthält Folgendes:

- Systeminformationen
- Übersicht über die Speicher Integrität (Anzahl der Knoten, Ressourcen Online, freigegebene Clustervolumes Online, fehlerhafte Komponenten usw.)
- Details zu fehlerhaften Komponenten (offline-, Fehler-oder Online ausstehende Cluster Ressourcen)
- Firmware-und Treiber Informationen
- Details zu Pool, physischem Datenträger und Volume
- Speicherleistung (Leistungsindikatoren werden erfasst)

Dieser Bericht wird fortlaufend aktualisiert, um nützlichere Informationen zu enthalten. Die neuesten Informationen finden Sie in der [GitHub](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md)-Infodatei.

### <a name="logs-and-xml-files"></a>Protokolle und XML-Dateien

Das Skript führt verschiedene Protokoll Sammlungs Skripts aus und speichert die Ausgabe als XML-Dateien. Wir erfassen Cluster-und Integritäts Protokolle, Systeminformationen (Msinfo32), ungefilterte Ereignisprotokolle (Failoverclustering, DIS-Diagnose, Hyper-v, Speicherplätze usw.) und Speicher Diagnoseinformationen (Betriebs Protokolle). Die neuesten Informationen darüber, welche Informationen gesammelt werden, finden Sie in der [GitHub-Infodatei (was wir sammeln)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include).

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>Verwenden der XML-Dateien aus Get-pcstoragediagnosticinfo
Sie können die Daten aus den XML-Dateien nutzen, die in den vom Cmdlet " **Get-pcstoragediagnosticinfo** " gesammelten Daten bereitgestellt werden. Diese Dateien enthalten Informationen zu den virtuellen Festplatten, physischen Datenträgern, grundlegenden Cluster Informationen und anderen PowerShell-bezogenen Ausgaben. 

Öffnen Sie ein PowerShell-Fenster, und führen Sie die folgenden Schritte aus, um die Ergebnisse dieser Ausgaben anzuzeigen. 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>Was ist als nächstes zu erwarten?
Viele Verbesserungen und neue Cmdlets zur Analyse der SDDC-Systemintegrität.
Geben Sie uns Feedback dazu, was Sie sehen möchten, indem Sie [hier](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)Probleme einreichen. Außerdem können Sie durch das Senden einer [Pull Request](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls)hilfreiche Änderungen am Skript einbringen.
