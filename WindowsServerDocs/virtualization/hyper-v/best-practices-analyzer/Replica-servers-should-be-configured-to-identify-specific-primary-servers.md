---
title: Replikatserver müssen konfiguriert werden, zum Identifizieren von bestimmten primärer Servern autorisiert werden, um Replikationsdatenverkehr zu senden.
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 47b215d4c84e68d93ae1189ddd370358e2781eff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822241"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>Replikatserver müssen konfiguriert werden, zum Identifizieren von bestimmten primärer Servern autorisiert werden, um Replikationsdatenverkehr zu senden.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Konfiguration wird diesen Replikatserver Replikations-Datenverkehr von allen primären Servern akzeptiert und speichert sie in einem zentralen Ort.*  
  
### <a name="impact"></a>Auswirkungen  
*Alle Replikationen über alle primäre Server ist an einem Ort gespeichert, die Datenschutz oder Sicherheitsprobleme entstehen könnten.*  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Hyper-V-Manager, um neue replikationsautorisierungseinträge für den bestimmten primären Servern zu erstellen und die Angabe separater Speicherorte für jede von ihnen. Sie können Platzhalterzeichen verwenden, zum Gruppieren von primärer Servern in Gruppen für jeden autorisierungseintrag.*  
  
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
  
## <a name="see-also"></a>Siehe auch  
[New-VMReplicationAuthorizationEntry](https://technet.microsoft.com/library/hh848606.aspx)  
  


