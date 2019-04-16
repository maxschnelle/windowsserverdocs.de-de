---
ms.assetid: 70c99703-ff0d-4278-9629-b8493b43c833
title: "Konfigurieren geschützter Konten"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4de7b1c9e3d12556f67c4515467bccd124e5e73e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="how-to-configure-protected-accounts"></a>Konfigurieren geschützter Konten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Über Pass-the-Hash (PtH)-Angriffe kann ein Angreifer mithilfe des zugrunde liegenden NTLM-Hashs des Kennworts eines Benutzers (oder anderer Teile der Anmeldeinformationen) auf einem Remoteserver oder Dienst authentifizieren. Microsoft hat bereits [veröffentlichte Anleitung](https://www.microsoft.com/download/details.aspx?id=36036) werden Pass-the-Hash-Angriffe.  Windows Server 2012 R2 umfasst neue Features, die bei solcher Angriffe weiter zu verringern. Weitere Informationen zu sonstigen Sicherheitsfeatures, die Schutz gegen den Diebstahl von Anmeldeinformationen finden Sie unter [Anmeldeinformationen Schutz und Verwaltung von](https://technet.microsoft.com/library/dn408190.aspx). In diesem Thema wird erläutert, wie so konfigurieren Sie die folgenden neuen Features:

-   [Geschützte Benutzer](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_AddtoProtectedUsers)

-   [Authentifizierungsrichtlinien](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicies)

-   [Authentifizierungsrichtliniensilos](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicySilos)

Es gibt zusätzliche Schutzmaßnahmen Windows 8.1 und Windows Server 2012 R2 zum Schutz vor Diebstahl von Anmeldeinformationen, die in den folgenden Themen behandelt werden:

-   [Eingeschränkter Administratormodus für Remote Desktop](http://blogs.technet.com/b/kfalde/archive/2013/08/14/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)

-   [LSA-Schutz](https://technet.microsoft.com/library/dn408187)

## <a name="BKMK_AddtoProtectedUsers"></a>Geschützte Benutzer
Geschützte Benutzer ist eine neue globale Sicherheitsgruppe, die Sie neue oder existierende Benutzer hinzufügen können. Windows 8.1-Geräte und Windows Server 2012 R2-Hosts haben spezielle Verhaltensweisen für Mitglieder dieser Gruppe um besseren Schutz gegen den Diebstahl von Anmeldeinformationen bereitzustellen. Für ein Mitglied der Gruppe zwischenspeichert ein Windows 8.1-Gerät oder Windows Server 2012 R2-Hosts nicht Anmeldeinformationen, die nicht für geschützte Benutzer unterstützt werden. Mitglieder dieser Gruppe haben keinen zusätzlichen Schutz, wenn sie auf einem Gerät angemeldet sind, die eine Windows-Version vor Windows 8.1 ausgeführt wird.

Mitglieder der geschützten Benutzer gruppieren, die für Windows 8.1-Geräte auf sind und Windows Server 2012 R2-Hosts können *nicht mehr* verwenden:

-   Delegierung der Standardanmeldeinformationen (CredSSP) - Klartext-Anmeldeinformationen werden nicht zwischengespeichert, selbst wenn die **zulassen der Delegierung von Standardanmeldeinformationen** Richtlinie aktiviert ist

-   Windows Digest - Klartext-Anmeldeinformationen nicht werden zwischengespeichert, selbst, wenn diese aktiviert sind

-   NTLM - NTOWF wird nicht zwischengespeichert.

-   Langfristig Kerberos-Schlüssel - Kerberos-Ticket-granting Ticket (TGT) wird bei der Anmeldung abgerufen und kann nicht automatisch erneut abgerufen werden

-   Einmaliges Anmelden ist offline - die zwischengespeicherte anmeldungsprüfung nicht erstellt

Wenn die Domänenfunktionsebene auf Windows Server 2012 R2 ist, können nicht mehr Mitglied der Gruppe:

-   Mithilfe der NTLM-Authentifizierung authentifizieren

-   Verwenden Sie Datenverschlüsselungsstandard (Data Encryption Standard, DES) oder RC4-Verschlüsselungssammlungen in Kerberos-Vorauthentifizierung

-   Delegieren per uneingeschränkter oder eingeschränkter Delegierung

-   Erneuern von Benutzertickets (TGTs) nach der ursprünglichen 4-stündigen Lebensdauer

Um Benutzer zur Gruppe hinzufügen möchten, können Sie [Benutzeroberflächentools](https://technet.microsoft.com/library/cc753515.aspx) z. B. Active Directory-Verwaltungscenter (ADAC) oder Active Directory-Benutzer und Computer oder ein Befehlszeilentool, z. B. [Dsmod Group](https://technet.microsoft.com/library/cc732423.aspx), oder die Windows PowerShell[Add-ADGroupMember](https://technet.microsoft.com/library/ee617210.aspx) Cmdlet. Konten für Dienste und Computer *sollten nicht* Mitglieder der Gruppe der geschützten Benutzer. Die Mitgliedschaft für diese Konten bietet keinen lokalen Schutz, da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist.

> [!WARNING]
> Die authentifizierungseinschränkungen können nicht umgangen werden, was bedeutet, dass Mitglieder der höher privilegierten Gruppen wie z. B. der Gruppe Organisations-Admins oder Domänen-Admins unterliegen denselben Einschränkungen wie andere Mitglieder der Gruppe der geschützten Benutzer sind. Wenn alle Mitglieder dieser Gruppen zur Gruppe geschützte Benutzer hinzugefügt werden, ist es möglich, dass alle diese Konten ausgesperrt werden. Sie sollten niemals alle höher privilegierte Konten zur Gruppe geschützte Benutzer hinzufügen, bis Sie die mögliche Auswirkungen gründlich getestet haben.

Mitglieder der Gruppe der geschützten Benutzer müssen mithilfe von Kerberos mit Standards AES (Advanced Encryption) authentifizieren können. Diese Methode erfordert die AES-Schlüssel für das Konto in Active Directory. Das integrierte Administratorkonto hat einen AES-Schlüssel keinen, es sei denn, das Kennwort wurde geändert wurden, auf einem Domänencontroller mit Windows Server 2008 oder höher. Darüber hinaus werden alle Konten mit einem Kennwort geschützt, die auf einem Domänencontroller geändert wurde, die eine frühere Version von Windows Server ausgeführt wird ist, gesperrt. Daher sollten Sie diese bewährten Methoden:

-   Testen Sie, sofern nicht in Domänen **allen Domänencontrollern WindowsServer 2008 oder höher ausführen**.

-   **Kennwort ändern** für alle Domänenkonten, die erstellt wurden *vor* die Domäne erstellt wurde. Andernfalls können nicht diese Konten nicht authentifiziert werden.

-   **Kennwort ändern** für jeden Benutzer vor dem Hinzufügen des Kontos zur der geschützten Benutzer gruppieren, oder stellen Sie sicher, dass das Kennwort wurde vor kurzem auf einem Domänencontroller, der Windows Server 2008 ausgeführt wird, geändert oder höher.

### <a name="BKMK_Prereq"></a>Anforderungen für die Verwendung geschützter Konten
Für geschützte Konten gelten die folgenden bereitstellungsanforderungen:

-   Um clientseitige Einschränkungen für geschützte Benutzer bereitzustellen, müssen die Hosts Windows 8.1 oder Windows Server 2012 R2 ausführen. Ein Benutzer muss nur mit einem Konto anmelden, das Mitglied der Gruppe geschützte Benutzer ist. In diesem Fall kann Gruppe der geschützten Benutzer erstellt werden, indem Sie [übertragen die Emulatorrolle primärer Domänencontroller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) auf einen Domänencontroller, der Windows Server 2012 R2 ausgeführt wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann der PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, die eine frühere Version von Windows Server ausgeführt wird.

-   Um Domain Controller-Seite-Einschränkungen für geschützte Benutzer, der zum Einschränken der Verwendung der NTLM-Authentifizierung, und andere Einschränkungen bereitzustellen, muss die Domänenfunktionsebene auf Windows Server 2012 R2. Weitere Informationen zu Funktionsebenen finden Sie unter [Grundlegendes zur Active Directory-Domänendienste (AD DS) Functional Levels](../active-directory-functional-levels.md).

### <a name="BKMK_TrubleshootingEvents"></a>Problembehandlung für Ereignisse im Zusammenhang mit geschützten Benutzern
In diesem Abschnitt behandelt neue Protokollereignisse zur Behandlung von Ereignissen, die im Zusammenhang mit geschützten Benutzern und wie geschützte Benutzer Änderungen an den beiden Ticket-granting Ticket (TGT)-Ablauf und Delegierungsproblemen Problembehandlung auswirken können.

#### <a name="new-logs-for-protected-users"></a>Neue Protokolle für geschützte Benutzer

Zwei neue operationalen administrationsprotokollen sind für die Behandlung von Ereignissen, die im Zusammenhang mit geschützten Benutzern zur Verfügung: geschützte Benutzer – Client-Protokoll und Fehler für geschützte Benutzer – Domänencontroller-Protokoll. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert. Um ein Protokoll zu aktivieren, klicken Sie auf **Anwendungs- und Dienstprotokolle**, klicken Sie auf **Microsoft**, klicken Sie auf **Windows**, klicken Sie auf **Authentifizierung**, und klicken Sie dann auf den Namen des Protokolls und klicken Sie auf **Aktion** (oder mit der rechten Maustaste in des Protokolls), und klicken Sie auf **Protokoll aktivieren**.

Weitere Informationen zu Ereignissen in diesen Protokollen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx).

#### <a name="troubleshoot-tgt-expiration"></a>Problembehandlung bei TGT-Ablauf
Normalerweise legt der Domänencontroller die TGT-Lebensdauer und-Erneuerung anhand der Domänenrichtlinie festgelegt, wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster dargestellt.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

Für **geschützte Benutzer**, sind folgende Einstellungen hartcodiert:

-   Max. Gültigkeitsdauer des Benutzertickets: 240 Minuten

-   Max. Zeitraum für die Erneuerung von Benutzertickets: 240 Minuten

#### <a name="troubleshoot-delegation-issues"></a>Problembehandlung für delegierungsprobleme
Zuvor, wenn eine Technologie, die Kerberos-Delegierung ein Fehler war, das Konto wurde daraufhin überprüft, ob **Konto ist vertraulich und kann nicht delegiert werden** festgelegt wurde. Allerdings ist das Konto Mitglied der **geschützte Benutzer**, ist diese Einstellung in Active Directory-Verwaltungscenter (ADAC) konfiguriert ist. Überprüfen Sie daher die Einstellung und die Gruppenmitgliedschaft bei der Problembehandlung von Delegierungsproblemen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

### <a name="BKMK_AuditAuthNattempts"></a>Überwachen von Authentifizierungsversuchen
Authentifizierungsversuche für die Mitglieder explizit Überwachen der **geschützte Benutzer** Gruppe können Sie weiterhin Überwachungsereignisse im Sicherheitsprotokoll erfasst oder die Daten in den neuen operationalen administrationsprotokollen sammeln. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx)

### <a name="BKMK_ProvidePUdcProtections"></a>Bereitstellen von Schutzmaßnahmen für DC-Seite für Dienste und Computer
Konten für Dienste und Computer können keine Mitglieder sein **geschützte Benutzer**. In diesem Abschnitt wird erläutert, welche Domäne Schutzmaßnahmen für diese Konten angeboten werden können:

-   Ablehnen von NTLM-Authentifizierung: nur konfigurierbar über [NTLM-Sperrrichtlinien](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

-   Datenverschlüsselungsstandard (Data Encryption Standard, DES) in der Kerberos-vorabauthentifizierung ablehnen: akzeptieren Windows Server 2012 R2-Domänencontroller kein DES für Computerkonten, es sei denn, sie für DES konfiguriert sind, da jede mit Kerberos veröffentlichte Windows-Version auch RC4 unterstützt.

-   Ablehnen von RC4 Kerberos-vorabauthentifizierung: nicht konfigurierbar.

    > [!NOTE]
    > Obwohl es möglich ist, [ändern Sie die Konfiguration unterstützter Verschlüsselungstypen](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx), es wird nicht empfohlen, diese Einstellungen für Computerkonten ändern, ohne in der zielumgebung zu testen.

-   Einschränken von Benutzertickets (TGTs), eine ursprüngliche 4-stündige Lebensdauer: Verwenden von Authentifizierungsrichtlinien.

-   Sperren der Delegierung per uneingeschränkter oder eingeschränkter Delegierung: Wenn Sie ein Konto einzuschränken, öffnen Sie Active Directory-Verwaltungscenter (ADAC), und wählen Sie die **Konto ist vertraulich und kann nicht delegiert werden** Kontrollkästchen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

## <a name="BKMK_CreateAuthNPolicies"></a>Authentifizierungsrichtlinien
Authentifizierungsrichtlinien sind ein neuer Container in AD DS, der authentifizierungsrichtlinienobjekte enthält. Authentifizierungsrichtlinien können Einstellungen angeben, mit deren Hilfe zu den Diebstahl von Anmeldeinformationen, z. B. Einschränkung der TGT-Lebensdauer für Konten oder andere Bedingungen hinzufügen zu verringern.

In Windows Server 2012 eingeführte dynamische Zugriffssteuerung eine Active Directory-Gesamtstruktur-Bereich Objektklasse, die Namen zentrale Zugriffsrichtlinie aus, um eine einfache Möglichkeit zum Konfigurieren von Dateiservern in der gesamten Organisation bereitzustellen. In Windows Server 2012 R2 kann eine neue Objektklasse mit dem Namen Authentifizierungsrichtlinie (ObjectClass MsDS-AuthNPolicies) verwendet werden, um die Authentifizierungskonfiguration auf Kontoklassen in Domänen mit Windows Server 2012 R2 gelten. Active Directory-Konto-Klassen sind:

-   Benutzer

-   Computer

-   Verwaltete Dienstkonten und Gruppenverwalteten Dienstkontos (GMSA)

### <a name="quick-kerberos-refresher"></a>Kurze Kerberos-Auffrischung
Das Kerberos-Authentifizierungsprotokoll besteht aus drei Austauschtypen, auch bekannt als Unterprotokolle:

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbRefresher.gif)

-   Der Authentifizierungsdienstaustausch (AS) (KRB_AS_ *)

-   Der Ticket-Granting Service (TGS)-Austausch (krb_as_ *)

-   Der Client/Server (AP)-Austausch (KRB_AP_ *)

Der AS-Austausch ist, bei denen der Client Kennwort des Kontos oder den privaten Schlüssel verwendet, um einen vorab-Authentifikator zum Anfordern einer Ticket granting Ticket (TGT) zu erstellen. Dies erfolgt bei der Benutzeranmeldung oder beim ersten, die ein Dienstticket benötigt wird.

Beim TGS-Austausch ist, in dem TGT des Kontos verwendet wird, erstellen Sie einen Authentifikator um ein Dienstticket anzufordern. Dies geschieht, wenn eine authentifizierte Verbindung benötigt wird.

Der AP-Austausch erfolgt normalerweise in Form von Daten innerhalb des Anwendungsprotokolls und wird nicht von Authentifizierungsrichtlinien beeinflusst.

Ausführlichere Informationen finden Sie unter [wie die Kerberos Version 5-Authentifizierungsprotokolls](https://technet.microsoft.com/library/cc772815(v=WS.10).aspx).

### <a name="overview"></a>(Übersicht)
Authentifizierungsrichtlinien bieten geschützten Benutzern die Möglichkeit, konfigurierbare Einschränkungen für Konten einzurichten und bieten außerdem Einschränkungen für Konten für Dienste und Computer. Authentifizierungsrichtlinien werden während der AS-Austausch oder der TGS erzwungen Exchange.

Sie können durch Konfigurieren von anfänglichen Authentifizierung oder den AS-Austausch einschränken:

-   Eine TGT-Lebensdauer

-   Zugriffssteuerungsbedingungen, Benutzer anmelden, beschränken, die von Geräten erfüllt werden müssen, von denen der AS-Austausch stammt

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictAS.gif)

Sie können Dienstticket-Anfragen über einen Austausch der Ticket-granting Service (TGS) einschränken, durch konfigurieren:

-   Zugriffssteuerungsbedingungen der vom Client (Benutzer, Dienst, Computer) erfüllt werden müssen oder ein Gerät, von dem der TGS-Austausch, stammt

### <a name="BKMK_ReqForAuthnPolicies"></a>Anforderungen für die Verwendung von Authentifizierungsrichtlinien

|Richtlinie|Anforderungen|
|----------|----------------|
|Geben Sie benutzerdefinierte TGT-Lebensdauer| Windows Server 2012 R2-Domäne funktionale Kontodomänen|
|Benutzeranmeldung beschränken|– Windows Server 2012 R2-Domäne funktionale Kontodomänen mit Unterstützung für dynamische Zugriffssteuerung<br />– Support Windows 8, Windows 8.1, Windows Server 2012 oder Windows Server 2012 R2-Geräte mit der dynamischen Zugriffssteuerung|
|Einschränken der Dienstticket-Ausstellung, die auf Benutzer und Sicherheitsgruppen Gruppen basiert| Windows Server 2012 R2-Domäne funktionale Ressourcendomänen|
|Einschränken der Dienstticket-Ausstellung basierend auf Benutzer- oder Gerätekonto, Sicherheitsgruppen oder Ansprüchen| Windows Server 2012 R2-Domäne funktionale Ressourcendomänen mit Unterstützung für dynamische Zugriffssteuerung|

### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>Einschränken von Benutzerkonten mit bestimmten Geräten und hosts
Eine besonders wichtige Konten mit Administratorrechten sollte ein Mitglied der **geschützte Benutzer** Gruppe. Standardmäßig sind keine Benutzerkonten Mitglieder der **geschützte Benutzer** Gruppe. Bevor Sie Konten zur Gruppe hinzufügen, Domänencontroller-Unterstützung konfigurieren und Erstellen einer Überwachungsrichtlinie, um sicherzustellen, dass keine blockierenden Probleme vorliegen.

#### <a name="configure-domain-controller-support"></a>Konfigurieren der Domänencontroller-Unterstützung

Die Domäne des Benutzerkontos muss auf Windows Server 2012 R2-Domänenfunktionsebene (DFL) sein. Sicherzustellen, dass alle Domänencontroller sind Windows Server 2012 R2, und verwenden Sie Active Directory-Domänen und-Vertrauensstellungen auf [die DFL](https://technet.microsoft.com/library/cc753104.aspx) für Windows Server 2012 R2.

**Konfigurieren der Unterstützung für die dynamische Zugriffssteuerung**

1.  In der Standarddomänencontroller-Richtlinie, klicken Sie auf **aktiviert** aktivieren **(Key Distribution Center, KDC)-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring** unter Computerkonfiguration | Administrative Vorlagen | System | KDC.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)

2.  Klicken Sie unter **Optionen**, wählen Sie im Dropdown-Listenfeld **immer Ansprüche bereitstellen**.

    > [!NOTE]
    > **Unterstützt** kann auch konfiguriert werden, aber da ist die Domäne unter Windows Server 2012 R2 DFL, müssen die DCs immer Ansprüche bereitstellen, anspruchsbasierter Zugriff überprüft auftreten, wenn Ansprüche nicht bekannt sind und zum Herstellen der Ansprüche unterstützende Dienste hostet.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)

    > [!WARNING]
    > Konfigurieren von **Authentifizierungsanfragen** führt dazu, dass Authentifizierungsversuche von Betriebssystemen die Kerberos-hochrüstung, z. B. Windows 7 und früheren Betriebssystemen nicht unterstützt oder Betriebssystemen ab Windows 8 nicht explizit konfiguriert wurden zur Unterstützung.

#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>Erstellen von Benutzerkonten-Überwachung für die Authentifizierungsrichtlinie in ADAC

1.  Öffnen Sie Active Directory-Verwaltungscenter (ADAC).

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_OpenADAC.gif)

    > [!NOTE]
    > Der ausgewählte **Authentifizierung** -Knoten ist sichtbar für Domänen mit der Windows Server 2012 R2-Domänenfunktionsebene. Wenn der Knoten nicht angezeigt wird, versuchen Sie dann erneut mit einem Domänenadministratorkonto aus einer Domäne, die unter Windows Server 2012 R2-Domänenfunktionsebene ist.

