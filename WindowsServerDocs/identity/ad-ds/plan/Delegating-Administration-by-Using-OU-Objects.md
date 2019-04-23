---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 39c4278270e4ab4fba9ff1062d2aa043d203a74b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886941"
---
# <a name="delegating-administration-by-using-ou-objects"></a>Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Organisationseinheiten (OUs) können zum Delegieren der Verwaltung von Objekten, z. B. Benutzer oder Computer, in der Organisationseinheit an eine bestimmte Person oder Gruppe. Um die Verwaltung delegieren, indem Sie mit einer Organisationseinheit, platzieren Sie die Person oder Gruppe, die auf die Sie über Administratorrechte in eine Gruppe delegieren, platzieren Sie den Satz von Objekten in einer Organisationseinheit gesteuert werden und anschließend Delegieren von Verwaltungsaufgaben für die Organisationseinheit, die dieser Gruppe.  
  
Active Directory-Domänendienste (AD DS) können Sie die administrativen Aufgaben zu steuern, die auf einer sehr detaillierte Ebene delegiert werden können. Beispielsweise können Sie einer Gruppe haben Vollzugriff auf alle Objekte in einer Organisationseinheit zuweisen. Zuweisen von einer anderen Gruppe die Berechtigungen nur erstellen, löschen und Verwalten von Benutzerkonten in der Organisationseinheit; und dann Zuweisen einer dritten Gruppe das Recht nur für das Zurücksetzen der Kennwörter von Benutzerkonten. Sie können diese Berechtigungen vererbbar vornehmen, sodass sie alle Organisationseinheiten gelten, die in Unterstrukturen von der ursprünglichen Organisationseinheit platziert werden.  
  
Standardorganisationseinheiten und Container werden während der Installation von AD DS erstellt und die von den Dienstadministratoren gesteuert. Es wird empfohlen, wenn Dienstadministratoren fortfahren, um diese Container zu steuern. Wenn Sie die Kontrolle über die Objekte im Verzeichnis zu delegieren möchten, erstellen Sie zusätzliche Organisationseinheiten, und platzieren Sie die Objekte in diesen Organisationseinheiten. Delegieren Sie Kontrolle über diesen Organisationseinheiten, an die Administratoren der entsprechenden Daten. Dies ermöglicht es, Kontrolle über die Objekte im Verzeichnis ohne das standardmäßige Steuerelement übergeben, um die Dienstadministratoren zu delegieren.  
  
Der Gesamtstrukturbesitzer bestimmt die Autorität, die an einen Besitzer delegiert werden kann. Diese reichen von der Möglichkeit zum Erstellen und Bearbeiten von Objekten in der Organisationseinheit nur zugelassen wird, um ein einzelnes Attribut eines einzelnen Typs des Objekts in der Organisationseinheit zu steuern. Gewähren einem Benutzer die Möglichkeit zum Erstellen eines Objekts in der Organisationseinheit implizit gewährt, Benutzer können Sie alle Attribute eines Objekts zu ändern, die der Benutzer erstellt. Darüber hinaus, wenn das Objekt, das erstellt wird, ist ein Container ist, hat der Benutzer implizit die Möglichkeit zum Erstellen und bearbeiten alle Objekte, die in den Container eingefügt werden.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [Delegieren der Verwaltung der Konto-OEs und Ressourcenorganisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


