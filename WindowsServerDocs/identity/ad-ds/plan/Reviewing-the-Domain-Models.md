---
ms.assetid: e727a33d-133b-43c9-b6a4-7c00f9cb6000
title: Überprüfen der Domänenmodelle
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 23c1eb66eeecab8df63cbd7910a9398bc4e3c705
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870921"
---
# <a name="reviewing-the-domain-models"></a>Überprüfen der Domänenmodelle

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die folgenden Faktoren haben Auswirkungen auf das Domänenmodell für den Entwurf, das Sie auswählen aus:  
  
- Die Menge der verfügbaren Kapazität in Ihrem Netzwerk, die Sie zu Active Directory Domain Services (AD DS) bereit. Das Ziel ist ein Modell aus, die effiziente Replikation von Informationen mit minimalen Auswirkungen auf die verfügbare Netzwerkbandbreite bereitstellt.  

- Anzahl der Benutzer in Ihrer Organisation. Wenn Ihre Organisation über eine große Anzahl von Benutzern enthält, Bereitstellen von mehr als eine Domäne ermöglicht es Ihnen, Ihre Daten partitionieren, und gibt Ihnen mehr Kontrolle über den Umfang des Replikationsdatenverkehrs, die über eine Netzwerk-Verbindung übergeben wird. Dadurch können Sie steuern, wo Daten repliziert werden, und verringern Sie die Auslastung von Replikationsdatenverkehr für langsame Verbindungen in Ihrem Netzwerk erstellt werden.  

Das einfachste domänendesign ist eine einzelne Domäne. In einem Entwurf Einzeldomäne werden alle Informationen für alle Domänencontroller repliziert. Falls erforderlich, jedoch können Sie zusätzliche regionale Domänen bereitstellen. Dies kann auftreten, wenn Teile der Netzwerkinfrastruktur über langsame Verbindungen verbunden sind, und der Gesamtstruktur möchte sicher sein, dass der Replikationsdatenverkehr nicht die Kapazität überschreitet, die in AD DS belegt wurde.  

Es wird empfohlen, um die Anzahl der Domänen zu minimieren, die Sie in der Gesamtstruktur bereitstellen. Dies reduziert die Komplexität der Bereitstellung und wird daher der Gesamtbetriebskosten reduziert. Die folgende Tabelle enthält die Verwaltungskosten Regionaldomänen hinzufügen.  

|Kosten|Auswirkungen auf die|  
|--------|----------------|  
|Verwaltung von mehreren Dienstadministrator-Gruppen|Jede Domäne verfügt über eine eigene Dienstadministrator-Gruppen, die unabhängig voneinander verwaltet werden müssen. Die Mitgliedschaft dieser Gruppen der Service-Administrator muss sorgfältig kontrolliert werden.|  
|Aufrechterhaltung der Konsistenz zwischen der gruppenrichtlinieneinstellungen, die für mehrere Domänen gelten|Gruppenrichtlinieneinstellungen, die angewendet werden Gesamtstruktur müssen müssen separat für jede einzelne Domäne in der Gesamtstruktur angewendet werden.|  
|Aufrechterhaltung der Konsistenz zwischen Zugriffssteuerung und Überwachung von Einstellungen, die für mehrere Domänen gelten|Zugriffssteuerung und Überwachung von Einstellungen, die in der Gesamtstruktur angewendet werden müssen, müssen separat für jede einzelne Domäne in der Gesamtstruktur angewendet werden.|  
|Erhöhte Wahrscheinlichkeit von Objekten zwischen Domänen verschoben|Je größer die Anzahl der Domänen, desto größer die Wahrscheinlichkeit, die Benutzer von einer Domäne in eine andere verschieben müssen. Diese Umstellung kann potenziell Endbenutzer auswirken.|  

