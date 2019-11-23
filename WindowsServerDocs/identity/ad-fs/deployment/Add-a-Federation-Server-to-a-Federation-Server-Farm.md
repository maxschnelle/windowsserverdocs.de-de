---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: Hinzufügen eines Verbundservers zu einer Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 57c59241c36ba4ed657b83e7c691931f57978a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408520"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer Verbundserverfarm


Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mit der folgenden Prozedur fügen Sie einen Computer einer neuen Verbundserverfarm hinzu.  
  
Wenn Sie einen Computer mit dem Konfigurations-Assistenten für AD FS Verbund Server einer Farm hinzufügen. Wenn Sie diesen Assistenten zum Hinzufügen eines Computers zu einer vorhandenen Farm verwenden, wird der Computer mit einer Schreib\-Kopie der AD FS Konfigurations Datenbank konfiguriert und muss Aktualisierungen von einem primären Verbund Server empfangen.  
  
> [!NOTE]  
> Für den Verbund-SSO-\-Sign\-on \(SSO\) Design müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>So fügen Sie einer Verbund Serverfarm einen Verbund Server hinzu  
  
1.  Es gibt zwei Möglichkeiten, den Assistenten für die Konfiguration des AD FS-Verbund Servers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Öffnen Sie nach Abschluss der Installation des Verbunddienst Rollen Dienstanbieter das\-Snap-in AD FS Verwaltung, und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link Konfigurations-Assistent für AD FS-Verbund **Server** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C:\\Windows\\ADFS** , und Doppel\-klicken Sie auf **fsconfigwizard. exe**.  
  
2.  Überprüfen Sie auf der Seite **Willkommen**, ob **Verbundserver vorhandenem Verbunddienst hinzufügen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. Klicken Sie in diesem Fall auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS Datenbank nicht wichtig sind oder nicht in einer Produktions-Verbund Serverfarm verwendet werden.  
  
4.  Geben Sie auf der Seite **Primären Verbundserver und Dienstkonto angeben** unter **Name des primären Verbundservers** den Computernamen des primären Verbundservers in der Farm ein, und klicken Sie dann auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** das Domänenkonto, das von allen anderen Verbundservern in der vorhandenen Verbundserverfarm als Dienstkonto verwendet werden soll, und klicken Sie dann auf **OK**. Geben Sie das Kennwort ein, bestätigen Sie es, und klicken Sie dann auf **weiter**:  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienst Kontos für eine Verbund Serverfarm finden Sie unter [Manuelles Konfigurieren eines Dienst Kontos für eine Verbund Serverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Jeder Verbund Server in der Verbund Serverfarm muss das gleiche Dienst Konto angeben, damit die Farm betriebsbereit ist. Wenn beispielsweise das erstellte Dienst Konto "ttoso\\ADFS2SVC" ist, muss jeder Computer, den Sie für die Verbund Server Rolle konfigurieren und der Teil derselben Farm sein wird, in diesem Schritt im Assistenten für die Konfiguration des Verbund Servers die Angabe von "\\ADFS2SVC" angeben, damit die Farm betriebsbereit ist.  
  
5.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **weiter** , um mit dem Konfigurieren von AD FS mit diesen Einstellungen zu beginnen.  
  
6.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  

