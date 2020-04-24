---
title: Verwaltung
description: Erfahren Sie mehr über Tools, Empfehlungen und Anleitungen zum Verwalten von Windows Server.
ms.prod: windows-server
layout: LandingPage
ms.technology: manage
ms.topic: landing-page
author: lizap
ms.author: elizapo
ms.localizationpriority: high
ms.openlocfilehash: 4166d4e8d2819946cdc859ef643cf53315e7290a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "71370420"
---
# <a name="management"></a>Verwaltung


>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows Server? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />

Nachdem Sie Windows Server in Ihrer Umgebung bereitgestellt haben, einschließlich der spezifischen Rollen für die benötigten Features und Funktionen, besteht der nächste Schritt darin, diese Server zu verwalten. Windows Server enthält eine Reihe von Tools, mit denen Sie Ihre Windows Server-Umgebung besser verstehen, bestimmte Server verwalten, die Leistung optimieren und viele Verwaltungsaufgaben automatisieren können. 

Die Tools, die Sie zum Verwalten von Windows Server-Instanzen verwenden, hängen in hohem Maße von den bereitgestellten Systemtypen (Windows Server mit Desktopdarstellung oder Server Core), physischen und virtuellen Computern sowie dem Standort der Server ab. Verwenden Sie die folgenden Informationen, um grundlegende Verwaltungsaufgaben unter Windows Server auszuführen.

Verwenden Sie die folgende Tabelle, um ermitteln, welche Tools wann zu verwenden sind.

| Ich bin   | Installieren und Ausführen von Windows Admin Center | Server Manager unter Windows Server ausführen | Server Manager in RSAT unter Windows 10 ausführen |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Benutzer an einem Windows 10-PC | X  |                                      | X                                        |
| Benutzer an einem Windows Server-System, das mit der Desktopdarstellung arbeitet | X | X | X |
| Benutzer an einem Windows Server-System, das mit Server Core arbeitet |X (unter Windows 10 installieren, zum Verwalten von Server Core verwenden) | | X |
| Von meinem Windows Server-System weit entfernt |X | | X |
| Von meinem Windows Server-System, das mit der Desktopdarstellung arbeitet, weit entfernt |X | Verwendung von RDS für die Remoteverbindung mit dem Server, dann Verwendung von Server-Manager | X |

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
                    <h3>Verwalten von Windows Server-Systemen und -Umgebungen</h3>
<HR />
                        <p><h3><a href="../manage/windows-admin-center/overview.md">Verwalten von lokalen Systemen, Remotesystemen und Systemen ohne Benutzeroberfläche mit Windows Admin Center</a></h3>Eine browserbasierte Verwaltungs-App, die lokale Verwaltung von Windows-Servern ohne Abhängigkeit von Azure oder der Cloud ermöglicht. Windows Admin Center (früher „Projekt Honolulu“ genannt) ermöglicht Ihnen die vollständige Kontrolle über alle Aspekte Ihrer Serverinfrastruktur und ist besonders nützlich für die Verwaltung in privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center unter Windows 10, auf einem Gatewayserver oder direkt auf dem Windows Server-System installieren, das Sie verwalten möchten.</p>
<HR />
                        <p><h3><a href="server-manager/server-manager.md">Verwalten von lokalen Systemen mit Server-Manager</a></h3>Eine Verwaltungskonsole, die in der vollständigen Installation von Windows Server enthalten ist. (Es ist nicht verfügbar bei Installationen ohne Benutzeroberfläche – in Server Core ist Server-Manager nicht enthalten). Verwenden Sie Server-Manager zum Installieren und Entfernen von Serverrollen, Hinzufügen und Entfernen von Remoteservern, Starten und Beenden von Diensten sowie zum Anzeigen von Daten, die über Ihre Umgebung gesammelt wurden.</p>
