---
title: Verwenden der Livemigration ohne Failoverclustering zum Verschieben eines virtuellen Computers
description: Erhalten die Voraussetzungen und Anweisungen zum Ausführen einer Livemigration in einer eigenständigen Umgebung.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75c32e42-97f7-48df-aac9-1d82d34825e1
author: KBDAzure
ms.author: kathydav
ms.date: 01/17/2017
ms.openlocfilehash: 9be61fbc860e9d8c5cbc020d6dd4082722e32509
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812098"
---
# <a name="use-live-migration-without-failover-clustering-to-move-a-virtual-machine"></a>Verwenden der Livemigration ohne Failoverclustering zum Verschieben eines virtuellen Computers

>Gilt für: Windows Server 2016

In diesem Artikel wird das Verschieben eines virtuellen Computers durch Ausführen einer Livemigration ohne Failover-Clusterunterstützung veranschaulicht. Eine Livemigration verschiebt die ausgeführten virtuellen Computer zwischen Hyper-V-Hosts ohne nennenswerte Ausfallzeit.   
  
Um zu diesem Zweck können, benötigen Sie:   

- Ein Benutzerkonto, das ein Mitglied der lokalen Administratorengruppe von Hyper-V oder die Gruppe "Administratoren" auf den Quell- und Ziel-Computern ist. 
  
- Hyper-V-Rolle in Windows Server 2016 oder Windows Server 2012 R2 auf den Quell- und Ziel-Anwendungsservern installiert, und richten Sie für livemigrationen. Sie erreichen eine Livemigration zwischen Hosts, auf denen Windows Server 2016 und Windows Server 2012 R2, ob die virtuelle Maschine mindestens Version 5.

    Version Anweisungen finden Sie unter [Upgrade VM-Konfigurationsversion in Hyper-V unter Windows 10 oder Windows Server 2016](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Installationsanweisungen finden Sie unter [Einrichten von Hosts für die Livemigration](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md).

- Die Hyper-V-Verwaltungstools auf einem Computer unter Windows Server 2016 oder Windows 10 installiert werden, es sei denn, die Tools, auf dem Quell- oder Ziel-Server, und Sie installiert sind werden sie von dort aus auszuführen.  
   
## <a name="use-hyper-v-manager-to-move-a-running-virtual-machine"></a>Verwenden Sie Hyper-V-Manager, um einen ausgeführten virtuellen Computer verschieben  
  
1.  Öffnen Sie den Hyper-V-Manager. (In Server-Manager, klicken Sie auf **Tools** >>**Hyper-V-Manager**.)  
  
2.  Wählen Sie im Navigationsbereich einen der Server aus. (Wenn er nicht angegeben ist, mit der rechten Maustaste **Hyper-V-Manager**, klicken Sie auf **Herstellen einer Verbindung mit Server**, geben Sie den Servernamen ein, und klicken Sie auf **OK**. Wiederholen Sie zum Hinzufügen weiterer Server.)  
  
3.  Von der **VMs** Bereich mit der rechten Maustaste den virtuellen Computer, und klicken Sie dann auf **verschieben**. Dies öffnet den Assistenten zum Verschieben. 
  
4.  Verwenden Sie die Seiten des Assistenten, um den Typ des verschieben, Zielserver und Optionen auswählen.
  
5.  Überprüfen Sie auf der Seite **Zusammenfassung** die von Ihnen ausgewählten Einstellungen, und klicken Sie dann auf **Fertig stellen**.  

## <a name="use-windows-powershell-to-move-a-running-virtual-machine"></a>Verwenden Sie Windows PowerShell, um einen ausgeführten virtuellen Computer verschieben
  
Im folgenden Beispiel wird das Cmdlet "Move-VM" zum Verschieben eines virtuellen Computers mit dem Namen *LMTest* zu einem Zielserver mit dem Namen *TestServer02* und verschiebt die virtuellen Festplatten und die andere Datei, die solche Prüfpunkte und Smart-Auslagerungsdateien, zu der *D:\LMTest* Verzeichnis auf dem Zielserver.  
  
```  
PS C:\> Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest  
```  
  
## <a name="troubleshooting"></a>Problembehandlung

### <a name="failed-to-establish-a-connection"></a>Fehler beim Herstellen einer Verbindung 

Wenn Sie die eingeschränkte Delegierung eingerichtet haben, müssen Sie auf Quellserver anmelden, bevor Sie einen virtuellen Computer verschieben können. Wenn Sie dies nicht tun, wird der Authentifizierungsversuch fehlschlägt, ein Fehler auftritt, und diese Meldung wird angezeigt:  
  
"VM-Migration Fehler bei Vorgang an der Migrationsquelle.  
Fehler beim Herstellen einer Verbindung mit Host *Computername*: Sind keine Anmeldeinformationen im Sicherheitspaket 0x8009030E verfügbar."
  
 Um dieses Problem zu beheben, melden Sie sich auf dem Quellserver, und versuchen Sie es die Verschiebung erneut aus. Richten Sie nicht auf einem Quellserver melden Sie sich vor dem Ausführen einer Livemigration, die eingeschränkte Delegierung. Sie benötigen Domänenadministrator-Anmeldeinformationen, um die eingeschränkte Delegierung einzurichten. Anweisungen hierzu finden Sie unter [Einrichten von Hosts für die Livemigration](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md). 
 
 ### <a name="failed-because-the-host-hardware-isnt-compatible"></a>Fehler bei, da die Hosthardware nicht kompatibel ist
 
 Wenn ein virtueller Computer verfügt nicht über die Prozessorkompatibilität aktiviert und verfügt über eine oder mehrere Momentaufnahmen, schlägt die Verschiebung die Hosts mit verschiedenen Prozessorversionen haben. Ein Fehler auftritt, und diese Meldung wird angezeigt:
 
**Die virtuelle Maschine kann nicht auf dem Zielcomputer nicht verschoben werden. Die Hardware auf dem Zielcomputer ist nicht kompatibel mit der hardwareanforderungen für diesen virtuellen Computer.**
 
 Um dieses Problem zu beheben, fahren Sie den virtuellen Computer herunter, und aktivieren Sie die kompatibilitätseinstellung für den Prozessor.
 
1. Hyper-V-Manager in der **VMs** Bereich mit der rechten Maustaste den virtuellen Computer, und klicken Sie auf Einstellungen.
2. Erweitern Sie im Navigationsbereich **Prozessoren** , und klicken Sie auf **Kompatibilität**.
3. Überprüfen Sie **zu einem Computer mit einer anderen Prozessorversion migrieren**.
4. Klicken Sie auf **OK**.
 
   Verwenden Sie zur Verwendung von Windows PowerShell die [Set-VMProcessor](https://technet.microsoft.com/library/hh848533.aspx) Cmdlet:
 
   ```
   PS C:\> Set-VMProcessor TestVM -CompatibilityForMigrationEnabled $true
   ```