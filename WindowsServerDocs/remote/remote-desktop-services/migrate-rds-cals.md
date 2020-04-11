---
title: Migrieren von Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)
description: In diesem Artikel erfährst du, wie du deine Remotedesktopdienste-Clientzugriffslizenzen zu neuen Windows Server 2016-Lizenzservern migrierst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.topic: article
ms.assetid: 91bdedce-6145-469f-b72e-7e113c4391e9
author: christianmontoya
manager: scottman
ms.openlocfilehash: 5d95c2bc3a92a8cdcba4b308c88d94cb9af6d2a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855993"
---
# <a name="migrate-your-remote-desktop-services-client-access-licenses-rds-cals"></a>Migrieren von Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)

RDS-CALs können auf drei Arten migriert werden:
1. Automatische Verbindungsmethode: Bei dieser empfohlenen Methode wird über das Internet direkt mit dem Microsoft Clearinghouse (ausgehende Verbindung über den TCP-Port 443) kommuniziert.  
2. Webbrowser: Diese Migrationsmethode kann verwendet werden, wenn der Server, auf dem der Remotedesktoplizenzierungs-Manager ausgeführt wird, nicht mit dem Internet verbunden ist und der Administrator über ein separates Gerät auf das Internet zugreifen kann. Die URL für die Webmigrationsmethode wird im Assistenten zum Verwalten von RDS-CALs angezeigt. 
3. Telefon: Bei dieser Methode kann der Administrator den Migrationsprozess telefonisch mit einem Microsoft-Mitarbeiter durchführen. Die Telefonnummer hängt davon ab, welches Land/welche Region du im Serveraktivierungs-Assistenten ausgewählt hast, und wird im Assistenten zum Verwalten von RDS-CALs angezeigt.

In diesem Artikel werden unter [Einrichten der RDS-CAL-Migrationsmethode](#establish-rds-cal-migration-method) zunächst die allgemeinen Schritte erläutert, die bei allen RDS-CAL-Migrationsmethoden ausgeführt werden müssen. Die spezifischen Schritte für die jeweilige Migrationsmethode werden dann unter [Migrieren von RDS-CALs](#migrate-rds-cals) beschrieben.

Unabhängig von der Migrationsmethode musst du mindestens der lokalen Gruppe „Administratoren“ angehören, um die Migrationsschritte ausführen zu können.

## <a name="establish-rds-cal-migration-method"></a>Einrichten der RDS-CAL-Migrationsmethode

1. Öffne auf dem Lizenzserver den **Remotedesktoplizenzierungs-Manager**. Klicke auf **Start > Verwaltung**. Öffne das Verzeichnis **Remotedesktopdienste**, und starte **Remotedesktoplizenzierungs-Manager**.)
2. Überprüfe die Verbindungsmethode für den Remotedesktop-Lizenzserver: Klicke hierzu mit der rechten Maustaste auf den Lizenzserver, zu dem du die RDS-CALs migrieren möchtest, und klicke anschließend auf **Eigenschaften**. Überprüfe auf der Registerkarte **Verbindungsmethode** die **Verbindungsmethode**. Sie kann über das Dropdownmenü geändert werden. Klicken Sie auf **OK**.
3. Klicke mit der rechten Maustaste auf den Lizenzserver, zu dem du die RDS-CALs migrieren möchtest, und klicke anschließend auf **RDS-CALs verwalten**.
4. Führe die Schritte des Assistenten aus, um zur Seite **Aktionsauswahl** zu gelangen. Klicke auf **Clientzugriffslizenzen für Remotedesktopdienste von anderem Lizenzserver zu diesem Lizenzserver migrieren**.
6. Wähle den Grund für die Migration der RDS-CALs aus, und klicke anschließend auf **Weiter**. Hierzu stehen Ihnen folgende Optionen zur Verfügung:
    - Der Quelllizenzserver wird durch diesen Lizenzserver ersetzt.
    - Der Quelllizenzserver kann nicht mehr ausgeführt werden.
