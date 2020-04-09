---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: Hinzufügen eines Verbundservers zu einer Verbundserverfarm
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ea826f8984937c5d32a830131f042a8519528268
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815053"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer Verbundserverfarm


Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mit der folgenden Prozedur fügen Sie einen Computer einer neuen Verbundserverfarm hinzu.  
  
Zum Hinzufügen eines Computers zu einer Farm verwenden Sie den AD FS-Assistenten für die Konfiguration des Verbundservers. Wenn Sie diesen Assistenten zum Hinzufügen eines Computers zu einer vorhandenen Farm verwenden, wird der Computer mit einer Schreib\-Kopie der AD FS Konfigurations Datenbank konfiguriert und muss Aktualisierungen von einem primären Verbund Server empfangen.  
  
> [!NOTE]  
> Für den Verbund-SSO-\-Sign\-on \(SSO\) Design müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>So fügen Sie einer Verbund Serverfarm einen Verbund Server hinzu  
  
1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Öffnen Sie nach Abschluss der Installation des Verbunddienst Rollen Dienstanbieter das\-Snap-in AD FS Verwaltung, und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link Konfigurations-Assistent für AD FS-Verbund **Server** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C:\\Windows\\ADFS** , und Doppel\-klicken Sie auf **fsconfigwizard. exe**.  
  
2.  Vergewissern Sie sich auf der Seite **Willkommen**, dass die Option **Einem vorhandenen Verbunddienst einen Verbundserver hinzufügen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Wenn die AD FS-Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **Vorhandene AD FS-Konfigurationsdatenbank ermittelt** angezeigt. In diesem Fall klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank unwichtig sind bzw. nicht in einer Produktions-Verbundserverfarm verwendet werden.  
  
4.  Geben Sie auf der Seite **Primären Verbundserver und Dienstkonto angeben** unter **Name des primären Verbundservers** den Computernamen des primären Verbundservers in der Farm ein, und klicken Sie dann auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** nach dem Domänenkonto, das von allen anderen Verbundservern als Dienstkonto in der vorhandenen Verbundserverfarm verwendet wird, und klicken Sie dann auf **OK**. Geben Sie das Kennwort ein, bestätigen Sie es, und klicken Sie dann auf **Weiter**:  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienst Kontos für eine Verbund Serverfarm finden Sie unter [Manuelles Konfigurieren eines Dienst Kontos für eine Verbund Serverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Jeder Verbund Server in der Verbund Serverfarm muss das gleiche Dienst Konto angeben, damit die Farm betriebsbereit ist. Wenn beispielsweise das erstellte Dienst Konto "ttoso\\ADFS2SVC" ist, muss jeder Computer, den Sie für die Verbund Server Rolle konfigurieren und der Teil derselben Farm sein wird, in diesem Schritt im Assistenten für die Konfiguration des Verbund Servers die Angabe von "\\ADFS2SVC" angeben, damit die Farm betriebsbereit ist.  
  
5.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um AD FS mit diesen Einstellungen zu konfigurieren.  
  
6.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  

