---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: da91a3e8c34c86f7fd03ca875b3800fdb6001750
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192118"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importieren eines Serverauthentifizierungszertifikats in die Standardwebsite

Nachdem Sie ein Serverauthentifizierungszertifikat von einer Zertifizierungsstelle erhalten \(Zertifizierungsstelle\), müssen Sie manuell installieren dieses Zertifikats auf der Standardwebsite für jeden Verbundserver oder Verbundserverproxy in einer Serverfarm.  
  
Für Webserver müssen Sie das Serverauthentifizierungszertifikat manuell auf der entsprechenden Website oder in dem virtuellen Verzeichnis installieren, im dem sich Ihre Verbundanwendung befindet.  
  
Wenn Sie eine Farm einrichten, achten Sie darauf, dass Sie dieses Verfahren auf jedem der Server in der Farm identisch – mit exakt denselben Einstellungen – durchführen.  
  
> [!NOTE]  
> Die AD FS-Verwaltungs-Snap\-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>So importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite  
  
1.  Auf der **starten** geben**Internet Information Services \(IIS\) Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Doppelklicken Sie im mittleren Bereich\-klicken Sie auf **Serverzertifikate**.  
  
4.  Klicken Sie im Bereich **Aktionen** auf **Importieren**.  
  
5.  In der **Zertifikatimport** Dialogfeld klicken Sie auf die **...** .  
  
6.  Navigieren Sie zum Speicherort der PFX-Zertifikatdatei, markieren Sie diese, und klicken Sie dann auf **Öffnen**.  
  
7.  Geben Sie das Kennwort für das Zertifikat ein, und klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Zertifikatanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

