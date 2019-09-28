---
title: Erstellen des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 10230b57075943a5d92dce7155e794293157cba4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356638"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>Erstellen des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Verfahren verwenden, um das BranchCache-Hash Veröffentlichungs Gruppenrichtlinie-Objekt (GPO) zu erstellen.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Vor dem Ausführen dieses Verfahrens müssen Sie die Organisationseinheit mit den BranchCache-Dateiservern erstellen und Dateiserver in die Organisationseinheit verschieben. Weitere Informationen finden Sie unter [Aktivieren der Hash Veröffentlichung für Domänen Mitglieds-Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>So erstellen Sie die BranchCache-Hash Veröffentlichung Gruppenrichtlinie-Objekt  
  
1.  Öffnen Sie Windows PowerShell, geben Sie **mmc**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienverwaltung**, und klicken Sie anschließend auf **OK**.  
  
4.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-MMC den Pfad zur Organisationseinheit mit den BranchCache-Dateiservern, die Sie zuvor erstellt haben. Wenn Ihre Gesamtstruktur beispielsweise den Namen example.com hat, die Domäne example1.com lautet und ihre Organisationseinheit den Namen BranchCache-Dateiserver hat, erweitern Sie den folgenden Pfad: **Gruppenrichtlinie Verwaltung**, Gesamtstruktur **: example.com**, **Domänen**, **example1.com**, **BranchCache-Dateiserver**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **BranchCache-Dateiserver**, und klicken Sie dann auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. Geben Sie unter **Name**einen Namen für das neue Gruppenrichtlinien Objekt ein. Wenn Sie das Objekt z. B. „BranchCache-Hashveröffentlichung“ nennen möchten, geben Sie **BranchCache-Hashveröffentlichung** ein. Klicken Sie auf **OK**.  
  


