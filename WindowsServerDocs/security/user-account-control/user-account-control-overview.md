---
title: Benutzerkontensteuerung (Übersicht)
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887671"
---
# <a name="user-account-control-overview"></a>Benutzerkontensteuerung (Übersicht)
Der Benutzerkontensteuerung \(UAC\) ist eine grundlegende Komponente der übergreifenden Sicherheitsvision von Microsoft.  Die Benutzerkontensteuerung trägt dazu bei, die Auswirkungen von Schadsoftware zu reduzieren.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Mithilfe der Benutzerkontensteuerung können sich alle Benutzer an ihren Computern mit einem Standardbenutzerkonto anmelden. Mit einem standardmäßigen Benutzertoken gestartete Prozesse führen möglicherweise Aufgaben unter Verwendung von Zugriffsrechten eines Standardbenutzers aus. Windows-Explorer erbt z. B. automatisch Berechtigungen auf Standardbenutzerebene. Darüber hinaus auf alle Programme, die ausgeführt werden, mit dem Windows-Explorer \(z. B. durch doppelte\-auf eine anwendungsverknüpfung\) auch mit den Standardsatz von Benutzerberechtigungen ausgeführt. Viele Anwendungen, einschließlich derjenigen, die mit dem Betriebssystem selbst eingeschlossen werden sollen ordnungsgemäß auf diese Weise funktioniert.

Andere Anwendungen, besonders solche, die mit Sicherheitseinstellungen, denken Sie daran, nicht speziell entwickelt wurden, erfordern häufig zusätzliche Berechtigungen für die erfolgreiche Ausführung. Diese Arten von Programmen sind ältere Anwendungen genannt. Darüber hinaus müssen Aktionen wie das Installieren neuer Software oder konfigurationsänderungen auf Programme, z. B. Windows-Firewall, mehr Berechtigungen als ein Standardbenutzerkonto zur Verfügung.

Wenn ein Anwendungen muss mit mehr als standardmäßigen Benutzerberechtigungen ausgeführt werden, kann zusätzliche Benutzergruppen von UAC auf das Token wiederherstellen. Dadurch kann der Benutzer damit explizite Kontrolle über Programme, die auf Änderungen am Informationssystem auf ihren Computer oder Gerät erfolgen.

## <a name="BKMK_APP"></a>Praktische Anwendungen
Admin Approval Mode in die Benutzerkontensteuerung verhindert, dass böswillige Programme im Hintergrund ohne Kenntnis der eines Administrators installiert. Auch dadurch verhindern versehentliches System\-große Änderungen. Schließlich kann ein höherer Kompatibilitätsgrad erzwungen werden, beim dem Administratoren jedem administrativen Prozess aktiv zustimmen oder dafür Anmeldeinformationen angeben müssen.