7. Die nächste Seite des Assistenten hängt vom ausgewählten Migrationsgrund ab.
    - Wenn du als Grund für die Migration der RDS-CALs die Option **Der Quelllizenzserver wird durch diesen Lizenzserver ersetzt.** ausgewählt hast, wird die Seite **Informationen zum Quelllizenzserver** angezeigt.
    
       Gib auf der Seite „Informationen zum Quelllizenzserver“ den Namen oder die IP-Adresse des Quelllizenzservers ein.

       Wenn der Quelllizenzserver im Netzwerk verfügbar ist, klicke auf **Weiter**. Der Assistent kontaktiert den Quelllizenzserver. Wenn auf dem Quelllizenzserver ein Betriebssystem vor Windows Server 2008 R2 ausgeführt wird oder der Quelllizenzserver deaktiviert ist, wirst du daran erinnert, dass du die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernen musst. Nach Bestätigung dieser Information wird die Seite **Schlüsselpaket für die Clientlizenz anfordern** angezeigt.

       Ist der Quelllizenzserver im Netzwerk nicht verfügbar, wähle **Der angegebene Quelllizenzserver ist im Netzwerk nicht verfügbar.** aus. Gib das auf dem Quelllizenzserver ausgeführte Betriebssystem und die Lizenzserver-ID für den Quelllizenzserver an. Nach dem Klicken auf **Weiter** wirst du daran erinnert, dass du die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernen musst. Nach Bestätigung dieser Information wird die Seite **Schlüsselpaket für die Clientlizenz anfordern** angezeigt.

    - Wenn du als Grund für die Migration der RDS-CALs die Option **Der Quelllizenzserver kann nicht mehr ausgeführt werden.** ausgewählt hast, wirst du daran erinnert, dass du die RDS-CALs nach Abschluss des Assistenten manuell vom Quelllizenzserver entfernen musst. Nach Bestätigung dieser Information wird die Seite **Schlüsselpaket für die Clientlizenz anfordern** angezeigt.

Als Nächstes müssen die CALs migriert werden. Verwende die folgenden Informationen, um den Assistenten abzuschließen. Der Inhalt des Assistenten hängt davon ab, welche Verbindungsmethode du weiter oben in Schritt 2 ausgewählt hast.

## <a name="migrate-rds-cals"></a>Migrieren der RDS-CALs

