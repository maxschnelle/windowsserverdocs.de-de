---
ms.assetid: e727a33d-133b-43c9-b6a4-7c00f9cb6000
title: "Überprüfen der Domänenmodelle"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c57c23c0bd8694b66ab29b45bd9e47826ed1e01d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="reviewing-the-domain-models"></a>Überprüfen der Domänenmodelle

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die folgenden Faktoren Auswirkungen auf die Design-Domänenmodell, das Sie auswählen:  
  
-   Menge der verfügbaren Kapazität in Ihrem Netzwerk, das Sie Active Directory-Domänendienste (AD DS) verteilen möchten. Das Ziel ist ein Modell aus, das effiziente Replikation von Informationen mit minimalem Einfluss auf die verfügbare Netzwerkbandbreite ermöglicht.  
  
-   Anzahl der Benutzer in Ihrer Organisation. Wenn Ihre Organisation eine große Anzahl von Benutzern enthält, Bereitstellen von mehr als einer Domäne ermöglicht es Ihnen, Ihre Daten zu partitionieren und bietet Ihnen mehr Kontrolle über die Menge des Replikations-Datenverkehr, der einer bestimmten Netzwerkverbindung weitergeleitet werden. Dadurch können Sie steuern, in denen Daten repliziert werden, und verringern Sie die Auslastung von Replikationsdatenverkehr für langsame Verbindungen in Ihrem Netzwerk erstellt werden.  
  
Die einfachste Domänenentwurf ist eine einzelne Domäne. In einer einzelnen Domäne-Design werden alle Informationen auf alle Domänencontroller repliziert. Falls erforderlich, jedoch können Sie zusätzliche regionale Domänen bereitstellen. Dies kann vorkommen, wenn Teile der Netzwerkinfrastruktur langsame verbunden sind, und möchte, dass des Besitzers der Gesamtstruktur sicher sein, dass die Replikation die Kapazität nicht überschreitet, die in AD DS zugewiesen wurde.  
  
Es wird empfohlen, die Anzahl von Domänen zu minimieren, die Sie in der Gesamtstruktur bereitstellen. Dies reduziert die Komplexität der Bereitstellung und daher Gesamtbetriebskosten reduziert. Die folgende Tabelle enthält die Verwaltungskosten, die mit dem regionale Domänen hinzufügen.  
  
|Kosten|Auswirkungen|  
|--------|----------------|  
|Verwaltung von mehreren Dienstadministrator-Gruppen|Jede Domäne verfügt über einen eigenen Dienstadministrator-Gruppen, die unabhängig voneinander verwaltet werden müssen. Die Mitgliedschaft dieser Dienstadministrator-Gruppen muss sorgfältig gesteuert werden.|  
|Verwalten von Konsistenz zwischen Gruppenrichtlinieneinstellungen, die mehreren Domänen gelten|Mithilfe von Gruppenrichtlinieneinstellungen, die angewendet werden Gesamtstrukturebene müssen müssen separat für jede einzelne Domäne in der Gesamtstruktur angewendet werden.|  
|Verwalten von Konsistenz zwischen Zugriffskontrolle und Überwachung von Einstellungen, die mehreren Domänen|Zugriffskontrolle und Überwachung von Einstellungen, die in der Gesamtstruktur angewendet werden müssen, müssen separat für jede einzelne Domäne in der Gesamtstruktur angewendet werden.|  
|Eine erhöhte Wahrscheinlichkeit, dass Objekte verschieben zwischen Domänen|Je größer die Anzahl von Domänen, desto größer ist die Wahrscheinlichkeit, die Benutzer von einer Domäne auf einen anderen verschieben müssen. Verschiebung kann potenziell Endbenutzer auswirken.|  
  
