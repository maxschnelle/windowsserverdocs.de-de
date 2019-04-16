---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: Festlegen eines Dienstkommunikationszertifikats
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0d630372d82cf1519da82397a9c90d6a28903ed0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="set-a-service-communications-certificate"></a>Festlegen eines Dienstkommunikationszertifikats

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Verbundserver in Active Directory Federation Services \(AD FS\) verwenden dienstkommunikationszertifikat Webdienstdatenverkehr für Secure Sockets Layer \(SSL\) Kommunikation mit Webclients oder Verbundserverproxies zu sichern. Dies ist das gleiche Zertifikat, das ein Verbundserver als SSL-Zertifikats in Internetinformationsdienste \(IIS\) verwendet.  
  
Das folgende Verfahren können um das Dienstzertifikat für die Kommunikation mit AD FS-Verwaltungs-Snap-In zu ändern.  
  
> [!NOTE]  
> AD FS-Verwaltungs-Snap-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-set-a-service-communications-certificate"></a>Festlegen ein dienstkommunikationszertifikats  
  
1.  Auf der **starten** geben**AD FS-Verwaltungs**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der Konsolenstruktur auf Variablenname **Service**, und klicken Sie dann auf **Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf die **Festlegen eines Dienstkommunikationszertifikats** Link.  
  
4.  In der **auswählen ein dienstkommunikationszertifikats** Dialogfeld Feld, navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, legen Sie als dienstkommunikationszertifikat, wählen die Zertifikatdatei und klicken Sie dann auf **öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)  
  

