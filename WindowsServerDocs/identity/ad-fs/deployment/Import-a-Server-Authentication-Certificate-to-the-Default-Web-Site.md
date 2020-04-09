---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3f02358167b024247f934a46218028575e393ba9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855403"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite

Nachdem Sie ein Server Authentifizierungszertifikat von einer Zertifizierungsstelle \(Zertifizierungsstelle\)erhalten haben, müssen Sie dieses Zertifikat manuell auf der Standard Website jedes Verbund Servers oder Verbund Server Proxys in einer Serverfarm installieren.  
  
Für Webserver müssen Sie das Serverauthentifizierungszertifikat manuell auf der entsprechenden Website oder in dem virtuellen Verzeichnis installieren, im dem sich Ihre Verbundanwendung befindet.  
  
Wenn Sie eine Farm einrichten, achten Sie darauf, dass Sie dieses Verfahren auf jedem der Server in der Farm identisch – mit exakt denselben Einstellungen – durchführen.  
  
> [!NOTE]  
> Der AD FS-Verwaltungs-Snap\-in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>So importieren Sie ein Serverauthentifizierungszertifikat auf die Standardwebsite  
  
1.  Geben Sie auf dem **Start** Bildschirm**Internetinformationsdienste \(IIS-\)-Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Doppel\-klicken Sie im mittleren Bereich auf **Server Zertifikate**.  
  
4.  Klicken Sie im Bereich **Aktionen** auf **Importieren**.  
  
5.  Klicken Sie im Dialogfeld **Zertifikat importieren** auf die **...** .  
  
6.  Suchen Sie nach dem Speicherort der Zertifikatsdatei mit der Erweiterung **PFX**, wählen Sie sie aus, und klicken Sie auf Öffnen.  
  
7.  Geben Sie das Kennwort für das Zertifikat ein, und klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Zertifikatanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

