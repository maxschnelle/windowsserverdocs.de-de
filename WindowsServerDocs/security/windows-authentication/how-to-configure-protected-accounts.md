---
title: Konfigurieren geschützter Benutzerkonten
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 28296b588c87bddb0364b9c3e10ad443870dc52f
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266826"
---
# <a name="how-to-configure-protected-accounts"></a>Konfigurieren geschützter Benutzerkonten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bei Pass-the-hash (PtH)-Angriffen können Angreifer den zugrunde liegenden NTLM-Hash eines Benutzerkennworts (oder anderer Teile der Anmeldeinformationen) verwenden, um sich bei einem Remote-Server zu authentifizieren. Microsoft hat bereits [Anleitungen veröffentlicht](https://www.microsoft.com/download/details.aspx?id=36036) um Pass-the-Hash-Angriffen zu verringern.  Windows Server 2012 R2 enthält neue Features, um solcher Angriffe weiter zu verringern. Weitere Informationen zu sonstigen Sicherheitsfeatures, die Schutz vor Diebstahl von Anmeldeinformationen finden Sie unter [Anmeldeinformationen Schutz und Verwaltung von](https://technet.microsoft.com/library/dn408190.aspx). Dieser Artikel beschreibt die Konfiguration der folgenden neuen Features:  
  
