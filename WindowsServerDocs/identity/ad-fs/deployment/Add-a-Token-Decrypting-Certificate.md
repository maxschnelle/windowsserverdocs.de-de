---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: Hinzufügen eines Tokenverschlüsselungszertifikats
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 388414fff97705901bf52ee844b90508d62f8c83
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408451"
---
# <a name="add-a-token-decrypting-certificate"></a>Hinzufügen eines Tokenverschlüsselungszertifikats

Verbund Server verwenden ein Token @ no__t-0entschlüsselungs Zertifikat, wenn ein Verbund Server der vertrauenden Seite Token entschlüsseln muss, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungs Zertifikat festgelegt wurde. Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 verwendet das Secure Sockets Layer \(ssl @ no__t-3-Zertifikat für Internetinformationsdienste \(iis @ no__t-5 als Standard Entschlüsselungs Zertifikat.  
  
> [!CAUTION]  
> Die für das Token @ no__t-0decrypting verwendeten Zertifikate sind wichtig für die Stabilität der Verbunddienst. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Mithilfe des folgenden Verfahrens können Sie das Token "@ no__t-0decryprypting" dem AD FS-Verwaltungs-Snap @ no__t-1In aus einer exportierten Datei hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/swlink? LinkId\=83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>So fügen Sie ein Token @ no__t-0entschlüsselungszertifikat hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolen Struktur auf "Double @ no__t-0click **Service**", und klicken Sie dann auf **Zertifikate**.  
  
3.  Klicken Sie im Bereich **Aktionen** auf den Link **Token hinzufügen @ no__t-2decrypting Certificate** .  
  
4.  Navigieren Sie im Dialogfeld **nach Zertifikat Datei suchen** zu der Zertifikatsdatei, die Sie hinzufügen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  

