---
title: Benutzerkontensteuerung (Übersicht)
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 1b7a39cd-fc10-4408-befd-4b2c45806732
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 2729bafe910db6814479464a007ce0e49f8b3205
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638860"
---
# <a name="user-account-control-overview"></a>Benutzerkontensteuerung (Übersicht)
Die Benutzerkontensteuerung (User Account Control, \( UAC) \) ist eine wesentliche Komponente der allgemeinen Sicherheitsvision von Microsoft.  Die Benutzerkontensteuerung trägt dazu bei, die Auswirkungen von Schadsoftware zu reduzieren.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Funktionsbeschreibung
Mithilfe der Benutzerkontensteuerung können sich alle Benutzer an ihren Computern mit einem Standardbenutzerkonto anmelden. Mit einem standardmäßigen Benutzertoken gestartete Prozesse führen möglicherweise Aufgaben unter Verwendung von Zugriffsrechten eines Standardbenutzers aus. Windows-Explorer erbt z. B. automatisch Berechtigungen auf Standardbenutzerebene. Außerdem werden alle Programme, die mit Windows-Explorer ausgeführt werden \( , beispielsweise durch Doppel \- Klicken auf eine Anwendungs Verknüpfung, \) auch mit dem Standardsatz von Benutzerberechtigungen ausgeführt. Viele Anwendungen, einschließlich derjenigen, die im Betriebssystem selbst enthalten sind, sind so konzipiert, dass Sie auf diese Weise ordnungsgemäß funktionieren.

Andere Anwendungen, insbesondere solche, die nicht speziell mit Sicherheitseinstellungen entworfen wurden, erfordern häufig zusätzliche Berechtigungen, um erfolgreich ausgeführt zu werden. Diese Programmtypen werden als Legacy Anwendungen bezeichnet. Darüber hinaus erfordern Aktionen wie das Installieren neuer Software und das vornehmen von Konfigurationsänderungen an Programmen wie der Windows-Firewall mehr Berechtigungen, als für ein Standardbenutzer Konto verfügbar sind.

Wenn eine Anwendung mit mehr als Standardbenutzer Rechten ausgeführt werden muss, kann die Benutzerkontensteuerung weitere Benutzergruppen für das Token wiederherstellen. Dadurch kann der Benutzer die Programme explizit steuern, die auf dem Computer oder Gerät Änderungen auf Systemebene vornehmen.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Der Administrator Genehmigungs Modus in der UAC verhindert, dass böswillige Programme unbeaufsichtigt installiert werden, ohne dass ein Administrator wissen. Außerdem wird der Schutz vor unbeabsichtigten System \- weiten Änderungen unterstützt. Schließlich kann ein höherer Kompatibilitätsgrad erzwungen werden, beim dem Administratoren jedem administrativen Prozess aktiv zustimmen oder dafür Anmeldeinformationen angeben müssen.



