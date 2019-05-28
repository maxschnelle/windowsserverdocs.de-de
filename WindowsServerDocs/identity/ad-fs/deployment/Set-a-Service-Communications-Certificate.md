---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: Festlegen eines Dienstkommunikationszertifikats
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 140e8e4204148dd8862385054554d7b8336856ec
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192011"
---
# <a name="set-a-service-communications-certificate"></a>Festlegen eines Dienstkommunikationszertifikats


Verbundserver in Active Directory Federation Services \(AD FS\) dienstkommunikationszertifikat zum Sichern von Web Services – Verkehr für Secure Sockets Layer verwenden \(SSL\) Kommunikation mit dem Web Clients oder Verbundserverproxys bestimmen.

> [!NOTE]  
> Dienstkommunikationszertifikat ist nicht identisch mit einem SSL-Zertifikat. Um das AD FS-SSL-Zertifikat zu ändern, müssen Sie Powershell verwenden. Befolgen Sie die Anweisungen in diesem [Artikel](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap).


Sie können das folgende Verfahren verwenden, so ändern Sie das Dienstzertifikat für die Kommunikation mit dem AD FS-Verwaltungs-Snap\-in.  

> [!NOTE]  
> Die AD FS-Verwaltungs-Snap\-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   

### <a name="to-set-a-service-communications-certificate"></a>Festlegen ein dienstkommunikationszertifikats  

1.  Auf der **starten** geben**AD FS-Verwaltung**, und drücken Sie dann die EINGABETASTE.  

2.  Doppelklicken Sie in der Konsolenstruktur\-klicken Sie auf **Service**, und klicken Sie dann auf **Zertifikate**.  

3.  In der **Aktionen** Bereich, klicken Sie auf die **Festlegen eines Dienstkommunikationszertifikats** Link.  

4.  In der **wählen ein dienstkommunikationszertifikats** Dialogfeld navigieren Sie zu der Zertifikatdatei, die Sie verwenden möchten, legen Sie als dienstkommunikationszertifikat, wählen Sie die Zertifikatdatei, und klicken Sie dann auf **Öffnen**.  

## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  

[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
