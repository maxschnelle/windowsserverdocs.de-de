---
title: Erstellen einer Dateiablaufaufgabe
description: Dieser Artikel beschreibt den Prozess der Erstellung einer Datei Verwaltungsaufgabe für Dateien, die ablaufen.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0ff4b46064ca780d63c6f06898c114cb180c3665
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971127"
---
# <a name="create-a-file-expiration-task"></a>Erstellen einer Dateiablaufaufgabe

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das folgende Verfahren führt Sie durch die Schritte zum Erstellen einer Datei Verwaltungsaufgabe für ablaufende Dateien. Datei Ablauf Tasks werden verwendet, um automatisch alle Dateien, die bestimmte Kriterien erfüllen, in ein bestimmtes Ablauf Verzeichnis zu verschieben, in dem ein Administrator diese Dateien sichern und löschen kann.

Wenn eine Datei Ablauf Aufgabe ausgeführt wird, wird ein neues Verzeichnis innerhalb des Ablauf Verzeichnisses erstellt, gruppiert nach dem Servernamen, auf dem die Aufgabe ausgeführt wurde.

Der neue Verzeichnisname basiert auf dem Namen der Dateiverwaltungsaufgabe und der Ausführungszeit.Wird eine abgelaufene Datei gefunden, wird sie in das neue Verzeichnis verschoben, ohne dabei die ursprüngliche Verzeichnisstruktur zu verändern.

## <a name="to-create-a-file-expiration-task"></a>So erstellen Sie eine Datei Ablauf Aufgabe

1. Klicken Sie auf den Knoten **Dateiverwaltungsaufgaben**.

2. Klicken Sie mit der rechten Maustaste auf **Datei Verwaltungsaufgaben**, und klicken Sie dann auf **Datei Verwaltungsaufgabe erstellen** (oder klicken Sie im **Aktions** Bereich auf **Datei Verwaltungsaufgabe erstellen** ). Daraufhin wird das Dialogfeld **Dateiverwaltungsaufgabe erstellen** geöffnet.

3. Geben Sie auf der Registerkarte **Allgemein** folgende Informationen ein:

   -   **Name**: Geben Sie einen Namen für die neue Aufgabe ein.

   -   **Beschreibung**. Geben Sie eine optionale aussagekräftige Bezeichnung für die Aufgabe ein.

   -   **Umfang**. Fügen Sie mithilfe der Schaltfläche **Hinzufügen** die Verzeichnisse hinzu, mit denen diese Aufgabe arbeiten soll. Optional können Verzeichnisse mithilfe der Schaltfläche " **Entfernen** " aus der Liste entfernt werden. Die Datei Verwaltungsaufgabe gilt für alle Ordner und deren Unterordner in dieser Liste.

4. Geben Sie auf der Registerkarte **Aktion** folgende Informationen ein:

   - **Art:** Wählen Sie im Dropdown Feld **Datei Ablauf** aus.

   - **Ablaufverzeichnis** Wählen Sie ein Verzeichnis aus, in das die Dateien abgelaufen sein sollen.

     > [!Warning]
     > Wählen Sie dabei kein Verzeichnis aus, das sich gemäß der Definition im vorangegangenen Schritt im Bereich der Aufgabe befindet. Andernfalls entsteht unter Umständen eine iterative Schleife, die zu Systeminstabilität und Datenverlusten führen kann.

5. Optional können Sie auf der Registerkarte **Benachrichtigung** auf **Hinzufügen** klicken, um E-Mail-Benachrichtigungen zu senden, Ereignisse zu protokollieren oder um einen Befehl oder ein Skript für eine minimale Anzahl von Tagen auszuführen, bevor von der Aufgabe eine Aktion für die Datei ausgeführt wird.

   - Geben Sie im Kombinations Feld **Anzahl der Tage vor dem Ausführen der Aufgabe zum Senden von Benachrichtigungen** einen Wert ein, oder wählen Sie einen Wert aus, um die Mindestanzahl von Tagen anzugeben, bevor eine Datei bearbeitet wird, in der eine Benachrichtigung gesendet wird.

     > [!Note]
     > Benachrichtigungen werden nur gesendet, wenn eine Aufgabe ausgeführt wird. Wenn die angegebene Mindestanzahl von Tagen, für die eine Benachrichtigung gesendet wird, nicht mit einer geplanten Aufgabe übereinstimmt, wird die Benachrichtigung am Tag der vorhergehenden geplanten Aufgabe gesendet.

   - Klicken Sie zum Konfigurieren von e-Mail-Benachrichtigungen auf die Registerkarte **e-Mail** , und geben Sie die folgenden Informationen ein

     - Wenn Sie Administratoren benachrichtigen möchten, wenn ein Schwellenwert erreicht wird, aktivieren Sie das Kontrollkästchen **e-Mail an folgende Administratoren senden** , und geben Sie dann die Namen der Administrator Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie das Format <em>account@domain</em> , und verwenden Sie Semikolons zum Trennen mehrerer Konten.

     - Wenn Sie eine e-Mail an die Person senden möchten, deren Dateien ablaufen, aktivieren Sie das Kontrollkästchen **e-Mail an den Benutzer senden, dessen Dateien demnächst ablaufen** .

     - Um die Meldung zu konfigurieren, bearbeiten Sie die Standard Betreffzeile und den Nachrichtentext, die bereitgestellt werden. Der Text in Klammern fügt Variablen Informationen über das Kontingent Ereignis ein, das die Benachrichtigung verursacht hat. Beispielsweise fügt die ** \[ Quelldatei Besitzer \] ** -Variable den Namen des Benutzers ein, dessen Datei demnächst abläuft. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.

     - Um eine Liste der Dateien anzufügen, die ablaufen, klicken Sie auf **an die e-Mail-Liste der Dateien anfügen, für die die Aktion ausgeführt**werden soll, und geben Sie einen Wert ein, oder wählen Sie einen Wert für **Maximale Anzahl von Dateien in der Liste**aus.

     - Um zusätzliche Header (einschließlich from, CC, BCC und Reply-to) zu konfigurieren, klicken Sie auf **zusätzliche e-Mail-Header**.

   - Wenn Sie ein Ereignis protokollieren möchten, klicken Sie auf die Registerkarte **Ereignisprotokoll** , und aktivieren Sie das Kontrollkästchen **Warnung an Ereignisprotokoll senden** , und bearbeiten Sie dann den Standardprotokoll Eintrag.

   - Wenn Sie einen Befehl oder ein Skript ausführen möchten, klicken Sie auf die Registerkarte **Befehl** , und aktivieren Sie das Kontrollkästchen **diesen Befehl oder Skript ausführen** . Geben Sie dann den Befehl ein, oder klicken Sie auf **Durchsuchen** , um den Speicherort des Skripts zu suchen. Sie können auch Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder das Skript auswählen oder die Einstellung für die Befehls Sicherheit ändern.

