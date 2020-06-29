---
title: Erstellen eines automatisch zugewiesenen Kontingents
description: In diesem Artikel wird beschrieben, wie basierend auf einer Kontingent Vorlage automatisch Apply-Kontingente erstellt werden.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 38354a6c6e39f58574a64c752bb86800f3fc3039
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474067"
---
# <a name="create-an-auto-apply-quota"></a>Erstellen eines automatisch zugewiesenen Kontingents

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Mithilfe von "automatisch anwenden"-Kontingenten können Sie einem übergeordneten Volume oder Ordner eine Kontingent Vorlage zuweisen. Anschließend generiert der Datei Server Ressourcen-Manager automatisch Kontingente, die auf dieser Vorlage basieren. Kontingente werden für jeden der vorhandenen Unterordner und für Unterordner generiert, die Sie zukünftig erstellen.

Beispielsweise können Sie ein automatisches Apply-Kontingent für Unterordner definieren, die bei Bedarf erstellt werden, für roamingprofilbenutzer oder für neue Benutzer. Jedes Mal, wenn ein Unterordner erstellt wird, wird automatisch ein neuer Kontingent Eintrag generiert, indem die Vorlage aus dem übergeordneten Ordner verwendet wird. Diese automatisch generierten Kontingent Einträge können dann unter dem Knoten **Kontingente** als einzelne Kontingente angezeigt werden. Jeder Kontingent Eintrag kann separat verwaltet werden.

## <a name="to-create-an-auto-apply-quota"></a>So erstellen Sie ein automatisches Apply-Kontingent

1.  Klicken Sie in **Kontingent Verwaltung**auf den Knoten **Kontingente** .

2.  Klicken Sie mit der rechten Maustaste auf **Kontingente**, und klicken Sie dann auf **Kontingent erstellen** (oder wählen Sie im Bereich **Aktionen** die Option **Kontingent erstellen** ). Dadurch wird das Dialogfeld **Kontingent erstellen** geöffnet.

3.  Geben Sie unter **Kontingent Pfad**den Namen des übergeordneten Ordners ein, auf den das Kontingent Profil angewendet werden soll, oder navigieren Sie zu diesem. Das automatische Apply-Kontingent wird auf jeden Unterordner (Current und Future) in diesem Ordner angewendet.

4.  Klicken Sie **auf Vorlage automatisch anwenden, und erstellen Sie Kontingente für vorhandene und neue Unterordner**.

5.  Wählen Sie unter **Eigenschaften von dieser Kontingent Vorlage ableiten**die Kontingent Vorlage aus der Dropdown Liste aus, die Sie anwenden möchten. Beachten Sie, dass die Eigenschaften jeder Vorlage unter **Zusammenfassung der Kontingent Eigenschaften**angezeigt werden.

6.  Klicken Sie auf **Erstellen**.

> [!Note]
> Sie können alle automatisch generierten Kontingente überprüfen, indem Sie den Knoten **Kontingente** auswählen und dann **Aktualisieren**auswählen. Ein individuelles Kontingent für jeden Unterordner und das automatisch angewendende Kontingent Profil im übergeordneten Volume oder Ordner werden aufgelistet.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Kontingentverwaltung](quota-management.md)
-   [Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents](edit-auto-apply-quota-properties.md)