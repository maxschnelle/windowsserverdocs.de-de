---
ms.assetid: da7b6dcf-53ec-4394-88c0-c087d92f3893
title: "Dienstadministrator Autoritätsumfang"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ba682067b9c7a7b4bf583482abe6470b60b25450
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="service-administrator-scope-of-authority"></a>Dienstadministrator Autoritätsumfang

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie Active Directory-Gesamtstruktur teilnehmen möchten, müssen Sie der Gesamtstrukturbesitzer und die Dienstadministratoren vertrauen. Die Gesamtstrukturbesitzer sind verantwortlich für das auswählen und Verwalten der Dienstadministratoren; Wenn Sie einen Gesamtstrukturbesitzer vertrauen, vertrauen Sie daher auch die Dienstadministratoren, die der Gesamtstrukturbesitzer verwaltet. Diese Dienstadministratoren haben Zugriff auf alle Ressourcen in der Gesamtstruktur. Vor der Entscheidung zur Teilnahme an einer Gesamtstruktur ist es wichtig zu wissen, dass der Gesamtstrukturbesitzer und die Dienstadministratoren vollständigen Zugriff auf Ihre Daten. Dieser Zugriff verhindern nicht.  
  
Aller Dienstadministratoren in einer Gesamtstruktur über Vollzugriff auf alle Daten und Dienste auf allen Computern in der Gesamtstruktur verfügen. Administratoren haben die Möglichkeit, die folgenden Schritteausführen:  
  
-   Beheben von Fehlern auf Zugriffssteuerungslisten (ACLs) von Objekten. Dies ermöglicht dem Dienstadministrator, lesen, ändern oder Löschen von Objekten unabhängig von der ACLs, die für diese Objekte festgelegt werden.  
  
-   Ändern Sie die Systemsoftware auf einem Domänencontroller, normale Sicherheitskontrollen zu umgehen. Dies ermöglicht dem Dienstadministrator, anzeigen oder bearbeiten ein Objekt in der Domäne, unabhängig von der ACL für das Objekt.  
  
-   Verwenden Sie die Sicherheitsrichtlinie für eingeschränkte Gruppen, um alle Benutzer oder Gruppe administrativen Zugriff auf einem beliebigen Computer in der Domäne zu gewähren. Auf diese Weise können Dienstadministratoren Steuerelement von einem beliebigen Computer in der Domäne ungeachtet dessen die Absichten der Besitzer des Computers erhalten.  
  
-   Zurücksetzen von Kennwörtern oder Gruppenmitgliedschaft für Benutzer ändern.  
  
-   Erhalten Sie Zugriff auf andere Domänen in der Gesamtstruktur durch Ändern der Systemsoftware auf einem Domänencontroller. Dienstadministratoren können Einfluss auf die Ausführung einer beliebigen Domäne in der Gesamtstruktur, anzeigen oder Bearbeiten von Konfigurationsdaten für die Gesamtstruktur, anzeigen oder Bearbeiten von Daten in einer beliebigen Domäne gespeichert und Daten anzeigen oder Bearbeiten auf einem beliebigen Computer in der Gesamtstruktur gespeichert.  
  
Aus diesem Grund Gruppen, die Speichern von Daten in Organisationseinheiten (OUs) in der Gesamtstruktur und Join-Computern in einer Gesamtstruktur die Dienstadministratoren vertrauen müssen. Für eine Gruppe zu eine Gesamtstruktur hinzufügen müssen sie auswählen aller Dienstadministratoren in der Gesamtstruktur vertrauen. Dies umfasst, um sicherzustellen, dass:  
  
-   Der Gesamtstrukturbesitzer kann als vertrauenswürdig festgelegt sein, um in das Interesse der Gruppe zu fungieren und keinen Grund für die Gruppe in böswilliger Absicht verwendet.  
  
-   Der Gesamtstrukturbesitzer beschränkt entsprechend den physischen Zugriff auf Domänencontroller. Domänencontroller in einer Gesamtstruktur nicht möglich, voneinander isoliert. Es ist möglich, dass ein Angreifer mit physischem Zugriff auf einen einzelnen Domänencontroller offline vornehmen der Verzeichnisdatenbank und auf diese Weise, beeinträchtigen die Ausführung von einer beliebigen Domäne in der Gesamtstruktur, anzeigen oder Bearbeiten von Daten, die an einer beliebigen Stelle in der Gesamtstruktur gespeichert und anzeigen und Bearbeiten von Daten auf einem beliebigen Computer in der Gesamtstruktur gespeichert. Aus diesem Grund muss physischen Zugriff auf Domänencontroller, auf vertrauenswürdige Mitarbeiter beschränkt.  
  
-   Sie verstehen und akzeptieren das potenzielle Risiko, das vertrauenswürdige Dienstadministratoren umgewandelt werden können, in die Sicherheit des Systems gefährden.  
  
Einige Gruppen entscheiden möglicherweise, dass die Zusammenarbeit und Kostenersparnis Vorteile der Teilnahme an einem gemeinsamen Infrastruktur, die Risiken, die Dienstadministratoren missbraucht werden, oder werden überwiegen in ihrer Behörde missbraucht umgewandelt werden. Diese Gruppen können gemeinsame Gesamtstruktur und Organisationseinheiten um delegieren. Allerdings können andere Gruppen dieses Risiko nicht akzeptieren, da die Konsequenzen einer Gefährdung der Sicherheit zu groß sind. Diese Gruppen erfordern separate Gesamtstrukturen.  
  


