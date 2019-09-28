---
title: Verwalten von Benutzerstationen
description: Erfahren Sie, wie Sie Benutzer Stationen in Multipoint Services verwalten.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b418578d-3a4c-49b0-90db-8389b320b2f6
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 7f46d2a68fc6247bddc1251c32ac55544b6fbf52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405066"
---
# <a name="manage-user-stations"></a>Verwalten von Benutzerstationen
Dieser Abschnitt behandelt die Verwaltung der *Stationen*, aus denen das MultiPoint Services-System besteht. Die Verwaltung eines Multipoint Services-Systems umfasst die Verwaltung der Hardware-und Softwarekomponenten von Multipoint Manager. In einem Multipoint Services-System ist ein Desktop die Software Benutzeroberfläche, die auf dem Monitor für jede Benutzer Station angezeigt wird.  
  
## <a name="station-status"></a>Stationsstatus  
Für jeden Desktop können die folgenden Statustypen auf der Registerkarte **Stationen** angezeigt werden. Der Status umfasst folgende Informationen:  
  
-   Angemeldete Benutzer  
  
-   Benutzersitzungen, die angehalten, aber auf dem Computer noch aktiv sind  
  
-   Verwendete Stationen mit Benutzern  
  
Weitere Informationen zur Anzeige des Desktopstatus finden Sie im Thema [Anzeigen des Benutzerverbindungsstatus](View-User-Connection-Status.md).  

>[!TIP] 
> Sie können jeder Station Anzeigenamen zuweisen, wodurch Sie die Stationen leichter identifizieren können. Verwenden Sie **Identify station** (Station identifizieren), um den Stationsname auf dem zugewiesenen Bildschirm anzuzeigen.
  
## <a name="different-ways-to-log-standard-users-off-of-the-multipoint-services-system"></a>Unterschiedliche Arten zum Abmelden von Standardbenutzern vom MultiPoint Services-System  
Als *Administrator* können Sie Windows jederzeit abmelden, ohne dass dies Auswirkungen auf aktive Benutzer in Ihrem MultiPoint Services-Systems hat. *Standardbenutzer* können ihre Sitzung *trennen* oder das MultiPoint Services-System ebenfalls *abmelden*. Wenn ein Benutzer seine Arbeit beendet und den Computer verlässt, sollte er seine Arbeit auf dem Computer oder einem externen Speichergerät speichern, damit er nach dem Herunterfahren des MultiPoint Services-Systems seine gespeicherte Arbeit an einem anderen Tag wieder abrufen kann.  
  
Als Administrator müssen Sie möglicherweise die *Sitzung*eines Standard Benutzers beenden, anstatt den Benutzer abzumelden. Eine Standardbenutzer Sitzung kann auf zwei Arten beendet werden:  
  
-   Beenden Sie die Sitzung, und melden Sie den Benutzer ab. Weitere Informationen zum Beenden der Sitzung eines Benutzers finden Sie im Thema [Beenden einer Benutzersitzung](End-a-User-Session.md) .  
  
-   Sperren Sie den Benutzer, um die Sitzung des Benutzers vorübergehend zu beenden, behalten Sie jedoch die aktive Sitzung im Computerspeicher des Multipoint Services-Systems bei. Der angehaltene Benutzer kann dann von derselben oder einer anderen Station aus wieder eine Verbindung mit der Sitzung herstellen und seine Arbeit fortsetzen. Weitere Informationen zum Anhalten der Sitzung eines Benutzers finden Sie im Thema anhalten [und verlassen der Benutzersitzung](Suspend-and-Leave-User-Session-Active.md) .  
  
## <a name="set-a-station-to-automatically-log-on"></a>Festlegen der automatischen Anmeldung für eine Station  
Als Administrator können Sie für eine oder mehrere Station(en) die automatische Anmeldung beim Starten des Computers festlegen, auf dem MultiPoint Services ausgeführt werden. Weitere Informationen zur automatischen Anmeldung finden Sie im Thema [Einrichten einer Station für die automatische Anmeldung](Set-up-a-Station-for-Automatic-Logon.md).  
  
## <a name="split-a-station"></a>Teilen einer Station  
Jeder Stationsmonitor mit einer Auflösung von mehr als 1024x768 kann in zwei Stationen geteilt werden. Weitere Informationen zum Teilen einer Station finden Sie im Thema [Teilen einer Benutzerstation](Split-a-User-Station.md).  
  
## <a name="see-also"></a>Siehe auch  
[Anzeigen des Benutzerverbindungsstatus](View-User-Connection-Status.md)  
[Abmelden oder Trennen von Benutzersitzungen](Log-off-or-Disconnect-User-Sessions.md)  
[Aussetzen und Benutzersitzung aktiv lassen](Suspend-and-Leave-User-Session-Active.md)  
[Einrichten einer Station für die automatische Anmeldung](Set-up-a-Station-for-Automatic-Logon.md)  
[Beenden einer Benutzersitzung](End-a-User-Session.md)  
[Teilen einer Benutzerstation](Split-a-User-Station.md)