---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: Hinzufügen eines Tokenverschlüsselungszertifikats
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5714a41950b9c2f818ddc154a9af7a55fdb362d8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814964"
---
# <a name="add-a-token-decrypting-certificate"></a>Hinzufügen eines Tokenverschlüsselungszertifikats

Verbund Server verwenden ein Token\-Entschlüsselungs Zertifikats, wenn ein Verbund Server der vertrauenden Seite Token entschlüsseln muss, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungs Zertifikat festgelegt wurde. Active Directory-Verbunddienste (AD FS) \(AD FS\) verwendet das Secure Sockets Layer \(SSL-\) Zertifikat für Internetinformationsdienste \(IIS-\) als Standard Entschlüsselungs Zertifikat.  
  
> [!CAUTION]  
> Zertifikate, die für das Token\-Entschlüsselung verwendet werden, sind wichtig für die Stabilität des Verbunddienst. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Mithilfe des folgenden Verfahrens können Sie das Token\-Entschlüsselungszertifikat zum AD FS Verwaltungs-Snap\-in aus einer exportierten Datei hinzufügen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>So fügen Sie ein Token\-entschlüsselnden Zertifikats hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppel\-klicken Sie in der Konsolen Struktur auf **Dienst**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Klicken Sie im Bereich **Aktionen** auf den Link **Token\-Entschlüsselungs Zertifikat hinzufügen** .  
  
4.  Navigieren Sie im Dialogfeld **nach Zertifikat Datei suchen** zu der Zertifikatsdatei, die Sie hinzufügen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  

