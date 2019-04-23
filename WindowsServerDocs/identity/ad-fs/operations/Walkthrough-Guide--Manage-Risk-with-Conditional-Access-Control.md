---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: 'Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11d2d567f9264dca53a3426263a172649d7d7c11
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826651"
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung

>Gilt für: Windows Server 2012 R2


## <a name="about-this-guide"></a>Informationen zum Handbuch
Diese exemplarische Vorgehensweise enthält Anweisungen zum Verwalten von Risiken mit einer der Faktoren (Benutzerdaten) zur Verfügung, über den Mechanismus für den bedingten Zugriff in Active Directory Federation Services (AD FS) in Windows Server 2012 R2. Weitere Informationen zu den bedingten Zugriff von Zugriffssteuerung und Autorisierungsmechanismen in AD FS unter Windows Server 2012 R2, finden Sie unter [Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md).

Die exemplarische Vorgehensweise enthält die folgenden Abschnitte:

-   [Schritt 1: Einrichten der testumgebung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Schritt 2: Überprüfen Sie die standardmäßige AD FS-Zugriffssteuerungsmechanismus](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [Schritt 3: Konfigurieren von Richtlinien für bedingten Zugriff basierend auf Benutzerdaten](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [Schritt 4: Überprüfen des Mechanismus für den bedingten Zugriff-Zugriffssteuerung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>Schritt 1: Einrichten der Testumgebung
Damit die exemplarische Vorgehensweise abgeschlossen werden kann, benötigen Sie eine Umgebung mit den folgenden Komponenten:

-   Active Directory-Domäne mit einem Testbenutzer und testgruppenkonten unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 mit einem Schema, das ein Upgrade auf Windows Server 2012 R2 oder Active Directory-Domäne unter Windows Server 2012 R2

-   Verbundserver unter Windows Server 2012 R2

-   Webserver, auf dem die Beispielanwendung gehostet wird

-   Clientcomputer, über den Sie auf die Beispielanwendung zugreifen können

> [!WARNING]
> Es wird (sowohl in Produktions- als auch in Testumgebungen) dringend empfohlen, nicht denselben Computer für den Verbundserver und den Webserver zu verwenden.

In dieser Umgebung gibt der Verbundserver die erforderlichen Ansprüche aus, sodass Benutzer auf die Beispielanwendung zugreifen können. Auf dem Webserver wird eine Beispielanwendung gehostet, die den Benutzern vertraut, die die vom Verbundserver ausgestellten Ansprüche vorweisen.

Anweisungen zum Einrichten dieser Umgebung finden Sie [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

## <a name="BKMK_2"></a>Schritt 2: Überprüfen des Standardmechanismus für die AD FS-Zugriffssteuerung
In diesem Schritt überprüfen Sie den Standardmechanismus für die AD FS-Zugriffssteuerung, bei dem der Benutzer auf die AD FS-Anmeldeseite umgeleitet wird, gültige Anmeldeinformationen eingibt und Zugriff auf die Anwendung erhält. Können Sie die **Robert Hatley** AD-Konto und die **Claimapp** beispielanwendung, die Sie in konfiguriert [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>So überprüfen Sie den Standardmechanismus für die AD FS-Zugriffssteuerung

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Mit dieser Aktion wird die Anforderung automatisch an den Verbundserver umgeleitet, und Sie werden zur Anmeldung mit einem Benutzernamen und einem Kennwort aufgefordert.

2.  Geben Sie die Anmeldeinformationen der **Robert Hatley** AD-Konto, das Sie in erstellt [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Ihnen wird der Zugriff auf die Anwendung gewährt.

## <a name="BKMK_3"></a>Schritt 3: Konfigurieren von Richtlinien für die bedingte Zugriffssteuerung auf Grundlage von Benutzerdaten
In diesem Schritt richten Sie basierend auf den Daten der Benutzergruppenmitgliedschaft eine Richtlinie für die Zugriffssteuerung ein. Sie konfigurieren also eine **Ausstellungsautorisierungsregel** auf dem Verbundserver für eine Vertrauensstellung der vertrauenden Seite, die Ihre Beispielanwendung **claimapp**darstellt. Von der Logik dieser Regel **Robert Hatley** AD-Benutzer werden Ansprüche ausgestellt, die erforderlich sind, um diese Anwendung zugreifen, da er zu gehört eine **Finance** Gruppe. Sie hinzugefügt haben, die **Robert Hatley** Konto die **Finance** Gruppe [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Sie können diese Aufgabe über die AD FS-Verwaltungskonsole oder über Windows PowerShell ausführen.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>So konfigurieren Sie die Richtlinie für die bedingte Zugriffssteuerung basierend auf Benutzerdaten über die AD FS-Verwaltungskonsole

1.  Navigieren Sie in der AD FS-Verwaltungskonsole zu **Vertrauensstellungen**und anschließend zu **Vertrauensstellungen der vertrauenden Seite**.

2.  Wählen Sie die Vertrauensstellung der vertrauenden Seite für Ihre Beispielanwendung (**claimapp**) aus, und wählen Sie anschließend entweder im Bereich **Aktionen** oder durch Rechtsklick auf diese Vertrauensstellung der vertrauenden Seite die Option **Anspruchsregeln bearbeiten** aus.

3.  Wählen Sie im Fenster **Anspruchsregeln für claimapp bearbeiten** die Registerkarte **Ausstellungsautorisierungsregeln** aus, und klicken Sie dann auf **Regel hinzufügen**.

4.  Wählen Sie in **Assistent zum Hinzufügen einer Ausstellungsautorisierungs-Anspruchsregel**auf der Seite **Regelvorlage auswählen**die Anspruchsregelvorlage **Benutzern den Zugriff auf Grundlage eines eingehenden Anspruchs gewähren oder verweigern** aus, und klicken Sie dann auf **Weiter**.

5.  Führen Sie auf der Seite **Regel konfigurieren** alle folgenden Aktionen aus, und klicken Sie dann auf **Fertig stellen**:

    1.  Geben Sie einen Namen für die Anspruchsregel ein, z. B. **TestRule**.

    2.  Wählen Sie für **Eingehender Anspruchstyp** die Option **Gruppen-SID** aus.

    3.  Klicken Sie auf **Durchsuchen**, geben Sie **Finance** als Name der AD-Testgruppe ein, und lösen Sie ihn für das Feld **Eingehender Anspruchswert** auf.

    4.  Wählen Sie die Option **Benutzern mit diesem eingehenden Anspruch Zugriff verweigern** aus.

6.  Stellen Sie im Fenster **Anspruchsregeln für claimapp bearbeiten** sicher, dass die Regel **Allen Benutzern Zugriff gewähren** , die beim Erstellen dieser Vertrauensstellung der vertrauenden Seite generiert wurde, gelöscht wird.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>So konfigurieren Sie die Richtlinie für die bedingte Zugriffssteuerung basierend auf Benutzerdaten über Windows PowerShell

1.  Öffnen Sie auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:


    `$rp = Get-AdfsRelyingPartyTrust -Name claimapp`


2.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:


    `$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`

> [!NOTE]
> Achten Sie darauf, <group_SID> durch den Wert der SID der AD-Gruppe **Finance** zu ersetzen.

## <a name="BKMK_4"></a>Schritt 4: Überprüfung des Mechanismus der bedingten Zugriffssteuerung
In diesem Schritt überprüfen Sie die Richtlinie für die bedingte Zugriffssteuerung, die Sie im vorherigen Schritt eingerichtet haben. Sie können mithilfe der folgenden Vorgehensweise überprüfen, ob der AD-Benutzer **Robert Hatley** auf die Beispielanwendung zugreifen kann, da er zur Gruppe **Finance** gehört. AD-Benutzer, die nicht zur Gruppe **Finance** gehören, können nicht auf die Beispielanwendung zugreifen.

1.  Klicken Sie auf dem Clientcomputer öffnen Sie ein Browserfenster, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**

    Mit dieser Aktion wird die Anforderung automatisch an den Verbundserver umgeleitet, und Sie werden zur Anmeldung mit einem Benutzernamen und einem Kennwort aufgefordert.

2.  Geben Sie die Anmeldeinformationen der **Robert Hatley** AD-Konto, das Sie in erstellt [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Ihnen wird der Zugriff auf die Anwendung gewährt.

3.  Geben Sie die Anmeldeinformationen eines anderen AD-Benutzers ein, der NICHT zur Gruppe **Finance** gehört. (Weitere Informationen zum Erstellen von Benutzerkonten in AD finden Sie unter [ https://technet.microsoft.com/library/cc7833232.aspx ](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx).

    An diesem Punkt aufgrund der Access-Control-Richtlinie, die im vorherigen Schritt wurden eingerichtet, eine Nachricht "Zugriff verweigert" wird für diesen AD-Benutzer, die nicht zu gehört die **Finance** Gruppe. Der Standardtext der Meldung ist **Sie sind nicht berechtigt, diese Website zugreifen. Klicken Sie hier, um melden Sie sich ab und melden Sie sich erneut, oder wenden Sie sich an Ihren Administrator, Berechtigungen zu erhalten.** . Dieser Text kann jedoch vollständig angepasst werden. Weitere Informationen zum Anpassen der Anmeldeseiten finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
[Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



