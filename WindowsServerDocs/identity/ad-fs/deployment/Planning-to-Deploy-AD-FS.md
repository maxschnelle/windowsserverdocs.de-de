---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: Planen der Bereitstellung von AD FS
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2908595da34cc1a9721de6f830044ca65fe8fb25
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956062"
---
# <a name="planning-to-deploy-ad-fs"></a>Planen der Bereitstellung von AD FS


Nachdem Sie Informationen zu Ihrer Umgebung gesammelt haben und sich anhand \( \) der Anleitungen im [Leitfaden zum AD FS Design in Windows Server 2012](../design/ad-fs-design-guide-in-windows-server-2012.md)mit dem Entwurf einer Active Directory-Verbunddienste (AD FS) AD FS, können Sie mit der Planung der Bereitstellung des AD FS Entwurfs Ihrer Organisation beginnen. Mit dem abgeschlossenen Entwurf und den Informationen in diesem Thema können Sie ermitteln, welche Aufgaben zum Bereitstellen von AD FS in Ihrer Organisation durchgeführt werden müssen.  
  
## <a name="reviewing-your-ad-fs-design"></a>Überprüfen Ihres AD FS-Entwurfs  
Wenn das Entwurfs Team, das den ursprünglichen AD FS Entwurf für Ihre Organisation erstellt hat, nicht mit dem Bereitstellungs Team identisch ist, das die Bereitstellung implementiert, müssen Sie sicherstellen, dass das Bereitstellungs Team den endgültigen Entwurf mit dem Entwurfs Team überprüft. Überprüfen Sie die folgenden Punkte in Bezug auf den Entwurf:  
  
-   Die Strategie des Entwurfsteams zur Festlegung der besten Topologie für die Platzierung der Verbundserver in Ihrem Unternehmens- oder Umkreisnetzwerk. Das Bereitstellungs Team kann die Dokumentation zu diesem Thema lesen, indem Sie die folgenden Themen im AD FS Entwurfs Leit Faden betrachten:  
  
    -   [Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [Planen der Verbundserverplatzierung](../design/planning-federation-server-placement.md)  
  
    -   [Planen der Verbundserverproxy-Platzierung](../design/planning-federation-server-proxy-placement.md)  
  
    Möglicherweise überlässt das Entwurfsteam das Thema der Platzierung des Verbundservers oder des Verbundserverproxys dem Bereitstellungsteam. Das Bereitstellungsteam ist dann für die Dokumentation und Implementierung der physischen Topologie der Server verantwortlich.  
  
-   Die geschäftlichen Gründe für die Festlegung Ihrer Organisation als Anspruchsanbieter, vertrauende Seite oder beides innerhalb des Umfangs des dokumentierten AD FS-Entwurfs. Stellen Sie sicher, dass die Mitglieder des Bereitstellungs Teams die Gründe verstehen, warum AD FS bereitgestellt wird und welche anderen Unternehmen oder Organisationen an der Verbund Partnerschaft beteiligt sind. Stellen Sie sicher, dass die Mitglieder des Bereitstellungs Teams auch die Einschränkungen verstehen, die für andere Unternehmen oder Organisationen \( beschränkt sind Hardware, keine Extranetumgebung usw., die \) den Umfang des Entwurfs möglicherweise auf irgendeine Weise einschränken. Weitere Informationen zur Partnerorganisationen finden Sie unter [Planen Ihrer Bereitstellung](../design/planning-your-deployment.md).  
  
Nachdem die Entwurfs Teams und Bereitstellungs Teams diese Probleme zugestimmt haben, können Sie mit der Bereitstellung des AD FS Entwurfs fortfahren. Weitere Informationen finden Sie unter [Implementieren des AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