-   [Geschützte Benutzer](#protected-users)  
  
-   [Authentifizierungsrichtlinien](#authentication-policies)  
  
-   [Authentifizierungsrichtliniensilos](#authentication-policy-silos)  
  
Windows 8 und Windows Server 2012 R2 enthalten zusätzliche Schutzmaßnahmen gegen den Diebstahl von Anmeldeinformationen. Lesen Sie dazu die folgenden Artikel:  
  
-   [Eingeschränkter Administratormodus für Remote Desktop](http://blogs.technet.com/b/kfalde/archive/20../restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)  
  
-   [LSA-Schutzes](https://technet.microsoft.com/library/dn408187)  
  
## <a name="protected-users"></a>Geschützte Benutzer  
Geschützte Benutzer ist eine neue globale Sicherheitsgruppe, zu der Sie neue oder existierende Benutzer hinzufügen können. Windows 8.1-Geräte und Windows Server 2012 R2-Hosts weisen ein besonderes Verhalten mit Mitgliedern dieser Gruppe um besseren Schutz vor Diebstahl von Anmeldeinformationen bereitzustellen. Für ein Mitglied der Gruppe ist ein Windows 8.1-Gerät oder Windows Server 2012 R2-Host keine Anmeldeinformationen zwischenspeichern, die nicht für geschützte Benutzer unterstützt werden. Mitglieder dieser Gruppe haben keinen zusätzlichen Schutz, wenn sie auf einem Gerät angemeldet sind, die eine Version von Windows vor Windows 8.1 ausgeführt wird.  
  
Mitglieder der geschützten Benutzer, die bei Windows 8.1-Geräte anmelden werden-Gruppe und Windows Server 2012 R2-Hosts können *mehr* verwenden:  
  
-   Delegierung der Standardanmeldeinformationen (CredSSP) - Klartext-Anmeldeinformationen werden auch dann nicht zwischensgespeichert, wenn die Richtlinie **Delegierung von Standardanmeldeinformationen zulassen** aktiviert ist  
  
-   Windows Digest - Klartext-Anmeldeinformationen werden auch dann nicht zwischengespeichert, wenn diese aktiviert sind  
  
-   NTLM - NTOWF wird nicht zwischengespeichert  
  
-   Langfristig gültige Kerberos-Schlüssel - Kerberos Ticket Granting ticket (TGT) wird bei der Anmeldung abgerufen und kann nicht automatisch erneut abgerufen werden  
  
-   Offlineanmeldung - die zwischengespeicherte Anmeldungsprüfung wird nicht erstellt  
  
Wenn die Domänenfunktionsebene auf Windows Server 2012 R2 ist, können nicht mehr Mitglied der Gruppe:  
  
-   Authentifizierung per NTLM  
  
-   Datenverschlüsselungssstandard (DES) oder RC4- Verschlüsselungssammlungen in der Kerberos-Vorabauthentifizierung  
  
-   Delegieren per uneingeschränkter oder eingeschränkter Delegierung  
  
-   Erneuern von Benutzertickets (TGTs) jenseits der ursprünglichen 4-stündigen Lebensdauer  
  
Um Benutzer zur Gruppe hinzuzufügen, können Sie [Benutzeroberflächentools](https://technet.microsoft.com/library/cc753515.aspx) wie Active Directory-Verwaltungscenter (ADAC) oder Active Directory-Benutzer und Computer oder ein Befehlszeilentool wie z. B. [Dsmod Group](https://technet.microsoft.com/library/cc732423.aspx), oder die Windows PowerShell [Add-ADGroupMember](https://technet.microsoft.com/library/ee617210.aspx) Cmdlet. Konten für Dienste und Computer *sollten nicht* Mitglieder der Benutzergruppe Geschützte Benutzer sein. Die Mitgliedschaft bietet für diese Konten keinen lokalen Schutz, da Kennwort bzw. Zertifikat auf dem Host immer verfügbar sind.  
  
> [!WARNING]  
> Die Authentifizierungseinschränkungen können nicht umgangen werden, d. h. Mitglieder der höher privilegierten Gruppen wie z. B. Unternehmens-Admins oder Domänen-Admins unterliegen denselben Einschränkungen wie andere Mitglieder der Gruppe Geschützte Benutzer. Wenn alle Mitglieder dieser Gruppen zur Gruppe Geschützte Benutzer hinzugefügt werden, kann es passieren, dass all diese Konten ausgesperrt werden. Sie sollten niemals alle höher privilegierten Konten zur Gruppe Geschützte Benutzer hinzufügen, ohne die möglichen Auswirkungen gründlich getestet zu haben.  
  
Mitglieder der Gruppe Geschützte Benutzer müssen in der Lage sein, sich mit dem erweiterten Verschlüsselungsstandard (AES) und Kerberos anzumelden. Für diese Methode sind AES-Schlüssel in Active Directory erforderlich. Das integrierte Administratorkonto muss einen AES-Schlüssel nicht, es sei denn, das Kennwort wurde geändert, auf einem Domänencontroller mit Windows Server 2008 oder höher. Außerdem werden alle Konten mit Kennwörtern, die auf einem Domänencontroller unter älteren Windows Server-Versionen geändert wurden, ausgesperrt. Daher sollten Sie diese bewährten Methoden umsetzen:  
  
-   Testen Sie, sofern nicht in Domänen **alle Domänencontroller unter WindowsServer ausgeführt, 2008 oder höher**.  
  
-   **Ändern Sie die Kennwörter** aller Domänenkonten, die *vor* der Domänenerstellung erstellt wurden. Andernfalls können sich diese Konten nicht mehr authentifizieren.  
  
-   **Ändern von Kennwörtern** für jeden Benutzer vor dem Hinzufügen des Kontos auf der geschützten Benutzer gruppieren, oder stellen Sie sicher, dass das Kennwort wurde vor kurzem auf einem Domänencontroller, die Windows Server 2008 ausgeführt wird, geändert oder höher.  
  
### <a name="requirements-for-using-protected-accounts"></a>Anforderungen für die Verwendung geschützter Konten  
Für geschützte Konten gelten die folgenden Bereitstellungsanforderungen:  
  
-   Um clientseitige Einschränkungen für geschützte Benutzer bereitzustellen, müssen die Hosts mit Windows 8.1 oder Windows Server 2012 R2 ausführen. Benutzer müssen sich nur mit einem Konto anmelden, das Mitglied der Gruppe Geschützte Benutzer ist. In diesem Fall für die Gruppe der geschützten Benutzer erstellt werden kann, von [übertragen die Emulatorrolle primärer Domänencontroller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) zu einem Domänencontroller, die Windows Server 2012 R2 ausgeführt wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann die PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, der unter einer älteren Windows Server-Version läuft.  
  
-   Um die Domäne domänencontrollerseitige Einschränkungen für geschützte Benutzer, der zum Einschränken der Verwendung der NTLM-Authentifizierung ist, und andere Einschränkungen zu ermöglichen, muss die Domänenfunktionsebene auf Windows Server 2012 R2 sein. Weitere Informationen zu Funktionsebenen finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../../identity/ad-ds/active-directory-functional-levels.md).  
  
### <a name="troubleshoot-events-related-to-protected-users"></a>Problembehandlung für Ereignisse im Zusammenhang mit geschützten Benutzern  
Dieser Abschnitt behandelt neue Protokollereignisse im Zusammenhang mit geschützten Benutzern und die Möglichkeiten von geschützten Benutzern für die Problembehandlung von Ticket Granting Ticket (TGT)-Ablauf und Delegierungsproblemen.  
  
#### <a name="new-logs-for-protected-users"></a>Neue Protokolle für geschützte Benutzer  
Zwei neue Administrationsprotokolle helfen bei der Problembehandlung von Ereignissen im Zusammenhang mit geschützten Benutzern: Geschützte Benutzer – Client-Protokoll und Fehler bei geschützten Benutzern – Domänencontroller-Protokoll. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert. Um ein Protokoll zu aktivieren, klicken Sie auf **Anwendungs- und Dienstprotokolle**, klicken Sie auf **Microsoft**, dann auf **Windows**, auf **Authentifizierung**. Klicken Sie anschließend auf den Namen des Protokolls und klicken Sie auf **Aktion** (bzw. klicken Sie mit der rechten Maustaste auf das Protokoll) und klicken Sie auf **Protokoll aktivieren**.  
  
Weitere Informationen zu Ereignissen in diesen Protokollen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx).  
  
#### <a name="troubleshoot-tgt-expiration"></a>Problembehandlung für den TGT-Ablauf  
Normalerweise legt der Domänencontroller die TGT-Lebensdauer und -Erneuerung anhand der Domänenrichtlinie fest, wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster gezeigt.  
  
![Screenshot des Fensters Gruppenrichtlinienverwaltungs-Editor zeigt, wie der Domänencontroller die TGT-Lebensdauer und-Erneuerung anhand der Domänenrichtlinie festlegt](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
Für **Geschützte Benutzer** sind die folgenden Einstellungen hartcodiert:  
  
-   Max. Gültigkeitsdauer für Benutzertickets: 240 Minuten  
  
-   Max. Zeitraum für die Erneuerung von Benutzertickets: 240 Minuten  
  
#### <a name="troubleshoot-delegation-issues"></a>Problembehandlung für Delegierungsprobleme  
Bislang wurde bei Fehlern in Technologien mit Kerberos-Delegierung geprüft, ob die Option **Konto ist vertraulich und kann nicht delegiert werden** für das Clientkonto gesetzt ist. Wenn das Konto jedoch Mitglied der Gruppe **Geschützte Benutzer** ist, kann es jedoch sein, dass diese Einstellung im Active Directory-Verwaltungscenter (ADAC) nicht gesetzt ist. Daher sollten Sie bei der Problembehandlung von Delegierungsproblemen diese Einstellung und die Gruppenmitgliedschaft prüfen.  
  
![Screenshot zur überprüfen ** Konto ist vertraulich und kann nicht delegiert werden ** UI-Element](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
### <a name="audit-authentication-attempts"></a>Überwachen von Authentifizierungsversuchen  
Um Authentifizierungsversuche speziell für Mitglieder der Gruppe **Geschützte Benutzer** zu überwachen, können Sie weiterhin Überwachungsereignisse im Sicherheitslog sammeln oder die Daten in den neuen operationalen Administrationsprotokollen sammeln. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx).  
  
### <a name="provide-dc-side-protections-for-services-and-computers"></a>Domänencontrollerseitiger Schutz für Dienste und Computer  
Konten für Dienste und Computer dürfen nicht Mitglieder der Benutzergruppe **Geschützte Benutzer** sein. Dieser Abschnitt beschreibt die möglichen domänencontrollerseitigen Schutzmaßnahmen für diese Konten:  
  
-   Ablehnen von NTLM-Authentifizierung: Nur konfigurierbar über [NTLM Block Richtlinien](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx).  
  
-   Datenverschlüsselungssstandard (DES) in der Kerberos-Vorabauthentifizierung ablehnen:  Windows Server 2012 R2-Domänencontroller akzeptieren keine DES für Computerkonten, es sei denn, sie für DES konfiguriert sind, nur, weil jede mit Kerberos veröffentlichte Windows-Version auch RC4 unterstützt.  
  
-   Ablehnen von RC4 für die Kerberos-Vorabauthentifizierung: nicht konfigurierbar.  
  
    > [!NOTE]  
    > Obwohl es möglich ist, [ändern Sie die Konfiguration unterstützter Verschlüsselungstypen](http://blogs.msdn.com/b/openspecification/archive/20../windows-configurations-for-kerberos-supported-encryption-type.aspx), es wird nicht empfohlen, diese Einstellungen für Computerkonten zu ändern, ohne Sie in der zielumgebung zu testen.  
  
-   Einschränken von Benutzertickets (TGTs) auf die ursprüngliche 4-stündige Lebensdauer: Verwenden Sie Authentifizierungsrichtlinien.  
  
-   Sperren der Delegierung per uneingeschränkter oder eingeschränkter Delegierung: Um ein Konto einzuschränken, öffnen Sie das Active Directory-Verwaltungscenter und markieren Sie das Kontrollkästchen **Konto ist vertraulich und kann nicht delegiert werden**.  
  
    ![Screenshot, der anzeigt, wo Sie ein Konto einzuschränken](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
## <a name="authentication-policies"></a>Authentifizierungsrichtlinien  
Authentifizierungsrichtlinien sind ein neuer Container in AD DS, der Authentifizierungsrichtlinienobjekte enthält. Authentifizierungsrichtlinien enthalten Einstellungen zur Vermeidung des Diebstahls von Anmeldeinformationen, wie z. B. Einschränkung der TGT-Lebensdauer für Konten oder zusätzliche anspruchsrelevante Bedingungen.  
  
In Windows Server 2012 eingeführt Dynamic Access Control für eine Active Directory-Gesamtstruktur-Scope-Objektklasse, die Namen zentrale Zugriffsrichtlinie, um eine einfache Möglichkeit zum Konfigurieren von Dateiservern in der gesamten Organisation bereitzustellen. In Windows Server 2012 R2 kann eine neue Objektklasse mit dem Namen Authentifizierungsrichtlinie (ObjectClass MsDS-AuthNPolicies) verwendet werden, um die Authentifizierungskonfiguration auf Kontoklassen in Windows Server 2012 R2-Domänen anwenden. Es existieren die folgenden Active Directory-Kontoklassen:  
  
-   Benutzer  
  
-   Computer  
  
-   Verwaltete Dienstkonten und Gruppenverwaltete Dienstkonten (GMSA)  
  
### <a name="quick-kerberos-refresher"></a>Kurze Kerberos-Auffrischung  
Das Kerberos-Authentifizierungsprotokoll besteht aus drei Austauschtypen, auch bekannt als Unterprotokolle:  
  
![Screenshot mit den drei Arten von Kerberos-Authentifizierung Protokoll Austauschtypen, auch bekannt als Unterprotokolle](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbRefresher.gif)  
  
-   Der Authentifizierungsdienst (AS)-Austausch (KRB_AS_*)  
  
-   Der Ticket-Granting Service (TGS)-Austausch (KRB_AS_*)  
  
-   Der Client/Server (AP)-Austausch (KRB_AP_*)  
  
Der AS-Austausch ist, in dem der Client das Kennwort des Kontos oder der private Schlüssel verwendet, um einen vorab-Authentifikator zum Anfordern einer Ticket granting Ticket (TGT) erstellen. Dies erfolgt bei der Benutzeranmeldung oder beim ersten Mal, wenn ein Dienstticket benötigt wird.  
  
Beim TGS-Austausch ist, in denen des Kontos TGT verwendet wird, erstellen Sie einen Authentifikator um ein Dienstticket anzufordern. Dies erfolgt, wenn eine authentifizierte Verbindung benötigt wird.  
  
Der AP-Austausch erfolgt normalerweise in Form von Daten innerhalb des Anwendungsprotokolls und wird nicht von Authentifizierungsrichtlinien beeinflusst.  
  
Weitere Informationen finden Sie unter [Funktionsweise des Kerberos Version 5 Authentication-Protokoll](https://technet.microsoft.com/library/cc772815(v=WS.10.aspx)).  
  
### <a name="overview"></a>Übersicht  
Authentifizierungsrichtlinien bieten geschützten Benutzern die Möglichkeit, konfigurierbare Einschränkungen für Konten einzurichten und bieten außerdem Einschränkungen für Dienst- und Computerkonten. Authentifizierungsrichtlinien werden entweder beim AS- oder beim TGS-Austausch umgesetzt.  
  
Sie können die ursprüngliche Authentifizierung oder den AS-Austausch einschränken, indem Sie Folgendes konfigurieren:  
  
-   Eine TGT-Lebensdauer  
  
-   Bedingungen für die Zugriffssteuerung zum Einschränken der Benutzeranmeldung. Die Geräte, von denen der AS-Austausch stammt, müssen diese Bedingungen erfüllen  
  
![Screenshot der anfänglichen Authentifizierung zu beschränken, durch Konfigurieren der ein TGT Lebensdauer und den Zugriff steuern der Bedingungen Benutzeranmeldung beschränken](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictAS.gif)  
  
Sie können Dienstticket-Anfragen über den Ticket-Granting Service (TGS) einschränken, indem Sie Folgendes konfigurieren:  
  
-   Bedingungen für die Zugriffssteuerung, die vom Client (Benutzer, Dienst, Computer) bzw. vom Gerät erfüllt werden müssen, von dem der TGS-Austausch stammt  
  
### <a name="requirements-for-using-authentication-policies"></a>Anforderungen für die Verwendung von Authentifizierungsrichtlinien  
  
|Richtlinie|Anforderungen|  
|-----|--------|  
|Benutzerdefinierte TGT-Lebensdauer| Windows Server 2012 R2 Domäne funktionale Kontodomänen|  
|Benutzeranmeldung beschränken|– Windows Server 2012 R2 Domäne funktionale Kontodomänen dynamische Zugriffssteuerung unterstützen.<br />-Windows 8, Windows 8.1, Windows Server 2012 oder Windows Server 2012 R2-Geräte mit der dynamischen Zugriffssteuerung zu unterstützen.|  
|Einschränken der Dienstticket-Ausstellung auf Basis von Benutzerkonten und Sicherheitsgruppen| Windows Server 2012 R2 Domäne funktionale Ressourcendomänen|  
|Einschränken der Dienstticket-Ausstellung auf Basis von Benutzeransprüchen, Gerätekonten, Sicherheitsgruppen oder Ansprüchen| Windows Server 2012 R2 Domäne funktionale Ressourcendomänen dynamische Zugriffssteuerung unterstützen.|  
  
### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>Einschränken von Benutzerkonten auf bestimmte Geräte und Hosts  
Besonders wichtige Konten mit Administratorrechten sollten Mitglieder der Gruppe **Geschützte Benutzer** sein. Standardmäßig sind keine Benutzerkonten Mitglieder der Gruppe **Geschützte Benutzer**. Bevor Sie Konten zur Gruppe hinzufügen, sollten Sie die Domänencontroller-Unterstützung konfigurieren und eine Überwachungsrichtlinie erstellen, um sicherzugehen, dass keine blockierenden Probleme vorliegen.  
  
#### <a name="configure-domain-controller-support"></a>Konfigurieren der Domänencontroller-Unterstützung  
Windows Server 2012 R2-Domänenfunktionsebene (DFL) muss der Domäne des Benutzerkontos aufweisen. Sicherzustellen, dass alle Domänencontroller sind Windows Server 2012 R2, und verwenden Sie Active Directory-Domänen und Vertrauensstellungen, um [die DFL](https://technet.microsoft.com/library/cc753104.aspx) zu Windows Server 2012 R2.  
  
**Konfigurieren der Unterstützung für die dynamische Zugriffssteuerung**  
  
1.  Klicken Sie in der Standard-Domänencontrollerrichtlinie auf **Aktiviert**, um **die Clientunterstützung für das Schlüsselverteilungscenter (Key Distribution Center KDC) für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** unter Computerkonfiguration | Administrative Vorlagen | System | KDC zu aktivieren.  
  
    ![In der Standarddomänencontroller-Richtlinie, klicken Sie auf ** aktiviert ** aktivieren ** Schlüsselverteilungscenter (Key Distribution Center, KDC)-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring ** unter Computerkonfiguration | Administrative Vorlagen | System | KDC](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)  
  
2.  Wählen Sie unter **Optionen** im Dropdown-Listenfeld den Wert **Immer Ansprüche bereitstellen** aus.  
  
    > [!NOTE]  
    > **Unterstützt** kann auch konfiguriert werden, aber weil die Domäne auf Windows Server 2012 R2 Domänenfunktionsebene, müssen die DCs immer geben Ansprüche können Benutzer anspruchsbasierter Zugriff überprüft auftreten, wenn nicht anspruchsbasierten-fähigen Geräte und Hosts für die Verbindung Ansprüche unterstützende Dienste.  
  
    ![Klicken Sie unter ** Optionen **, in der Dropdown-Listenfeld auswählen ** immer Ansprüche bereitstellen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)  
  
    > [!WARNING]  
    > Konfigurieren von **; Fehler bei authentifizierungsanforderungen ohne Armor** führt zu Authentifizierungsfehlern aus einem anderen Betriebssystem, das Kerberos-hochrüstung, z. B. Windows 7 und früheren Betriebssystemen oder den Einsatz der nicht unterstützt Systeme, beginnend mit Windows 8, die nicht explizit konfiguriert wurden, die sie unterstützen.  
  
#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>Erstellen von Benutzerkonten-Überwachung für die Authentifizierungsrichtlinie im ADAC  
  
1.  Öffnen Sie das Active Directory-Verwaltungscenter (ADAC).  
  
    ![Screenshot der Active Directory-Verwaltungscenter](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_OpenADAC.gif)  
  
    > [!NOTE]  
    > Die ausgewählte **Authentifizierung** -Knoten ist sichtbar für Domänen mit der Windows Server 2012 R2-Domänenfunktionsebene. Wenn der Knoten nicht angezeigt wird, wiederholen Sie dann mit einem Administratorkonto aus einer Domäne, die unter Windows Server 2012 R2-Domänenfunktionsebene ist.  
  
2.  Klicken Sie auf **Authentifizierungsrichtlinien** und auf **Neu**, um eine neue Richtlinie zu erstellen.  
  
    ![Authentifizierungsrichtlinien](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)  
  
    Authentifizierungsrichtlinien müssen einen Anzeigenamen haben und werden standardmäßig erzwungen.  
  
3.  Klicken Sie auf **Nur Richtlinieneinschränkungen überwachen**, um eine Richtlinie zur reinen Überwachung zu erstellen.  
  
    ![Nur richtlinieneinschränkungen überwachen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)  
  
    Authentifizierungsrichtlinien werden auf Basis des Active Directory-Kontotyps angewendet. Sie können eine einzige Richtlinie für alle drei Kontotypen anwenden, indem Sie die Einstellungen für die einzelnen Typen konfigurieren. Es existieren die folgenden Kontotypen:  
  
    -   Benutzer  
  
    -   Computer  
  
    -   Verwaltete Dienstkonten und Gruppenverwaltete Dienstkonten  
  
    Falls Sie das Schema mit neuen Prinzipalen erweitert haben, die vom Schlüsselverteilungscenter (KDC) verwendet werden können, wird der neue Kontotyp über den nächstgelegenen abgeleiteten Kontotyp bestimmt.  
  
4.  Um eine TGT-Lebensdauer für Benutzerkonten zu konfigurieren, markieren Sie das Kontrollkästchen **Ticket Granting Ticket-Lebensdauer für Benutzerkonten angeben** und geben Sie die Lebensdauer in Minuten an.  
  
    ![Geben Sie eine Ticket Granting Ticket-Lebensdauer für Benutzerkonten](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTLifetime.gif)  
  
    Geben Sie z. B. wie gezeigt **600** für eine 10-stündige maximale TGT-Lebensdauer ein. Wenn keine TGT-Lebensdauer konfiguriert ist und das Konto Mitglied der Gruppe **Protected Users** ist, beträgt die TGT-Lebensdauer und -Erneuerung 4 Stunden. Ansonsten werden TGT-Lebensdauer und -Erneuerung anhand der Domänenrichtlinie festgelegt, wie im folgenden Gruppenrichtlinienverwaltungs-Editor-Fenster für eine Domäne mit Standardeinstellungen gezeigt.  
  
    ![Gruppenrichtlinienverwaltungs-Editor-Fenster für eine Domäne mit Standardeinstellungen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
5.  Um ein Benutzerkonto auf bestimmte Geräte zu beschränken, klicken Sie auf **Bearbeiten** und definieren Sie die Bedingungen für das Gerät.  
  
    ![Um das Benutzerkonto zum Auswählen von Geräten zu beschränken, klicken Sie auf ** Bearbeitungsformular **](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)  
  
6.  Klicken Sie im Fenster **Bedingungen für die Zugriffssteuerung bearbeiten** auf **Bedingung hinzufügen**.  
  
    ![Bearbeiten von Bedingungen für die Zugriffssteuerung](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCondition.png)  
  
##### <a name="add-computer-account-or-group-conditions"></a>Computerkonto- oder Gruppenbedingungen hinzufügen  
  
1.  Um Computerkonten oder Gruppen zu konfigurieren, ändern Sie im Dropdown-Listenfeld den Wert von **Mitglied aller Gruppen** zu **Mitglied einer oder mehrer Gruppen**.  
  
    ![Konfigurieren von Computerkonten oder Gruppen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompMember.png)  
  
    > [!NOTE]  
    > Diese Zugriffssteuerung definiert die Bedingungen für das Gerät bzw. den Host, von dem sich der Benutzer anmeldet. In der Zugriffssteuerungs-Terminologie ist das Computerkonto für das Gerät oder den Host der Benutzer. Daher ist **Benutzer** die einzige auswählbare Option.  
  
2.  Klicken Sie auf **Elemente hinzufügen**.  
  
    ![Hinzufügen von Elementen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddItems.png)  
  
3.  Klicken Sie auf **Objekttypen**, um die Objekttypen zu ändern.  
  
    ![Objekttypen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjects.gif)  
  
4.  Klicken Sie auf **Computer** und auf **OK**, um Computerobjekte in Active Directory auszuwählen.  
  
    ![Computer](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)  
  
5.  Geben Sie die Namen der Computer ein, auf die der Benutzer eingeschränkt werden soll, und klicken Sie auf **Namen überprüfen**.  
  
    ![Klicken Sie auf Namen überprüfen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)  
  
6.  Klicken Sie auf OK und erstellen Sie ggf. weitere Bedingungen für das Computerkonto.  
  
    ![Klicken Sie auf OK, und erstellen Sie ggf. Weitere Bedingungen für das Computerkonto](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddConditions.png)  
  
7.  Wenn Sie fertig sind, klicken Sie auf **OK**, um die definierten Bedingungen für das Computerkonto zu übernehmen.  
  
    ![Wenn Sie fertig sind, klicken Sie auf ** OK](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompDone.png)  
  
##### <a name="add-computer-claim-conditions"></a>Computer-Anspruchsbedingungen hinzufügen  
  
1.  Wählen Sie den Anspruch in der Gruppen-Dropdownliste aus, um Computeransprüche zu konfigurieren.  
  
    ![Um computeransprüche zu konfigurieren, Dropdown-Gruppe, um den Anspruch auszuwählen.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaim.gif)  
  
    Ansprüche sind nur verfügbar, wenn diese bereits in der Gesamtstruktur eingerichtet wurden.  
  
2.  Geben Sie den Namen der OU ein, auf die das Benutzerkonto bei der Anmeldung eingeschränkt werden soll.  
  
    ![Geben Sie den Namen der OU ein, auf die das Benutzerkonto bei der Anmeldung eingeschränkt werden soll.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimOUName.gif)  
  
3.  Wenn Sie fertig sind, klicken Sie auf OK, um die definierten Bedingungen zu übernehmen.  
  
    ![Klicken Sie anschließend auf OK](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimComplete.gif)  
  
##### <a name="troubleshoot-missing-computer-claims"></a>Problembehandlung für fehlende Computeransprüche  
Falls ein Anspruch konfiguriert wurde und nicht verfügbar ist, kann es sein, dass dieser nur für die **Computer**-Klassen konfiguriert wurde.  
  
Nehmen wir an Sie Authentifizierung basierend auf der Organisationseinheit (OU) beschränken möchten, von dem Computer, der bereits konfiguriert wurde, jedoch nur für **Computer** Klassen.  
  
![Screenshot der Authentifizierung, die basierend auf die Organisationseinheit (OU) des Computers zu beschränken](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictComputers.gif)  
  
Markieren Sie das Kontrollkästchen **Benutzer**, um den Anspruch zum Einschränken der Benutzeranmeldung am Gerät verfügbar zu machen.  
  
![Screenshot, der zeigt, wie Sie die Benutzer melden Sie sich bei dem Gerät durch die SELECT-Anweisung überprüfen ** Benutzer ** Kontrollkästchen.  ](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)  
  
#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>Einrichten eines Benutzerkontos mit Authentifizierungsrichtlinie in ADAC  
  
1.  Klicken Sie im **Benutzerkonto** auf **Richtlinien**.  
  
    ![Von der ** Benutzer ** Konto, klicken Sie auf **-Konfigurationsrichtlinie **](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicy.gif)  
  
2.  Aktivieren Sie das Kontrollkästchen **Diesem Konto eine Authentifizierungsrichtlinie zuweisen**.  
  
    ![Wählen Sie die ** Konto ** das Kontrollkästchen eine Authentifizierungsrichtlinie zuweisen](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)  
  
3.  Wählen Sie anschließend die gewünschte Authentifizierungsrichtlinie für den Benutzer aus.  
  
    ![Wählen Sie die Authentifizierungsrichtlinie für den Benutzer angewendet](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicySelect.png)  
  
#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>Konfigurieren der Unterstützung für dynamische Zugriffssteuerung auf Geräten und Hosts  
Sie können die TGT-Lebensdauer ohne dynamische Zugriffssteuerung (DAC) konfigurieren. DAC wird nur beim Überprüfen von AllowedToAuthenticateFrom und AllowedToAuthenticateTo verwendet.  
  
Aktivieren Sie **die Kerberos-Clientunterstützung für das Schlüsselverteilungscenter (Key Distribution Center KDC) für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** unter Computerkonfiguration | Administrative Vorlagen | System | Kerberos im Editor für Gruppenrichtlinien bzw. lokale Gruppenrichtlinien:  
  
![Screenshot, der zeigt, wie eine Gruppenrichtlinie oder der Editor für lokale Gruppenrichtlinien verwenden, um aktivieren ** Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring **](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)  
  
### <a name="troubleshoot-authentication-policies"></a>Problembehandlung für Authentifizierungsrichtlinien  
  
#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>Ermitteln der Konten, denen eine Authentifizierungsrichtlinie direkt zugewiesen ist  
Im Bereich Konten für die Authentifizierungsrichtlinie werden die Konten angezeigt, denen diese Richtlinie direkt zugewiesen ist.  
  
![Screenshot des Abschnitts "Konten" in der Authentifizierungsrichtlinie, die mit den Konten, die direkt auf die Richtlinie angewendet haben](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AccountsAssigned.gif)  
  
#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Verwenden Sie die Authentifizierung-Richtlinienfehler – Domänencontroller administratives Protokoll  
Ein neues **Fehler bei der Authentifizierung-Richtlinie – Domänencontroller** administratives Protokoll unter **Anwendungs- und Dienstprotokolle** > **Microsoft**  >  **Windows** > **Authentifizierung** erstellt, um die Suche nach Fehlern aufgrund von Authentifizierungsrichtlinien zu erleichtern. Dieses Protokoll ist standardmäßig deaktiviert. Klicken Sie mit der rechten Maustaste auf das Protokoll und klicken Sie auf **Protokoll aktivieren,** um dieses Protokoll zu aktivieren. Die neuen Ereignisse sind den existierenden Ereignissen für Kerberos TGT und die Überwachung von Diensttickets inhaltlich sehr ähnlich. Weitere Informationen zu diesen Ereignissen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](https://technet.microsoft.com/library/dn486813.aspx).  
  
### <a name="manage-authentication-policies-by-using-windows-powershell"></a>Verwalten von Authentifizierungsrichtlinien mit Windows PowerShell  
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
  
## <a name="authentication-policy-silos"></a>Authentifizierungsrichtliniensilos  
Authentifizierungsrichtliniensilos ist ein neuer Container (objectClass msDS-AuthNPolicySilos) in AD DS für Benutzer, Computer und Dienstkonten. Authentifizierungsrichtliniensilos helfen beim Schutz besonders wichtiger Konten. Die Mitglieder der Gruppen Unternehmens-Admins, Domänen-Admins und Schema-Admins müssen in allen Unternehmen geschützt werden, da Angreifer mit diesen Konten Zugriff auf die Gesamtstruktur erhalten können. Allerdings benötigen auch andere Konten Schutz.  
  
Manche Unternehmen isolieren die Arbeitsauslastung durch die Erstellung spezifischer Konten und die Anwendung von Gruppenrichtlinien, um die Berechtigungen für die interaktive Anmeldung lokal und remote einzuschränken. Authentifizierungsrichtliniensilos ergänzen diese Vorgehensweise um die Möglichkeit, Beziehungen zwischen Benutzern, Computern und verwalteten Dienstkonten zu definieren. Jedes Konto kann nur zu einem Silo gehören. Sie können Authentifizierungsrichtlinien für die einzelnen Kontotypen definieren, um Folgendes zu steuern:  
  
1.  Nicht erneuerbare TGT-Lebensdauer  
  
2.  Bedingungen für die Zugriffssteuerung für TGT (Hinweis: gilt nicht für Systeme, da Kerberos Armoring benötigt wird)  
  
3.  Bedingungen für die Zugriffssteuerung für die Rückgabe von Diensttickets  
  
Außerdem haben alle Konten in einem Authentifizierungsrichtliniensilo einen Siloanspruch, der von Ressourcen mit Anspruchsunterstützung wie z. B. Dateiservern für die Zugriffssteuerung genutzt werden kann.  
  
Sie können eine neue Sicherheitsbeschreibung definieren, um die Ausgabe von Diensttickets anhand der folgenden Entitäten zu steuern:  
  
-   Benutzer, die Benutzer Sicherheitsgruppen und/oder Benutzeransprüche  
  
-   Gerät, Geräte Sicherheitsgruppen und/oder Geräteansprüche  
  
Um diese Informationen der Ressource DCs benötigen dynamische Zugriffssteuerung:  
  
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
  
Sie können ein authentifizierungsrichtliniensilo erstellen, mithilfe von Active Directory-Verwaltungscenter oder Windows PowerShell. In der Standardeinstellung authentifizierungsrichtliniensilos nur silorichtlinien. Dies entspricht dem Angeben der **"WhatIf"** Parameter in Windows PowerShell-Cmdlets. In diesem Fall gelten Einschränkungen für Richtliniensilos nicht. Überwachungsdaten werden jedoch generiert und zeigen an, ob beim Anwenden der Einschränkungen Fehler auftreten würden.  
  
#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Erstellen von Authentifizierungsrichtliniensilos im Active Directory-Verwaltungscenter  
  
1.  Öffnen Sie das **Active Directory-Verwaltungscenter**, klicken Sie auf **Authentifizierung**, klicken Sie mit der rechten Maustaste auf **Authentifizierungsrichtliniensilos**, klicken Sie auf **Neu** und anschließend auf **Authentifizierungsrichtliniensilo**.  
  
    ![Öffnen ** Active Directory Administrative Center **, klicken Sie auf ** Authentifizierung **, mit der rechten Maustaste ** Authentication Policy Silos **, klicken Sie auf ** New **, und klicken Sie dann auf ** Authentication Policy Silo **](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)  
  
2.  Geben Sie unter **Anzeigename** einen Namen für den Silo ein. Klicken Sie unter **Erlaubte Konten** auf **Hinzufügen**, geben Sie die Namen der Konten ein und klicken Sie auf **OK**. Sie können Benutzer, Computer oder Dienstkonten angeben. Wählen Sie anschließend aus, ob Sie eine einzige Richtlinie für alle Prinzipale oder eine Richtlinie pro Prinzipal verwenden möchten, und geben Sie die Namen der Richtlinie(n) an.  
  
    ![In ** anzeigen Dienstname **, geben Sie einen Namen für den Silo. In ** dürfen Konten **, klicken Sie auf ** Hinzufügen **, geben Sie die Namen der Konten, und klicken Sie dann auf ** OK](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)  
  
### <a name="manage-authentication-policy-silos-by-using-windows-powershell"></a>Verwalten von Authentifizierungsrichtliniensilos mit Windows PowerShell  
Dieser Befehl erstellt und erzwingt ein Authentifizierungsrichtliniensilo-Objekt.  
  
```  
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce  
```  
  
Dieser Befehl ruft alle Authentifizierungsrichtliniensilos ab, die mit dem im **Filter**-Parameter angegebenen Filter übereinstimmen. Die Ausgabe wird anschließend an das **Format-Table**-Cmdlet weitergereicht, um den Namen der Richtlinie und den Wert für **Enforce** in den einzelnen Richtlinien anzuzeigen.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize  
  
Name  Enforce  
--  ----  
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
  

