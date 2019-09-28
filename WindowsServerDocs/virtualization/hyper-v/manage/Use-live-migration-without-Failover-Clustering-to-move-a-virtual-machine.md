---
title: Verwenden der Live Migration ohne Failoverclustering zum Verschieben einer virtuellen Maschine
description: Bietet Voraussetzungen und Anweisungen zum Durchführen einer Live Migration in einer eigenständigen Umgebung.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75c32e42-97f7-48df-aac9-1d82d34825e1
author: KBDAzure
ms.author: kathydav
ms.date: 01/17/2017
ms.openlocfilehash: 55c96ff4696871e4013c3abd6247209d0d4517c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392554"
---
# <a name="use-live-migration-without-failover-clustering-to-move-a-virtual-machine"></a>Verwenden der Live Migration ohne Failoverclustering zum Verschieben einer virtuellen Maschine

>Gilt für: Windows Server 2016

In diesem Artikel erfahren Sie, wie Sie einen virtuellen Computer mithilfe einer Live Migration ohne Failoverclustering verschieben. Bei einer Live Migration werden virtuelle Maschinen ohne erkennbare Ausfallzeiten zwischen Hyper-V-Hosts verschoben.   
  
Um dies zu erreichen, benötigen Sie Folgendes:   

- Ein Benutzerkonto, das Mitglied der lokalen Gruppe "Hyper-V-Administratoren" oder der Gruppe "Administratoren" auf dem Quell-und dem Zielcomputer ist. 
  
- Die Hyper-V-Rolle in Windows Server 2016 oder Windows Server 2012 R2, die auf dem Quell-und Zielserver installiert ist und für Live Migrationen eingerichtet ist. Sie können eine Live Migration zwischen Hosts ausführen, auf denen Windows Server 2016 und Windows Server 2012 R2 ausgeführt wird, wenn der virtuelle Computer mindestens Version 5 ist.

    Anweisungen zur Versions Aktualisierung finden Sie unter [Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server 2016](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Installationsanweisungen finden Sie unter [Einrichten von Hosts für die Live Migration](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md).

- Die Hyper-V-Verwaltungs Tools sind auf einem Computer installiert, auf dem Windows Server 2016 oder Windows 10 ausgeführt wird, es sei denn, die Tools sind auf dem Quell-oder Ziel Server installiert, und Sie führen Sie von dort aus.  
   
## <a name="use-hyper-v-manager-to-move-a-running-virtual-machine"></a>Verwenden des Hyper-V-Managers zum Verschieben eines laufenden virtuellen Computers  
  
1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie**in Server-Manager auf Extras  >>**Hyper-V-Manager**.)  
  
2.  Wählen Sie im Navigationsbereich einen der Server aus. (Falls nicht aufgeführt, klicken Sie mit der rechten Maustaste auf **Hyper-V-Manager**, klicken Sie auf **Verbindung mit Server herstellen**, geben Sie den Servernamen ein, und klicken Sie auf **OK** Wiederholen Sie den Vorgang, um weitere Server hinzuzufügen.  
  
3.  Klicken Sie im **Virtual Machines** Bereich mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie dann auf **verschieben**. Der Verschiebungs-Assistent wird geöffnet. 
  
4.  Verwenden Sie die Seiten des Assistenten, um den Typ der Verschiebung, den Zielserver und die Optionen auszuwählen.
  
5.  Überprüfen Sie auf der Seite **Zusammenfassung** die von Ihnen ausgewählten Einstellungen, und klicken Sie dann auf **Fertig stellen**.  

## <a name="use-windows-powershell-to-move-a-running-virtual-machine"></a>Verwenden von Windows PowerShell zum Verschieben eines laufenden virtuellen Computers
  
Im folgenden Beispiel wird das Cmdlet Move-VM verwendet, um einen virtuellen Computer mit dem Namen *lmtest* auf einen Zielserver mit dem Namen *Bezeichnung testserver02* zu verschieben und die virtuellen Festplatten und anderen Dateien, z. b. Prüfpunkte und Smart Paging-Dateien, in *d:\lmtest* zu verschieben. Verzeichnis auf dem Zielserver.  
  
```  
PS C:\> Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest  
```  
  
## <a name="troubleshooting"></a>Problembehandlung

### <a name="failed-to-establish-a-connection"></a>Fehler beim Herstellen einer Verbindung. 

Wenn Sie die eingeschränkte Delegierung noch nicht eingerichtet haben, müssen Sie sich beim Quell Server anmelden, bevor Sie einen virtuellen Computer verschieben können. Wenn Sie dies nicht tun, schlägt der Authentifizierungs Versuch fehl, es tritt ein Fehler auf, und die Meldung wird angezeigt:  
  
"Fehler beim Migrations Vorgang für den virtuellen Computer bei der Migrations Quelle.  
Fehler beim Herstellen einer Verbindung mit dem Host *Computernamen*: Im Sicherheitspaket 0x8009030E sind keine Anmelde Informationen verfügbar. "
  
 Um dieses Problem zu beheben, melden Sie sich beim Quell Server an, und wiederholen Sie den Vorgang. Um zu vermeiden, dass Sie sich vor einer Live Migration bei einem Quell Server anmelden müssen, richten Sie die eingeschränkte Delegierung ein. Zum Einrichten der eingeschränkten Delegierung benötigen Sie Domänen Administrator-Anmelde Informationen. Anweisungen hierzu finden [Sie unter Einrichten von Hosts für die Live Migration](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md). 
 
 ### <a name="failed-because-the-host-hardware-isnt-compatible"></a>Fehler, weil die Host Hardware nicht kompatibel ist.
 
 Wenn für einen virtuellen Computer die Prozessor Kompatibilität nicht aktiviert ist und eine oder mehrere Momentaufnahmen vorhanden sind, schlägt der Verschiebe Vorgang fehl, wenn die Hosts über unterschiedliche Prozessor Versionen verfügen. Es tritt ein Fehler auf, und diese Meldung wird angezeigt:
 
**der virtuelle Computer kann nicht auf den Zielcomputer verschoben werden. Die Hardware auf dem Zielcomputer ist nicht mit den Hardwareanforderungen dieser virtuellen Maschine kompatibel.**
 
 Um dieses Problem zu beheben, fahren Sie den virtuellen Computer herunter, und aktivieren Sie die Einstellung für die Prozessor Kompatibilität.
 
1. Klicken Sie im Hyper-V-Manager im **Virtual Machines** Bereich mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie dann auf Einstellungen.
2. Erweitern Sie im Navigationsbereich die Option **Prozessoren** , und klicken Sie auf **Kompatibilität**.
3. Überprüfen Sie **die Migration zu einem Computer mit einer anderen Prozessor Version**.
4. Klicken Sie auf **OK**.
 
   Verwenden Sie zum Verwenden von Windows PowerShell das Cmdlet [Set-vmprocessor](https://technet.microsoft.com/library/hh848533.aspx) :
 
   ```
   PS C:\> Set-VMProcessor TestVM -CompatibilityForMigrationEnabled $true
   ```