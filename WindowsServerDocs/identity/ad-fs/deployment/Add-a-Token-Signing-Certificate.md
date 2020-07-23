---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: Hinzufügen eines Tokensignaturzertifikats
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b2fc8d0d99530bf3700cac98e483d45f000af4a5
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966642"
---
# <a name="add-a-token-signing-certificate"></a>Hinzufügen eines Tokensignaturzertifikats


Für Verbund Server in Active Directory-Verbunddienste (AD FS) \( AD FS werden \) \- Tokensignaturzertifikate benötigt, um zu verhindern, dass Angreifer Sicherheits Token ändern oder fälschen, um nicht autorisierten Zugriff auf Verbund Ressourcen zu erlangen. Jedes \- Tokensignaturzertifikat enthält kryptografische private Schlüssel und öffentliche Schlüssel, die verwendet werden, um \( mithilfe des privaten Schlüssels \) ein Sicherheits Token Digital zu signieren. Später, nachdem diese Schlüssel von einem Partner Verbund Server empfangen wurden, überprüfen Sie die Authentizität \( mithilfe des öffentlichen Schlüssels \) des verschlüsselten Sicherheits Tokens.  
  
> [!CAUTION]  
> Zertifikate, die für \- die Tokensignierung verwendet werden, sind wichtig für die Stabilität der Verbunddienst. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Das \- Tokensignaturzertifikat sollte an einen vertrauenswürdigen Stamm im Verbunddienst verkettet werden. Mithilfe des folgenden Verfahrens können Sie das \- Tokensignaturzertifikat dem AD FS-Verwaltungs-Snap \- in aus einer exportierten Datei hinzufügen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .   
  
### <a name="to-add-a-token-signing-certificate"></a>So fügen Sie ein \- Tokensignaturzertifikat hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppelklicken Sie in der Konsolen Struktur auf \- **Dienst**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Klicken Sie im Bereich **Aktionen** auf den Link ** \- Tokensignaturzertifikat hinzufügen** .  
  
4.  Navigieren Sie im Dialogfeld **nach Zertifikat Datei suchen** zu der Zertifikatsdatei, die Sie hinzufügen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  
  
## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](../design/certificate-requirements-for-federation-servers.md)  
  
