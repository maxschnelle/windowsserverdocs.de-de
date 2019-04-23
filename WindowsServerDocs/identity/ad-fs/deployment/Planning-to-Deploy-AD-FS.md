---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: Planen der Bereitstellung von AD FS
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831691"
---
# <a name="planning-to-deploy-ad-fs"></a>Planen der Bereitstellung von AD FS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Nachdem Sie die Informationen zu Ihrer Umgebung gesammelt und eine Active Directory Federation Services erfordert \(AD FS\) Entwurf anhand der Anleitungen in den [AD FS-Entwurfshandbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx), Sie können beginnen, die Bereitstellung von AD FS-Entwurfs Ihrer Organisation zu planen. Mit dem fertigen Entwurf und die Informationen in diesem Thema können Sie die Aufgaben zum Bereitstellen von AD FS in Ihrer Organisation ermitteln.  
  
## <a name="reviewing-your-ad-fs-design"></a>Überprüfen Ihres AD FS-Entwurfs  
Wenn das Entwurfsteam, das der ursprünglichen AD FS erstellt Entwurf unterscheidet Ihrer Organisation das Bereitstellungsteam, die tatsächliche Implementierung bereitstellt, stellen Sie sicher, dass das Bereitstellungsteam den endgültigen Entwurf mit dem Entwurfsteam überprüft. Überprüfen Sie die folgenden Punkte in Bezug auf den Entwurf:  
  
-   Die Strategie des Entwurfsteams zur Festlegung der besten Topologie für die Platzierung der Verbundserver in Ihrem Unternehmens- oder Umkreisnetzwerk. Das Bereitstellungsteam kann in der Dokumentation zu diesem Thema finden Sie durch den folgenden Themen in der AD FS-Entwurfshandbuch überprüfen:  
  
    -   [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [Planen der Platzierung](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [Planen der Verbundserverproxy-Platzierung](https://technet.microsoft.com/library/dd807130.aspx)  
  
    Möglicherweise überlässt das Entwurfsteam das Thema der Platzierung des Verbundservers oder des Verbundserverproxys dem Bereitstellungsteam. Das Bereitstellungsteam ist dann für die Dokumentation und Implementierung der physischen Topologie der Server verantwortlich.  
  
-   Die geschäftlichen Gründe für die Festlegung Ihrer Organisation als Anspruchsanbieter, vertrauende Seite oder beides innerhalb des Umfangs des dokumentierten AD FS-Entwurfs. Stellen Sie sicher, dass die Mitglieder des Bereitstellungsteams die Gründe, warum AD FS bereitgestellt wird, und welche anderen Unternehmen oder Organisationen verstehen der verbundpartnerschaft beteiligt. Stellen Sie sicher, dass Mitglieder des Bereitstellungsteams auch die Einschränkungen verstehen, die für die anderen Unternehmen oder Organisationen vorhanden \(begrenzte Hardware, keine Extranetumgebung und So weiter\) , die möglicherweise den Geltungsbereich des Entwurfs in irgendeiner Form. Weitere Informationen zur Partnerorganisationen finden Sie unter [Planen Ihrer Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx).  
  
Nachdem sich das Entwurfs- und Bereitstellung verständigt haben auf dieser Probleme bei der Bereitstellung von AD FS-Entwurfs fortgesetzt werden kann. Weitere Informationen finden Sie unter [Implementieren des AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
