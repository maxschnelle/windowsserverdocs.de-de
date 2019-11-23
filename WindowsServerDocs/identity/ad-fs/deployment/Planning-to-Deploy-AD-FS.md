---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: Planen der Bereitstellung von AD FS
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ed2082706975d58a1535aaeb61e6c5283d23306a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359501"
---
# <a name="planning-to-deploy-ad-fs"></a>Planen der Bereitstellung von AD FS


Nachdem Sie Informationen zu Ihrer Umgebung gesammelt haben, und Sie sich für eine Active Directory-Verbunddienste (AD FS) \(AD FS\) Design entscheiden, indem Sie die Anleitungen im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx)befolgen, können Sie mit der Planung der Bereitstellung des AD FS Entwurfs Ihrer Organisation beginnen. Mit dem abgeschlossenen Entwurf und den Informationen in diesem Thema können Sie ermitteln, welche Aufgaben zum Bereitstellen von AD FS in Ihrer Organisation durchgeführt werden müssen.  
  
## <a name="reviewing-your-ad-fs-design"></a>Überprüfen Ihres AD FS-Entwurfs  
Wenn das Entwurfs Team, das den ursprünglichen AD FS Entwurf für Ihre Organisation erstellt hat, nicht mit dem Bereitstellungs Team identisch ist, das die Bereitstellung implementiert, müssen Sie sicherstellen, dass das Bereitstellungs Team den endgültigen Entwurf mit dem Entwurfs Team überprüft. Überprüfen Sie die folgenden Punkte in Bezug auf den Entwurf:  
  
-   Die Strategie des Entwurfsteams zur Festlegung der besten Topologie für die Platzierung der Verbundserver in Ihrem Unternehmens- oder Umkreisnetzwerk. Das Bereitstellungs Team kann die Dokumentation zu diesem Thema lesen, indem Sie die folgenden Themen im AD FS Entwurfs Leit Faden betrachten:  
  
    -   [Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [Planen der Verbundserverplatzierung](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [Planen der Verbundserverproxy-Platzierung](https://technet.microsoft.com/library/dd807130.aspx)  
  
    Möglicherweise überlässt das Entwurfsteam das Thema der Platzierung des Verbundservers oder des Verbundserverproxys dem Bereitstellungsteam. Das Bereitstellungsteam ist dann für die Dokumentation und Implementierung der physischen Topologie der Server verantwortlich.  
  
-   Die geschäftlichen Gründe für die Festlegung Ihrer Organisation als Anspruchsanbieter, vertrauende Seite oder beides innerhalb des Umfangs des dokumentierten AD FS-Entwurfs. Stellen Sie sicher, dass die Mitglieder des Bereitstellungs Teams die Gründe verstehen, warum AD FS bereitgestellt wird und welche anderen Unternehmen oder Organisationen an der Verbund Partnerschaft beteiligt sind. Stellen Sie sicher, dass die Mitglieder des Bereitstellungs Teams auch die Einschränkungen verstehen, die für die anderen Unternehmen oder Organisationen bestehen \(begrenzte Hardware, keine Extranetumgebung usw.\), die den Umfang des Entwurfs möglicherweise auf irgendeine Weise einschränken. Weitere Informationen zur Partnerorganisationen finden Sie unter [Planen Ihrer Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx).  
  
Nachdem die Entwurfs Teams und Bereitstellungs Teams diese Probleme zugestimmt haben, können Sie mit der Bereitstellung des AD FS Entwurfs fortfahren. Weitere Informationen finden Sie unter [Implementieren des AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