6. Optional: Generieren Sie mithilfe der Registerkarte **Bericht** Protokolle oder Speicherberichte.

   - Aktivieren Sie das Kontrollkästchen **Protokoll generieren** , und wählen Sie ein oder mehrere verfügbare Protokolle aus, um Protokolle zu generieren.

   - Zum Generieren von Berichten aktivieren Sie das Kontrollkästchen **Bericht generieren** , und wählen Sie dann ein oder mehrere verfügbare Berichtsformate aus.

   - Aktivieren Sie das Kontrollkästchen **Berichte an folgende Administratoren senden** , um per e-Mail generierte Protokolle oder Speicher Berichte zu erstellen, und geben Sie einen oder mehrere Administrator-e-Mail-Empfänger im Format ein <em>account@domain</em> . Verwenden Sie ein Semikolon, um mehrere Adressen voneinander zu trennen.

     > [!Note]
     > Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.

7. Optional: Verwenden Sie die Registerkarte **Bedingung**, um diese Aufgabe nur für Dateien auszuführen, von denen bestimmte Bedingungen erfüllt werden. Die folgenden Einstellungen sind verfügbar:

    -   **Eigenschafts Bedingungen**. Klicken Sie auf **Hinzufügen** , um eine neue Bedingung basierend auf der Klassifizierung der Datei zu erstellen. Dadurch wird das Dialogfeld **Eigenschaften Bedingung** geöffnet, in dem Sie eine Eigenschaft, einen Operator, der für die Eigenschaft auszuführen ist, und den Wert, mit dem die Eigenschaft verglichen werden soll, auswählen können. Nachdem Sie auf " **OK**" geklickt haben, können Sie weitere Bedingungen erstellen oder eine vorhandene Bedingung bearbeiten oder entfernen.

    -   **Tage seit der letzten Änderung der Datei**. Aktivieren Sie das Kontrollkästchen, und geben Sie dann eine Anzahl von Tagen in das Drehfeld ein. Dies führt dazu, dass die Datei Verwaltungsaufgabe nur auf Dateien angewendet wird, die seit mehr als der angegebenen Anzahl von Tagen nicht geändert wurden.

    -   **Tage seit dem letzten Zugriff**auf die Datei. Aktivieren Sie das Kontrollkästchen, und geben Sie dann eine Anzahl von Tagen in das Drehfeld ein. Wenn der Server für die Nachverfolgung von Zeitstempeln für den letzten Zugriff auf Dateien konfiguriert ist, führt dies dazu, dass die Datei Verwaltungsaufgabe nur auf Dateien angewendet wird, auf die seit mehr als der angegebenen Anzahl von Tagen nicht mehr zugegriffen wurde. Wenn der Server nicht für die Nachverfolgung der Zugriffszeiten konfiguriert ist, ist dieser Zustand wirkungslos.

    -   **Tage seit der Erstellung der Datei**. Aktivieren Sie das Kontrollkästchen, und geben Sie dann eine Anzahl von Tagen in das Drehfeld ein. Dies führt dazu, dass die Aufgabe nur auf Dateien angewendet wird, die mindestens vor der angegebenen Anzahl von Tagen erstellt wurden.

    -   **Effektive Starts**. Legen Sie ein Datum fest, an dem diese Datei Verwaltungsaufgabe die Verarbeitung von Dateien starten soll. Diese Option ist nützlich, um die Aufgabe zu verzögern, bis Sie die Möglichkeit haben, Benutzer zu benachrichtigen oder andere Vorbereitungen im Voraus zu treffen.

8. Klicken Sie auf der Registerkarte **Zeitplan** auf **Zeitplan erstellen**, und klicken Sie dann im Dialogfeld **Zeitplan** auf **neu**. Hiermit wird ein Standard Zeitplan für 9:00 Uhr angezeigt. täglich, Sie können den Standard Zeitplan jedoch ändern. Wenn Sie die Konfiguration des Zeitplans abgeschlossen haben, klicken Sie auf **OK** , und klicken Sie dann erneut auf **OK** .

## <a name="additional-references"></a>Weitere Verweise

-   [Klassifizierungsverwaltung](classification-management.md)
-   [Dateiverwaltungsaufgaben](file-management-tasks.md)