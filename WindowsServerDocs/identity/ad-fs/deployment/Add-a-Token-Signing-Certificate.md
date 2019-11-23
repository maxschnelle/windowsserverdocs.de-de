---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: Hinzufügen eines Tokensignaturzertifikats
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8b2246842dd70c06442faed995f6b883dbaf70a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360087"
---
# <a name="add-a-token-signing-certificate"></a>Hinzufügen eines Tokensignaturzertifikats


Verbund Server in Active Directory-Verbunddienste (AD FS) \(AD FS\) Token\-Signatur Zertifikate erfordern, um zu verhindern, dass Angreifer Sicherheits Token ändern oder fälschen, um nicht autorisierten Zugriff auf Verbund Ressourcen zu erlangen. Jedes Token\-Signaturzertifikat enthält kryptografische private Schlüssel und öffentliche Schlüssel, die verwendet werden, um \(mithilfe des privaten Schlüssels\) einem Sicherheits Token Digital zu signieren. Wenn diese Schlüssel später von einem Partner Verbund Server empfangen werden, überprüfen Sie die Authentizität \(mithilfe des öffentlichen Schlüssels\) des verschlüsselten Sicherheits Tokens.  
  
> [!CAUTION]  
> Zertifikate, die für die\-Signierung von Token verwendet werden, sind für die Stabilität des Verbunddienst entscheidend. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Das Token\-Signatur Zertifikats muss an einen vertrauenswürdigen Stamm im Verbunddienst verkettet werden. Sie können das folgende Verfahren verwenden, um das Token\-Signaturzertifikat zum Snap\-der AD FS Verwaltung aus einer exportierten Datei hinzuzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-add-a-token-signing-certificate"></a>So fügen Sie ein Token\-Signaturzertifikat hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppel\-klicken Sie in der Konsolen Struktur auf **Dienst**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Klicken Sie im Bereich **Aktionen** auf den Link **Token\-Signaturzertifikat hinzufügen** .  
  
4.  Navigieren Sie im Dialogfeld **nach Zertifikat Datei suchen** zu der Zertifikatsdatei, die Sie hinzufügen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  