2.  Klicken Sie auf **Authentifizierungsrichtlinien**, und klicken Sie dann auf **neu** um eine neue Richtlinie zu erstellen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)

    Authentifizierungsrichtlinien müssen einen Anzeigenamen ein und werden standardmäßig erzwungen.

3.  Klicken Sie zum Erstellen einer Richtlinie nur überwachen auf **nur richtlinieneinschränkungen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)

    Authentifizierungsrichtlinien werden basierend auf den Active Directory-Kontotyp angewendet. Eine einzige Richtlinie kann auf alle drei Kontotypen anwenden, durch Konfigurieren von Einstellungen für jeden Typ. Die folgenden Kontotypen:

    -   Benutzer

    -   Computer

    -   Verwaltete Dienstkonten und Gruppenverwaltete Dienstkonten

    Wenn Sie das Schema mit neuen Prinzipalen erweitert haben, die durch das Schlüsselverteilungscenter (KDC) verwendet werden kann, wird der neue Kontotyp über den nächstgelegenen abgeleiteten Kontotyp klassifiziert.

4.  Um eine TGT-Lebensdauer für Benutzerkonten zu konfigurieren, wählen Sie die **Geben Sie eine Ticket-Granting Ticket-Lebensdauer für Benutzerkonten** Kontrollkästchen, und geben Sie die Zeit in Minuten.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTLifetime.gif)

    Geben Sie z. B. Wenn Sie eine maximale TGT-Lebensdauer von 10 Stunden möchten, **600** wie dargestellt. Wenn keine TGT-Lebensdauer, dann konfiguriert ist ist das Konto Mitglied der **geschützte Benutzer** gruppieren, die TGT-Lebensdauer und-Erneuerung 4 Stunden ist. Andernfalls TGT-Lebensdauer und-Erneuerung die Domänenrichtlinie basieren auf wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster für eine Domäne mit Standardeinstellungen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

