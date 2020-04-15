---
title: Beim Herstellen der Verbindung erhält der Benutzer die Meldung „Der Remotedesktopdienst ist aktuell ausgelastet“
description: Problembehandlung des Fehlers „Der Remotedesktopdienst ist aktuell ausgelastet“, wenn Benutzer eine Remotedesktopverbindung starten.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: c345833ee63a1286a5615998649e8aa9d25896a6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857163"
---
# <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>Beim Herstellen der Verbindung erhält der Benutzer die Meldung „Der Remotedesktopdienst ist aktuell ausgelastet“

Um eine passende Reaktion auf dieses Problem zu ermitteln, beachten Sie Folgendes:

- Hört der Remotedesktopdienst auf, zu reagieren (beispielsweise scheint der Remotedesktopclient beim Begrüßungsbildschirm zu „hängen“)?  
   - Wenn der Dienst nicht mehr reagiert, sehen Sie beim [RDSH-Server-Arbeitsspeicherproblem](#rdsh-server-memory-issue) nach.
   - Wenn der Client normal mit dem Dienst zu interagieren scheint, fahren Sie mit dem nächsten Schritt fort.
- Wenn mindestens ein Benutzer seine Remotedesktopsitzungen trennt, kann er sie wieder herstellen?  
   - Wenn der Dienst Verbindungen auch weiterhin ablehnt, ganz gleich, wie viele Benutzer ihre Sitzungen trennen, lesen Sie [RD-Listener-Problem](#rd-listener-issue).
   - Wenn der Dienst beginnt, Verbindungen anzunehmen, nachdem eine Reihe von Benutzern ihre Sitzungen getrennt haben, [überprüfen Sie die Richtlinie für den Verbindungsgrenzwert](#check-the-connection-limit-policy).

## <a name="rdsh-server-memory-issue"></a>RDSH-Server-Arbeitsspeicherproblem

Auf einigen Windows Server 2012 R2-RDSH-Servern wurde Arbeitsspeicherverlust festgestellt. Im Lauf der Zeit beginnen diese Server, sowohl Remotedesktopverbindungen als auch lokale Konsolenanmeldungen mit Meldungen wie der folgenden abzulehnen:

> Die Aufgabe, die Sie erledigen möchten, kann nicht ausgeführt werden, da der Remotedesktopdienst zurzeit ausgelastet ist. Wiederholen Sie den Vorgang in einigen Minuten. Andere Benutzer sollten immer noch in der Lage sein, sich anzumelden.

Remotedesktopclients, die versuchen, eine Verbindung herzustellen, reagieren nicht mehr.

Um dieses Problem zu umgehen, führen Sie einen Neustart des RDSH-Servers durch.

Um dieses Problem zu beheben, wenden Sie KB 4093114, [10. April 2018 – KB4093114 (monatliches Rollup)](https://support.microsoft.com/help/4093114/) auf die RDSH-Server an.

## <a name="rd-listener-issue"></a>RD-Listener-Problem

Auf einigen RDSH-Servern, für die ein direktes Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wurde, wurde ein Problem festgestellt. Wenn ein Remotedesktopclient eine Verbindung mit dem RDSH-Server herstellt, erstellt der RDSH-Server einen RD-Listener für die Benutzersitzung. Die betroffenen Server unterhalten einen Zähler für die RD-Listener, der heraufgesetzt wird, wenn Benutzer Verbindungen herstellen, aber nicht wieder heruntergesetzt.

Sie können dieses Problem umgehen, indem Sie die folgenden Methoden verwenden:

  - Führen Sie einen Neustart des RDSH-Servers durch, um den Zähler der RD-Listener zurückzusetzen
  - Ändern Sie den Grenzwert der Verbindungsrichtlinie, und legen Sie sie auf einen sehr hohen Wert fest. Weitere Informationen zum Verwalten der Richtlinie für den Verbindungsgrenzwert finden Sie unter [Überprüfen der Richtlinie für den Verbindungsgrenzwert](#check-the-connection-limit-policy).

Um dieses Problem zu beheben, wenden Sie die folgenden Updates auf die RDSH-Server an:

  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)

## <a name="check-the-connection-limit-policy"></a>Überprüfen der Verbindungsgrenzwert-Richtlinie

Sie können die Anzahl der gleichzeitigen Remotedesktopverbindungen auf der Ebene der einzelnen Computer oder durch Konfiguration eines Gruppenrichtlinienobjekts (GPO) einschränken. Standardmäßig ist der Grenzwert nicht festgelegt.

Um die aktuellen Einstellungen zu überprüfen und die für die RDSH-Server vorhandenen Gruppenrichtlinienobjekte zu bestimmen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl ein:
  
```cmd
gpresult /H c:\gpresult.html
```
   
Öffnen Sie nach dem Abschluss dieses Befehls **gpresult.html**. Suchen Sie in **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** die Richtlinie **Anzahl der Verbindungen einschränken**.

  - Wenn die Einstellung für diese Richtlinie **Deaktiviert** ist, wird die Anzahl der RDP-Verbindungen nicht durch eine Gruppenrichtlinie eingeschränkt.
  - Wenn die Einstellung für diese Richtlinie **Aktiviert** ist, überprüfen Sie **Ausschlaggebendes Gruppenrichtlinienobjekt**. Wenn Sie den Grenzwert für Verbindungen entfernen oder ändern müssen, bearbeiten Sie dieses GPO.

Um die Änderung der Richtlinie zu erzwingen, öffnen Sie auf dem betroffenen Computer ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl ein:
  
```cmd
gpupdate /force
```
  
