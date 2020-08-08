---
title: Erstellen einer Kontingent Vorlage
description: In diesem Artikel wird beschrieben, wie Sie eine Kontingent Vorlage erstellen, um eine Speicherplatz Beschränkung zu definieren.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 785540c9b8e436ba994af5408b769ea37528c8ba
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954637"
---
# <a name="create-a-quota-template"></a>Erstellen einer Kontingent Vorlage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Kontingent Vorlage* definiert eine Speicherplatz Beschränkung, den Typ des Kontingents (Hard oder Soft) und optional einen Satz von Benachrichtigungen, die automatisch generiert werden, wenn die Kontingent Auslastung definierte Schwellenwerte erreicht.

Wenn Sie Kontingente ausschließlich auf der Grundlage von Vorlagen erstellen, können Sie die Kontingente zentral verwalten, indem Sie die Vorlagen aktualisieren, anstatt die Änderungen der einzelnen Kontingente zu replizieren. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

## <a name="to-create-a-quota-template"></a>So erstellen Sie eine Kontingent Vorlage

1.  Klicken Sie unter **Kontingentverwaltung** auf den Knoten **Kontingentvorlagen**.

2.  Klicken Sie mit der rechten Maustaste auf **Kontingentvorlagen**, und klicken Sie anschließend auf **Kontingentvorlage erstellen** (oder wählen Sie im Aktionsbereich**** die Option **Kontingentvorlage erstellen** aus). Das Dialogfeld **Kontingentvorlage erstellen** wird geöffnet.

3.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage kopieren möchten, die als Basis für die neue Vorlage verwendet werden soll, wählen Sie eine Vorlage aus der Dropdown Liste **Eigenschaften aus Kontingent Vorlage kopieren** aus. Klicken Sie dann auf **Kopieren**.

    Wenn Sie die Eigenschaften einer vorhandenen Vorlage verwenden oder eine neue Vorlage erstellen möchten, ändern Sie auf der Registerkarte **Einstellungen** die folgenden Werte, bzw. legen Sie sie fest:

4.  Geben Sie im Textfeld **Vorlagen Name** einen Namen für die neue Vorlage ein.

5.  Geben Sie im Textfeld **Bezeichnung** eine optionale beschreibende Bezeichnung ein, die neben den von der Vorlage abgeleiteten kontingenten angezeigt wird.

6.  Unter **Speicherplatzbeschränkung**:

    -   Geben Sie im Textfeld **Limit** eine Zahl ein, und wählen Sie eine Einheit (KB, MB, GB oder TB) aus, um die Speicherplatz Beschränkung für das Kontingent anzugeben.
    -   Klicken Sie auf die Option **Hard Quota** oder **Soft Quota** . (Bei einer harten Kontingentgrenze wird verhindert, dass Benutzer Dateien speichern können, wenn die Speicherplatzbeschränkung erreicht ist, und es werden Benachrichtigungen generiert, wenn das Datenvolume den jeweils konfigurierten Schwellenwert erreicht. Bei einer weichen Kontingentgrenze wird die Kontingentgrenze nicht erzwungen, aber es werden alle konfigurierten Benachrichtigungen generiert.)

7.  Sie können eine oder mehrere optionale Schwellenwert Benachrichtigungen für Ihre Kontingent Vorlage konfigurieren, wie im folgenden Verfahren beschrieben. Wählen Sie zunächst alle Kontingentvorlageneigenschaften aus, die verwendet werden sollen, und klicken Sie anschließend zum Speichern der Vorlage auf **OK**.

## <a name="setting-optional-notification-thresholds"></a>Festlegen optionaler Benachrichtigungs Schwellenwerte

Wenn der Speicher in einem Volume oder Ordner einen von Ihnen definierten Schwellenwert erreicht, kann der Datei Server Ressourcen-Manager e-Mail-Nachrichten an Administratoren oder bestimmte Benutzer senden, ein Ereignis protokollieren, einen Befehl oder ein Skript ausführen oder Berichte generieren. Sie können für jeden Schwellenwert mehr als einen Benachrichtigungstyp konfigurieren, und Sie können mehrere Schwellenwerte für ein beliebiges Kontingent (oder eine Kontingent Vorlage) definieren. Standardmäßig werden keine Benachrichtigungen generiert.

Beispielsweise können Sie Schwellenwerte konfigurieren, um eine e-Mail-Nachricht an den Administrator und die Benutzer zu senden, die wissen möchten, wenn ein Ordner 85 Prozent seiner Kontingent Grenze erreicht, und dann eine weitere Benachrichtigung senden, wenn das Kontingent Limit erreicht wird. Darüber hinaus können Sie ein Skript ausführen, das den **dirquota.exe** Befehl verwendet, um die Kontingent Grenze automatisch zu erhöhen, wenn ein Schwellenwert erreicht wird.

