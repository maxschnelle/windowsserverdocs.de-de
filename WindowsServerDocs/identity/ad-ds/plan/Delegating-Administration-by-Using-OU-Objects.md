---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4a097f42a0de7a28d93637e0c5df39e04fe50532
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947699"
---
# <a name="delegating-administration-by-using-ou-objects"></a>Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können Organisationseinheiten (OUs) verwenden, um die Verwaltung von Objekten (z. b. Benutzer oder Computer) innerhalb der OE an eine bestimmte Person oder Gruppe zu delegieren. Um die Verwaltung mithilfe einer Organisationseinheit zu delegieren, platzieren Sie die Einzelperson oder die Gruppe, der Sie Administratorrechte delegieren, in eine Gruppe, platzieren Sie den Satz der zu kontrollierenden Objekte in eine Organisationseinheit, und delegieren Sie dann administrative Aufgaben für die Organisationseinheit an diese Gruppe.

Mit Active Directory Domain Services (AD DS) können Sie die Verwaltungsaufgaben steuern, die auf einer sehr detaillierten Ebene delegiert werden können. Beispielsweise können Sie einer Gruppe eine vollständige Kontrolle über alle Objekte in einer Organisationseinheit zuweisen. Weisen Sie einer anderen Gruppe die Rechte nur zum Erstellen, löschen und Verwalten von Benutzerkonten in der Organisationseinheit zu. und weisen Sie dann eine dritte Gruppe mit der rechten Seite zu, um Kenn Wörter für Benutzerkonten zurückzusetzen. Sie können diese Berechtigungen vererbbar machen, sodass Sie für alle Organisationseinheiten gelten, die in den Teil Strukturen der ursprünglichen Organisationseinheit platziert werden.

Standard-OUs und-Container werden während der Installation von AD DS erstellt und von Dienst Administratoren gesteuert. Es ist am besten, wenn Dienst Administratoren diese Container weiterhin kontrollieren. Wenn Sie die Steuerung von Objekten im Verzeichnis delegieren müssen, erstellen Sie zusätzliche Organisationseinheiten, und platzieren Sie die Objekte in diesen Organisationseinheiten. Delegieren Sie die Kontrolle über diese Organisationseinheiten an die entsprechenden Daten Administratoren. Dadurch kann die Steuerung von Objekten im Verzeichnis delegiert werden, ohne das Standard Steuerelement zu ändern, das für die Dienst Administratoren angegeben wird.

Der Gesamtstruktur Besitzer bestimmt die Autoritäts Ebene, die an einen OE-Besitzer delegiert wird. Dies kann von der Fähigkeit zum Erstellen und Bearbeiten von Objekten innerhalb der OE reichen, sodass nur ein einzelnes Attribut eines einzelnen Objekt Typs in der OE gesteuert werden kann. Wenn ein Benutzer die Möglichkeit erhält, ein Objekt in der Organisationseinheit zu erstellen, erhält dieser Benutzer implizit die Möglichkeit, jedes beliebige Attribut eines beliebigen Objekts zu bearbeiten, das vom Benutzer erstellt wird. Wenn das Objekt, das erstellt wird, ein Container ist, kann der Benutzer außerdem implizit Objekte erstellen und bearbeiten, die im Container platziert werden.

## <a name="in-this-section"></a>In diesem Abschnitt

-   [Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)

-   [Delegieren der Verwaltung von Konto- und Ressourcenorganisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)



