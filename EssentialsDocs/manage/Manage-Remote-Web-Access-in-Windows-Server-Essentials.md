---
title: Verwalten des Remotewebzugriffs in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3ea40fa-b6ba-4d66-b754-221ca6271387
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: de01b2fd2395377b6e7b3349b9862eb0e51a59b8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-remote-web-access-in-windows-server-essentials"></a>Verwalten des Remotewebzugriffs in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 Remote Web Access in Windows Server Essentials oder in Windows Server2012 R2 mit installierter Windows Server Essentials Experience-Rolle, bietet eine optimierte, Fingereingabe geeignete Browserfunktionen, für den Zugriff auf Anwendungen und Daten von jedem beliebigen Standort, dass eine Internetverbindung und über fast alle Geräte. Um den Remotewebzugriff zu verwenden, müssen Sie zuerst aktivieren sie mithilfe der überall Zugriff Assistenten zum Einrichten und richten Sie den Router und Domänennamen.  
  
## <a name="in-this-topic"></a>In diesem Thema  
  
-   [Aktivieren Sie und konfigurieren Sie des Remotewebzugriffs](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Einrichten des Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Richten Sie Ihren Domänennamen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Anpassen von Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Beheben von Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_5)  
  
##  <a name="BKMK_1"></a>Aktivieren Sie und konfigurieren Sie des Remotewebzugriffs  
 In den folgenden Themen helfen Sie aktivieren und Konfigurieren des Remotewebzugriffs:  
  
