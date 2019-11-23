---
title: Benutzerkontensteuerung (Übersicht)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: bdc9f4dc4b8e19d62288f12a4f2b4e8c86b93b68
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403319"
---
# <a name="user-account-control-overview"></a>Benutzerkontensteuerung (Übersicht)
Die Benutzerkontensteuerung \(UAC\) ist eine grundlegende Komponente der allgemeinen Sicherheitsvision von Microsoft.  Die Benutzerkontensteuerung trägt dazu bei, die Auswirkungen von Schadsoftware zu reduzieren.

## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Mithilfe der Benutzerkontensteuerung können sich alle Benutzer an ihren Computern mit einem Standardbenutzerkonto anmelden. Mit einem standardmäßigen Benutzertoken gestartete Prozesse führen möglicherweise Aufgaben unter Verwendung von Zugriffsrechten eines Standardbenutzers aus. Windows-Explorer erbt z. B. automatisch Berechtigungen auf Standardbenutzerebene. Außerdem werden alle Programme, die mithilfe von Windows-\(Explorer ausgeführt werden, beispielsweise durch doppelte\-klicken auf eine Anwendungs Verknüpfung\) auch mit dem Standardsatz von Benutzerberechtigungen ausgeführt. Viele Anwendungen, einschließlich derjenigen, die im Betriebssystem selbst enthalten sind, sind so konzipiert, dass Sie auf diese Weise ordnungsgemäß funktionieren.

Andere Anwendungen, insbesondere solche, die nicht speziell mit Sicherheitseinstellungen entworfen wurden, erfordern häufig zusätzliche Berechtigungen, um erfolgreich ausgeführt zu werden. Diese Programmtypen werden als Legacy Anwendungen bezeichnet. Darüber hinaus erfordern Aktionen wie das Installieren neuer Software und das vornehmen von Konfigurationsänderungen an Programmen wie der Windows-Firewall mehr Berechtigungen, als für ein Standardbenutzer Konto verfügbar sind.

Wenn eine Anwendung mit mehr als Standardbenutzer Rechten ausgeführt werden muss, kann die Benutzerkontensteuerung weitere Benutzergruppen für das Token wiederherstellen. Dadurch kann der Benutzer die Programme explizit steuern, die auf dem Computer oder Gerät Änderungen auf Systemebene vornehmen.

## <a name="BKMK_APP"></a>Praktische Anwendungen
Der Administrator Genehmigungs Modus in der UAC verhindert, dass böswillige Programme unbeaufsichtigt installiert werden, ohne dass ein Administrator wissen. Außerdem wird der Schutz vor unbeabsichtigten System\-weiten Änderungen unterstützt. Schließlich kann ein höherer Kompatibilitätsgrad erzwungen werden, beim dem Administratoren jedem administrativen Prozess aktiv zustimmen oder dafür Anmeldeinformationen angeben müssen.



