---
title: Verwalten von NPS-Vorlagen
description: Dieses Thema enthält Anweisungen zum Erstellen, anwenden, exportieren und Importieren von NPS-Vorlagen für Netzwerkrichtlinienserver in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 989b00c5-4767-4081-ace5-6321f8b2c55e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0a7f4c50d87c155c1adcd445eae8df23aab7730b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-nps-templates"></a>Verwalten von NPS-Vorlagen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können Netzwerkrichtlinienserver \(NPS\) Vorlagen verwenden, Erstellen von Konfigurationselementen, z.B. Remote Authentication Dial-in User Service \(RADIUS\) Clients oder gemeinsame geheime Schlüssel, die Sie auf dem lokalen NPS-Server und für die Verwendung auf anderen Servern NPS Export wiederverwenden können. 

Vorlagen bietet einen Knoten in der NPS-Konsole, in dem Sie können erstellen, ändern, löschen, duplizieren und die Verwendung von NPS-Vorlagen anzeigen. NPS-Vorlagen sollen reduzieren die erforderliche Zeit und Kosten, die zum Konfigurieren von NPS auf einem oder mehreren Servern benötigt wird.

Die folgenden Arten NPS stehen für die Konfiguration in der Verwaltung von Vorlagen zur Verfügung.

- **Gemeinsame geheime Schlüssel**. Diesen Vorlagentyp ermöglicht es Ihnen, einen gemeinsamen geheimen Schlüssel angeben, die Sie (durch die Auswahl der Vorlage an der entsprechenden Stelle in der NPS-Konsole) wiederverwenden können beim Konfigurieren von RADIUS-Clients und Servern. 

- **RADIUS-Clients**. Diese Art von Vorlage ermöglicht es für Sie RADIUS-Clienteinstellungen zu konfigurieren, die Sie wiederverwenden können, durch die Auswahl der Vorlage an der entsprechenden Stelle in der NPS-Konsole.

- **Remote-RADIUS-Servern**. Diese Vorlage ermöglicht es für Sie Remoteeinstellungen RADIUS-Server zu konfigurieren, die Sie wiederverwenden können, durch die Auswahl der Vorlage an der entsprechenden Stelle in der NPS-Konsole. 

- **IP-Filter**. Diese Vorlage ermöglicht Ihnen, Internet Protocol Version 4 (IPv4) und Internet Protocol Version 6 \(IPv6\) Filter erstellen, die Sie wiederverwenden können \ (durch die Auswahl der Vorlage an der entsprechenden Stelle in der NPS-Console\) Wenn Sie die Netzwerkrichtlinien konfigurieren.

## <a name="create-an-nps-template"></a>Erstellen Sie eine NPS-Vorlage

Konfigurieren einer Vorlage unterscheidet sich den NPS-Server direkt konfigurieren. Erstellen einer Vorlage wirkt sich nicht auf dem NPS-Server-Funktionen. Es ist nur, wenn Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen und wenden Sie die Vorlage, dass die Vorlage Funktionalität des Netzwerkrichtlinienservers auswirkt. 

Beispielsweise, wenn Sie einen RADIUS-Client in der NPS-Konsole unter Konfigurieren **RADIUS-Clients und Servern**, Sie ändern die NPS-Serverkonfiguration und nutzen Sie einen Schrittbeim Konfigurieren von NPS für die Kommunikation mit einem der Server für den Netzwerkzugriff. \ (Im nächste Schrittwird so konfigurieren Sie Netzwerkzugriffsserver \(NAS\) zur Kommunikation mit NPS. \) 

Jedoch, wenn Sie ein neues konfigurieren **RADIUS-Clients** Vorlage in der NPS-Konsole unter **Vorlagenverwaltung** anstatt einen neuen RADIUS-Client unter **RADIUS-Clients und Servern**, Sie haben eine Vorlage erstellt, aber Sie haben die NPS-Server-Funktionen nicht noch geändert. Um die Funktionalität des Netzwerkrichtlinienservers ändern möchten, müssen Sie die Vorlage aus der richtigen Stelle in der NPS-Konsole anwenden.

Das folgende Verfahren bietet Anweisungen zum Erstellen einer neuen Vorlage.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-create-an-nps-template"></a>So erstellen Sie eine NPS-Vorlage


1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet. 

2. Erweitern Sie in der NPS-Konsole **Vorlagenverwaltung**, mit der rechten Maustaste beispielsweise auf eines Vorlagentyp **RADIUS-Clients**, und klicken Sie dann auf **neu**.

3. Ein neue Vorlage Eigenschaftendialogfeld wird geöffnet, dass Sie so konfigurieren Sie die Vorlage verwenden können.

## <a name="apply-an-nps-template"></a>Eine NPS-Vorlage anwenden

Sie können eine Vorlage, die Sie erstellt haben **Vorlagenverwaltung** durch Navigieren zu einer Position in der NPS-Konsole, in dem Sie die Vorlage anwenden können. Wenn Sie eine Vorlage für die gemeinsame geheime Schlüssel auf einem RADIUS-Clientkonfiguration anwenden möchten, können Sie das folgende Verfahren verwenden.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-apply-an-nps-template"></a>Eine NPS-Vorlage angewendet

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Erweitern Sie in der NPS-Konsole **RADIUS-Clients und Servern**, und erweitern Sie dann **RADIUS-Clients**.

3. In **RADIUS-Clients**, klicken Sie im Detailbereich mit der Maustaste des RADIUS-Clients, Sie möchten die NPS-Vorlage anwenden, und klicken Sie dann auf **Eigenschaften**.

4. Das Dialogfeld "Eigenschaften" im Feld für den RADIUS-Client im **wählen Sie eine vorhandene Vorlage für gemeinsame geheime Schlüssel**, wählen Sie die Vorlage, die Sie aus der Liste der Vorlagen anwenden möchten.

## <a name="export-or-import-nps-templates"></a>Export oder Import NPS-Vorlagen

Sie können Vorlagen für die Verwendung auf anderen NPS-Server exportieren, oder Sie können Vorlagen in importieren **Vorlagenverwaltung** für die Verwendung auf dem lokalen Computer. 

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-export-or-import-nps-templates"></a>Zum Exportieren und Importieren von NPS-Vorlagen

1. So exportieren Sie NPS-Vorlagen in der NPS-Konsole mit der rechten Maustaste **Vorlagenverwaltung**, und klicken Sie dann auf **Vorlagen in Datei exportieren**.

2. Importieren von NPS-Vorlagen in der NPS-Konsole mit der rechten Maustaste **Vorlagenverwaltung**, und klicken Sie dann auf **Vorlagen importieren, von einem Computer** oder **Vorlagen aus Datei importieren**.