-   [Remote Web Access (Übersicht)](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [Turn Sie on Remote Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)  
  
-   [Ändern Sie Ihrer Region](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Region)  
  
-   [Verwalten der Remotewebzugriffsberechtigungen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManagePerms)  
  
-   [Sicherer Remotewebzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SecureRWA)  
  
-   [Verwalten von Web Access für Remotedesktop und VPN-Benutzern](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManageRWAVPN)  
  
###  <a name="BKMK_Overview"></a>Remote Web Access (Übersicht)  
 Wenn Sie nicht im Büro sind, können Sie einen Webbrowser öffnen und Zugriff auf Remote Web Access von jedem beliebigen Standort, der über Internetzugriff verfügt. In Remote Web Access können Sie folgende Aktionen ausführen:  
  
-   Zugriff auf freigegebene Dateien und Ordner auf dem Server.  
  
-   Zugriff auf Ihre Server und Computer im Netzwerk. Dies bedeutet, dass Sie auf den Desktop von einem Computer im Netzwerk zugreifen können, als säßen Sie direkt vor dem am Arbeitsplatz.  
  
  Remote Web Access ist standardmäßig nicht aktiviert. Beim Ausführen der überall den Assistenten zum Einrichten, versucht der Assistent zum Einrichten von den Router und dem Internet verbunden. Nach dem Remote Web Access aktiviert ist, können Sie einen Domänennamen für den Server einrichten und Remotewebzugriff anpassen. Sie können auch den Router erneut einrichten, wenn Sie den Router wechseln.  
  
 Über die Berechtigung zum Zugriff auf Remote Web Access wird nicht automatisch gewährt, wenn Sie ein neues Benutzerkonto hinzufügen. Wenn Sie ein Benutzerkonto hinzufügen, können Sie den Zugriff auf freigegebene Ordner, der Medienbibliothek, Computer, Links zur Startseite und dem serverdashboard ermöglichen. Sie können auch angeben, dass ein Benutzer nicht Remote Web Access verwenden darf.  
  
 Die Remote Web Access-Einstellung wird für jedes Benutzerkonto angezeigt, auf die **Benutzer** Windows Server Essentials-Dashboard auf der Registerkarte. Um die Remotewebzugriff-Einstellung zu ändern, mit der rechten Maustaste des Benutzerkontos, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
###  <a name="BKMK_TurnOnRWA"></a>Turn Sie on Remote Web Access  
 Sie können durch Ausführen der überall den Assistenten zum Einrichten von Server-Dashboard Remote Web Access aktivieren.  
  
##### <a name="to-turn-on-remote-web-access"></a>So aktivieren Sie Remote Web Access  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
3.  Klicken Sie auf **konfigurieren**. Der überall Zugriff-Assistent wird angezeigt.  
  
4.  Auf der **Funktionen für Zugriff überall aktivieren** Seite auf die **Remote Web Access** Kontrollkästchen.  
  
5.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
###  <a name="BKMK_Region"></a>Ändern Sie Ihrer Region  
 Sie müssen Netzwerkadministrator so ändern Sie die Einstellung der Region in Windows Server Essentials sein.  
  
##### <a name="to-change-the-region-setting"></a>So ändern Sie die Einstellung der Region  
  
1.  Öffnen Sie auf einem Computer, der mit Windows Server Essentials verbunden ist das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**.  
  
3.  Auf der **allgemeine** Registerkarte, klicken Sie auf den Dropdownliste in der **Land/Region des Servers** Abschnitt.  
  
4.  Wählen Sie die neue Region aus der Dropdownliste, und klicken Sie dann auf **übernehmen** an die neue regionseinstellung zu bestätigen.  
  
###  <a name="BKMK_ManagePerms"></a>Verwalten der Remotewebzugriffsberechtigungen  
 Wenn Sie ein Benutzerkonto in Windows Server Essentials hinzufügen, ist der neue Benutzer standardmäßig zulässig, Remote Web Access verwenden. Wenn Sie nicht zulassen Remotewebzugriff für ein Benutzerkonto, und suchen Sie der Benutzer den Remotewebzugriff verwenden muss, können Sie die Eigenschaften des Benutzerkontos s aktualisieren.  
  
##### <a name="to-manage-remote-web-access-permissions-for-a-user-account"></a>Zum Verwalten von Remotewebzugriff-Berechtigungen für ein Benutzerkonto  
  
1.  Melden Sie sich auf das Dashboard, und klicken Sie dann auf **Benutzer**.  
  
2.  Klicken Sie auf das Benutzerkonto, das Sie verwalten möchten, und klicken Sie dann auf **Kontoeigenschaften anzeigen** in der **Aufgaben** Bereich.  
  
3.  In der **Eigenschaften** Dialogfeld, klicken Sie auf die **"Zugriff überall"** Registerkarte.  
  
4.  Auf der **"Zugriff überall"** Registerkarte die **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen** Kontrollkästchen, um Benutzer mit dem Server mit Remotewebzugriff herstellen kann.  
  
5.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
 Weitere Informationen finden Sie unter [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_SecureRWA"></a>Sicherer Remotewebzugriff  
 Windows Server Essentials verwendet ein Sicherheitszertifikat, um die Informationen zu sichern, die zwischen der Software und einem Webbrowser ausgetauscht werden. Wenn Sie die Connector-Software auf Ihren Computern installieren, wird das Sicherheitszertifikat für Windows Server Essentials der Liste der vertrauenswürdigen Zertifikate auf Ihren Computern hinzugefügt. Die beste Möglichkeit für Benutzer Remote Web Access zugreifen, wenn sie nicht im Büro sind ist die Verwendung ein tragbares Computers, das die Connector-Software installiert wurde.  
  
> [!WARNING]
>  Benutzer, die Remotewebzugriff von öffentlichen Standorten oder anderen nicht vertrauenswürdigen Computern verwenden, sollten sicherstellen, dass sie vor dem Verlassen des Computers für die unbeaufsichtigte Installation der Website abmelden oder wenn sie ihre Sitzung beendet haben.  
  
###  <a name="BKMK_ManageRWAVPN"></a>Verwalten von Web Access für Remotedesktop und VPN-Benutzern  
 Sie können VPN zum Verbinden mit Windows Server Essentials und Zugriff auf alle Ressourcen, die auf dem Server gespeichert sind. Dies ist besonders hilfreich, wenn Sie einen Clientcomputer verfügen, der mit Netzwerkkonten eingerichtet ist, die für die Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung verwendet werden können. Alle neu erstellten Benutzerkonten auf dem gehosteten Windows Server Essentials-Server müssen auf dem Client-Computer zum ersten Mal anmelden VPN verwenden.  
  
##### <a name="to-set-vpn-and-remote-web-access-permissions-for-network-users"></a>VPN- und Remotewebzugriff-Berechtigungen für Netzwerkbenutzer fest  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie per Remotezugriff auf den Desktop gewähren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, klicken Sie auf die **"Zugriff überall"** Registerkarte.  
  
6.  Auf der **"Zugriff überall"** Registerkarte, gehen Sie folgendermaßen vor:  
  
    1.  Einen Benutzer eine Verbindung mit dem Server über VPN, Aktivieren der **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen.  
  
    2.  Damit einen Benutzer mithilfe von Remote Web Access eine Verbindung mit dem Server herstellen kann, wählen Sie die **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen** Kontrollkästchen.  
  
7.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_2"></a>Einrichten des Routers  
 Beim Konfigurieren des Servers für den Remotewebzugriff versucht den Anywhere Access-Assistenten, um den Router einzurichten. Wenn Sie Router oder Einstellungen des Routers ändern, müssen Sie den Ihrer Router-Assistenten erneut ausführen. Weitere Informationen finden Sie unter den folgenden Themen:  
  
-   [Einrichten des Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpRouter)  
  
-   [Ersetzen eines Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ReplaceRouter)  
  
-   [Festgelegte Netzwerkadresse](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_NetworkLocation)  
  
-   [Aktivieren Sie Remote Desktop Services-ActiveX-Steuerelemente](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ActiveX)  
  
###  <a name="BKMK_SetUpRouter"></a>Einrichten des Routers  
 Windows Server Essentials versucht, während dieses Schrittsden Router anhand von UPnP-Befehlen automatisch zu konfigurieren. Zu diesem Zweck muss der Router UPnP-Standards unterstützen, und die UPnP-Einstellung muss auf dem Router aktiviert werden.  
  
> [!NOTE]
>  Die Netzwerkverbindung sollte die unterstützte Netzwerkanforderung für Windows Server Essentials erfüllen. Es sollte nur ein Router im Netzwerk vorhanden sein.  
  
 Wenn der Router nicht durch den der Domäne Name-Assistenten festgelegt ist, müssen Sie Port 443 manuell weiterleiten. Weitere Informationen zum Einrichten der portweiterleitung auf dem Router finden Sie unter [Routereinrichtung](https://social.technet.microsoft.com/wiki/contents/articles/windows-small-business-server-2011-essentials-router-setup.aspx).  
  
###  <a name="BKMK_ReplaceRouter"></a>Ersetzen eines Routers  
 Ersetzen Sie den Router gemäß den Anweisungen des Herstellers s, und führen Sie den Ihrer Router-Assistenten die neue Router konfigurieren.  
  
##### <a name="to-set-up-your-new-router"></a>Zum Einrichten des neuen Routers  
  
1.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf **Einstellungen**.  
  
2.  Klicken Sie auf die **"Zugriff überall"** Registerkarte, und klicken Sie dann in der **Router** auf **einrichten**. Der Ihrer Router-Assistent wird gestartet.  
  
3.  Folgen Sie den Anweisungen im Assistenten zum Abschließen der Einrichtung des neuen Routers.  
  
###  <a name="BKMK_NetworkLocation"></a>Festgelegte Netzwerkadresse  
 Eine Netzwerkadresse ist eine Sammlung von Netzwerkeinstellungen, die Windows angewendet, wenn Sie eine Verbindung mit einem Netzwerk herstellen. Die Einstellungen variieren und können basierend auf den Typ des Netzwerks, mit denen Sie angepasst werden. Die Einstellungen für eine Netzwerkadresse bestimmen, ob bestimmte Features (z.B. Datei- und Druckerfreigabe, Netzwerkerkennung und Freigabe öffentlicher Ordner) aktiviert oder deaktiviert werden. Netzwerkadressen sind nützlich, wenn Sie mit unterschiedlichen Netzwerken herstellen müssen.  
  
 Beispielsweise können Sie einen Laptop besitzen, den Sie zu Hause und bei der Arbeit verwenden. Wenn Sie im Büro sind, verbinden Sie sich mit dem Firmennetzwerk. Wenn Sie allerdings stammen privat, Sie verwenden Ihren Laptop zugreifen und Wiedergeben von Videos und Musik, die auf dem Heimserver gespeichert sind. Wenn Sie eine Verbindung mit einem neuen Netzwerk herstellen und den adressenart angeben, weist Windows ein Netzwerkprofil, die für diesen Speicherort voreingestellt ist. Beim nächsten Herstellen einer Verbindung mit diesem Netzwerk Windows erkennt das Netzwerk und weist automatisch die richtigen Einstellungen. Dadurch wird eine Sicherheitsebene zum Schutz der Informationen auf Ihrem Computer hinzugefügt, und nur die Netzwerkfeatures, die Sie für diesen Speicherort benötigen eingeschaltet sind.  
  
 Es gibt vier Arten von Netzwerkadressen:  
  
-   **Heimnetzwerk** wählen Sie dieses Netzwerk für Heimnetzwerke oder wenn Sie kennen und die Personen und Geräte im Netzwerk vertrauen. Computer in einem Heimnetzwerk können einer Heimnetzgruppe angehören. Die Netzwerkermittlung ist für Heimnetzwerke, können Sie andere Computer und Geräte im Netzwerk anzeigen und ermöglicht das andere Benutzer im Netzwerk Ihren Computer sehen aktiviert.  
  
-   **Firmennetzwerk** wählen Sie dieses Netzwerk für kleine Firmennetzwerke oder andere Arbeitsplatznetzwerke. Die Netzwerkermittlung, können Sie andere Computer und Geräte im Netzwerk anzeigen und andere Benutzer im Netzwerk Ihren Computer sehen kann, ist standardmäßig aktiviert, aber Sie können nicht erstellt oder eine Heimnetzgruppe beitreten.  
  
-   **Öffentliches Netzwerk** wählen Sie dieses Netzwerk für die öffentlichen Orten (z.B. her und Flughäfen). Dieser Ort dient zu verhindern, dass Ihr Computer für andere Computer sichtbar und zum Schutz Ihres Computers vor schädlicher Software aus dem Internet. Heimnetzgruppe ist nicht verfügbar in öffentlichen Netzwerken und die Netzwerkermittlung deaktiviert ist. Sie sollten diese Option auch auswählen, wenn Sie direkt mit dem Internet verbunden sind, ohne einen Router zu verwenden, oder wenn Sie eine mobile Breitbandverbindung haben.  
  
-   **Domäne** wählen Sie dieses Netzwerk für die, wie Sie beispielsweise an Arbeitsplätzen in Unternehmen Arbeitsplätze. Diese Art von Netzwerkadresse wird vom Netzwerkadministrator gesteuert und kann nicht ausgewählt oder geändert.  
  
###  <a name="BKMK_ActiveX"></a>Aktivieren Sie Remote Desktop Services-ActiveX-Steuerelemente  
 Remote Desktop Services ActiveX-Steuerelemente können Sie Zugriff auf Ihren Heim- oder Computer, über das Internet, von einem anderen Computer mithilfe von Remotewebzugriff.  
  
##### <a name="to-enable-remote-desktop-services-activex-controls"></a>So aktivieren Sie Remote Desktop Services-ActiveX-Steuerelemente  
  
1.  In Internet Explorer, klicken Sie auf **Tools**, und klicken Sie dann auf **Internetoptionen**.  
  
2.  Auf der **Security** auf **Stufe**.  
  
3.  In der **ActiveX-Steuerelemente und Plug-Ins** Abschnitt, gehen Sie folgendermaßen vor:  
  
    1.  Klicken Sie unter **Download von signierten ActiveX-Steuerelementen**, klicken Sie auf **Eingabeaufforderung**.  
  
    2.  Klicken Sie unter **Ausführen von ActiveX-Steuerelemente und Plug-Ins**, klicken Sie auf **aktivieren**.  
  
4.  Klicken Sie auf **OK** zweimal, um die Änderungen zu übernehmen und das Dialogfeld zu schließen.  
  
##  <a name="BKMK_3"></a>Richten Sie Ihren Domänennamen  
 Nach dem Einschalten des Remotewebzugriffs können Sie einen Domänennamen für den Server einrichten, auf denen Windows Server Essentials ausgeführt wird. Dies ist ein erforderlicher Schritt, wenn Sie den Remotewebzugriff auf einem Remotecomputer verwenden möchten. Weitere Informationen finden Sie unter den folgenden Themen:  
  
-   [Übersicht über Domänennamen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_DNOverview)  
  
-   [Verstehen von persönlichen Microsoft-Domänennamen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_PersonalizedNames)  
  
-   [Verwenden eines neuen oder vorhandenen Domänennamens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UseNewName)  
  
-   [Einrichten eines Domänennamens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpName)  
  
-   [Wählen Sie einen Domain Name Service-Anbieter](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseProvider)  
  
-   [Wählen Sie einen Domänennamen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseDomainName)  
  
-   [Wählen Sie ein domänennamenpräfix](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Prefixes)  
  
-   [Auswählen einer domänennamenerweiterung](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Extension)  
  
-   [Aktualisieren oder ein Upgrade Ihres Domain Name Service](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UpdateService)  
  
-   [Exportieren Sie oder importieren Sie Ihres Zertifikats auf dem Server](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ExportCert)  
  
-   [Manuelles Einrichten eines Domänennamens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetNameManually)  
  
-   [Suchen von Domain Name Service-Anbieter](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Find)  
  
###  <a name="BKMK_DNOverview"></a>Übersicht über Domänennamen  
 Ein Domänennamen wird den Server im Internet eindeutig identifiziert. Domänennamen bestehen aus mindestens zwei Teilen: einen Namen der Domäne der obersten Ebene (TLD) und einen zweiten Ebene Domänennamen. In contoso.com, z.B. com ist die TLD und Contoso ist der zweiten Ebene Domänenname.  
  
 Wenn Sie nicht im Büro sind, können Sie Ihren Domänennamen, den Zugriff auf freigegebene Dateien auf dem Server oder Computer im Netzwerk. Sie können auch auf den Server verwalten, wenn Sie unterwegs sind. Beispielsweise können Sie contoso.com für den Server registrieren. Wenn Sie nicht im Büro sind, können Sie einen Webbrowser auf Ihrem Laptop und Typ öffnen **contoso.com** in das adressentextfeld eine Verbindung mit der Instanz des Remotewebzugriffs, die Sie in Windows Server Essentials einrichten.  
  
###  <a name="BKMK_PersonalizedNames"></a>Verstehen von persönlichen Microsoft-Domänennamen  
 Ein personalisierten Domänennamen von Microsoft enthält die folgenden Features:  
  
-   Einen benutzerdefinierten Domänennamen für den Remotewebzugriff (z.B. *ihrhostname*. Remotewebaccess.com). Der Domänenname ist Ihrer öffentlichen IP-Adresse zugeordnet.  
  
-   Eine dynamische DNS-aktualisieren Protokolldienst, damit Remote Web Access Verwendung Ihres Domänennamens wird nicht unterbrochen werden, wenn sich Ihre öffentliche IP-Adresse ändert. In der Regel bieten Internetdienstanbieter (ISP) für Ihre Organisation s-breitbandverbindungen dynamische öffentliche IP-Adressen, die geändert werden können.  
  
-   Ein vertrauenswürdiges Zertifikat, mit dem Domänennamen verknüpft ist.  
  
 Um einen personalisierten Domänennamen von Microsoft in Ihren Server integrieren möchten, benötigen Sie ein Microsoft-Konto (früher als Windows Live ID bezeichnet). Wenn Sie nicht über ein Microsoft-Konto verfügen, Sie können sich anmelden bei der [Microsoft Hotmail](https://login.live.com/) Website.  
  
> [!IMPORTANT]
>  Windows Live erlaubt die Sonderzeichen in Ihrem Microsoft-Konto-Kennwort, das der Server nicht unterstützt. Wenn Sie eine personalisierte Microsoft-Domäne verwenden, stellen Sie sicher, dass das Kennwort für Ihr Microsoft-Konto nur Zeichen enthält, die der Server unterstützt. Der Server unterstützt nicht die Verwendung der Zeichen $, /, ', und %.  
  
###  <a name="BKMK_UseNewName"></a>Verwenden eines neuen oder vorhandenen Domänennamens  
 Um den Namen Ihrer Domäne auf einem Server unter Windows Server Essentials automatisch einzurichten, müssen Sie einen Domain Name Service-Anbieter verwenden, der in den des Domain Name-Assistenten aufgeführt ist. Sie können einen neuen Domänennamen erhalten oder einen vorhandenen Domänennamen verwenden. Führen Sie einen der folgenden:  
  
-   Sie erhalten einen neuen Domänennamen aus der Domäne Name Service-Anbieter aufgeführt sind im Assistenten, klicken Sie auf Wunsch **ich einen neuen Domänennamen einrichten möchten**.  
  
-   Wenn Sie einen vorhandenen Domänennamen, den Sie von einem der unterstützten Domain Name Service-Anbieter erworben haben verfügen, können Sie den Ihrer Domain Name-Assistenten, den Domänennamen für den Server einrichten. Klicken Sie auf **ich möchte einen Domänennamen verwenden ich bereits besitze**, und geben Sie den Domänennamen in die **legen Sie Ihren Domänennamen** Textfeld. Sie müssen angeben, den Benutzernamen und Kennwort, das Sie zum Erwerb des Domänennamens verwendet haben.  
  
-   Wenn Sie haben einen vorhandenen Domänennamen, den Sie von einem Domain Name Service-Anbieter erworben haben, die von Windows Server Essentials nicht unterstützt wird und Sie den Ihrer Domain Name-Assistenten zu verwenden, um den Domänennamen für den Server einrichten möchten, können Sie den Domänennamen zu einem der im Assistenten aufgeführten Domain Name Service-Anbieter übertragen. Klicken Sie auf **ich möchte einen Domänennamen verwenden ich bereits besitze**, geben Sie den Domänennamen in die **Domänennamen** Text ein, und folgen Sie dann die Anweisungen auf der Website Domain Name Service s-Anbieter den Domänennamen zu übertragen.  
  
###  <a name="BKMK_SetUpName"></a>Einrichten eines Domänennamens  
 Wenn Sie den Remotewebzugriff aktivieren, können Sie den Internetdomänennamen des Servers einrichten.  
  
##### <a name="to-set-up-or-manage-an-internet-domain-name"></a>Einrichten oder Verwalten eines Internetdomänennamens  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **servereinstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
3.  In der **Domänennamen** auf **einrichten**.  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen. Wenn Sie einen Domänennamen und das Zertifikat noch nicht besitzen, der Assistenten können Sie einen Domain Name-Anbieter und ein Zertifikat erwerben oder erhalten Sie einen personalisierten Domänennamen von Microsoft.  
  
###  <a name="BKMK_ChooseProvider"></a>Wählen Sie einen Domain Name Service-Anbieter  
 Sie sollten einen Domain Name Service-Anbieter auswählen, der die domänennamenerweiterung unterstützt, die Sie verwenden möchten. Den des Domain Name-Assistenten enthält eine Liste qualifizierter Anbieter, die Sie mit einem Link zu jeder Website des Anbieters s verwenden können. Klicken Sie auf die **mehr Informationen** links neben jeder s-Anbieter zum Abrufen von Informationen zu den Diensten und Preisen, die vom Anbieter angeboten werden.  
  
> [!NOTE]
>  Einige Domain Name Service-Anbieter bedienen international Breite Regionen und andere in kleineren Märkten tätig. Aus diesem Grund können einige Anbieter keine Website anbieten, die Ihre bevorzugte Sprache übersetzt wird.  
  
 Wenn Sie Ihren Domänennamen erwerben, können Sie auch Protokolldienst die Domain Name System (DNS) dynamische Updates vom Domain Name Service-Anbieter. DNS-Protokoll für dynamische Updates ist ein Dienst, der jeder im Internet Zugriff auf Ressourcen in einem lokalen Netzwerk, wenn die IP-Adresse des Netzwerks ständig ändern kann. Oder Sie können eine statische IP-Adresse von Ihrem Internet Internetdienstanbieter (ISP) um sicherzustellen, die Ihre IP-Adresse nicht ändert.  
  
###  <a name="BKMK_ChooseDomainName"></a>Wählen Sie einen Domänennamen  
 Wählen Sie einen Namen, der Ihren geschäftssserver eindeutig identifiziert. Wenn Ihr Unternehmen den Namen Contoso Ltd hat, können Sie z.B. Contoso zur eindeutigen Identifizierung von Ihrem Heim- oder Geschäftsserver im Internet auswählen. Wenn der Domänenname nicht verfügbar ist, probieren Sie eine Variante dieses Namens, oder wählen Sie einen völlig anderen.  
  
 Die von Ihnen eingegebene Name kann Folgendes enthalten:  
  
-   Maximale Länge 63 Zeichen  
  
-   Buchstaben (englische oder lokalisierten Zeichen), Zahlen oder Bindestriche (-). Der Name muss beginnen und enden mit einem Buchstaben oder einer Zahl.  
  
    > [!NOTE]
    >  Domänennamen werden nicht zwischen Groß- und Kleinschreibung unterschieden.  
  
###  <a name="BKMK_Prefixes"></a>Wählen Sie ein domänennamenpräfix  
 Ein Domänenname besteht aus hierarchischen Bezeichnungen.  
  
 **Die Domäne der obersten Ebene Erweiterung** ist die Bezeichnung ganz rechts im Domänennamen. Beispielsweise ist in www.contoso.com, com der domänennamenerweiterung der obersten Ebene.  
  
 **Der Domänenname der zweiten Ebene** ist die Bezeichnung neben der domänennamenerweiterung der obersten Ebene. Der Domänenname der zweiten Ebene wird häufig basierend auf den Firmennamen, Produkte oder Dienste erstellt. Beispielsweise wird in www.contoso.com, ein Contoso ist der Domänenname der zweiten Ebene und wurde für den Firmennamen von Contoso Pharmaceuticals gewählt. Die Domäne der zweiten Ebene wird manchmal als Hostname bezeichnet die IP-zugeordnet Adresse.  
  
 **Das domänennamenpräfix** identifiziert eine Unterdomäne. Der Name der Unterdomäne kann verwendet werden, um Dienste, Geräte oder Regionen zu identifizieren. Z.B. Contoso Pharmaceuticals möchte Remotebenutzern mit Remote Web Access anmelden zu ermöglichen, aber möchte nicht, dass die Website für die Öffentlichkeit verfügbar sein, damit sie eine untergeordnete Domäne, die nur Benutzer mit entsprechenden Berechtigungen erstellen auf die Website zugreifen können. Contoso Pharmaceuticals richtet remote.contoso.com als die Unterdomäne ein, und das domänennamenpräfix ist.  
  
> [!TIP]
>  Es wird empfohlen, das standardmäßige **Remote** als Präfix für Ihren Domänennamen.  
  
###  <a name="BKMK_Extension"></a>Auswählen einer domänennamenerweiterung  
 Wenn Sie einen Domänennamen für Ihre Website auswählen, müssen Sie auch die domänennamenerweiterung angeben, die Sie verwenden möchten. Die Erweiterung wird durch den Buchstaben identifiziert, die auf den letzten Punkt in einem Domänennamen folgen. (Formal heißt diese für die Erweiterung ist die Domäne der obersten Ebene oder TLD).  
  
 Es gibt zwei Haupttypen von domänenerweiterungen an, die Sie verwenden können: generischen und Ländercode.  
  
#### <a name="generic-top-level-domains"></a>Allgemeine Domänen der obersten Ebene  
 Allgemeine domänenerweiterungen sind mindestens drei Buchstaben lang, und sie werden in der Regel von bestimmten Typen von Organisationen verwendet.  
  
 **Beispiele für allgemeine Domänen der obersten Ebene**  
  
|Domänenerweiterung|Beschreibung|  
|----------------------|-----------------|  
|.com|In der Regel von kommerziellen Organisationen verwendet, aber es kann von jedem verwendet werden.|  
|.NET|Speziell für Unternehmen, die Netzwerkinfrastrukturdienste anbieten.|  
|.org|Ursprünglich verwendet von gemeinnützigen Organisationen und anderen Unternehmen, die nicht in einer anderen Domäne der obersten Ebene allgemeine Kategorie fallen. Kann von jedem verwendet werden.|  
|.edu|Für die Verwendung durch ausbildungseinrichtungen eingeschränkt.|  
  
#### <a name="country-code-top-level-domains"></a>Ländercode Domänen der obersten Ebene  
 Diese Domänen umfassen zwei Buchstaben. Sie sollen von Organisationen im Land oder Region, die mit diesem Code verknüpft ist, verwendet werden. Einige Ländercode Domänen der obersten Ebene sind für die Verwendung durch Angehörige des Landes oder der Region beschränkt. Andere sind für die Verwendung von allen Benutzern zur Verfügung.  
  
 **Beispiele für Ländercode Domänen der obersten Ebene**  
  
|Domänenerweiterung|Beschreibung|  
|----------------------|-----------------|  
|einer|Für die Verwendung durch Websites in Kanada|  
|Level|Für die Verwendung durch Websites in China|  
|.de|Für die Verwendung durch Websites in Deutschland|  
|. co.uk|Für die Verwendung durch Websites im Vereinigten Königreich|  
  
 Die vollständige Liste der Domänen der obersten Ebene finden Sie unter der [Internet Assigned Numbers Authority Website](https://go.microsoft.com/fwlink/?LinkId=117438).  
  
#### <a name="if-a-domain-extension-is-not-available-to-select-in-the-set-up-domain-name-wizard"></a>Wenn eine domänenerweiterung nicht in den Domain Name-Assistenten ausgewählt ist  
 Wenn Sie den Domain Name-Assistenten ausführen, sucht der Assistent die Systeminformationen Ihrem Land oder Ihrer Region zu ermitteln. Der Assistent zeigt dann nur die domänenerweiterungen an, die die teilnehmenden Anbieter in Ihrer Nähe zu unterstützen. Wenn die domänenerweiterung, die Sie möchten nicht in der Liste angezeigt wird, müssen Sie weiterhin eine andere domänenerweiterung wählen. Wählen Sie eine Erweiterung aus der Liste, die vom Assistenten zurückgegebenen.  
  
###  <a name="BKMK_UpdateService"></a>Aktualisieren oder ein Upgrade Ihres Domain Name Service  
 Sie müssen möglicherweise aktualisieren oder ein Upgrade Ihres Domain Name Service, wenn Sie einen Domänennamen gekauft, aber ein Zertifikat nicht erworben. Sie müssen ein Zertifikat für Ihren Domänennamen von Domain Name Service-Anbieter verfügen.  
  
> [!NOTE]
>  Arbeiten Sie mit Domain Name Service-Anbieter den Typ des Zertifikats zu bestimmen, die Sie benötigen. Das Zertifikat kann eines kostengünstigen Zertifikate sein, die angeboten werden. Sie sollten jedoch überprüfen, die Dokumentation und die Features von höherer Sicherheit auf Zertifikate zu bestimmen, ob sie Anforderungen Ihres Unternehmens besser erfüllen.  
  
###  <a name="BKMK_ExportCert"></a>Exportieren Sie oder importieren Sie Ihres Zertifikats auf dem Server  
 Wenn Sie eine Sicherungskopie eines Zertifikats erstellen oder auf einem anderen Server verwenden möchten, müssen Sie das Zertifikat exportieren. Informationen zum Exportieren von Zertifikaten finden Sie unter [Exportieren eines Zertifikats](https://go.microsoft.com/fwlink/p/?LinkId=214362).  
  
###  <a name="BKMK_SetNameManually"></a>Manuelles Einrichten eines Domänennamens  
 Wenn Sie diese Option auswählen, der Server nicht überwachen oder verwalten Sie Ihren Domänennamen, und es werden nicht benachrichtigt, wenn ein Konfigurationsproblem vorliegt. Sie können diese Option auch erwägen, wenn eine der folgenden Aussagen zutrifft:  
  
-   Für Ihr Land oder Ihre Region sind keine partneranbieter für Domänennamen aufgeführt.  
  
-   Ihre domänennamenerweiterung wird von den aufgeführten partnerdomänenanbietern nicht unterstützt.  
  
-   Sie haben eine vorhandene Domänenname stammt von einem domänennamenanbieter, der derzeit kein Partner ist, und nicht diesen Domänennamen auf einem Windows Server Essentials unterstützten-domänennamenanbieter übertragen möchten.  
  
-   Der Assistent wird die domänennamenerweiterung, die Sie verwenden möchten, nicht aufgeführt, aber die Erweiterung ist von einem domänennamenanbieter, der derzeit kein Partner ist verfügbar.  
  
 Wenn Sie Ihren Domänennamen manuell einrichten möchten, arbeiten Sie mit Ihrem Domain Name Service-Anbieter einen A-Eintrag für Ihre Domäne erstellen.  
  
##### <a name="to-create-an-a-record"></a>Um einen A-Eintrag erstellen  
  
1.  Legen Sie ein Hostname, z.B. Remote. Dies ist das domänennamenpräfix. Das domänennamenpräfix sowie Ihren Domänennamen wird die URL zum Öffnen der Anmeldeseite des Remotewebzugriffs definieren. beispielsweise **http://remote.contoso.com**.  
  
2.  Erstellen Sie in Ihrem Domain Name Service-Anbieter Konfiguration Dashboard (in der Regel auf der Webseite) den A-Eintrag für den Hostnamen, den Sie sich entschieden haben, klicken Sie in Schritt1. Stellen Sie sicher, dass die IP-Adresse, die Sie im A-Eintrag angeben der IP-Adresse des Routers (Seite mit Internetzugriff) die WAN-seitige ist. Weitere Informationen finden Sie in der Routerdokumentation, um die WAN-IP-Adresse zu suchen.  
  
3.  Es wird empfohlen, dass Sie Kontakt zu Ihr Internetdienstanbieter (ISP) um eine statische IP-Adresse für Ihr Netzwerk zu erwerben. Dadurch wird sichergestellt, dass die IP-Adresse nicht ändert und der DNS-Eintrag immer aktuell ist.  
  
     Wenn Sie nicht die Möglichkeit, eine statische IP-Adresse von Ihrem Internetdienstanbieter erhalten haben, sollten Sie der Domain Name System (DNS)-Protokolldienst für dynamische Updates vom Domain Name Service-Anbieter oder einem anderen Dienstanbieter erwerben. DNS-Protokoll für dynamische Updates ist ein Dienst, der die WAN-IP-Adresse für Ihr Netzwerk auf dem neuesten Stand bleiben, damit die IP-Adresse in Ihren Domänennamen aufgelöst werden kann, auch wenn sich die IP-Adresse ändert.  
  
4.  Importieren Sie ein vertrauenswürdiges Zertifikat, wenn Sie den Assistenten aufgefordert werden. Wenn Sie nicht über ein vertrauenswürdiges Zertifikat verfügen, können Sie eins von einem der im Assistenten aufgeführten unterstützten domänennamenanbieter oder einem vertrauenswürdigen Anbieter Ihrer Wahl erwerben. Weitere Informationen zu einem vertrauenswürdigen Zertifikat wenden Sie sich an Ihrem domänennamenanbieter.  
  
###  <a name="BKMK_Find"></a>Suchen von Domain Name Service-Anbieter  
  
##### <a name="to-find-the-domain-name-service-provider-for-your-domain-name"></a>Suchen Sie den Domain Name Service-Anbieter für Ihren Domänennamen  
  
1.  Öffnen Sie einen Webbrowser, und geben Sie dann **www.internic.com** in die Adressleiste, um zur Startseite von InterNIC zu gelangen.  
  
2.  Klicken Sie auf der Startseite von InterNIC, **Whois**.  
  
3.  In der **Whois** geben den Namen Ihrer Domäne (z.B. contoso.com).  
  
4.  Klicken Sie auf die **Domäne** aus, und klicken Sie dann auf **übermitteln**.  
  
5.  In den Suchergebnissen wird der Name des Domain Name Service-Anbieter aufgeführt, unter **Registrierungsstelle**.  
  
##  <a name="BKMK_4"></a>Anpassen von Web Access  
 Sie können Ihrer Website für Remotewebzugriff anpassen, indem Sie ein persönliches Logo oder Hintergrundbild hinzufügen. Sie können auch Links auf der Startseite hinzufügen, damit diese Informationen für alle Benutzer verfügbar ist. Weitere Informationen finden Sie unter den folgenden Themen:  
  
-   [Anpassen von Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeRWA)  
  
-   [Anpassen von Bildern für Hintergründe und Logos](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeImages)  
  
-   [Reparieren des Remotewebzugriffs](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_RepairRWA)  
  
###  <a name="BKMK_CustomizeRWA"></a>Anpassen von Web Access  
 Sie können Remote Web Access anpassen, indem Sie den Titel der Website ändern, ändern das Hintergrundbild und das Logo und Links zu anderen Websites auf der Startseite hinzufügen.  
  
##### <a name="to-customize-remote-web-access"></a>Anpassen des Remotewebzugriffs  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
3.  In der **websiteeinstellungen** auf **anpassen**.  
  
4.  Wenn Sie mit dem Anpassen des Remotewebzugriffs fertig sind, klicken Sie auf **OK**. Testen Sie Ihre Änderungen auf Remote Web Access.  
  
###  <a name="BKMK_CustomizeImages"></a>Anpassen von Bildern für Hintergründe und Logos  
 Dieser Abschnittenthält Informationen zu den Bildern, die Sie zum Anpassen des Remotewebzugriffs verwenden können.  
  
#### <a name="image-size"></a>Bildgröße  
 **Logos**  
  
 Es wird empfohlen, Logos zu verwenden, die 32 x 32 Pixel. Größere Bilder werden auf 32 x 32 verkleinert und kleinere Bilder werden gestreckt, 32 x 32, die das Bild verzerrt werden konnte.  
  
 **Hintergrundbilder**  
  
 Es gibt zwar keine größenbeschränkung für Hintergrundbilder für optimale Ergebnisse wird empfohlen, dass Sie Bilder verwenden, die CA. 800 x 500 Pixel. Das Hintergrundbild wird in der Mitte (vertikal und horizontal) der Anmeldeseite platziert. Damit können den Text auf der Anmeldeseite einfacher lesbar ist, sollte die Mitte des Hintergrundbildes helle Farbe haben.  
  
#### <a name="image-file-types"></a>Bilddateitypen  
 Die folgenden Bilddateitypen können verwendet werden, das standardmäßige Hintergrund und das Website-Logo zu ersetzen:  
  
-   Bitmap (*.bmp, \*.dib, \*.rle)  
  
-   GIF-Datei (*.gif)  
  
-   PNG (*.PNG)  
  
-   JPG (*.jpg)  
  
###  <a name="BKMK_RepairRWA"></a>Reparieren des Remotewebzugriffs  
 Der Standortreparatur-Assistenten können Sie die Erkennung und Behebung von Problemen mit Ihrem Router oder den Domänennamen. Es gibt zwei Möglichkeiten, um Probleme mit Remote Web Access zu ermitteln:  
  
-   Im Server-Einstellungen auf dem Dashboard auf der Registerkarte "Zugriff überall" wird ein Symbol mit einem roten X zusammen mit einer Beschreibung des Problems angezeigt.  
  
-   Eine Warnung in der Meldungsanzeige.  
  
> [!NOTE]
>  Der Standortreparatur-Assistent ist nicht verfügbar, bis Sie den Remotewebzugriff zu aktivieren. Informationen zum Aktivieren des Remotewebzugriffs finden Sie unter [Turn on Remote Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA).  
  
##### <a name="to-repair-remote-web-access"></a>So reparieren Sie Remote Web Access  
  
1.  Melden Sie sich bei dem Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
3.  Klicken Sie auf **Reparatur**. Die **Reparieren des Remotewebzugriffs** -Assistent wird gestartet.  
  
4.  Klicken Sie auf **Weiter**. Der Assistent analysiert den Remotewebzugriff, identifiziert das Problem und versucht anschließend, das Problem zu beheben.  
  
5.  Wenn Sie eine Warnung erhalten, wenn der Assistent abgeschlossen ist, klicken Sie auf **wiederholen** versuchen, das Problem erneut zu reparieren. Wenn Sie eine Warnung erhalten weiterhin, überprüfen Sie die Warnung auf Weitere Informationen zu dem Problem und Schrittezur Problembehandlung.  
  
##  <a name="BKMK_5"></a>Beheben von Web Access  
  
-   [Behandeln von Problemen Sie Remotewebzugriff-Verbindung](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [Problembehandlung bei der Firewall](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](../support/Troubleshoot-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Remotedesktop-Optionen](Remote-desktop-options.md)  
  
-   [Verwenden von Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
