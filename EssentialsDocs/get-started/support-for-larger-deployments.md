---
title: "Unterstützung für größere Bereitstellungen"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: c60e5f73c88a225fbd1067992894f9d20da745ad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
#<a name="support-for-larger-deployments"></a>Unterstützung für größere Bereitstellungen

>Gilt für: Windows Server2016 Essentials

> [!IMPORTANT]  
> In diesem Thema beschriebenen Features funktionieren nur auf Windows Server2016 mit aktivierter Essentials Experience-Rolle und nicht mit dem Windows Server2016 Essentials-SKU.


Windows Server Essentials unterstützt jetzt größere Bereitstellungen mit:

- Mehrere Domänen
- Mehrere Domänencontroller
- Möglichkeit, einen bestimmten Domänencontroller angeben
- Unterstützung für bis zu 500 Benutzern und 500 Geräte

##<a name="support-for-multiple-domains"></a>Unterstützung mehrerer Domänen

Windows Server 2012 R2 Essentials unterstützt nur eine Domäne pro Server, der erforderlich ist, und der Essentials-Server muss den Stamm der Gesamtstruktur sein. Während einer Domäne und Gesamtstruktur noch erforderlich sind, kann jetzt Windows Server2016 Essentials Experience-Rolle auf Windows Server2016 Standard oder Datacenter, Unterstützung für mehrere Domänen bereitgestellt werden.

## <a name="support-for-multiple-domain-controllers"></a>Unterstützung für mehrere Domänencontroller

 Windows Server Essentials 2012 R2 blockiert alle Dienste, die Azure Active Directory, z.B. Office365, nutzen, in denen mehrere Domänencontroller bereitgestellt wird. Der Grund ist das Konto und Kennwort-Synchronisierung zwischen dem lokalen Domänencontroller und Azure Active Directory Kontoanmeldeinformationen mit Kennwörtern dazu führen, dass kann, die nicht mehr synchron sind. Diese Einschränkung wurde in Windows Server2016 Essentials entfernt.

##<a name="ability-to-specify-a-designated-domain-controller"></a>Möglichkeit, einen bestimmten Domänencontroller angeben

Sie können jetzt wird verbessert abrufen, wie oft für Objekte der Active Directory-Domäne sowie Synchronisierung von Änderung alle anderen Domänencontroller in der Domäne zu koordinieren designierten Domänencontroller auswählen.

Standard-Domänencontroller benannt werden dem gleichen Server, auf der die Windows Server Essentials Experience-Serverrolle ausgeführt wird. Wenn dieser Server ein Mitgliedsserver ist, hat was bedeutet, dass es sich nicht um einen Domänencontroller, ist die Standardeinstellung, die dafür vorgesehenen Domänencontroller automatisch basierend bestimmt wird auf Tests, welcher Domänencontroller in der Domäne die niedrigste Netzwerklatenz auf den Server mit der Windows Server Experience-Serverrolle. Wenn Sie möchten manuell ändern, welcher Server dem designierten Domänencontroller ist, Sie können die notwendigen Schritteim **Einstellungen** in der **Windows Server Essentials-Dashboard** wie unten dargestellt.

![Ein Bildschirmfoto, mit der Systemsteuerung im Vordergrund und im Windows Server Essentials-Dashboard im Hintergrund. Zurzeit ist die Domänencontroller festgelegt Seite die Einstellungen der Systemsteuerung ausgewählt.](media/larger-deployments-1.PNG)

##<a name="support-for-500-users-and-500-devices"></a>Unterstützung für 500 Benutzer und 500 Geräte
-------------------------------------

Die maximale Anzahl von unterstützten Benutzern und Geräten in Windows Server2012 R2 Essentials ist 25 und 50. Mit der Einführung der Windows Server Essentials Experience-Serverrolle wurde diese Beschränkung zu 100 Benutzern und 200 Geräten erhöht.

Windows Server2016 Essentials unterstützt 500 Benutzer und 500 Geräte. Dies möglich ist ein Update für die anbieterframework und Objekt Listensteuerelemente Zwischenspeichern und große Objektlisten für Benutzer und Gerät schnell zu rendern. Darüber hinaus wurde ein Feature zum Suchen und Filtern hinzugefügt, um den Benutzer oder Gerät, das Sie (siehe Abbildung5-2 Suchen) schnell zu finden. Erfahren Sie, suchen und Filtern von Funktionen in der **Windows Server Essentials-Dashboard**, **Remote Web Access**, und den Windows und Windows Phone Store **My Server** Anwendungen.

![Ein Bildschirmfoto zeigt die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards zum Suchen nach der Zeichenfolge "d5c." Die Ergebnisse der Suche enthalten zwei Dateien und Ordner und zwei Benutzer.](media/larger-deployments-2.PNG)

Ein Bildschirmfoto zeigt die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards zum Suchen nach der Zeichenfolge "d5c". Die Ergebnisse der Suche enthalten zwei Dateien und Ordner und zwei Benutzer.

> [!NOTE]  
> Während das unterstützte Limit für Benutzer und Gerät für Windows Server Essentials-Server-Rolle, das unterstützte Limit für den Client sichern bleibt bei 75 gestiegen ist.

<a name="see-also"></a>Siehe auch
--------
[Erste Schrittemit Windows Server Essentials](get-started.md)