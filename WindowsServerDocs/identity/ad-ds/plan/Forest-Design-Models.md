---
ms.assetid: c7f49a65-c3eb-4383-99d3-756aa8c79fc0
title: Gesamtstruktur-Entwurfsmodelle
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b24eba7173a4878102ac7b7a84f7322425df8a52
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="forest-design-models"></a>Gesamtstruktur-Entwurfsmodelle

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können eines der folgenden drei Gesamtstruktur-Entwurfsmodelle in Ihrer Active Directory-Umgebung anwenden:  
  
-   Organisations-Gesamtstrukturmodell  
  
-   Ressourcen-Gesamtstrukturmodell  
  
-   Gesamtstrukturmodell für eingeschränkten Zugriff  
  
Es ist wahrscheinlich, dass Sie eine Kombination dieser Modelle verwenden, auf die Bedürfnisse aller anderen Gruppen in Ihrer Organisation benötigen.  
  
## <a name="organizational-forest-model"></a>Organisations-Gesamtstrukturmodell  
In der Organisations-Gesamtstrukturmodell sind in der Gesamtstruktur Benutzerkonten und Ressourcen enthalten und unabhängig verwaltet. Wenn die Gesamtstruktur konfiguriert ist, um Zugriff auf alle Personen außerhalb der Gesamtstruktur zu verhindern, kann die Organisationseinheit Gesamtstruktur Service Autonomie, Diensten oder Daten isoliert, Bereitstellen verwendet werden.  
  
Wenn Benutzer in einer Organisationseinheit Gesamtstruktur benötigen Zugriff auf Ressourcen in anderen Gesamtstrukturen aufweist (oder umgekehrt), können die Vertrauensstellungen zwischen einer Organisation Gesamtstruktur und den anderen Gesamtstrukturen hergestellt werden. Dadurch können Administratoren zum Gewähren von Zugriff auf Ressourcen in der anderen Gesamtstruktur. Die folgende Abbildung zeigt die Organisations-Gesamtstrukturmodell.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/b1ddb47e-78a5-49c7-bb21-d7421b7b84b8.gif)  
  
Alle Active Directory-Entwurf enthält mindestens eine Organisationseinheit Gesamtstruktur.  
  
## <a name="resource-forest-model"></a>Ressourcen-Gesamtstrukturmodell  
Im Ressourcen-Gesamtstrukturmodell wird eine separate Gesamtstruktur verwendet, um Ressourcen zu verwalten. Ressourcengesamtstrukturen enthalten keine Benutzerkonten als für die Verwaltung von Diensten und alternativen Zugriff auf die Ressourcen in dieser Gesamtstruktur erforderlich, die die Benutzerkonten in der Organisationseinheit Gesamtstruktur nicht verfügbar sind. Gesamtstruktur-Vertrauensstellungen sind so eingerichtet, dass Benutzer aus anderen Gesamtstrukturen die Ressourcen in der Gesamtstruktur zugreifen können. Die folgende Abbildung zeigt die Ressourcen-Gesamtstrukturmodell.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/c0b348a6-958c-4fc5-9035-e2d2a54d5573.gif)  
  
Ressourcengesamtstrukturen Dienstisolation, mit dem Schützen von Bereichen des Netzwerks, die einen Zustand hoher Verfügbarkeit beibehalten müssen. Wenn Ihr Unternehmen einem Fertigungsstandort, die weiterhin ausgeführt werden enthält, treten Probleme auf den Rest des Netzwerks muss, können Sie z. B. eine separate Ressourcen-Gesamtstruktur für die Produktion Gruppe erstellen.  
  
## <a name="restricted-access-forest-model"></a>Gesamtstrukturmodell für eingeschränkten Zugriff  
In der Gesamtstrukturmodell für eingeschränkten Zugriff ist eine separate Gesamtstruktur erstellt, um die Benutzerkonten und Daten, die vom Rest des Unternehmens isoliert werden müssen. Eingeschränkter Zugriff Gesamtstrukturen bieten datenisolierung in Situationen, in denen die Folgen der Gefährdung Projektdaten schwerwiegende sind. Die folgende Abbildung zeigt ein Gesamtstrukturmodell für eingeschränkten Zugriff.  
  
![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/e49cfc8c-a58a-4386-93bd-d4a6ee00f89c.gif)  
  
Benutzer aus anderen Gesamtstrukturen können nicht den Zugriff auf geschützte Daten gewährt werden, da keine Vertrauensstellung vorhanden ist. In diesem Modell können Benutzer ein Konto in einer Organisationseinheit Gesamtstruktur für den Zugriff auf allgemeine Ressourcen der Organisation und kein separates Benutzerkonto in der Gesamtstruktur mit eingeschränktem Zugriff für den Zugriff auf die geschützten Daten. Diese Benutzer müssen zwei Arbeitsstationen, die einer ist mit der Organisationseinheit Gesamtstruktur und der andere mit der Gesamtstruktur mit eingeschränktem Zugriff verbunden. Dies schützt vor die Möglichkeit, dass ein Dienstadministrator aus einer Gesamtstruktur auf einer Arbeitsstation in der eingeschränkten Gesamtstruktur zugreifen kann.  
  
In extremen Fällen kann die Gesamtstruktur mit eingeschränktem Zugriff auf einem separaten physischen Netzwerk verwaltet werden. Organisationen, die in einigen Fällen an geschützte funktionieren verwalten mit eingeschränktem Zugriff Gesamtstrukturen auf separate Netzwerke, die Sicherheit erfüllen.  
  


