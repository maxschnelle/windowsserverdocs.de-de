---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: "Hinzufügen eines Verbundservers zu einer Verbundserverfarm"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d67f4c252ad25a05f11b88771f12fd01d13137d4
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer Verbundserverfarm

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Das folgende Verfahren können zum Hinzufügen eines Computers zu einer neuen Verbundserverfarm.  
  
In einer Farm mit AD FS Federation Server-Konfigurations-Assistenten können Sie einen Computer hinzufügen. Wenn Sie diesen Assistenten zum Hinzufügen eines Computers zu einer vorhandenen Farm verwenden, der Computer ist eine schreibgeschützte Kopie der AD FS-Konfigurationsdatenbank konfiguriert, und es Updates von einem primären Verbundserver empfangen muss.  
  
> [!NOTE]  
> Für den Federated-Web-Single\-Sign\-On \(SSO\)-Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation. Weitere Informationen finden Sie unter [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx).  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen ein Verbundservers zu einer Verbundserverfarm  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Federation Server-Konfigurations-Assistenten zu starten. Um den Assistenten zu starten, führen Sie eine der folgenden:  
  
    -   Nach der Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap-In, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** link der **Übersicht** Seite oder in der **Aktionen** Bereich.  
  
    -   Jederzeit nach Abschluss des Setup-Assistenten öffnen Windows Explorer, navigieren Sie zu der **C:\\Windows\\ADFS** Ordner, und klicken Sie mit der doppelten **FsConfigWizard.exe**.  
  
2.  Auf der **Willkommen** überprüfen Sie, ob Seite **Verbundserver vorhandenem Verbunddienst hinzufügen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Wenn die AD FS-Konfigurationsdatenbank, die Sie ausgewählt haben bereits vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Klicken Sie in diesem Fall **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Konfigurationsdatenbank nicht wichtig ist oder diese nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
4.  Auf der **Geben Sie den primären Verbundserver und Dienstkonto** Seite unter **primären Verbundserver Servername**, geben Sie den Computernamen des primären Verbundservers in der Farm ein, und klicken Sie dann auf **Durchsuchen**. In der **Durchsuchen** Dialogfeld, suchen Sie das Domänenkonto an, die durch alle anderen Verbundserver in der vorhandenen Verbundserverfarm als Dienstkonto verwendet wird, und klicken Sie dann auf **OK**. Geben Sie das Kennwort und bestätigen Sie es, und klicken Sie dann auf **Weiter**:  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienstkontos für eine Verbundserverfarm finden Sie unter [manuell konfigurieren eines Dienstkontos für eine Verbundserverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Jeder Verbundserver in der Verbundserverfarm muss für die Farm betriebsbereit ist das gleiche Dienstkonto angeben. Wenn beispielsweise das Dienstkonto, das erstellt wurde contoso\\ADFS2SVC war, muss jeden Computer, die Sie für die Verbundserver-Rolle konfigurieren und in derselben Farm einbezogen wird contoso\\ADFS2SVC an dieser Stelle in der Konfigurations-Assistenten für die Farm betriebsbereit ist angeben.  
  
5.  Auf der **bereit zum Anwenden der Einstellungen** Seite, überprüfen Sie die Detail. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** zum Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
6.  Auf der **Konfigurationsergebnisse** Seite, überprüfen Sie die Ergebnisse. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

