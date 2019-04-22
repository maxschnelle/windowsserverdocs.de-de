---
title: NPS-Vorlagen
description: Dieses Thema enthält eine Übersicht über Network Policy Server-Vorlagen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0647dbf0f99a01e32ba68475b439501e2dbeebfe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823311"
---
# <a name="nps-templates"></a>NPS-Vorlagen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Netzwerkrichtlinienserver \(NPS\) Vorlagen ermöglichen Ihnen die Erstellung der Konfigurationselemente, z. B. Remote Authentication Dial-in User Service \(RADIUS\) Clients oder freigegebene geheime Daten, die auf dem lokalen wiederverwendet werden können NPS und Export für die Verwendung auf anderen NPSs.

NPS-Vorlagen dienen zum Verringern der Anzahl der Zeit- und Kostenaufwand, die zum Konfigurieren von NPS auf einem oder mehreren Servern benötigt. Die folgenden Typen der NPS-Vorlagen stehen für die Konfiguration in der Verwaltung von Vorlagen zur Verfügung:

- Gemeinsamen geheimen Schlüssel
- RADIUS-Clients
- Remote-RADIUS-Server
- IP-Filter
- Wiederherstellungsservergruppen

Konfigurieren einer Vorlage unterscheidet sich von den NPS direkt konfigurieren. Erstellen einer Vorlage wirkt sich nicht auf den NPS Funktionen aus. Es ist nur bei Auswahl der Vorlage in die entsprechende Position in der NPS-Konsole, dass die Vorlage die NPS-Funktionalität auswirkt. 

Z. B. Wenn Sie einen RADIUS-Client in der NPS-Konsole unter RADIUS-Clients und Servern konfigurieren, Sie haben die NPS-Konfiguration geändert und einen Schritt zum Konfigurieren von NPS für die Kommunikation mit einem der Server für den Netzwerkzugriff \(NAS\) . \(Im nächste Schritt muss das NAS für die Kommunikation mit NPS konfiguriert werden.\) Jedoch wenn Sie eine neue Vorlage für RADIUS-Clients, in der Konsole "NPS" unter Konfigurieren **Vorlagenverwaltung** anstatt zu einer neuen RADIUS-Clients unter Erstellen **RADIUS-Clients und Servern**, Sie erstellt haben eine Vorlage, aber Sie haben die NPS-Funktionen nicht noch geändert. Um die NPS-Funktionalität ändern, müssen Sie die Vorlage von der richtigen Position in der NPS-Konsole auswählen.

## <a name="creating-templates"></a>Erstellen von Vorlagen

Um eine Vorlage zu erstellen, öffnen Sie die NPS-Konsole der rechten Maustaste auf eines Vorlagentyps der Form, wie z. B. **IP-Filter**, und klicken Sie dann auf **neu**. Ein neues Vorlage Eigenschaften-Dialogfeld wird geöffnet, die Ihnen ermöglicht, Ihre Vorlage zu konfigurieren.

## <a name="using-templates-locally"></a>Lokal mithilfe von Vorlagen

Sie können eine Vorlage, die Sie in erstellt haben **Vorlagenverwaltung** durch Navigieren zu einem Speicherort in der NPS-Konsole, die Vorlage angewendet werden kann. Z. B. Wenn Sie eine neue Vorlage für freigegebene geheime Schlüssel, die erstellen Sie an einen RADIUS-Client-Konfiguration in anwenden möchten **RADIUS-Clients und Servern** und **RADIUS-Clients**, öffnen Sie die RADIUS-Client-Eigenschaften. In **auswählen eine vorhandene Vorlage für freigegebene geheime Schlüssel**, wählen Sie die Vorlage, die Sie zuvor erstellt, aus der Liste der verfügbaren Vorlagen haben.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
