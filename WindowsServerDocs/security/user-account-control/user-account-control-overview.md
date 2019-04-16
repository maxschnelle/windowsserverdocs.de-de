---
title: User Account Control Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tpm
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b7a39cd-fc10-4408-befd-4b2c45806732
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 90ce72cb3d1850563d16a12d09a6872d107c0690
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="user-account-control-overview"></a>User Account Control Overview
User Account Control \(UAC\) ist ein grundlegender Baustein der gesamtsicherheitsvision von Microsoft.  Benutzerkontensteuerung trägt dazu bei, die Auswirkungen von Schadsoftware zu reduzieren.

## <a name="BKMK_OVER"></a>Featurebeschreibung
UAC ermöglicht allen Benutzern auf ihren Computern mit einem Standardbenutzerkonto anmelden. Mit einem standardmäßigen Benutzertoken gestartete Prozesse können mithilfe von Zugriffsrechten eines Standardbenutzers Aufgaben ausführen. Windows-Explorer erbt z. B. automatisch Berechtigungen auf standardbenutzerebene. Darüber hinaus alle Programme, die ausgeführt werden, mithilfe von Windows Explorer \ (z. B. durch einen doppelten Klick eine Anwendung Shortcut\) auch mit dem Standardsatz von Benutzerberechtigungen ausgeführt. Viele Anwendungen, einschließlich derer, die das Betriebssystem selbst integriert werden sollen auf diese Weise ordnungsgemäß funktionieren.

Andere Anwendungen, insbesondere solche, die nicht speziell mit Sicherheitseinstellungen, denken Sie daran, entworfen wurden, erfordern häufig zur erfolgreichen Ausführung zusätzliche Berechtigungen. Diese Art von Programmen werden als legacy-Anwendungen bezeichnet. Darüber hinaus erfordern Aktionen wie das Installieren neuer Software und Ändern der Konfiguration auf Programme, z. B. Windows-Firewall mehr Berechtigungen als ein Standardbenutzerkonto verfügbar ist.

Wenn ein Anwendungen muss mit mehr als den Standardbenutzerrechten ausgeführt wird, kann UAC zusätzliche Benutzergruppen für das Token wiederherstellen. Dies ermöglicht die Benutzer explizit die Kontrolle der Programme, die die auf Systemebene Änderungen am Computer oder Gerät vornehmen.

## <a name="BKMK_APP"></a>In der Praxis
Administratorbestätigungsmodus in UAC wird verhindert, dass Schadsoftware automatisch installiert wird, ohne ein Administrator wissen. Darüber hinaus Schutz vor unbeabsichtigten systemweiten Änderungen. Schließlich kann es ein höheres Maß an Kompatibilität erzwingen, in denen Administratoren müssen aktiv Zustimmung oder Anmeldeinformationen jedem administrativen Prozess, verwendet werden.



