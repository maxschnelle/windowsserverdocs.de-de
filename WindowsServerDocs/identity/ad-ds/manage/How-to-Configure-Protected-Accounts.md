---
ms.assetid: 70c99703-ff0d-4278-9629-b8493b43c833
title: Konfigurieren geschützter Benutzerkonten
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6410936e50f4fad34b18fb8f287d9df710347863
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823453"
---
# <a name="how-to-configure-protected-accounts"></a>Konfigurieren geschützter Benutzerkonten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bei Pass-the-hash (PtH)-Angriffen können Angreifer den zugrunde liegenden NTLM-Hash eines Benutzerkennworts (oder anderer Teile der Anmeldeinformationen) verwenden, um sich bei einem Remote-Server zu authentifizieren. Microsoft hat bereits eine Anleitung zur Entschärfung von Pass-the-Hash-Angriffen [veröffentlicht](https://www.microsoft.com/download/details.aspx?id=36036) .  Windows Server 2012 R2 enthält neue Features, die dazu beitragen, derartige Angriffe weiter zu verringern. Weitere Informationen zu anderen Sicherheitsfeatures, die zum Schutz vor Diebstahl von Anmelde Informationen beitragen, finden Sie unter [Schutz und Verwaltung von Anmelde](https://technet.microsoft.com/library/dn408190.aspx)Informationen. Dieser Artikel beschreibt die Konfiguration der folgenden neuen Features:

-   [Geschützte Benutzer](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_AddtoProtectedUsers)

-   [Authentifizierungs Richtlinien](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicies)

-   [Authentifizierungs Richtlinien Silos](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicySilos)

Windows 8 und Windows Server 2012 R2 enthalten zusätzliche Schutzmaßnahmen gegen den Diebstahl von Anmeldeinformationen. Lesen Sie dazu die folgenden Artikel:

