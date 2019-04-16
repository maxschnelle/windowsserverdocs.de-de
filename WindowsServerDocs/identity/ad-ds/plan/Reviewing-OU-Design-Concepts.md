---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: "Überprüfen von Entwurfskonzepten für Organisationseinheiten"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e832d068a4d03316853d8b59e3f2ac4a6ebc816
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="reviewing-ou-design-concepts"></a>Überprüfen von Entwurfskonzepten für Organisationseinheiten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die Struktur der Organisationseinheit (OU) für eine Domäne umfasst Folgendes:  
  
-   Ein Diagramm der Hierarchie der Organisationseinheiten  
  
-   Eine Liste der Organisationseinheiten  
  
-   Für jede Organisationseinheit:  
  
    -   Der Zweck für die Organisationseinheit  
  
    -   Eine Liste von Benutzern oder Gruppen, die Kontrolle über die Organisationseinheit oder die Objekte in der Organisationseinheit  
  
    -   Der Typ des Steuerelements, die Benutzer und Gruppen über die Objekte in der Organisationseinheit  
  
Die Hierarchie der Organisationseinheiten muss nicht die Abteilung Hierarchie des Unternehmens oder der Gruppe wiedergeben. Organisationseinheiten sind für einen bestimmten Zweck, z.B. die Delegierung von Verwaltung, die Anwendung der Gruppenrichtlinie oder beschränken Sie die Sichtbarkeit von Objekten erstellt.  
  
Sie können die OE-Struktur zum Delegieren der Verwaltung an andere Personen oder Gruppen in Ihrer Organisation, die Autonomie verwalten Sie ihre eigenen Ressourcen und die Daten benötigen, entwerfen. Organisationseinheiten Verwaltungsgrenzen darstellen, und aktivieren Sie den Umfang der Autorität Datenadministratoren steuern.  
  
Sie können z.B. Erstellen einer Organisationseinheit ResourceOU und verwenden, um alle der Computerkonten zu speichern, die die Datei- und Druckserver verwaltet eine Gruppe angehören. Klicken Sie dann können Sie in der Organisationseinheit Sicherheit konfigurieren, damit nur von Datenadministratoren in der Gruppe Zugriff auf die Organisationseinheit verfügen. Dadurch wird verhindert, dass Datenadministratoren in anderen Gruppen Manipulationen an der Datei- und Druckserver Konten.  
  
Sie können die OU-Struktur weiter optimieren, durch das Erstellen von Unterstrukturen von Organisationseinheiten für bestimmte Zwecke, z.B. die Anwendung der Gruppenrichtlinie oder die Sichtbarkeit des geschützten Objekte beschränken, sodass nur bestimmte Benutzer sie sehen können. Z.B., wenn Sie eine Gruppenrichtlinie für eine ausgewählte Gruppe von Benutzern oder Ressourcen anwenden müssen, können Sie die Benutzer oder Ressourcen mit einer Organisationseinheit hinzufügen und dann Anwenden von Gruppenrichtlinien auf die Organisationseinheit. Die Hierarchie der Organisationseinheiten können auch um weitere Zuweisen von Verwaltungsfunktionen aktivieren.  
  
Es gibt zwar keine technische Beschränkung der Anzahl der Ebenen in der OU-Struktur, empfohlen für die Verwaltung, die OU-Struktur auf eine Tiefe von nicht mehr als 10 Ebenen zu beschränken. Es gibt keine technische Beschränkung der Anzahl der Organisationseinheiten auf jeder Ebene. Beachten Sie die Active Directory-Domänendienste (AD DS)-aktivierte Anwendungen möglicherweise Einschränkungen auf der Anzahl der Zeichen, die in den distinguished Name (d.h. den vollständigen Lightweight Directory Access Protocol (LDAP) Pfad auf das Objekt im Verzeichnis) verwendet oder auf die Organisationseinheit Tiefe innerhalb der Hierarchie.  
  
Die Struktur der Organisationseinheiten in AD DS kann nicht für Endbenutzer angezeigt werden. Die OU-Struktur ist ein Verwaltungstool für Dienstadministratoren und Datenadministratoren und ganz einfach ändern. Weiterhin überprüfen und aktualisieren Sie den Entwurf Ihrer OU-Struktur, Änderungen an eine Verwaltungsstruktur aktualisiert und richtlinienbasierte Verwaltung zu unterstützen.  
  


