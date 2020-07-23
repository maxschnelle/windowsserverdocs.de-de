---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importieren eines Serverauthentifizierungszertifikats zur Standardwebsite
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3205085f11f84d96513d31da6dbe0853c686429f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960032"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importieren eines Serverauthentifizierungszertifikats zur Standardwebsite

Nachdem Sie ein Server Authentifizierungszertifikat von einer Zertifizierungsstellen- \( Zertifizierungs \) Stelle erhalten haben, müssen Sie dieses Zertifikat manuell auf der Standard Website jedes Verbund Servers oder Verbund Server Proxys in einer Serverfarm installieren.  
  
Für Webserver müssen Sie das Serverauthentifizierungszertifikat manuell auf der entsprechenden Website oder in dem virtuellen Verzeichnis installieren, im dem sich Ihre Verbundanwendung befindet.  
  
Wenn Sie eine Farm einrichten, achten Sie darauf, dass Sie dieses Verfahren auf jedem der Server in der Farm identisch – mit exakt denselben Einstellungen – durchführen.  
  
> [!NOTE]  
> Das Snap-in "AD FS-Verwaltung" \- bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>So importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite  
  
1.  Geben Sie auf dem **Start** Bildschirm**Internetinformationsdienste \( IIS- \) Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Doppelklicken Sie im mittleren Bereich \- auf **Server Zertifikate**.  
  
4.  Klicken Sie im Bereich **Aktionen** auf **Importieren**.  
  
5.  Klicken Sie im Dialogfeld **Zertifikat importieren** auf die **...** .  
  
6.  Suchen Sie nach dem Speicherort der Zertifikatsdatei mit der Erweiterung **PFX**, wählen Sie sie aus, und klicken Sie auf Öffnen.  
  
7.  Geben Sie das Kennwort für das Zertifikat ein, und klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](../design/certificate-requirements-for-federation-servers.md)  
  
[Zertifikatanforderungen für Verbundserverproxys](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807054(v=ws.11))  
   
  
