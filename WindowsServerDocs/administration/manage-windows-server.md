---
title: Verwaltung
description: Erfahren Sie mehr über Tools, Empfehlungen und Anleitungen zum Verwalten von Windows Server
ms.prod: windows-server-threshold
layout: LandingPage
ms.technology: manage
ms.topic: landing-page
author: lizap
ms.author: elizapo
ms.localizationpriority: high
ms.openlocfilehash: e6a5357e3e33b3d3318a3e281bbb5c80be842155
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339278"
---
# Verwaltung


>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere anderen [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen auf [dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) .

<hr />

Nachdem Sie Windows Server in Ihrer Umgebung bereitgestellt haben, einschließlich der spezifischen Rollen für die Features und Funktionen, die Sie benötigen, besteht der nächste Schritt darin, diese Server zu verwalten. Windows Server enthält eine Reihe von Tools, mit denen Sie Ihre Windows Server-Umgebung besser verstehen, bestimmte Server verwalten, die Leistung optimieren und viele Verwaltungsaufgaben automatisieren können. 

Die Tools, die Sie zum Verwalten von Windows Server-Instanzen verwenden, hängen in hohem Maße von den bereitgestellten Systemtypen (Windows Server mit Desktop Experience oder Server Core), physischen und virtuellen Computern sowie dem Standort der Server ab. Verwenden Sie die folgenden Informationen, um grundlegende Verwaltungsaufgaben unter Windows Server durchzuführen.

Verwenden Sie die folgende Tabelle, um ermitteln, welche Tools wann zu verwenden sind.

| Ich bin   | Installieren und Ausführen von Windows Admin Center | Ausführen des Server-Managers unter Windows Server | Ausführen des Server-Managers in RSAT unter Windows 10 |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Benutzer an einem Windows10-PC | X  |                                      | X                                        |
| Benutzer an einem Windows Server-System, das mit der Desktopoberfläche arbeitet | X | X | X |
| Benutzer an einem Windows Server-System, das mit Server Core arbeitet |X (unter Windows10 installieren, verwenden zum Verwalten von Server Core) | | X |
| weit von meinem Windows Server-System entfernt |X | | X |
| weit von meinem Windows Server-System entfernt, das mit der Desktopoberfläche arbeitet |X | Verwendung von RDS für die Remoteverbindung mit dem Server, dann Verwendung von Server-Manager | X |

Zusätzlich zu den unten aufgeführten Tools können Sie auch [Remotedesktopdienste](../remote/remote-desktop-services/welcome-to-rds.md) für den Zugriff auf lokale, remote und virtuelle Server verwenden. Dann können Sie mit Server-Manager Verwaltungsaufgaben ausführen.

<HR />

<ul class="cardsI panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Verwalten von Windows Server-Systemen und Umgebungen</h3>
<HR />
                        <p><h3><a href="../manage/windows-admin-center/overview.md">Verwalten von lokalen Systemen, remote-Systemen und Systemen ohne Benutzeroberfläche mit Windows Admin Center</a></h3>Eine browserbasierte Verwaltungs-app, die lokale Verwaltung von Windows-Servern ohne Abhängigkeit von Azure oder der Cloud ermöglicht. Windows Admin Center (früher "Projekt Honolulu" genannt) ermöglicht die vollständige Kontrolle über alle Aspekte Ihrer Serverinfrastruktur und ist besonders nützlich für die Verwaltung in privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center auf Windows 10, auf einem Gatewayserver oder direkt auf dem Windows Server System installieren, das Sie verwalten möchten.</p>
<HR />
                        <p><h3><a href="server-manager/server-manager.md">Verwalten von lokalen Systemen mit Server-Manager</a></h3>Eine Verwaltungskonsole, die in der vollständigen Installation von Windows Server enthalten. (Sie ist nicht für Installationen verfügbar, die keine Benutzeroberfläche haben – Server Core enthält Server-Manager nicht.) Verwenden Sie Server-Manager zum Installieren und Entfernen von Serverrollen, Hinzufügen und Entfernen von Remoteservern, Starten und Stoppen von Diensten und zum Anzeigen von Daten über die Umgebung.</p>
<HR />
                        <p><h3><a href="../remote/remote-server-administration-tools.md">Verwalten von Remotesystemen und Systemen ohne Benutzeroberfläche mit Remote Server Administration Tools (RSAT)</a></h3>Wenn Ihre Umgebung Installationen von Server Core oder Remoteservern (lokal oder virtuelle Computer) enthält, können Sie RSAT (Remoteserver-Verwaltungstools) verwenden, um diese Systeme zu verwalten. RSAT enthält Server-Manager, sodass Sie alle Ihre Server verwalten können. Beachten Sie, dass RSAT unter Windows 10 ausgeführt wird. RSAT kann nicht unter Windows Server Core installiert werden. Server Core-Installationen können über die Befehlszeile verwaltet werden. Finden Sie unter <a href="server-core/server-core-administer.md">grundlegende Verwaltungsaufgaben in Server Core</a>
<HR />
                        <p><h3><a href="windows-server-update-services/get-started/windows-server-update-services-wsus.md">Verwalten von Updates für Windows Server-Systeme</a></h3>Verwenden Sie Windows Server Update Services (WSUS) zum Verwalten und Bereitstellen von Updates für die Systeme in Ihrer Umgebung Windows Server.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Sammeln von Informationen über die Umgebung</h3>
<HR />
                        <p><h3><a href="get-started-with-setup-and-boot-event-collection.md">Ereignissammlung für Setup und Start</a></h3>Das Feature „Setup and Boot Event Collection”ermöglicht die Festlegung eines Sammelcomputers, der eine Reihe von wichtigen Ereignissen erfasst, die auf anderen Computern auftreten, während diese Computer gestartet werden oder den Setupvorgang durchlaufen. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren. </p>
<HR />
                        <p><h3><a href="software-inventory-logging/get-started-with-software-inventory-logging.md">Protokollierung des Softwarebestands (Software Inventory Logging, SIL)</a></h3>Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet das Feature die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.</p>
<HR />
                        <p><h3><a href="user-access-logging/get-started-with-user-access-logging.md">Benutzerzugriffsprotokollierung (User Access Logging, UAL)</a></h3>Die Benutzerzugriffsprotokollierung aggregiert eindeutige Ereignisse auf Clientgeräten sowie Benutzeranforderungsereignisse, die auf einem Computer unter Windows Server2016, Windows Server2012 R2 oder Windows Server2012 in einer lokalen Datenbank protokolliert wurden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen. Zudem bietet UAL auch Nicht-Microsoft-Softwareentwicklern die Möglichkeit, ihre UAL-Ereignisse zu instrumentieren und zu aggregieren. </a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Leistungsoptimierung für die Windows Server-Umgebung</h3>
<HR />
                        <p><h3><a href="performance-tuning/index.md">Richtlinien zur Leistungsoptimierung</a></h3>Überprüfen Sie eine Reihe von Richtlinien, mit denen Sie die Servereinstellungen in Windows Server optimieren und inkrementelle Leistungs- oder Energieeffizienzsteigerungen erzielen können, insbesondere wenn sich die Art der Auslastung im Laufe der Zeit nur wenig ändert.</p>
<HR />
                        <p><h3><a href="server-performance-advisor/microsoft-server-performance-advisor.md">Microsoft Server Performance Advisor</a></h3>Mit Microsoft Server Performance Advisor (SPA) können Sie Messdaten sammeln, um Leistungsprobleme auf Windows-Servern unauffällig zu diagnostizieren, ohne Softwareagenten hinzuzufügen oder Produktionsserver neu zu konfigurieren. SPA generiert umfassende Berichte und historische Diagramme mit Empfehlungen.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Automatisieren der Windows Server-Verwaltung</h3>
<HR />
                        <p><h3><a href="https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-5.1">Windows PowerShell</a></h3>Windows PowerShell ist eine Befehlszeilen-Shell und Skriptsprache, die mit der Sie Verwaltungsaufgaben schnell automatisieren können. </p>
<HR />
                        <p><h3><a href="windows-commands/windows-commands.md">Windows-Befehle</a></h3>Die Windows-Befehlszeilentools dienen zum Durchführen von Verwaltungsaufgaben in Windows. Mit der Befehlsreferenz können Sie sich mit den Befehlszeilentools vertraut machen, mehr über die Befehlsshell erfahren und Befehlszeilenaufgaben mithilfe von Stapeldateien oder Skripting-Tools automatisieren.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Automatisieren der Windows Server-Verwaltung</h3>
<HR />
                        <p><h3><a href="..\manage\system-insights\overview.md">Systemeinblicke</h3></a>Systemeigene vorhersehbare Analytics lokal vorhersehbare Windows Server Systemdaten, wie z. B. Leistungsindikatoren und ETW-Ereignisse, und helfen IT-Administratoren proaktiv erkennen und beheben Sie problematische Verhalten in Bereitstellungen.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>