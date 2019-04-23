---
title: Windows Server verwalten
description: Tools, Empfehlungen und Anleitungen zum Verwalten von Windows Server
ms.prod: windows-server-threshold
ms.technology: manage
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4faadb811927626c26a5b01e2ce0598d40792b68
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846761"
---
# <a name="manage-windows-server"></a>Windows Server verwalten

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

 <ul class="cardse panelContent cols cols3">
    <li>
        <a href="https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback-hub">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>Verwalten</h2>
                <p>Nachdem Sie Windows Server in Ihrer Umgebung bereitgestellt haben, einschließlich der spezifischen Rollen für die Features und Funktionen, die Sie benötigen, besteht der nächste Schritt darin, diese Server zu verwalten. Windows Server enthält eine Reihe von Tools, mit denen Sie Ihre Windows Server-Umgebung besser verstehen, bestimmte Server verwalten, die Leistung optimieren und viele Verwaltungsaufgaben automatisieren können. </p>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li> 
</ul> 

## <a name="manage-windows-server-systems-and-environments"></a>Verwalten von Windows Server-Systemen und Umgebungen
Die Tools, die Sie zum Verwalten von Windows Server-Instanzen verwenden, hängen in hohem Maße von den bereitgestellten Systemtypen (Windows Server mit Desktop Experience oder Server Core), physischen und virtuellen Computern sowie dem Standort der Server ab. Verwenden Sie die folgenden Informationen, um grundlegende Verwaltungsaufgaben unter Windows Server durchzuführen.

Verwenden Sie die folgende Tabelle, um ermitteln, welche Tools wann zu verwenden sind.

| Ich bin   | Installieren und Ausführen von Windows Admin Center | Server Manager unter Windows Server ausführen | Server Manager in RSAT unter Windows 10 ausführen |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Benutzer an einem Windows 10-PC | X  |                                      | X                                        |
| Benutzer an einem Windows Server-System, das mit der Desktopoberfläche arbeitet | X | X | X |
| Benutzer an einem Windows Server-System, das mit Server Core arbeitet |X (unter Windows 10 installieren, verwenden zum Verwalten von Server Core) | | X |
| weit von meinem Windows Server-System entfernt |X | | X |
| weit von meinem Windows Server-System entfernt, das mit der Desktopoberfläche arbeitet |X | Verwendung von RDS für die Remoteverbindung mit dem Server, dann Verwendung von Server-Manager | X |

Zusätzlich zu den unten aufgeführten Tools können Sie auch [Remotedesktopdienste](../remote/remote-desktop-services/welcome-to-rds.md) für den Zugriff auf lokale, remote und virtuelle Server verwenden. Dann können Sie mit Server-Manager Verwaltungsaufgaben ausführen.

### <a name="manage-on-premises-systems-remote-systems-and-systems-without-ui-with-windows-admin-center"></a>Verwalten von lokalen Systemen, remote-Systemen und Systemen ohne Benutzeroberfläche mit Windows Admin Center
[Windows Admin Center](../manage/windows-admin-center/overview.md) ist eine browserbasierte Management-App, die die lokale Verwaltung von Windows-Servern ohne Abhängigkeit von Azure oder der Cloud ermöglicht. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Server-Infrastruktur und ist besonders nützlich für die Verwaltung auf privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center auf Windows 10, auf einem Gatewayserver oder direkt auf dem Windows Server System installieren, das Sie verwalten möchten.

>[!NOTE]
>Windows Admin Center ist der offizielle Name was von "Projekt Honolulu."

### <a name="manage-on-premises-systems-with-server-manager"></a>Verwalten von lokalen Systemen mit Server-Manager
[Server-Manager](server-manager/server-manager.md) ist eine Verwaltungskonsole, die in der vollständigen Installation von Windows Server enthalten ist. (Es ist nicht verfügbar für Installationen, die keine Benutzeroberfläche haben – Server Core Server-Manager beinhaltet keine). Verwenden von Server-Manager zum Installieren und Entfernen von Serverrollen, hinzufügen und Entfernen von Remoteservern, starten und Beenden von Diensten und Anzeigen von Daten über Ihre Umgebung gesammelt.

### <a name="manage-remote-systems-and-systems-without-ui-with-remote-server-administration-tools-rsat"></a>Verwalten von Remotesystemen und Systemen ohne Benutzeroberfläche mit Remote Server Administration Tools (RSAT)
Wenn Ihre Umgebung Installationen von Server Core oder Remoteservern (lokal oder virtuelle Computer) enthält, können Sie diese Systeme mithilfe der [Remote Server Administration Tools (RSAT)](../remote/remote-server-administration-tools.md) verwalten. RSAT enthält Server-Manager, sodass Sie alle Ihre Server verwalten können.

> [!IMPORTANT]
> RSAT wird unter Windows 10 ausgeführt. RSAT kann nicht unter Windows Server Core installiert werden.

Server Core-Installationen können über die Befehlszeile verwaltet werden. Weitere Informationen finden Sie unter [Grundlegende Verwaltungsaufgaben in Server Core](server-core/server-core-administer.md).

