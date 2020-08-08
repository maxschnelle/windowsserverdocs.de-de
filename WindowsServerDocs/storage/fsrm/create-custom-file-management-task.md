---
title: Erstellen einer benutzerdefinierten Dateiverwaltungsaufgabe
description: In diesem Artikel wird beschrieben, wie Sie eine benutzerdefinierte Datei Verwaltungsaufgabe und benutzerdefinierte Tasks erstellen.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7fcfd9958787817a6945b220115c507f48924cbf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954677"
---
# <a name="create-a-custom-file-management-task"></a>Erstellen einer benutzerdefinierten Dateiverwaltungsaufgabe

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das Ablaufdatum ist nicht immer eine gewünschte Aktion, die für Dateien ausgeführt werden soll. Mit Datei Verwaltungsaufgaben können Sie auch benutzerdefinierte Befehle ausführen.

> [!Note]
> Bei diesem Verfahren wird davon ausgegangen, dass Sie mit Datei Verwaltungsaufgaben vertraut sind und daher nur die Registerkarte **Aktion** abdecken, auf der benutzerdefinierte Einstellungen konfiguriert sind.

## <a name="to-create-a-custom-task"></a>So erstellen Sie einen benutzerdefinierten Task

1.  Klicken Sie auf den Knoten **Dateiverwaltungsaufgaben**.

2.  Klicken Sie mit der rechten Maustaste auf **Datei Verwaltungsaufgaben**, und klicken Sie dann auf **Datei Verwaltungsaufgabe erstellen** (oder klicken Sie im **Aktions** Bereich auf **Datei Verwaltungsaufgabe erstellen** ). Daraufhin wird das Dialogfeld **Dateiverwaltungsaufgabe erstellen** geöffnet.

3.  Geben Sie auf der Registerkarte **Aktion** folgende Informationen ein:

    -   **Art:** Wählen Sie im Dropdown Menü die Option **Benutzer** definiert aus.
    -   **Ausführbare Datei**. Geben Sie einen Befehl ein, der ausgeführt werden soll, wenn die Datei Verwaltungsaufgabe Dateien verarbeitet. Für diese ausführbare Datei muss festgelegt werden, dass Sie nur von Administratoren und System beschreibbar ist. Wenn andere Benutzer Schreibzugriff auf die ausführbare Datei haben, wird Sie nicht ordnungsgemäß ausgeführt.
    -   **Befehls Einstellungen**. Um die Argumente zu konfigurieren, die an die ausführbare Datei geleitet werden, wenn ein Datei Verwaltungsauftrag Dateien verarbeitet, bearbeiten Sie das Textfeld mit der Bezeichnung **Arguments** Wenn Sie zusätzliche Variablen in den Text einfügen möchten, platzieren Sie den Cursor an der Position im Textfeld, an der Sie die Variable einfügen möchten, wählen Sie die Variable aus, die Sie einfügen möchten, und klicken Sie dann auf **Variable einfügen**. Der Text in Klammern fügt Variablen Informationen ein, die die ausführbare Datei empfangen kann. Die \[ Variable Quelldatei Pfad fügt z \] . b. den Namen der Datei ein, die von der ausführbaren Datei verarbeitet werden soll. Klicken Sie optional auf die Schaltfläche **Arbeitsverzeichnis** , um den Speicherort der benutzerdefinierten ausführbaren Datei anzugeben.
    -   **Befehls Sicherheit**. Konfigurieren Sie die Sicherheitseinstellungen für diese ausführbare Datei. Standardmäßig wird der Befehl als lokaler Dienst ausgeführt. Dies ist das restriktivste Konto, das verfügbar ist.

4.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Klassifizierungsverwaltung](classification-management.md)
-   [Dateiverwaltungsaufgaben](file-management-tasks.md)