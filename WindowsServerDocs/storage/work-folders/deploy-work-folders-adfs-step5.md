---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy - Schritt 5, Einrichten des Clients
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: 4b2c771a83824318f889c955f6194bcb062761f3
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976796"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 5: Einrichten von Clients

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird der fünfte Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Übersicht über die](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 1: Einrichten der AD FS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 2, und AD FS-Konfiguration nach der Arbeit](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 3, Einrichten von Arbeitsordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 4: Einrichten des Webanwendungsproxys](deploy-work-folders-adfs-step4.md)  
  
Gehen Sie folgendermaßen vor, um den mit einer Domäne verbundenen und nicht mit einer Domäne verbundenen Windows-Client einzurichten. Sie können diese Clients verwenden, um zu testen, ob Dateien zwischen den Arbeitsordnern von Clients synchronisiert werden.  
  
## <a name="set-up-a-domain-joined-client"></a>Domänenverbundenen Clientcomputer einrichten  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS- und Arbeitsordner-Zertifikate installieren  
Sie müssen die AD FS- und Arbeitsordner-Zertifikate, die Sie zuvor erstellt haben, in den Zertifikatspeicher des lokalen Computers auf dem domänenverbundenen Clientcomputer installieren.  
  
Da Sie erneut selbstsignierte Zertifikate installieren, die nicht auf einen Herausgeber im Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen zurückverfolgt werden können, müssen Sie auch diese Zertifikate in den Speicher kopieren.  
  
Gehen Sie folgendermaßen vor, um die Zertifikate zu installieren:  
  
1.  Klicken Sie auf **Start** und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap\--In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner Console Root\Certificates\(Local Computer)\Personal\Certificates.  
  
9. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
10. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Zertifikatspeicher.  
  
11. Wiederholen Sie die Schritte 9 und 10, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
12. Erweitern Sie den Ordner Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates.  
  
13. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
14. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Vertrauenswürdige Stammzertifizierungsstellen-Speicher.  
  
15. Wiederholen Sie die Schritte 13 und 14, indem Sie zum Arbeitsordner des Zertifikats navigieren und es importieren.  
  
### <a name="configure-work-folders-on-the-client"></a>Arbeitsordner auf dem Client konfigurieren  
Gehen Sie folgendermaßen vor, um Arbeitsordner auf dem Clientcomputer zu konfigurieren:  
  
1.  Öffnen Sie auf dem Clientcomputer **Systemsteuerung** und klicken Sie auf **Arbeitsordner**.  
  
2.  Klicken Sie auf **Arbeitsordner einrichten**.  
  
3.  Auf der **Geben Sie Ihre geschäftliche e-Mail-Adresse** Seite, die der Benutzer e-Mail-Adresse eingeben (z. B. user@contoso.com) oder die Arbeitsordner-URL (im Testbeispiel Https:\//workfolders.contoso.com), und klicken Sie dann auf  **Nächste**.  
  
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
  
## <a name="see-also"></a>Siehe auch  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  

