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
ms.openlocfilehash: 6e0f9e6cca4fe915d3faed77fd5b5db543596d70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855303"
---
# <a name="set-a-service-communications-certificate"></a>Festlegen eines Dienstkommunikationszertifikats


Verbund Server in Active Directory-Verbunddienste (AD FS) \(AD FS\) das Dienst Kommunikations Zertifikat zum Schützen von Webdienst-Datenverkehr für Secure Sockets Layer \(SSL-\) Kommunikation mit Webclients oder Verbund Server Proxys verwenden.

> [!NOTE]  
> Das Dienst Kommunikations Zertifikat ist nicht das gleiche wie ein SSL-Zertifikat. Um das AD FS SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden. Befolgen Sie die Anleitungen in diesem [Artikel](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap).


Mithilfe des folgenden Verfahrens können Sie das Dienst Kommunikations Zertifikat mit dem AD FS-Verwaltungs-Snap\-in ändern.  

> [!NOTE]  
> Der AD FS-Verwaltungs-Snap\-in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   

### <a name="to-set-a-service-communications-certificate"></a>So legen Sie ein Dienst Kommunikations Zertifikat fest  

1.  Geben Sie auf dem **Start** Bildschirm**AD FS Management**ein, und drücken Sie dann die EINGABETASTE.  

2.  Doppel\-klicken Sie in der Konsolen Struktur auf **Dienst**, und klicken Sie dann auf **Zertifikate**.  

3.  Klicken Sie im Bereich **Aktionen** auf den Link **Service Communications-Zertifikat festlegen** .  

4.  Navigieren Sie im Dialogfeld **Dienst Kommunikations Zertifikat auswählen** zu der Zertifikat Datei, die Sie als Dienst Kommunikations Zertifikat festlegen möchten, wählen Sie die Zertifikat Datei aus, und klicken Sie dann auf **Öffnen**.  

## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  

[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
