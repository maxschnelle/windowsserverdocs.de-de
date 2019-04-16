---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: "Hinzufügen einer Tokenverschlüsselungszertifikats"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0eba51521e7ef88542bccf93d92d2e783d800b5e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-decrypting-certificate"></a>Hinzufügen einer Tokenverschlüsselungszertifikats

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Verbundserver verwenden ein Token\ Entschlüsselungszertifikat beim relying Party Verbundserver Token entschlüsseln muss, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungszertifikat festgelegt wurde. Active Directory-Verbunddienste \(AD FS\) wird das \(SSL\) Secure Sockets Layer-Zertifikat für Internetinformationsdienste \(IIS\) als das Standardzertifikat für die Entschlüsselung verwendet.  
  
> [!CAUTION]  
> Zertifikate, die zum Entschlüsseln von Token\ sind entscheidend für die Stabilität des Verbunddiensts. Da der Verlust oder die ungeplante Entfernung von Zertifikaten für diesen Zweck konfigurierten Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Das folgende Verfahren können das Zertifikat Token\ entschlüsseln AD FS-Verwaltungs-Snap-In aus einer Datei hinzufügen, die Sie exportiert haben.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>Hinzufügen ein Zertifikats Token\ entschlüsseln  
  
1.  Auf der **starten** geben**AD FS-Verwaltungs**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der Konsolenstruktur auf Variablenname **Service**, und klicken Sie dann auf **Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf die **Zertifikat hinzufügen Token\ entschlüsseln** Link.  
  
4.  In der **Zertifikatsdatei suchen** Dialogfeld Feld, navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, hinzufügen, wählen Sie die Zertifikatdatei, und klicken Sie dann auf **öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)  
  

