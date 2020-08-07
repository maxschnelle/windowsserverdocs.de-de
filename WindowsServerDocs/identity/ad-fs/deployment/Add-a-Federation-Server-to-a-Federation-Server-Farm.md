---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: Hinzufügen eines Verbundservers zu einer Verbundserverfarm
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 0b814a791b510cc32b496cabf272dedfd307caac
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947678"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer Verbundserverfarm


Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mit der folgenden Prozedur fügen Sie einen Computer einer neuen Verbundserverfarm hinzu.

Zum Hinzufügen eines Computers zu einer Farm verwenden Sie den AD FS-Assistenten für die Konfiguration des Verbundservers. Wenn Sie diesen Assistenten zum Hinzufügen eines Computers zu einer vorhandenen Farm verwenden, wird der Computer mit einer schreibgeschützten \- Kopie der AD FS Konfigurations Datenbank konfiguriert und muss Aktualisierungen von einem primären Verbund Server empfangen.

> [!NOTE]
> Für den Verbund \- \- \( -SSO-Entwurf für einmaliges Anmelden (SSO) \) müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807127(v=ws.11)).

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .

### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>So fügen Sie einer Verbund Serverfarm einen Verbund Server hinzu

1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:

    -   Nachdem der Verbunddienst-Rollen Dienst installiert ist, öffnen Sie das Snap-in AD FS Verwaltung, \- und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link AD FS Verbund Server- **Konfigurations-Assistent** .

    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C: \\ Windows \\ ADFS** , und Doppel \- Klicken Sie auf **FsConfigWizard.exe**.

2.  Vergewissern Sie sich auf der Seite **Willkommen**, dass die Option **Einem vorhandenen Verbunddienst einen Verbundserver hinzufügen** ausgewählt ist, und klicken Sie dann auf **Weiter**.

3.  Wenn die AD FS-Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **Vorhandene AD FS-Konfigurationsdatenbank ermittelt** angezeigt. In diesem Fall klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.

    > [!CAUTION]
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank unwichtig sind bzw. nicht in einer Produktions-Verbundserverfarm verwendet werden.

4.  Geben Sie auf der Seite **Primären Verbundserver und Dienstkonto angeben** unter **Name des primären Verbundservers** den Computernamen des primären Verbundservers in der Farm ein, und klicken Sie dann auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** nach dem Domänenkonto, das von allen anderen Verbundservern als Dienstkonto in der vorhandenen Verbundserverfarm verwendet wird, und klicken Sie dann auf **OK**. Geben Sie das Kennwort ein, bestätigen Sie es, und klicken Sie dann auf **Weiter**:

    > [!NOTE]
    > Weitere Informationen zum Angeben eines Dienst Kontos für eine Verbund Serverfarm finden Sie unter [Manuelles Konfigurieren eines Dienst Kontos für eine Verbund Serverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Jeder Verbund Server in der Verbund Serverfarm muss das gleiche Dienst Konto angeben, damit die Farm betriebsbereit ist. Wenn das erstellte Dienst Konto z. b. " \\ ADFS2SVC" lautet, muss jeder Computer, den Sie für die Verbund Server Rolle konfigurieren und der Teil derselben Farm sein wird, in diesem Schritt im Assistenten für die Konfiguration des Verbund Servers "" angeben, damit \\ die Farm betriebsbereit ist.

5.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um AD FS mit diesen Einstellungen zu konfigurieren.

6.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)

