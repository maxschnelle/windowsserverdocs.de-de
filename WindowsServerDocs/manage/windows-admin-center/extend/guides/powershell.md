---
title: PowerShell in Erweiterungen verwenden
description: Mithilfe von PowerShell in Ihrer Erweiterung-SDK für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7375732fd464519cd1533043d271065e488fd46a
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621355"
---
# <a name="using-powershell-in-your-extension"></a>PowerShell in Erweiterungen verwenden #

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In das Windows Admin Center-Extensions-SDK wechseln wir tiefer greifende - sprechen wir über die PowerShell-Befehle zu Ihrer Erweiterung hinzufügen.

## <a name="powershell-in-typescript"></a>PowerShell in TypeScript ##

Der Gulp-Build-Prozess ist einen Schritt generieren, mit denen alle gelangen ```{!ScriptName}.ps1``` , befindet sich der ```\src\resources\scripts``` Ordner, und erstellen sie in der ```powershell-scripts``` -Klasse der ```\src\generated``` Ordner.

>[!NOTE] 
> Nicht manuell aktualisiert die ```powershell-scripts.ts``` noch die ```strings.ts``` Dateien. Jede Änderung, die Sie vornehmen, werden auf der nächsten Generierung überschrieben.

## <a name="running-a-powershell-script"></a>Ausführen eines PowerShell-Skripts ##
Alle Skripts, die auf einem Knoten ausgeführt werden soll, die in eingefügt werden können ```\src\resources\scripts\{!ScriptName}.ps1```. 
>[!IMPORTANT] 
> Keine Änderungen vornehmen, einem ```{!ScriptName}.ps1``` Datei werden nicht übernommen werden, in Ihrem Projekt bis ```gulp generate``` ausgeführt wurde.

Die API funktioniert, indem Sie zunächst eine PowerShell-Sitzung auf den Knoten, die Sie als Ziel, erstellen das PowerShell-Skript mit den Parametern, die übergeben werden müssen, die und klicken Sie dann das Skript ausführen, auf die Sitzungen, die erstellt wurden.

Angenommen, wir haben dieses Skript ```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

Wir erstellen eine PowerShell-Sitzung für unsere Zielknoten:
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
Anschließend erstellen wir das PowerShell-Skript mit einem Eingabeparameter:
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
Abschließend müssen wir das Skript in der Sitzung ausgeführt wird, die wir erstellt haben:
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
Jetzt müssen wir die Observable-Funktion zu abonnieren, die wir gerade erstellt haben. Platzieren Sie diese, müssen Sie die Funktion zum Ausführen des PowerShell-Skripts aufrufen:
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
Durch die Bereitstellung des Knotennamens ein, die CreateSession-Methode, eine neue PowerShell-Sitzung erstellt, verwendet, und klicken Sie dann sofort nach Abschluss des PowerShell-Aufrufs zerstört. 

### <a name="key-options"></a>Schlüsseloptionen ###
Einige Optionen sind verfügbar, beim Aufrufen der PowerShell-API. Jedes Mal, wenn einer Sitzung Erstellung können sie mit oder ohne einen Schlüssel erstellt werden. 

**Schlüssel:** Dadurch wird eine verschlüsselte Sitzung, die kann nachgeschlagen und wiederverwendet werden, auch über Komponenten (d. h. Component1 eine Sitzung mit Schlüssel "KMU-ROCKS" erstellen kann und Component2 dieselbe Sitzung können) erstellt. Wenn ein Schlüssel angegeben wird, muss die Sitzung, die erstellt wird von aufrufenden Dispose() verworfen werden, wie im obigen Beispiel durchgeführt wurde. Eine Sitzung dürfen nicht gespeichert werden, ohne für mehr als 5 Minuten verworfen wird. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**Keyless:** Ein Schlüssel wird automatisch für die Sitzung erstellt werden. Diese Sitzung mit werden automatisch nach 3 Minuten verworfen. Können ohne Schlüssel mit die Erweiterung, um die Verwendung von jedem Runspace wiederverwenden, die zum Zeitpunkt der Erstellung einer Sitzung bereits verfügbar ist. Wenn keine Runspace verfügbar ist, als eine neue Ressourcengruppe erstellt wird. Diese Funktion eignet sich für die einmalige aufrufen, aber die wiederholte Verwendung kann die Leistung beeinträchtigen. Eine Sitzung dauert ungefähr 1 Sekunde erstellen, daher kontinuierlich Wiederverwendung Sitzungen kann Verzögerungen verursachen.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
oder 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
In den meisten Fällen erstellen Sie eine verschlüsselte Sitzung in der ```ngOnInit()``` -Methode, und klicken Sie dann verwerfen Sie sie in ```ngOnDestroy()```. Folgen Sie diesem Muster, wenn mehrere PowerShell-Skripts in eine Komponente, aber der zugrundeliegenden Sitzung, die Komponenten ist nicht gemeinsam vorhanden sind.
Für optimale Ergebnisse Sie sitzungserstellung innerhalb von Komponenten anstelle von Services verwaltet wird – damit wird sichergestellt, Lebensdauer und die Bereinigung ordnungsgemäß verwaltet werden kann.

Für optimale Ergebnisse Sie sitzungserstellung innerhalb von Komponenten anstelle von Services verwaltet wird – damit wird sichergestellt, Lebensdauer und die Bereinigung ordnungsgemäß verwaltet werden kann.

### <a name="powershell-stream"></a>PowerShell-Stream ###
Wenn Sie eine lang ausgeführte Skripts und Daten haben ein PowerShell-Streams können Sie die Daten zu verarbeiten, ohne zu warten, bis das Skript abgeschlossen progressiv, ausgegeben. Der Observable Next()"wird aufgerufen, sobald Daten empfangen werden.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>Lang ausgeführte Skripts ###
Wenn Sie eine lang ausgeführte Skript, die im Hintergrund ausgeführt werden sollen verfügen, kann eine Arbeitsaufgabe übermittelt werden. Der Status des Skripts werden vom Gateway verfolgt werden, und Updates für den Status an eine Benachrichtigung gesendet werden können. 
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
> Write-Progress muss für den Status angezeigt werden im Skript enthalten sein, die Sie geschrieben haben. Zum Beispiel:
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### <a name="workitem-options"></a>WorkItem-Optionen ####

| Funktion | Erläuterung |
| ----- | ----------- |
| submit() | Übermittelt das Arbeitselement 
| submitAndWait() | Übermitteln Sie das Arbeitselement, und Warten auf den Abschluss der Ausführung
| wait() | Warten Sie, vorhandene Arbeit Element abgeschlossen
| query() | Abfrage für ein vorhandenes Arbeitselement nach id
| find() | Suchen, und vorhandene Arbeitsaufgabe durch die TargetNodeName, ModuleName oder TypeId.

### <a name="powershell-batch-apis"></a>PowerShell-Batch-APIs ###
Wenn Sie das gleiche Skript auf mehreren Knoten ausführen möchten, kann eine Batch-PowerShell-Sitzung verwendet werden. Zum Beispiel:
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


#### <a name="powershellbatch-options"></a>PowerShellBatch-Optionen ####
| option | Erläuterung |
| ----- | ----------- |
| runSingleCommand | Führen Sie einen einzelnen Befehl für alle Knoten im array 
| ausführen | Führen Sie die entsprechenden-Befehl auf gekoppelten Knoten
| Abbrechen | Der Befehl auf allen Knoten im Array Abbrechen
