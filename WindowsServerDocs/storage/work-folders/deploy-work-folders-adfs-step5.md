---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy - Schritt5, Einrichten des Clients
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: fa8b2b15ff411a59b28308a329d7ca2341ef0886
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt5, Einrichten des Clients

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird der fünfte Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt1, Einrichten von ADFS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt2, Konfigurationsaufgaben nach dem Einrichten von AD FS](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt3, Einrichten von Arbeitsordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt4, Einrichten des Webanwendungsproxy](deploy-work-folders-adfs-step4.md)  
  
Gehen Sie folgendermaßen vor, um den mit einer Domäne verbundenen und nicht mit einer Domäne verbundenen Windows-Client einzurichten. Sie können diese Clients verwenden, um zu testen, ob Dateien zwischen den Arbeitsordnern von Clients synchronisiert werden.  
  
## <a name="set-up-a-domain-joined-client"></a>Domänenverbundenen Clientcomputer einrichten  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS- und Arbeitsordner-Zertifikate installieren  
Sie müssen die AD FS- und Arbeitsordner-Zertifikate, die Sie zuvor erstellt haben, in den Zertifikatspeicher des lokalen Computers auf dem domänenverbundenen Clientcomputer installieren.  
  
Da Sie erneut selbstsignierte Zertifikate installieren, die nicht auf einen Herausgeber im Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen zurückverfolgt werden können, müssen Sie auch diese Zertifikate in den Speicher kopieren.  
  
Gehen Sie folgendermaßen vor, um die Zertifikate zu installieren:  
  
1.  Klicken Sie auf **Start**und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap-In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner „Konsolenstamm\Zertifikate\(Lokaler Computer)\Persönlich\Zertifikate“.  
  
9. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
10. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Zertifikatspeicher.  
  
11. Wiederholen Sie die Schritte9 und 10, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
12. Erweitern Sie den Ordner „Konsolenstamm\Zertifikate\(Lokaler Computer)\Vertrauenswürdige Stammzertifizierungsstellen\Zertifikate“.  
  
13. Klicken Sie mit der rechten Maustaste auf das **Zertifikat** und dann auf **Alle Aufgaben**Alle Aufgaben **Importieren**.  
  
14. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Vertrauenswürdige Stammzertifizierungsstellen-Store.  
  
15. Wiederholen Sie die Schritte13 und 14, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
### <a name="configure-work-folders-on-the-client"></a>Arbeitsordner auf dem Client konfigurieren  
Gehen Sie folgendermaßen vor, um Arbeitsordner auf dem Clientcomputer zu konfigurieren:  
  
1.  Öffnen Sie auf dem Clientcomputer **Systemsteuerung** und klicken Sie auf **Arbeitsordner**.  
  
2.  Klicken Sie auf **Arbeitsordner einrichten**.  
  
3.  Geben Sie auf der Seite **Geben Sie Ihre Arbeits-E-Mail-Adresse ein** die E-Mail-Adresse des Benutzers (z.B. user@contoso.com) oder die Arbeitsordner-URL ein (im Testbeispiel „https://workfolders.contoso.com“), und klicken Sie dann auf **Weiter**.  
  
4.  Wenn der Benutzer mit dem Unternehmensnetzwerk verbunden ist, erfolgt die Authentifizierung durch die integrierte Windows-Authentifizierung. Wenn der Benutzer nicht mit dem Unternehmensnetzwerk verbunden ist, erfolgt die Authentifizierung durch AD FS (OAuth) und der Benutzer wird zur Eingabe der Anmeldeinformationen aufgefordert. Geben Sie Ihre Anmeldeinformationen ein, und klicken Sie auf **OK**.  
  
5.  Nach der Authentifizierung wird die Seite **Einführung in Arbeitsordner** angezeigt, auf der Sie optional das Verzeichnis der Arbeitsordner ändern können. Klicken Sie auf **Weiter**.  
  
6.  Die Seite mit den **Sicherheitsrichtlinien** enthält die Sicherheitsrichtlinien, die Sie für Arbeitsordner eingerichtet haben. Klicken Sie auf **Weiter**.  
  
7.  Es wird eine Meldung angezeigt, dass die Synchronisierung der Arbeitsordner mit Ihrem PC beginnt. Klicken Sie auf **Schließen**.  
  
8.  Auf der Seite **Arbeitsordner verwalten** wird der verfügbare Speicherplatz auf dem Server, der Synchronisierungsstatus und so weiter angezeigt. Falls erforderlich, können Sie hier Ihre Anmeldeinformationen erneut eingeben. Schließen Sie das Fenster.  
  
9. Der Ordner „Arbeitsordner” wird automatisch geöffnet. Sie können diesem Ordner Inhalte hinzufügen, die zwischen Ihren Geräten synchronisiert werden sollen.  
  
    Fügen Sie für den Test diesem Ordner Arbeitsordner eine Testdatei hinzu. Nach dem Einrichten der Arbeitsordner auf dem nicht-domänenverbundenen Computer, können Sie Dateien zwischen den Arbeitsordnern auf jedem Computer synchronisieren.  
  
## <a name="set-up-a-non-domain-joined-client"></a>Nicht-Domänenverbundenen Clientcomputer einrichten  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS- und Arbeitsordner-Zertifikate installieren  
Installieren Sie die AD FS- und Arbeitsordner-Zertifikate auf dem nicht-domänenverbundenen Computer, indem Sie das gleiche Verfahren anwenden, das für domänenverbundene Computer verwendet wurde.  
  
### <a name="update-the-hosts-file"></a>Die Hosts-Datei aktualisieren  
Die Hostdatei auf dem nicht-domänenverbundenen Computer muss für die Testumgebung aktualisiert werden, da keine öffentlichen DNS-Einträge für Arbeitsordner erstellt wurden. Fügen Sie der Hostsdatei diese Einträge hinzu:  
  
-  workfolders.domain  
  
-  AD FS service name.domain  
  
-  enterpriseregistration.domain  
  
Verwenden Sie für das Testbeispiel diese Werte:  
  
-  **10.0.0.10 workfolders.contoso.com**  
  
-  **10.0.0.10 blueadfs.contoso.com**  
  
-  **10.0.0.10 enterpriseregistration.contoso.com**  
  
### <a name="configure-work-folders-on-the-client"></a>Arbeitsordner auf dem Client konfigurieren  
Konfigurieren Sie Arbeitsordner auf dem nicht-domänenverbundenen Computer, indem Sie das gleiche Verfahren anwenden, das Sie für der domänenverbundenen Computer verwendeten.  
  
Wenn die neuen Arbeitsordner auf dem Client geöffnet werden, können Sie sehen, dass die Datei des domänenverbundenen Computers bereits mit dem nicht-domänenverbundenen Computer synchronisiert wurde. Sie können dem Ordner Inhalte hinzufügen, der zwischen Geräten synchronisiert werden soll.  
  
Dies schließt das Verfahren für die Bereitstellung von Arbeitsordnern, AD FS und Webanwendungsproxy über die Windows Server-Benutzeroberfläche ab.  
  
## <a name="see-also"></a>Weitere Informationen  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  

