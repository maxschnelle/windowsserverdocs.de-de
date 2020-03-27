---
title: Zugriffsberechtigung
description: Dieses Thema bietet einen Überblick über die Netzwerk Richtlinien-Zugriffsberechtigung für den Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d6d1ca5e-bde0-4509-9e14-dc3fa9ff447e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d0521b44eb2b2733ecd8a259c5f9ca25d8bfdef1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315803"
---
# <a name="access-permission"></a>Zugriffsberechtigung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die Zugriffsberechtigung wird auf der Registerkarte " **Übersicht** " jeder Netzwerk Richtlinie auf dem Netzwerk Richtlinien Server (Network Policy Server, NPS) konfiguriert. 

Mit dieser Einstellung können Sie die Richtlinie so konfigurieren, dass Benutzern der Zugriff gewährt oder verweigert wird, wenn die Bedingungen und Einschränkungen der Netzwerk Richtlinie mit der Verbindungsanforderung abgeglichen werden. 

Zugriffs Berechtigungseinstellungen haben folgende Auswirkungen:

- **Gewähren von Zugriff**. Der Zugriff wird gewährt, wenn die Verbindungsanforderung mit den Bedingungen und Einschränkungen übereinstimmt, die in der Richtlinie konfiguriert sind.
- **Verweigern des Zugriffs**. Der Zugriff wird verweigert, wenn die Verbindungsanforderung mit den Bedingungen und Einschränkungen übereinstimmt, die in der Richtlinie konfiguriert sind.

Die Zugriffsberechtigung wird auch basierend auf Ihrer Konfiguration der DFÜ-Eigenschaften der einzelnen Benutzerkonten gewährt oder verweigert.

>[!NOTE]
>Benutzerkonten und deren Eigenschaften, wie z. b. Einwähleigenschaften, werden entweder in der Active Directory Benutzer und Computer oder in der Microsoft-Verwaltungskonsole \(MMC-\)-Snap-in konfiguriert, je nachdem, ob Active Directory&reg; Domänen Dienste (AD DS) installiert sind.

Die Benutzerkonto Einstellung **Netzwerk Zugriffsberechtigung**, die in den Einwähleigenschaften von Benutzerkonten konfiguriert ist, überschreibt die Einstellung für die Zugriffsberechtigung für Netzwerk Richtlinien. Wenn die Netzwerk Zugriffsberechtigung für ein Benutzerkonto auf die **Netzwerk Richtlinien Option Zugriff über NPS Steuern** festgelegt ist, legt die Zugriffs Berechtigungseinstellung für Netzwerk Richtlinien fest, ob dem Benutzer der Zugriff gewährt oder verweigert wird.

>[!NOTE]
>In Windows Server 2016 ist der Standardwert der **Netzwerk Zugriffsberechtigung** in AD DS Benutzerkonto-DFÜ-Eigenschaften die **Zugriffs Steuerung über die NPS-Netzwerk Richtlinie**.

Wenn NPS Verbindungsanforderungen für konfigurierte Netzwerk Richtlinien auswertet, führt es die folgenden Aktionen aus:

- Wenn die Bedingungen der ersten Richtlinie nicht übereinstimmen, wertet NPS die nächste Richtlinie aus und setzt diesen Prozess fort, bis entweder eine Übereinstimmung gefunden wird oder alle Richtlinien für eine Übereinstimmung ausgewertet wurden.
- Wenn die Bedingungen und Einschränkungen einer Richtlinie übereinstimmen, gewährt oder verweigert NPS den Zugriff, je nach dem Wert der Zugriffs Berechtigungseinstellung in der Richtlinie.
- Wenn die Bedingungen einer Richtlinie stimmen, aber die Einschränkungen in der Richtlinie nicht entsprechen, lehnt NPS die Verbindungsanforderung ab.
- Wenn die Bedingungen aller Richtlinien nicht stimmen, lehnt NPS die Verbindungsanforderung ab.

