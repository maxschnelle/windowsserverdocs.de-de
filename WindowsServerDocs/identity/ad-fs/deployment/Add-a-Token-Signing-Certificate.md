---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: Hinzufügen eines Tokensignaturzertifikats
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ac9f9b95ad6226a8e3b7012e317899f1d48c60c9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192467"
---
# <a name="add-a-token-signing-certificate"></a>Hinzufügen eines Tokensignaturzertifikats


Verbundserver in Active Directory Federation Services \(AD FS\) erfordern Token\-Signaturzertifikate zum hindert Angreifer daran, ändern oder zu fälschen Sicherheitstoken zu versuchen, nicht autorisierten Zugriff zu erhalten. mit verbundenen Ressourcen. Jedes Token\-Signaturzertifikat enthält, kryptografische private und öffentliche Schlüssel, die verwendet werden, zum digitalen Signieren von \(mit dem privaten Schlüssel\) ein Sicherheitstoken. Später, nachdem diese Schlüssel von einem Partnerverbundserver empfangen werden, überprüfen sie die Echtheit \(mit dem öffentlichen Schlüssel\) des verschlüsselten Sicherheitstokens.  
  
> [!CAUTION]  
> Zertifikate für die Token\-Signieren sind entscheidend, um die Stabilität des Verbunddiensts. Da es sich bei Verlust oder die ungeplante Entfernung von Zertifikaten für diesen Zweck konfiguriert den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Das Token\-Signaturzertifikat an einen vertrauenswürdigen Stamm im Verbunddienst verketten sollten. Sie können wie folgt vor, die Token hinzuzufügen\-Signaturzertifikat auf dem AD FS-Verwaltungs-Snap\-in aus einer Datei, die Sie exportiert haben.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-token-signing-certificate"></a>Um ein Token hinzuzufügen\-Signaturzertifikat  
  
1.  Auf der **starten** geben**AD FS-Verwaltung**, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppelklicken Sie in der Konsolenstruktur\-klicken Sie auf **Service**, und klicken Sie dann auf **Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf die **hinzufügen-Token\-Signing Certificate** Link.  
  
4.  In der **Zertifikatsdatei suchen** Dialogfeld navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, hinzufügen, wählen Sie die Zertifikatdatei aus, und klicken Sie dann auf **öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  