5.  Um das Benutzerkonto Geräte zu beschränken, klicken Sie auf **bearbeiten** Bedingungen zu definieren, die für das Gerät erforderlich sind.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)

6.  In der **Zugriffssteuerungsbedingungen bearbeiten** Fenster, klicken Sie auf **fügen Sie eine Bedingung**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCondition.png)

##### <a name="add-computer-account-or-group-conditions"></a>Computer Computerkonto- oder gruppenbedingungen hinzufügen

1.  Um Computerkonten oder Gruppen in der Dropdown-Liste zu konfigurieren, wählen Sie im Dropdown-Listenfeld **Member jedes** und ändern Sie in **Mitglied einer**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompMember.png)

    > [!NOTE]
    > Diese Zugriffssteuerung definiert die Bedingungen für das Gerät oder den Host, von dem der Benutzer sich anmeldet. In der Access-Steuerelement Terminologie ist das Computerkonto für das Gerät oder den Host der Benutzer, weshalb **Benutzer** ist die einzige Option.

2.  Klicken Sie auf **Elemente hinzufügen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddItems.png)

3.  Um die Objekttypen zu ändern, klicken Sie auf **Objekttypen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjects.gif)

4.  Klicken Sie zum Auswählen eines Computerobjekts in Active Directory auf **Computer**, und klicken Sie dann auf **OK**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)

