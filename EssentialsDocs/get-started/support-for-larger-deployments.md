---
title: Unterstützung für größere Bereitstellungen
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a99698519524c3b5050dc534d61921560522528c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433869"
---
# <a name="support-for-larger-deployments"></a>Unterstützung für größere Bereitstellungen

>Gilt für: Windows Server 2016 Essentials

> [!IMPORTANT]  
> In diesem Thema beschriebenen Features können nur unter Windows Server 2016, mit die Essentials Experience-Rolle aktiviert und nicht mit der Windows Server 2016 Essentials-SKU.


Windows Server Essentials unterstützt nun die größere Bereitstellungen mit:

- mehrere Domänen
- mehrere Domänencontroller
- Möglichkeit zum Angeben eines designierten Domänencontrollers
- Support für bis zu 500 Benutzer und 500 Geräte

## <a name="support-for-multiple-domains"></a>Unterstützung mehrerer Domänen

Windows Server 2012 R2 Essentials unterstützt nur eine Domäne pro Server, der erforderlich ist, und der Essentials-Server muss der Stamm der Gesamtstruktur sein. Während einer Domäne und Gesamtstruktur nach wie vor erforderlich sind, kann nun die Windows Server 2016 Essentials Experience-Rolle auf Windows Server 2016 Standard oder Datacenter Unterstützung für mehrere Domänen bereitgestellt werden.

## <a name="support-for-multiple-domain-controllers"></a>Unterstützung für mehrere Domänencontroller

 Windows Server Essentials 2012 R2 blockiert alle Dienste, die Azure Active Directory, z. B. Office 365 nutzen, in denen mehr als einen Domänencontroller bereitgestellt wird. Der Grund ist, dass die Konto- und kennwortsynchronisierung zwischen dem lokalen Domänencontroller und Azure Active Directory, Anmeldeinformationen mit Kennwörtern führen kann, die nicht mehr synchron sind. Diese Einschränkung wurde in Windows Server 2016 Essentials entfernt.

## <a name="ability-to-specify-a-designated-domain-controller"></a>Möglichkeit zum Angeben eines designierten Domänencontrollers

Jetzt können Sie einen designierten Domänencontroller die wird Abrufzeiten für Objekte der Active Directory-Domäne zu verbessern sowie Synchronisierung von kontoänderung in andere Domänencontroller in der Domäne zu koordinieren.

Standard festgelegten Domänencontroller wird derselbe Server sein, der die Windows Server Essentials Experience-Serverrolle ausgeführt wird. Wenn dieser Server auf einem Mitgliedsserver, d. h., es ist dabei nicht um einen Domänencontroller, und klicken Sie dann die Standardeinstellung designierten Domänencontroller automatisch ermittelt werden wird, basieren auf Tests in ist der Domänencontroller in der Domäne hat, auf den Server mit die niedrigste Netzwerklatenz die Windows Server-Umgebung-Server-Rolle. Sollten Sie manuell ändern, welcher Server auf dem designierten Domänencontroller ist, Sie können dazu **Einstellungen** in die **Windows Server Essentials-Dashboard** wie unten dargestellt.

![Dieser Screenshot zeigt die Einstellungen steuern das Bereich in den Vordergrund und dem Windows Server Essentials-Dashboard im Hintergrund. Derzeit ist die Domänencontroller festgelegt-Seite der Systemsteuerung Einstellungen ausgewählt.](media/larger-deployments-1.PNG)

## <a name="support-for-500-users-and-500-devices"></a>Unterstützung von 500 Benutzern und 500 Geräte
-------------------------------------

Die maximale Anzahl von unterstützten Benutzer und Geräte in Windows Server 2012 R2 Essentials ist 25 und 50. Mit der Einführung der Windows Server Essentials Experience-Serverrolle diesen Grenzwert zu 100 Benutzern und 200 Geräten erhöht wurde.

Windows Server 2016 Essentials unterstützt 500 Benutzer "und" 500 Geräte. Dadurch kann ein Update für das anbieterframework und Objektliste steuert, damit sie zwischenspeichern und umfangreiche Listen der Benutzer und Gerät Objekt schnell zu rendern. Darüber hinaus wurde eine Funktion zum Suchen und Filtern hinzugefügt, um dem Benutzer oder Gerät gewünschte (siehe Abbildung 5-2) werden möglicherweise schnell zu finden. Finden Sie Such- und Filterparameter Funktionen in der **Windows Server Essentials-Dashboard**, **Remote Web Access**, und die Windows und Windows Phone Store **My Server** Anwendungen.

![Dieser Screenshot zeigt die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards zum Suchen nach der Zeichenfolge "d5c." Die Ergebnisse dieser Suche enthalten zwei Dateien und Ordner und zwei Benutzer.](media/larger-deployments-2.PNG)

Dieser Screenshot zeigt die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards für die Zeichenfolge "d5c" suchen. Die Ergebnisse dieser Suche enthalten zwei Dateien und Ordner und zwei Benutzer.

> [!NOTE]  
> Das unterstützte Limit von Benutzern und Geräten für Windows Server Essentials-Server-Rolle, das unterstützte Limit für den Client sichern bleibt unverändert 75 gesteigert.

<a name="see-also"></a>Siehe auch
--------
[Erste Schritte in Windows Server Essentials](get-started.md)