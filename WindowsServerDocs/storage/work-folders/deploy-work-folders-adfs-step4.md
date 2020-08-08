---
title: Arbeitsordner mit AD FS und webanwendungsproxy
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 06/24/2017
ms.assetid: 4a11ede0-b000-4188-8190-790971504e17
ms.openlocfilehash: 0b7748332d8760db24010a04d0ecf3a5094bcda6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965827"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-4-set-up-web-application-proxy"></a>Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4, Einrichten des webanwendungsproxys

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird der vierte Schritt beim Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy beschrieben. Die anderen Schritte in diesem Prozess finden Sie in den folgenden Themen:

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)

> [!NOTE]
>   Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2019-oder Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, befolgen Sie die [Anweisungen unter Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)).

Verwenden Sie die folgenden Verfahren, um den webanwendungsproxy für die Verwendung mit Arbeits Ordnern einzurichten.

## <a name="install-the-ad-fs-and-work-folder-certificates"></a>Installieren der AD FS-und Arbeitsordner Zertifikate
Sie müssen die AD FS-und Arbeitsordner Zertifikate installieren, die Sie zuvor erstellt haben (in Schritt 1, Einrichten von AD FS und Schritt 3, Einrichten von Arbeits Ordnern) in den Zertifikat Speicher des lokalen Computers auf dem Computer, auf dem die webanwendungsproxy-Rolle installiert wird.

Da Sie selbst signierte Zertifikate installieren, die nicht an einen Verleger im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen zurückverfolgt werden können, müssen Sie auch die Zertifikate in diesen Speicher kopieren.

Um die Zertifikate zu installieren, führen Sie die folgenden Schritte aus:

1.  Klicken Sie im **Startmenü**auf **Ausführen**.

2.  Geben Sie **MMC**ein.

3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.

4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**. Der Zertifikat-Snap-in-Assistent wird gestartet.

5.  Wählen Sie **Computerkonto** aus, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie **lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird) aus**, und klicken Sie dann auf **Fertig**stellen.

7.  Klicken Sie auf **OK**.

8.  Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \personal\zertifikate**.

9. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.

10. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Zertifikat Speicher zu platzieren.

11. Wiederholen Sie die Schritte 9 und 10. wechseln Sie diesmal zum Arbeitsordner Zertifikat, und importieren Sie es.

12. Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \trusted Root Certification autorities\zertifikate**.

13. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.

14. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Speicher Vertrauenswürdige Stamm Zertifizierungsstellen zu platzieren.

15. Wiederholen Sie die Schritte 13 und 14, und navigieren Sie dieses Mal zum Arbeitsordner Zertifikat, und importieren Sie es.

## <a name="install-web-application-proxy"></a>Webanwendungsproxy installieren
Führen Sie die folgenden Schritte aus, um den webanwendungsproxy

1.  Öffnen Sie auf dem Server, auf dem Sie den webanwendungsproxy installieren möchten, **Server-Manager** , und starten Sie den Assistenten zum **Hinzufügen von Rollen und Features**

2.  Klicken Sie auf der ersten und zweiten Seite des Assistenten auf **weiter** .

3.  Wählen Sie auf der Seite **Server Auswahl** Ihren Server aus, und klicken Sie dann auf **weiter**.

4.  Wählen Sie auf der Seite **Server Rolle** die Rolle **Remote Zugriff** aus, und klicken Sie dann auf **weiter**.

5.  Klicken Sie auf der Seite Features und Remote Zugriff auf **weiter**.

6.  Wählen Sie auf der Seite **Rollen Dienste** die Option **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.

7.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.

## <a name="configure-web-application-proxy"></a>Konfigurieren des Webanwendungsproxys
Gehen Sie zum Konfigurieren des webanwendungsproxys folgendermaßen vor

1.  Klicken Sie oben in Server-Manager auf das Warn Flag, und klicken Sie dann auf den Link, um den Assistenten zum Konfigurieren von webanwendungsproxys zu öffnen

