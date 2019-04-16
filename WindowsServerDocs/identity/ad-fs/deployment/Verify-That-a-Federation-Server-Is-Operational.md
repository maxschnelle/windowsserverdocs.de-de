---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: Stellen Sie sicher, dass ein Verbundserver betriebsbereit ist
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2034b4c35061879a64004486395d0887c59087b2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="verify-that-a-federation-server-is-operational"></a>Stellen Sie sicher, dass ein Verbundserver betriebsbereit ist

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die folgenden Verfahren können überprüfen, ob ein Verbundserver betriebsbereit ist. Das heißt, dass alle Clients im gleichen Netzwerk einen neuen Verbundserver erreichen kann.  
  
Mitgliedschaft in **Benutzer**, **Sicherungsoperatoren**, **Hauptbenutzer**, **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer ist mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>Schritt 1: Überprüfen, ob ein Verbundserver betriebsbereit ist  
  
1.  Um zu überprüfen, ob Internetinformationsdienste \(IIS\) auf dem Verbundserver richtig konfiguriert ist, melden Sie sich bei einem Clientcomputer, der sich in derselben Gesamtstruktur wie der Verbundserver befindet.  
  
2.  Öffnen Sie ein Browserfenster, in der Leiste Adresstyp am Verbund des Server-DNS-Hostnamen, und fügen Sie /adfs/fs/federationserverservice.asmx, für den neuen Verbundserver, beispielsweise:  
  
    **https://FS1.Fabrikam.com/ADFS/FS/federationserverservice.asmx**  
  
3.  Drücken Sie die EINGABETASTE, und führen Sie das nächste Verfahren auf dem verbundservercomputer. Wenn die Meldung **besteht ein Problem mit dem Sicherheitszertifikat dieser Website**, klicken Sie auf **Laden dieser Website fortsetzen**.  
  
    Die erwartete Ausgabe ist eine XML-Anzeige mit dem Dienstbeschreibungsdokument. Wenn diese Seite angezeigt wird, ist IIS auf dem Verbundserver funktionstüchtig und verarbeitet Anforderungen Seiten erfolgreich.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>Schritt 2: Überprüfen, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich an den neuen Verbundserver als Administrator an.  
  
2.  Auf der **starten** geben **Ereignisanzeige**, und drücken Sie dann die EINGABETASTE.  
  
3.  Klicken Sie im Detailbereich doppelten Mausklick **Anwendungs- und Dienstprotokolle**, doppelten Mausklick **Ereignisse für AD FS**, und klicken Sie dann auf **Admin**.  
  
4.  In der **Ereignis-ID** Spalte, suchen Sie nach der Ereignis-ID 100. Wenn der Verbundserver richtig konfiguriert ist, sehen Sie ein neues Ereignis – im Anwendungsprotokoll der Ereignisanzeige – mit der Ereignis-ID 100. Dieses Ereignis ist Beleg dafür, dass der Verbundserver erfolgreich mit dem Verbunddienst kommunizieren konnte.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

