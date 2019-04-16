---
title: PowerShell in Erweiterungen verwenden
description: Mithilfe von PowerShell in der Erweiterung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b1be4fe7639d913243cc28371dff9e98e0f5827e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296722"
---
# PowerShell in Erweiterungen verwenden #

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

In Windows Admin Center-Erweiterungen SDK ausführlicheren gehen wir – sprechen wir über PowerShell-Befehle zur Erweiterung hinzufügen.

## PowerShell in typescript integriert ##

Der Buildprozess schlucken dienen hat einen Schritt generieren, die alle dauert ```{!ScriptName}.ps1``` , die in platziert wird die ```\src\resources\scripts``` Ordner und erstellen sie in der ```powershell-scripts``` -Klasse unter der ```\src\generated``` Ordner.

>[!NOTE] 
> Nicht manuell aktualisieren der ```powershell-scripts.ts``` noch die ```strings.ts``` Dateien. Die vorgenommenen Änderungen werden auf der nächsten generieren überschrieben.

## Ausführen eines Skripts Powerhell ##
Alle Skripts, die auf einem Knoten ausgeführt werden soll, können in platziert werden ```\src\resources\scripts\{!ScriptName}.ps1```. 
>[!IMPORTANT] 
> Keine Änderungen vornehmen, einer ```{!ScriptName}.ps1``` Datei werden nicht in Ihrem Projekt wiedergegeben werden, es sei denn, ein generieren 

Die API funktioniert, indem Sie zunächst eine PowerShell-Sitzung auf den Knoten, die Sie als Ziel, erstellen das PowerShell-Skript mit Parameter, die in übergeben werden müssen, die und dann Ausführen des Skripts auf den Sitzungen, die erstellt wurden.

Beispielsweise haben wir dieses Skript ```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

Wir erstellen Sie eine PowerShell-Sitzung für unsere Zielknoten:
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
Anschließend erstellen wir das PowerShell-Skript mit einem Eingabeparameter:
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
Abschließend müssen wir dieses Skript in der Sitzung ausführen, die wir erstellt haben:
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
Jetzt müssen wir die Observable-Funktion abonnieren, wir gerade erstellt haben. Platzieren Sie diese, wenn Sie die Funktion zum Ausführen des PowerShell-Skripts aufrufen, müssen:
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
Durch die Bereitstellung des Knotennamens an die Methode CreateSession, ist eine neue PowerShell-Sitzung erstellt, verwendet und dann sofort nach Abschluss des Aufrufs PowerShell gelöscht. 

### Tastenoptionen ###
Einige Optionen sind verfügbar, wenn die PowerShell-API aufrufen. Jedes Mal, wenn eine Sitzung erstellt wird können sie mit oder ohne einen Schlüssel erstellt werden. 

**Schlüssel:** Dadurch entsteht eine mit Schlüssel-Sitzung, die nachgeschlagen und wiederverwendet werden, auch über Komponenten (d. h. Component1 Sie eine Sitzung mit dem Schlüssel "SME-FELSEN erstellen können", und Component2 können dieselbe Sitzung) werden kann. Wenn ein Schlüssel bereitgestellt wird, muss Sitzung, die erstellt wird von der aufrufenden dispose() freigegeben werden wie im obigen Beispiel durchgeführt wurde. Eine Sitzung sollte nicht aufbewahrt werden, ohne für mehr als 5 Minuten verworfen. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**:** Ein Schlüssel wird automatisch für die Sitzung erstellt werden. Dieser Sitzung mit werden automatisch nach drei Minuten freigegeben. , Können Ihre Erweiterung für die Verwendung von alle Runspace wiederverwenden, die zum Zeitpunkt der Erstellung einer Sitzung bereits verfügbar ist. Wenn keine Runspace verfügbar ist, als eine neue erstellt wird. Diese Funktion ist eignet sich gut für einmaligen Aufrufe wiederholte verwenden kann die Leistung beeinträchtigen. Eine Sitzung dauert ungefähr 1 Sekunde erstellen, also kontinuierlich Wiederverwendung Sitzungen Verlangsamung verursachen kann.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
oder 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
Erstellen Sie in den meisten Fällen eine weiteren Sitzung in die ```ngOnInit()``` -Methode auf, und dann Dispose dafür ```ngOnDestroy()```. Führen Sie dieses Muster, wenn es gibt mehrere PowerShell-Skripts in einer Komponente, aber der zugrunde liegenden Sitzungsschlüssel IS NOT mehreren Komponenten verwendet.
Für optimale Ergebnisse zu erzielen stellen Sie sicher Sitzung Erstellung erfolgt in Komponenten anstelle von Services – Dadurch werden sicherzustellen, dass diese Lebensdauer, und Bereinigung ordnungsgemäß verwaltet werden kann.

Für optimale Ergebnisse zu erzielen stellen Sie sicher Sitzung Erstellung erfolgt in Komponenten anstelle von Services – Dadurch werden sicherzustellen, dass diese Lebensdauer, und Bereinigung ordnungsgemäß verwaltet werden kann.

### PowerShell-Stream ###
Falls Sie eine mit langer Ausführungsdauer Skript und Daten haben werden schrittweise ausgegeben ein PowerShell-Stream ohne zu warten, bis das Skript zum Abschließen der Verarbeitung der Daten ermöglicht. Observable next() wird aufgerufen werden, sobald Daten empfangen werden.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### Lange Ausführung von Skripts ###
Wenn Sie ein Skript mit langer Ausführungsdauer, die im Hintergrund ausgeführt werden soll verfügen, kann eine Arbeitsaufgabe übermittelt werden. Der Zustand des Skripts wird vom Gateway nachverfolgt werden, und Updates auf den Status an eine Benachrichtigung gesendet werden können. 
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
> Für die Bearbeitung angezeigt werden muss Write-Progress im Skript enthalten sein, die Sie geschrieben haben. Beispiel:
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### Arbeitsaufgabe-Optionen ####

| function | Erläuterung |
| ----- | ----------- |
| ein | Die Arbeitsaufgabe sendet 
| submitAndWait() | Senden der Arbeitsaufgabe und Warten auf den Abschluss der Ausführung
| Wait() | Warten Sie vorhandene Arbeit Element abgeschlossen
| ein | Abfrage für eine vorhandene Arbeitsaufgabe nach id
| Find() | Suchen und vorhandene Arbeitsaufgabe durch das TargetNodeName, Modulname oder TypeId.

### PowerShell-Stapel APIs ###
Wenn Sie das gleiche Skript auf mehreren Knoten ausführen müssen, kann eine Batch-PowerShell-Sitzung verwendet werden. Beispiel:
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


#### PowerShellBatch-Optionen ####
| Option | Erläuterung |
| ----- | ----------- |
| runSingleCommand | Führen Sie einen einzelnen Befehl für alle Knoten im array 
| Führen Sie | Führen Sie die entsprechenden Befehl auf gekoppelten Knoten
| Abbrechen | Abbrechen des Befehls auf allen Knoten im array