-   [Eingeschränkter Administrator Modus für Remotedesktop](https://blogs.technet.com/b/kfalde/archive/2013/08/14/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)

-   [LSA-Schutz](https://technet.microsoft.com/library/dn408187)

## <a name="protected-users"></a><a name="BKMK_AddtoProtectedUsers"></a>Geschützte Benutzer
Geschützte Benutzer ist eine neue globale Sicherheitsgruppe, zu der Sie neue oder existierende Benutzer hinzufügen können. Windows 8.1 Geräte und Windows Server 2012 R2-Hosts haben ein spezielles Verhalten mit Mitgliedern dieser Gruppe, um einen besseren Schutz vor Diebstahl von Anmelde Informationen zu gewährleisten. Bei einem Mitglied der Gruppe werden von einem Windows 8.1 Gerät oder einem Windows Server 2012 R2-Host keine Anmelde Informationen zwischengespeichert, die für geschützte Benutzer nicht unterstützt werden. Mitglieder dieser Gruppe haben keinen zusätzlichen Schutz, wenn Sie auf einem Gerät angemeldet sind, auf dem eine frühere Windows-Version als Windows 8.1 ausgeführt wird.

Mitglieder der Gruppe der geschützten Benutzer, die bei Windows 8.1 Geräten und Windows Server 2012 R2-Hosts angemeldet sind, können *nicht mehr* verwenden:

-   Delegierung der Standardanmeldeinformationen (CredSSP) - Klartext-Anmeldeinformationen werden auch dann nicht zwischensgespeichert, wenn die Richtlinie **Delegierung von Standardanmeldeinformationen zulassen** aktiviert ist

-   Windows Digest - Klartext-Anmeldeinformationen werden auch dann nicht zwischengespeichert, wenn diese aktiviert sind

-   NTLM - NTOWF wird nicht zwischengespeichert

-   Langfristig gültige Kerberos-Schlüssel - Kerberos Ticket Granting ticket (TGT) wird bei der Anmeldung abgerufen und kann nicht automatisch erneut abgerufen werden

-   Offlineanmeldung - die zwischengespeicherte Anmeldungsprüfung wird nicht erstellt

Wenn die Domänen Funktionsebene Windows Server 2012 R2 ist, können Mitglieder der Gruppe nicht mehr folgende Aktionen ausführen:

-   Authentifizierung per NTLM

-   Datenverschlüsselungssstandard (DES) oder RC4- Verschlüsselungssammlungen in der Kerberos-Vorabauthentifizierung

-   Delegieren per uneingeschränkter oder eingeschränkter Delegierung

-   Erneuern von Benutzertickets (TGTs) jenseits der ursprünglichen 4-stündigen Lebensdauer

Wenn Sie der Gruppe Benutzer hinzufügen möchten, können Sie Benutzeroberflächen [Tools](https://technet.microsoft.com/library/cc753515.aspx) wie Active Directory-Verwaltungscenter (ADAC) oder Active Directory Benutzer und Computer oder ein Befehlszeilen Tool wie [dsmod group](https://technet.microsoft.com/library/cc732423.aspx)oder das Windows PowerShell-Cmdlet[Add-adgroupmember](https://technet.microsoft.com/library/ee617210.aspx) verwenden. Konten für Dienste und Computer *sollten nicht* Mitglieder der Benutzergruppe Geschützte Benutzer sein. Die Mitgliedschaft bietet für diese Konten keinen lokalen Schutz, da Kennwort bzw. Zertifikat auf dem Host immer verfügbar sind.

> [!WARNING]
> Die Authentifizierungseinschränkungen können nicht umgangen werden, d. h. Mitglieder der höher privilegierten Gruppen wie z. B. Unternehmens-Admins oder Domänen-Admins unterliegen denselben Einschränkungen wie andere Mitglieder der Gruppe Geschützte Benutzer. Wenn alle Mitglieder dieser Gruppen der Gruppe "geschützte Benutzer" hinzugefügt werden, können alle diese Konten gesperrt werden. Sie sollten niemals alle Konten mit hohen Berechtigungen zur Gruppe der geschützten Benutzer hinzufügen, bis Sie die möglichen Auswirkungen gründlich getestet haben.

Mitglieder der Gruppe Geschützte Benutzer müssen in der Lage sein, sich mit dem erweiterten Verschlüsselungsstandard (AES) und Kerberos anzumelden. Für diese Methode sind AES-Schlüssel in Active Directory erforderlich. Der integrierte Administrator verfügt über keinen AES-Schlüssel, es sei denn, das Kennwort wurde auf einem Domänen Controller geändert, auf dem Windows Server 2008 oder höher ausgeführt wird. Außerdem wird jedes Konto, das über ein Kennwort verfügt, das auf einem Domänen Controller mit einer früheren Version von Windows Server geändert wurde, gesperrt. Befolgen Sie daher die folgenden bewährten Methoden:

-   Testen Sie die Domänen nur dann, wenn auf **allen Domänen Controllern Windows Server 2008 oder höher ausgeführt**wird.

-   **Ändern Sie die Kennwörter** aller Domänenkonten, die *vor* der Domänenerstellung erstellt wurden. Andernfalls können sich diese Konten nicht mehr authentifizieren.

-   **Ändern Sie das Kennwort** für jeden Benutzer, bevor Sie das Konto der Gruppe der geschützten Benutzer hinzufügen, oder stellen Sie sicher, dass das Kennwort kürzlich auf einem Domänen Controller mit Windows Server 2008 oder höher geändert wurde.

### <a name="requirements-for-using-protected-accounts"></a><a name="BKMK_Prereq"></a>Anforderungen für die Verwendung geschützter Konten
Für geschützte Konten gelten die folgenden Bereitstellungsanforderungen:

-   Zum Bereitstellen von Client seitigen Einschränkungen für geschützte Benutzer müssen Hosts Windows 8.1 oder Windows Server 2012 R2 ausgeführt werden. Benutzer müssen sich nur mit einem Konto anmelden, das Mitglied der Gruppe Geschützte Benutzer ist. In diesem Fall kann die Gruppe der geschützten Benutzer erstellt werden, indem [die Rolle "primärer Domänen Controller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) " auf einen Domänen Controller übertragen wird, auf dem Windows Server 2012 R2 ausgeführt wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann die PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, der unter einer älteren Windows Server-Version läuft.

-   Um Domänen Controller seitige Einschränkungen für geschützte Benutzer bereitzustellen, d. h. die Verwendung der NTLM-Authentifizierung und andere Einschränkungen einzuschränken, muss die Domänen Funktionsebene Windows Server 2012 R2 sein. Weitere Informationen zu Funktionsebenen finden Sie unter [Understanding Active Directory Domain Services (AD DS) Funktionsebenen](../active-directory-functional-levels.md).

### <a name="troubleshoot-events-related-to-protected-users"></a><a name="BKMK_TrubleshootingEvents"></a>Behandeln von Problemen im Zusammenhang mit geschützten Benutzern
Dieser Abschnitt behandelt neue Protokollereignisse im Zusammenhang mit geschützten Benutzern und die Möglichkeiten von geschützten Benutzern für die Problembehandlung von Ticket Granting Ticket (TGT)-Ablauf und Delegierungsproblemen.

#### <a name="new-logs-for-protected-users"></a>Neue Protokolle für geschützte Benutzer

Es stehen zwei neue operative administrative Protokolle zur Verfügung, die bei der Problembehandlung bei Ereignissen im Zusammenhang mit geschützten Benutzern helfen: geschütztes Benutzer-Client Protokoll und geschützte Benutzerfehler-Domänen Controller Protokoll. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert. Um ein Protokoll zu aktivieren, klicken Sie auf **Anwendungs- und Dienstprotokolle**, klicken Sie auf **Microsoft**, dann auf **Windows**, auf **Authentifizierung**. Klicken Sie anschließend auf den Namen des Protokolls und klicken Sie auf **Aktion** (bzw. klicken Sie mit der rechten Maustaste auf das Protokoll) und klicken Sie auf **Protokoll aktivieren**.

Weitere Informationen zu Ereignissen in diesen Protokollen finden Sie unter [Authentifizierungs Richtlinien und Authentifizierungs Richtlinien Silos](https://technet.microsoft.com/library/dn486813.aspx).

#### <a name="troubleshoot-tgt-expiration"></a>Problembehandlung für den TGT-Ablauf
Normalerweise legt der Domänencontroller die TGT-Lebensdauer und -Erneuerung anhand der Domänenrichtlinie fest, wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster gezeigt.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

Für **Geschützte Benutzer** sind die folgenden Einstellungen hartcodiert:

-   Maximale Lebensdauer des Benutzer Tickets: 240 Minuten

-   Maximale Lebensdauer für die Verlängerung des Benutzer Tickets: 240 Minuten

#### <a name="troubleshoot-delegation-issues"></a>Problembehandlung für Delegierungsprobleme
Bislang wurde bei Fehlern in Technologien mit Kerberos-Delegierung geprüft, ob die Option **Konto ist vertraulich und kann nicht delegiert werden** für das Clientkonto gesetzt ist. Wenn das Konto jedoch Mitglied der Gruppe **Geschützte Benutzer** ist, kann es jedoch sein, dass diese Einstellung im Active Directory-Verwaltungscenter (ADAC) nicht gesetzt ist. Daher sollten Sie bei der Problembehandlung von Delegierungsproblemen diese Einstellung und die Gruppenmitgliedschaft prüfen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

### <a name="audit-authentication-attempts"></a><a name="BKMK_AuditAuthNattempts"></a>Authentifizierungs Versuche überwachen
Um Authentifizierungsversuche speziell für Mitglieder der Gruppe **Geschützte Benutzer** zu überwachen, können Sie weiterhin Überwachungsereignisse im Sicherheitslog sammeln oder die Daten in den neuen operationalen Administrationsprotokollen sammeln. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungs Richtlinien und Authentifizierungs Richtlinien Silos](https://technet.microsoft.com/library/dn486813.aspx) .

### <a name="provide-dc-side-protections-for-services-and-computers"></a><a name="BKMK_ProvidePUdcProtections"></a>Bereitstellen eines Domänen Controller seitigen Schutzes für Dienste und Computer
Konten für Dienste und Computer dürfen nicht Mitglieder der Benutzergruppe **Geschützte Benutzer** sein. Dieser Abschnitt beschreibt die möglichen domänencontrollerseitigen Schutzmaßnahmen für diese Konten:

-   NTLM-Authentifizierung ablehnen: nur über [NTLM-Block Richtlinien](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx) konfigurierbar.

-   Ablehnen von Daten Verschlüsselungs Standard (Data Encryption Standard, des) bei der Kerberos-Vorauthentifizierung: Windows Server 2012 R2-Domänen Controller akzeptieren des nicht für Computer Konten, es sei denn, Sie sind nur für die konfiguriert, weil jede mit Kerberos freigegebene Version von Windows auch RC4 unterstützt

-   Ablehnen von RC4 für die Kerberos-Vorabauthentifizierung: nicht konfigurierbar.

    > [!NOTE]
    > Obwohl es möglich ist, [die Konfiguration unterstützter Verschlüsselungstypen zu ändern](https://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx), empfiehlt es sich nicht, diese Einstellungen für Computer Konten zu ändern, ohne in der Zielumgebung zu testen.

-   Beschränken Sie die Benutzer Tickets (TGTs) auf eine anfängliche Zeit von 4 Stunden: Verwenden Sie Authentifizierungs Richtlinien.

-   Delegierung mit eingeschränkter oder eingeschränkter Delegierung verweigern: um ein Konto einzuschränken, öffnen Sie Active Directory-Verwaltungscenter (ADAC), und aktivieren Sie das Kontrollkästchen **Konto ist vertraulich und kann nicht delegiert werden** .

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

## <a name="authentication-policies"></a><a name="BKMK_CreateAuthNPolicies"></a>Authentifizierungs Richtlinien
Authentifizierungsrichtlinien sind ein neuer Container in AD DS, der Authentifizierungsrichtlinienobjekte enthält. Authentifizierungsrichtlinien enthalten Einstellungen zur Vermeidung des Diebstahls von Anmeldeinformationen, wie z. B. Einschränkung der TGT-Lebensdauer für Konten oder zusätzliche anspruchsrelevante Bedingungen.

In Windows Server 2012 wurde durch dynamische Access Control eine Active Directory-Objektklasse im Gesamtstruktur Bereich namens "zentrale Zugriffs Richtlinie" eingeführt, um eine einfache Möglichkeit zum Konfigurieren von Dateiservern in einer Organisation bereitzustellen. In Windows Server 2012 R2 kann eine neue Objektklasse namens Authentifizierungs Richtlinie (objectClass MSDS-authnpolicies) zum Anwenden der Authentifizierungs Konfiguration auf Konto Klassen in Windows Server 2012 R2-Domänen verwendet werden. Es existieren die folgenden Active Directory-Kontoklassen:

-   Benutzer

-   Computer

-   Verwaltete Dienstkonten und Gruppenverwaltete Dienstkonten (GMSA)

### <a name="quick-kerberos-refresher"></a>Kurze Kerberos-Auffrischung
Das Kerberos-Authentifizierungsprotokoll besteht aus drei Austauschtypen, auch bekannt als Unterprotokolle:

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbRefresher.gif)

-   Der Authentifizierungsdienst (AS)-Austausch (KRB_AS_*)

-   Der Ticket-Granting Service (TGS)-Austausch (KRB_AS_*)

-   Der Client/Server (AP)-Austausch (KRB_AP_*)

Beim AS-Austausch verwendet der Client das Kennwort oder den privaten Schlüssel des Kontos, um einen Pre-Authenticator zum Anfordern eines Ticket Zustellungs Tickets (TGT) zu erstellen. Dies erfolgt bei der Benutzeranmeldung oder beim ersten Mal, wenn ein Dienstticket benötigt wird.

Beim TGS-Austausch wird das TGT des Kontos zum Erstellen eines Authentifikators verwendet, um ein Dienst Ticket anzufordern. Dies erfolgt, wenn eine authentifizierte Verbindung benötigt wird.

Der AP-Austausch erfolgt normalerweise in Form von Daten innerhalb des Anwendungsprotokolls und wird nicht von Authentifizierungsrichtlinien beeinflusst.

Ausführlichere Informationen finden Sie unter [Funktionsweise des Kerberos Version 5-Authentifizierungs Protokolls](https://technet.microsoft.com/library/cc772815(v=WS.10).aspx).

### <a name="overview"></a>Übersicht
Authentifizierungsrichtlinien bieten geschützten Benutzern die Möglichkeit, konfigurierbare Einschränkungen für Konten einzurichten und bieten außerdem Einschränkungen für Dienst- und Computerkonten. Authentifizierungsrichtlinien werden entweder beim AS- oder beim TGS-Austausch umgesetzt.

Sie können die ursprüngliche Authentifizierung oder den AS-Austausch einschränken, indem Sie Folgendes konfigurieren:

-   Eine TGT-Lebensdauer

-   Bedingungen für die Zugriffssteuerung zum Einschränken der Benutzeranmeldung. Die Geräte, von denen der AS-Austausch stammt, müssen diese Bedingungen erfüllen

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictAS.gif)

Sie können Dienstticket-Anfragen über den Ticket-Granting Service (TGS) einschränken, indem Sie Folgendes konfigurieren:

-   Bedingungen für die Zugriffssteuerung, die vom Client (Benutzer, Dienst, Computer) bzw. vom Gerät erfüllt werden müssen, von dem der TGS-Austausch stammt

### <a name="requirements-for-using-authentication-policies"></a><a name="BKMK_ReqForAuthnPolicies"></a>Anforderungen für die Verwendung von Authentifizierungs Richtlinien

|Policy (Richtlinie)|Voraussetzungen|
|----------|----------------|
|Benutzerdefinierte TGT-Lebensdauer| Konto Domänen auf Domänen Funktionsebene auf Windows Server 2012 R2|
|Benutzeranmeldung beschränken|-Windows Server 2012 R2 Domänen Funktionsebene Konto Domänen mit dynamischer Access Control Unterstützung<br />-Windows 8-, Windows 8.1-, Windows Server 2012-oder Windows Server 2012 R2-Geräte mit dynamischer Access Control Unterstützung|
|Einschränken der Dienstticket-Ausstellung auf Basis von Benutzerkonten und Sicherheitsgruppen| Windows Server 2012 R2-Domänen Funktionsebene-Ressourcen Domänen|
|Einschränken der Dienstticket-Ausstellung auf Basis von Benutzeransprüchen, Gerätekonten, Sicherheitsgruppen oder Ansprüchen| Ressourcen Domänen auf Windows Server 2012 R2-Domänen Funktionsebene mit dynamischer Access Control Unterstützung|

### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>Einschränken von Benutzerkonten auf bestimmte Geräte und Hosts
Besonders wichtige Konten mit Administratorrechten sollten Mitglieder der Gruppe **Geschützte Benutzer** sein. Standardmäßig sind keine Benutzerkonten Mitglieder der Gruppe **Geschützte Benutzer**. Bevor Sie Konten zur Gruppe hinzufügen, sollten Sie die Domänencontroller-Unterstützung konfigurieren und eine Überwachungsrichtlinie erstellen, um sicherzugehen, dass keine blockierenden Probleme vorliegen.

#### <a name="configure-domain-controller-support"></a>Konfigurieren der Domänencontroller-Unterstützung

Die Konto Domäne des Benutzers muss sich auf der Windows Server 2012 R2-Domänen Funktionsebene befinden. Stellen Sie sicher, dass alle Domänen Controller Windows Server 2012 R2 sind, und verwenden Sie dann Active Directory Domänen und Vertrauens Stellungen, um [die DFL](https://technet.microsoft.com/library/cc753104.aspx) auf Windows Server 2012 R2 zu erhöhen.

**So konfigurieren Sie die Unterstützung für dynamische Access Control**

1.  Klicken Sie in der Standard-Domänencontrollerrichtlinie auf **Aktiviert**, um **die Clientunterstützung für das Schlüsselverteilungscenter (Key Distribution Center KDC) für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** unter Computerkonfiguration | Administrative Vorlagen | System | KDC zu aktivieren.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)

2.  Wählen Sie unter **Optionen** im Dropdown-Listenfeld den Wert **Immer Ansprüche bereitstellen** aus.

    > [!NOTE]
    > **Unterstützt** kann auch konfiguriert werden, aber da die Domäne unter Windows Server 2012 R2-DFL ist, ermöglichen die DCS immer Ansprüche, dass Anspruchs basierte Zugriffs Überprüfungen durchgeführt werden, wenn Geräte und Hosts, die Ansprüche unterstützen, keine Ansprüche unterstützenden Dienste verwenden.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)

    > [!WARNING]
    > Das Konfigurieren von **fehlgeschlagenen Authentifizierungsanforderungen** ohne hoch Rüstung führt zu Authentifizierungs Fehlern von Betriebssystemen, die Kerberos armoring nicht unterstützen, wie z. b. Windows 7 und ältere Betriebssysteme, oder Betriebssysteme ab Windows 8, die nicht explizit für deren Unterstützung konfiguriert wurden.

#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>Erstellen von Benutzerkonten-Überwachung für die Authentifizierungsrichtlinie im ADAC

1.  Öffnen Sie das Active Directory-Verwaltungscenter (ADAC).

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_OpenADAC.gif)

    > [!NOTE]
    > Der ausgewählte **Authentifizierungs** Knoten ist für Domänen unter Windows Server 2012 R2-DFL sichtbar. Wenn der Knoten nicht angezeigt wird, versuchen Sie es erneut, indem Sie ein Domänen Administrator Konto aus einer Domäne unter Windows Server 2012 R2-DFL verwenden.

2.  Klicken Sie auf **Authentifizierungsrichtlinien** und auf **Neu**, um eine neue Richtlinie zu erstellen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)

    Authentifizierungsrichtlinien müssen einen Anzeigenamen haben und werden standardmäßig erzwungen.

3.  Klicken Sie auf **Nur Richtlinieneinschränkungen überwachen**, um eine Richtlinie zur reinen Überwachung zu erstellen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)

    Authentifizierungsrichtlinien werden auf Basis des Active Directory-Kontotyps angewendet. Sie können eine einzige Richtlinie für alle drei Kontotypen anwenden, indem Sie die Einstellungen für die einzelnen Typen konfigurieren. Es existieren die folgenden Kontotypen:

    -   Benutzer

    -   Computer

    -   Verwaltete Dienstkonten und Gruppenverwaltete Dienstkonten

    Falls Sie das Schema mit neuen Prinzipalen erweitert haben, die vom Schlüsselverteilungscenter (KDC) verwendet werden können, wird der neue Kontotyp über den nächstgelegenen abgeleiteten Kontotyp bestimmt.

4.  Um eine TGT-Lebensdauer für Benutzerkonten zu konfigurieren, markieren Sie das Kontrollkästchen **Ticket Granting Ticket-Lebensdauer für Benutzerkonten angeben** und geben Sie die Lebensdauer in Minuten an.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTLifetime.gif)

    Geben Sie z. B. wie gezeigt **600** für eine 10-stündige maximale TGT-Lebensdauer ein. Wenn keine TGT-Lebensdauer konfiguriert ist und das Konto Mitglied der Gruppe **Protected Users** ist, beträgt die TGT-Lebensdauer und -Erneuerung 4 Stunden. Ansonsten werden TGT-Lebensdauer und -Erneuerung anhand der Domänenrichtlinie festgelegt, wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster für eine Domäne mit Standardeinstellungen gezeigt.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

