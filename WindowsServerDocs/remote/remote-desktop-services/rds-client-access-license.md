---
title: Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)
description: Hier findest du eine Übersicht über die Clientlizenzierung in den Remotedesktopdiensten.
ms.topic: article
ms.assetid: 5be6546b-df16-4475-bcba-aa75aabef3e3
author: lizap
ms.author: elizapo
ms.date: 02/12/2020
manager: dongill
ms.openlocfilehash: d257893e19286ab2a4c8293a2cf2b2e6697898ce
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936989"
---
# <a name="license-your-rds-deployment-with-client-access-licenses-cals"></a>Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Jeder Benutzer und jedes Gerät, der bzw. das eine Verbindung mit einem Remotedesktop-Sitzungshost herstellt, benötigt eine Clientzugriffslizenz (Client Access License, CAL). Zum Installieren, Ausstellen und Nachverfolgen der RDS-CALs verwendest du die RD-Lizenzierung.

Wenn ein Benutzer oder ein Gerät eine Verbindung mit einem RD-Sitzungshostserver herstellt, bestimmt der RD-Sitzungshostserver, ob eine RDS-CAL benötigt wird. Der RD-Sitzungshostserver fordert dann eine RDS-CAL vom Remotedesktop-Lizenzserver an. Wenn eine geeignete RDS-CAL auf einem Lizenzserver verfügbar ist, wird die RDS-CAL für den Client ausgestellt, und der Client kann eine Verbindung mit dem RD-Sitzungshostserver und von dort aus mit den Desktops oder Apps herstellen, die verwendet werden sollen.

Es gibt eine Lizenzierungskarenzzeit von 180 Tagen, in der kein Lizenzserver erforderlich ist. Nach Ablauf dieses Zeitraums müssen die Clients eine gültige RDS-CAL von einem Lizenzserver erhalten, bevor sie sich bei einem RD-Sitzungshostserver anmelden können.

Verwende die folgenden Informationen, um zu erfahren, wie die Clientzugriffslizenzierung in den Remotedesktopdiensten funktioniert, und um deine Lizenzen bereitzustellen und zu verwalten:

- [Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)](#license-your-rds-deployment-with-client-access-licenses-cals)
  - [Grundlegendes zum RDS-CAL-Modell](#understanding-the-rds-cal-model)
  - [RDS-CAL-Versionskompatibilität](#rds-cal-version-compatibility)

## <a name="understanding-the-rds-cal-model"></a>Grundlegendes zum RDS-CAL-Modell

Es gibt zwei Typen von RDS-CALs:

- RDS-CALs pro Gerät
- RDS-CALs pro Benutzer

Die folgende Tabelle zeigt die Unterschiede zwischen den beiden CAL-Typen:

| Pro Gerät                                                     | Pro Benutzer                                                                         |
|----------------------------------------------------------------|----------------------------------------------------------------------------------|
| RDS-CALs werden jedem Gerät physisch zugewiesen.                   | RDS-CALs werden einem Benutzer in Active Directory zugewiesen.                                 |
| RDS-CALs werden vom Lizenzserver nachverfolgt.                        | RDS-CALs werden vom Lizenzserver nachverfolgt.                                          |
| RDS-CALs können unabhängig von der Mitgliedschaft in Active Directory nachverfolgt werden. | RDS-CALs können innerhalb einer Arbeitsgruppe nicht nachverfolgt werden.                                       |
| Du kannst bis zu 20 % der RDS-CALs widerrufen.                              | Du kannst keine RDS-CALs widerrufen.                                                      |
| Temporäre RDS-CALs sind 52–89 Tage lang gültig.                       | Es sind keine temporären RDS-CALs verfügbar.                                                |
| RDS-CALs können nicht überlastet werden.                                  | RDS-CALs können überlastet werden (entgegen der Remotedesktop-Lizenzvereinbarung). |

Bei Verwendung des Pro-Gerät-Modells wird eine temporäre Lizenz ausgestellt, wenn ein Gerät zum ersten Mal eine Verbindung mit dem Remotedesktop-Sitzungshost herstellt. Bei der zweiten Verbindungsherstellung stellt der Lizenzserver eine permanente RDS-CAL pro Gerät aus, sofern der Server aktiviert ist und RDS-CALs verfügbar sind.

Wenn du das Pro-Benutzer-Modell verwendest, wird die Lizenzierung nicht erzwungen, und jedem Benutzer wird eine Lizenz erteilt, mit der er von einer beliebigen Anzahl von Geräten aus eine Verbindung mit einem Remotedesktop-Sitzungshost herstellen kann. Der Lizenzserver stellt Lizenzen aus dem verfügbaren RDS-CAL-Pool oder dem RDS-CAL-Pool „Überbeansprucht“ aus. Du musst sicherstellen, dass all deine Benutzer eine gültige Lizenz und keine CALs aus dem Pool „Überbeansprucht“ besitzen– andernfalls liegt ein Verstoß gegen die Lizenzbedingungen der Remotedesktopdienste vor.

Ein Beispiel für die Verwendung des „Pro Gerät“-Modells wäre eine Umgebung, in der zwei oder mehr Schichten die gleichen Computer für den Zugriff auf die RD-Sitzungshosts verwenden. Das „Pro Benutzer“-Modell eignet sich am besten für Umgebungen, in denen Benutzer über ein eigenes dediziertes Windows-Gerät für den Zugriff auf die RD-Sitzungshosts verfügen.

Um die Einhaltung der Lizenzbedingungen der Remotedesktopdienste gewährleisten, verfolge die Anzahl von RDS-CALs pro Benutzer nach, die in deiner Organisation verwendet werden. Stelle außerdem sicher, dass auf dem Lizenzserver genügend Pro-Benutzer-RDS-CALs für all deine Benutzer installiert sind.

Du kannst den Remotedesktoplizenzierungs-Manager verwenden, um die RDS-CALs pro Benutzer nachzuverfolgen und Berichte dazu zu generieren.

## <a name="rds-cal-version-compatibility"></a>RDS-CAL-Versionskompatibilität

Die RDS-CAL für deine Benutzer oder Geräte muss mit der Windows Server-Version kompatibel sein, mit der der Benutzer oder das Gerät eine Verbindung herstellt. Du kannst keine RDS-CALs für ältere Versionen für den Zugriff auf neuere Windows Server-Versionen verwenden, aber du kannst mit neueren Versionen von RDS-CALs auf ältere Versionen von Windows Server zugreifen. Beispielsweise ist eine RDS 2016 CAL oder höher erforderlich, um eine Verbindung mit einem Windows Server 2016-RD-Sitzungshost herzustellen, während eine RDS 2012 CAL oder höher erforderlich ist, um eine Verbindung mit einem Windows Server 2012 R2-RD-Sitzungshost herzustellen.

In der folgenden Tabelle wird gezeigt, welche RDS-CAL- und RD-Sitzungshostversionen miteinander kompatibel sind.

|                  | RDS 2008 R2 CAL und niedriger | RDS 2012 CAL | RDS 2016CAL | RDS 2019CAL |
|---------------------------------|--------|--------|--------|--------|
| **2008-, 2008 R2-Sitzungshost** | Ja    | Ja    | Ja    | Ja     |
| **2012-Sitzungshost**         | Nein     | Ja    | Ja    | Ja    |
| **2012 R2-Sitzungshost**      | Nein     | Ja    | Ja    | Ja    |
| **2016-Sitzungshost**         | Nein     | Nein     | Ja    | Ja    |
| **2019-Sitzungshost**         | Nein     | Nein     | Nein     | Ja    |

Sie müssen Ihre RDS-CAL auf einem kompatiblen RD-Lizenzserver installieren. Jeder RDS-Lizenzserver kann Lizenzen der aktuellen und aller früheren Versionen der Remotedesktopdienste hosten. Ein Windows Server 2016-RDS-Lizenzserver kann beispielsweise Lizenzen aller früheren Versionen von RDS hosten, ein Windows Server 2012 R2-RDS-Lizenzserver nur Lizenzen für Versionen bis zu Windows Server 2012 R2.

In der folgenden Tabelle wird gezeigt, welche RDS-CAL- und Lizenzserverversionen miteinander kompatibel sind.

|                  | RDS 2008 R2 CAL und niedriger | RDS 2012 CAL | RDS 2016CAL | RDS 2019CAL |
|---------------------------------|--------|--------|--------|--------|
| **Lizenzserver: 2008, 2008 R2** | Ja    | Nein   | Nein   | Nein    |
| **Lizenzserver: 2012**         | Ja     | Ja    | Nein   | Nein    |
| **Lizenzserver: 2012 R2**      | Ja     | Ja    | Nein   | Nein    |
| **Lizenzserver: 2016**         | Ja     | Ja    | Ja   | Nein    |
| **Lizenzserver: 2019**         | Ja     | Ja    | Ja  | Ja   |