2.  Klicken Sie auf der Willkommensseite auf **weiter**.

3.  Geben Sie auf der Seite Verbund **Server** den Namen des Verbunddienst ein. Im Beispiel Test ist dies **blueadfs.contoso.com**.

4.  Geben Sie die Anmelde Informationen eines lokalen Administrator Kontos auf den Verbund Servern ein. Geben Sie keine Anmelde Informationen für die Domäne ein (z. b. condeso\administrator), sondern lokale Anmelde Informationen (z. b. Administrator).

5.  Wählen Sie auf der Seite **AD FS Proxy Zertifikat** das AD FS Zertifikat aus, das Sie zuvor importiert haben. Im Testfall ist dies **blueadfs.contoso.com**. Klicken Sie auf **Weiter**.

6.  Auf der Seite Bestätigung wird der Windows PowerShell-Befehl angezeigt, der zum Konfigurieren des-Dienstanbieter ausgeführt wird. Klicken Sie auf **Konfigurieren**.

## <a name="publish-the-work-folders-web-application"></a>Veröffentlichen der Arbeitsordner-Webanwendung
Der nächste Schritt besteht darin, eine Webanwendung zu veröffentlichen, mit der Arbeitsordner für Clients verfügbar gemacht werden. Führen Sie die folgenden Schritte aus, um die Webanwendung für Arbeitsordner zu veröffentlichen:

1. Öffnen Sie **Server-Manager**, und klicken Sie **im Menü Extras** auf **Remote Zugriffs Verwaltung** , um die Remote Zugriffs-Verwaltungskonsole zu öffnen.

2. Klicken Sie unter **Konfiguration**auf **webanwendungsproxy**.

3. Klicken Sie unter **Aufgaben**auf **veröffentlichen**. Der Assistent zum Veröffentlichen einer neuen Anwendung wird geöffnet.

4. Klicken Sie auf der Seite Willkommenauf **Weiter**.

5. Wählen Sie auf der Seite **Vorauthentifizierung** die Option **Active Directory-Verbunddienste (AD FS) (AD FS)** aus, und klicken Sie auf **weiter**.

6. Wählen Sie auf der Seite **Support Clients** die Option **OAuth2**aus, und klicken Sie auf **weiter**.

7. Wählen Sie **auf der Seite vertrauende Seite die** Option **Arbeitsordner**aus, und klicken Sie dann auf **weiter**. Diese Liste wird vom AD FS auf dem webanwendungsproxy veröffentlicht.

8. Geben Sie auf der Seite **Veröffentlichungs Einstellungen** Folgendes ein, und klicken Sie dann auf **weiter**:

   -   Der Name, den Sie für die Webanwendung verwenden möchten.

   -   Die externe URL für Arbeitsordner

   -   Der Name des Arbeitsordner Zertifikats

   -   Die Back-End-URL für Arbeitsordner

   Standardmäßig wird die Back-End-URL vom Assistenten mit der externen URL identisch.

   Verwenden Sie für das Testbeispiel folgende Werte:

   Name: **Arbeitsordner**

   Externe URL:**https://workfolders.contoso.com**

   Externes Zertifikat: **das Arbeitsordner Zertifikat, das Sie zuvor installiert** haben

   URL des Backend-Servers:**https://workfolders.contoso.com**

9. Auf der Seite Bestätigung wird der Windows PowerShell-Befehl angezeigt, der zum Veröffentlichen der Anwendung ausgeführt wird. Klicken Sie auf **Veröffentlichen**.

10. Auf der Seite **Ergebnisse** sollten Sie sehen, dass die Anwendung erfolgreich veröffentlicht wurde.
    >[!NOTE]
    > Wenn Sie über mehrere Arbeitsordner Server verfügen, müssen Sie eine Arbeitsordner-Webanwendung für jeden Arbeitsordner Server veröffentlichen (wiederholen Sie die Schritte 1-10).

Nächster Schritt: [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)

## <a name="see-also"></a>Weitere Informationen
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)

