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
ms.openlocfilehash: e703b9966fdd443c2799120464dcb92b2458428b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966782"
---
# <a name="add-a-token-decrypting-certificate"></a>Hinzufügen eines Tokenverschlüsselungszertifikats

Verbund Server verwenden ein \- tokenentschlüsselungszertifikat, wenn ein Verbund Server der vertrauenden Seite Token entschlüsseln muss, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungs Zertifikat festgelegt wurde. \(In Active Directory-Verbunddienste (AD FS) AD FS wird \) das Secure Sockets Layer \( SSL- \) Zertifikat für Internetinformationsdienste \( IIS \) als Standard Entschlüsselungs Zertifikat verwendet.  
  
> [!CAUTION]  
> Zertifikate, die für \- die tokenentschlüsselung verwendet werden, sind wichtig für die Stabilität der Verbunddienst. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.  
  
Mithilfe des folgenden Verfahrens können Sie das \- tokenentschlüsselungszertifikat dem AD FS-Verwaltungs-Snap \- in aus einer exportierten Datei hinzufügen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .   
  
### <a name="to-add-a-token-decrypting-certificate"></a>So fügen Sie ein \- tokenentschlüsselungszertifikat hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppelklicken Sie in der Konsolen Struktur auf \- **Dienst**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Klicken Sie im Bereich **Aktionen** auf den Link ** \- tokenentschlüsselungszertifikat hinzufügen** .  
  
4.  Navigieren Sie im Dialogfeld **nach Zertifikat Datei suchen** zu der Zertifikatsdatei, die Sie hinzufügen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  
  
## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Zertifikatanforderungen für Verbundserver](../design/certificate-requirements-for-federation-servers.md)  
  
