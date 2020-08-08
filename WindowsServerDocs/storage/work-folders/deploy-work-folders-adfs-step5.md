---
title: 'Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients'
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: fd8015b1a72477c00fda0c3483bbdd6504ff86b8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965817"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5, Einrichten von Clients

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird der fünfte Schritt beim Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy beschrieben. Die anderen Schritte in diesem Prozess finden Sie in den folgenden Themen:

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)

Verwenden Sie die folgenden Verfahren zum Einrichten der in die Domäne eingebundenen und nicht in die Domäne eingebundenen Windows-Clients. Sie können diese Clients verwenden, um zu testen, ob Dateien zwischen den Arbeits Ordnern der Clients ordnungsgemäß synchronisiert werden.

## <a name="set-up-a-domain-joined-client"></a>Einrichten eines in die Domäne eingebundenen Clients

### <a name="install-the-ad-fs-and-work-folder-certificates"></a>Installieren der AD FS-und Arbeitsordner Zertifikate
Sie müssen die Zertifikate für AD FS und Arbeitsordner, die Sie zuvor erstellt haben, im Zertifikat Speicher des lokalen Computers auf dem in die Domäne eingebundenen Client Computer installieren.

Da Sie selbst signierte Zertifikate installieren, die nicht an einen Verleger im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen zurückverfolgt werden können, müssen Sie auch die Zertifikate in diesen Speicher kopieren.

Um die Zertifikate zu installieren, führen Sie die folgenden Schritte aus:

1.  Klicken Sie im **Startmenü**auf **Ausführen**.

2.  Geben Sie **MMC**ein.

3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.

4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**. Der Snap- \- in-Assistent für Zertifikate wird gestartet.

5.  Wählen Sie **Computerkonto** aus, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie **lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird) aus**, und klicken Sie dann auf **Fertig**stellen.

7.  Klicken Sie auf **OK**.

8.  Erweitern Sie die Ordner Konsole root\zertifikate \( lokaler Computer) \personal \ certificates.

9. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.

10. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Zertifikat Speicher zu platzieren.

11. Wiederholen Sie die Schritte 9 und 10. wechseln Sie diesmal zum Arbeitsordner Zertifikat, und importieren Sie es.

12. Erweitern Sie die Ordner Konsole root\zertifikate \( lokaler Computer) \trusted Root Certification autorities\certifikates.

13. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.

14. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Speicher Vertrauenswürdige Stamm Zertifizierungsstellen zu platzieren.

15. Wiederholen Sie die Schritte 13 und 14, und navigieren Sie dieses Mal zum Arbeitsordner Zertifikat, und importieren Sie es.

### <a name="configure-work-folders-on-the-client"></a>Arbeitsordner auf dem Client konfigurieren
Führen Sie die folgenden Schritte aus, um Arbeitsordner auf dem Client Computer zu konfigurieren:

1. Öffnen Sie auf dem Client Computer die **Systemsteuerung** , und klicken Sie auf **Arbeitsordner**.

2. Klicken Sie auf **Arbeitsordner einrichten**.

3. Geben Sie auf der Seite **Geben Sie Ihre geschäftliche e-Mail-Adresse** ein entweder die e-Mail-Adresse des Benutzers (z. b. user@contoso.com ) oder die URL für Arbeitsordner (im Testbeispiel https: \/ /workfolders.contoso.com) ein, und klicken Sie dann auf **weiter**.

4. Wenn der Benutzer mit dem Unternehmensnetzwerk verbunden ist, wird die Authentifizierung von der integrierten Windows-Authentifizierung durchgeführt. Wenn der Benutzer nicht mit dem Unternehmensnetzwerk verbunden ist, wird die Authentifizierung von ADFS (OAuth) ausgeführt, und der Benutzer wird zur Eingabe von Anmelde Informationen aufgefordert. Geben Sie Ihre Anmelde Informationen ein, und klicken Sie auf **OK**

5. Nachdem Sie sich authentifiziert haben, wird die Seite "Einführung in die **Arbeitsordner** " angezeigt, auf der Sie optional den Speicherort des Arbeitsordner Verzeichnisses ändern können. Klicken Sie auf **Weiter**.

6. Auf der Seite **Sicherheitsrichtlinien** werden die Sicherheitsrichtlinien aufgelistet, die Sie für Arbeitsordner einrichten. Klicken Sie auf **Weiter**.

7. Es wird eine Meldung angezeigt, die besagt, dass die Synchronisierung der Arbeitsordner mit Ihrem PC gestartet wurde. Klicken Sie auf **Schließen**.

8. Auf der Seite **Arbeitsordner verwalten** wird der verfügbare Speicherplatz auf dem Server, der Synchronisierungs Status usw. angezeigt. Wenn erforderlich, können Sie hier Ihre Anmelde Informationen erneut eingeben. Schließen Sie das Fenster.

9. Der Ordner "Arbeitsordner" wird automatisch geöffnet. Sie können diesem Ordnerinhalte hinzufügen, um eine Synchronisierung zwischen ihren Geräten durchzusetzen.

    Fügen Sie für das Testbeispiel dem Ordner für Arbeitsordner eine Testdatei hinzu. Nachdem Sie die Arbeitsordner auf dem Computer eingerichtet haben, der nicht der Domäne beigetreten ist, können Sie Dateien zwischen den Arbeits Ordnern auf den einzelnen Computern synchronisieren.

## <a name="set-up-a-non-domain-joined-client"></a>Einrichten eines Clients, der keiner Domäne beigetreten ist

### <a name="install-the-ad-fs-and-work-folder-certificates"></a>Installieren der AD FS-und Arbeitsordner Zertifikate
Installieren Sie die AD FS-und Arbeitsordner Zertifikate auf dem Computer, der nicht der Domäne beigetreten ist, und verwenden Sie dabei die gleichen Schritte wie für den in die Domäne eingebundenen Computer.

### <a name="update-the-hosts-file"></a>Aktualisieren der Datei "Hosts"
Die Hostdatei auf dem Client, der nicht der Domäne beigetreten ist, muss für die Testumgebung aktualisiert werden, da keine öffentlichen DNS-Einträge für Arbeitsordner erstellt wurden. Fügen Sie diese Einträge der Hosts-Datei hinzu:

-  Arbeitsordner. Domäne

-  AD FS Dienst Name. Domäne

-  enterpriseregistration. Domäne

Verwenden Sie für das Testbeispiel folgende Werte:

-  **10.0.0.10 workfolders.contoso.com**

-  **10.0.0.10 blueadfs.contoso.com**

-  **10.0.0.10 enterpriseregistration.contoso.com**

### <a name="configure-work-folders-on-the-client"></a>Arbeitsordner auf dem Client konfigurieren
Konfigurieren Sie Arbeitsordner auf dem Computer, der nicht der Domäne beigetreten ist, und verwenden Sie das Verfahren, das Sie für den in die Domäne eingebundenen Computer verwendet haben.

Wenn der Ordner neuer Arbeitsordner auf diesem Client geöffnet wird, können Sie sehen, dass die Datei auf dem Computer, der der Domäne angehört, bereits mit dem Computer synchronisiert wurde, der keiner Domäne angehört. Sie können mit dem Hinzufügen von Inhalt zum Ordner zum Synchronisieren zwischen ihren Geräten beginnen.

Dies schließt das Verfahren zum Bereitstellen von Arbeits Ordnern, AD FS und webanwendungsproxy über die Windows Server-Benutzeroberfläche ab.

## <a name="see-also"></a>Weitere Informationen
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)


