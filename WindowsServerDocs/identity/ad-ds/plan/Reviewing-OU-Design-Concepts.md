---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: Überprüfen von Entwurfskonzepten für Organisationseinheiten
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f05104466c1cedcfbc8d94060ffa8fbfd9d18033
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832171"
---
# <a name="reviewing-ou-design-concepts"></a>Überprüfen von Entwurfskonzepten für Organisationseinheiten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Struktur der Organisationseinheit (OU) für eine Domäne umfasst Folgendes:  
  
-   Ein Diagramm der Hierarchie der Organisationseinheiten  
  
-   Eine Liste von Organisationseinheiten  
  
-   Für jede Organisationseinheit:  
  
    -   Der Zweck der Organisationseinheit  
  
    -   Eine Liste von Benutzern oder Gruppen, die Kontrolle über die Organisationseinheit oder die Objekte in der Organisationseinheit verfügen.  
  
    -   Der Typ des Steuerelements, die Benutzer und Gruppen über die Objekte in der Organisationseinheit  
  
Die Hierarchie der Organisationseinheiten muss nicht von der Organisation oder die Gruppe der Abteilung Hierarchie entspricht. Organisationseinheiten sind für einen bestimmten Zweck, z. B. die Delegierung der Verwaltung auf, die Anwendung der Gruppenrichtlinie oder die Sichtbarkeit von Objekten beschränken erstellt.  
  
Sie können die Struktur der Organisationseinheit Delegieren der Verwaltung an Einzelpersonen oder Gruppen in Ihrer Organisation, die die Autonomie verwalten ihre eigenen Ressourcen und die Daten erfordern entwerfen. Organisationseinheiten Verwaltungsgrenzen darstellen und ermöglichen es Ihnen, den Umfang der Autorität für die der Datenadministratoren steuern.  
  
Sie können z. B. erstellen eine Organisationseinheit, die mit dem Namen ResourceOU und verwenden, um alle Computerkonten zu speichern, die die Datei- und Druckserver verwaltet, die von einer Gruppe angehören. Anschließend können Sie in der Organisationseinheit Sicherheit konfigurieren, damit nur Datenadministratoren in der Gruppe haben Zugriff auf die Organisationseinheit. Dadurch wird verhindert, dass Data-Administratoren in anderen Gruppen der Datei- und Druckserver Konten manipulieren.  
  
Sie können die Struktur der Organisationseinheit weiter optimieren, durch das Erstellen von Unterstrukturen von Organisationseinheiten für bestimmte Zwecke, z. B. die Anwendung der Gruppenrichtlinie oder die Sichtbarkeit der geschützte Objekte zu beschränken, sodass nur bestimmte Benutzer, die sie sehen können. Z. B. Wenn Sie die Gruppenrichtlinie für eine ausgewählte Gruppe von Benutzern oder Ressourcen anwenden müssen, können Sie diese Benutzer oder die Ressourcen mit einer Organisationseinheit hinzufügen und dann anwenden der Gruppenrichtlinie zu dieser Organisationseinheit. Sie können die Hierarchie der Organisationseinheiten auch verwenden, um Delegierung von Verwaltungsfunktionen weiter zu aktivieren.  
  
Es gibt zwar keine technische Grenze um die Anzahl der Ebenen in Ihrer Organisationsstruktur, zu Zwecken der Verwaltbarkeit empfehlen wir die Struktur der Organisationseinheit zu einer Tiefe von maximal 10 Ebenen zu beschränken. Es gibt keine technische Grenze auf die Anzahl von OEs für jede Ebene ein. Beachten Sie, Active Directory Domain Services (AD DS)-aktivierte Anwendungen verfügen möglicherweise über Einschränkungen für die Anzahl der Zeichen, die in den distinguished Name (d. h. den vollständigen Lightweight Directory Access Protocol (LDAP) Pfad auf das Objekt in das Verzeichnis) verwendet oder auf der Organisationseinheit Tiefe innerhalb der Hierarchie.  
  
Die Struktur der Organisationseinheiten in AD DS ist nicht vorgesehen, für den Endbenutzer sichtbar sein soll. Die OE-Struktur ist ein Verwaltungstool für Dienstadministratoren und Datenadministratoren, und es ist einfach, zu ändern. Überprüfen und Aktualisieren des Entwurfs der OE-Struktur an eine Verwaltungsstruktur widerzuspiegeln und zur Unterstützung der Richtlinie der richtlinienbasierten Verwaltung weiterhin.  
  