5.  Um ein Benutzerkonto auf bestimmte Geräte zu beschränken, klicken Sie auf **Bearbeiten** und definieren Sie die Bedingungen für das Gerät.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)

6.  Klicken Sie im Fenster **Bedingungen für die Zugriffssteuerung bearbeiten** auf **Bedingung hinzufügen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCondition.png)

##### <a name="add-computer-account-or-group-conditions"></a>Computerkonto- oder Gruppenbedingungen hinzufügen

1.  Um Computerkonten oder Gruppen zu konfigurieren, ändern Sie im Dropdown-Listenfeld den Wert von **Mitglied aller Gruppen** zu **Mitglied einer oder mehrer Gruppen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompMember.png)

    > [!NOTE]
    > Diese Zugriffssteuerung definiert die Bedingungen für das Gerät bzw. den Host, von dem sich der Benutzer anmeldet. In der Zugriffssteuerungs-Terminologie ist das Computerkonto für das Gerät oder den Host der Benutzer. Daher ist **Benutzer** die einzige auswählbare Option.

2.  Klicken Sie auf **Elemente hinzufügen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddItems.png)

3.  Klicken Sie auf **Objekttypen**, um die Objekttypen zu ändern.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjects.gif)

4.  Klicken Sie auf **Computer** und auf **OK**, um Computerobjekte in Active Directory auszuwählen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)

