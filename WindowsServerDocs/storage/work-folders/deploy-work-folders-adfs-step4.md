---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy - Schritt 4, Einrichten des Webanwendungsproxy
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 6/24/2017
ms.assetid: 4a11ede0-b000-4188-8190-790971504e17
ms.openlocfilehash: 17adf89d3a26767bbc736a31da7b7b2b204570a2
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945240"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-4-set-up-web-application-proxy"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 4, Einrichten des Webanwendungsproxy

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird der vierte Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)  

> [!NOTE]
>   Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2019-oder Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, folgen Sie den [Anweisungen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx).

Gehen Sie folgendermaßen vor, um Webanwendungsproxy für die Verwendung mit Arbeitsordner einzurichten.  
  
## <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS- und Arbeitsordner-Zertifikate installieren  
Installieren Sie die AD FS und Arbeitsordner Zertifikate, die Sie zuvor erstellt haben (in Schritt 1, Einrichten von AD FS und Schritt 3 Arbeitsordner einrichten) im lokalen Zertifikatspeicher auf dem Computer, auf dem die Webanwendungsproxy-Rolle installiert wird.  
  
Da Sie selbstsignierte Zertifikate installieren, die nicht auf einen Herausgeber im Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen zurückverfolgt werden können, müssen Sie auch diese Zertifikate in den Speicher kopieren.  
  
Gehen Sie folgendermaßen vor, um die Zertifikate zu installieren:  
  
1.  Klicken Sie auf **Start**und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap-In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner **Console Root\Certificates\(Local Computer)\Personal\Certificates**.  
  
9. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
10. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Zertifikatspeicher.  
  
11. Wiederholen Sie die Schritte 9 und 10, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
12. Erweitern Sie den Ordner **Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates**.  
  
13. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
14. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Vertrauenswürdige Stammzertifizierungsstellen-Speicher.  
  
15. Wiederholen Sie die Schritte 13 und 14, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
## <a name="install-web-application-proxy"></a>Webanwendungsproxy installieren  
Gehen Sie folgendermaßen vor, um Webanwendungsproxys zu installieren:  
  
1.  Öffnen Sie auf dem Server, auf dem Sie die Webanwendungsproxy installieren möchten den **Server-Manager** und starten Sie den Assistenten zum **Hinzufügen von Rollen und Features**.  
  
2.  Klicken Sie auf auf der ersten und zweiten Seite des Assistenten auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Serverauswahl** den Server aus und klicken Sie auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Serverrolle** **Remotezugriff** und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite Features und Remotezugriff auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Rollendienste** **Webanwendungsproxy** aus, klicken Sie auf **Features hinzufügen** und dann auf **Weiter**.

7.  Klicken Sie auf der Seite **Confirm installation selections** auf **Install**.  
  
## <a name="configure-web-application-proxy"></a>Konfigurieren des Webanwendungsproxys  
Gehen Sie folgendermaßen vor, um Webanwendungsproxys zu konfigurieren:  
  
1.  Klicken Sie oben im Server Manager auf die Warnung und dann auf den Link zum Öffnen des Assistenten zum Konfigurieren des Webanwendungsproxys.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Verbundserver** den Namen des Verbunddienstes an. In diesem Testbeispiel ist der Wert **blueadfs.contoso.com**.  
  
4.  Geben Sie die Anmeldeinformationen für ein lokales Administratorkonto auf dem Verbundserver ein. Geben Sie nicht die Domänenanmeldeinformation ein (z. B. Contoso\administrator), sondern die lokale Anmeldeinformationen (z. B. "Administrator").  
  
5.  Wählen Sie auf der Seite **D FS-Proxyzertifikat** das AD FS-Zertifikat, das Sie zuvor importiert haben aus. In diesem Testbeispiel ist der Wert **blueadfs.contoso.com**. Klicken Sie auf **Weiter**.  
  
6.  Auf der Seite „Bestätigung” wird der Windows PowerShell-Befehl angezeigt, der ausgeführt wird, um den Dienst zu konfigurieren. Klicken Sie auf **Konfigurieren**.  
  
## <a name="publish-the-work-folders-web-application"></a>Veröffentlichen Sie die Arbeitsordner-Webanwendung  
Im nächste Schritt wird gezeigt, wie eine Anwendung veröffentlicht wird, die Arbeitsordner für Clients verfügbar machen. Um die Arbeitsordner-Webanwendung zu veröffentlichen, gehen Sie folgendermaßen vor:  
  
1. Öffnen Sie **Server Manager** und klicken Sie auf das Menü **Tools** Menü, klicken Sie auf **Remotezugriffsverwaltung**, um die in der Remotezugriffs-Verwaltungskonsole.  
  
2. Klicken Sie unter **Konfiguration** auf **Webanwendungsproxy**.  
  
3. Klicken Sie unter **Aufgaben** auf **Veröffentlichen**. Der Assistenten zum Veröffentlichen neuer Anwendungen wird geöffnet.  
  
4. Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
5. Klicken Sie auf der Seite **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS)** und klicken Sie dann auf **Weiter**.  
  
6. Wählen Sie auf der Seite **Clients unterstützen** **OAuth2** aus und klicken Sie auf **Weiter**.

7. Wählen Sie auf der Seite **Vertrauensstellung der vertrauenden Seite** **Arbeitsordner** aus und klicken Sie dann auf **Weiter**. Diese Liste wird von AD FS auf der Webanwendungsproxy veröffentlicht.  
  
8. Geben Sie auf der Seite **Veröffentlichungseinstellungen** folgende Informationen ein und klicken Sie dann auf **Weiter**:  
  
   -   Der Name, den Sie für die Webanwendung verwenden möchten.  
  
   -   Die externe URL für Arbeitsordner  
  
   -   Der Name des Arbeitsordner-Zertifikats  
  
   -   Die Back-End-URL für Arbeitsordner  
  
   Standardmäßig benennt der Assistent die Back-End-URL genauso wie die externe URL.  
  
   Verwenden Sie für das Testbeispiel diese Werte:  
  
   Name: **Arbeitsordner**  
  
   Externe URL: **https://workfolders.contoso.com**  
  
   Externes Zertifikat: **Das Arbeitsordner-Zertifikat, das Sie bereits installiert haben**  
  
   URL des Backend-Servers: **https://workfolders.contoso.com**  
  
9. Auf der Seite „Bestätigung” wird der Windows PowerShell-Befehl angezeigt, der ausgeführt wird, um die Anwendung zu veröffentlichen. Klicken Sie auf **Veröffentlichen**.  
  
10. Auf der Seite **Ergebnisse** wird angezeigt, ob die Anwendung erfolgreich veröffentlicht wurde.
    >[!NOTE]
    > Wenn Sie über mehrere Arbeitsordner-Server verfügen, müssen Sie eine Arbeitsordner-Webanwendung für die einzelnen Arbeitsordner-Server veröffentlichen (Wiederholen Sie die Schritte 1 bis 10).  
  
Nächster Schritt: [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 5, Einrichten von Clients](deploy-work-folders-adfs-step5.md)  
  
## <a name="see-also"></a>Weitere Informationen  
[Übersicht über Arbeitsordner](Work-Folders-Overview.md)  
  

