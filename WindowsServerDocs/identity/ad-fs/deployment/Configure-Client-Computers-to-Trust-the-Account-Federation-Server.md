---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: Konfigurieren von Client Computern, um dem Konto Verbund Server zu Vertrauen
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 31a878460b94dadcb01578a45c21d270e1560391
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938452"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>Konfigurieren von Client Computern, um dem Konto Verbund Server zu Vertrauen

Damit Client Computer mit Active Directory-Verbunddienste (AD FS) AD FS erfolgreich auf Verbund Anwendungen zugreifen können \( \) , müssen Sie zuerst die Internet Explorer-Einstellungen auf jedem Client Computer konfigurieren, damit der Browser dem Konto Verbund Server vertraut. Sie können dies manuell oder über Gruppenrichtlinie durchführen, indem Sie eines der folgenden Verfahren ausführen.

## <a name="configuring-internet-explorer-settings-manually"></a>Manuelles Konfigurieren von Internet Explorer-Einstellungen
Mithilfe des folgenden Verfahrens können Sie die Internet Explorer-Einstellungen der einzelnen Benutzer manuell konfigurieren, um den Verbund über AD FS zu unterstützen. Wenn mehrere Benutzer einen einzelnen Computer verwenden, führen Sie dieses Verfahren mehrmals aus – einmal für jedes Benutzerprofil.

Um dieses Verfahren auszuführen, melden Sie sich als der Benutzer an, der auf Verbund Anwendungen zugreifen soll. Dies ist eine Profil \- spezifische Einstellung. Daher ist es erforderlich, diese Einstellung für jedes Profil, das auf einem bestimmten Computer vorhanden ist, manuell hinzuzufügen.

#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>So konfigurieren Sie Client Computer manuell so, dass Sie dem Konto Verbund Server Vertrauen

1.  Starten Sie Internet Explorer auf dem Client Computer.

2.  Klicken Sie **im Menü Extras** auf **Internet Optionen**.

3.  Klicken Sie auf der Registerkarte **Sicherheit** auf das Symbol **Lokales Intranet** , und klicken Sie dann auf **Sites**.

4.  Klicken Sie auf **erweitert**, und geben Sie in **diese Website zur Zone hinzufügen**den vollständigen Domain Name System \( DNS \) -Namen des Konto Verbund Servers ein, z. b \( . https: \/ \/ FS1.fabrikam.com \) , und klicken Sie dann auf **Hinzufügen**.

5.  Klicken Sie dreimal auf **OK**.

## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>Konfigurieren von Internet Explorer-Einstellungen mit Gruppenrichtlinie
Bei den meisten bereit Stellungen wird empfohlen, Gruppenrichtlinie zu verwenden, um die entsprechenden Internet Explorer-Einstellungen an jeden Client Computer zu überführen.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** , Organisations- **Admins**oder einer entsprechenden Gruppe in Active Directory Domain Services \( AD DS \) erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .

#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>So konfigurieren Sie Client Computer für die Vertrauensstellung des Konto Verbund Servers mithilfe von Gruppenrichtlinie

1.  Starten Sie auf einem Domänen Controller in der Gesamtstruktur der Konto Partnerorganisation das Snap-in " **Gruppenrichtlinie-Verwaltung** " \- .

2.  Suchen Sie das entsprechende Gruppenrichtlinie Objekt \( -GPO, klicken Sie mit der \) rechten \- Maustaste darauf, und klicken Sie dann auf **Bearbeiten**

3.  Öffnen Sie in der Konsolen **Struktur Benutzer Konfigurations \\ Einstellungen \\ Windows-Einstellungen \\ Internet Explorer Wartung**, und klicken Sie dann auf **Sicherheit**.

4.  Doppelklicken Sie im Detailbereich \- auf **Sicherheitszonen und Inhalts Bewertungen**.

5.  Klicken Sie unter **Sicherheitszonen und Datenschutz**auf **aktuelle Sicherheitszonen und Datenschutzeinstellungen importieren**, und klicken Sie dann auf **Einstellungen ändern**.

6.  Klicken Sie auf **Lokales Intranet**und dann auf **Sites**.

7.  Geben Sie unter **diese Website zur Zone hinzufügen**den vollständigen DNS-Namen des Konto Verbund Servers ein, z. b. \( https: \/ \/ FS1.fabrikam.com \) , klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Schließen**.

8.  Klicken Sie zwei Mal auf **OK** , um diese Änderungen auf Gruppenrichtlinie anzuwenden.

