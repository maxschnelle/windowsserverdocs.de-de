---
ms.assetid: c7f49a65-c3eb-4383-99d3-756aa8c79fc0
title: Gesamtstruktur-Entwurfsmodelle
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b0c6b42812592b5c9b0e763fcdad6b77a8776f0e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941074"
---
# <a name="forest-design-models"></a>Gesamtstruktur-Entwurfsmodelle

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können eines der folgenden drei Gesamtstruktur-Entwurfsmodelle in Ihrer Active Directory Umgebung anwenden:

-   Organisations Gesamtstruktur Modell

-   Ressourcen Gesamtstruktur Modell

-   Gesamtstruktur Modell mit eingeschränktem Zugriff

Es ist wahrscheinlich, dass Sie eine Kombination dieser Modelle verwenden müssen, um die Anforderungen aller verschiedenen Gruppen in Ihrer Organisation zu erfüllen.

## <a name="organizational-forest-model"></a>Organisations Gesamtstruktur Modell
Im Modell der Organisations Gesamtstruktur sind Benutzerkonten und Ressourcen in der Gesamtstruktur enthalten und werden unabhängig verwaltet. Die Organisations Gesamtstruktur kann verwendet werden, um Dienst Autonomie, Dienst Isolation oder Daten Isolation bereitzustellen, wenn die Gesamtstruktur so konfiguriert ist, dass der Zugriff auf Personen außerhalb der Gesamtstruktur verhindert wird.

Wenn Benutzer in einer Organisations Gesamtstruktur auf Ressourcen in anderen Gesamtstrukturen (oder umgekehrt) zugreifen müssen, können Vertrauens Stellungen zwischen einer Organisations Gesamtstruktur und den anderen Gesamtstrukturen eingerichtet werden. Dies ermöglicht es Administratoren, Zugriff auf Ressourcen in der anderen Gesamtstruktur zu gewähren. In der folgenden Abbildung wird das Modell der Organisations Gesamtstruktur dargestellt.

![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/b1ddb47e-78a5-49c7-bb21-d7421b7b84b8.gif)

Jeder Active Directory Entwurf umfasst mindestens eine Organisations Gesamtstruktur.

## <a name="resource-forest-model"></a>Ressourcen Gesamtstruktur Modell
Im Ressourcen Gesamtstruktur Modell wird eine separate Gesamtstruktur verwendet, um Ressourcen zu verwalten. Ressourcen Gesamtstrukturen enthalten keine Benutzerkonten, die nicht für die Dienst Verwaltung erforderlich sind, und diejenigen, die zum Bereitstellen eines alternativen Zugriffs auf die Ressourcen in dieser Gesamtstruktur erforderlich sind, wenn die Benutzerkonten in der Organisations Gesamtstruktur nicht verfügbar sind. Gesamtstruktur-Vertrauens Stellungen werden eingerichtet, sodass Benutzer aus anderen Gesamtstrukturen auf die in der Ressourcen Gesamtstruktur enthaltenen Ressourcen zugreifen können. Die folgende Abbildung zeigt das Ressourcen Gesamtstruktur Modell.

![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/c0b348a6-958c-4fc5-9035-e2d2a54d5573.gif)

Ressourcen Gesamtstrukturen bieten eine Dienst Isolation, die verwendet wird, um Bereiche des Netzwerks zu schützen, die den Status Hochverfügbarkeit aufrechterhalten müssen. Wenn Ihr Unternehmen z. b. eine Fertigungs Einrichtung umfasst, die weiterhin ausgeführt werden muss, wenn im restlichen Netzwerkprobleme auftreten, können Sie eine separate Ressourcen Gesamtstruktur für die Fertigungs Gruppe erstellen.

## <a name="restricted-access-forest-model"></a>Gesamtstruktur Modell mit eingeschränktem Zugriff
Im Gesamtstruktur Modell mit eingeschränktem Zugriff wird eine separate Gesamtstruktur erstellt, die Benutzerkonten und Daten enthält, die vom Rest der Organisation isoliert werden müssen. Eingeschränkte Zugriffs Strukturen bieten Daten Isolation in Situationen, in denen die Folgen der Gefährdung von Projektdaten schwerwiegend sind. Die folgende Abbildung zeigt ein Gesamtstruktur Modell mit eingeschränktem Zugriff.

![Gesamtstruktur-Entwurfsmodelle](media/Forest-Design-Models/e49cfc8c-a58a-4386-93bd-d4a6ee00f89c.gif)

Benutzern aus anderen Gesamtstrukturen kann kein Zugriff auf die eingeschränkten Daten gewährt werden, da keine Vertrauensstellung vorhanden ist. In diesem Modell verfügen Benutzer über ein Konto in einer Organisations Gesamtstruktur, das Zugriff auf allgemeine Organisations Ressourcen und ein separates Benutzerkonto in der Gesamtstruktur mit eingeschränktem Zugriff für den Zugriff auf die klassifizierten Daten hat. Diese Benutzer müssen über zwei separate Arbeitsstationen verfügen, von denen eine mit der Organisations Gesamtstruktur verbunden ist, und die andere mit der Gesamtstruktur mit eingeschränktem Zugriff. Dies schützt vor der Möglichkeit, dass ein Dienst Administrator aus einer Gesamtstruktur Zugriff auf eine Arbeitsstation in der eingeschränkten Gesamtstruktur erhält.

In den Extremfällen kann die Gesamtstruktur mit eingeschränktem Zugriff in einem separaten physischen Netzwerk verwaltet werden. Organisationen, die an klassifizierten Government-Projekten arbeiten, pflegen manchmal eingeschränkte Zugriffs Strukturen in separaten Netzwerken, um die Sicherheitsanforderungen zu erfüllen.



