---
title: PowerShell in Erweiterungen verwenden
description: Verwenden von PowerShell in ihrer Erweiterung Windows Admin Center SDK (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6e99fc43d4acb7a70dfd3a8ba19dae6492c41b2b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357050"
---
# <a name="using-powershell-in-your-extension"></a>PowerShell in Erweiterungen verwenden #

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Im Windows Admin Center Extensions SDK werden wir ausführlicher auf das Hinzufügen von PowerShell-Befehlen zu ihrer Erweiterung eingehen.

## <a name="powershell-in-typescript"></a>PowerShell in typescript ##

Der Gulp-Buildprozess weist einen Schritt "generieren" ```{!ScriptName}.ps1``` ```\src\resources\scripts``` auf, bei dem alle im Ordner abgelegt und in der ```powershell-scripts``` -Klasse unter ```\src\generated``` dem Ordner erstellt werden.

>[!NOTE] 
> Aktualisieren Sie weder das ```powershell-scripts.ts``` manuell noch ```strings.ts``` die Dateien. Alle Änderungen, die Sie vornehmen, werden bei der nächsten Generierung überschrieben.

## <a name="running-a-powershell-script"></a>Ausführen eines PowerShell-Skripts ##
Alle Skripts, die Sie auf einem Knoten ausführen möchten, können in ```\src\resources\scripts\{!ScriptName}.ps1```platziert werden. 
>[!IMPORTANT] 
> Alle Änderungen, die in ```{!ScriptName}.ps1``` einer Datei vorgenommen werden, werden in Ihrem Projekt ```gulp generate``` erst wiedergegeben, wenn Sie ausgeführt wurde.

Die API erstellt zunächst eine PowerShell-Sitzung auf den Zielknoten, erstellt das PowerShell-Skript mit allen Parametern, die übergeben werden müssen, und führt dann das Skript für die Sitzungen aus, die erstellt wurden.

Wir haben z. b. Folgendes ```\src\resources\scripts\Get-NodeName.ps1```Skript:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

Wir erstellen eine PowerShell-Sitzung für den Zielknoten:
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
Anschließend erstellen wir das PowerShell-Skript mit einem Eingabeparameter:
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
Schließlich müssen wir das Skript in der von uns erstellten Sitzung ausführen:
``` ts
  public ngOnInit(): void {
    this.session = this.appContextService.powerShell.createAutomaticSession('{!TargetNode}');
  }

  public getNodeName(): Observable<any> {
    const script = PowerShell.createScript(PowerShellScripts.Get_NodeName.script, { stringFormat: 'The name of the node is {0}!'});
    return this.appContextService.powerShell.run(this.session, script)
    .pipe(
        map(
        response => {
            if (response && response.results) {
                return response.results;
            }
            return 'no response';
        }
      ) 
    );
  }

  public ngOnDestroy(): void {
    this.session.dispose()
  }

```
Nun müssen wir die soeben erstellte Observable-Funktion abonnieren. Platzieren Sie diese Funktion, um die Funktion zum Ausführen des PowerShell-Skripts aufzurufen:
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
Durch Bereitstellen des Knoten namens für die Methode "kreatesession" wird eine neue PowerShell-Sitzung erstellt, verwendet und nach Abschluss des PowerShell-Aufrufes sofort zerstört. 

### <a name="key-options"></a>Schlüsseloptionen ###
Beim Aufrufen der PowerShell-API stehen einige Optionen zur Verfügung. Jedes Mal, wenn eine Sitzung erstellt wird, kann Sie mit oder ohne Schlüssel erstellt werden. 

**Schlüssel:** Dadurch wird eine Schlüssel gebundene Sitzung erstellt, die auch über Komponenten hinweg gesucht und wieder verwendet werden kann (was bedeutet, dass Component1 eine Sitzung mit dem Schlüssel "SME-Rocks" erstellen kann, und Component2 kann dieselbe Sitzung verwenden). Wenn ein Schlüssel angegeben wird, muss die erstellte Sitzung verworfen werden, indem "verwerfen ()" aufgerufen wird, wie im obigen Beispiel gezeigt. Eine Sitzung sollte nicht beibehalten werden, ohne dass Sie länger als 5 Minuten verworfen wird. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**Schlüssel** Es wird automatisch ein Schlüssel für die Sitzung erstellt. Diese Sitzung wird nach 3 Minuten automatisch verworfen. Wenn Sie Schlüssel verwenden, kann die Erweiterung die Verwendung eines beliebigen Runspace wieder verwenden, der zum Zeitpunkt der Erstellung einer Sitzung bereits verfügbar ist. Wenn kein Runspace verfügbar ist, wird ein neuer erstellt. Diese Funktion eignet sich für einmalige Aufrufe, aber die wiederholte Verwendung kann sich auf die Leistung auswirken. Die Erstellung einer Sitzung dauert ungefähr 1 Sekunde, sodass das fortlaufende wieder verwenden von Sitzungen zu Verlangsamungen führen kann.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
oder 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
Erstellen Sie in den meisten Situationen eine Schlüssel gebundene Sitzung in ```ngOnInit()``` der-Methode, und löschen Sie Sie ```ngOnDestroy()```dann in. Gehen Sie folgendermaßen vor, wenn mehrere PowerShell-Skripts in einer-Komponente vorhanden sind, die zugrunde liegende Sitzung aber nicht Komponenten übergreifend gemeinsam verwendet wird.
Um optimale Ergebnisse zu erzielen, stellen Sie sicher, dass die Sitzungs Erstellung innerhalb von Komponenten statt in Diensten verwaltet wird. Dadurch wird sichergestellt, dass die Lebensdauer und Bereinigung ordnungsgemäß verwaltet werden kann

Um optimale Ergebnisse zu erzielen, stellen Sie sicher, dass die Sitzungs Erstellung innerhalb von Komponenten statt in Diensten verwaltet wird. Dadurch wird sichergestellt, dass die Lebensdauer und Bereinigung ordnungsgemäß verwaltet werden kann

### <a name="powershell-stream"></a>PowerShell-Stream ###
Wenn Sie ein Skript mit langer Ausführungszeit haben und die Daten progressiv ausgegeben werden, können Sie mit einem PowerShell-Stream die Daten verarbeiten, ohne auf das Skript warten zu müssen. Das Observable Next () wird aufgerufen, sobald Daten empfangen werden.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>Skripts mit langer Laufzeit ###
Wenn Sie über ein Skript mit langer Ausführungszeit verfügen, das Sie im Hintergrund ausführen möchten, können Sie ein Arbeits Element übermitteln. Der Status des Skripts wird vom Gateway nachverfolgt, und Aktualisierungen des Status können an eine Benachrichtigung gesendet werden. 
```ts
const workItem: WorkItemSubmitRequest = {
    typeId: 'Long Running Script',
    objectName: 'My long running service',
    powerShellScript: script,
    
    //in progress notifications
    inProgressTitle: 'Executing long running request',
    startedMessage: 'The long running request has been started',
    progressMessage: 'Working on long running script – {{ percent }} %',

    //success notification
    successTitle: 'Successfully executed a long running script!',
    successMessage: '{{objectName}} was successful',
    successLinkText: 'Bing',
    successLink: 'http://www.bing.com',
    successLinkType: NotificationLinkType.Absolute,

    //error notification
    errorTitle: 'Failed to execute long running script',
    errorMessage: 'Error: {{ message }}'

    nodeRequestOptions: {
       logAudit: true,
       logTelemetry: true
    }
};

return this.appContextService.workItem.submit('{!TargetNode}', workItem);
```

>[!NOTE] 
> Damit der Fortschritt angezeigt wird, muss Write-Progress in dem Skript enthalten sein, das Sie geschrieben haben. Zum Beispiel:
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!' -percentComplete 95
>```

#### <a name="workitem-options"></a>Workitem-Optionen ####

| Funktion | Erläuterung |
| ----- | ----------- |
| Submit () | Übermittelt das Arbeits Element 
| submitandwait () | Senden Sie das Arbeits Element, und warten Sie, bis die Ausführung abgeschlossen ist.
| Wait () | Warten, bis ein vorhandenes Arbeits Element fertiggestellt ist
| Abfrage () | Abfragen für ein vorhandenes Arbeits Element nach ID
| Suchen () | Suchen und vorhandenes Arbeits Element nach "targetnodename", "ModuleName" oder "typeid".

### <a name="powershell-batch-apis"></a>PowerShell-Batch-APIs ###
Wenn Sie das gleiche Skript auf mehreren Knoten ausführen müssen, kann eine Batch-PowerShell-Sitzung verwendet werden. Zum Beispiel:
```ts
const batchSession = this.appContextService.powerShell.createBatchSession(
    ['{!TargetNode1}', '{!TargetNode2}', sessionKey);
  this.appContextService.powerShell.runBatchSingleCommand(batchSession, command).subscribe((responses: PowerShellBatchResponseItem[]) => {
    for (const response of responses) { 
      if (response.error || response.errors) {
        //handle error
      } else {
        const results = response.properties && response.properties.results;
        //response.nodeName
        //results[0]
      }
    }
     },
     Error => { /* handle error */ });  

```


#### <a name="powershellbatch-options"></a>Powershellbatch-Optionen ####
| Andere | Erläuterung |
| ----- | ----------- |
| runsinglecommand | Ausführen eines einzelnen Befehls für alle Knoten im Array 
| ausführen | Entsprechenden Befehl auf gekoppelten Knoten ausführen
| cancel | Befehl für alle Knoten im Array Abbrechen
