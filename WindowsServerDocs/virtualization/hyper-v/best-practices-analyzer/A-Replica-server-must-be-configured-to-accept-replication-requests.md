---
title: Replikatserver muss konfiguriert werden, zum Akzeptieren von replikationsanforderungen
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c5e30ddc50b176b83db081a29c6427356ab946c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827521"
---
# <a name="a-replica-server-must-be-configured-to-accept-replication-requests"></a>Replikatserver muss konfiguriert werden, zum Akzeptieren von replikationsanforderungen

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>Problem  
*Dieser Computer als Hyper-V Replica Server festgelegt ist, aber nicht zum Akzeptieren von eingehenden Replikationsdaten vom primären Server konfiguriert ist.*  
  
## <a name="impact"></a>Auswirkungen  
*Dieser Server kann keine auf Replikationsdatenverkehr vom primären Server akzeptieren.*  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Hyper-V-Manager, um anzugeben, welche Primärserver diesen Replikatserver Replikationsdaten vom akzeptieren soll.*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>Erstellen Sie autorisierungseinträge, die mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. (In Server-Manager, klicken Sie auf **Tools** > **Hyper-V-Manager**.)  
  
2.  In der Liste der Hosts Maustaste diejenige werden soll, und klicken Sie dann **Hyper-V-Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf **Replikationskonfiguration**.  
  
4.  Klicken Sie unter **Autorisierung und Speicherung**, klicken Sie auf **zulassen der Replikation von den angegebenen Servern**.  
  
5.  Klicken Sie unterhalb der Liste der Server, auf **hinzufügen**.  
  
6.  Klicken Sie unter **hinzufügen Autorisierungseintrag**:  
  
    -   Geben Sie den vollqualifizierten Namen des ersten Servers ein.  
  
    -   Geben Sie einen dedizierten Speicherort zum Speichern von nur die Dateien des Servers.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Für jeden primären Server wiederholen.  
  
9. Klicken Sie auf **OK** zu beenden, und schließen Sie das Fenster.  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Erstellen Sie mithilfe von Windows PowerShell replikationsautorisierungseinträge  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf Start, und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl ähnlich dem folgenden, und Ersetzen Sie dabei:  
  
    -   Der primäre Server-Name des SERVER01.domain01.contoso.com geleitet verwendet mit dem vollqualifizierten Domänennamen des Servers.  
  
    -   Der Speicherort der D:\ReplicaVMStorage mit Ihrem Standort.  
  
    -   Die vertrauensgruppe mit dem Namen DEFAULT mit dem Namen der Gruppe, wenn Sie eine solche erstellt haben. Wenn dies nicht der Fall ist, verwenden Sie die STANDARDEINSTELLUNG.  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  


