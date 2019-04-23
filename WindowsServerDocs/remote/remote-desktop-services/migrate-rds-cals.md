---
title: Migrieren von Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)
description: Dieser Artikel beschreibt, wie Sie Remote Desktop Services Client Access Licenses zu neuen Windows Server 2016-Lizenzserver zu migrieren.
ms.custom: na
ms.prod: windows-server-threshold
msreviewer: ''
nams.suite: ''
nams.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91bdedce-6145-469f-b72e-7e113c4391e9
author: christianmontoya
manager: scottman
ms.openlocfilehash: cb30c703adb7e3a791e41caab4561300faa8fcd3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845021"
---
# <a name="migrate-your-remote-desktop-services-client-access-licenses-rds-cals"></a>Migrieren von Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)

Sie haben drei Optionen zum Migrieren Ihre RDS-CALs:
1. Automatische Verbindung-Methode: Diese empfohlenen Methode, die über TCP-Port 443 über das Internet direkt an das Microsoft Clearinghouse ausgehende kommuniziert werden.  
2. Verwenden einen Webbrowser ein: Diese Methode ermöglicht die Migration, wenn der Server mit den Remotedesktoplizenzierungs-Manager-Tool keine Internetverbindung verfügt, aber der Administrator auf einem separaten Gerät über eine Internetverbindung verfügt. Die URL für die Webmethode für die Migration wird in den Assistenten zum Verwalten von RDS-CALs angezeigt. 
3. Per Telefon: Diese Methode kann der Administrator per Telefon mit einem Microsoft-Mitarbeiter den Migrationsprozess abzuschließen. Die Telefonnummer wird durch das Land bzw. die Region bestimmt, die Sie in der Serveraktivierungs-Assistent ausgewählt haben, und werden im Assistenten für die Verwaltung von RDS-CALs angezeigt.

