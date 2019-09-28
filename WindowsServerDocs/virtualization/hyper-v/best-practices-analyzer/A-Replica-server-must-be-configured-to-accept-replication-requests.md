---
title: Ein Replikat Server muss für die Annahme von Replikations Anforderungen konfiguriert
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 54868d4db2dccc893bd2897134d9125446873384
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366720"
---
# <a name="a-replica-server-must-be-configured-to-accept-replication-requests"></a>Ein Replikat Server muss für die Annahme von Replikations Anforderungen konfiguriert

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>Problem  
*Dieser Computer ist als Hyper-V-Replikat Server festgelegt, jedoch nicht so konfiguriert, dass eingehende Replikations Daten von primären Servern akzeptiert werden.*  
  
## <a name="impact"></a>Auswirkungen  
*Dieser Server kann Replikations Datenverkehr von primären Servern nicht akzeptieren.*  
  
## <a name="resolution"></a>Auflösung  
*Legen Sie mit dem Hyper-V-Manager fest, von welchen primären Servern dieser Replikat Server Replikations Daten akzeptieren soll.*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>Erstellen von Autorisierungs Einträgen mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie**in Server-Manager auf Extras  > **Hyper-V-Manager**.)  
  
2.  Klicken Sie in der Liste der Hosts mit der rechten Maustaste auf das gewünschte, und klicken Sie dann auf **Hyper-V-Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf **Replikationskonfiguration**.  
  
4.  Klicken Sie unter **Autorisierung und Speicher**auf **Replikation von den angegebenen Servern zulassen**.  
  
5.  Klicken Sie unter der Liste der Server auf **Hinzufügen**.  
  
6.  Unter **Autorisierungs Eintrag hinzufügen**:  
  
    -   Geben Sie den voll qualifizierten Namen des ersten Servers ein.  
  
    -   Geben Sie einen dedizierten Speicherort an, um nur die Dateien dieses Servers zu speichern.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Wiederholen Sie diesen Vorgang für jeden primären Server.  
  
9. Klicken Sie erneut auf **OK** , um das Fenster zu schließen und zu schließen.  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Erstellen von Autorisierungs Einträgen mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf Start, und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl ähnlich dem folgenden aus, und ersetzen Sie dabei:  
  
    -   Der primäre Servername von Server01.domain01.contoso.com mit dem voll qualifizierten Domänen Namen des Servers.  
  
    -   Der Speicherort von d:\replicavmstorage mit ihrem Speicherort.  
  
    -   Die Vertrauens Gruppe mit dem Namen "Default" (Standard) mit dem Namen der Gruppe, wenn Sie eine erstellt haben. Wenn nicht, verwenden Sie die Standardeinstellung.  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  


