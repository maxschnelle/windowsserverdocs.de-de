---
title: NPS-Vorlagen
description: Dieses Thema enthält eine Übersicht über das Netzwerk Server Vorlagen in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2835959b8c076ef7b6aeb1fca31a62717ef95037
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nps-templates"></a>NPS-Vorlagen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Network Policy Server \(NPS\) Vorlagen ermöglichen Ihnen das Erstellen von Konfigurationselementen, z.B. Remote Authentication Dial-in User Service \(RADIUS\) Clients oder gemeinsame geheime Schlüssel, die Sie auf dem lokalen NPS-Server und für die Verwendung auf anderen Servern NPS Export wiederverwenden können.

NPS-Vorlagen sollen reduzieren die erforderliche Zeit und Kosten, die zum Konfigurieren von NPS auf einem oder mehreren Servern benötigt wird. Die folgenden Arten NPS stehen für die Konfiguration in der Verwaltung von Vorlagen zur Verfügung:

- Gemeinsame geheime Schlüssel
- RADIUS-Clients
- Remote-RADIUS-Server
- IP-Filter
- Wiederherstellungsservergruppen

Konfigurieren einer Vorlage unterscheidet sich den NPS-Server direkt konfigurieren. Erstellen einer Vorlage wirkt sich nicht auf dem NPS-Server-Funktionen. Es ist nur bei Auswahl der Vorlage an der entsprechenden Stelle in der NPS-Konsole, dass die Vorlage Funktionalität des Netzwerkrichtlinienservers auswirkt. 

Wenn Sie einen RADIUS-Client in der NPS-Konsole unter RADIUS-Clients und Servern konfigurieren, haben Sie z.B. die NPS-Serverkonfiguration geändert und erstellt einen Schrittbeim Konfigurieren von NPS für die Kommunikation mit einem der Ihr Netzwerk Access Server \(NAS's\). \ (Werden im nächste Schrittkonfigurieren Sie die NAS zur Kommunikation mit NPS. \) jedoch, wenn Sie eine neue Vorlage für RADIUS-Clients in der NPS-Konsole unter Konfigurieren **Vorlagenverwaltung** anstatt einen neuen RADIUS-Client unter **RADIUS-Clients und Servern**, Sie haben eine Vorlage erstellt, aber Sie haben die NPS-Server-Funktionen nicht noch geändert. Um die Funktionalität des Netzwerkrichtlinienservers ändern möchten, müssen Sie die Vorlage aus der richtigen Stelle in der NPS-Konsole auswählen.

## <a name="creating-templates"></a>Erstellen von Vorlagen

Um eine Vorlage zu erstellen, öffnen Sie die NPS-Konsole der rechten Maustaste auf einen Vorlagentyp, wie z.B. **IP-Filter**, und klicken Sie dann auf **neu**. Ein neue Vorlage Eigenschaftendialogfeld wird geöffnet, mit dem Sie die Vorlage konfigurieren können.

## <a name="using-templates-locally"></a>Lokal mithilfe von Vorlagen

Sie können eine Vorlage, die Sie in erstellt haben **Vorlagenverwaltung** durch Navigieren zu einer Position in der NPS-Konsole, die die Vorlage angewendet werden kann. Wenn beispielsweise Sie eine neue Vorlage für gemeinsame geheime Schlüssel erstellen Sie einen RADIUS-Clientkonfiguration in zuweisen möchten **RADIUS-Clients und Servern** und **RADIUS-Clients**, öffnen Sie die Eigenschaften des RADIUS-Client. In **wählen Sie eine vorhandene Vorlage für gemeinsame geheime Schlüssel**, wählen Sie die Vorlage, die Sie zuvor erstellt, aus der Liste der verfügbaren Vorlagen haben.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
