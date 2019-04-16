---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: Planen der Bereitstellung von AD FS
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-to-deploy-ad-fs"></a>Planen der Bereitstellung von AD FS

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Nachdem Sie die Informationen zu Ihrer Umgebung sammeln und Sie auf einem Active Directory Federation Services \(AD FS\) Entwurf unter Beachtung der Richtlinien in der [AD FS-Entwurfshandbuch in Windows Server2012](https://technet.microsoft.com/library/dd807036.aspx), Sie können mit der Planung der Bereitstellung von AD FS-Entwurfs Ihrer Organisation beginnen. Mit dem fertigen Entwurf und die Informationen in diesem Thema können Sie die Aufgaben zum Bereitstellen von AD FS in Ihrer Organisation ermitteln.  
  
## <a name="reviewing-your-ad-fs-design"></a>Überprüfen Ihre AD FS-Entwurfs  
Wenn das Entwurfsteam, das die ursprüngliche AD FS erstellt für entwerfen unterscheidet Ihrer Organisation das Bereitstellungsteam, die tatsächlich Implementieren der Bereitstellung, stellen Sie sicher, dass das Bereitstellungsteam den endgültigen Entwurf mit dem Entwurfsteam überprüft. Überprüfen Sie die folgenden Punkte in Bezug auf den Entwurf:  
  
-   Das Entwurfsteam Strategie zum Ermitteln der physischen Topologie für die Platzierung der Verbundserver in Ihrem Unternehmens- oder Umkreisnetzwerk. Das Bereitstellungsteam kann in der Dokumentation zu diesem Thema finden Sie die folgenden Themen im AD FS-Entwurfshandbuch:  
  
    -   [Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [Planen der Platzierung des Verbundservers](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [Planen der Verbundserverproxy-Platzierung](https://technet.microsoft.com/library/dd807130.aspx)  
  
    Es ist möglich, dass das Entwurfsteam den Betreff der Verbundserver oder Verbundserverproxy-Platzierung dem Bereitstellungsteam überlässt. Das Bereitstellungsteam ist dann für das Dokumentieren und Implementieren der physischen Topologie der Server verantwortlich.  
  
-   Die geschäftlichen Gründe für die Festlegung Ihrer Organisation als Anspruchsanbieter, vertrauende Seite oder beides innerhalb des Bereichs des dokumentierten AD FS-Entwurfs. Stellen Sie sicher, dass die Mitglieder des Bereitstellungsteams die Gründe, warum AD FS bereitgestellt wird, und welche anderen Unternehmen oder Organisationen verstehen an der verbundpartnerschaft beteiligt. Stellen Sie sicher, dass die Mitglieder des Bereitstellungsteams auch die Einschränkungen verstehen, die für die anderen Unternehmen oder Organisationen existieren \ (begrenzte Hardware, keine Extranetumgebung und so Forth\), die möglicherweise den Geltungsbereich des Entwurfs in irgendeiner Form. Weitere Informationen zur Partnerorganisationen finden Sie unter [Planen der Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx).  
  
Nachdem sich das Entwurfs- und Bereitstellungsteam auf einigen dieser Probleme mit der Bereitstellung des AD FS-Entwurfs fortgesetzt werden kann. Weitere Informationen finden Sie unter [Implementieren Ihrer AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