> [!NOTE]  
>  Windows Server2008 abgestimmte Kennwort- und Kontosperrungsrichtlinien können auch das Domänenmodell der Entwurf auswirken, das Sie auswählen. Vor dieser Version von Windows Server2008 können Sie nur eine Kennwort- und Kontosperrungsrichtlinie, die in der Domäne Default Domain Policy angegeben wird, für alle Benutzer in der Domäne anwenden. Daher Wunsch unterschiedliche Kennwort- und kontosperrungseinstellungen für verschiedene Gruppen von Benutzern, mussten Sie entweder einen Kennwortfilter erstellen oder mehrere Domänen bereitstellen. Sie können differenzierte Kennwortrichtlinien jetzt an mehrere Kennwortrichtlinien und Einschränkungen für unterschiedliche Kennwort- und Kontosperrungsrichtlinien für verschiedene Gruppen von Benutzern in einer einzelnen Domäne gelten. Weitere Informationen zu abgestimmte Kennwort- und Kontosperrungsrichtlinien finden Sie unter der Step-by-Step Anleitung für differenzierte Konfiguration Kennwort- und Kontosperrungsrichtlinien Richtlinie ([https://go.microsoft.com/fwlink/?LinkID=91477](https://go.microsoft.com/fwlink/?LinkID=91477)).  
  
## <a name="single-domain-model"></a>Einfache Domänenmodell  
Ein einfaches Domänenmodell ist am einfachsten zu verwalten und kostengünstigsten zu verwalten. Es besteht aus einer Gesamtstruktur mit einer einzelnen Domäne. Diese Domäne ist die Stammdomäne der Gesamtstruktur, und es enthält alle von der Benutzer- und Gruppenkonten in der Gesamtstruktur.  
  
Eine einzelne Domäne Gesamtstrukturmodell reduziert Verwaltungsaufwand durch die folgenden Vorteile:  
  
-   Alle Domänencontroller kann alle Benutzer in der Gesamtstruktur authentifizieren.  
  
-   Alle Domänencontroller können globale Kataloge sein, daher Sie nicht planen der Platzierung des globalen Katalogservers müssen.  
  
In einer Gesamtstruktur mit einer Domäne werden alle Verzeichnisdaten in allen geografische Standorte, die anderen Domänencontroller repliziert. Während dieses Modell am einfachsten zu verwalten ist, wird auch die meisten Replikations-Datenverkehr von der zwei Domänenmodelle erstellt. Der Partitionierung des Verzeichnisses in mehreren Domänen beschränkt die Replikation von Objekten führt steigt der Verwaltungsaufwand jedoch bestimmte geografische Regionen.  
  
## <a name="regional-domain-model"></a>Regionales Domänenmodell  
Alle Daten des Objekts in einer Domäne wird auf allen Domänencontrollern in der Domäne repliziert. Aus diesem Grund enthält die Gesamtstruktur eine große Anzahl von Benutzern, die in unterschiedlichen geografischen Standorten befinden, über ein wide Area Network (WAN) verbunden verteilt werden müssen Sie zum Bereitstellen von Regionaldomänen um Replikations-Datenverkehr über die WAN-Links reduzieren. Geografisch je Regionaldomänen können entsprechend der WAN-Netzwerkkonnektivität organisiert werden.  
  
Die regionales Domänenmodell können Sie eine stabile Umgebung mit der Zeit verwalten. Basis-Regionen Domänen im Modell für stabile Elemente, z.B. continental Grenzen definiert. Domänen, die basierend auf anderen Faktoren, wie Gruppen innerhalb der Organisation, können sich häufig ändern und möglicherweise müssen Sie Ihre Umgebung umstrukturieren.  
  
Die regionales Domänenmodell besteht aus einer Gesamtstruktur-Stammdomäne und eine oder mehrere regionale Domänen. Erstellen eines Entwurfs für regionale Domäne Modell umfasst die identifizieren, welche Domäne Stammdomäne der Gesamtstruktur ist, und Bestimmen der Anzahl der zusätzlichen Domänen, die erforderlich sind, um die Replikation zu erfüllen. Wenn Ihre Organisation Gruppen, die Datenisolation oder Dienstisolation aus anderen Gruppen in der Organisation erfordern enthält, erstellen Sie eine separate Gesamtstruktur für diese Gruppen. Die Trennung von Daten oder Dienstisolation bereit Domänen nicht.  
  