5.  Geben Sie die Namen der Computer ein, auf die der Benutzer eingeschränkt werden soll, und klicken Sie auf **Namen überprüfen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)

6.  Klicken Sie auf OK und erstellen Sie ggf. weitere Bedingungen für das Computerkonto.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddConditions.png)

7.  Wenn Sie fertig sind, klicken Sie auf **OK**, um die definierten Bedingungen für das Computerkonto zu übernehmen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompDone.png)

##### <a name="add-computer-claim-conditions"></a>Computer-Anspruchsbedingungen hinzufügen

1.  Wählen Sie den Anspruch in der Gruppen-Dropdownliste aus, um Computeransprüche zu konfigurieren.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaim.gif)

    Ansprüche sind nur verfügbar, wenn diese bereits in der Gesamtstruktur eingerichtet wurden.

2.  Geben Sie den Namen der OU ein, auf die das Benutzerkonto bei der Anmeldung eingeschränkt werden soll.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimOUName.gif)

3.  Wenn Sie fertig sind, klicken Sie auf OK, um die definierten Bedingungen zu übernehmen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimComplete.gif)

##### <a name="troubleshoot-missing-computer-claims"></a>Problembehandlung für fehlende Computeransprüche
Falls ein Anspruch konfiguriert wurde und nicht verfügbar ist, kann es sein, dass dieser nur für die **Computer**-Klassen konfiguriert wurde.