### <a name="manage-updates-to-windows-server-systems"></a>Verwalten von Updates für Windows Server-Systeme
Sie können [Windows Server Update Services (WSUS)](windows-server-update-services/get-started/windows-server-update-services-wsus.md) verwenden, um Updates für die Systeme in Ihrer Windows Server -Umgebung zu verwalten und bereitzustellen.

## <a name="gather-information-about-your-environment"></a>Sammeln von Informationen über die Umgebung
Viele der Entscheidungen, die Sie als Administrator treffen, hängen von Daten über Systeme und Benutzer in Ihrer Umgebung ab. Verwenden Sie die folgenden Informationen und Tools, um solche Daten zu sammeln.

Beginnen Sie mit [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](/windows/configuration/configure-windows-diagnostic-data-in-your-organization). Dort finden Sie Informationen über die Diagnosedaten, die von Windows 10 und Windows Server gesammelt werden können.

### <a name="setup-and-boot-event-collectionget-started-with-setup-and-boot-event-collectionmd"></a>[Setup und Start-Ereignissammlung](get-started-with-setup-and-boot-event-collection.md)
Das Feature „Setup and Boot Event Collection”ermöglicht die Festlegung eines Sammelcomputers, der eine Reihe von wichtigen Ereignissen erfasst, die auf anderen Computern auftreten, während diese Computer gestartet werden oder den Setupvorgang durchlaufen. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren. 

### <a name="software-inventory-logging-silsoftware-inventory-loggingget-started-with-software-inventory-loggingmd"></a>[(SIL) Protokollierung des Softwarebestands](software-inventory-logging/get-started-with-software-inventory-logging.md)

Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet sie die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.

### <a name="user-access-logging-ualuser-access-loggingget-started-with-user-access-loggingmd"></a>[User Access Logging (UAL)](user-access-logging/get-started-with-user-access-logging.md)

Die Benutzerzugriffsprotokollierung aggregiert eindeutige Ereignisse auf Clientgeräten sowie Benutzeranforderungsereignisse, die auf einem Computer unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einer lokalen Datenbank protokolliert wurden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen. Zudem bietet UAL auch Nicht-Microsoft-Softwareentwicklern die Möglichkeit, ihre UAL-Ereignisse zu instrumentieren und zu aggregieren. 

## <a name="tune-your-windows-server-environment-for-performance"></a>Leistungsoptimierung für die Windows Server-Umgebung
Verwenden Sie die folgende Informationen, um Ihre Umgebung leistungsmäßig zu optimieren.

### <a name="performance-tuning-guidelinesperformance-tuningindexmd"></a>[Richtlinien zur leistungsoptimierung](performance-tuning/index.md)
Nutzen Sie eine Reihe von Richtlinien, mit denen Sie die Servereinstellungen in Windows Server 2016 optimieren und Leistungs- oder Energieeffizienzsteigerungen erzielen können, insbesondere wenn sich die Art der Auslastung im Laufe der Zeit nur wenig ändert.

### <a name="microsoft-server-performance-advisorserver-performance-advisormicrosoft-server-performance-advisormd"></a>[Microsoft Server Performance Advisor](server-performance-advisor/microsoft-server-performance-advisor.md)

Mit Microsoft Server Performance Advisor (SPA) können Sie Messdaten sammeln, um Leistungsprobleme auf Windows-Servern unauffällig zu diagnostizieren, ohne Softwareagenten hinzuzufügen oder Produktionsserver neu zu konfigurieren. SPA generiert umfassende Berichte und historische Diagramme mit Empfehlungen.


## <a name="automate-windows-server-management"></a>Automatisieren der Windows Server-Verwaltung

Windows Server enthält eine Reihe von Befehlen und Windows PowerShell-Modulen, die Sie zum Automatisieren von Verwaltungsaufgaben verwenden können.

### <a name="windows-powershellpowershellscriptingpowershell-scriptingviewpowershell-51"></a>[Windows PowerShell](/powershell/scripting/powershell-scripting?view=powershell-5.1)
Windows PowerShell ist eine Sprache für die Befehlszeile und zudem eine Skriptsprache, mit der Sie Verwaltungsaufgaben schnell automatisieren können. 

### <a name="windows-commandswindows-commandswindows-commandsmd"></a>[Windows-Befehle](windows-commands/windows-commands.md)

Die Windows-Befehlszeilentools dienen zum Durchführen von Verwaltungsaufgaben in Windows. Mit der Befehlsreferenz können Sie sich mit den Befehlszeilentools vertraut machen, mehr über die Befehlsshell erfahren und Befehlszeilenaufgaben mithilfe von Stapeldateien oder Skripting-Tools automatisieren.

## <a name="windows-server-insider-preview"></a>Windows Server-Insider – Vorschau
### <a name="system-insightsmanagesystem-insightsoverviewmd"></a>[System-Einblicke](..\manage\system-insights\overview.md)
Systemeinblicke ist ein neues Feature, das auf Windows Server systemintern vorhersehbare Analytics einführt. Diese Funktionen analysieren lokal vorhersehbare Windows Server Systemdaten, wie die Leistungsindikatoren oder ETW-Ereignisse, und helfen IT-Administratoren proaktiv problematische Verhalten in ihrer Bereitstellung zu entdecken und zu beheben. 
