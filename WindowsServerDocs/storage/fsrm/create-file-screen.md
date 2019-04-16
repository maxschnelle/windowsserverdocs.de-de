---
title: "Erstellen einer Dateiprüfung"
description: "In diesem Artikel wird beschrieben, wie Sie eine Dateiprüfung erstellen"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c1f261eb926eca3ead58b87aeb00a5060b9d957c
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="create-a-file-screen"></a>Erstellen einer Dateiprüfung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Beim Erstellen einer neuen Dateiprüfung können Sie eine Dateiprüfungsvorlage speichern, die auf den benutzerdefinierten Dateiprüfungseigenschaften basiert, die Sie definieren. Der Vorteil besteht darin, dass eine Verknüpfung zwischen den Dateiprüfungen und der verwendeten Vorlage bestehen bleibt, sodass in Zukunft durch ein Ändern der Vorlage diese Änderung auf alle Dateiprüfungen angewendet werden kann, die davon abgeleitet sind. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

## <a name="to-create-a-file-screen-with-custom-properties"></a>So erstellen Sie eine Dateiprüfung mit benutzerdefinierten Eigenschaften

1.  Klicken Sie unter **Dateiprüfungsverwaltung** auf den Knoten **Dateiprüfungen**.

2.  Klicken Sie mit der rechten Maustaste auf **Dateiprüfungen,** und dann auf **Dateiprüfung erstellen** (oder wählen Sie **Dateiprüfung erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Dateiprüfung erstellen** geöffnet.

3.  Geben Sie unter **Dateiprüfungspfad** den Namen des übergeordneten Ordner ein (oder navigieren Sie dahin), auf den die Dateiprüfung angewendet wird. Die Dateiprüfung gilt für den ausgewählten Ordner und alle Unterordner.

4.  Klicken Sie unter **Wie möchten Sie die Dateiprüfungseigenschaften konfigurieren?** auf **Definieren von benutzerdefinierten Dateiprüfungseigenschaften**, und klicken Sie dann auf **Benutzerdefinierte Eigenschaften**. Daraufhin wird das Dialogfeld **Dateiprüfungseigenschaften** geöffnet.

5.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage als Grundlage für eine Datenprüfung kopieren und verwenden möchten, wählen Sie in der Dropdownliste **Eigenschaften aus Vorlage kopieren** aus. Klicken Sie anschließend auf **Kopieren**.

    Ändern oder legen Sie im Dialogfeld **Dateiprüfungseigenschaften** die Werte der Registerkarte **Einstellungen** fest:

6.  Klicken Sie unter **Prüfungstyp** auf die Option **Aktives prüfen** oder **Passives prüfen**. (Aktives Prüfen verhindert, dass Benutzer Dateien speichern, die blockierten Dateigruppen angehören und Benachrichtigungen generieren, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern. Passives Prüfen sendet Konfigurationsbenachrichtigungen, aber es verhindert nicht, dass Benutzer Dateien speichern können.)

7.  Wählen Sie unter **Dateigruppen** jede Dateigruppe aus, die in Ihrer Dateiprüfung enthalten sein sollen. (Um das Kontrollkästchen für die Dateigruppe zu aktivieren, doppelklicken Sie auf die Bezeichnung der Dateigruppe.)

    Wenn Sie die Dateitypen ansehen möchten, die in der Dateigruppe enthalten und ausgeschlossen sind, klicken Sie auf die Bezeichnung für die Dateigruppe und dann auf **Bearbeiten**. Klicken Sie zum Erstellen einer neuen Dateigruppe auf **Erstellen**.

8.  Darüber hinaus können Sie den **Ressourcen-Manager für Dateiserver** so konfigurieren, dass eine oder mehrere Benachrichtigungen erstellt werden. Dies geschieht durch das Festlegen der Optionen in den Registerkarten **E-Mail-Nachricht**, **Ereignisprotokoll**, **Befehl**, und **Bericht**. Weitere Informationen zu den Benachrichtigungsoptionen der Dateiprüfung finden Sie unter [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md).

9.  Wählen Sie zunächst alle Dateiprüfungseigenschaften aus, die verwendet werden sollen, und klicken Sie anschließend auf **OK**, um das Dialogfeld **Dateiprüfungseigenschaften** zu schließen.

10. Klicken Sie im Dialogfeld **Dateiprüfung erstellen** auf **Erstellen**, um die Dateiprüfung zu speichern. Daraufhin wird das Dialogfeld **Benutzerdefinierte Eigenschaften als Vorlage speichern** geöffnet.

11. Wählen Sie den Typ der benutzerdefinierten Dateiprüfung aus, den Sie erstellen möchten:

    -   Wenn Sie eine Vorlage speichern möchten, die auf diesen benutzerdefinierten Eigenschaften (empfohlen) basiert, klicken Sie auf **Benutzerdefinierte Eigenschaften als Vorlage speichern** und geben Sie einen Namen für die Vorlage ein. Diese Option wendet die Vorlage auf die neue Datei an, und Sie können die Vorlage verwenden, um in Zukunft zusätzliche Dateiprüfungen zu erstellen. Dadurch können Sie später die Dateiprüfungen automatisch aktualisieren, indem Sie die Vorlage aktualisieren.
    -   Wenn Sie die Vorlage nicht mit der Datei speichern möchten, klicken Sie auf **Benutzerdefinierte Dateiprüfung ohne Erstellen einer Vorlage speichern**.

12. Klicken Sie auf **OK**.

## <a name="see-also"></a>Weitere Informationen:

-   [Dateiprüfungsverwaltung](file-screening-management.md)
-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlagen](edit-file-screen-template-properties.md)


