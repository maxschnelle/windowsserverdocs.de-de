---
title: Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)
description: Hier findest du eine Übersicht über die Clientlizenzierung in den Remotedesktopdiensten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5be6546b-df16-4475-bcba-aa75aabef3e3
author: lizap
ms.author: elizapo
ms.date: 09/20/2018
manager: dongill
ms.openlocfilehash: 0254c03396cba69a86eed021319ca2e2483ca625
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743863"
---
# <a name="license-your-rds-deployment-with-client-access-licenses-cals"></a>Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Jeder Benutzer und jedes Gerät, der bzw. das eine Verbindung mit einem Remotedesktop-Sitzungshost herstellt, benötigt eine Clientzugriffslizenz (Client Access License, CAL). Zum Installieren, Ausstellen und Nachverfolgen der RDS-CALs verwendest du die RD-Lizenzierung.  

Wenn ein Benutzer oder ein Gerät eine Verbindung mit einem RD-Sitzungshostserver herstellt, bestimmt der RD-Sitzungshostserver, ob eine RDS-CAL benötigt wird. Der RD-Sitzungshostserver fordert dann eine RDS-CAL vom Remotedesktop-Lizenzserver an. Wenn eine geeignete RDS-CAL auf einem Lizenzserver verfügbar ist, wird die RDS-CAL für den Client ausgestellt, und der Client kann eine Verbindung mit dem RD-Sitzungshostserver und von dort aus mit den Desktops oder Apps herstellen, die verwendet werden sollen.

Es gibt zwar eine Lizenzierungskarenzzeit, in der kein Lizenzserver erforderlich ist, nach Ablauf dieses Zeitraums müssen die Clients aber eine gültige RDS-CAL von einem Lizenzserver erhalten, bevor sie sich bei einem RD-Sitzungshostserver anmelden können.

Verwende die folgenden Informationen, um zu erfahren, wie die Clientzugriffslizenzierung in den Remotedesktopdiensten funktioniert, und um deine Lizenzen bereitzustellen und zu verwalten:

- [Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)](#license-your-rds-deployment-with-client-access-licenses-cals)
  - [Grundlegendes zum Modell der Clientzugriffslizenzen](#understanding-the-cals-model)
  - [Hinweis zu CAL-Versionen](#note-about-cal-versions)

## <a name="understanding-the-cals-model"></a>Grundlegendes zum Modell der Clientzugriffslizenzen

Es gibt zwei Typen von CALs:

- RDS-CALs pro Gerät
- RDS-CALs pro Benutzer

Die folgende Tabelle zeigt die Unterschiede zwischen den beiden CAL-Typen:

| Pro Gerät                                                     | Pro Benutzer                                                                         |
|----------------------------------------------------------------|----------------------------------------------------------------------------------|
| CALs werden jedem Gerät physisch zugewiesen.                   | CALs werden einem Benutzer in Active Directory zugewiesen.                                 |
| CALs werden vom Lizenzserver nachverfolgt.                        | CALs werden vom Lizenzserver nachverfolgt.                                          |
| CALs können unabhängig von der Mitgliedschaft in Active Directory nachverfolgt werden. | CALs können innerhalb einer Arbeitsgruppe nicht nachverfolgt werden.                                       |
| Du kannst bis zu 20 % der CALs widerrufen.                              | Du kannst keine CALs widerrufen.                                                      |
| Temporäre CALs sind 52–89 Tage lang gültig.                       | Es sind keine temporären CALs verfügbar.                                                |
| CALs können nicht überprovisioniert werden.                                  | CALs können überprovisioniert werden (entgegen der Remotedesktop-Lizenzvereinbarung). |

Bei Verwendung des Pro-Gerät-Modells wird eine temporäre Lizenz ausgestellt, wenn ein Gerät zum ersten Mal eine Verbindung mit dem Remotedesktop-Sitzungshost herstellt. Bei der zweiten Verbindungsherstellung stellt der Lizenzserver eine permanente RDS-CAL pro Gerät aus, sofern der Server aktiviert ist und CALs verfügbar sind.

Wenn du das Pro-Benutzer-Modell verwendest, wird die Lizenzierung nicht erzwungen, und jedem Benutzer wird eine Lizenz erteilt, mit der er von einer beliebigen Anzahl von Geräten aus eine Verbindung mit einem Remotedesktop-Sitzungshost herstellen kann. Der Lizenzserver stellt Lizenzen aus dem verfügbaren CAL-Pool oder dem CAL-Pool „Überbeansprucht“ aus. Du musst sicherstellen, dass all deine Benutzer eine gültige Lizenz und keine CALs aus dem Pool „Überbeansprucht“ besitzen– andernfalls liegt ein Verstoß gegen die Lizenzbedingungen der Remotedesktopdienste vor.

Um die Einhaltung der Lizenzbedingungen der Remotedesktopdienste gewährleisten, verfolge die Anzahl von RDS-CALs pro Benutzer nach, die in deiner Organisation verwendet werden. Stelle außerdem sicher, dass auf dem Lizenzserver genügend Pro-Benutzer-CALs für all deine Benutzer installiert sind.

Du kannst den Remotedesktoplizenzierungs-Manager verwenden, um die RDS-CALs pro Benutzer nachzuverfolgen und Berichte dazu zu generieren.

## <a name="note-about-cal-versions"></a>Hinweis zu CAL-Versionen

Die von Benutzern oder Geräten verwendete CAL muss der Windows Server-Version entsprechen, mit der der Benutzer oder das Gerät eine Verbindung herstellt. Du kannst keine älteren CALs für den Zugriff auf neuere Windows Server-Versionen verwenden, aber du kannst mit neueren CALs auf ältere Versionen von Windows Server zugreifen.

Die folgende Tabelle zeigt die CALs, die auf RD-Sitzungshosts und RD-Virtualisierungshosts kompatibel sind.

|                  |CAL für 2008 R2 und früher|CAL für 2012|CAL für 2016|CAL für 2019|
|---------------------------------|--------|--------|--------|--------|
| **Lizenzserver: 2008, 2008 R2**| Ja    | Nein     | Nein     | Nein     |
| **Lizenzserver: 2012**         | Ja    | Ja    | Nein     | Nein     |
| **Lizenzserver: 2012 R2**      | Ja    | Ja    | Nein     | Nein     |
| **Lizenzserver: 2016**         | Ja    | Ja    | Ja    | Nein     |
| **Lizenzserver: 2019**         | Ja    | Ja    | Ja    | Ja    |

Jeder RDS-Lizenzserver kann Lizenzen der aktuellen und aller früheren Versionen der Remotedesktopdienste hosten. Ein Windows Server 2016-RDS-Lizenzserver kann beispielsweise Lizenzen aller früheren Versionen von RDS hosten, ein Windows Server 2012 R2-RDS-Lizenzserver nur Lizenzen für Versionen bis zu Windows Server 2012 R2.