Nehmen wir an, Sie möchten die Authentifizierung auf der Grundlage der Organisationseinheit (OU) des Computers beschränken, die bereits konfiguriert war, aber nur für **Computer** Klassen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictComputers.gif)

Markieren Sie das Kontrollkästchen **Benutzer**, um den Anspruch zum Einschränken der Benutzeranmeldung am Gerät verfügbar zu machen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)

#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>Einrichten eines Benutzerkontos mit Authentifizierungsrichtlinie in ADAC

1.  Klicken Sie im **Benutzerkonto** auf **Richtlinien**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicy.gif)

2.  Aktivieren Sie das Kontrollkästchen **Diesem Konto eine Authentifizierungsrichtlinie zuweisen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)

3.  Wählen Sie anschließend die gewünschte Authentifizierungsrichtlinie für den Benutzer aus.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicySelect.png)

#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>Konfigurieren der Unterstützung für dynamische Zugriffssteuerung auf Geräten und Hosts
Sie können die TGT-Lebensdauer ohne dynamische Zugriffssteuerung (DAC) konfigurieren. DAC wird nur beim Überprüfen von AllowedToAuthenticateFrom und AllowedToAuthenticateTo verwendet.

Aktivieren Sie **die Kerberos-Clientunterstützung für das Schlüsselverteilungscenter (Key Distribution Center KDC) für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** unter Computerkonfiguration | Administrative Vorlagen | System | Kerberos im Editor für Gruppenrichtlinien bzw. lokale Gruppenrichtlinien:

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)

