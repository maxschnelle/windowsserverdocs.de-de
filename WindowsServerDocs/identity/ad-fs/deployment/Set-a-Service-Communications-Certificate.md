---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: Festlegen eines Dienstkommunikationszertifikats
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6549b120768bf01c43f38fc5252529e971043eaa
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956052"
---
# <a name="set-a-service-communications-certificate"></a>Festlegen eines Dienstkommunikationszertifikats


Verbund Server in Active Directory-Verbunddienste (AD FS) \( AD FS \) das Dienst Kommunikations Zertifikat zum Sichern des Webdienst-Datenverkehrs für die Secure Sockets Layer \( SSL- \) Kommunikation mit Webclients oder Verbund Server Proxys verwenden.

> [!NOTE]  
> Das Dienst Kommunikations Zertifikat ist nicht das gleiche wie ein SSL-Zertifikat. Um das AD FS SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden. Befolgen Sie die Anleitungen in diesem [Artikel](../operations/manage-ssl-certificates-ad-fs-wap.md).


Mithilfe des folgenden Verfahrens können Sie das Dienst Kommunikations Zertifikat mit dem Snap-in für die AD FS Verwaltung ändern \- .  

> [!NOTE]  
> Das Snap-in "AD FS-Verwaltung" \- bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .   

### <a name="to-set-a-service-communications-certificate"></a>So legen Sie ein Dienst Kommunikations Zertifikat fest  

1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  

2.  Doppelklicken Sie in der Konsolen Struktur auf \- **Dienst**, und klicken Sie dann auf **Zertifikate**.  

3.  Klicken Sie im Bereich **Aktionen** auf den Link **Service Communications-Zertifikat festlegen** .  

4.  Navigieren Sie im Dialogfeld **Dienst Kommunikations Zertifikat auswählen** zu der Zertifikat Datei, die Sie als Dienst Kommunikations Zertifikat festlegen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  

## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  

[Zertifikatanforderungen für Verbundserver](../design/certificate-requirements-for-federation-servers.md)  