Lizenzen können auf drei Arten zum Ziellizenzserver migriert werden. Fahre mit den entsprechenden Schritten für die in Schritt 2 überprüfte **Verbindungsmethode** fort:
  - [Automatische Verbindungsmethode](#automatic-connection-method)
  - [Webbrowser](#using-a-web-browser)
  - [Telefon](#using-a-telephone)

### <a name="automatic-connection-method"></a>Automatische Verbindungsmethode

1. Wähle auf der Seite **Lizenzprogramm** das Programm aus, über das du deine RDS-CALs erworben hast, und klicke anschließend auf **Weiter**.
2. Gib die erforderlichen Informationen ein (in der Regel einen Lizenzcode oder eine Vertragsnummer, abhängig vom **Lizenzprogramm**), und klicke anschließend auf **Weiter**. Weitere Informationen findest du in der Dokumentation, die du beim Erwerb der RDS-CALs erhalten hast.
4. Wähle die Produktversion, den Lizenztyp und die Anzahl von RDS-CALs für deine Umgebung auf der Grundlage deines RDS-CAL-Kaufvertrags aus, und klicke anschließend auf **Weiter**.
5. Es wird automatisch eine Verbindung mit dem Microsoft Clearinghouse hergestellt, das die Anforderung verarbeitet. Anschließend werden die RDS-CALs zum Lizenzserver migriert.
6. Klicke auf **Fertig stellen**, um die RDS-CAL-Migration abzuschließen.

### <a name="using-a-web-browser"></a>Webbrowser
1. Klicke auf der Seite **Schlüsselpaket für die Clientlizenz anfordern** auf den Link, um eine Verbindung mit der Lizenzierungswebsite für Remotedesktopdienste herzustellen.
   Wenn du den Remotedesktoplizenzierungs-Manager auf einem Computer ohne Internetkonnektivität ausführst, notiere dir die Adresse der Lizenzierungswebsite für Remotedesktopdienste, und stelle anschließend auf einem Computer mit Internetkonnektivität eine Verbindung mit der Website her. 
2. Wähle auf der Lizenzierungswebsite für Remotedesktopdienste unter **Option auswählen** die Option **CALs verwalten** aus, und klicke anschließend auf **Weiter**.
3. Gib die folgenden erforderlichen Informationen an, und klicke anschließend auf **Weiter**:
    - **ID des Ziellizenzservers**: Eine 35-stellige, in Fünfergruppen unterteilte Nummer, die im Assistenten zum Verwalten von RDS-CALs auf der Seite **Schlüsselpaket für die Clientlizenz anfordern** angezeigt wird.
    - **Grund für die Wiederherstellung**: Wähle den Grund für die Migration der RDS-CALs aus.
    - **Lizenzprogramm**: Wähle das Programm aus, über das du deine RDS-CALs erworben hast.
4. Gib die folgenden erforderlichen Informationen an, und klicke anschließend auf **Weiter**:
   - Nachname
   - Vorname
   - Firmenname
   - Land/Region

     Du kannst auch optionale Informationen wie Firmenadresse, E-Mail-Adresse und Telefonnummer angeben. Im Feld „Organisationseinheit“ kannst du die Einheit in deiner Organisation beschreiben, für die dieser Lizenzserver verwendet wird.

5. Welche Informationen auf der nächsten Seite angegeben werden müssen, hängt davon ab, welches Lizenzprogramm du auf der vorherigen Seite ausgewählt hast. In den meisten Fällen muss entweder ein Lizenzcode oder eine Vertragsnummer angegeben werden. Weitere Informationen findest du in der Dokumentation, die du beim Erwerb der RDS-CALs erhalten hast. Darüber hinaus musst du Art und Menge der RDS-CALs angeben, die du zum Lizenzserver migrieren möchtest.
6. Klicken Sie, nachdem Sie die erforderlichen Informationen eingegeben haben, auf **Weiter**.
7. Vergewissere dich, dass alle eingegebenen Informationen korrekt sind, und klicke anschließend auf **Weiter**, um deine Anforderung an das Microsoft Clearinghouse zu übermitteln. Daraufhin wird auf der Webseite eine vom Microsoft Clearinghouse generierte Lizenzschlüsselpaket-ID angezeigt.

   > [!IMPORTANT] 
   > Bewahre eine Kopie der Lizenzschlüsselpaket-ID auf. Diese Information erleichtert die Kommunikation mit dem Microsoft Clearinghouse, falls du Unterstützung bei der Wiederherstellung der RDS-CALs benötigst.

8. Gib auf der Seite **Schlüsselpaket für die Clientlizenz anfordern** die Lizenzschlüsselpaket-ID ein, und klicke anschließend auf **Weiter**, um die RDS-CALs zu deinem Lizenzserver zu migrieren.
9. Klicke auf **Fertig stellen**, um die RDS-CAL-Migration abzuschließen.

### <a name="using-a-telephone"></a>Telefon
1. Setze dich unter der auf der Seite **Schlüsselpaket für die Clientlizenz anfordern** angegebenen Telefonnummer mit dem Microsoft Clearinghouse in Verbindung. Gib die ID deines Remotedesktop-Lizenzservers sowie die erforderlichen Informationen für das Lizenzierungsprogramm an, über das du deine RDS-CALs erworben hast. Der Mitarbeiter bearbeitet deine RDS-CAL-Migrationsanforderung und vergibt eine eindeutige ID für die RDS-CALs. Diese eindeutige ID wird als **Lizenzschlüsselpaket-ID** bezeichnet.

   > [!IMPORTANT]
   > Bewahre eine Kopie der Lizenzschlüsselpaket-ID auf. Diese Information erleichtert die Kommunikation mit dem Microsoft Clearinghouse, falls du Unterstützung bei der Wiederherstellung der RDS-CALs benötigst.

2. Gib auf der Seite **Schlüsselpaket für die Clientlizenz anfordern** die Lizenzschlüsselpaket-ID ein, und klicke anschließend auf **Weiter**, um die RDS-CALs zu deinem Lizenzserver zu migrieren.
3. Klicke auf **Fertig stellen**, um die RDS-CAL-Migration abzuschließen.