## <a name="ignore-user-account-dial-in-properties"></a>Benutzerkonto-Einwähleigenschaften ignorieren

Sie können die NPS-Netzwerk Richtlinie so konfigurieren, dass die DFÜ-Eigenschaften von Benutzerkonten ignoriert werden, indem Sie auf der Registerkarte "Übersicht" einer Netzwerk Richtlinie auf der Registerkarte " **Übersicht** " das Kontrollkästchen **Benutzerkonto-Einwähleigenschaften ignorieren** 

Wenn NPS die Autorisierung einer Verbindungsanforderung ausführt, überprüft es normalerweise die DFÜ-Eigenschaften des Benutzerkontos, wobei der Wert der Einstellung für die Netzwerk Zugriffsberechtigung sich darauf auswirken kann, ob der Benutzer zum Herstellen einer Verbindung mit dem Netzwerk autorisiert ist. Wenn Sie NPS so konfigurieren, dass die DFÜ-Eigenschaften von Benutzerkonten während der Autorisierung ignoriert werden, legen Netzwerk Richtlinien Einstellungen fest, ob dem Benutzer Zugriff auf das Netzwerk gewährt wird.

Die Eigenschaften der einwählenden Benutzerkonten enthalten Folgendes:

- Netzwerk Zugriffsberechtigung
- Anrufer-ID
- Rückruf Optionen
- Statische IP-Adresse
- Statische Routen

Um mehrere Typen von Verbindungen zu unterstützen, für die NPS Authentifizierung und Autorisierung bereitstellt, kann es erforderlich sein, die Verarbeitung der Einwähleigenschaften des Benutzerkontos zu deaktivieren. Dies kann dazu dienen, Szenarios zu unterstützen, in denen bestimmte Einwähleigenschaften nicht erforderlich sind.

Die Eigenschaften "Aufrufer-ID", "Rückruf", "statische IP-Adresse" und "statische Routen" sind z. b. für einen Client konzipiert, der sich in einem Netzwerk Zugriffs Server \(NAS\)befindet, nicht für Clients, die eine Verbindung mit drahtlos Zugriffs Punkten herstellen. Ein drahtloser Zugriffspunkt, der diese Einstellungen in einer RADIUS-Nachricht von NPS empfängt, kann diese möglicherweise nicht verarbeiten, was dazu führen kann, dass der drahtlose Client getrennt wird.

Wenn NPS Authentifizierung und Autorisierung für Benutzer bereitstellt, die sich auf Ihr Unternehmensnetzwerk über drahtlos Zugriffspunkte einwählen und auf Ihr Unternehmensnetzwerk zugreifen möchten, müssen Sie die DFÜ-Eigenschaften so konfigurieren, dass die DFÜ-Verbindungen unterstützt werden \(indem Sie die Einwähleigenschaften\) oder drahtlos Verbindungen \(festlegen, indem Sie die DFÜ-Eigenschaften nicht\).

Sie können NPS verwenden, um die Verarbeitung der DFÜ-Eigenschaften für das Benutzerkonto in einigen Szenarios zu aktivieren \(z. b. das Einwähl\) und die Verarbeitung der DFÜ-Eigenschaften in anderen Szenarien \(wie z. b. 802.1 x drahtlos und Authentifizieren von Switch\).

Sie können auch die DFÜ **-Eigenschaften Benutzerkonto ignorieren** verwenden, um die Netzwerk Zugriffs Steuerung über Gruppen und die Zugriffs Berechtigungseinstellung für die Netzwerk Richtlinie zu verwalten. Wenn Sie das Kontrollkästchen **Benutzerkonto-Einwähleigenschaften ignorieren** aktivieren, wird die Netzwerk Zugriffsberechtigung für das Benutzerkonto ignoriert.

Der einzige Nachteil bei dieser Konfiguration besteht darin, dass Sie die zusätzlichen Benutzerkonto-Einwähleigenschaften von Aufrufer-ID, Rückruf, statischer IP-Adresse und statischen Routen nicht verwenden können.

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