5.  Geben Sie den Namen der Computer, die für Benutzer, und klicken Sie dann auf **Namen überprüfen**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)

6.  Klicken Sie auf OK, und erstellen Sie alle sonstigen Bedingungen für das Computerkonto.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddConditions.png)

7.  Wenn Sie fertig sind, klicken Sie dann auf **OK** und die definierten Bedingungen für das Computerkonto.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompDone.png)

##### <a name="add-computer-claim-conditions"></a>Computer-anspruchsbedingungen hinzufügen

1.  Um computeransprüche zu konfigurieren, Dropdown-Gruppe, um den Anspruch auszuwählen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaim.gif)

    Ansprüche sind nur verfügbar, wenn sie bereits in der Gesamtstruktur bereitgestellt werden.

2.  Geben Sie den Namen der Organisationseinheit, die das Benutzerkonto anmelden eingeschränkt werden soll.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimOUName.gif)

3.  Wenn abgeschlossen ist, klicken Sie dann auf OK, und zeigt das definierten Bedingungen zu.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimComplete.gif)

##### <a name="troubleshoot-missing-computer-claims"></a>Problembehandlung für fehlende computeransprüche
Wenn der Anspruch bereitgestellt wurde, aber es nicht verfügbar ist, es kann nur konfiguriert werden für **Computer** Klassen.

