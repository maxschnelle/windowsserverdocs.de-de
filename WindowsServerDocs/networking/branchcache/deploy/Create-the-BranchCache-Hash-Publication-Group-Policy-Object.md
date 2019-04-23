---
title: Erstellen des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15e89b961d20b6f14065392553e413374358062d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865431"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>Erstellen des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um die BranchCache-hashveröffentlichung (Group Policy Object, GPO) zu erstellen.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Vor dem Ausführen dieses Verfahrens müssen Sie die Organisationseinheit mit den BranchCache-Dateiservern erstellen und Dateiserver in die Organisationseinheit verschieben. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>Um die BranchCache-hashveröffentlichung Gruppenrichtlinienobjekt zu erstellen  
  
1.  Öffnen Sie Windows PowerShell, geben Sie **mmc**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienverwaltung**, und klicken Sie anschließend auf **OK**.  
  
4.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-MMC den Pfad zur Organisationseinheit mit den BranchCache-Dateiservern, die Sie zuvor erstellt haben. Wenn Ihre Gesamtstruktur ist "Beispiel.com" mit dem Namen, Ihrer Domäne, ist example1.com ", und der Name der Organisationseinheit" BranchCache-Dateiservern, erweitern Sie z. B. den folgenden Pfad: **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: "example.com"**, **Domänen**, **example1.com**, **BranchCache-Dateiservern**.  
  
5.  Mit der rechten Maustaste **BranchCache-Dateiservern**, und klicken Sie dann auf **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. In **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt. Wenn Sie das Objekt z. B. „BranchCache-Hashveröffentlichung“ nennen möchten, geben Sie **BranchCache-Hashveröffentlichung** ein. Klicken Sie auf **OK**.  
  


