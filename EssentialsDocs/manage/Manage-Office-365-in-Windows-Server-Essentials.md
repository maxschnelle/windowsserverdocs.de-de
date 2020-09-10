---
title: Verwalten von Microsoft 365 in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 71e8204c8b11f423871f890badffdfb96206feb8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623068"
---
# <a name="manage-microsoft-365-in-windows-server-essentials"></a>Verwalten von Microsoft 365 in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Ihren Windows Server Essentials-Server mit Microsoft 365 integrieren, können Sie Ihre Microsoft 365 Dienste und Online Konten zusammen mit Ihren lokalen Ressourcen über das Windows Server Essentials-Dashboard verwalten. In diesem Thema erfahren Sie, was Sie erreichen können, indem Sie Ihren Server in Microsoft 365 integrieren, wie Sie vorgehen und wie Sie die Microsoft 365 Integration verwalten und Probleme beheben.



> [!IMPORTANT]
>   Microsoft 365 Integration wird nur in einer Umgebung mit einem einzelnen Domänen Controller unterstützt. Außerdem muss der Assistent für die Microsoft 365 Integration auf einem Domänen Controller ausgeführt werden.

## <a name="in-this-topic"></a>In diesem Thema

-   [Warum sollte ich Microsoft 365 in meinen Server integrieren?](#BKMK_IntegrationOverview)

-   [Einrichten Microsoft 365 Integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)

-   [Verwalten der Microsoft 365 Integration](#BKMK_ManageIntegration)

-   [Problembehandlung Microsoft 365 Integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)

##  <a name="why-should-i-integrate-microsoft-365-with-my-server"></a><a name="BKMK_IntegrationOverview"></a> Warum sollte ich Microsoft 365 in meinen Server integrieren?
 Es gibt viele gute Gründe für die Integration von Microsoft 365 in den Windows Server Essentials-Server. Wenn Sie einige ihrer Ressourcen intern verwalten, aber Microsoft 365 für andere Dienste verwenden, können Sie Ihre Microsoft 365 Dienste und-Ressourcen zusammen mit Ihren lokalen Ressourcen über das Dashboard verwalten, statt an zwei Orten zu arbeiten.

- Verwalten Sie die Online Konten, die Ihren Benutzern Zugriff auf Microsoft 365 zusammen mit ihren Benutzerkonten gewährt:

  -   Erstellen Sie Microsoft Online Services-Konten für die Benutzer in einem einzigen Schritt, oder erstellen Sie Benutzerkonten auf dem Server für bereits vorhandene Onlinekonten. Sie können auch ein Onlinekonto zu einem neuen oder bereits vorhandenen Benutzerkonto hinzufügen.

       Wenn Sie die Online Konten über das Dashboard erstellen, melden sich Benutzer mit demselben Kennwort, das Sie auf dem Server verwenden, bei Microsoft 365 an. Wenn sie das Kennwort für dieses Benutzerkonto ändern, ändert sich auch das Online-Kennwort. Und Sie können sich sicher sein, dass die Kennwörter der Onlinekonten immer die Sicherheitsanforderungen erfüllen, die Sie für Ihre Benutzerkonten festlegen.

  -   Verwalten Sie Onlinekonten zusammen mit Benutzerkonten, während des gesamten Lebenszyklus der Benutzerkonten. Wenn Sie ein Benutzerkonto deaktivieren, wird auch das Onlinekonto deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt.

  -   Verwalten Sie auf einem Windows Server Essentials-Server auch Exchange Online-Verteiler Gruppen für e-Mails.

- Senden und empfangen Sie e-Mails von der Internet Domäne Ihrer Organisation (z. b. contoso.com), indem Sie eine benutzerdefinierte Internet Domäne mit Ihrem Microsoft 365-Abonnement verknüpfen.

- Verwalten Sie Ihr Abonnement, und Microsoft 365 Sie die Integration über das Dashboard.

- Wenn Ihr Abonnement SharePoint Online-Bibliotheken umfasst, können Sie Microsoft 365 Integration in einen Windows Server Essentials-Server folgende Aktionen ausführen:

  - Erstellen und verwalten Sie Ihre SharePoint Online-Bibliotheken über das Dashboard.

    > [!NOTE]
    >  Sie können auch die My Server 2012 R2-App verwenden, um mit Dokumenten in Ihren SharePoint Online-Bibliotheken auf Ihrem Laptop, mobilen Gerät oder Windows Phone zu arbeiten. Diese Funktion ist nur für Windows Server Essentials verfügbar. Weitere Informationen finden Sie unter [Verwenden der My Server-App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).

  - Ändern Sie die Berechtigungen für eine SharePoint Online-Team Website über das Dashboard, oder öffnen Sie die Team Website über das Dashboard, um andere Änderungen vorzunehmen.

    Weitere Informationen finden Sie unter [Verwalten von SharePoint Online](Manage-SharePoint-Online-in-Windows-Server-Essentials.md).

- Wenn Sie Exchange Online abonnieren, können Sie mit Microsoft 365 Integration in einen Windows Server Essentials-Server die mobilen Geräte verwalten, mit denen Ihre Benutzer eine Verbindung mit dem e-Mail-Server Ihres Unternehmens herstellen:

  -   Fordern Sie Kennwortschutz, wenn sich mobile Geräte mit dem E-Mail-Server des Unternehmens verbinden. Legen Sie eine minimale Kennwortlänge, die Anzahl der zulässigen fehlgeschlagenen Anmeldeversuche und die minimal erforderliche Zeit zwischen Anmeldeversuchen fest.

  -   Blockieren Sie ein mobiles Gerät, das eine Verbindung zu Exchange Online herstellen möchte, wenn Ihnen Sicherheitsprobleme mit dem Modell bekannt sind.

  -   Wenn ein mobiles Gerät verloren geht oder gestohlen wird, löschen Sie das Gerät, um sensible Daten zu löschen, wenn das Gerät das nächste Mal aktiviert wird.

- Microsoft 365 Integration bietet Ihnen neue Möglichkeiten zum Herstellen einer Verbindung mit Microsoft 365 Diensten und Ressourcen:

  -   Öffnen Sie Microsoft 365 Services aus dem Windows Server Essentials-launchpad. Weitere Informationen finden [Sie unter Schnellstarthandbuch to using Microsoft 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).

  -   Verwenden Sie die My Server 2012 R2-APP, um mit Dokumenten in Ihren SharePoint Online-Bibliotheken auf Ihrem Laptop, mobilen Gerät oder Windows Phone zu arbeiten. Weitere Informationen finden Sie unter [Verwenden der My Server-App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md). Diese Funktion ist nur in Windows Server Essentials verfügbar.

##  <a name="set-up-microsoft-365-integration"></a><a name="BKMK_Configure"></a> Einrichten Microsoft 365 Integration
 Sie können den Server jederzeit in Microsoft 365 integrieren, nachdem Sie die Server Installation fertiggestellt haben. Wenn Sie noch nicht über ein Microsoft 365-Abonnement verfügen, können Sie eines erwerben oder sich für ein kostenloses Testabonnement registrieren.

 Führen Sie die folgenden Aufgaben aus:

-   [Schritt 1: Überprüfen der Microsoft 365 Integrationsanforderungen](#BKMK_StepOne_VERIFY)

-   [Schritt 2: Integrieren des Servers mit Microsoft 365](#BKMK_StepTwo)

-   [Schritt 3: Verknüpfen des Internet Domänen Namens Ihres Unternehmens mit Microsoft 365 (optional)](#BKMK_StepThree)

###  <a name="step-1-verify-microsoft-365-integration-requirements"></a><a name="BKMK_StepOne_VERIFY"></a> Schritt 1: Überprüfen der Microsoft 365 Integrationsanforderungen
 Bevor Sie beginnen, stellen Sie sicher, dass der Server die folgenden Anforderungen erfüllt:

-   Der Server kann eines der folgenden Betriebssysteme aufweisen: Windows Server Essentials, Windows Server Essentials oder das Betriebssystem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials-Rolle.

-   Die Umgebung kann nur einen Domänen Controller haben, und Sie müssen Microsoft 365 Integration auf dem Domänen Controller durchführen.

-   Sie müssen den Server mit dem Internet verbinden können.

-   Sie sollten alle wichtigen und wichtigen Updates auf dem Server installieren, bevor Sie mit der Microsoft 365 Integration beginnen.

-   Wenn Sie die Internet Domäne Ihres Unternehmens in e-Mail-Adressen und in Ihren SharePoint Online-Ressourcen verwenden möchten, müssen Sie den Domänen Namen registrieren, damit Sie die Domäne während der Integration mit Microsoft 365 verknüpfen können. Weitere Informationen finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).

> [!NOTE]
>  Sie müssen Microsoft 365 im Voraus nicht abonnieren. Während der Microsoft 365 Integration können Sie ein Abonnement erwerben oder sich für eine kostenlose Testversion registrieren. Wenn Sie Pläne und Preise für Microsoft 365 betrachten möchten, [vergleichen Sie Microsoft 365 Pläne für Unternehmen](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text).

###  <a name="step-2-integrate-the-server-with-microsoft-365"></a><a name="BKMK_StepTwo"></a> Schritt 2: Integrieren des Servers mit Microsoft 365
 Führen Sie die folgenden Schritte auf dem Domänen Controller aus, um Ihren Windows Server Essentials-Server in Microsoft 365 zu integrieren.

> [!NOTE]
>  Das Verfahren ist identisch, unabhängig davon, ob Sie über Windows Server Essentials oder Windows Server Essentials verfügen, aber Sie beginnen von einem anderen Ort auf der Startseite. In Windows Server Essentials integrieren Sie den Server auf der Registerkarte " **Dienste** " in Microsoft 365 und andere Microsoft Online Services. In Windows Server Essentials wird Microsoft 365 Integration auf der Registerkarte " **e-Mail** " durchgeführt.

##### <a name="to-integrate-the-server-with-microsoft-365"></a>So integrieren Sie den Server mit Microsoft 365

1. Melden Sie sich auf dem Server als Administrator an, und öffnen Sie das Windows Server Essentials-Dashboard.

2. Klicken Sie auf der **Start** Seite auf **Dienste** (in Windows Server Essentials, klicken Sie auf **e-Mail**), klicken Sie auf **in Microsoft 365 integrieren**, und klicken Sie dann auf **Microsoft 365 Integration einrichten**.

    Der Assistent zum Integrieren in Microsoft 365 wird angezeigt.

3. Führen Sie auf der Seite **Erste Schritte** eine der folgenden Aktionen aus:

   -   Wenn Sie nicht über ein Abonnement für Microsoft 365 verfügen, klicken Sie auf **weiter**, und befolgen Sie die Anweisungen, um Microsoft 365 zu abonnieren oder sich für ein Testabonnement anzumelden.

        Sie müssen sich bei Microsoft 365 anmelden, bevor Sie zum Assistenten zurückkehren. Sie müssen jedoch keine der Aufgaben im Abschnitt " **Starten Sie hier** " im Microsoft 365-Portal ausführen.

   -   Wenn Sie bereits über ein Abonnement für Microsoft 365 verfügen, das Sie in den Server integrieren möchten, wählen Sie **Ich habe bereits ein Abonnement für Microsoft 365 aus**, und klicken Sie dann auf **weiter**.

4. Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

   Nachdem der Assistent erfolgreich abgeschlossen wurde, bemerken Sie die folgenden Änderungen am Dashboard:

-   Es gibt eine neue **Microsoft 365** Seite, die zum Verwalten der Integration und Ihres Microsoft 365 Abonnements verwendet wird.

-   Auf der Seite **Benutzer** sehen Sie eine Registerkarte **Online Konten** , auf der Sie die Microsoft Online Services-Konten erstellen und verwalten können, mit denen Ihre Benutzer Zugriff auf Microsoft 365 erhalten. Wenn Sie Exchange Online verwenden und über einen Windows Server Essentials-Server verfügen, wird Ihnen auch eine Registerkarte **Verteiler Gruppen** angezeigt.

-   Die Seite **Speicher** auf einem Windows Server Essentials-Server verfügt über eine Registerkarte **SharePoint-Bibliotheken** zum Verwalten von SharePoint Online-Bibliotheken und zum Ändern von Berechtigungen für Ihre Team Websites. Jeder Geschäftsplan für Microsoft 365 umfasst diese grundlegenden SharePoint Online-Features.

###  <a name="step-3-link-your-organizations-internet-domain-name-to-microsoft-365-optional"></a><a name="BKMK_StepThree"></a> Schritt 3: Verknüpfen des Internet Domänen Namens Ihres Unternehmens mit Microsoft 365 (optional)
 Wenn Sie Ihre eigene Internet Domäne in e-Mail-Nachrichten an Ihre Organisation und die URLs für Ihre SharePoint Online-Ressourcen verwenden möchten, können Sie eine benutzerdefinierte Domäne mit Ihrem Microsoft 365-Abonnement verknüpfen. Wenn Sie Ihren Windows Server Essentials-Server in Microsoft 365 integrieren, können Sie dazu das Dashboard verwenden.

 Es ist am einfachsten, dies zu tun, bevor Sie Online Konten für Ihre Benutzer erstellen, damit Sie die Domäne verwenden können, wenn Sie die Online Konten per Massen Vorgang erstellen.

 Wenn Sie sich für Microsoft 365 registrieren, erhalten Sie einen Domänen Namen, z *. b*. "onmicrosoft.com". Wenn Sie stattdessen einen anderen Domänen Namen verwenden möchten, sagen Sie einfach contoso.com? Sie können dies tun. Sie müssen einen Domänen Namen erwerben, wenn Sie nicht bereits einen besitzen, und einige der DNS-Einträge ändern.

 Das Einrichten einer benutzerdefinierten Domäne für die Verwendung mit Microsoft 365 umfasst vier Aufgaben:

1. **Erwerben eines Domänennamens** Das bedeutet, registrieren Sie ihn über eine Domänenregistrierungsstelle oder einen DNS-Hostinganbieter.

   -   Wählen Sie einen Domänen Namen aus, der mit Microsoft 365 funktioniert. Sie können einen Domänen Namen auf zweiter Ebene verwenden, z. b. buycontoso.com?, aber keinen Domänen Namen auf der dritten Ebene, z. b. Marketing.contoso.com. Weitere Informationen zum Auswählen einer Domäne für die Verwendung in Microsoft 365 finden Sie unter [Domänen](/office365/servicedescriptions/office-365-platform-service-description/domains).

   -   Erwerben Sie es von einer Domänen Registrierungsstelle, die die von Microsoft 365 benötigten DNS-Einträge (Domain Nameserver) zulässt. Informationen dazu, welche Domänenregistrierungsstellen die erforderlichen DNS-Einträge ermöglichen, finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660). Wenn Sie Ihre Domäne bereits bei einer anderen Registrierungsstelle registriert haben, machen Sie sich keine Sorgen. Sie können die Domäne in eine andere Registrierungsstelle übertragen, wenn Sie die Domäne mit Microsoft 365 verknüpfen.

2. **Konfigurieren Sie DNS-Einträge, die Microsoft 365 Services den Domänen Namen verwenden können.** Die einfachste Möglichkeit besteht darin, den Assistenten die DNS-Einträge für Sie konfigurieren zu lassen, wenn Sie die Domäne in Schritt 3 mit Ihrem Microsoft 365-Abonnement verknüpfen. Wenn Sie dies stattdessen selbst tun möchten, finden Sie weitere Informationen unter [Manuelles Konfigurieren von DNS](#BKMK_ManuallyConfigureDNS)-Einträgen für die Microsoft 365-Integration.

3. **Verknüpfen Sie Ihre benutzerdefinierte Internet Domäne mit Ihrem Microsoft 365-Abonnement.** Verwenden Sie die Aktion **Domäne mit Microsoft 365 verknüpfen** .

4. **Vergewissern Sie sich, dass die Microsoft 365-Dienste den neuen Domänen Namen verwenden.**

   Wenn Sie die Schritte 1 und 2 ausgeführt haben, bevor Sie die Aufgabe **Domäne mit Microsoft 365 verknüpfen** verwenden, kann der Assistent den Domänen Namen mit Microsoft 365 verknüpfen. Alternativ kann Sie der Assistent bei Teilen von oder den gesamten Schritten 1 und 2 unterstützen.

##### <a name="to-link-your-organizations-internet-domain-to-microsoft-365"></a>So verknüpfen Sie die Internet Domäne Ihrer Organisation mit Microsoft 365

1.  Öffnen Sie auf dem Dashboard die Seite **Microsoft 365** , und klicken Sie auf **Domäne mit Microsoft 365 verknüpfen**.

2.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

     Der Assistent kann Ihnen bei einigen oder allen Schritten zum Registrieren, konfigurieren und Verknüpfen eines neuen oder bereits vorhandenen Internet Domänen Namens für die Verwendung in Microsoft 365 helfen.

     Klicken Sie auf den Hilfelink auf der Seite des Assistenten, um die Informationen abzurufen, die Sie benötigen, um eine Aufgabe auszuführen. Eine Prozessübersicht und Anforderungen finden Sie im Abschnitt "Einrichten eines Domänen namens" unter [Verwalten von Remote Webzugriff in Windows Server Essentials](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) .

    > [!NOTE]
    >  Um den Assistenten zu verwenden, um einen neuen Domänennamen zu registrieren, müssen Sie einen Domain Name Service-Anbieter verwenden, der Partner von Microsoft ist, um eine nahtlose Integration mit dem Assistenten bereitstellen zu können. Eine Domänennamen-Registrierungsstelle finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).

3.  Wenn der Assistent erkennt, dass der Domänen Name nicht vom Server verwaltet wird, müssen Sie die erforderlichen DNS-Einträge manuell konfigurieren, um die Konfiguration abzuschließen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Manuelles Konfigurieren von DNS](#BKMK_ManuallyConfigureDNS)-Einträgen für die Microsoft 365-Integration.

4.  Vergewissern Sie sich, dass die Domäne in Microsoft 365 verwendet wird.

     Nachdem der Assistent abgeschlossen ist, wird ein wenig gewartet, während die Domänen Namen-Registrierungsstelle die DNS-Einträge überprüft. Dies geschieht automatisch. Sie müssen nichts tun. Es dauert jedoch im Allgemeinen ungefähr eine Stunde, aber manchmal etwas länger. Nach Abschluss der Domänen Überprüfung wird auf der **Microsoft 365** Seite die Domäne Ihrer Organisation aufgelistet.

####  <a name="how-to-manually-configure-dns-records-for-microsoft-365-integration"></a><a name="BKMK_ManuallyConfigureDNS"></a> Manuelles Konfigurieren von DNS-Einträgen für Microsoft 365 Integration
 Wenn der Assistent zum Verknüpfen ihrer Domäne mit Microsoft 365 erkennt, dass der Domänen Name nicht vom Server verwaltet wird, müssen Sie zum Durchführen der Konfiguration die erforderlichen DNS-Einträge (Domain Nameserver) manuell konfigurieren. In diesem Fall finden Sie eine Liste der DNS-Einträge, die Sie konfigurieren müssen, unter **% username% \ NewDNSRecords_ (n). txt**, wobei *(n)* eine zufällige Zahl ist.

 Die folgende Tabelle beschreibt die DNS-Einträge, die Sie hinzufügen müssen. Eintragsmethoden können bei unterschiedlichen Domänennamen-Registrierungsstellen variieren. Wenn Sie Fragen haben, wenden Sie sich an die Domänennamen-Registrierungsstelle.

### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-microsoft-365"></a>Erforderliche DNS-Einträge für die Verknüpfung eines benutzerdefinierten Internet Domänen Namens mit Microsoft 365

|Dienst|Erforderliche DNS-Einträge|Zweck|
|-------------|--------------------------|-------------|
|(Mehrere Dienste)|MX| Microsoft 365 verwendet diesen Datensatz, um zu überprüfen, ob Sie einen bestimmten Domänen Namen besitzen. Dieser MX-Eintrag beeinträchtigt das Routing von E-Mail-Nachrichten nicht.|
|Exchange Online|MX|Ermöglicht Routing von E-Mail-Nachrichten. **Wichtig:**  Wenn Sie e-Mail migrieren, weisen Sie dem neuen MX-Eintrag keine Einstellung von NULL (**0**) zu. Stellen Sie sicher, dass der Wert für den Eintrag größer ist, als der Wert, der dem aktuellen MX-Eintrag zugewiesen ist. Wenn die e-Mail-Migration abgeschlossen ist und Sie bereit sind, den e-Mail-Server in Microsoft 365 zu ändern, muss die Domänen Namen-Registrierungsstelle den Wert des neuen MX-Einsatzes zurücksetzen.|
|Exchange Online|Alias (CNAME)|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen Exchange Online und dem Outlook-Client auf deren Desktops oder einem mobilen E-Mail-Client zu unterstützen. **Hinweis:**  Wenn Sie den Zugriff auf Outlook Webzugriff bevorzugen, indem Sie den eigenen Domänen Namen Ihrer Organisation verwenden (z. b. http://mail.contoso.com) anstelle der Standard-URL ( https://outlook.com/owa/office365.com) ), können Sie den Alias Eintrag (CNAME) wie folgt konfigurieren: **Type = CNAME, TTL = 01:00:00, Hostname = Mail, Address = Mail. Office 365. com**|
|Exchange Online|TXT|Gibt an, dass Outlook.com, die von den Microsoft 365-e-Mail-Servern verwendete Domäne, autorisiert ist, im Auftrag Ihrer Domäne eine e-Mail zu senden. Erstellen Sie diesen Eintrag, um zu verhindern, dass Ihre ausgehenden E-Mail-Nachrichten als Spam gekennzeichnet werden.|
|Lync Online|SRV|Hilft, den Verbund mit anderen Instant Messaging-Diensten, wie z. B. Windows Live oder Yahoo! zu ermöglichen.|
|Lync Online|SRV|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen dem Lync-Desktopclient und Microsoft Lync Online zu unterstützen.|

> [!IMPORTANT]
>  Versuchen Sie nach Abschluss der Domänen Überprüfung nicht, Änderungen an den DNS-Einträgen aus dem Microsoft 365-Portal hinzuzufügen oder weitere Änderungen vorzunehmen.

###  <a name="next-step"></a><a name="BKMK_StepFour_ACCOUNTS"></a> Nächster Schritt

-   Erstellen Sie Microsoft Online Services-Konten für die Benutzer.

     Um Microsoft 365 Dienste verwenden zu können, müssen die Benutzer über ein Microsoft Online Services-Konto verfügen, das Ihrem Netzwerk Benutzerkonto zugeordnet ist. Dies ist mit dem Dashboard ganz einfach. Wenn Sie ein neues Microsoft 365-Abonnement verwenden, können Sie Online Konten für vorhandene Benutzerkonten per Massen Vorgang erstellen. Wenn Sie einen neuen Server mit einem Microsoft 365 Abonnement integrieren, das Sie bereits verwenden, können Sie Benutzerkonten aus Ihren vorhandenen Online Konten importieren. Informationen zu Verfahren finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

> [!NOTE]
>  Auf dem Dashboard in Windows Server Essentials werden Microsoft Online Services-Konten als Microsoft 365 Konten bezeichnet. Die Konten sind identisch, nur die Terminologie ist anders.

##  <a name="manage-microsoft-365-integration"></a><a name="BKMK_ManageIntegration"></a> Verwalten der Microsoft 365 Integration
 Nachdem Sie den Server in Microsoft 365 integriert haben, werden auf der **Microsoft 365** Seite des Dashboards Informationen zu Ihrem Microsoft 365-Abonnement angezeigt, und diese Aufgaben werden zur Verfügung gestellt:

-   [Verwalten Ihres Microsoft 365 Abonnements](#BKMK_ManageO365) Ändern Sie das Administrator Konto, das Sie zum Verwalten des Abonnements verwenden. Öffnen Sie das Microsoft 365 Admin-Dashboard, um Ihr Abonnement zu verwalten.

-   [Verknüpfen Sie die Internet Domäne Ihres Unternehmens mit Microsoft 365](#BKMK_StepThree) ? Wenn Sie in der Lage sein möchten, e-Mail-Nachrichten an Ihre eigene Domäne zu senden und zu empfangen, können Sie die Domäne mit Microsoft 365 verknüpfen. (Zuvor erläutert in [Schritt 3: Verknüpfen Sie die Domäne Ihrer Organisation mit Microsoft 365](#BKMK_StepThree).)

-   [Microsoft 365 Integration deaktivieren](#BKMK_Disable) ? Wenn Sie Ihre Microsoft 365-Dienste,-Abonnements und-Online Konten nicht über das Dashboard verwalten möchten, können Sie Microsoft 365 Integration deaktivieren. Die Dienste sind weiterhin im Microsoft 365-Portal verfügbar.

###  <a name="manage-your-microsoft-365-subscription"></a><a name="BKMK_ManageO365"></a> Verwalten Ihres Microsoft 365 Abonnements
 Wenn Sie Änderungen an Ihrem Microsoft 365-Abonnement vornehmen müssen, während Sie auf dem Server arbeiten, können Sie das Abonnement in Microsoft 365 auf der **Microsoft 365** Seite des Dashboards öffnen. Sie können auch das Administrator Konto ändern, das der Server verwendet, um Änderungen an Microsoft 365-Diensten vorzunehmen.

##### <a name="to-open-your-subscription-on-the-microsoft-365-admin-dashboard"></a>So öffnen Sie Ihr Abonnement im Microsoft 365 Admin-Dashboard

1.  Öffnen Sie im Windows Server Essentials-Dashboard die Seite **Microsoft 365** .

2.  Klicken Sie unter **Konfigurationsaufgaben**auf **Microsoft 365 verwalten**.

3.  Melden Sie sich bei Microsoft 365 mit dem Microsoft-Onlinekonto an, das Sie zum Verwalten Ihres Abonnements verwenden.

     Das Microsoft 365 Admin-Dashboard wird geöffnet.

##### <a name="to-change-the-microsoft-365-administrator-account"></a>So ändern Sie das Microsoft 365 Administrator Konto

1.  Klicken Sie auf dem Dashboard auf **Microsoft 365**.

2.  Klicken Sie unter **Konfigurationsaufgaben**auf **Microsoft 365 Administrator Konto ändern**. Der Assistent zum Ändern von Administratorenkonten wird angezeigt. (In Windows Server Essentials heißt der Assistent Microsoft 365 Administrator Konto einrichten.)

3.  Geben Sie die Anmelde Informationen für das Konto ein, das Sie zum Herstellen einer Verbindung mit Ihrem Microsoft 365-Abonnement verwenden möchten, und klicken Sie dann auf **weiter**.

4.  Klicken Sie auf **Schließen**. Das Dashboard wird neu gestartet.

###  <a name="disable-microsoft-365-integration"></a><a name="BKMK_Disable"></a> Deaktivieren der Microsoft 365 Integration
 Wenn Sie die Microsoft 365 Dienste und Online Konten nicht über das Dashboard verwalten möchten, können Sie Microsoft 365 Integration deaktivieren. Ihr Microsoft 365-Abonnement bleibt aktiv, und alle Konfigurationsänderungen, die Sie aus dem Dashboard vorgenommen haben, bleiben in Kraft. Beispielsweise erhalten Sie eine e-Mail, die an einen Domänen Namen gerichtet ist, den Sie mit Ihrem Microsoft 365-Abonnement verknüpft haben. Sie verlieren keine e-Mails, und die von Ihnen für mobile Geräte festgelegten Steuerelemente werden weiterhin in Exchange Online verwendet.

 In Zukunft verwalten Sie Ihre Microsoft 365-Abonnements,-Dienste und-Ressourcen in Microsoft 365, und Ihre Benutzer müssen die Kenn Wörter für Ihre Online Konten in Microsoft 365 verwalten. Die Kenn Wort Synchronisierung erfolgt nicht mehr, und das Deaktivieren oder Entfernen eines Benutzerkontos hat keine Auswirkung auf das Onlinekonto des Benutzers.

 Da die Microsoft 365-Integrationssoftware auf dem lokalen Server installiert ist, können Sie die Funktion deaktivieren, auch wenn der Integrations Dienst keine Verbindung mit Microsoft 365 herstellen kann.

##### <a name="to-disable-microsoft-365-integration-with-the-server"></a>So deaktivieren Sie die Microsoft 365 Integration mit dem Server

1.  Klicken Sie auf dem Dashboard auf **Microsoft 365**.

2.  Klicken Sie auf **Microsoft 365 Integration deaktivieren**. Der Assistent zum Deaktivieren von Microsoft 365 wird angezeigt.

3.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

> [!NOTE]
>  Um Microsoft 365 Integration erneut zu aktivieren, verwenden Sie die Aufgabe in **Microsoft 365 integrieren** auf der Registerkarte **Dienst** auf der **Start** Seite des Dashboards. Anweisungen hierzu finden Sie weiter oben in diesem Thema unter [Schritt 2: integrieren Ihres Windows Server Essentials-Servers mit Microsoft 365](#BKMK_StepTwo).

##  <a name="troubleshoot-microsoft-365-integration"></a><a name="BKMK_Troubleshoot"></a> Problembehandlung Microsoft 365 Integration
 Dieser Abschnitt enthält Informationen, die Ihnen bei der Behebung allgemeiner Probleme helfen, die möglicherweise auftreten, wenn Sie die Microsoft 365 Integrations Features in Windows Server Essentials verwenden.

###  <a name="some-microsoft-online-services-accounts-were-not-created"></a><a name="BKMK_AcctsNotCreated"></a> Einige Microsoft Online Services-Konten wurden nicht erstellt.
 **Beschreibung**

 Der Versuch, ein oder mehrere Microsoft Online Services-Konten über das Dashboard zu erstellen, war nicht erfolgreich.

 **Lösung**

1.  Klicken Sie auf die Abschlussseite des Assistenten, um eine Ergebnisdatei zu öffnen, die ausführliche Informationen zu jeder Anforderung zum Erstellen eines Kontos enthält, die nicht erfolgreich abgeschlossen wurde. Beispielsweise kann ein Ergebnis Ihnen aufzeigen, dass ein Microsoft Online Services-Konto mit dem Namen eines angeforderten Kontos bereits vorhanden ist.

2.  Führen Sie die empfohlenen Aktionen aus, um jeden Fehler zu beheben.

3.  Wenn dieses Problem weiterhin besteht, starten Sie den Server neu, und versuchen Sie, die Onlinekonten erneut zu erstellen.

###  <a name="there-was-a-problem-uninstalling-microsoft-365-integration"></a><a name="BKMK_ProblemUninstalling"></a> Beim deinstallieren Microsoft 365 Integration ist ein Problem aufgetreten.
 **Beschreibung**

 Unbekannter Fehler beim Versuch, Microsoft 365 Integration zu deaktivieren.

 **Lösung**

1.  Stellen Sie sicher, dass der Computer mit dem Internet verbunden ist, und versuchen Sie es erneut.

2.  Wenn der Fehler erneut auftritt, starten Sie den Server neu, und versuchen Sie es erneut.

## <a name="additional-references"></a>Weitere Verweise

-   [Übersicht über die Dienst Integration für Windows Server Essentials-Teil 1](/archive/blogs/sbs/services-integration-overview-for-windows-server-2012-r2-essentials-part-1)

-   [Übersicht über die Dienst Integration für Windows Server Essentials-Teil 2](/archive/blogs/sbs/services-integration-overview-for-windows-server-2012-r2-essentials-part-2)

-   [Schnellstarthandbuch mit Microsoft 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)

-   [Verwalten von Microsoft Online Services](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)