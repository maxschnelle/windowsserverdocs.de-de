---
title: Die Anzahl der ausgeführten oder konfigurierte virtuelle Computer muss innerhalb der unterstützten Limits
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9d3c4aa3-8416-46ec-a253-26dc98088d7b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8a971a48b2d8199a6c279f1bd3f1715039fa6e0d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855351"
---
# <a name="the-number-of-running-or-configured-virtual-machines-must-be-within-supported-limits"></a>Die Anzahl der ausgeführten oder konfigurierte virtuelle Computer muss innerhalb der unterstützten Limits

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt Text erscheint in der Best Practices Analyzer-Tool zur Lösung dieses Problems Kursivdruck an.  
  
## <a name="issue"></a>Problem  
*Weitere virtuelle Computer werden ausgeführt oder als unterstützt konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
*Microsoft unterstützt nicht die aktuelle Anzahl von virtuellen Computern ausgeführt wird oder auf diesem Server konfiguriert.*  
  
## <a name="resolution"></a>Auflösung  
*Verschieben Sie eine oder mehrere virtuelle Computer, auf einen anderen Server.*  
  
Informationen zur maximal unterstützten Konfigurationen für Hyper-V, z. B. die Anzahl der ausgeführten virtuellen Computern finden Sie unter [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).  
  
Um einen virtuellen Computer auf einen anderen Server verschieben, können Sie folgende Aktionen ausführen:  
  
- Exportieren Sie die virtuelle Maschine vom aktuellen Server, und klicken Sie dann auf einen neuen Server importieren Sie, wie unten beschrieben.   
- Führen Sie eine Livemigration:   
    - Wenn dieser Server zu einem Failovercluster gehört, verwenden Sie die Tools, mit dem Feature "Failoverclustering" bereitgestellt. Anweisungen hierzu finden Sie unter [Livemigration, Schnellmigration oder Verschieben eines virtuellen Computers von Knoten zu Knoten](https://go.microsoft.com/fwlink/?LinkID=181519).  
    - Wenn dies auf einem eigenständigen Server ist, finden Sie Anweisungen in [Livemigration konfigurieren und Migrieren von virtuellen Maschinen ohne Failoverclustering](https://technet.microsoft.com//library/jj134199(v=ws.11).aspx)  
  
### <a name="to-export-a-virtual-machine"></a>Zum Exportieren eines virtuellen Computers  
  
   > [!IMPORTANT]  
   > Wenn der Hyper-V-Host, die, dem Sie beim Exportieren aus, einer Domäne angehört, und die exportierten Dateien an einem Remotestandort gespeichert werden soll, muss der Hyper-V-Host für die eingeschränkte Delegierung konfiguriert werden. Ein Remotespeicherort kann sein, einen freigegebenen Netzwerkordner oder einen Ordner auf dem Host, dem Sie in importieren können. Eingeschränkter Delegierung können das Computerkonto des Hyper-V-Hosts, für den delegierten Anmeldeinformationen für den Dienst Common Internet File System (CIFS) auf den Remotecomputer anzugeben. Anweisungen zum Konfigurieren der eingeschränkten Delegierung finden Sie im Abschnitt nach dem Export, und importieren Sie die Anweisungen unten.  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**mit der rechten Maustaste auf einen virtuellen Computer, und klicken Sie dann auf **exportieren**.  
  
3.  In der **Exportieren eines virtuellen Computers** (Dialogfeld), Typ oder suchen Sie einen Speicherort mit ausreichend freiem Speicherplatz für alle Ressourcen des virtuellen Computers zu speichern. Wenn Sie einen virtuellen Computer exportieren, werden alle virtuellen Festplatten (VHD-Dateien oder vhdx-Dateien), Prüfpunkte (AVHD-Dateien) und der virtuellen Maschine zugeordneten Dateien mit gespeichertem Zustand in den angegebenen Ordner kopiert.  
  
4.  Klicken Sie auf **Exportieren**.  
  
Importieren Sie die virtuellen Computer nach dem Exportieren der virtuellen Computer, auf dem anderen Server.  
  
### <a name="to-import-a-virtual-machine-to-another-server"></a>So importieren Sie einen virtuellen Computer auf einen anderen server  
  
1.  Verbinden mit dem Server mit Hyper-V und Hyper-V-Manager zu öffnen.  
  
2.  In der **Aktion** Bereich, klicken Sie auf **importieren virtueller Computer**.  
  
3.  In der **importieren virtueller Computer** Dialogfeld geben den Speicherort, in dem Sie den virtuellen Computer exportiert haben. Wenn Sie diesen virtuellen Computer importieren möchten, lassen Sie die Importieren von Einstellungen unverändert.  
  
4.  Klicken Sie auf **Importieren**.  
  
### <a name="to-configure-constrained-delegation"></a>So konfigurieren Sie eingeschränkte Delegierung  
  
Mitgliedschaft in der **Domänenadministratoren** Gruppe ist erforderlich, um dieses Verfahren abzuschließen.  
  
1.  Auf einem Computer mit der Active Directory Domain Services-Tools-Feature installiert haben, im **Verwaltung**öffnen **Active Directory-Benutzer und-Computer**, und navigieren Sie dann auf das Computerkonto für der Computer mit Hyper-V.  
  
    > [!NOTE]  
    > Wenn **Active Directory-Benutzer und -Computer** nicht angezeigt wird, installieren Sie die Tools für die Active Directory-Domänendienste. Anweisungen hierzu finden Sie unter [Installieren von Remoteserver-Verwaltungstools für AD DS](https://go.microsoft.com/fwlink/?LinkId=140463) (https://go.microsoft.com/fwlink/?LinkId=140463).  
  
2.  Mit der rechten Maustaste in des Computerkontos für den Computer mit Hyper-V, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf die Option **Computer bei Delegierungen angegebener Dienste auswählen** auf der Registerkarte **Delegierung**, und wählen Sie dann **Beliebiges Authentifizierungsprotokoll verwenden** aus.  
  
4.  So ermöglichen Sie das Hyper-V-Computerkonto in delegierten Anmeldeinformationen für den Remotecomputer anwendbar:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  In der **Dienste hinzufügen** Dialogfeld klicken Sie auf **Benutzer oder Computer**, wählen Sie den Remotecomputer, und klicken Sie dann auf **OK**.  
  
    3.  In der **verfügbare Dienste** Liste der **Cifs** -Protokolls (auch bezeichnet als das Server Message Block (SMB)-Protokoll), und klicken Sie dann auf **hinzufügen**.  
  
  
  


