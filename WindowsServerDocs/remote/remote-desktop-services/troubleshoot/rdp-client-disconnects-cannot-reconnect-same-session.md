---
title: Remotedesktopclient wird getrennt und kann keine Verbindung mit der gleichen Sitzung wiederherstellen
description: Behandeln eines Problems, bei dem der Remotedesktopclient getrennt wird und keine Verbindung mit der gleichen Sitzung wiederherstellen kann.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0d116c99b7c8b1daffc4ec58bd93414781eea321
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857203"
---
# <a name="remote-desktop-client-disconnects-and-cant-reconnect-to-the-same-session"></a>Remotedesktopclient wird getrennt und kann keine Verbindung mit der gleichen Sitzung wiederherstellen

Nachdem der Remotedesktopclient die Verbindung mit dem Remotedesktop verloren hat, kann der Client die Verbindung nicht sofort wiederherstellen. Der Benutzer erhält eine der folgenden Fehlermeldungen:

  - Der Client konnte aufgrund eines Sicherheitsfehlers keine Verbindung mit dem Terminalserver herstellen. Vergewissern Sie sich, dass Sie beim Netzwerk angemeldet sind, und versuchen Sie nochmals, eine Verbindung herzustellen.
  - Remotedesktop getrennt. Aufgrund eines Sicherheitsfehlers konnte der Client keine Verbindung mit dem Remotecomputer herstellen. Stellen Sie sicher, dass Sie am Netzwerk angemeldet sind, und versuchen Sie dann noch einmal, eine Verbindung herzustellen.

Wenn der Remotedesktopclient wieder eine Verbindung herstellt, stellt der RDSH-Server bei der erneuten Clientverbindung eine Verbindung mit einer neuen Sitzung anstatt mit der ursprünglichen Sitzung her. Wenn Sie jedoch auf dem RDSH-Server nachsehen, ist die ursprüngliche Sitzung nach wie vor aktiv und nicht in einen Trennungszustand gewechselt.

Um dieses Problem zu umgehen, können Sie die Richtlinie **„Keep Alive“-Verbindungsintervall konfigurieren** im Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** aktivieren. Wenn Sie diese Richtlinie aktivieren, müssen Sie ein Keep-Alive-Intervall angeben. Das Keep-Alive-Intervall bestimmt, wie oft der Server den Sitzungsstatus überprüft (Angabe in Minuten).

Dieses Problem kann auch behoben werden, indem Sie Ihre Authentifizierungs- und Konfigurationseinstellungen neu konfigurieren. Sie können diese Einstellungen entweder auf Serverebene oder mithilfe von Gruppenrichtlinienobjekten (Group Policy Objects, GPOs) neu konfigurieren. So konfigurieren Sie die Einstellungen neu Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Sicherheit**:

1. Öffnen Sie auf dem RD-Sitzungshostserver die **Konfiguration des Remotedesktop-Sitzungshosts**.
2. Klicken Sie unter **Verbindungen** mit der rechten Maustaste auf den Namen der Verbindung, und wählen Sie dann **Eigenschaften**.
3. Wählen Sie im Dialogfeld **Eigenschaften** für die Verbindung auf der Registerkarte **Allgemein** in der Schicht **Sicherheit** eine Sicherheitsmethode aus.
4. Wechseln Sie zur **Verschlüsselungsstufe**, und wählen Sie die gewünschte Ebene aus. Sie können zwischen **Niedrig**, **Clientkompatibel**, **Hoch** und **FIPS-konform** wählen.

> [!NOTE]  
>  - Wenn für Verbindungen zwischen Clients und RD-Sitzungshostservern die höchste Verschlüsselungsstufe erforderlich ist, verwenden Sie FIPS-konforme Verschlüsselung.
>  - Alle Einstellungen zur Verschlüsselungsstufe, die Sie in Gruppenrichtlinien konfigurieren, setzen die Einstellungen außer Kraft, die Sie mithilfe des Konfigurationstools für Remotedesktopdienste konfiguriert haben. Und wenn Sie die Richtlinie [Systemkryptografie: FIPS-konforme Algorithmen für Verschlüsselung, Hashing und Signatur verwenden](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing) aktivieren, setzt diese Einstellung die Richtlinie **Verschlüsselungsstufe der Clientverbindung festlegen** außer Kraft. Die Richtlinie für Systemkryptografie befindet sich im Ordner **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\Lokale Richtlinien\\Sicherheitsoptionen**.
>  - Wenn Sie die Verschlüsselungsstufe ändern, wird die neue Verschlüsselungsstufe wirksam, sobald sich das nächste Mal ein Benutzer anmeldet. Wenn Sie mehrere Verschlüsselungsstufen auf einem Server unterstützen müssen, installieren Sie mehrere Netzwerkadapter, und konfigurieren Sie jeden Adapter separat.
>  - Um zu überprüfen, ob ein Zertifikat über einen entsprechenden privaten Schlüssel verfügt, klicken Sie in „Remotedesktopdienste-Konfiguration“ mit der rechten Maustaste auf die Verbindung, für die Sie das Zertifikat anzeigen möchten, wählen Sie **Allgemein** und dann **Bearbeiten**. Wählen Sie anschließend **Zertifikat anzeigen** aus. Auf der Registerkarte **Allgemein** sollte die Aussage „Sie verfügen über einen privaten Schlüssel, der diesem Zertifikat entspricht“ angezeigt werden, sofern ein Schlüssel vorhanden ist. Sie können diese Informationen auch über das Zertifikat-Snap-In abrufen.
>  - FIPS-konforme Verschlüsselung (die Richtlinie **Systemkryptografie: FIPS-konforme Algorithmen für Verschlüsslung, Hashing und Signatur verwenden** oder die Einstellung **FIPS-konform** in der Remotedesktop-Serverkonfiguration) verschlüsselt und entschlüsselt die zwischen Server und Client ausgetauschten Daten mit Verschlüsselungsalgorithmen nach dem FIPS 140-1-Standard (Federal Information Processing Standard ) mithilfe von Microsoft-Kryptografiemodulen. Weitere Informationen finden Sie unter [FIPS 140-Überprüfung](https://docs.microsoft.com/windows/security/threat-protection/fips-140-validation).
>  - Bei der Einstellung **Hoch** werden zwischen Server und Client gesendete Daten mithilfe von starker 128-Bit-Verschlüsselung verschlüsselt.
>  - Bei der Einstellung **Clientkompatibel** werden die zwischen dem Client und dem Server ausgetauschten Daten mit der vom Client unterstützten maximalen Schlüsselstärke verschlüsselt.
>  - Die Einstellung **Niedrig** verschlüsselt vom Client an den Server gesendete Daten mit 56-Bit-Verschlüsselung.
