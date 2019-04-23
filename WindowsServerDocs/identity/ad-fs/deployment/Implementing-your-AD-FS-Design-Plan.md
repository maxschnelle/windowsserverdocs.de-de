---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: Implementieren des AD FS-Entwurfsplans
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 31c2e048c3c125d0ea60610b049501151d7aa823
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830781"
---
# <a name="implementing-your-ad-fs-design-plan"></a>Implementieren des AD FS-Entwurfsplans

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die folgenden umgebungsbedingungen und Anforderungen sind wichtige Faktoren für die Implementierung Ihrer Active Directory Federation Services \(AD FS\) Entwurfsplan:  
  
-   **Unterstützte-Partner:** Sie verwenden in der Regel von AD FS mit anderen Organisationen arbeiten. Bestimmen Sie zum Einrichten des Identitätsverbunds mit dem Sie eine Partnerschaft bilden möchten Organisationen. Nachdem eine Konfigurationsbasislinie AD FS-Bereitstellung vorhanden ist, umfasst das Arbeiten mit Partnern Partner hinzufügen und Löschen von Partnern Partnerinformationen aktualisieren. Änderungen an Partnerschaften können eine Vielzahl von Gründen auftreten. AD FS-Bereitstellung kann z. B. Partnerschaft Updates erfordern, wenn Ihr Partner die Geschäftsabläufe des Unternehmens erheblich ändert, Ihrer Organisation Teil einer größeren Organisation oder einen Verbund von Unternehmen ist oder Ihrer Organisation, von einem anderen abgerufen wird Unternehmen. In jedem Szenario, in dem Sie einen Verbund Identitäten aus mehreren Domänen erstellen, müssen Sie wissen, die Domänen \(Partner\) , die Sie unterstützen derzeit und alle weiteren Domänen, die potenzielle Partner darstellen.  
  
-   **Unterstützte Anwendungs- und Diensttypen:** Einige Anwendungen und Dienste benötigen Zugriff auf Ressourcen des Betriebssystems, während andere "als eine Ansprüche unterstützende." Es ist wichtig zu verstehen, die Arten von Anwendungen und Dienste, die AD FS unterstützt, sodass Sie Verwaltung Anforderungen zu formulieren können.  
  
-   **Logische und physische Architekturdiagramme oder Bereitstellungstopologie:** Sie müssen wissen:  
  
    -   Gibt an, ob Verbundserver in einer Menge von Fleisch von Servern oder auf einem einzelnen Server funktionieren.  
  
    -   Wird bereitgestellt, in denen Ihr Netzwerk, Firewalls und Proxys.  
  
    -   Der Speicherort der Ressourcen und gibt an, ob Benutzer auf Ressourcen in Ihrer Organisation, außerhalb der Organisation oder beides zugreifen.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>Gewusst wie: Implementieren Sie Ihre AD FS-Entwurfs anhand dieses Handbuchs  
Der nächste Schritt bei der Implementierung des Entwurfs ist, um zu bestimmen, in welcher Reihenfolge jede Bereitstellungsaufgabe durchgeführt werden muss. In diesem Handbuch werden Prüflisten verwendet, anhand derer Sie die verschiedenen Bereitstellungsaufgaben für Server und Anwendungen durchlaufen, die zum Implementieren des Entwurfsplans erforderlich sind. Über- und untergeordnete Prüflisten werden verwendet, nach Bedarf, um die Reihenfolge darzustellen, in der die Aufgaben für eine bestimmte AD FS-Entwurf verarbeitet werden muss.  
  
Verwenden Sie die folgende übergeordnete Prüfliste in diesem Abschnitt des Handbuchs mit den einzelnen Bereitstellungsaufgaben bei der Implementierung von bevorzugten AD FS-Entwurfs Ihrer Organisation vertraut:  
  
-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
