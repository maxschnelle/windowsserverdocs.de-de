---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: Überprüfen von Entwurfskonzepten für Organisationseinheiten
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 67f8ef3ec37146002f3e099caa459fc209fcf5b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821974"
---
# <a name="reviewing-ou-design-concepts"></a>Überprüfen von Entwurfskonzepten für Organisationseinheiten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Struktur der Organisationseinheit (OU) für eine Domäne umfasst Folgendes:  
  
-   Ein Diagramm der OE-Hierarchie  
  
-   Eine Liste der Organisationseinheiten  
  
-   Für jede Organisationseinheit:  
  
    -   Zweck der Organisationseinheit  
  
    -   Eine Liste von Benutzern oder Gruppen, die die Kontrolle über die Organisationseinheit oder die Objekte in der Organisationseinheit haben  
  
    -   Der Typ des Steuer Elements, das Benutzer und Gruppen über die Objekte in der Organisationseinheit verfügen.  
  
Die Hierarchie der Organisationseinheiten muss die Abteilungs Hierarchie der Organisation oder Gruppe nicht widerspiegeln. Organisationseinheiten werden für einen bestimmten Zweck erstellt, z. b. die Delegierung der Verwaltung, die Anwendung von Gruppenrichtlinie oder das Einschränken der Sichtbarkeit von Objekten.  
  
Sie können Ihre OE-Struktur so entwerfen, dass die Verwaltung an Einzelpersonen oder Gruppen in Ihrem Unternehmen delegiert wird, die Autonomie benötigen, um Ihre eigenen Ressourcen und Daten zu verwalten. Organisationseinheiten stellen administrative Grenzen dar und ermöglichen es Ihnen, den Gültigkeitsbereich von Daten Administratoren zu steuern.  
  
Beispielsweise können Sie eine Organisationseinheit mit dem Namen "ResourceOU" erstellen und diese zum Speichern aller Computer Konten verwenden, die zu den von einer Gruppe verwalteten Datei-und Druckservern gehören. Anschließend können Sie die Sicherheit für die Organisationseinheit so konfigurieren, dass nur Daten Administratoren in der Gruppe Zugriff auf die Organisationseinheit haben. Dadurch wird verhindert, dass Daten Administratoren in anderen Gruppen die Datei-und Druckserver Konten manipulieren.  
  
Sie können Ihre OE-Struktur weiter verfeinern, indem Sie Unterstrukturen von Organisationseinheiten für bestimmte Zwecke erstellen, z. b. die Anwendung von Gruppenrichtlinie, oder um die Sichtbarkeit geschützter Objekte einzuschränken, sodass nur bestimmte Benutzer Sie sehen können. Wenn Sie z. b. Gruppenrichtlinie auf eine ausgewählte Gruppe von Benutzern oder Ressourcen anwenden müssen, können Sie diese Benutzer oder Ressourcen einer Organisationseinheit hinzufügen und dann Gruppenrichtlinie auf diese Organisationseinheit anwenden. Sie können auch die Hierarchie der Organisationseinheiten verwenden, um die Delegierung der administrativen Kontrolle zu aktivieren.  
  
Es gibt zwar keine technische Beschränkung für die Anzahl der Ebenen in der OE-Struktur, aber für die Verwaltbarkeit wird empfohlen, dass Sie Ihre OE-Struktur auf eine Tiefe von höchstens 10 Ebenen beschränken. Es gibt keine technische Beschränkung für die Anzahl der Organisationseinheiten auf jeder Ebene. Beachten Sie, dass Active Directory Domain Services (AD DS)-aktivierten Anwendungen möglicherweise Beschränkungen hinsichtlich der Anzahl von Zeichen aufweisen, die im Distinguished Name verwendet werden (d. h. der LDAP-Pfad (Full Lightweight Directory Access Protocol) für das Objekt im Verzeichnis) oder in der Organisationseinheit innerhalb der Hierarchie.  
  
Die OE-Struktur in AD DS sollte nicht für Endbenutzer sichtbar sein. Die OE-Struktur ist ein Verwaltungs Tool für Dienst Administratoren und für Daten Administratoren und kann leicht geändert werden. Überprüfen und aktualisieren Sie den Entwurf ihrer OU-Struktur, um Änderungen an der administrativen Struktur und die Unterstützung der Richtlinien basierten Verwaltung zu berücksichtigen.  
  


