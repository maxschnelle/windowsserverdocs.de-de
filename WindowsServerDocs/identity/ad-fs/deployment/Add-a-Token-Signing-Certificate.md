---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: "Fügen Sie ein Token-Signing Certificate"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8a94e0724d6fd2a04e2fbfc22b3054b49d87f440
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-signing-certificate"></a>Fügen Sie ein Token-Signing Certificate

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Verbundserver in Active Directory Federation Services \(AD FS\) müssen Token\-Signierung Zertifikate hindert Angreifer daran ändern oder zu fälschen Sicherheitstoken versuchen, nicht autorisierten Zugriff auf verbundene Ressourcen. Alle Token\-Signaturzertifikat enthält kryptografische private und öffentliche Schlüssel, die verwendet werden, zum digitalen Signieren \ (über die private für schlüssel\) ein Sicherheitstoken. Später, nachdem diese Schlüssel von einem Partnerverbundserver empfangen werden, überprüfen sie die Echtheit \ (über den öffentlichen für schlüssel\) des verschlüsselten Sicherheitstokens.  
  
> [!CAUTION]  
> Mithilfe von Zertifikaten für das Signieren von Token\ sind entscheidend für die Stabilität des Verbunddiensts. Da der Verlust oder die ungeplante Entfernung von Zertifikaten für diesen Zweck konfigurierten Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Das Token\-Signaturzertifikat sollte an einen vertrauenswürdigen Stamm im Verbunddienst verketten. Das folgende Verfahren können das Signaturzertifikat Token\ AD FS-Verwaltungs-Snap-In aus einer Datei hinzufügen, die Sie exportiert haben.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-add-a-token-signing-certificate"></a>So fügen Sie ein Signaturzertifikat Token\ hinzu  
  
1.  Auf der **starten** geben**AD FS-Verwaltungs**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der Konsolenstruktur auf Variablenname **Service**, und klicken Sie dann auf **Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf die **hinzufügen Token\-Signaturzertifikat** Link.  
  
4.  In der **Zertifikatsdatei suchen** Dialogfeld Feld, navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, hinzufügen, wählen Sie die Zertifikatdatei, und klicken Sie dann auf **öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)  
  