Angenommen Sie Authentifizierung basierend auf die Organisationseinheit (OU) beschränken möchten, von dem Computer, der bereits konfiguriert wurde, jedoch nur für **Computer** Klassen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictComputers.gif)

Wählen Sie für den Anspruch Benutzer anmelden auf dem Gerät eingeschränkt verfügbar sein, die **Benutzer** Kontrollkästchen.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)

#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>Einrichten eines Benutzerkontos mit Authentifizierungsrichtlinie in ADAC

1.  Von der **Benutzer** auf **Richtlinie**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicy.gif)

2.  Wählen Sie die **dieses Konto eine Authentifizierungsrichtlinie zuweisen** Kontrollkästchen.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)

3.  Wählen Sie dann die Authentifizierungsrichtlinie für den Benutzer gelten.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicySelect.png)

#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>Konfigurieren der dynamischen Zugriffssteuerung Unterstützung auf Geräten und hosts
Sie können TGT-Lebensdauer ohne dynamische Zugriffssteuerung (DAC) konfigurieren. DAC wird nur benötigt, Überprüfen von AllowedToAuthenticateFrom und allowedtoauthenticateto verwendet.

Aktivieren Sie mithilfe von Gruppenrichtlinien oder Editor für lokale Gruppenrichtlinien **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring** unter Computerkonfiguration | Administrative Vorlagen | System | Kerberos:

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)

