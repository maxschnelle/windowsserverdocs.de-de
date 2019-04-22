---
ms.assetid: c7f49a65-c3eb-4383-99d3-756aa8c79fc0
title: Gesamtstruktur-Entwurfsmodelle
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aca59a31f75628b311a92bd842d93ee91408dc4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819791"
---
# <a name="forest-design-models"></a>Gesamtstruktur-Entwurfsmodelle

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können eines der folgenden drei Gesamtstruktur-Entwurfsmodelle in Ihrer Active Directory-Umgebung anwenden:  
  
-   Organisations-Gesamtstrukturmodell  
  
-   Ressourcen-Gesamtstrukturmodell  
  
-   Gesamtstrukturmodell für eingeschränkten Zugriff  
  
Es ist wahrscheinlich, dass Sie eine Kombination aus diesen Modellen verwenden, um die Anforderungen aller anderen Gruppen in Ihrer Organisation erfüllen müssen.  
  
## <a name="organizational-forest-model"></a>Organisations-Gesamtstrukturmodell  
In der Organisations-Gesamtstrukturmodell sind in der Gesamtstruktur Benutzerkonten und Ressourcen enthalten und unabhängig voneinander verwaltet. Wenn die Gesamtstruktur für das Verhindern des Zugriffs auf Personen außerhalb der Gesamtstruktur konfiguriert ist, kann der Organisationsgesamtstruktur die Autonomie eines Dienstes, Isolation von Diensten oder die Datenisolation, verwendet werden.  
  
Wenn Benutzer in einer Organisation Gesamtstruktur benötigen Zugriff auf Ressourcen in anderen Gesamtstrukturen aufweist (oder umgekehrt), können die Vertrauensstellungen zwischen einer Organisation Gesamtstruktur und den anderen Gesamtstrukturen eingerichtet werden. Dies ermöglicht es Administratoren gewähren Zugriff auf Ressourcen in der anderen Gesamtstruktur. Die folgende Abbildung zeigt die Organisations-Gesamtstrukturmodell.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/b1ddb47e-78a5-49c7-bb21-d7421b7b84b8.gif)  
  
Alle Active Directory-Entwurf enthält mindestens ein Organisationsgesamtstruktur.  
  
## <a name="resource-forest-model"></a>Ressourcen-Gesamtstrukturmodell  
Im Ressourcen-Gesamtstrukturmodell wird eine separate Gesamtstruktur verwendet, um Ressourcen zu verwalten. Ressourcen-Gesamtstrukturen enthalten keine Benutzerkonten als für die Verwaltung von Diensten und alternativen Zugriff auf die Ressourcen in dieser Gesamtstruktur erforderlich sind, wenn die Benutzerkonten in der Organisationsgesamtstruktur nicht mehr verfügbar sind. Gesamtstruktur-Vertrauensstellungen sind so eingerichtet, dass Benutzer aus anderen Gesamtstrukturen, die in der Ressourcengesamtstruktur enthaltenen Ressourcen zugreifen können. Die folgende Abbildung zeigt das Ressourcen-Forest-Modell.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/c0b348a6-958c-4fc5-9035-e2d2a54d5573.gif)  
  
Eine Ressourcengesamtstruktur bieten Isolation von Diensten, mit dem Schützen von Bereichen des Netzwerks, die einen Zustand der hochverfügbarkeit verwalten müssen. Wenn Ihr Unternehmen eine Produktionsstätte, die weiterhin ausgeführt enthält, wenn Probleme, auf den Rest des Netzwerks vorliegen muss, können Sie z. B. eine separate Ressource-Gesamtstruktur für die Gruppe "Produktion" erstellen.  
  
## <a name="restricted-access-forest-model"></a>Gesamtstrukturmodell für eingeschränkten Zugriff  
In der Gesamtstrukturmodell für eingeschränkten Zugriff wird eine separate Gesamtstruktur erstellt, Benutzerkonten und Daten, die vom Rest des Unternehmens isoliert werden müssen. Eingeschränkter Zugriff Gesamtstrukturen bieten die Datenisolation in Situationen, in denen die Folgen einer Gefährdung Projektdaten schwerwiegend sind. Die folgende Abbildung zeigt ein Gesamtstrukturmodell für eingeschränkten Zugriff.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/e49cfc8c-a58a-4386-93bd-d4a6ee00f89c.gif)  
  
Benutzer aus anderen Gesamtstrukturen können nicht zum Zugriff auf geschützte Daten gewährt werden, da keine Vertrauensstellung vorhanden ist. In diesem Modell haben Benutzer ein Konto in einer Organisation Gesamtstruktur für den Zugriff auf allgemeine Ressourcen der Organisation und ein separates Benutzerkonto in der Gesamtstruktur mit eingeschränktem Zugriff für den Zugriff auf die klassifizierten Daten an. Diese Benutzer müssen über zwei separate Arbeitsstationen, einer ist mit der Organisationsgesamtstruktur verfügen, und der andere mit der Gesamtstruktur mit eingeschränktem Zugriff verbunden. Dies schützt gegen die Möglichkeit, ein Dienstadministrator aus mehrere Gesamtstrukturen einer Arbeitsstation in der eingeschränkten Gesamtstruktur zugreifen kann.  
  
In extremen Fällen kann die Gesamtstruktur mit eingeschränktem Zugriff auf einem separaten physischen Netzwerk verwaltet werden. Organisationen, die an Projekten für klassifizierte Government funktioniert in einigen Fällen behalten die eingeschränkten Zugriff Gesamtstrukturen in getrennten Netzwerken um sicherheitsanforderungen zu erfüllen.  
  