<HR />
                        <p><h3><a href="../remote/remote-server-administration-tools.md">Verwalten von Remotesystemen und Systemen ohne Benutzeroberfläche mit Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT)</a></h3>Wenn Ihre Umgebung Installationen von Server Core oder Remoteservern (lokal oder virtuelle Computer) enthält, können Sie diese Systeme mithilfe von RSAT verwalten. RSAT enthält Server-Manager, sodass Sie alle Ihre Server damit verwalten können. Beachten Sie, dass RSAT unter Windows 10 ausgeführt wird. RSAT kann nicht unter Windows Server Core installiert werden. Server Core-Installationen können auch über die Befehlszeile verwaltet werden. Weitere Informationen finden Sie unter <a href="server-core/server-core-administer.md">Grundlegende Verwaltungsaufgaben in Server Core</a>
.<HR />
                        <p><h3><a href="windows-server-update-services/get-started/windows-server-update-services-wsus.md">Verwalten von Updates für Windows Server-Systeme</a></h3>Verwenden Sie Windows Server Update Services (WSUS) zum Verwalten und Bereitstellen von Updates für die Systeme in Ihrer Windows Server-Umgebung.</p>
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
                    <h3>Sammeln von Informationen über Ihre Umgebung</h3>
<HR />
                        <p><h3><a href="get-started-with-setup-and-boot-event-collection.md">Ereignissammlung für Setup und Start</a></h3>Mit „Ereignissammlung für Setup und Start“ können Sie einen Computer zum „Sammeln“ angeben, der eine Vielzahl von wichtigen Ereignissen erfasst, die auf anderen Computern auftreten, wenn sie starten oder den Installationsvorgang durchlaufen. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren. </p>
<HR />
                        <p><h3><a href="software-inventory-logging/get-started-with-software-inventory-logging.md">Protokollierung des Softwarebestands (Software Inventory Logging, SIL)</a></h3>Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet sie die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.</p>
<HR />
                        <p><h3><a href="user-access-logging/get-started-with-user-access-logging.md">Benutzerzugriffsprotokollierung (User Access Logging, UAL)</a></h3>Die Benutzerzugriffsprotokollierung aggregiert eindeutige Ereignisse auf Clientgeräten sowie Benutzeranforderungsereignisse, die auf einem Computer unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einer lokalen Datenbank protokolliert wurden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen. Außerdem bietet UAL auch Nicht-Microsoft-Softwareentwicklern die Möglichkeit, ihre UAL-Ereignisse für die Aggregierung zu instrumentieren. </a>
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
                        <p><h3><a href="performance-tuning/index.md">Richtlinien zur Leistungsoptimierung</a></h3>Überprüfen Sie eine Reihe von Richtlinien, mit denen Sie die Servereinstellungen in Windows Server optimieren und inkrementelle Leistungs- oder Energieeffizienzsteigerungen erzielen können – insbesondere, wenn sich die Art der Arbeitsauslastung im Laufe der Zeit nur wenig ändert.</p>
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
                        <p><h3><a href="https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-5.1">Windows PowerShell</a></h3>Windows PowerShell ist eine Befehlszeilen-Shell und -Skriptsprache, die mit der Sie Verwaltungsaufgaben schnell automatisieren können. </p>
<HR />
                        <p><h3><a href="windows-commands/windows-commands.md">Windows-Befehle</a></h3>Die Windows-Befehlszeilentools dienen zum Ausführen von Verwaltungsaufgaben in Windows. Anhand der Befehlsreferenz können Sie sich mit den Befehlszeilentools vertraut machen, mehr über die Befehlsshell erfahren und Befehlszeilenaufgaben mithilfe von Stapeldateien oder Skripting-Tools automatisieren.</p>
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
                        <p><h3><a href="..\manage\system-insights\overview.md">Systemdaten</h3></a>Systemeigene vorhersehbare Analysen analysieren lokal Windows Server-Systemdaten wie Leistungsindikatoren und ETW-Ereignisse und helfen IT-Administratoren proaktiv, problematisches Verhalten in ihren Bereitstellungen zu erkennen und zu beheben.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>