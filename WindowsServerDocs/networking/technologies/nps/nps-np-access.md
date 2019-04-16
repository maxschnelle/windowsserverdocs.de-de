---
title: Zugriffsberechtigung
description: Dieses Thema enthält eine Übersicht über die Netzwerkzugriffsberechtigungen der Richtlinie für Netzwerkrichtlinienserver in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d6d1ca5e-bde0-4509-9e14-dc3fa9ff447e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: aeacfaeb159598d2e53bac29fb09ffc3e7739476
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="access-permission"></a>Zugriffsberechtigung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Berechtigung ist konfiguriert, auf die **(Übersicht)** jede Netzwerkrichtlinie in den Netzwerkzugriffsschutz (Network Policy Server, NPS) auf der Registerkarte. 

Mit dieser Einstellung können Sie konfigurieren die Richtlinie zum gewähren oder Verweigern des Zugriffs auf Benutzer, wenn die Bedingungen und Einschränkungen der Netzwerkrichtlinie die Verbindungsanforderung zugeordnet sind. 

Einstellungen für den Zugriff über die Berechtigung verfügen, hat folgende Auswirkung:

- **Zugriff gewähren**. Zugriff wird gewährt, wenn die Verbindungsanforderung übereinstimmt, die Bedingungen und Einschränkungen, die in der Richtlinie konfiguriert sind.
- **Verweigern des Zugriffs**. Wenn die Verbindungsanforderung übereinstimmt, die Bedingungen und Einschränkungen, die in der Richtlinie konfiguriert sind, wird der Zugriff verweigert.

Zugriffsrechte gewährt oder verweigert basierend auf Ihrer Konfiguration der Dial-in Eigenschaften der einzelnen Benutzerkonten.

>[!NOTE]
>Benutzerkonten und deren Eigenschaften, z.B. DFÜ-Eigenschaften, werden in entweder das Active Directory-Benutzer und -Computer oder lokale Benutzer und Gruppen Microsoft Management Console \(MMC\) Snap-In, je nachdem, ob Active Directory ist konfiguriert&reg; -Domänendienste (AD DS) installiert.

Die benutzerkontoeinstellung **Netzwerkzugriffsberechtigungen**, die auf die DFÜ-Eigenschaften von Benutzerkonten konfiguriert ist, überschreibt die Netzwerkrichtlinie Zugriffsberechtigung festlegen. Wenn die Netzwerkzugriffsberechtigungen für ein Benutzerkonto festgelegt ist, um die **steuern den Zugriff über die NPS-Netzwerkrichtlinien** Option der Netzwerk-Richtlinie Zugriff über die Berechtigung legen Sie fest, ob der Benutzer wird Zugriff gewährt oder verweigert.

>[!NOTE]
>In Windows Server2016, der Standardwert von **Netzwerkzugriffsberechtigungen** in AD DS-Einwahl Eigenschaften des Benutzerkontos ist **steuern den Zugriff über die NPS-Netzwerkrichtlinien**.

Ergibt NPS Verbindungsanforderungen konfigurierten Netzwerkrichtlinien, werden die folgenden Aktionen ausgeführt:

- Wenn die Bedingungen für die erste Richtlinie nicht übereinstimmen, wird NPS wertet die nächste Richtlinie, und dieser Prozess wird fortgesetzt, bis entweder eine Übereinstimmung gefunden wird, oder alle Richtlinien für eine Übereinstimmung ausgewertet wurden.
- Wenn die Bedingungen und Einschränkungen einer Richtlinie übereinstimmen, NPS gewährt oder verweigert den Zugriff, abhängig vom Wert für die Einstellung "Berechtigungen" in der Richtlinie.
- Wenn die Bedingungen für eine richtlinienübereinstimmung jedoch die Einschränkungen in der Richtlinie nicht übereinstimmen, lehnt NPS die Verbindungsanforderung ab.
- Wenn die Bedingungen für alle Richtlinien nicht übereinstimmen, lehnt NPS die Verbindungsanforderung ab.

