---
title: Mindestens ein Netzwerk für den Live Migrations Datenverkehr muss über eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s verfügen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
ms.date: 8/16/2016
ms.openlocfilehash: cf1f09a635d6f6a46ee2a0bab2de53c898af9084
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746295"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>Mindestens ein Netzwerk für den Live Migrations Datenverkehr muss über eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s verfügen.

>Gilt für: Windows Server 2016



|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Keines der Netzwerke für den Live Migrations Datenverkehr hat eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s.*

## <a name="impact"></a>Auswirkung
*Live Migrationen können langsam erfolgen, was die Netzwerkverbindung aufgrund eines TCP-Verbindungs Timeouts stören könnte.*

## <a name="resolution"></a>Lösung
*Konfigurieren Sie mindestens ein Live Migrationsnetzwerk mit einer Geschwindigkeit von 1 Gbit/s oder schneller.*

Sehen Sie sich die Dokumentation Ihres Netzwerkhardware Herstellers an, um herauszufinden, ob vorhandene Netzwerkadapter eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s unterstützen können.