> [!Important]
> Um e-Mail-Benachrichtigungen zu senden und die Speicher Berichte mit Parametern zu konfigurieren, die für Ihre Serverumgebung geeignet sind, müssen Sie zuerst die Optionen für allgemeine Dateiserver Ressourcen-Manager festlegen. Weitere Informationen finden Sie unter [Festlegen von Datei Server-Ressourcen-Manager Optionen](setting-file-server-resource-manager-options.md) .

**So konfigurieren Sie Benachrichtigungen, die vom Datei Server Ressourcen-Manager mit einem Kontingent Schwellenwert generiert werden**

1. Klicken Sie im Dialogfeld **Kontingent Vorlage erstellen** unter **Benachrichtigungs Schwellenwerte**auf **Hinzufügen**. Das Dialogfeld **Schwellenwert hinzufügen** wird angezeigt.

2. So legen Sie ein Kontingent Limit in Prozent fest, das eine Benachrichtigung generiert:

   Geben Sie im Textfeld " **Benachrichtigungen generieren, wenn die Verwendung erreicht (%)** " einen Prozentsatz der Kontingent Grenze für den Benachrichtigungs Schwellenwert ein. (Der Standard Prozentsatz für den ersten Benachrichtigungs Schwellenwert ist 85 Prozent.)

3. So konfigurieren Sie e-Mail-Benachrichtigungen

   Legen Sie auf der Registerkarte **e-Mail-Nachricht** die folgenden Optionen fest:

   - Wenn Sie Administratoren benachrichtigen möchten, wenn ein Schwellenwert erreicht wird, aktivieren Sie das Kontrollkästchen **e-Mail an folgende Administratoren senden** , und geben Sie dann die Namen der Administrator Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie das Format <em>account@domain</em> , und verwenden Sie Semikolons zum Trennen mehrerer Konten.
   - Wenn Sie eine e-Mail an die Person senden möchten, die den Kontingent Schwellenwert erreicht hat, aktivieren Sie das Kontrollkästchen **e-Mail an den Benutzer senden, der den Schwellenwert überschritten** hat.
   - Um die Meldung zu konfigurieren, bearbeiten Sie die Standard Betreffzeile und den Nachrichtentext, die bereitgestellt werden. Der Text in Klammern fügt Variablen Informationen über das Kontingent Ereignis ein, das die Benachrichtigung verursacht hat. Beispielsweise fügt die ** \[ Quell-IO \] -Besitzer** Variable den Namen des Benutzers ein, der die Datei gespeichert hat, die den Kontingent Schwellenwert erreicht hat. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.
   - Um zusätzliche Header (einschließlich from, CC, BCC und Reply-to) zu konfigurieren, klicken Sie auf **zusätzliche e-Mail-Header**.

4. So protokollieren Sie ein Ereignis:

   Aktivieren Sie auf der Registerkarte **Ereignisprotokoll** das Kontrollkästchen **Warnung an Ereignisprotokoll senden** , und bearbeiten Sie den Standardprotokoll Eintrag.

5. So führen Sie einen Befehl oder ein Skript aus:

   Aktivieren Sie auf der Registerkarte **Befehl** das Kontrollkästchen **diesen Befehl oder Skript ausführen** . Geben Sie dann den Befehl ein, oder klicken Sie auf **Durchsuchen** , um den Speicherort des Skripts zu suchen. Sie können auch Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder das Skript auswählen oder die Einstellung für die Befehls Sicherheit ändern.

6. So generieren Sie einen oder mehrere Speicher Berichte:

   Aktivieren Sie auf der Registerkarte **Bericht** das Kontrollkästchen **Berichte generieren** , und wählen Sie dann aus, welche Berichte generiert werden sollen. (Sie können einen oder mehrere e-Mail-Empfänger für den Bericht auswählen oder den Bericht an den Benutzer senden, der den Schwellenwert erreicht hat.)

   Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.

7. Klicken Sie zum Speichern des Benachrichtigungs Schwellenwerts auf **OK** .

8. Wiederholen Sie diese Schritte, wenn Sie zusätzliche Benachrichtigungs Schwellenwerte für die Kontingent Vorlage konfigurieren möchten.

## <a name="additional-references"></a>Weitere Verweise

-   [Kontingentverwaltung](quota-management.md)
-    [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Bearbeiten von Kontingentvorlageneigenschaften](edit-quota-template-properties.md)
-   [Befehlszeilentools](command-line-tools.md)


