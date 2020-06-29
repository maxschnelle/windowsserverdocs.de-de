---
title: Verwalten von Office 365 in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: e21f8b38c126f699fda8245ab620ce5cd210fa11
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470675"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Verwalten von Office 365 in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Ihren Windows Server Essentials-Server in Microsoft Office 365 integrieren, können Sie Ihre Office 365-Dienste und Online Konten zusammen mit Ihren lokalen Ressourcen über das Windows Server Essentials-Dashboard verwalten. In diesem Thema erfahren Sie, was Sie erreichen können, indem Sie Ihren Server in Office 365 integrieren, wie Sie vorgehen und wie Sie die Verwaltung und Problembehandlung bei der Integration von Office 365 durchführen.



> [!IMPORTANT]
>   Die Integration von Office 365 wird nur in einer Umgebung mit einzelnem Domänencontroller unterstützt. Außerdem muss der Assistent zum Integrieren von Office 365 auf einem Domänen Controller ausgeführt werden.

## <a name="in-this-topic"></a>In diesem Thema

-   [Warum sollte ich Office 365 in den Server integrieren?](#BKMK_IntegrationOverview)

-   [Einrichten der Integration von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)

-   [Verwalten der Integration von Office 365](#BKMK_ManageIntegration)

-   [Problembehandlung bei der Integration von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)

##  <a name="why-should-i-integrate-office-365-with-my-server"></a><a name="BKMK_IntegrationOverview"></a>Warum sollte ich Office 365 in meinen Server integrieren?
 Es gibt viele gute Gründe für die Integration von Office 365 in Ihren Windows Server Essentials-Server. Wenn Sie einige ihrer Ressourcen intern verwalten, aber Office 365 für andere Dienste verwenden, können Sie Ihre Office 365-Dienste und-Ressourcen zusammen mit Ihren lokalen Ressourcen über das Dashboard verwalten, statt an zwei Orten zu arbeiten.

- Verwalten Sie die Online Konten, mit denen Ihre Benutzer zusammen mit ihren Benutzerkonten Zugriff auf Office 365 erhalten:

  -   Erstellen Sie Microsoft Online Services-Konten für die Benutzer in einem einzigen Schritt, oder erstellen Sie Benutzerkonten auf dem Server für bereits vorhandene Onlinekonten. Sie können auch ein Onlinekonto zu einem neuen oder bereits vorhandenen Benutzerkonto hinzufügen.

       Wenn Sie die Online Konten über das Dashboard erstellen, melden sich Benutzer mit dem gleichen Kennwort, das Sie auf dem Server verwenden, bei Office 365 an. Wenn sie das Kennwort für dieses Benutzerkonto ändern, ändert sich auch das Online-Kennwort. Und Sie können sich sicher sein, dass die Kennwörter der Onlinekonten immer die Sicherheitsanforderungen erfüllen, die Sie für Ihre Benutzerkonten festlegen.

  -   Verwalten Sie Onlinekonten zusammen mit Benutzerkonten, während des gesamten Lebenszyklus der Benutzerkonten. Wenn Sie ein Benutzerkonto deaktivieren, wird auch das Onlinekonto deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt.

  -   Verwalten Sie auf einem Windows Server Essentials-Server auch Exchange Online-Verteiler Gruppen für e-Mails.

- Senden und empfangen Sie e-Mails von der Internet Domäne Ihrer Organisation (z. b. contoso.com), indem Sie eine benutzerdefinierte Internet Domäne mit Ihrem Office 365-Abonnement verknüpfen.

- Verwalten Sie Ihr Abonnement und die Office 365-Integration über das Dashboard.

- Wenn Ihr Abonnement SharePoint Online-Bibliotheken umfasst, können Sie bei der Integration von Office 365 in einen Windows Server Essentials-Server folgende Aktionen ausführen:

  - Erstellen und verwalten Sie Ihre SharePoint Online-Bibliotheken über das Dashboard.

    > [!NOTE]
    >  Sie können auch die My Server 2012 R2-App verwenden, um mit Dokumenten in Ihren SharePoint Online-Bibliotheken auf Ihrem Laptop, mobilen Gerät oder Windows Phone zu arbeiten. Diese Funktion ist nur für Windows Server Essentials verfügbar. Weitere Informationen finden Sie unter [Verwenden der My Server-App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).

  - Ändern Sie die Berechtigungen für eine SharePoint Online-Team Website über das Dashboard, oder öffnen Sie die Team Website über das Dashboard, um andere Änderungen vorzunehmen.

    Weitere Informationen finden Sie unter [Verwalten von SharePoint Online](Manage-SharePoint-Online-in-Windows-Server-Essentials.md).

- Wenn Sie Exchange Online abonnieren, können Sie mit der Office 365-Integration in einen Windows Server Essentials-Server die mobilen Geräte verwalten, mit denen Ihre Benutzer eine Verbindung mit dem e-Mail-Server Ihres Unternehmens herstellen:

  -   Fordern Sie Kennwortschutz, wenn sich mobile Geräte mit dem E-Mail-Server des Unternehmens verbinden. Legen Sie eine minimale Kennwortlänge, die Anzahl der zulässigen fehlgeschlagenen Anmeldeversuche und die minimal erforderliche Zeit zwischen Anmeldeversuchen fest.

  -   Blockieren Sie ein mobiles Gerät, das eine Verbindung zu Exchange Online herstellen möchte, wenn Ihnen Sicherheitsprobleme mit dem Modell bekannt sind.

  -   Wenn ein mobiles Gerät verloren geht oder gestohlen wird, löschen Sie das Gerät, um sensible Daten zu löschen, wenn das Gerät das nächste Mal aktiviert wird.

- Die Integration von Office 365 bietet Ihnen neue Möglichkeiten zum Herstellen einer Verbindung mit Office 365-Diensten und-Ressourcen:

  -   Öffnen Sie Office 365-Dienste über das Windows Server Essentials-launchpad. Weitere Informationen finden [Sie unter Schnellstarthandbuch to using Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).

  -   Verwenden Sie die My Server 2012 R2-APP, um mit Dokumenten in Ihren SharePoint Online-Bibliotheken auf Ihrem Laptop, mobilen Gerät oder Windows Phone zu arbeiten. Weitere Informationen finden Sie unter [Verwenden der My Server-App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md). Diese Funktion ist nur in Windows Server Essentials verfügbar.

##  <a name="set-up-office-365-integration"></a><a name="BKMK_Configure"></a>Einrichten der Integration von Office 365
 Sie können den Server jederzeit nach Abschluss der Server Installation mit Office 365 integrieren. Wenn Sie nicht bereits über ein Office 365-Abonnement verfügen, können Sie eines erwerben oder sich für ein kostenloses Testabonnement registrieren.

 Führen Sie die folgenden Aufgaben aus:

-   [Schritt 1: Überprüfen der Integrationsvoraussetzungen für Office 365](#BKMK_StepOne_VERIFY)

-   [Schritt 2: Integrieren des Servers mit Microsoft Office 365](#BKMK_StepTwo)

-   [Schritt 3: Verknüpfen des Internet Domänen Namens Ihres Unternehmens mit Office 365 (optional)](#BKMK_StepThree)

###  <a name="step-1-verify-office-365-integration-requirements"></a><a name="BKMK_StepOne_VERIFY"></a>Schritt 1: Überprüfen der Integrationsanforderungen für Office 365
 Bevor Sie beginnen, stellen Sie sicher, dass der Server die folgenden Anforderungen erfüllt:

-   Der Server kann eines der folgenden Betriebssysteme aufweisen: Windows Server Essentials, Windows Server Essentials oder das Betriebssystem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials-Rolle.

-   Die Umgebung kann nur einen Domänen Controller haben, und Sie müssen die Office 365-Integration auf dem Domänen Controller durchführen.

-   Sie müssen den Server mit dem Internet verbinden können.

-   Vor dem Starten der Integration von Office 365 sollten Sie alle wichtigen und wichtigen Updates auf dem Server installieren.

-   Wenn Sie die Internet Domäne Ihres Unternehmens in e-Mail-Adressen und in Ihren SharePoint Online-Ressourcen verwenden möchten, müssen Sie den Domänen Namen registrieren, damit Sie die Domäne während der Integration mit Office 365 verknüpfen können. Weitere Informationen finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).

> [!NOTE]
>  Sie müssen Office 365 nicht vorab abonnieren. Während der Integration von Office 365 können Sie ein Abonnement erwerben oder sich für eine kostenlose Testversion registrieren. Wenn Sie Pläne und Preise für Office 365 ansehen möchten, [vergleichen Sie Office 365-Pläne für Unternehmen](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text).

###  <a name="step-2-integrate-the-server-with-microsoft-office-365"></a><a name="BKMK_StepTwo"></a>Schritt 2: Integrieren des Servers in Microsoft Office 365
 Führen Sie das folgende Verfahren auf dem Domänen Controller aus, um Ihren Windows Server Essentials-Server in Office 365 zu integrieren.

> [!NOTE]
>  Das Verfahren ist identisch, unabhängig davon, ob Sie über Windows Server Essentials oder Windows Server Essentials verfügen, aber Sie beginnen von einem anderen Ort auf der Startseite. In Windows Server Essentials integrieren Sie den Server in Office 365 und andere Microsoft Online Services auf der Registerkarte " **Dienste** ". In Windows Server Essentials wird die Integration von Office 365 auf der Registerkarte " **e-Mail** " durchgeführt.

##### <a name="to-integrate-the-server-with-office-365"></a>So integrieren Sie den Server mit Office 365

1. Melden Sie sich auf dem Server als Administrator an, und öffnen Sie das Windows Server Essentials-Dashboard.

2. Klicken Sie auf der **Start** Seite auf **Dienste** (in Windows Server Essentials, klicken Sie auf e-Mail), klicken Sie auf **in Microsoft Office 365 integrieren**, und klicken Sie dann auf **Microsoft Office 365-Integration einrichten**. **Email**

    Der Assistent für die Integration in Microsoft Office 365 wird angezeigt.

3. Führen Sie auf der Seite **Erste Schritte** eine der folgenden Aktionen aus:

   -   Wenn Sie nicht über ein Abonnement für Office 365 verfügen, klicken Sie auf **weiter**, und befolgen Sie die Anweisungen, um Office 365 zu abonnieren oder sich für ein Testabonnement anzumelden.

        Sie müssen sich bei Office 365 anmelden, bevor Sie zum Assistenten zurückkehren. Sie müssen jedoch keine der Aufgaben im Abschnitt " **Starten Sie hier** " des Office 365-Portals ausführen.

   -   Wenn Sie bereits über ein Abonnement für Office 365 verfügen, das Sie in den Server integrieren möchten, wählen Sie **Ich habe bereits ein Abonnement für Office 365 aus**, und klicken Sie dann auf **weiter**.

4. Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

   Nachdem der Assistent erfolgreich abgeschlossen wurde, bemerken Sie die folgenden Änderungen am Dashboard:

-   Es gibt eine neue **Office 365** -Seite, die zum Verwalten der Integration und Ihres Office 365-Abonnements verwendet wird.

-   Auf der Seite **Benutzer** sehen Sie eine Registerkarte **Online Konten** , auf der Sie die Microsoft Online Services-Konten erstellen und verwalten können, mit denen Ihre Benutzer Zugriff auf Office 365 erhalten. Wenn Sie Exchange Online verwenden und über einen Windows Server Essentials-Server verfügen, wird Ihnen auch eine Registerkarte **Verteiler Gruppen** angezeigt.

-   Die Seite **Speicher** auf einem Windows Server Essentials-Server verfügt über eine Registerkarte **SharePoint-Bibliotheken** zum Verwalten von SharePoint Online-Bibliotheken und zum Ändern von Berechtigungen für Ihre Team Websites. Jeder Geschäftsplan für Office 365 umfasst diese grundlegenden SharePoint Online-Features.

###  <a name="step-3-link-your-organizations-internet-domain-name-to-office-365-optional"></a><a name="BKMK_StepThree"></a>Schritt 3: Verknüpfen des Internet Domänen Namens Ihres Unternehmens mit Office 365 (optional)
 Wenn Sie Ihre eigene Internet Domäne in e-Mail-Nachrichten an Ihre Organisation und die URLs für Ihre SharePoint Online-Ressourcen verwenden möchten, können Sie eine benutzerdefinierte Domäne mit Ihrem Office 365-Abonnement verknüpfen. Wenn Sie Ihren Windows Server Essentials-Server in Office 365 integrieren, können Sie dazu das Dashboard verwenden.

 Es ist am einfachsten, dies zu tun, bevor Sie Online Konten für Ihre Benutzer erstellen, damit Sie die Domäne verwenden können, wenn Sie die Online Konten per Massen Vorgang erstellen.

 Sie erhalten einen Domänen Namen, wenn Sie sich für Office 365 registrieren? z *. b*. "onmicrosoft.com". Wenn Sie stattdessen einen anderen Domänen Namen verwenden möchten, sagen Sie einfach contoso.com? Sie können dies tun. Sie müssen einen Domänen Namen erwerben, wenn Sie nicht bereits einen besitzen, und einige der DNS-Einträge ändern.

 Das Einrichten einer benutzerdefinierten Domäne für die Verwendung mit Office 365 umfasst vier Aufgaben:

1. **Erwerben eines Domänennamens** Das bedeutet, registrieren Sie ihn über eine Domänenregistrierungsstelle oder einen DNS-Hostinganbieter.

   -   Wählen Sie einen Domänen Namen aus, der mit Office 365 funktioniert. Sie können einen Domänen Namen auf zweiter Ebene verwenden, z. b. buycontoso.com?, aber keinen Domänen Namen auf der dritten Ebene, z. b. Marketing.contoso.com. Weitere Informationen zum Auswählen einer Domäne für die Verwendung in Office 365 finden Sie unter [Domänen](https://technet.microsoft.com/library/office-365-domains.aspx).

   -   Erwerben Sie es von einer Domänen Registrierungsstelle, die die von Office 365 benötigten DNS-Einträge (Domain Nameserver) zulässt. Informationen dazu, welche Domänenregistrierungsstellen die erforderlichen DNS-Einträge ermöglichen, finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660). Wenn Sie Ihre Domäne bereits bei einer anderen Registrierungsstelle registriert haben, machen Sie sich keine Sorgen. Sie können die Domäne in eine andere Registrierungsstelle übertragen, wenn Sie die Domäne mit Office 365 verknüpfen.

2. **Konfigurieren Sie DNS-Einträge, die Office 365-Diensten ermöglichen, den Domänennamen zu verwenden.** Die einfachste Möglichkeit besteht darin, den Assistenten die DNS-Einträge für Sie konfigurieren zu lassen, wenn Sie die Domäne in Schritt 3 mit Ihrem Office 365-Abonnement verknüpfen. Wenn Sie dies stattdessen selbst tun möchten, finden Sie weitere Informationen unter [Manuelles Konfigurieren von DNS-Einträgen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS).

3. **Verknüpfen Sie Ihre benutzerdefinierte Internetdomäne mit Ihrem Office 365-Abonnement.** Verwenden Sie die Aktion **Domäne mit Office 365 verknüpfen** .

4. **Prüfen Sie, ob die Office 365-Dienste den neuen Domänennamen verwenden.**

   Wenn Sie die Schritte 1 und 2 ausgeführt haben, bevor Sie die Aufgabe **Domäne mit Office 365 verknüpfen** verwenden, kann der Assistent den Domänen Namen mit Office 365 verknüpfen. Alternativ kann Sie der Assistent bei Teilen von oder den gesamten Schritten 1 und 2 unterstützen.

##### <a name="to-link-your-organizations-internet-domain-to-office-365"></a>So verknüpfen Sie die Internet Domäne Ihrer Organisation mit Office 365

1.  Öffnen Sie auf dem Dashboard die Seite **Office 365** , und klicken Sie auf **Domäne mit Office 365 verknüpfen**.

2.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

     Der Assistent kann Ihnen bei einigen oder allen Schritten zum Registrieren, konfigurieren und Verknüpfen eines neuen oder bereits vorhandenen Internet Domänen Namens für die Verwendung in Office 365 helfen.

     Klicken Sie auf den Hilfelink auf der Seite des Assistenten, um die Informationen abzurufen, die Sie benötigen, um eine Aufgabe auszuführen. Eine Prozessübersicht und Anforderungen finden Sie im Abschnitt "Einrichten eines Domänen namens" unter [Verwalten von Remote Webzugriff in Windows Server Essentials](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) .

    > [!NOTE]
    >  Um den Assistenten zu verwenden, um einen neuen Domänennamen zu registrieren, müssen Sie einen Domain Name Service-Anbieter verwenden, der Partner von Microsoft ist, um eine nahtlose Integration mit dem Assistenten bereitstellen zu können. Eine Domänennamen-Registrierungsstelle finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).

3.  Wenn der Assistent erkennt, dass der Domänen Name nicht vom Server verwaltet wird, müssen Sie die erforderlichen DNS-Einträge manuell konfigurieren, um die Konfiguration abzuschließen. Anweisungen finden Sie unter [Gewusst wie: Manuelles Konfigurieren von DNS-Datensätzen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS) weiter unten in diesem Thema.

4.  Vergewissern Sie sich, dass die Domäne in Office 365 verwendet wird.

     Nachdem der Assistent abgeschlossen ist, wird ein wenig gewartet, während die Domänen Namen-Registrierungsstelle die DNS-Einträge überprüft. Dies geschieht automatisch. Sie müssen nichts tun. Es dauert jedoch im Allgemeinen ungefähr eine Stunde, aber manchmal etwas länger. Nach Abschluss der Domänen Überprüfung wird auf der Seite **Office 365** die Domäne Ihrer Organisation aufgelistet.

####  <a name="how-to-manually-configure-dns-records-for-office-365-integration"></a><a name="BKMK_ManuallyConfigureDNS"></a>Manuelles Konfigurieren von DNS-Einträgen für die Integration von Office 365
 Wenn der Assistent für die Verknüpfung Ihrer Domäne mit Office 365 erkennt, dass der Domänenname nicht vom Server verwaltet wird, müssen zum Abschließen der Konfiguration manuell die erforderlichen Domänennamenserver (DNS)-Einträge konfigurieren. In diesem Fall finden Sie eine Liste der DNS-Einträge, die Sie konfigurieren müssen, unter **% username% \ NewDNSRecords_ (n). txt**, wobei *(n)* eine zufällige Zahl ist.

 Die folgende Tabelle beschreibt die DNS-Einträge, die Sie hinzufügen müssen. Eintragsmethoden können bei unterschiedlichen Domänennamen-Registrierungsstellen variieren. Wenn Sie Fragen haben, wenden Sie sich an die Domänennamen-Registrierungsstelle.

### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>Erforderliche DNS-Einträge für die Verknüpfung eines benutzerdefinierten Internetdomänennamens mit Office 365

|Dienst|Erforderliche DNS-Einträge|Zweck|
|-------------|--------------------------|-------------|
|(Mehrere Dienste)|MX| Office 365 verwendet diesen Datensatz, um zu überprüfen, ob Sie einen bestimmten Domänen Namen besitzen. Dieser MX-Eintrag beeinträchtigt das Routing von E-Mail-Nachrichten nicht.|
|Exchange Online|MX|Ermöglicht Routing von E-Mail-Nachrichten. **Wichtig:**  Wenn Sie e-Mail migrieren, weisen Sie dem neuen MX-Eintrag keine Einstellung von NULL (**0**) zu. Stellen Sie sicher, dass der Wert für den Eintrag größer ist, als der Wert, der dem aktuellen MX-Eintrag zugewiesen ist. Wenn die e-Mail-Migration abgeschlossen ist und Sie bereit sind, den e-Mail-Server in Office 365 zu ändern, muss die Domänen Namen-Registrierungsstelle den Wert des neuen MX-Einsatzes zurücksetzen.|
|Exchange Online|Alias (CNAME)|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen Exchange Online und dem Outlook-Client auf deren Desktops oder einem mobilen E-Mail-Client zu unterstützen. **Hinweis:**  Wenn Sie den Zugriff auf Outlook Webzugriff bevorzugen, indem Sie den eigenen Domänen Namen Ihrer Organisation verwenden (z. b. http://mail.contoso.com) anstelle der Standard-URL ( https://outlook.com/owa/office365.com) ), können Sie den Alias Eintrag (CNAME) wie folgt konfigurieren: **Type = CNAME, TTL = 01:00:00, Hostname = Mail, Address = Mail. Office 365. com**|
|Exchange Online|TXT|Gibt an, dass Outlook.com, die Domäne, die von den Office 365-e-Mail-Servern verwendet wird, autorisiert ist, e-Mails im Namen Ihrer Domäne zu senden. Erstellen Sie diesen Eintrag, um zu verhindern, dass Ihre ausgehenden E-Mail-Nachrichten als Spam gekennzeichnet werden.|
|Lync Online|SRV|Hilft, den Verbund mit anderen Instant Messaging-Diensten, wie z. B. Windows Live oder Yahoo! zu ermöglichen.|
|Lync Online|SRV|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen dem Lync-Desktopclient und Microsoft Lync Online zu unterstützen.|

> [!IMPORTANT]
>  Versuchen Sie nach Abschluss der Domänen Überprüfung nicht, die DNS-Einträge im Office 365-Portal hinzuzufügen oder weitere Änderungen vorzunehmen.

###  <a name="next-step"></a><a name="BKMK_StepFour_ACCOUNTS"></a>Nächster Schritt

-   Erstellen Sie Microsoft Online Services-Konten für die Benutzer.

     Um Office 365-Dienste verwenden zu können, müssen die Benutzer über ein Microsoft Online Services-Konto verfügen, das Ihrem Netzwerk Benutzerkonto zugeordnet ist. Dies ist mit dem Dashboard ganz einfach. Wenn Sie ein neues Office 365-Abonnement verwenden, können Sie Online Konten für vorhandene Benutzerkonten per Massen Vorgang erstellen. Wenn Sie einen neuen Server mit einem Office 365-Abonnement integrieren, das Sie bereits verwenden, können Sie Benutzerkonten aus Ihren vorhandenen Online Konten importieren. Informationen zu Verfahren finden Sie unter [Verwalten von Online Konten für Benutzer](Manage-Online-Accounts-for-Users.md).

> [!NOTE]
>  Auf dem Dashboard in Windows Server Essentials werden Microsoft Online Services-Konten als Office 365-Konten bezeichnet. Die Konten sind identisch, nur die Terminologie ist anders.

##  <a name="manage-office-365-integration"></a><a name="BKMK_ManageIntegration"></a>Verwalten der Integration von Office 365
 Nachdem Sie den Server in Office 365 integriert haben, zeigt die Seite **Office 365** auf dem Dashboard Informationen zu Ihrem Office 365-Abonnement an und stellt diese Aufgaben zur Verfügung:

-   [Verwalten Sie Ihr Office 365-Abonnement](#BKMK_ManageO365) ? Ändern Sie das Administrator Konto, das Sie zum Verwalten des Abonnements verwenden. Öffnen Sie das Office 365 Admin-Dashboard, um Ihr Abonnement zu verwalten.

-   [Verknüpfen Sie die Internet Domäne Ihrer Organisation mit Office 365](#BKMK_StepThree) ? Wenn Sie in der Lage sein möchten, e-Mail-Nachrichten an Ihre eigene Domäne zu senden und zu empfangen, können Sie die Domäne mit Office 365 verknüpfen. (Zuvor erläutert in [Schritt 3: Verknüpfen Sie die Domäne Ihrer Organisation mit Office 365](#BKMK_StepThree).)

-   [Integration von Office 365 deaktivieren](#BKMK_Disable) ? Wenn Sie Ihre Office 365-Dienste,-Abonnements und-Online Konten nicht über das Dashboard verwalten möchten, können Sie die Integration von Office 365 deaktivieren. Die Dienste sind weiterhin im Office 365-Portal verfügbar.

###  <a name="manage-your-office-365-subscription"></a><a name="BKMK_ManageO365"></a>Verwalten Ihres Office 365-Abonnements
 Wenn Sie Änderungen an Ihrem Office 365-Abonnement vornehmen müssen, während Sie auf dem Server arbeiten, können Sie das Abonnement in Office 365 auf der Seite **Office 365** des Dashboards öffnen. Sie können auch das Administrator Konto ändern, mit dem der Serveränderungen an den Office 365-Diensten vornimmt.

##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>So öffnen Sie das Abonnement mit dem Office 365-Administratordashboard

1.  Öffnen Sie im Windows Server Essentials-Dashboard die Seite **Office 365** .

2.  Klicken Sie unter **Konfigurationsaufgaben** auf **Office 365 verwalten**.

3.  Melden Sie sich mit dem Microsoft-Onlinekonto, das Sie zum Verwalten Ihres Abonnements verwenden, bei Office 365 an.

     Das Office 365 Admin-Dashboard wird geöffnet.

##### <a name="to-change-the-office-365-administrator-account"></a>So ändern Sie das Administratorkonto für Office 365

1.  Klicken Sie auf dem Dashboard auf **Office 365**.

2.  Klicken Sie unter **Konfigurationsaufgaben**auf **Office 365-Administratorkonto ändern**. Der Assistent zum Ändern von Administratorenkonten wird angezeigt. (In Windows Server Essentials heißt der Assistent "Office 365-Administrator Konto einrichten".)

3.  Geben Sie die Anmelde Informationen für das Konto ein, das Sie zum Herstellen einer Verbindung mit Ihrem Office 365-Abonnement verwenden möchten, und klicken Sie dann auf **weiter**.

4.  Klicken Sie auf **Schließen**. Das Dashboard wird neu gestartet.

###  <a name="disable-office-365-integration"></a><a name="BKMK_Disable"></a>Deaktivieren der Integration von Office 365
 Wenn Sie entscheiden, dass Sie Ihre Office 365-Dienste und Online Konten nicht über das Dashboard verwalten möchten, können Sie die Integration von Office 365 deaktivieren. Ihr Office 365-Abonnement bleibt aktiv, und alle Konfigurationsänderungen, die Sie über das Dashboard vorgenommen haben, bleiben in Kraft. Beispielsweise erhalten Sie eine e-Mail, die an einen Domänen Namen gerichtet ist, den Sie mit Ihrem Office 365-Abonnement verknüpft haben. Sie verlieren keine e-Mails, und die von Ihnen für mobile Geräte festgelegten Steuerelemente werden weiterhin in Exchange Online verwendet.

 In Zukunft verwalten Sie Ihr Office 365-Abonnement, Dienste und Ressourcen in Office 365, und Ihre Benutzer müssen die Kenn Wörter für Ihre Online Konten in Office 365 verwalten. Die Kenn Wort Synchronisierung erfolgt nicht mehr, und das Deaktivieren oder Entfernen eines Benutzerkontos hat keine Auswirkung auf das Onlinekonto des Benutzers.

 Da die Office 365-Integrationssoftware auf dem lokalen Server installiert ist, können Sie die Funktion auch dann deaktivieren, wenn der Integrations Dienst keine Verbindung mit Office 365 herstellen kann.

##### <a name="to-disable-office-365-integration-with-the-server"></a>So deaktivieren Sie die Office 365-Integration mit dem Server

1.  Klicken Sie auf dem Dashboard auf **Office 365**.

2.  Klicken Sie auf **Office 365-Integration deaktivieren**. Der Assistent für das Deaktivieren von Office 365 wird angezeigt.

3.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

> [!NOTE]
>  Um die Integration von Office 365 erneut zu aktivieren, verwenden Sie die Aufgabe in **Office 365 integrieren** auf der Registerkarte **Dienst** auf der **Start** Seite des Dashboards. Anweisungen finden Sie unter [Schritt 2: Integrieren des Windows Server Essentials-Servers mit Microsoft Office 365](#BKMK_StepTwo)weiter oben in diesem Thema.

##  <a name="troubleshoot-office-365-integration"></a><a name="BKMK_Troubleshoot"></a>Problembehandlung bei der Integration von Office 365
 Dieser Abschnitt enthält Informationen, die Ihnen helfen, häufige Probleme zu beheben, die bei der Verwendung der Office 365-Integrationsfunktionen in Windows Server Essentials auftreten können.

###  <a name="some-microsoft-online-services-accounts-were-not-created"></a><a name="BKMK_AcctsNotCreated"></a>Einige Microsoft Online Services-Konten wurden nicht erstellt.
 **Beschreibung**

 Der Versuch, ein oder mehrere Microsoft Online Services-Konten über das Dashboard zu erstellen, war nicht erfolgreich.

 **Lösung**

1.  Klicken Sie auf die Abschlussseite des Assistenten, um eine Ergebnisdatei zu öffnen, die ausführliche Informationen zu jeder Anforderung zum Erstellen eines Kontos enthält, die nicht erfolgreich abgeschlossen wurde. Beispielsweise kann ein Ergebnis Ihnen aufzeigen, dass ein Microsoft Online Services-Konto mit dem Namen eines angeforderten Kontos bereits vorhanden ist.

2.  Führen Sie die empfohlenen Aktionen aus, um jeden Fehler zu beheben.

3.  Wenn dieses Problem weiterhin besteht, starten Sie den Server neu, und versuchen Sie, die Onlinekonten erneut zu erstellen.

###  <a name="there-was-a-problem-uninstalling-office-365-integration"></a><a name="BKMK_ProblemUninstalling"></a>Beim Deinstallieren der Integration von Office 365 ist ein Problem aufgetreten.
 **Beschreibung**

 Unbekannter Fehler beim Versuch, die Integration von Office 365 zu deaktivieren.

 **Lösung**

1.  Stellen Sie sicher, dass der Computer mit dem Internet verbunden ist, und versuchen Sie es erneut.

2.  Wenn der Fehler erneut auftritt, starten Sie den Server neu, und versuchen Sie es erneut.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Übersicht über die Dienst Integration für Windows Server Essentials-Teil 1](https://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)

-   [Übersicht über die Dienst Integration für Windows Server Essentials-Teil 2](https://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)

-   [Erste Schritte für die Verwendung von Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)

-   [Verwalten von Microsoft Online Services](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)