### <a name="troubleshoot-authentication-policies"></a><a name="BKMK_TroubleshootAuthnPolicies"></a>Behandeln von Problemen mit Authentifizierungs Richtlinien

#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>Ermitteln der Konten, denen eine Authentifizierungsrichtlinie direkt zugewiesen ist
Im Bereich Konten für die Authentifizierungsrichtlinie werden die Konten angezeigt, denen diese Richtlinie direkt zugewiesen ist.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AccountsAssigned.gif)

#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Verwenden des Authentifizierungs Richtlinien Fehlers-Domänen Controller-Verwaltungs Protokoll
Ein neues **Authentifizierungs Richtlinien-Fehler-Domänen Controller-** Verwaltungs Protokoll unter **Anwendungs-und Dienst Protokolle** > **Microsoft** > **Windows** > - **Authentifizierung** wurde erstellt, um das Auffinden von Fehlern aufgrund von Authentifizierungs Richtlinien zu vereinfachen. Dieses Protokoll ist standardmäßig deaktiviert. Klicken Sie mit der rechten Maustaste auf das Protokoll und klicken Sie auf **Protokoll aktivieren,** um dieses Protokoll zu aktivieren. Die neuen Ereignisse sind den existierenden Ereignissen für Kerberos TGT und die Überwachung von Diensttickets inhaltlich sehr ähnlich. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungs Richtlinien und Authentifizierungs Richtlinien Silos](https://technet.microsoft.com/library/dn486813.aspx).

### <a name="manage-authentication-policies-by-using-windows-powershell"></a><a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Verwalten von Authentifizierungs Richtlinien mithilfe von Windows PowerShell
Dieser Befehl erstellt eine Authentifizierungsrichtlinie mit dem Namen **TestAuthenticationPolicy**. Der **UserAllowedToAuthenticateFrom**-Parameter gibt die Geräte, an denen sich Benutzer anmelden können, in Form einer SDDL-Zeichenfolge in der Datei mit dem Namen someFile.txt an.

```
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl
```

Dieser Befehl ruft alle Authentifizierungsrichtlinien ab, die mit dem im **Filter**-Parameter angegebenen Filter übereinstimmen.

```
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com

```

Dieser Befehl ändert die Beschreibung und die **UserTGTLifetimeMins**-Eigenschaften der angegebenen Authentifizierungsrichtlinie.

```
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45
```

Dieser Befehl entfernt die im **Identity**-Parameter angegebene Authentifizierungsrichtlinien.

```
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1
```

Dieser Befehl verwendet das **Get-ADAuthenticationPolicy**-Cmdlet mit dem **Filter**-Parameter, um alle nicht erzwungenen Authentifizierungsrichtlinien abzurufen. Das Ergebnis wird an das **Remove-ADAuthenticationPolicy**-Cmdlet weitergereicht.

```
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy
```

## <a name="authentication-policy-silos"></a><a name="BKMK_CreateAuthNPolicySilos"></a>Authentifizierungs Richtlinien Silos
Authentifizierungsrichtliniensilos ist ein neuer Container (objectClass msDS-AuthNPolicySilos) in AD DS für Benutzer, Computer und Dienstkonten. Authentifizierungsrichtliniensilos helfen beim Schutz besonders wichtiger Konten. Die Mitglieder der Gruppen Unternehmens-Admins, Domänen-Admins und Schema-Admins müssen in allen Unternehmen geschützt werden, da Angreifer mit diesen Konten Zugriff auf die Gesamtstruktur erhalten können. Allerdings benötigen auch andere Konten Schutz.

Manche Unternehmen isolieren die Arbeitsauslastung durch die Erstellung spezifischer Konten und die Anwendung von Gruppenrichtlinien, um die Berechtigungen für die interaktive Anmeldung lokal und remote einzuschränken. Authentifizierungsrichtliniensilos ergänzen diese Vorgehensweise um die Möglichkeit, Beziehungen zwischen Benutzern, Computern und verwalteten Dienstkonten zu definieren. Jedes Konto kann nur zu einem Silo gehören. Sie können Authentifizierungsrichtlinien für die einzelnen Kontotypen definieren, um Folgendes zu steuern:

1.  Nicht erneuerbare TGT-Lebensdauer

2.  Bedingungen für die Zugriffssteuerung für TGT (Hinweis: gilt nicht für Systeme, da Kerberos Armoring benötigt wird)

3.  Bedingungen für die Zugriffssteuerung für die Rückgabe von Diensttickets

Außerdem haben alle Konten in einem Authentifizierungsrichtliniensilo einen Siloanspruch, der von Ressourcen mit Anspruchsunterstützung wie z. B. Dateiservern für die Zugriffssteuerung genutzt werden kann.

Sie können eine neue Sicherheitsbeschreibung definieren, um die Ausgabe von Diensttickets anhand der folgenden Entitäten zu steuern:

-   Benutzer, Sicherheitsgruppen des Benutzers und/oder Benutzer Ansprüche

-   Gerät, Sicherheitsgruppe des Geräts und/oder Geräteansprüche

Um diese Informationen für die DCS der Ressource zu erhalten, sind dynamische Access Control erforderlich:

-   Benutzeransprüche:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Kontodomäne unterstützt dynamische Zugriffssteuerung und Ansprüche

-   Geräte- und/oder Gerätesicherheitsgruppe:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Für Verbundauthentifizierung konfigurierte Ressource

-   Geräteansprüche:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Gerätedomäne unterstützt dynamische Zugriffssteuerung und Ansprüche

    -   Für Verbundauthentifizierung konfigurierte Ressource

Authentifizierungsrichtlinien können für alle Mitglieder eines Authentifizierungsrichtliniensilos gleichzeitig angewendet werden. Für unterschiedliche Kontotypen innerhalb eines Silos können unterschiedliche Authentifizierungsrichtlinien angewendet werden. Sie können z. B. eine Authentifizierungsrichtlinie für Benutzerkonten mit höheren Berechtigungen anwenden, und eine andere Richtlinie für Dienstkonten. Sie müssen mindestens eine Authentifizierungsrichtlinie erstellen, um ein Authentifizierungsrichtliniensilo erstellen zu können.

> [!NOTE]
> Authentifizierungsrichtlinien können für alle Mitglieder eines Authentifizierungsrichtliniensilos gleichzeitig oder auch unabhängig vom Silo angewendet werden, um deren Auswirkungen auf bestimmte Konten einzuschränken. Um z. B. ein einzelnes Konto oder eine kleine Gruppe von Konten zu schützen, können Sie eine Richtlinie für diese Konten einstellen, ohne die Konten zu einem Silo hinzuzufügen.

Sie können ein Authentifizierungs Richtlinien Silo mithilfe von Active Directory-Verwaltungscenter oder Windows PowerShell erstellen. Standardmäßig überwacht ein Authentifizierungs Richtlinien Silo nur Silo-Richtlinien, was dem Angeben des **WhatIf** -Parameters in Windows PowerShell-Cmdlets entspricht. In diesem Fall gelten Einschränkungen für Richtliniensilos nicht. Überwachungsdaten werden jedoch generiert und zeigen an, ob beim Anwenden der Einschränkungen Fehler auftreten würden.

#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Erstellen von Authentifizierungsrichtliniensilos im Active Directory-Verwaltungscenter

1.  Öffnen Sie das **Active Directory-Verwaltungscenter**, klicken Sie auf **Authentifizierung**, klicken Sie mit der rechten Maustaste auf **Authentifizierungsrichtliniensilos**, klicken Sie auf **Neu** und anschließend auf **Authentifizierungsrichtliniensilo**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)

