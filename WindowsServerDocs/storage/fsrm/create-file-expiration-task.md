---
title: Erstellen einer Dateiablaufaufgabe
description: In diesem Artikel wird das Verfahren zum Erstellen einer Dateiablaufaufgabe für Dateien beschrieben, die in Kürze ablaufen
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b3aa535128786d0de5c1a5ef7186e26aa62b478d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859301"
---
# <a name="create-a-file-expiration-task"></a>Erstellen einer Dateiablaufaufgabe

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Die folgende Prozedur dient zum Erstellen einer Dateiverwaltungsaufgabe für ablaufende Dateien. Dateiablaufaufgaben werden verwendet, um alle Dateien, die bestimmte Kriterien erfüllen, automatisch in ein bestimmtes Ablaufverzeichnis zu verschieben.

Bei Ausführung einer Dateiablaufaufgabe wird innerhalb des Ablaufverzeichnisses ein neues Verzeichnis erstellt.

Der neue Verzeichnisname basiert auf dem Namen der Dateiverwaltungsaufgabe und der Ausführungszeit. Wird eine abgelaufene Datei gefunden, wird sie in das neue Verzeichnis verschoben, ohne dabei die ursprüngliche Verzeichnisstruktur zu verändern.

## <a name="to-create-a-file-expiration-task"></a>So erstellen Sie eine Dateiablaufaufgabe

1.  Klicken Sie auf den Knoten **Dateiverwaltungsaufgaben**.