## <a name="ignore-user-account-dial-in-properties"></a>Ignorieren Sie DFÜ-Eigenschaften des Kontos

Sie können konfigurieren, dass NPS-Netzwerkrichtlinien, um die DFÜ-Eigenschaften von Benutzerkonten zu ignorieren, durch Aktivieren oder Deaktivieren der **ignorieren DFÜ-Eigenschaften des Benutzerkontos** auf das Kontrollkästchen der **(Übersicht)** eine Netzwerkrichtlinie auf der Registerkarte. 

Bei Genehmigung der Anforderung eine Verbindung von NPS ausgeführt wird, überprüft normalerweise die DFÜ-Eigenschaften des Benutzerkontos, in denen die Netzwerkzugriffsberechtigungen Wert auswirken können, ob der Benutzer berechtigt ist, eine Verbindung mit dem Netzwerk herstellen. Wenn Sie NPS, ignorieren die DFÜ-Eigenschaften von Benutzerkonten im Rahmen der Autorisierung konfigurieren, bestimmen Netzwerkrichtlinien, ob der Benutzer Zugriff auf das Netzwerk gewährt wird.

Die DFÜ-Eigenschaften von Benutzerkonten enthalten Folgendes:

- Netzwerk-Berechtigungen
- Anrufer-ID
- Rückrufoptionen
- Statische IP-Adresse
- Statische Routen

Um mehrere Arten von Verbindungen unterstützen, für die NPS-Authentifizierung und Autorisierung bereitstellt, kann es erforderlich, deaktivieren die Verarbeitung von DFÜ-Eigenschaften des Kontos sein. Dies kann erfolgen, um Szenarien zu unterstützen, in denen bestimmte Eigenschaften nicht erforderlich sind.

Zeigt \(NAS\), z.B. den Anrufer-ID, Rückruf, statische IP-Adresse, und statische Routen, die Eigenschaften für einen Client entworfen werden, die einen Netzwerkzugriffsserver Einwählen ist nicht für Clients, die mit WLAN verbinden. Ein drahtlosen Zugriffspunkt, der diese Einstellungen in einer RADIUS-Nachricht vom Netzwerkrichtlinienserver empfängt möglicherweise nicht verarbeiten, wodurch der Drahtlosclient getrennt werden kann.

Wenn NPS ermöglicht die Authentifizierung und Autorisierung für Benutzer, die sowohl einwählen und Zugriff auf das Netzwerk Ihrer Organisation über WLAN-Zugangspunkten sind, müssen Sie konfigurieren, dass die DFÜ-Eigenschaften zur Unterstützung von beiden DFÜ-Verbindungen \ (durch Festlegen einwählen Properties\) oder drahtlose Verbindung \ (mit Nicht-Einwahl Properties\).

Sie können NPS DFÜ-Eigenschaften für das Benutzerkonto in einigen Szenarien Verarbeitung ermöglichen \ (z.B. DFÜ-Taste) und So deaktivieren Sie DFÜ-Eigenschaften in anderen Szenarien Verarbeitung \ (z.B. 802. 1 X und -Authentifizierungsswitch Switch\).

Können Sie auch **ignorieren DFÜ-Eigenschaften des Benutzerkontos** Netzwerkzugriffsteuerung über Gruppen und die Einstellung für die Netzwerkrichtlinie verwalten. Bei Auswahl der **ignorieren DFÜ-Eigenschaften des Benutzerkontos** Kontrollkästchen, die Netzwerkzugriffsberechtigungen für das Benutzerkonto wird ignoriert.

Der einzige Nachteil dieser Konfiguration ist, dass Sie die zusätzliche Dial-Eigenschaften des Benutzerkontos der Anrufer-ID, Rückruf, statische IP-Adresse und statische Routen verwenden können.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