2.  Geben Sie unter **Anzeigename** einen Namen für den Silo ein. Klicken Sie unter **Erlaubte Konten** auf **Hinzufügen**, geben Sie die Namen der Konten ein und klicken Sie auf **OK**. Sie können Benutzer, Computer oder Dienstkonten angeben. Wählen Sie anschließend aus, ob Sie eine einzige Richtlinie für alle Prinzipale oder eine Richtlinie pro Prinzipal verwenden möchten, und geben Sie die Namen der Richtlinie(n) an.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)

### <a name="manage-authentication-policy-silos-by-using-windows-powershell"></a><a name="BKMK_ManageAuthnSilosUsingPSH"></a>Verwalten von Authentifizierungs Richtlinien Silos mithilfe von Windows PowerShell
Dieser Befehl erstellt und erzwingt ein Authentifizierungsrichtliniensilo-Objekt.

```
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce
```

Dieser Befehl ruft alle Authentifizierungsrichtliniensilos ab, die mit dem im **Filter**-Parameter angegebenen Filter übereinstimmen. Die Ausgabe wird anschließend an das **Format-Table**-Cmdlet weitergereicht, um den Namen der Richtlinie und den Wert für **Enforce** in den einzelnen Richtlinien anzuzeigen.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize

Name  Enforce
----  -------
silo     True
silos   False

