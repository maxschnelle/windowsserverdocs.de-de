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
ms.openlocfilehash: 2034b4c35061879a64004486395d0887c59087b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877711"
---
# <a name="verify-that-a-federation-server-is-operational"></a>Überprüfen, ob ein Verbundserver betriebsbereit ist

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit den folgenden Prozeduren können Sie sicherstellen, dass ein Verbundserver funktionstüchtig ist, d. h., dass jeder Client in demselben Netzwerk einen neuen Verbundserver erreichen kann.  
  
Zum Abschließen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Benutzer**, **Sicherungs-Operatoren**, **Hauptbenutzer**, **Administratoren** oder in einer anderen entsprechenden Gruppe auf dem lokalen Computer erforderlich.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>Schritt 1: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Um sicherzustellen, dass Internetinformation Services \(IIS\) ordnungsgemäß konfiguriert ist, auf dem Verbundserver, melden Sie sich bei einem Clientcomputer, die in der gleichen Gesamtstruktur wie der Verbundserver befindet.  
  
2.  Öffnen ein Browserfenster, in der Adressleiste den Verbund des Server-DNS-Hostname, und fügen Sie dann /adfs/fs/federationserverservice.asmx, für den neuen Verbundserver, z. B.:  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Drücken Sie die EINGABETASTE, und führen Sie dann auf dem Verbundservercomputer die nächste Prozedur aus. Wenn die Meldung **Es besteht ein Problem mit dem Sicherheitszertifikat der Website** angezeigt wird, klicken Sie auf **Laden dieser Website fortsetzen**.  
  
    Als Ausgabe wird eine XML-Anzeige mit dem Dienstbeschreibungsdokument erwartet. Wenn diese Seite angezeigt wird, ist IIS auf dem Verbundserver funktionstüchtig und verarbeitet Anforderungen der Seiten erfolgreich.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>Schritt 2: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich an den neuen Verbundserver als Administrator an.  
  
2.  Auf der **starten** geben **Ereignisanzeige**, und drücken Sie dann die EINGABETASTE.  
  
3.  Doppelklicken Sie im Detailbereich,\-klicken Sie auf **Anwendungs- und Dienstprotokolle**, double\-klicken Sie auf **AD FS-Ereignisse**, und klicken Sie dann auf **Admin**.  
  
4.  In der **Ereignis-ID** Spalte, suchen Sie nach Ereignis-ID 100. Wenn der Verbundserver ordnungsgemäß konfiguriert ist, sehen Sie ein neues Ereignis – im Anwendungsprotokoll der Ereignisanzeige, mit der Ereignis-ID 100. Dieses Ereignis bestätigt, dass der Verbundserver erfolgreich mit dem Verbunddienst kommunizieren konnte.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Das Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

