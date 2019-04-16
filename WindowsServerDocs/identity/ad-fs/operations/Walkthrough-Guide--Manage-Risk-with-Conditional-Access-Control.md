---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: Handbuch mit exemplarischer Vorgehensweise - Verwalten von Risiken mit Steuerung des bedingten Zugriffs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11d2d567f9264dca53a3426263a172649d7d7c11
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit Steuerung des bedingten Zugriffs

>Gilt für: Windows Server 2012 R2


## <a name="about-this-guide"></a>Informationen zum Handbuch
Diese exemplarische Vorgehensweise enthält Anweisungen zum Verwalten von Risiken mit einem der Faktoren (Benutzerdaten) verfügbar über den Mechanismus der bedingten Steuerelement in Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2. Weitere Informationen zu der bedingten Zugriffssteuerung und Autorisierungsmechanismen in AD FS unter Windows Server 2012 R2, finden Sie unter [Manage Risk with Conditional Access Control](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md).

In dieser exemplarischen Vorgehensweise besteht aus den folgenden Abschnitten:

-   [Schritt 1: Einrichten der testumgebung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Schritt 2: Überprüfen Sie den standardmäßigen AD FS-Mechanismus](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [Schritt 3: Konfigurieren von bedingten Zugriffssteuerungsrichtlinien basierend auf Benutzerdaten](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [Schritt 4: Überprüfen Sie, ob Mechanismus der bedingten Zugriffssteuerung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>Schritt 1: Einrichten der testumgebung
Um diese exemplarische Vorgehensweise abzuschließen, benötigen Sie eine Umgebung, die die folgenden Komponenten:

-   Active Directory-Domäne mit einem Testbenutzer und testgruppenkonten unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 mit einem Windows Server 2012 R2 oder Windows Server 2012 R2 unter Active Directory-Domäne

-   Verbundserver unter Windows Server 2012 R2

-   Ein Webserver, der für Ihre beispielanwendung gehostet

-   Ein Clientcomputer, von dem Sie die beispielanwendung zugreifen können

> [!WARNING]
> Es wird dringend empfohlen (sowohl in Produktions-Umgebungen), dass Sie nicht denselben Computer den Verbundserver und den Webserver zu verwenden.

In dieser Umgebung gibt der Verbundserver die Ansprüche, die erforderlich sind, damit Benutzer auf die beispielanwendung zugreifen können. Der Webserver hostet einer beispielanwendung, die den Benutzern vertraut wird, die die Ansprüche, die vorhanden vom Verbundserver ausgestellten.

Eine Anleitung zum Einrichten dieser Umgebung finden Sie unter [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

## <a name="BKMK_2"></a>Schritt 2: Überprüfen Sie den standardmäßigen AD FS-Mechanismus
In diesem Schritt überprüfen Sie die standardmäßige AD FS-Zugriffssteuerungsmechanismus, wo der Benutzer auf die AD FS-Anmeldeseite umgeleitet wird, gültige Anmeldeinformationen, und Zugriff auf die Anwendung gewährt. Können die **Robert Hatley** AD-Konto und die **Claimapp** Beispiel-App, die Sie in konfiguriert [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>Überprüfen Sie den Zugriff auf AD FS Steuermechanismus

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Diese Aktion aus, leitet die Anforderung automatisch an den Verbundserver und Sie werden aufgefordert, sich mit einem Benutzernamen und Kennwort anmelden.

2.  Geben Sie die Anmeldeinformationen von der **Robert Hatley** AD-Konto, das Sie erstellt haben [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Sie können den Zugriff auf die Anwendung gewährt werden.

## <a name="BKMK_3"></a>Schritt 3: Konfigurieren von bedingten Zugriffssteuerungsrichtlinien basierend auf Benutzerdaten
In diesem Schritt richten Sie eine Zugriffssteuerungsrichtlinie Grundlage der Gruppenmitgliedschaftsdaten des Benutzers ein. Anders ausgedrückt, konfigurieren Sie eine **Ausstellungsautorisierungsregel** auf dem Verbundserver für eine Vertrauensstellung einer vertrauenden Seite, die Ihre beispielanwendung **Claimapp**. Von der Logik dieser Regel **Robert Hatley** AD-Benutzer, die erforderlich sind, auf die Anwendung zugreifen, da er zur Gruppe Ansprüche ausgestellt eine **Finanzen** Gruppe. Sie hinzugefügt haben die **Robert Hatley** Konto die **Finanzen** Gruppe [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Sie können diese Aufgabe mithilfe der beiden AD FS-Verwaltungskonsole oder über Windows PowerShell.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>So konfigurieren Sie bedingten Zugriffssteuerungsrichtlinien basierend auf Benutzerdaten über die AD FS-Verwaltungskonsole

1.  Wechseln Sie in der AD FS-Verwaltungskonsole zu **Vertrauensstellungen**, und klicken Sie dann **Vertrauensstellungen für vertrauende Seiten**.

2.  Wählen Sie die Vertrauensstellung aus der vertrauenden Seite, die Ihre beispielanwendung (**Claimapp**), und klicken Sie dann entweder in der **Aktionen** Bereich oder durch Rechtsklick auf diese Vertrauensstellung der vertrauenden Seite, die Option **Anspruchsregeln bearbeiten**.

3.  In der **Anspruchsregeln für Claimapp bearbeiten** wählen **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie auf **Regel hinzufügen**.

4.  In der **Ausstellung Autorisierung Anspruch Assistenten zum Hinzufügen**auf die **Regelvorlage auswählen Seite**Option **zulassen oder verweigern Benutzer auf Basis eines eingehenden Anspruchs** anspruchsregelvorlage, und klicken Sie dann auf **Weiter**.

5.  Auf der **Regel konfigurieren** Seite, führen Sie die folgenden Schritte aus, und klicken Sie dann auf **Fertig stellen**:

    1.  Geben Sie einen Namen für die Anspruchsregel ein, z. B. **TestRule**.

    2.  Wählen Sie **Gruppen-SID** als **eingehender Anspruchstyp**.

    3.  Klicken Sie auf **Durchsuchen**, geben Sie im **Finanzen** für den Namen der AD Testgruppe aus, und lösen Sie ihn für die **eingehender Anspruchswert** Feld.

    4.  Wählen Sie die **Benutzern mit diesem eingehenden Anspruch Zugriff verweigern** Option.

6.  In der **Anspruchsregeln für Claimapp bearbeiten** Fenster, stellen Sie sicher, dass Sie das Löschen der **ermöglichen den Zugriff auf alle Benutzer** Regel, die standardmäßig erstellt wurde, wenn Sie diese Vertrauensstellung der vertrauenden Seite erstellt haben.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>So konfigurieren Sie bedingten Zugriffssteuerungsrichtlinien basierend auf Benutzerdaten über Windows PowerShell

1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus:


    `$rp = Get-AdfsRelyingPartyTrust -Name claimapp`


2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein:


    `$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`

> [!NOTE]
> Achten Sie darauf, < Group_SID > durch den Wert der SID der AD ersetzen **Finanzen** Gruppe.

## <a name="BKMK_4"></a>Schritt 4: Überprüfen Sie, ob Mechanismus der bedingten Zugriffssteuerung
In diesem Schritt überprüfen Sie die Richtlinie für die bedingte Zugriffssteuerung, die Sie im vorherigen Schritt haben eingerichtet. Können die folgende Verfahren überprüfen, ob **Robert Hatley** AD-Benutzer auf Ihre beispielanwendung zugreifen kann, da er zur Gruppe der **Finanzen** AD- Benutzer, die nicht angehören, die **Finanzen** Gruppe kann nicht auf die beispielanwendung zugreifen.

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**

    Diese Aktion aus, leitet die Anforderung automatisch an den Verbundserver und Sie werden aufgefordert, sich mit einem Benutzernamen und Kennwort anmelden.

2.  Geben Sie die Anmeldeinformationen von der **Robert Hatley** AD-Konto, das Sie erstellt haben [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Sie können den Zugriff auf die Anwendung gewährt werden.

3.  Geben Sie die Anmeldeinformationen eines anderen AD-Benutzer, die nicht zur Gruppe der **Finanzen** Gruppe. (Weitere Informationen zum Erstellen von Benutzerkonten in AD finden Sie unter [https://technet.microsoft.com/library/cc7833232.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx).

    Zu diesem Zeitpunkt aufgrund der Zugriffssteuerungsrichtlinie, die Sie im vorherigen Schritt eingerichtet, "Zugriff verweigert" erscheint eine für diesen AD-Benutzer, die nicht zur Gruppe der **Finanzen** Gruppe. Der Standardtext der Meldung ist **Sie sind nicht berechtigt, diese Website zuzugreifen. Klicken Sie hier, um melden Sie sich ab und melden Sie sich erneut oder wenden Sie sich an Ihren Administrator Berechtigungen.** Dieser Text kann jedoch vollständig angepasst werden. Weitere Informationen zur Vorgehensweise beim Anpassen der Anmeldeseiten finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
[Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



