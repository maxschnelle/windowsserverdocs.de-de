---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: Hinzufügen eines Tokenverschlüsselungszertifikats
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: cf89972120f3f0effa3eb1cf0fee6d29dbc8ed4e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192481"
---
# <a name="add-a-token-decrypting-certificate"></a>Hinzufügen eines Tokenverschlüsselungszertifikats

Verbundserver verwenden ein Token\-Entschlüsselungszertifikat, wenn ein der vertrauenden Seite einen Verbundserver Token entschlüsseln muss, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungszertifikat festgelegt wurde. Active Directory-Verbunddienste \(AD FS\) verwendet das Secure Sockets Layer \(SSL\) Zertifikat für die Internet Information Services \(IIS\) als die Standard-Entschlüsselung das Zertifikat.  
  
> [!CAUTION]  
> Zertifikate für die Token\-entschlüsseln sind entscheidend, um die Stabilität des Verbunddiensts. Da es sich bei Verlust oder die ungeplante Entfernung von Zertifikaten für diesen Zweck konfiguriert den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Sie können wie folgt vor, die Token hinzuzufügen\-Entschlüsseln der Zertifikat der AD FS-Verwaltungs-Snap\-in aus einer Datei, die Sie exportiert haben.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>Um ein Token hinzuzufügen\-Entschlüsseln der Zertifikat  
  
1.  Auf der **starten** geben**AD FS-Verwaltung**, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppelklicken Sie in der Konsolenstruktur\-klicken Sie auf **Service**, und klicken Sie dann auf **Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf die **hinzufügen-Token\-Zertifikat entschlüsselt** Link.  
  
4.  In der **Zertifikatsdatei suchen** Dialogfeld navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, hinzufügen, wählen Sie die Zertifikatdatei aus, und klicken Sie dann auf **öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  