### <a name="BKMK_TroubleshootAuthnPolicies"></a>Problembehandlung für Authentifizierungsrichtlinien

#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>Ermitteln der Konten, die eine Authentifizierungsrichtlinie direkt zugewiesen werden
Im Bereich Konten für die Authentifizierungsrichtlinie zeigt die Konten, die direkt auf die Richtlinie angewendet haben.

![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AccountsAssigned.gif)

#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Verwenden Sie die Fehler bei Authentifizierungsrichtlinien – Domänencontroller-Administrationsprotokoll
Ein neues **Fehler bei Authentifizierungsrichtlinien – Domänencontroller** Administrationsprotokoll unter **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **Authentifizierung** zum Ermitteln von Fehlern aufgrund von Authentifizierungsrichtlinien vereinfachen erstellt wurde. Das Protokoll ist standardmäßig deaktiviert. Um es zu aktivieren, mit der rechten Maustaste in den Namen des Protokolls, und klicken Sie auf **Protokoll aktivieren**. Die neuen Ereignisse sind sehr ähnlich im Inhalt der vorhandenen Kerberos-TGT und Diensttickets überwachen. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx).

### <a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Verwalten von Authentifizierungsrichtlinien mit Windows PowerShell
Dieser Befehl erstellt eine Authentifizierungsrichtlinie mit dem Namen **TestAuthenticationPolicy**. Die **UserAllowedToAuthenticateFrom** -Parameter gibt an, die Geräte, von dem Benutzer authentifizieren können, indem eine SDDL-Zeichenfolge in der Datei mit dem Namen SomeFile.txt an.

