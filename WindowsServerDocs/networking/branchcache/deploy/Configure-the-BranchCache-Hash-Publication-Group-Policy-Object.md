---
title: Konfigurieren des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 660a4979aa5e29a6dd22cb2e0e6659966d077a8e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319329"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>Konfigurieren des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit diesem Verfahren können Sie das BranchCache-Hash Veröffentlichungs Gruppenrichtlinie-Objekt (GPO) konfigurieren, sodass auf alle Dateiserver, die Sie Ihrer Organisationseinheit hinzugefügt haben, dieselbe Hash Veröffentlichungs Richtlinien Einstellung angewendet wird.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Bevor Sie dieses Verfahren ausführen, müssen Sie die Organisationseinheit für die BranchCache-Dateiserver erstellen, Dateiserver in die Organisationseinheit verschieben und das Gruppenrichtlinien Objekt BranchCache-Hash Veröffentlichung erstellen. Weitere Informationen finden Sie unter [Aktivieren der Hash Veröffentlichung für Domänen Mitglieds-Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>So konfigurieren Sie die BranchCache-Hash Veröffentlichung Gruppenrichtlinie-Objekt  
  
1.  Führen Sie Windows PowerShell als Administrator aus, geben Sie **MMC**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienverwaltung**, und klicken Sie anschließend auf **OK**.  
  
4.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-MMC den Pfad zum Gruppenlinienobjekt BranchCache-Hashveröffentlichung, das Sie zuvor erstellt haben. Wenn die Gesamtstruktur beispielsweise example.com lautet, die Domäne example1.com lautet und Ihr Gruppenrichtlinien Objekt den Namen **BranchCache Hash Publication**hat, erweitern Sie den folgenden Pfad: **Gruppenrichtlinie Verwaltung**, Gesamtstruktur **: example.com**, **Domänen**, **example1.com**, **Gruppenrichtlinie Objekte**, **BranchCache-Hash Veröffentlichung**.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **BranchCache-Hashveröffentlichung**, und wählen Sie **Bearbeiten** aus. Die Gruppenrichtlinienverwaltungs-Editor-Konsole wird geöffnet.  
  
6.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole den folgenden Pfad: **Computer Konfiguration**, **Richtlinien**, **Administrative Vorlagen**, **Netzwerk**, **LanMan-Server**.  
  
7.  Klicken Sie in der Konsole des Gruppenrichtlinienverwaltungs-Editors auf **LanMan-Server**. Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Das Dialogfeld **Hashveröffentlichung für BranchCache** wird geöffnet.  
  
8.  Klicken Sie im Dialogfeld **Hashveröffentlichung für BranchCache** auf **Aktiviert**.  
  
9. Klicken Sie unter Optionen auf **Hash Veröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf eine der folgenden **Optionen**:  
  
    1.  Um die Hash Veröffentlichung für alle freigegebenen Ordner für alle Dateiserver zu aktivieren, die Sie der Organisationseinheit hinzugefügt haben, klicken Sie auf **Hash Veröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um Hashveröffentlichung nur für freigegebene Ordner zu aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **Hashveröffentlichung nur für freigegebene Ordner mit aktiviertem BranchCache zulassen.**  
  
    3.  Um keine Hashveröffentlichung für alle freigegebenen Ordner auf dem Computer zuzulassen, auch wenn BranchCache auf den Dateifreigaben aktiviert ist, klicken Sie auf **Hashveröffentlichung für keinen freigegebenen Ordner zulassen**.  
  
10. Klicken Sie auf **OK**.  
  
> [!NOTE]  
> In den meisten Fällen müssen Sie die MMC-Konsole speichern und aktualisieren, um die vorgenommenen Konfigurationsänderungen anzuzeigen.  
  