> [!NOTE]  
> WindowsServer abgestimmte Kennwort- und Kontosperrungsrichtlinien können auch das Domänenmodell für den Entwurf auswirken, das Sie auswählen. Vor dieser Version von Windows Server 2008 konnten Sie nur eine Kennwort- und Kontosperrungsrichtlinien Richtlinie, die in der Domäne Default Domain Policy angegeben wird, für alle Benutzer in der Domäne anwenden. Daher, wenn Sie unterschiedliche Kennwort- und kontosperrungseinstellungen für verschiedene Gruppen von Benutzern wollten, mussten Sie entweder einen Kennwortfilter erstellen oder mehrere Domänen bereitstellen. Sie können jetzt fein abgestimmte Kennwortrichtlinien verwenden, die sich auf mehrere Kennwortrichtlinien angeben und Anwenden von Einschränkungen für unterschiedliche Kennwort- und Kontosperrungsrichtlinien auf verschiedene Gruppen von Benutzern innerhalb einer einzelnen Domäne. Weitere Informationen über differenzierte Kennwort- und Kontosperrungsrichtlinien, finden Sie im Artikel [schrittweisen Anleitung für die Konfiguration abgestimmter Kennwort- und Account Lockout Richtlinienkonfiguration](https://go.microsoft.com/fwlink/?LinkID=91477).  

## <a name="single-domain-model"></a>Domänenmodell

Ein Domänenmodell ist am einfachsten zu verwalten und den geringsten Aufwand zu verwalten. Es besteht aus einer Gesamtstruktur, die eine Einzeldomäne enthält. Diese Domäne ist die Gesamtstruktur-Stammdomäne, und er enthält alle von der Benutzer- und Gruppenkonten in der Gesamtstruktur.  

Eine einzelne Domäne Forest-Modell reduziert die Komplexität der Verwaltung, durch die Bereitstellung die folgenden Vorteile:  

- Alle Domänencontroller kann alle Benutzer in der Gesamtstruktur authentifizieren.  

- Alle Domänencontroller können globale Kataloge werden, benötigen Sie nicht zum Planen der Platzierung des globalen Katalogservers.  
  
In einer Gesamtstruktur mit einer Domäne werden alle geografischen Orten, auf denen Domänencontroller gehostet alle Verzeichnisdaten repliziert. Während dieses Modell am einfachsten zu verwalten ist, wird auch der Replikationsdatenverkehr die meisten der beiden Domänencontroller Modelle erstellt. Der Partitionierung des Verzeichnisses in mehreren Domänen beschränkt die Replikation von Objekten, steigt der Verwaltungsaufwand führt jedoch zu bestimmten geografischen Regionen.  
  
## <a name="regional-domain-model"></a>Regionales Domänenmodell

Alle Daten des Objekts innerhalb einer Domäne wird auf allen Domänencontrollern in der Domäne repliziert. Aus diesem Grund ist Wenn Ihre Gesamtstruktur eine große Anzahl von Benutzern enthält, die in unterschiedlichen geografischen Standorten befinden, durch das ein wide Area Network (WAN) verbunden sind verteilt werden müssen Sie zum Bereitstellen von Regionaldomänen um Replikationsdatenverkehr über die WAN-Verbindungen zu reduzieren. Geografisch basierend Regionaldomänen können entsprechend der WAN-Verbindung zum Netzwerk organisiert werden.  
  
Regionales Domänenmodell können Sie eine stabile Umgebung im Laufe der Zeit zu gewährleisten. Basis für die Regionen, die zum Definieren von Domänen in Ihrem Modell auf stabile Elemente, z. B. kontinentalen Grenzen verwendet. Domänen, die basierend auf anderen Faktoren, z. B. Gruppen innerhalb der Organisation, sich häufig ändern können und möglicherweise müssen Sie Ihre Umgebung umstrukturieren möchten.  
  
Regionales Domänenmodell besteht aus einer Gesamtstruktur-Stammdomäne und eine oder mehrere Regionaldomänen. Erstellen ein Modell des regionaldomänenentwurfs umfasst das bestimmen, welche Domänenlisten Stammdomäne der Gesamtstruktur befindet, und Bestimmen der Anzahl der zusätzlichen Domänen, die erforderlich sind, um Ihren Anforderungen zu erfüllen. Wenn Ihre Organisation Gruppen, die die Datenisolation oder Isolation von Diensten aus anderen Gruppen in der Organisation erforderlich enthält, erstellen Sie eine separate Gesamtstruktur für diese Gruppen. Domänen bieten keine Datenisolation oder die Isolation von Diensten.  