```
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl
```

Dieser Befehl ruft alle Authentifizierungsrichtlinien, die den Filterkriterien entsprechen, die die **Filter** Parameter angegeben.

```
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com

```

Dieser Befehl ändert die Beschreibung und die **UserTGTLifetimeMins** Eigenschaften der angegebenen Authentifizierungsrichtlinie.

```
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45
```

Dieser Befehl entfernt die Authentifizierungsrichtlinie, die die **Identität** Parameter angegeben.

```
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1
```

Dieser Befehl verwendet den **Get-ADAuthenticationPolicy** Cmdlet mit dem **Filter** Parameter, um alle Authentifizierungsrichtlinien abzurufen, die nicht erzwungen werden. Der Ergebnissatz ist über die Pipeline an das **Remove-ADAuthenticationPolicy** Cmdlet.

```
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy
```

## <a name="BKMK_CreateAuthNPolicySilos"></a>Authentifizierungsrichtliniensilos
Authentifizierungsrichtliniensilos ist ein neuer Container (ObjectClass MsDS-AuthNPolicySilos) in AD DS für Benutzer, Computer und Dienstkonten. Sie schützen hochwertige Konten möchten. Während alle Organisationen müssen Mitglieder der Gruppen Organisations-Admins, Domänen-Admins und Schema-Admins zu schützen, da diese Konten zum Zugreifen auf die Gesamtstruktur von einem Angreifer verwendet werden können, können andere Konten auch Schutz benötigen.

Einige Unternehmen isolieren die arbeitsauslastung durch das Erstellen von Konten, die speziell für sie und die Anwendung von gruppenrichtlinieneinstellungen lokal und remote interaktive Anmeldung und Administratorrechte beschränken. Authentifizierungsrichtliniensilos ergänzen diese Erstellen einer Möglichkeit, eine Beziehung zwischen Benutzern, Computern und verwalteten Dienstkonten zu definieren. Konten können nur zu einem Silo gehören. Sie können die Authentifizierungsrichtlinie für jede Art von Konto konfigurieren, um zu steuern:

1.  Nicht erneuerbare TGT-Lebensdauer

2.  Zugriff auf die Bedingungen für die Zugriffssteuerung für TGT (Hinweis: gilt nicht für Systeme, da Kerberos armoring erforderlich ist)

3.  Zugriffssteuerungsbedingungen zur Rückgabe von Diensttickets

Außerdem haben alle Konten in einem authentifizierungsrichtliniensilo einen siloanspruch, die zum Steuern des Zugriffs von Ansprüche unterstützende Ressourcen wie z. B. Dateiservern verwendet werden kann.

Eine neue Sicherheitsbeschreibung kann so konfiguriert werden, um zu steuern, die Ausgabe von Diensttickets basierend auf:

-   Benutzer, Benutzer Sicherheitsgruppen und/oder Benutzeransprüche

-   Gerät, Geräte Sicherheitsgruppen und/oder Geräteansprüche

Um diese Informationen für die Ressource Domänencontroller benötigen dynamische Zugriffssteuerung:

-   Benutzeransprüche:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Kontodomäne unterstützt dynamische Zugriffssteuerung und Ansprüche

-   Geräte- und/oder gerätesicherheitsgruppe:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Für Verbundauthentifizierung konfigurierte Ressource

-   Geräteansprüche:

    -   Windows 8 und neuere Clients unterstütze dynamische Zugriffssteuerung

    -   Gerätedomäne unterstützt dynamische Zugriffssteuerung und Ansprüche

    -   Für Verbundauthentifizierung konfigurierte Ressource

