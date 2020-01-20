---
title: Clients können keine Verbindung herstellen und erhalten den Fehler „Keine Lizenzen verfügbar“
description: Beheben des Fehlers „Keine Lizenzen verfügbar“ bei der Remotedesktopverbindung
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 74b4656216d5568f546d1a13722eeec748f1f9b5
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265892"
---
# <a name="clients-cant-connect-and-see-no-licenses-available-error"></a>Clients können keine Verbindung herstellen und erhalten den Fehler „Keine Lizenzen verfügbar“

Diese Situation betrifft alle Bereitstellungen, die einen RDSH-Server und einen Remotedesktop-Lizenzierungsserver beinhalten.

Bestimmen Sie zunächst, welches Verhalten die Benutzer beobachten:

- Die Verbindung mit der Sitzung wurde getrennt, da keine Lizenzen verfügbar sind oder kein Lizenzserver verfügbar ist.
- Der Zugriff wurde aufgrund eines Sicherheitsfehlers verweigert.

Melden Sie sich beim RD-Sitzungshost als Domänenadministrator an, und öffnen Sie die RD-Lizenzdiagnose. Suchen Sie nach Nachrichten wie der folgenden:

  - Die Kulanzfrist für den Remotedesktop-Sitzungshostserver ist abgelaufen, der RD-Sitzungshostserver wurde jedoch noch nicht mit Lizenzservern konfiguriert. Verbindungen mit dem RD-Sitzungshostserver werden abgelehnt, bis ein Lizenzserver für den RD-Sitzungshostserver konfiguriert wurde.
  - Der Lizenzserver \<Computername\> ist nicht verfügbar. Dies könnte durch Probleme mit der Netzwerkverbindung verursacht sein oder darauf beruhen, dass der Remotedesktop-Lizenzierungsdienst auf dem Lizenzserver beendet wurde oder die RD-Lizenzierung nicht mehr verfügbar ist.

Diese Probleme gehen häufig mit den folgenden Benutzermeldungen einher:

  - Die Remotesitzung wurde getrennt, da für diesen Computer keine Remotedesktop-Clientzugriffslizenzen verfügbar sind.
  - Die Remotesitzung wurde getrennt, da keine Remotedesktop-Lizenzserver verfügbar sind, um eine Lizenz bereitzustellen.

In diesem Fall können Sie [den RD-Lizenzierungsdienst konfigurieren](#configure-the-rd-licensing-service).

Wenn die RD-Lizenzdiagnose andere Probleme auflistet, wie etwa „Die RDP-Protokollkomponente X.224 hat einen Fehler im Protokolldatenstrom erkannt und den Client getrennt“, liegt möglicherweise ein Problem vor, das die Lizenzzertifikate betrifft. Solche Probleme gehen häufig mit Benutzermeldungen einher, wie etwa der folgenden:

Aufgrund eines Sicherheitsfehlers konnte der Client keine Verbindung mit dem Terminalserver herstellen. Nachdem Sie sichergestellt haben, dass Sie beim Netzwerk angemeldet sind, versuchen Sie noch einmal, eine Verbindung mit dem Server herzustellen.

In diesem Fall können Sie [die Registrierungsschlüssel des X509-Zertifikats aktualisieren](#refresh-the-x509-certificate-registry-keys).

## <a name="configure-the-rd-licensing-service"></a>Konfigurieren des RD-Lizenzierungsdiensts

Im folgenden Verfahren wird der Server-Manager für die Konfigurationsänderungen verwendet. Weitere Informationen zum Konfigurieren und Verwenden des Server-Managers finden Sie unter [Server-Manager](../../../administration/server-manager/server-manager.md).

1. Öffnen Sie **Server-Manager**, und navigieren Sie dann zu **Remotedesktopdienste**.
2. Wählen Sie unter **Bereitstellungsübersicht** zuerst **Aufgaben** und anschließend **Bereitstellungseigenschaften bearbeiten** aus.
3. Wählen Sie **RD-Lizenzierung** und dann den passenden Lizenzierungsmodus für Ihre Bereitstellung aus (**Pro Gerät** oder **Pro Benutzer**).
4. Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres RD-Lizenzservers ein, und wählen Sie dann **Hinzufügen** aus.
5. Wenn Sie über mehrere RD-Lizenzserver verfügen, wiederholen Sie Schritt 4 für jeden Server. 
    ![Konfigurationsoptionen für den RD-Lizenzserver in Server-Manager.](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

## <a name="refresh-the-x509-certificate-registry-keys"></a>Aktualisieren der Registrierungsschlüssel des X509-Zertifikats

> [!IMPORTANT]  
> Befolgen Sie die Anweisungen in diesem Abschnitt sorgfältig. Es können schwerwiegende Probleme auftreten, wenn fehlerhafte Änderungen an der Registrierung vorgenommen werden. Bevor Sie die Registrierung ändern, müssen Sie die [Registrierung sichern](https://support.microsoft.com/help/322756), damit Sie sie bei einem Fehler wiederherstellen können.

Um dieses Problem zu beheben, sichern Sie die Registrierungsschlüssel des X509-Zertifikats, entfernen Sie sie anschließend, starten Sie den Computer neu, und aktivieren Sie den RD-Lizenzierungsserver erneut. Führen Sie die folgenden Schritte aus.

> [!NOTE]
> Führen Sie den folgenden Vorgang auf jedem der RDSH-Server durch.

So aktivieren Sie den RD-Lizenzierungsserver erneut

1. Öffnen Sie den Registrierungs-Editor, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**.
2. Wählen Sie im Menü „Registrierung“ **Registrierungsdatei exportieren** aus.
3. Geben Sie **exportiertes Zertifikat** im Feld **Dateiname** ein, und wählen Sie dann **Speichern** aus.
4. Klicken Sie mit der rechten Maustaste auf jeden der folgenden Werte, wählen Sie **Löschen** und anschließend **Ja** aus, um die Löschung zu bestätigen:  
      - **Zertifikat**
      - **X509-Zertifikat**
      - **X509-Zertifikat-ID**
      - **X509-Zertifikat2**
5. Schließen Sie den Registrierungs-Editor, und starten Sie den RDSH-Server neu.