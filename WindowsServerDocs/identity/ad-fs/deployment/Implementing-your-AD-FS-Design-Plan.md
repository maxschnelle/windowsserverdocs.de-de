---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: Implementieren des AD FS-Entwurfsplans
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6306b87dd06774bfde5ffc3ff98818d47d0c858f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408376"
---
# <a name="implementing-your-ad-fs-design-plan"></a>Implementieren des AD FS-Entwurfsplans

Die folgenden Umgebungsbedingungen und Anforderungen sind wichtige Faktoren bei der Implementierung Ihres Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Entwurfs Plans:  
  
-   **Unterstützte Partner:** In der Regel verwenden Sie AD FS, um mit Partnerorganisationen zu arbeiten. Legen Sie zum Einrichten des Identitäts Verbunds fest, welche Organisationen eine Partnerschaft bilden möchten. Nachdem eine Baseline AD FS Bereitstellung vorhanden ist, umfasst der Betrieb mit Partnern das Hinzufügen von Partnern, das Löschen von Partnern und das Aktualisieren von Partner Informationen. Änderungen an Partnerschaften können aus verschiedenen Gründen auftreten. Beispielsweise ist für Ihre AD FS-Bereitstellung möglicherweise ein partnerschaftliches Update erforderlich, wenn Ihr Partner das Unternehmen erheblich ändert, Ihr Unternehmen zu einer größeren Organisation oder einem Verbund von Organisationen gehört, oder wenn Ihre Organisation durch eine andere Geschäfts. In jedem Szenario, in dem Sie Identitäten aus mehreren Domänen bilden, müssen Sie die Domänen \(partner @ no__t-1 kennen, die Sie derzeit unterstützen, sowie alle zusätzlichen Domänen, die potenzielle Partner darstellen.  
  
-   **Unterstützte Anwendungs-und Dienst Typen:** Einige Anwendungen und Dienste benötigen Zugriff auf Betriebssystemressourcen, während andere Anwendungen "Ansprüche" unterstützen. Es ist wichtig, die Typen von Anwendungen und Diensten zu verstehen, die von AD FS unterstützt werden, damit Sie die Verwaltungsanforderungen formulieren können.  
  
-   **Logische und physische Architektur Diagramme oder Bereitstellungs Topologie:** Sie müssen Folgendes wissen:  
  
    -   Gibt an, ob Verbund Server in einer Gruppe von Servern oder auf einem einzelnen Server verwendet werden.  
  
    -   In Ihrem Netzwerk werden Firewalls und Proxys bereitgestellt.  
  
    -   Der Speicherort der Ressourcen und ob Benutzer innerhalb Ihrer Organisation, außerhalb der Organisation oder beides auf Ressourcen zugreifen.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>So implementieren Sie den AD FS Entwurf mithilfe dieses Handbuchs  
Der nächste Schritt bei der Implementierung des Entwurfs besteht darin zu bestimmen, in welcher Reihenfolge die einzelnen Bereitstellungs Aufgaben ausgeführt werden müssen. In diesem Handbuch werden Prüflisten verwendet, anhand derer Sie die verschiedenen Bereitstellungsaufgaben für Server und Anwendungen durchlaufen, die zum Implementieren des Entwurfsplans erforderlich sind. Übergeordnete und untergeordnete Prüf Listen werden bei Bedarf verwendet, um die Reihenfolge darzustellen, in der die Aufgaben für einen bestimmten AD FS Entwurf verarbeitet werden müssen.  
  
Verwenden Sie die folgenden übergeordneten Checklisten in diesem Abschnitt des Handbuchs, um sich mit den Bereitstellungs Aufgaben für die Implementierung des bevorzugten AD FS Entwurfs Ihrer Organisation vertraut zu machen:  
  
-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
