---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8d0b4765304d8b302fc174c191af2c8e87a25304
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-by-using-ou-objects"></a>Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Organisationseinheiten (OUs) können zum Delegieren der Verwaltung von Objekten, z. B. Benutzer oder Computer innerhalb der Organisationseinheit an eine bestimmte Person oder Gruppe. Zum Delegieren von Verwaltung mithilfe einer Organisationseinheit platzieren Sie die Person oder Gruppe, dem Sie Administratorrechte in einer Gruppe delegieren, platzieren Sie die Gruppe von Objekten in einer Organisationseinheit gesteuert werden und dann delegieren Sie administrative Aufgaben für die Organisationseinheit, die dieser Gruppe zu.  
  
Active Directory-Domänendienste (AD DS) können Sie die administrativen Aufgaben zu steuern, die auf einer sehr detaillierte Ebene delegiert werden kann. Sie können beispielsweise eine Gruppe Vollzugriff auf alle Objekte in einer Organisationseinheit zuweisen. Zuweisen einer anderen Gruppe Rechte nur für das Erstellen, löschen und Verwalten von Benutzerkonten in der Organisationseinheit. und klicken Sie dann weisen eine dritte Gruppe das Recht nur Kennwörter von Benutzerkonten zurücksetzen. Sie können diese Berechtigungen vererbbare machen, sodass sie für alle Organisationseinheiten gelten, die in der ursprünglichen Organisationseinheit Unterstrukturen platziert werden.  
  
Standard-Organisationseinheiten und Container werden während der Installation von AD DS erstellt und die von Dienstadministratoren gesteuert. Es wird empfohlen, wenn Administratoren weiterhin diese Container steuern. Wenn Sie die Kontrolle über Objekte im Verzeichnis möchten, erstellen Sie zusätzliche Organisationseinheiten, und setzen Sie die Objekte in diesen Organisationseinheiten. Delegieren der Steuerung dieser OUs an die entsprechenden Datenadministratoren. Dadurch möglich, die Kontrolle über Objekte im Verzeichnis zu delegieren, ohne Änderung des standardmäßigen-Steuerelements übergeben, um die Dienstadministratoren.  
  
Der Gesamtstrukturbesitzer bestimmt die Ebene der Berechtigungen, die an einen Besitzer delegiert werden. Diese reichen von der Möglichkeit zum Erstellen und Bearbeiten von Objekten in einer Organisationseinheit nur ein Attribut mit einem einzelnen Typ des Objekts in der Organisationseinheit steuern zugelassen wird. Gewähren einem Benutzer die Möglichkeit, ein Objekt implizit in der Organisationseinheit erstellen erhält der betreffende Benutzer die Möglichkeit, alle Attribute für ein beliebiges Objekt zu bearbeiten, die der Benutzer erstellt. Darüber hinaus ist das Objekt, das erstellt wird, ist ein Container, hat der Benutzer implizit die Möglichkeit zum Erstellen und bearbeiten alle Objekte, die im Container platziert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


