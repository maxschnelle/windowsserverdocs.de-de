---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importieren Sie ein Serverauthentifizierungszertifikat auf die Standardwebsite
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7bc890c744de5cd86d4e8b0418e75512518f656c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importieren Sie ein Serverauthentifizierungszertifikat auf die Standardwebsite

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie einen Server-Authentifizierungszertifikat von einer Zertifizierungsstelle erhalten \(CA\), müssen Sie manuell installieren dieses Zertifikats auf der Standardwebsite für jeden Verbundserver oder Verbundserverproxy in einer Serverfarm.  
  
Für Webserver installieren manuell Sie das Serverauthentifizierungszertifikat auf die entsprechende Website oder das virtuelle Verzeichnis, in dem sich Ihre verbundanwendung befindet.  
  
Wenn Sie eine Farm einrichten, müssen Sie für dieses Verfahren identisch – mit exakten denselben Einstellungen – auf allen Servern in der Farm.  
  
> [!NOTE]  
> AD FS-Verwaltungs-Snap-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>So importieren Sie ein Serverauthentifizierungszertifikat auf die Standardwebsite  
  
1.  Auf der **starten** geben**Internetinformationsdienste \(IIS\) Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Im mittleren Bereich doppelten Mausklick **Serverzertifikate**.  
  
4.  In der **Aktionen** Bereich, klicken Sie auf **Import**.  
  
5.  In der **Zertifikat importieren** Dialogfeld, klicken Sie auf die **...** Schaltfläche.  
  
6.  Navigieren Sie zum Speicherort der Pfx-Zertifikatdatei, markieren Sie ihn, und klicken Sie dann auf **öffnen**.  
  
7.  Geben Sie ein Kennwort für das Zertifikat, und klicken Sie dann auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Certificate Requirements for Federation Server Proxies](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

