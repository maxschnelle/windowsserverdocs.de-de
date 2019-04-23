---
ms.assetid: da7b6dcf-53ec-4394-88c0-c087d92f3893
title: 'Dienstadministrator: Autoritätsumfang'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b5bf2fb3b06a47d730b9dd124b2b66a0a4c9c691
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864851"
---
# <a name="service-administrator-scope-of-authority"></a>Dienstadministrator: Autoritätsumfang

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie Active Directory-Gesamtstruktur teilnehmen möchten, müssen Sie der Gesamtstrukturbesitzer und die Dienstadministratoren vertrauenswürdig. Die Gesamtstrukturbesitzer sind verantwortlich für das auswählen und die Dienstadministratoren verwalten; Wenn Sie einen Gesamtstrukturbesitzer vertrauen, vertrauen Sie daher auch die Dienstadministratoren, die der Gesamtstrukturbesitzer verwaltet. Diese Dienstadministratoren haben Zugriff auf alle Ressourcen in der Gesamtstruktur. Vor der Entscheidung zur Teilnahme an einer Gesamtstruktur, ist es wichtig zu wissen, dass der Gesamtstrukturbesitzer und die Dienstadministratoren Vollzugriff auf Ihre Daten. Dieser Zugriff lässt sich nicht verhindern.  
  
Aller Dienstadministratoren in einer Gesamtstruktur über Vollzugriff auf alle Daten und Dienste auf allen Computern in der Gesamtstruktur verfügen. Administratoren haben die Möglichkeit, die folgenden Schritte ausführen:  
  
-   Beheben von Fehlern auf Zugriffssteuerungslisten (ACLs) von Objekten. Dies ermöglicht dem Dienstadministrator, lesen, ändern oder Löschen von Objekten unabhängig von den ACLs, die für diese Objekte festgelegt werden.  
  
-   Ändern Sie die Systemsoftware auf einem Domänencontroller, normale sicherheitsüberprüfungen zu umgehen. Dies ermöglicht dem Dienstadministrator, anzeigen oder ändern jedes Objekt in der Domäne, unabhängig von der ACL des Objekts.  
  
-   Verwenden Sie die Sicherheitsrichtlinie für eingeschränkte Gruppen Benutzer oder Gruppe administrativen Zugriff auf einem beliebigen Computer in der Domäne gewähren. Auf diese Weise können Dienstadministratoren Kontrolle von einem beliebigen Computer in der Domäne unabhängig von den Zweck der Besitzer des Computers zu erhalten.  
  
-   Zurücksetzen von Kennwörtern, oder ändern Sie die Gruppenmitgliedschaften für Benutzer.  
  
-   Erhalten Sie Zugriff auf andere Domänen in der Gesamtstruktur, indem Sie die Systemsoftware auf einem Domänencontroller ändern. Dienstadministratoren können Auswirkungen auf einer beliebigen Domäne in der Gesamtstruktur, anzeigen oder Ändern der Konfigurationsdaten der Gesamtstruktur, anzeigen oder Bearbeiten von Daten in einer beliebigen Domäne aus, und anzeigen oder bearbeiten Daten auf einem beliebigen Computer in der Gesamtstruktur.  
  
Aus diesem Grund Gruppen, die Daten in Organisationseinheiten (OEs) in der Gesamtstruktur und Join-Computer in einer Gesamtstruktur vertrauen müssen, die Dienstadministratoren zu speichern. Für eine Gruppe eine Gesamtstruktur zu verknüpfen müssen sie auswählen, aller Dienstadministratoren in der Gesamtstruktur vertrauen. Dies umfasst, um sicherzustellen, dass:  
  
-   Der Gesamtstrukturbesitzer kann im Interesse der Gruppe fungieren vertrauenswürdig sein und hat keinen Grund, die für die Gruppe in böswilliger Absicht fungiert.  
  
-   Der Gesamtstrukturbesitzer beschränkt entsprechend physischen Zugriff auf Domänencontroller. Domänencontroller in einer Gesamtstruktur darf nicht voneinander isoliert sein. Es ist möglich, dass ein Angreifer mit physischem Zugriff auf einen einzelnen Domänencontroller offline Änderungen vornehmen, um die Directory-Datenbank und auf diese Weise, beeinträchtigt den Betrieb von einer beliebigen Domäne in der Gesamtstruktur, anzeigen oder Bearbeiten von Daten an einer beliebigen Stelle in der Gesamtstruktur , und anzeigen oder Bearbeiten von Daten, die auf einem beliebigen Computer in der Gesamtstruktur gespeichert. Aus diesem Grund muss die physischer Zugriff auf den Domänencontrollern auf vertrauenswürdige Mitarbeiter beschränkt sein.  
  
-   Verstehen und akzeptieren Sie das potenzielle Risiko, das als, dass die Dienstadministratoren umgewandelt werden können vertrauenswürdig, in die Sicherheit des Systems beeinträchtigen.  
  
Einige Gruppen können bestimmen, dass die Zusammenarbeit und kostengünstiges Vorteile der Teilnahme an einer freigegebenen Infrastruktur gegenüber den Risiken, die Dienstadministratoren missbrauchen werden oder werden überwiegen in ihre Autorität für die Verwendung umgewandelt werden. Diese Gruppen können gemeinsame Gesamtstruktur und Organisationseinheiten, um Autorität zu delegieren. Jedoch können andere Gruppen dieses Risiko nicht akzeptiert, da die Folgen einer Gefährdung der Sicherheit zu schwerwiegend sind. Diese Gruppen erfordern separate Gesamtstrukturen.  
  


