---
title: Lizenzieren Sie Ihre RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)
description: Übersicht über die Lizenzierung in Remote Desktop Services Client.
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
ms.openlocfilehash: 6648a52bb4d09725935a2197d6ce6fa6d8cc74a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853441"
---
# <a name="license-your-rds-deployment-with-client-access-licenses-cals"></a>Lizenzieren Sie Ihre RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Jeden Benutzer und Gerät für die Verbindung mit einem Remote Desktop Session Host benötigt eine Client-Clientzugriffslizenzen (CAL). Sie verwenden RD-Lizenzierung zum Installieren, ausstellen und Nachverfolgen von RDS-CALs.  

Wenn ein Benutzer oder ein Gerät mit einem RD Session Host-Server verbunden ist, bestimmt der RD-Sitzungshost-Server bei Bedarf eine RDS-CAL ist. Der Remotedesktop-Sitzungshostserver fordert dann eine RDS-CAL aus dem Remotedesktop-Lizenzserver. Wenn eine entsprechende RDS-CAL von einem Lizenzserver verfügbar ist, die RDS-CAL für den Client ausgestellt wird, und der Client ist eine Verbindung herstellen, auf dem RD-Sitzungshost-Server und von dort auf dem Desktop oder apps, die sie verwenden möchten.

Jedoch besteht eine Kulanzfrist, in dem kein, die Lizenzserver erforderlich ist, nachdem der Toleranzperiode endet, Clients eine gültige RDS-CAL von einem Lizenzserver, bevor Sie ausgestellt haben, müssen, können sie mit einem RD Session Host-Server anmelden.

Verwenden Sie die folgende Informationen, um zu erfahren, wie die Clientzugriffslizenz in Remote Desktop Services funktioniert und zum Bereitstellen und verwalten Ihre Lizenzen:

- [Verstehen des Modells CALs](#understanding-the-cals-model)
- [Aktivieren des Lizenzservers](rds-activate-license-server.md)
- [RDS-CALs auf dem Lizenzserver installieren](rds-install-cals.md)
- [Verfolgen Sie die in Ihrer Bereitstellung verwendeten CALs](rds-track-cals.md)

## <a name="understanding-the-cals-model"></a>Grundlegendes zum Datenmodell CALs

Es gibt zwei Arten von Clientzugriffslizenzen:

- RDS pro Geräte-Clientzugriffslizenzen
- RDS pro-Benutzer-CALs

Die folgende Tabelle beschreibt die Unterschiede zwischen den zwei Arten von Clientzugriffslizenzen:

| Pro Gerät                                                     | Pro Benutzer                                                                         |
|----------------------------------------------------------------|----------------------------------------------------------------------------------|
| Clientzugriffslizenzen sind für jedes Gerät physisch zugewiesen.                   | CALs werden zu einem Benutzer in Active Directory zugewiesen.                                 |
| CALs werden von der Lizenzserver nachverfolgt.                        | CALs werden von der Lizenzserver nachverfolgt.                                          |
| Clientzugriffslizenzen, die unabhängig von Active Directory-Gruppenmitgliedschaft überwacht werden können. | Clientzugriffslizenzen können nicht in einer Arbeitsgruppe nachverfolgt werden.                                       |
| Sie können bis zu 20 % der CALs widerrufen.                              | Sie können nicht widerrufen, dass keine Clientzugriffslizenzen.                                                      |
| Temporären CALs sind 52: 89 Tagen gültig.                       | Es sind keine temporären CALs zur Verfügung.                                                |
| Clientzugriffslizenzen können nicht überlastet werden.                                  | (In einer der Remote Desktop licensing Agreement) können CALs überlastet werden. |

Wenn Sie das Modell "pro Gerät" verwenden, wird eine temporäre Lizenz erstmalig ausgegeben, die ein Gerät mit dem Remotedesktop-Sitzungshost verbindet. Beim zweiten Mal eine Verbindung herstellt, Gerät, solange der Lizenzserver aktiviert ist, und es CALs verfügbar, der Lizenzserver eine permanente Clientzugriffslizenz für RDS-pro-Gerät sind.

Wenn Sie das Modell pro Benutzer verwenden, Lizenzierung wird nicht erzwungen, und jeder Benutzer erhält eine Lizenz von einer beliebigen Anzahl von Geräten eine Verbindung mit RD-Sitzungshosts. Der Lizenzserver gibt Lizenzen aus dem verfügbaren CAL-Pool oder den Over-Used CAL-Pool. Es Ihrer Verantwortung, sicherzustellen, dass alle Benutzer eine gültige Lizenz und Over-Used CALs NULL ist, andernfalls, befinden Sie sich in der Verstoß gegen die Lizenzbedingungen für Remote Desktop Services.

Um sicherzustellen, dass Sie gemäß den Lizenzbedingungen für Remotedesktop Services, Nachverfolgen von RDS-CALs pro Benutzer in Ihrer Organisation verwendet, und achten Sie darauf, dass Sie eine ausreichende Clientzugriffslizenzen pro Benutzer auf dem Lizenzserver für alle Benutzer installiert haben.

Sie können den Remotedesktoplizenzierungs-Manager verwenden, zum Nachverfolgen und Berichte für RDS-CALs pro Benutzer.

## <a name="note-about-cal-versions"></a>Informationen zu CAL-Versionen Beachten

Die CAL von Benutzern oder Geräten verwendet muss die Version von Windows Server entsprechen, die dem Benutzer oder Gerät eine Verbindung herstellt. Können keine ältere CALs auf neuere Versionen von Windows Server, jedoch können Sie neuere CALs frühere Versionen von Windows Server zuzugreifen.

Die folgende Tabelle zeigt die CALs, die auf RD-Sitzungshosts und Remotedesktop-Virtualisierungshosts kompatibel sind.

|                  |2008 R2 und früheren CAL|2012 CAL|2016 CAL|2019 CAL|
|---------------------------------|--------|--------|--------|--------|
| **2008, 2008 R2-Lizenz-server**| Ja    | Nein     | Nein     | Nein     |
| **2012-Lizenzserver**         | Ja    | Ja    | Nein     | Nein     |
| **2012 R2-Lizenzserver**      | Ja    | Ja    | Nein     | Nein     |
| **2016-Lizenzserver**         | Ja    | Ja    | Ja    | Nein     |
| **2019-Lizenzserver**         | Ja    | Ja    | Ja    | Ja    |

Alle RDS-Server-Lizenz kann Lizenzen alle früheren Versionen von Remote Desktop Services und die aktuelle Version von Remote Desktop Services hosten. Beispielsweise kann ein Windows Server 2016-RDS-Lizenzserver Lizenzen alle früheren Versionen von RDS, hosten, während ein Windows Server 2012 R2 RDS-Lizenzservers nur Lizenzen bis zu Windows Server 2012 R2 hosten kann.