2.  Klicken Sie mit der rechten Maustaste auf **Dateiverwaltungsaufgaben**und dann auf **Dateiverwaltungsaufgabe erstellen** (oder klicken Sie auf **Dateiverwaltungsaufgabe erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Dateiverwaltungsaufgabe erstellen** geöffnet.

3.  Geben Sie auf der Registerkarte **Allgemein** folgende Informationen ein:

    -   **Name**: Geben Sie einen Namen für die neue Aufgabe ein.  

    -   **Beschreibung** Geben Sie eine optionale aussagekräftige Bezeichnung für die Aufgabe ein.  
    
    -   **Umfang**. Fügen Sie mithilfe der Schaltfläche **Hinzufügen** die Verzeichnisse hinzu, in der diese Aufgabe angewendet werden sollen. Optional: Verzeichnisse können aus der Liste mithilfe der Schaltfläche **Entfernen** entfernt werden. Die Dateiverwaltungsaufgabe gilt für alle Ordner und die zugehörigen Unterordner in dieser Liste.

4.  Geben Sie auf der Registerkarte **Aktion** folgende Informationen ein:

    -   **Typ**. Wählen Sie im Dropdownfeld **Dateiablauf** aus.

    -   **Ablaufverzeichnis** Wählen Sie ein Verzeichnis als Ziel für abgelaufene Dateien aus.

     > [!Warning]
     > Wählen Sie dabei kein Verzeichnis aus, das sich gemäß der Definition im vorangegangenen Schritt im Bereich der Aufgabe befindet. Andernfalls entsteht unter Umständen eine iterative Schleife, die zu Systeminstabilität und Datenverlusten führen kann.

5.  Optional können Sie auf der Registerkarte **Benachrichtigung** auf **Hinzufügen** klicken, um E-Mail-Benachrichtigungen zu senden, Ereignisse zu protokollieren oder um einen Befehl oder ein Skript für eine minimale Anzahl von Tagen auszuführen, bevor von der Aufgabe eine Aktion für die Datei ausgeführt wird.

    -   Geben Sie oder wählen Sie aus dem Kombinationsfeld **Tage vor Aufgabenausführung bis zur Benachrichtigung** den Wert ein, um die minimale Anzahl von Tagen auszuwählen, in der die Datei behandelt wird, bevor eine Benachrichtigung gesendet wird.

     > [!Note]
     > Benachrichtigungen werden nur gesendet, wenn eine Aufgabe ausgeführt wird. Wenn die angegebene minimale Anzahl von Tagen zum Senden einer Benachrichtigung nicht mit einer geplanten Aufgabe übereinstimmt, wird die Benachrichtigung am Tag der vorherigen geplanten Aufgabe gesendet.

    -   Um E-Mail-Benachrichtigungen zu konfigurieren, klicken Sie auf die Registerkarte **E-Mail-Nachricht** und geben Sie folgende Informationen ein:

        -   Um Administratoren zu benachrichtigen, wenn ein Schwellenwert erreicht wird, aktivieren Sie das Kontrollkästchen **E-Mail an die folgenden Administratoren senden** und geben Sie die Namen der administrativen Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie das Format *account@domain*, und verwenden Sie Semikolons zum Trennen mehrerer Konten.  

        -   Aktivieren Sie zum Senden einer E-Mail an die Person, deren Dateien ablaufen, das Kontrollkästchen **E-Mail an den Benutzer senden, dessen Dateien demnächst ablaufen**.

        -   Um die Nachricht zu konfigurieren, ändern Sie den vorgegebenen standardmäßigen Betreff und Textkörper. Der Text in Klammern fügt die Variableninformationen über das Kontingent-Ereignis ein, das die Benachrichtigung verursacht hat. Z. B. die **\[Source File Owner\]** Variable fügt den Namen des Benutzers, dessen Datei ist in Kürze abläuft. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.

        -   Um eine Liste der Dateien einzufügen, die demnächst abläuft, klicken Sie auf **An die E-Mail-Liste der Dateien anhängen, für die die Aktion ausgeführt wird** und geben oder wählen Sie einen Wert für **Maximale Anzahl von Dateien in der Liste** aus.

        -   Wenn Sie weitere Header konfigurieren möchten (einschließlich Von, Cc, Bcc und Antwort an), klicken Sie auf **Weitere E-Mail-Kopfzeilen**.  

    -   Um ein Ereignis zu protokollieren, klicken Sie auf die Registerkarte **Ereignisprotokoll** und wählen Sie das Kontrollkästchen **Warnung an Ereignisprotokoll senden**. Bearbeiten Sie anschließend den Standard-Protokolleintrag.  

    -   Um einen Befehl oder ein Skript auszuführen, klicken Sie auf die Registerkarte **Befehl** und aktivieren Sie das Kontrollkästchen **Diesen Befehl oder dieses Skript ausführen**. Geben Sie anschließend den Befehl ein oder klicken Sie auf **Durchsuchen**, um den Speicherort zu suchen, in dem das Skript gespeichert ist. Sie können ebenfalls Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder ein Skript auswählen oder die Sicherheitsstufeneinstellungen für den Befehl ändern.

6.  Optional: Generieren Sie mithilfe der Registerkarte **Bericht** Protokolle oder Speicherberichte.

    -   Aktivieren Sie zum Erstellen der Protokolldateien das Kontrollkästchen **Protokoll erstellen** und wählen Sie dann einen oder mehrere verfügbare Protokolle.  

    -   Aktivieren Sie zum Erstellen der Berichte das Kontrollkästchen **Bericht erstellen** und wählen Sie dann einen oder mehrere verfügbare Berichtsformate aus.  

    -   Aktivieren Sie zum Erstellen von E-Mail-Protokolldateien oder Speicherberichten das Kontrollkästchen **Berichte an die folgenden Administratoren senden** und geben Sie einen oder mehrere Administratoren als E-Mail-Empfänger mit dem Format *account@domain* ein. Trennen Sie mehrere E-Mail-Adressen durch Semikola.

     > [!Note]
     > Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.
        
7. Optional: Verwenden Sie die Registerkarte **Bedingung**, um diese Aufgabe nur für Dateien auszuführen, von denen bestimmte Bedingungen erfüllt werden. Die folgenden Einstellungen sind verfügbar:

    -   **Eigenschaftenbedingungen**. Klicken Sie auf **Hinzufügen**, um basierend auf der Klassifizierung der Datei eine neue Bedingung zu erstellen. Daraufhin öffnet sich das Dialogfeld **Eigenschaftenbedingung**, das Ihnen ermöglicht, eine Eigenschaft, einen Operator zum Ausführen der Eigenschaft und den Wert der zu vergleichenden Eigenschaft auszuwählen. Nach dem Klicken auf **OK** können Sie zusätzliche Bedingungen erstellen oder eine vorhandene Bedingung bearbeiten oder entfernen.

    -   **Tage seit der letzten Dateiänderung**. Klicken Sie auf das Kontrollkästchen und geben Sie die Anzahl der Tage in das Drehfeld ein. Dadurch wird die Dateiverwaltungsaufgabe nur auf Dateien angewendet, die nicht seit mehr als der angegebenen Anzahl von Tagen geändert wurden.

    -   **Tage seit letztem Zugriff auf die Datei**. Klicken Sie auf das Kontrollkästchen und geben Sie die Anzahl der Tage in das Drehfeld ein. Wenn der Server so konfiguriert ist, dass er die Zeitstempel für Dateien konfiguriert, auf die zuletzt zugegriffen wurde, wird dadurch die Dateiverwaltungsaufgabe nur auf Dateien ausgeführt, auf die nicht in der mehr als die angegebene Anzahl von Tagen zugegriffen wurde. Wenn der Server nicht konfiguriert ist, um die Zugriffszeiten zu verfolgen, sind diese Bedingung wirkungslos.

    -   **Tage seit der Dateierstellung**. Klicken Sie auf das Kontrollkästchen und geben Sie die Anzahl der Tage in das Drehfeld ein. Dadurch wird die Aufgabe nur auf Dateien angewendet, die mindestens in der angegebenen Anzahl von Tagen erstellt wurden.  

    -   **Gültig ab**. Legen Sie ein Startdatum für den Beginn der Dateiverwaltungsaufgabe für diese Dateien fest. Diese Option ist nützlich für das Verzögern der Aufgabe, bis Sie die Gelegenheit haben, die Benutzer zu benachrichtigen oder andere Vorkehrungen zu treffen.

8.  Klicken Sie auf der Registerkarte **Zeitplan** auf **Zeitplan erstellen** und dann im Dialogfeld **Zeitplan** auf **Neu**. Die zeigt den Standardzeitplan für 9:00 Uhr täglich an, Sie können allerdings den Standardzeitplan ändern. Wenn Sie die Konfiguration des Zeitplans abgeschlossen haben, klicken Sie auf **OK** und dann erneut auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Klassifizierungsverwaltung](classification-management.md)
-   [Dateiverwaltungsaufgaben](file-management-tasks.md)