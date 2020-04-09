---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: Überprüfen, ob ein Verbundserver betriebsbereit ist
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b6ce4f826809e2c07fdbe4424d427f1244ea5172
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814253"
---
# <a name="verify-that-a-federation-server-is-operational"></a>Überprüfen, ob ein Verbundserver betriebsbereit ist


Mit den folgenden Prozeduren können Sie sicherstellen, dass ein Verbundserver funktionstüchtig ist, d. h., dass jeder Client in demselben Netzwerk einen neuen Verbundserver erreichen kann.  
  
Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer mindestens der Gruppe **Benutzer**, **Sicherungsoperatoren**, **Hauptbenutzer**, **Administratoren** o. ä. angehören.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>Prozedur 1: So überprüfen Sie, ob ein Verbund Serverbetriebs bereit ist  
  
1.  Melden Sie sich bei einem Client Computer an, der sich in derselben Gesamtstruktur wie der Verbund Server befindet, um zu überprüfen, ob Internetinformationsdienste \(IIS\) ordnungsgemäß auf dem Verbund Server konfiguriert ist.  
  
2.  Öffnen Sie ein Browserfenster, geben Sie in der Adressleiste den DNS-Hostnamen des Verbund Servers ein, und fügen Sie dann/ADFS/fs/FederationServerService.asmx für den neuen Verbund Server an. Beispiel:  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Drücken Sie die EINGABETASTE, und führen Sie dann auf dem Verbundservercomputer die nächste Prozedur aus. Wenn die Meldung Es besteht **ein Problem mit dem Sicherheitszertifikat der Website**angezeigt wird, klicken Sie **auf diese Website fortsetzen**.  
  
    Als Ausgabe wird eine XML-Anzeige mit dem Dienstbeschreibungsdokument erwartet. Wenn diese Seite angezeigt wird, ist IIS auf dem Verbundserver funktionstüchtig und verarbeitet Anforderungen der Seiten erfolgreich.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>Prozedur 2: So überprüfen Sie, ob ein Verbund Serverbetriebs bereit ist  
  
1.  Melden Sie sich am neuen Verbundserver als Administrator an.  
  
2.  Geben Sie auf dem **Start** Bildschirm **Ereignisanzeige**ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Doppel\-klicken Sie im Detailbereich auf **Anwendungs-und Dienst Protokolle**, Doppel\-klicken Sie auf **AD FS**Ereignis, und klicken Sie dann auf **Admin**.  
  
4.  Suchen Sie in der Spalte **Ereignis-ID** nach der Ereignis-ID 100. Wenn der Verbund Server ordnungsgemäß konfiguriert ist, wird ein neues Ereignis – im Anwendungsprotokoll von Ereignisanzeige – mit der Ereignis-ID 100 angezeigt. Dieses Ereignis überprüft, ob der Verbund Server erfolgreich mit dem Verbunddienst kommunizieren konnte.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  