In diesem Artikel die [herzustellen RDS-CAL-Migrationsmethode](#establish-RDS-CAL-migration-method) werden die allgemeinen Schritte, die häufig über alle RDS-CAL-Migrationsmethode während [Migrieren der RDS-CALs](#migrate-RDS-CALs) werden die Schritte für jede Migration -Methode.

Unabhängig von Migrationsmethode müssen Sie mindestens Mitglied der lokalen Gruppe "Administratoren" Ausführen der Migrationsschritte sein.


## <a name="establish-rds-cal-migration-method"></a>Einrichten von RDS-CAL-Migration-Methode
1. Öffnen Sie auf dem Lizenzserver **Remotedesktoplizenzierungs-Manager**. (Klicken Sie auf **Start > Verwaltung**. Geben Sie die **Remote Desktop Services** Verzeichnis, und starten **Remotedesktoplizenzierungs-Manager**.)
2. Überprüfen Sie die Verbindungsmethode für den Remotedesktop-Lizenzserver: mit der rechten Maustaste auf die Sie migrieren möchten die RDS-CALs, und klicken Sie dann auf den Lizenzserver **Eigenschaften**. Auf der **Verbindungsmethode** Registerkarte, vergewissern Sie sich die **Verbindungsmethode** -können Sie sie im Dropdownmenü ändern. Klicken Sie auf **OK**.
3. Mit der rechten Maustaste auf die Sie migrieren möchten die RDS-CALs, und klicken Sie dann auf den Lizenzserver **RDS-CALs verwalten**.
4. Führen Sie die Schritte im Assistenten, um die **Aktionsauswahl** Seite. Klicken Sie auf **migrieren RDS-CALs in einen anderen Lizenzserver zu diesem Lizenzserver**.
6. Wählen Sie den Grund für die Migration der RDS-CALs, und klicken Sie dann auf **Weiter**. Hierzu stehen Ihnen folgende Optionen zur Verfügung:
    - Der Quelllizenzserver wird durch diesen Lizenzserver ersetzt wird.
    - Der Quelllizenzserver funktioniert nicht mehr.
7. Die nächste Seite im Assistenten hängt von der Migration Grund, den Sie ausgewählt haben.
    - Wenn Sie ausgewählt haben **der Quelllizenzserver ist vom Lizenzserver ersetzten** als Grund für das Migrieren der RDS-CALs, die **Quellserverinformationen für die Lizenz** angezeigt wird.
    
       Geben Sie auf der Seite Informationen zu Quelllizenzserver den Namen oder die IP-Adresse des Quellservers Lizenz aus.

       Wenn der Quelllizenzserver im Netzwerk verfügbar ist, klicken Sie auf **Weiter**. Der Assistent kontaktiert den Quelllizenzserver. Wenn der Quelllizenzserver ein Betriebssystem vor Windows Server 2008 R2 ausgeführt wird, oder der Quelllizenzserver ist deaktiviert, werden Sie daran erinnert, dass die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernt werden müssen. Nachdem Sie bestätigt haben, dass Sie verstehen, dass diese Anforderung die **Clientlizenz Schlüssel anfordern** Seite wird angezeigt.

       Wenn der Quelllizenzserver nicht im Netzwerk verfügbar ist, wählen Sie **angegebenen Quelllizenzserver ist nicht verfügbar ist, im Netzwerk**. Geben Sie das Betriebssystem, das der Quelllizenzserver ausgeführt wird, und geben Sie dann die Lizenzserver-ID für den Quellserver-Lizenz. Nachdem Sie auf **Weiter**, Sie daran erinnert, dass die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernt werden müssen. Nachdem Sie bestätigt haben, dass Sie verstehen, dass diese Anforderung die **Clientlizenz Schlüssel anfordern** Seite wird angezeigt.

    - Wenn Sie ausgewählt haben **der Quelllizenzserver funktioniert nicht mehr** als Grund für die Migration der RDS-CALs, Sie daran erinnert, dass die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernt werden müssen. Nachdem Sie bestätigt haben, dass Sie verstehen, dass diese Anforderung die **Clientlizenz Schlüssel anfordern** Seite wird angezeigt.

Der nächste Schritt ist die Clientzugriffslizenzen migrieren – verwenden die folgenden Informationen, um den Assistenten abzuschließen. Beachten Sie, dass im Assistenten finden Sie auf die Verbindungsmethode abhängt, die Sie in Schritt2 oben identifiziert.

## <a name="migrate-rds-cals"></a>Migrieren der RDS-CALs
Es gibt drei Mechanismen Lizenzen auf den Ziel-Lizenzserver zu migrieren. die Schritte für die **Verbindungsmethode** überprüft, die in Schritt2:
  - [Automatische Verbindung-Methode](#Automatic-connection-method)
  - [Mithilfe eines Webbrowsers](#Using-a-web-browser)
  - [Per Telefon](#Using-a-telephone)

### <a name="automatic-connection-method"></a>Automatische Verbindung-Methode
1. Auf der **License-Programm** Seite, wählen Sie das Programm über das Sie Ihre RDS-CALs erworben haben, und klicken Sie dann **Weiter**.
2. Geben Sie die erforderlichen Informationen (in der Regel einen Lizenzcode oder eine Vertragsnummer, je nach den **License-Programm**), und klicken Sie dann auf **Weiter**. Finden Sie in der Dokumentation bereitgestellt, wenn Sie Ihre RDS-CALs erworben haben.
4. Wählen Sie die Produktversion, Lizenztyp und Menge der RDS-CALs für Ihre Umgebung basierend auf Ihre RDS-CAL-Kaufvertrags, und klicken Sie dann auf **Weiter**.
5. Es wird automatisch eine Verbindung mit dem Microsoft Clearinghouse hergestellt, das die Anforderung verarbeitet. Die RDS-CALs werden dann auf dem Lizenzserver migriert.
6. Klicken Sie auf **Fertig stellen** um die RDS-CAL-Migration abzuschließen.

### <a name="using-a-web-browser"></a>Mithilfe eines Webbrowsers
1. Auf der **Clientlizenz Schlüssel anfordern** auf den Link, um die Verbindung mit der Remote Desktop Services Licensing-Website.
Wenn Sie Remotedesktoplizenzierungs-Manager auf einem Computer, die nicht über Internetkonnektivität verfügt ausführen, beachten Sie die Adresse für die Remote Desktop Services Licensing-Website, und verbinden Sie dann auf der Website von einem Computer, der dem Internet verbunden ist. 
2. Auf der Seite Remote Desktop Services Licensing Web unter **auswählen**Option **CALs verwalten**, und klicken Sie dann auf **Weiter**.
3. Geben Sie die folgende erforderliche Informationen ein, und klicken Sie auf **Weiter**:
    - **Lizenzserver-ID als Ziel**: Eine Nummer 35 Ziffern in Gruppen von 5 Zahlen, die auf angezeigt wird der **Clientlizenz Schlüssel anfordern** Seite im Assistenten für die Verwaltung von RDS-CALs.
    - **Grund für die Wiederherstellung**: Wählen Sie den Grund für die Migration der RDS-CALs.
    - **Lizenz Programm**: Wählen Sie das Programm, das über das Sie Ihre RDS-CALs erworben haben.
4. Geben Sie die folgende erforderliche Informationen ein, und klicken Sie auf **Weiter**:
    - Nachname
    - Vorname oder Vorname
    - Firmenname
    - Land/Region

    Sie können auch optionale Informationen angefordert werden, z. B. Unternehmensadresse, e-Mail-Adresse und Telefonnummer angeben. Im Feld Organisationseinheit können Sie die Einheit in Ihrer Organisation beschreiben, die dieser Lizenzserver verwendet.

5. Die License-Programm, das Sie auf der vorherigen Seite ausgewählt bestimmt, welche Informationen Sie benötigen, geben Sie auf der nächsten Seite. In den meisten Fällen müssen Sie entweder einen Lizenzcode oder eine Vertragsnummer angeben. Finden Sie in der Dokumentation bereitgestellt, wenn Sie Ihre RDS-CALs erworben haben. Darüber hinaus müssen Sie angeben, welche Art von RDS-CAL und die Menge, die Sie auf den Lizenzserver migrieren möchten.
6. Klicken Sie, nachdem Sie die erforderlichen Informationen eingegeben haben, auf **Weiter**.
7. Prüfen Sie alle Informationen, die Sie eingegeben haben, und klicken Sie dann **Weiter** zum Microsoft Clearinghouse anfordern. Die Webseite zeigt eine Lizenzschlüsselpaket-ID generiert, indem Sie das Microsoft Clearinghouse.

   > [!IMPORTANT] 
   > Bewahren Sie eine Kopie der Lizenz Lizenzschlüsselpaket-ID Diese Informationen für Sie erleichtern die Kommunikation mit dem Microsoft Clearinghouse, Sie Unterstützung bei der Wiederherstellung der RDS-CALs benötigen sollten.

8. Auf dem gleichen **Clientlizenz Schlüssel anfordern** Seite Geben Sie die Lizenzschlüsselpaket-ID, und klicken Sie dann auf **Weiter** die RDS-CALs auf den Lizenzserver zu migrieren.
9. Klicken Sie auf **Fertig stellen** um die RDS-CAL-Migration abzuschließen.

### <a name="using-a-telephone"></a>Per Telefon
1. Auf der **Clientlizenz Schlüssel anfordern** verwenden Sie die angezeigte Telefonnummer an, das Microsoft Clearinghouse anrufen. Teilen Sie dem Kundendienst, Ihre Remotedesktop-Lizenzserver-ID und die erforderlichen Informationen für das Lizenzierungsprogramm, das über das Sie Ihre RDS-CALs erworben haben. Der Kundendienstmitarbeiter verarbeitet Ihre Anforderung zum Migrieren der RDS-CALs und bietet Ihnen eine eindeutige ID für die RDS-CALs. Eindeutige ID wird als bezeichnet die **Lizenz Lizenzschlüsselpaket-ID**.

   > [!IMPORTANT]
   > Bewahren Sie eine Kopie der Lizenz Lizenzschlüsselpaket-ID Diese Informationen für Sie erleichtern die Kommunikation mit dem Microsoft Clearinghouse Sie Unterstützung bei der Wiederherstellung der RDS-CALs benötigen sollten.

2. Auf dem gleichen **Clientlizenz Schlüssel anfordern** Seite Geben Sie die Lizenzschlüsselpaket-ID, und klicken Sie dann auf **Weiter** die RDS-CALs auf den Lizenzserver zu migrieren.
3. Klicken Sie auf **Fertig stellen** um die RDS-CAL-Migration abzuschließen.
