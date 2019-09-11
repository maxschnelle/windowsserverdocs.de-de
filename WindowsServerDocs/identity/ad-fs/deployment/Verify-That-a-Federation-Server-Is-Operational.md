---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: Überprüfen, ob ein Verbundserver betriebsbereit ist
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdaa43fcb501405529415de950ecdf40a91ed088
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868046"
---
# <a name="verify-that-a-federation-server-is-operational"></a>Überprüfen, ob ein Verbundserver betriebsbereit ist


Mit den folgenden Prozeduren können Sie sicherstellen, dass ein Verbundserver funktionstüchtig ist, d. h., dass jeder Client in demselben Netzwerk einen neuen Verbundserver erreichen kann.  
  
Zum Abschließen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Benutzer**, **Sicherungs-Operatoren**, **Hauptbenutzer**, **Administratoren** oder in einer anderen entsprechenden Gruppe auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>Prozedur 1: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich bei \(einem\) Client Computer an, der sich in derselben Gesamtstruktur wie der Verbund Server befindet, um zu überprüfen, ob Internetinformationsdienste IIS ordnungsgemäß auf dem Verbund Server konfiguriert ist.  
  
2.  Öffnen Sie ein Browserfenster, geben Sie in der Adressleiste den DNS-Hostnamen des Verbund Servers ein, und fügen Sie dann/ADFS/fs/FederationServerService.asmx für den neuen Verbund Server an. Beispiel:  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Drücken Sie die EINGABETASTE, und führen Sie dann auf dem Verbundservercomputer die nächste Prozedur aus. Wenn die Meldung Es besteht **ein Problem mit dem Sicherheitszertifikat der Website**angezeigt wird, klicken Sie **auf diese Website fortsetzen**.  
  
    Als Ausgabe wird eine XML-Anzeige mit dem Dienstbeschreibungsdokument erwartet. Wenn diese Seite angezeigt wird, ist IIS auf dem Verbundserver funktionstüchtig und verarbeitet Anforderungen der Seiten erfolgreich.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>Prozedur 2: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich beim neuen Verbund Server als Administrator an.  
  
2.  Geben Sie auf dem **Start** Bildschirm **Ereignisanzeige**ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Doppel\-klicken Sie im Detailbereich auf **Anwendungs-und Dienst Protokolle**,\-Doppelklicken Sie auf **AD FS**Ereignis, und klicken Sie dann auf **Admin**.  
  
4.  Suchen Sie in der Spalte **Ereignis-ID** nach der Ereignis-ID 100. Wenn der Verbund Server ordnungsgemäß konfiguriert ist, wird ein neues Ereignis – im Anwendungsprotokoll von Ereignisanzeige – mit der Ereignis-ID 100 angezeigt. Dieses Ereignis überprüft, ob der Verbund Server erfolgreich mit dem Verbunddienst kommunizieren konnte.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

