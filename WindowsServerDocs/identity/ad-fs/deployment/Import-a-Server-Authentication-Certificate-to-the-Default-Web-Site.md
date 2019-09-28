---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b1c602d0cdfa562469419de223f5691ec2ff4527
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359562"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite

Nachdem Sie ein Server Authentifizierungszertifikat von einer Zertifizierungsstelle erhalten \(ca @ no__t-1, müssen Sie dieses Zertifikat manuell auf der Standard Website für jeden Verbund Server oder Verbund Server Proxy in einer Serverfarm installieren.  
  
Für Webserver müssen Sie das Serverauthentifizierungszertifikat manuell auf der entsprechenden Website oder in dem virtuellen Verzeichnis installieren, im dem sich Ihre Verbundanwendung befindet.  
  
Wenn Sie eine Farm einrichten, achten Sie darauf, dass Sie dieses Verfahren auf jedem der Server in der Farm identisch – mit exakt denselben Einstellungen – durchführen.  
  
> [!NOTE]  
> Das AD FS-Verwaltungs-Snap @ no__t-0in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>So importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite  
  
1.  Geben Sie auf dem **Start** Bildschirm**Internetinformationsdienste \(iis @ no__t-3 Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Doppelklicken Sie im mittleren Bereich auf **Server Zertifikate**no__t-0.  
  
4.  Klicken Sie im Bereich **Aktionen** auf **Importieren**.  
  
5.  Klicken Sie im Dialogfeld **Zertifikat importieren** auf die **...** .  
  
6.  Navigieren Sie zum Speicherort der PFX-Zertifikatdatei, markieren Sie diese, und klicken Sie dann auf **Öffnen**.  
  
7.  Geben Sie das Kennwort für das Zertifikat ein, und klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Zertifikatanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

