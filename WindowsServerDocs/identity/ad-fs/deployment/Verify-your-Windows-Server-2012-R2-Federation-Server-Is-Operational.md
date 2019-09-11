---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: Überprüfen, ob Ihr Windows Server 2012 R2-Verbund Server betriebsbereit ist
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d32338d0e9242d12ab18fd30192736ea3b44fdb4
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868055"
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Überprüfen, ob Ihr Windows Server 2012 R2-Verbund Server betriebsbereit ist



Mit den folgenden Prozeduren können Sie sicherstellen, dass ein Verbundserver funktionstüchtig ist, d. h., dass jeder Client in demselben Netzwerk einen neuen Verbundserver erreichen kann.  
  
Zum Abschließen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Benutzer**, **Sicherungs-Operatoren**, **Hauptbenutzer**, **Administratoren** oder in einer anderen entsprechenden Gruppe auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>Prozedur 1: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich bei \(einem\) Client Computer an, der sich in derselben Gesamtstruktur wie der Verbund Server befindet, um zu überprüfen, ob Internetinformationsdienste IIS ordnungsgemäß auf dem Verbund Server konfiguriert ist.  
  
2.  Öffnen Sie ein Browserfenster, geben Sie in der Adressleiste den DNS-Hostnamen des Verbund Servers ein, \/und fügen\/Sie\/dann ADFS fs FederationServerService. asmx für den neuen Verbund Server hinzu, z. b.:  
  
    **https:\/\/FS1.fabrikam.comADFS\/FS\/FederationServerService.asmx\/**  
  
3.  Drücken Sie die EINGABETASTE, und führen Sie dann auf dem Verbundservercomputer die nächste Prozedur aus. Wenn die Meldung Es besteht **ein Problem mit dem Sicherheitszertifikat der Website**angezeigt wird, klicken Sie **auf diese Website fortsetzen**.  
  
    Als Ausgabe wird eine XML-Anzeige mit dem Dienstbeschreibungsdokument erwartet. Wenn diese Seite angezeigt wird, ist IIS auf dem Verbundserver funktionstüchtig und verarbeitet Anforderungen der Seiten erfolgreich.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>Prozedur 2: So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Melden Sie sich beim neuen Verbund Server als Administrator an.  
  
2.  Geben Sie auf dem **Start** Bildschirm**Ereignisanzeige**ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Doppel\-klicken Sie im Detailbereich auf **Anwendungs-und Dienst Protokolle**,\-Doppelklicken Sie auf **AD FS**Ereignis, und klicken Sie dann auf **Admin**.  
  
4.  Suchen Sie in der Spalte **Ereignis-ID** nach der Ereignis-ID 100. Wenn der Verbund Server ordnungsgemäß konfiguriert ist, wird ein neues Ereignis – im Anwendungsprotokoll von Ereignisanzeige – mit der Ereignis-ID 100 angezeigt. Dieses Ereignis überprüft, ob der Verbund Server erfolgreich mit dem Verbunddienst kommunizieren konnte.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
   
  

