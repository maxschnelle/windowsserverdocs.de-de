---
title: Erstellen einer Kontingentvorlage
description: In diesem Artikel wird beschrieben, wie Sie eine Kontingentvorlage zum Definieren einer Speicherplatzbeschränkung erstellen
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 28a64c77d09bffeccbbc94ba7648d1bc0227e945
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394155"
---
# <a name="create-a-quota-template"></a>Erstellen einer Kontingentvorlage

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Kontingentvorlage* dient zum Definieren einer Speicherplatzbeschränkung, des Kontingenttyps (weich oder hart) und einer Gruppe von Benachrichtigungen, die automatisch generiert werden, wenn der Kontingentbedarf die definierten Schwellenwerte erreicht.

Wenn Sie Kontingente ausschließlich auf der Grundlage von Vorlagen erstellen, können Sie die Kontingente zentral verwalten, indem Sie die Vorlagen aktualisieren, anstatt die Änderungen der einzelnen Kontingente zu replizieren. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

## <a name="to-create-a-quota-template"></a>So erstellen Sie eine Kontingentvorlage

1.  Klicken Sie unter **Kontingentverwaltung** auf den Knoten **Kontingentvorlagen**.

2.  Klicken Sie mit der rechten Maustaste auf **Kontingentvorlagen**, und klicken Sie anschließend auf **Kontingentvorlage erstellen** (oder wählen Sie im Aktionsbereich die Option **Kontingentvorlage erstellen** aus). Das Dialogfeld **Kontingentvorlage erstellen** wird geöffnet.

3.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage als Grundlage für eine neue Vorlage kopieren und verwenden möchten, wählen Sie in der Dropdownliste **Eigenschaften aus Kontingentvorlage kopieren** eine Vorlage aus, und klicken Sie anschließend auf Kopieren. Klicken Sie anschließend auf **Kopieren**.

    Wenn Sie die Eigenschaften einer vorhandenen Vorlage verwenden oder eine neue Vorlage erstellen möchten, ändern Sie auf der Registerkarte **Einstellungen** die folgenden Werte, bzw. legen Sie sie fest:

4.  Geben Sie im Textfeld **Vorlagenname** einen Namen für die neue Vorlage ein.

5.  Geben Sie im Textfeld **Bezeichnung** eine optionale aussagekräftige Bezeichnung ein, die neben allen Kontingenten angezeigt wird, die auf der Grundlage dieser Vorlage erstellt werden.

6.  Unter **Speicherplatzbeschränkung**:

    -   Geben Sie im Textfeld **Grenze** eine Zahl ein, und wählen Sie eine Einheit (KB, MB, GB oder TB) aus, um die Speicherplatzbeschränkung für das Kontingent anzugeben.
    -   Wählen Sie die Option **Harte Kontingentgrenze** oder **Weiche Kontingentgrenze** aus. (Bei einer harten Kontingentgrenze wird verhindert, dass Benutzer Dateien speichern können, wenn die Speicherplatzbeschränkung erreicht ist, und es werden Benachrichtigungen generiert, wenn das Datenvolume den jeweils konfigurierten Schwellenwert erreicht. Bei einer weichen Kontingentgrenze wird die Kontingentgrenze nicht erzwungen, aber es werden alle konfigurierten Benachrichtigungen generiert.)

7.  Für die Kontingentgrenze können optionale Schwellenwertbenachrichtigungen konfiguriert werden. . Die Vorgehensweise wird nachfolgend beschrieben. Wählen Sie zunächst alle Kontingentvorlageneigenschaften aus, die verwendet werden sollen, und klicken Sie anschließend zum Speichern der Vorlage auf **OK**.

## <a name="setting-optional-notification-thresholds"></a>Optionale Schwellenwerte für Benachrichtigungen festlegen

Wenn der Speicher in einem Volume oder in einem Ordner einen Schwellenwert erreicht, den Sie definieren, sendet der Ressourcen-Manager für Dateiserver E-Mail-Nachrichten an Administratoren oder bestimmte Benutzern, protokolliert ein Ereignis, führt einen Befehl oder ein Skript aus oder erstellt Berichte. Sie können mehr als eine Art der Benachrichtigung für jeden Schwellenwert konfigurieren, und Sie können mehrere Schwellenwerte für Kontingente (oder Kontingentvorlagen) definieren. Standardmäßig werden keine Benachrichtigungen erstellt.

Beispielsweise können Sie Schwellenwerte konfigurieren, um eine E-Mail-Nachricht an den Administrator und an die Benutzer zu senden, die wissen möchten, wann ein Ordner 85 % der Kontingentgrenze erreicht, und eine weitere Benachrichtigung, wenn die Kontingentgrenze erreicht ist. Darüber hinaus sollten Sie ein Skript ausführen, das den Befehl **dirquota.exe** verwendet, um das Kontingentlimit automatisch auszulösen, wenn ein Schwellenwert erreicht wird.

