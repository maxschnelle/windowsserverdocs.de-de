---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: Hinzufügen eines Verbundservers zu einer Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 040caf6395b7c70313de900d522241f97699a999
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192502"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer Verbundserverfarm


Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Mit der folgenden Prozedur fügen Sie einen Computer einer neuen Verbundserverfarm hinzu.  
  
Zum Hinzufügen eines Computers zu einer Farm mit AD FS Federation Server-Konfigurations-Assistenten. Wenn Sie diesen Assistenten zum Hinzufügen eines Computers zu einer vorhandenen Farm verwenden, wird der Computer für einen Lesevorgang konfiguriert\-nur Kopie der AD FS-Konfigurationsdatenbank und Updates von einem primären Verbundserver empfangen muss.  
  
> [!NOTE]  
> Für die einzelnen für Federated Web\-anmelden\-auf \(SSO\) -Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation . Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>Einer Verbundserverfarm einen Verbundserver hinzu  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Konfigurations-Assistenten zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Nachdem die Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap\-in, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** auf einen link auf die **Übersicht über die** Seite oder in der **Aktionen** Bereich.  
  
    -   Nachdem der Setup-Assistent abgeschlossen wurde, öffnen ein Windows-Explorer, navigieren zu der **"c:"\\Windows\\ADFS** Ordner und die doppelte\-klicken Sie auf **FsConfigWizard.exe**.  
  
2.  Überprüfen Sie auf der Seite **Willkommen**, ob **Verbundserver vorhandenem Verbunddienst hinzufügen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Wenn die AD FS-Datenbank, die Sie bereits ausgewählt vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Klicken Sie in diesem Fall auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank nicht von Bedeutung ist oder sie nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
4.  Geben Sie auf der Seite **Primären Verbundserver und Dienstkonto angeben** unter **Name des primären Verbundservers** den Computernamen des primären Verbundservers in der Farm ein, und klicken Sie dann auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** das Domänenkonto, das von allen anderen Verbundservern in der vorhandenen Verbundserverfarm als Dienstkonto verwendet werden soll, und klicken Sie dann auf **OK**. Geben Sie das Kennwort, und bestätigen Sie es, und klicken Sie dann auf **Weiter**:  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienstkontos für eine Verbundserverfarm finden Sie unter [manuell konfigurieren eines Dienstkontos für eine Verbundserverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Jeden Verbundserver in der Verbundserverfarm muss für die Farm betriebsbereit ist dasselbe Dienstkonto angeben. Wenn das Dienstkonto, das erstellt wurde, Contoso wurde z. B.\\ADFS2SVC, muss jeder Computer, die Sie für die Verbundserver-Rolle konfigurieren und in der gleichen Farm einbezogen wird Contoso angeben\\ADFS2SVC in diesem Schritt die Konfigurations-Assistenten für die Farm betriebsbereit ist.  
  
5.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn Sie die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** um Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
6.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

