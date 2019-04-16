---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: Implementieren des AD FS-Entwurfsplans
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 31c2e048c3c125d0ea60610b049501151d7aa823
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="implementing-your-ad-fs-design-plan"></a>Implementieren des AD FS-Entwurfsplans

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die folgenden Umweltbedingungen und Anforderungen sind wichtige Faktoren bei der Implementierung von Ihrem Active Directory Federation Services \(AD FS\) Entwurfsplan:  
  
-   **Partner unterstützt:** in der Regel mit der AD FS Organisationen zusammenarbeiten. Bestimmen Sie, um Identitätsverbund einzurichten, die Organisationen, die mit denen Sie eine Partnerschaft bilden möchten. Nach eine Basislinie AD FS-Bereitstellung vorhanden ist, umfasst das Arbeiten mit Partnern Partner hinzufügen, Löschen von Partnern und Partnerinformationen aktualisieren. Änderungen an Partnerschaften können aus verschiedenen Gründen auftreten. Beispielsweise kann die AD FS-Bereitstellung Partnerschaft Updates erfordern, wenn Ihr Partner seiner Tätigkeit erheblich ändert, Ihrer Organisation wird ein Teil einer größeren Organisation oder ein Verbund Organisationen oder Ihrer Organisation wird durch ein anderes Unternehmen erworben hat. In jedem Szenario, in dem Sie die Identitäten aus mehreren Domänen verbinden, müssen Sie wissen, dass die \(partners\) Domänen, die Sie derzeit unterstützen und alle zusätzlichen Domänen, die potenzielle Partner darstellen.  
  
-   **Unterstützte Anwendung und Diensttypen:** einige Anwendungen und Dienste erfordern den Zugriff auf Ressourcen des Betriebssystems, während andere "Ansprüche kennen." sind Es ist wichtig zu wissen, welche Anwendungen und Dienste, die AD FS unterstützt, sodass Sie Verwaltungsaufwand formulieren können.  
  
-   **Logische und physische Architektur Diagramme oder Bereitstellungstopologie:** müssen Sie wissen:  
  
    -   Gibt an, ob Verbundserver in einer Reihe von Zuchtwild Servern oder auf einem einzelnen Server funktionieren.  
  
    -   In denen Ihr Netzwerk Firewalls und Proxys bereitgestellt wird.  
  
    -   Der Speicherort der Ressourcen und gibt an, ob Benutzer auf Ressourcen in Ihrer Organisation, außerhalb der Organisation oder beides zugreifen.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>Implementieren Sie Ihre AD FS-Entwurfs anhand dieses Handbuchs  
Der nächste Schritt bei der Implementierung des Entwurfs ist, um zu bestimmen, in welcher Reihenfolge die einzelnen Aufgaben für die Bereitstellung ausgeführt werden muss. Dieses Handbuch werden Prüflisten verwendet, können Sie die verschiedenen Bereitstellungsaufgaben für Server und Anwendungen durchlaufen, die zum Implementieren des entwurfsplans erforderlich sind. Übergeordnete und untergeordnete Prüflisten werden verwendet, nach Bedarf, um die Reihenfolge darzustellen, in der die Aufgaben für eine bestimmte AD FS Design verarbeitet werden muss.  
  
Verwenden Sie die folgenden übergeordneten Prüflisten in diesem Abschnitt des Handbuchs, mit der Bereitstellungsaufgaben für die Implementierung der bevorzugten AD FS-Entwurfs Ihrer Organisation vertraut:  
  
-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