Authentifizierungsrichtlinien können für alle Mitglieder einer authentifizierungsrichtliniensilo statt an einzelne Konten angewendet werden, oder unterschiedliche Authentifizierungsrichtlinien können auf verschiedene Arten von innerhalb eines Silos angewendet werden. Z. B. eine Authentifizierungsrichtlinie kann sehr privilegierten Benutzerkonten angewendet werden, und eine andere Richtlinie Dienstkonten angewendet werden kann. Mindestens eine Authentifizierungsrichtlinie muss erstellt werden, bevor ein authentifizierungsrichtliniensilo erstellt werden kann.

> [!NOTE]
> Authentifizierungsrichtlinien kann Mitglieder der authentifizierungsrichtliniensilos angewendet werden, oder kann unabhängig von der Auswirkungen auf bestimmte Konten einzuschränken angewendet werden. Beispielsweise kann um ein einzelnes Konto oder eine kleine Gruppe von Konten zu schützen, eine Richtlinie für diese Konten festgelegt werden, ohne Hinzufügen von Konten zu einem Silo hinzuzufügen.

Sie können ein authentifizierungsrichtliniensilo erstellen, mithilfe von Active Directory-Verwaltungscenter oder Windows PowerShell. In der Standardeinstellung authentifizierungsrichtliniensilos nur silorichtlinien. dieses Verhalten entspricht dem Angeben der **WhatIf** Parameter in Windows PowerShell-Cmdlets. In diesem Fall gelten Einschränkungen für richtliniensilos gelten nicht, aber es werden Überwachungen generiert, um anzugeben, ob Fehler auftreten, wenn die Einschränkungen angewendet werden.

#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Um ein authentifizierungsrichtliniensilo erstellen Sie mithilfe von Active Directory-Verwaltungscenter

1.  Öffnen **Active Directory-Verwaltungscenter**, klicken Sie auf **Authentifizierung**, mit der rechten Maustaste **Authentifizierungsrichtliniensilos**, klicken Sie auf **neu**, und klicken Sie dann auf **Authentifizierungsrichtliniensilo**.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)

2.  In **Anzeigenamen**, geben Sie einen Namen für das Silo. In **erlaubte Konten**, klicken Sie auf **hinzufügen**, geben Sie die Namen der Konten ein, und klicken Sie dann auf **OK**. Sie können Benutzern, Computern oder Dienstkonten angeben. Geben Sie dann, ob Sie eine einzige Richtlinie für alle Prinzipale oder eine Richtlinie für jede Art von Prinzipal und den Namen der Richtlinie verwenden.

    ![geschützte Konten](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)

### <a name="BKMK_ManageAuthnSilosUsingPSH"></a>Verwalten von authentifizierungsrichtliniensilos mit Windows PowerShell
Mit diesem Befehl wird ein authentifizierungsrichtliniensilo-Objekt erstellt und erzwingt.

```
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce
```

Dieser Befehl ruft alle authentifizierungsrichtliniensilos, die den Filterkriterien, die vom angegebenen entsprechen der **Filter** Parameter. Die Ausgabe übergeben, die **Format-Table** -Cmdlet zum Anzeigen der Namen der Richtlinie und der Wert für **erzwingen** in den einzelnen Richtlinien.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize

Name  Enforce
----  -------
silo     True
silos   False

```

Dieser Befehl verwendet den **Get-ADAuthenticationPolicySilo** Cmdlet mit dem **Filter** Parameter, um alle authentifizierungsrichtliniensilos, die nicht erzwungen werden und reicht das Ergebnis des Filters an die **Remove-ADAuthenticationPolicySilo** Cmdlet.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo
```

Dieser Befehl bietet Zugriff auf das authentifizierungsrichtliniensilo mit dem Namen *Silo* für das Benutzerkonto mit dem Namen *User01*.

```
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01
```

Dieser Befehl entzieht den Zugriff auf das authentifizierungsrichtliniensilo mit dem Namen *Silo* für das Benutzerkonto mit dem Namen *User01*. Da die **bestätigen** -Parameters **$False**, keine bestätigungsmeldung angezeigt.

```
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False
```

Dieses Beispiel ruft zunächst die **Get-ADComputer** Cmdlet, um alle Computerkonten abzurufen, die den Filterkriterien entsprechen, die die **Filter** Parameter angegeben. Die Ausgabe dieses Befehls wird übergeben, um **Set-ADAccountAuthenticatinPolicySilo** , weisen Sie das authentifizierungsrichtliniensilo mit dem Namen *Silo* und die Authentifizierungsrichtlinie mit dem Namen *AuthenticationPolicy02* werden.

```
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02
```