```

Dieser Befehl verwendet das **Get-ADAuthenticationPolicySilo**-Cmdlet mit dem **Filter**-Parameter, um alle nicht erzwungenen Authentifizierungsrichtliniensilos abzurufen, die nicht erzwungen werden, und reicht das Ergebnis des Filters an das **Remove-ADAuthenticationPolicySilo**-Cmdlet weiter.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo
```

Dieser Befehl bietet Zugriff auf das Authentifizierungsrichtliniensilo mit dem Namen *Silo* für das Benutzerkonto mit dem Namen *User01*.

```
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01
```

Dieser Befehl entzieht den Zugriff auf das Authentifizierungsrichtliniensilo mit dem Namen *Silo* für das Benutzerkonto mit dem Namen *User01*. Da der Parameter **Confirm** mit **$False** angegeben ist, wird keine Bestätigungsmeldung angezeigt.

```
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False
```

Dieses Beispiel ruft zunächst das **Get-ADComputer**-Cmdlet auf, um alle Computerkonten abzurufen, die mit dem **Filter**-Parameter übereinstimmen. Anschließend wird die Ausgabe an **Set-ADAccountAuthenticatinPolicySilo** weitergereicht, um diesen Konten das Authentifizierungsrichtliniensilo mit dem Namen *Silo* und die Authentifizierungsrichtlinie mit dem Namen *AuthenticationPolicy02* zuzuweisen.

```
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02
```



