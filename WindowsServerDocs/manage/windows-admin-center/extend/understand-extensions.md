---
title: Grundlegendes zu Windows Admin Center-Erweiterungen
description: Grundlegendes zu Windows Admin Center SDK-Erweiterungen (Projekt Honolulu)
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b00ee847088d038e59266154bcbbe9499bfe47fa
ms.sourcegitcommit: 4b9b21ca1f366388a78ead7413cb581f2b23d4c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "2712095"
---
# Grundlegendes zu Windows Admin Center-Erweiterungen

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Falls Sie noch nicht mit der Funktionsweise von Windows Admin Center vertraut sind, beginnen wir mit der allgemeinen Architektur: Windows Admin Center besteht aus zwei Hauptkomponenten:

- Einfacher **Webdienst**, der Webseiten von Windows Admin Center-Benutzeroberflächen für Webbrowseranforderungen dient.
- **Gateway-Komponente**, die REST-API-Anforderungen von Webseiten überwacht und WMI-Aufrufe oder PowerShell-Skripts aufruft, um auf einem Zielserver oder einem Cluster ausgeführt zu werden.

![Windows Admin Center-Architektur](../media/understand-extensions/wac-architecture-500px.png)

Die vom Webdienst bedienten Webseiten der Windows Admin Center-Benutzeroberfläche besteht aus zwei UI Komponenten aus Sicht der Erweiterbarkeit, Lösungen und Tools, die als Erweiterungen implementiert werden, und einem dritten Erweiterungstyp der Gateway-Plug-In genannt wird.

## Erweiterungen für Lösungen

In der Windows Admin Center-Startseite können Sie in der Standardeinstellung vier Typen von Verbindungen hinzufügen – Windows Server-Verbindungen, Windows-PC-Verbindungen, Failoverclusterverbindungen und hyperkonvergente Clusterverbindungen. Nachdem eine Verbindung hinzugefügt wird, wird der Verbindungsname und der Typ in der Startseite angezeigt. Durch Klicken auf den Verbindungsnamen wird versucht, eine Verbindung mit dem Zielserver oder Cluster zu erstellen und die Benutzeroberfläche für die Verbindung hochzuladen.

![Windows Admin Center-Architektur](../media/understand-extensions/solutions-ui.png)

Jeder dieser Verbindungstypen ist einer Lösung zugeordnet und Lösungen werden über einen Typ der Erweiterung mit dem Namen "Lösung"-Erweiterungen definiert. Lösungen definieren normalerweise einen eindeutigen Objekttyp, das Sie über Windows Admin Center verwalten, wie Server, PCs oder Failovercluster. Sie können auch eine neue Lösung zum Verbinden mit und Verwalten von anderen Geräten wie Netzwerkswitches und Linux-Server oder sogar Diensten wie Remotedesktopdienste definieren.

## Tool-Erweiterungen

Wenn Sie auf eine Verbindung auf der Startseite im Windows Admin Center klicken und eine Verbindung herstellen, wird die Erweiterung der Lösung für den ausgewählten Verbindungstyp geladen, und wer wird mit der Lösungs-Benutzeroberfläche einschließlich einer Liste der Tools im linken Navigationsbereich angezeigt. Wenn Sie auf ein Tool klicken, wird die Tool-UI geladen und im rechten Bereich angezeigt.

![Windows Admin Center UI-Architektur](../media/understand-extensions/ui-architecture.png)

Alle diese Tools werden durch einen zweiten Typ der Erweiterung mit dem Namen "Tools"-Erweiterungen definiert. Wenn ein Tool geladen wird, können sie WMI-Aufrufe oder PowerShell-Skripts auf einem Zielserver oder Cluster ausführen und Informationen in der Benutzeroberfläche anzeigen oder basierend auf Benutzereingaben Befehle ausführen. Erweiterung Tool definiert, welche Lösungen, angezeigt werden sollte sich ergebenden in einen anderen Satz von Tools für jede bereitzustellende Lösung. Wenn Sie eine neue Lösungserweiterung erstellen, müssen Sie außerdem einen oder mehrere Tool-Erweiterungen schreiben, die Funktionen für die Lösung bereitstellen.

![Liste der Tools für jede bereitzustellende Lösung](../media/understand-extensions/tools-for-solutions.png)

## Gateway-Plug-Ins

Der Gatewaydienst macht REST-APIs für die Benutzeroberfläche verfügbar und leitet Befehle und Skripts auf den Zielcomputer. Der Gatewaydienst kann von Gateway-Plug-Ins erweitert werden, die verschiedene Protokolle unterstützen. Windows Admin Center ist vorkonfigurierte mit zwei Gateway-Plug-Ins, eins für PowerShell-Skripts und das andere für WMI-Befehle. Wenn Sie mit dem Ziel über ein anderes Protokoll als PowerShell oder WMI kommunizieren, wie etwa REST, können Sie ein Gateway-Plug-In für dieses erstellen.

## Nächste Schritte

Je nachdem, welche Funktionen Sie in Windows Admin Center erstellen, reicht das [Erstellen einer Tool-Erweiterung](develop-tool.md) für einen vorhandenen Server oder Clusterlösungen möglicherweise aus, und es ist am einfachsten, zunächst die Erweiterungen zu erstellen. Wenn die Funktion für die Verwaltung eines Geräts, Services oder eines vollständig neuen Dienstes anstatt eines Servers oder Clusters ist, sollten Sie [eine Lösungserweiterung](develop-solution.md) mit einem oder mehreren Tools erstellen. Wenn Sie mit dem Ziel über ein anderes Protokoll als WMI-Filterung oder PowerShell kommunizieren, müssen Sie [ein Gateway-Plug-In erstellen](develop-gateway-plugin.md). [Lesen Sie weiter](developing-extensions.md) für Informationen zum Einrichten Ihrer Entwicklungsumgebung und zum Schreiben der ersten Erweiterung.