> [!Important]
> Zum Senden von E-Mail-Benachrichtigungen und um Speicherberichte mit Parametern zu konfigurieren, die für die Serverumgebung geeignet sind, müssen Sie zuerst die allgemeinen Optionen des Ressourcen-Managers für Dateiserver festlegen. Weitere Informationen finden Sie unter [Festlegen der Einstellungen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)

**So konfigurieren Sie Benachrichtigungen, die vom Datei Server Ressourcen-Manager mit einem Kontingent Schwellenwert generiert werden**

1. Klicken Sie im Dialogfeld **Kontingentvorlage erstellen** unter **Benachrichtigungsschwellenwerte** auf **Hinzufügen**. Das Dialogfeld **Schwellenwert hinzufügen** wird geöffnet.

2. So legen Sie eine prozentuale Kontingentgrenze fest, die eine Benachrichtigung generiert:

   Geben Sie in das Textfeld **Benachrichtigungen generieren, wenn die Auslastung den folgenden Prozentwert erreicht: (%)** einen Prozentsatz der Kontingentgrenze für den Benachrichtigungsschwellenwert ein. (Der Standardprozentsatz des ersten Benachrichtigungsschwellenwerts ist 85 %.)

3. So konfigurieren Sie E-Mail-Benachrichtigungen:

   Legen Sie auf der Registerkarte **E-Mail-Nachricht** folgende Optionen fest:

   - Um Administratoren zu benachrichtigen, wenn ein Schwellenwert erreicht wird, aktivieren Sie das Kontrollkästchen **E-Mail an die folgenden Administratoren senden** und geben Sie die Namen der administrativen Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie das Format <em>account@domain</em>, und verwenden Sie Semikolons zum Trennen mehrerer Konten.
   - Aktivieren Sie zum Senden der E-Mail an die Person, deren gespeicherte Datei den Kontingentschwelle erreicht hat, das Kontrollkästchen **E-Mail an den Benutzer senden, der den Schwellenwert überschritten hat**.
   - Um die Nachricht zu konfigurieren, ändern Sie den vorgegebenen standardmäßigen Betreff und Textkörper. Der Text in Klammern fügt die Variableninformationen über das Kontingent-Ereignis ein, das die Benachrichtigung verursacht hat. Beispielsweise fügt die Variable **\[Quelle IO Owner\]** den Namen des Benutzers ein, der die Datei gespeichert hat, die den Kontingent Schwellenwert erreicht hat. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.
   - Wenn Sie weitere Header konfigurieren möchten (einschließlich Von, Cc, Bcc und Antwort an), klicken Sie auf **Weitere E-Mail-Kopfzeilen**.

4. So protokollieren Sie ein Ereignis:

   Klicken Sie auf die Registerkarte **Ereignisprotokoll** und wählen Sie das Kontrollkästchen **Warnung an Ereignisprotokoll senden**. Bearbeiten Sie anschließend den Standard-Protokolleintrag.

5. So führen Sie einen Befehl oder ein Skript aus:

   Aktivieren Sie auf der Registerkarte **Befehl** das Kontrollkästchen **Diesen Befehl oder dieses Skript ausführen** . Geben Sie anschließend den Befehl ein oder klicken Sie auf **Durchsuchen**, um den Speicherort zu suchen, in dem das Skript gespeichert ist. Sie können ebenfalls Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder ein Skript auswählen oder die Sicherheitsstufeneinstellungen für den Befehl ändern.

6. So erstellen Sie einen oder mehrere Speicherberichte:

   Aktivieren Sie auf der Registerkarte **Bericht** das Kontrollkästchen **Berichte** und wählen Sie dann aus, welche Berichte erstellt werden sollen. (Sie können einen oder mehrere Administratoren als E-Mail-Empfänger für den Bericht auswählen oder den Bericht per E-Mail an den Benutzer senden, dessen Datei den Schwellenwert erreicht hat.)

   Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.

7. Klicken Sie auf **OK**, um den Benachrichtigungsschwellenwert zu speichern.

8. Wiederholen Sie diese Schritte aus, wenn Sie zusätzliche Benachrichtigungsschwellenwerte für die Kontingentvorlage konfigurieren möchten.

## <a name="see-also"></a>Weitere Informationen

-   [Kontingentverwaltung](quota-management.md)
-    [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Bearbeiten von Kontingentvorlageneigenschaften](edit-quota-template-properties.md)
-   [Befehlszeilentools](command-line-tools.md)


