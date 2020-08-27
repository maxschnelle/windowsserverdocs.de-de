---
ms.assetid: da7b6dcf-53ec-4394-88c0-c087d92f3893
title: 'Dienstadministrator: Autoritätsumfang'
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e34f8a7aac27719bc2841324fb87d9e5ca5548bb
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88938430"
---
# <a name="service-administrator-scope-of-authority"></a>Dienstadministrator: Autoritätsumfang

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie sich für die Teilnahme an einer Active Directory Gesamtstruktur entscheiden, müssen Sie dem Gesamtstruktur Besitzer und den Dienst Administratoren Vertrauen. Die Gesamtstruktur Besitzer sind dafür verantwortlich, die Dienst Administratoren auszuwählen und zu verwalten. Wenn Sie einen Gesamtstruktur Besitzer als vertrauenswürdig einstufen, Vertrauen Sie daher auch den Dienst Administratoren, die der Gesamtstruktur Besitzer verwaltet. Diese Dienst Administratoren haben Zugriff auf alle Ressourcen in der Gesamtstruktur. Bevor Sie sich für die Teilnahme an einer Gesamtstruktur entscheiden, ist es wichtig zu verstehen, dass der Gesamtstruktur Besitzer und die Dienst Administratoren vollen Zugriff auf Ihre Daten haben. Dieser Zugriff kann nicht verhindert werden.

Alle Dienst Administratoren in einer Gesamtstruktur verfügen über vollständige Kontrolle über alle Daten und Dienste auf allen Computern in der Gesamtstruktur. Dienst Administratoren haben folgende Möglichkeiten:

-   Korrigieren von Fehlern in Zugriffs Steuerungs Listen (ACLs) von Objekten. Dies ermöglicht es dem Dienst Administrator, Objekte unabhängig von den ACLs, die für diese Objekte festgelegt sind, zu lesen, zu ändern oder zu löschen.

-   Ändern Sie die Systemsoftware auf einem Domänen Controller, um normale Sicherheitsüberprüfungen zu umgehen. Dies ermöglicht es dem Dienst Administrator, ein beliebiges Objekt in der Domäne unabhängig von der ACL des Objekts anzuzeigen oder zu bearbeiten.

-   Verwenden Sie die Sicherheitsrichtlinie eingeschränkte Gruppen, um allen Benutzern oder Gruppen administrativen Zugriff auf jeden Computer zu gewähren, der der Domäne beigetreten ist. Auf diese Weise können Dienst Administratoren unabhängig von den Absichten des Computer Besitzers die Kontrolle über jeden Computer erhalten, der der Domäne beigetreten ist.

-   Zurücksetzen von Kenn Wörtern oder Ändern von Gruppenmitgliedschaften für Benutzer.

-   Sie erhalten Zugriff auf andere Domänen in der Gesamtstruktur, indem Sie die Systemsoftware auf einem Domänen Controller ändern. Dienst Administratoren können den Betrieb einer beliebigen Domäne in der Gesamtstruktur beeinflussen, Gesamtstruktur-Konfigurationsdaten anzeigen oder bearbeiten, in einer beliebigen Domäne gespeicherte Daten anzeigen oder bearbeiten und auf jedem Computer, der der Gesamtstruktur hinzugefügt wird, gespeicherte Daten anzeigen oder bearbeiten.

Aus diesem Grund müssen Gruppen, die Daten in Organisationseinheiten (OUs) in der Gesamtstruktur speichern und den Computern in einer Gesamtstruktur beitreten, den Dienst Administratoren Vertrauen. Damit eine Gruppe einer Gesamtstruktur beitreten kann, muss Sie alle Dienst Administratoren in der Gesamtstruktur als vertrauenswürdig einstufen. Dazu muss Folgendes sichergestellt werden:

-   Der Gesamtstruktur Besitzer kann als vertrauenswürdig eingestuft werden, um in den Interessen der Gruppe zu agieren, und es besteht keine Begründung, um für die Gruppe böswillig zu agieren.

-   Der Gesamtstruktur Besitzer schränkt den physischen Zugriff auf Domänen Controller entsprechend ein. Domänen Controller innerhalb einer Gesamtstruktur können nicht voneinander isoliert werden. Ein Angreifer, der überphysischen Zugriff auf einen einzelnen Domänen Controller verfügt, kann offline Änderungen an der Verzeichnis Datenbank vornehmen. Dadurch stören Sie den Betrieb von Domänen in der Gesamtstruktur, zeigen oder bearbeiten Sie Daten, die an beliebiger Stelle in der Gesamtstruktur gespeichert sind, und zeigen Sie die Daten an, die auf jedem Computer, der der Gesamtstruktur hinzugefügt wurde, gespeichert sind. Aus diesem Grund muss der physische Zugriff auf Domänen Controller auf vertrauenswürdige Mitarbeiter beschränkt sein.

-   Sie verstehen und übernehmen das potenzielle Risiko, dass vertrauenswürdige Dienst Administratoren die Sicherheit des Systems beeinträchtigen können.

Einige Gruppen können feststellen, dass die gemeinsamen und kostensparenden Vorteile der Teilnahme an einer gemeinsam genutzten Infrastruktur die Risiken überwiegen, die Dienst Administratoren missbrauchen oder in ihre Autorität missbrauchen werden. Diese Gruppen können eine Gesamtstruktur gemeinsam verwenden und Organisationseinheiten verwenden, um Autorität zu delegieren. Andere Gruppen akzeptieren dieses Risiko jedoch möglicherweise nicht, da die Folgen einer Gefährdung der Sicherheit zu schwer sind. Diese Gruppen erfordern separate Gesamtstrukturen.



