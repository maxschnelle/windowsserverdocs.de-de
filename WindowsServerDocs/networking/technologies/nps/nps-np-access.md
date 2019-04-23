---
title: Zugriffsberechtigung
description: Dieses Thema enthält eine Übersicht über das Netzwerk Richtlinie Zugriffsberechtigungen für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d6d1ca5e-bde0-4509-9e14-dc3fa9ff447e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cdec41fb7925061bb8c8402634e1d9b1625bf301
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849491"
---
# <a name="access-permission"></a>Zugriffsberechtigung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Access-Berechtigung ist so konfiguriert, auf die **Übersicht über die** jede Netzwerkrichtlinie in der Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) auf der Registerkarte. 

Mit dieser Einstellung können Sie konfigurieren die Richtlinie zum gewähren oder Verweigern des Zugriffs für Benutzer, wenn die verbindungsanforderung die Bedingungen und Einschränkungen der Netzwerkrichtlinie entsprechen. 

Zugriffseinstellungen für die Berechtigung haben folgende Auswirkungen:

- **Gewähren des Zugriffs**. Wenn die verbindungsanforderung entspricht, die Bedingungen und Einschränkungen, die in der Richtlinie konfiguriert sind, wird der Zugriff gewährt.
- **Verweigern des Zugriffs**. Zugriff wird verweigert, wenn die verbindungsanforderung entspricht, die Bedingungen und Einschränkungen, die in der Richtlinie konfiguriert sind.

Zugriffsberechtigungen auch gewährt oder verweigert wird basierend auf Ihrer Konfiguration von der DFÜ-Eigenschaften für jedes Benutzerkonto.

>[!NOTE]
>Benutzerkonten und deren Eigenschaften, z. B. DFÜ-Eigenschaften, in entweder Active Directory-Benutzer und Computer oder die lokale Benutzer und Gruppen Microsoft Management Console konfiguriert \(MMC\) -Snap-in, abhängig davon, ob Sie Active Directory&reg; Domain Services (AD DS) installiert.

Die Einstellung für Benutzerkonto **Netzwerk Zugriffsberechtigung**, die für die DFÜ-Eigenschaften von Benutzerkonten konfiguriert ist, überschreibt die Netzwerkrichtlinie Zugriffsberechtigung festlegen. Wenn Netzwerk-Zugriffsberechtigung für ein Benutzerkonto festgelegt ist, um die **steuern den Zugriff über die Netzwerkrichtlinie für NPS** Option, die Network Access-Berechtigung richtlinieneinstellung bestimmt, ob der Benutzer wird Zugriff gewährt oder verweigert.

>[!NOTE]
>In Windows Server 2016, der Standardwert von **Netzwerk Zugriffsberechtigung** in AD DS DFÜ-Eigenschaften des Benutzerkontos ist **steuern den Zugriff über die Netzwerkrichtlinie für NPS**.

Wenn NPS verbindungsanforderungen konfigurierten Netzwerkrichtlinien ausgewertet wird, führt er die folgenden Aktionen aus:

- Wenn die Bedingungen für die erste Richtlinie nicht übereinstimmen, wird NPS ausgewertet wird die nächste Richtlinie, und dieser Prozess wird fortgesetzt, bis eine Übereinstimmung gefunden wird oder alle Richtlinien für eine Übereinstimmung ausgewertet wurden.
- Wenn die Bedingungen und Einschränkungen einer Richtlinie entsprechen, NPS entweder Zugriff gewährt oder verweigert, abhängig vom Wert der berechtigungseinstellung für den Zugriff in der Richtlinie.
- Wenn die Bedingungen für eine richtlinienübereinstimmung, aber die Einschränkungen in der Richtlinie nicht übereinstimmen, lehnt NPS die verbindungsanforderung an.
- Wenn die Bedingungen aller Richtlinien nicht übereinstimmen, lehnt NPS die verbindungsanforderung an.

## <a name="ignore-user-account-dial-in-properties"></a>DFÜ-Eigenschaften des Kontos ignorieren

Sie können konfigurieren, dass NPS-Netzwerkrichtlinien, um die DFÜ-Eigenschaften von Benutzerkonten zu ignorieren, durch Aktivieren oder Deaktivieren der **Einwähleigenschaften des Kontos ignorieren** auf das Kontrollkästchen der **Übersicht über die** Registerkarte eines Netzwerks die Richtlinie. 

Wenn NPS Autorisierung eine verbindungsanforderung ausführt, prüft sie normalerweise die Einwähleigenschaften des Benutzerkontos, in die Netzwerk-Zugriffsberechtigung Einstellungswert beeinflussen können, ob der Benutzer autorisiert ist, eine Verbindung mit dem Netzwerk herstellen. Wenn Sie NPS, um die DFÜ-Eigenschaften von Benutzerkonten zu ignorieren, während der Autorisierung konfigurieren, bestimmen netzwerkrichtlinieneinstellungen an, ob der Benutzer Zugriff auf das Netzwerk gewährt wird.

Die DFÜ-Eigenschaften von Benutzerkonten, die Folgendes beinhalten:

- Netzwerk-Zugriffsberechtigung
- Anrufer-ID
- Rückrufoptionen
- Statische IP-Adresse
- Statische Routen

Um mehrere Arten von Verbindungen unterstützen, für die NPS-Authentifizierung und Autorisierung bereitstellt, kann es notwendig, deaktivieren die Verarbeitung von DFÜ-Eigenschaften des Benutzerkontos sein. Dies kann erfolgen, um Szenarien zu unterstützen, in denen bestimmte DFÜ-Eigenschaften nicht erforderlich sind.

Z. B. die Anrufer-ID, Rückruf, statische IP-Adresse und statische Routen Eigenschaften dienen für einen Client, der ein Einwählen ist \(NAS\), jedoch nicht für Clients, die eine Verbindung mit Drahtloszugriffspunkten herstellen. Ein drahtlosen Zugriffspunkt, der diese Einstellungen in einer von NPS RADIUS-Nachricht empfängt möglicherweise nicht verarbeiten, dadurch kann der drahtlose Client getrennt wird.

Wenn es sich bei NPS bietet Authentifizierung und Autorisierung für Benutzer, die sowohl in einwählen und Zugriff auf Ihr Unternehmensnetzwerk über drahtlose Zugriffspunkte sind, müssen Sie die DFÜ-Eigenschaften zur Unterstützung von beiden DFÜ-Verbindungen konfigurieren \(durch Festlegen von Einwähleigenschaften\) oder Drahtlosverbindungen \(durch Festlegen von DFÜ-Eigenschaften nicht\).

Sie können NPS verwenden, um Dial-in-Eigenschaften, die Verarbeitung für das Benutzerkonto in einigen Szenarien können \(wie Dial-in\) und DFÜ-Eigenschaften in anderen Szenarien verarbeiten deaktivieren \(wie z. B. 802.1 X-WLAN und Authentifizieren von Switch\).

Sie können auch **Einwähleigenschaften des Kontos ignorieren** zum Verwalten von Netzwerk-Zugriffssteuerung über Gruppen und die berechtigungseinstellung für den Zugriff auf die Netzwerkrichtlinie. Bei der Auswahl der **Einwähleigenschaften des Kontos ignorieren** Kontrollkästchen Netzwerk-Zugriffsberechtigung für das Benutzerkonto wird ignoriert.

Der einzige Nachteil bei dieser Konfiguration ist, können Sie zusätzliche einwählen Benutzerkontoeigenschaften der Anrufer-ID, Rückruf, statische IP-Adresse und statische Routen verwenden.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
