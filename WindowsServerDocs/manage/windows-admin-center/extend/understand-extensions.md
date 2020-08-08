---
title: Grundlegendes zu Windows Admin Center-Erweiterungen
description: Grundlegendes zu Windows Admin Center SDK Extensions (Project Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 44038185bb4f9cb61920033ce5edc67afb3de99b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964576"
---
# <a name="understanding-windows-admin-center-extensions"></a>Grundlegendes zu Windows Admin Center-Erweiterungen

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Wenn Sie noch nicht mit der Funktionsweise des Windows Admin Centers vertraut sind, beginnen wir mit der Architektur auf hoher Ebene. Das Windows Admin Center besteht aus zwei Hauptkomponenten:

- Der Lightweight- **Webdienst** , der Benutzeroberflächen-Webseiten von Windows Admin Center für Webbrowser Anforderungen bedient.
- Die **Gatewaykomponente** , die Rest-API-Anforderungen von den Webseiten und WMI-aufrufen oder PowerShell-Skripts überwacht, die auf einem Zielserver oder-Cluster ausgeführt werden.

![Architektur des Windows Admin Centers](../media/understand-extensions/wac-architecture-500px.png)

Die Benutzeroberflächen-Webseiten von Windows Admin Center, die vom Webdienst bereitgestellt werden, haben zwei Hauptkomponenten der Benutzeroberfläche aus Erweiterbarkeits Perspektive, Lösungen und Tools, die als Erweiterungen implementiert sind, und einen dritten Erweiterungstyp mit dem Namen "Gateway-Plug-ins".

## <a name="solution-extensions"></a>Projektmappenerweiterungen

Im Windows Admin Center-Startbildschirm können Sie standardmäßig Verbindungen hinzufügen, die einen von vier Typen haben – Windows Server-Verbindungen, Windows-PC-Verbindungen, failoverclusterverbindungen und hyperkonvergierte Cluster Verbindungen. Nachdem eine Verbindung hinzugefügt wurde, werden der Name und Typ der Verbindung auf dem Startbildschirm angezeigt. Wenn Sie auf den Verbindungs Namen klicken, wird versucht, eine Verbindung mit dem Zielserver oder-Cluster herzustellen und dann die Benutzeroberfläche für die Verbindung zu laden.

![Architektur des Windows Admin Centers](../media/understand-extensions/solutions-ui.png)

Jeder dieser Verbindungstypen ist einer Projekt Mappe zugeordnet, und Projektmappen werden durch einen Erweiterungstyp namens "Solution"-Erweiterungen definiert. Lösungen definieren in der Regel einen eindeutigen Objekttyp, den Sie über das Windows Admin Center verwalten möchten, z. b. Server, PCs oder Failovercluster. Sie können auch eine neue Lösung für das Herstellen einer Verbindung mit und die Verwaltung anderer Geräte (z. b. Netzwerk Switches und Linux-Server) oder sogar für Dienste wie Remotedesktopdienste definieren.

## <a name="tool-extensions"></a>Tool Erweiterungen

Wenn Sie auf dem Windows Admin Center-Startbildschirm auf eine Verbindung klicken und verbinden, wird die projektmappenerweiterung für den ausgewählten Verbindungstyp geladen. Anschließend wird die Benutzeroberfläche der Projekt Mappe einschließlich einer Liste von Tools im linken Navigationsbereich angezeigt. Wenn Sie auf ein Tool klicken, wird die Benutzeroberfläche des Tools geladen und im rechten Bereich angezeigt.

![Architektur der Windows Admin Center-Benutzeroberfläche](../media/understand-extensions/ui-architecture.png)

Jedes dieser Tools wird durch einen zweiten Erweiterungstyp namens "Tool" Erweiterungen definiert. Wenn ein Tool geladen wird, kann es WMI-Aufrufe oder PowerShell-Skripts auf einem Zielserver oder-Cluster ausführen und Informationen in der Benutzeroberfläche anzeigen oder Befehle auf der Grundlage von Benutzereingaben ausführen. Eine Tool Erweiterung definiert, für welche Projektmappen Sie angezeigt werden sollen, was zu einem anderen Satz von Tools für jede Lösung führt. Wenn Sie eine neue projektmappenerweiterung erstellen, müssen Sie zusätzlich mindestens eine Tool Erweiterung schreiben, die die Funktionalität für die Lösung bereitstellt.

![Liste der Tools für jede Lösung](../media/understand-extensions/tools-for-solutions.png)

## <a name="gateway-plugins"></a>Plug-ins

Der Gatewaydienst macht Rest-APIs verfügbar, die von der Benutzeroberfläche aufgerufen werden, und Relays Befehle und Skripts, die auf dem Ziel ausgeführt werden. Der Gatewaydienst kann durch Gateway-Plug-ins erweitert werden, die verschiedene Protokolle unterstützen. Das Windows Admin Center ist mit zwei Gateway-Plug-ins vorgepackt, eines zum Ausführen von PowerShell-Skripts und das andere für WMI-Befehle. Wenn Sie mit dem Ziel über ein anderes Protokoll als PowerShell oder WMI (z. b. Rest) kommunizieren müssen, können Sie hierfür ein Gateway-Plug-in erstellen.

## <a name="next-steps"></a>Nächste Schritte

Abhängig von den Funktionen, die Sie im Windows Admin Center erstellen möchten, kann das Erstellen [einer Tool Erweiterung](develop-tool.md) für einen vorhandenen Server oder eine Cluster Lösung ausreichen und ist der einfachste erste Schritt beim Erstellen von Erweiterungen. Wenn Ihr Feature jedoch für die Verwaltung von Geräten, Diensten oder etwas neuer ist, anstatt einen Server oder Cluster, sollten Sie [eine Lösungs Erweiterung](develop-solution.md) mit einem oder mehreren Tools entwickeln. Und schließlich müssen Sie [ein Gateway-Plug](develop-gateway-plugin.md)-in erstellen, wenn Sie mit dem Ziel über ein anderes Protokoll als WMI oder PowerShell kommunizieren müssen. [Lesen Sie weiter](developing-extensions.md) , um zu erfahren, wie Sie Ihre Entwicklungsumgebung einrichten und beginnen, Ihre erste Erweiterung zu schreiben.
