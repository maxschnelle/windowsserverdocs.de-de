---
title: Erstellen eines automatisch zugewiesenen Kontingents
description: Dieser Artikel enthält Informationen zum Erstellen von automatisch zugewiesenen Kontingenten basierend auf einer Kontingentvorlage
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 68967ff920f25c05affc206ed45bad9275e781b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394235"
---
# <a name="create-an-auto-apply-quota"></a>Erstellen eines automatisch zugewiesenen Kontingents

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Mit automatisch zugewiesenen Kontingenten können Sie einem übergeordneten Volume oder Ordner eine Kontingentvorlage zuweisen. Der Ressourcen-Manager für Dateiserver generiert automatisch Kontingente, die auf dieser Vorlage basieren. Kontingente werden für jede der vorhandenen Unterordner und alle Unterordner erstellt, die Sie in der Zukunft zu erstellen.

Sie können z. B. ein automatisch zugewiesenes Kontingent für Unterordner erstellen, die bei Bedarf erstellt werden, für das Roamingbenutzer oder für neue Benutzer gelten. Jedes Mal, wenn ein Unterordner erstellt wird, wird mithilfe der Vorlage des übergeordneten Ordners automatisch ein neuer Kontingenteintrag generiert. Diese automatisch generierten Kontingenteinträge können dann als einzelne Kontingente unter dem **Kontingente**-Knoten angezeigt werden. Jeder Kontingenteintrag kann separat verwaltet werden.

## <a name="to-create-an-auto-apply-quota"></a>So erstellen Sie ein automatisch zugewiesenes Kontingent

1.  Klicken Sie unter **Kontingentverwaltung** auf den Knoten **Kontingent**.

2.  Klicken Sie mit der rechten Maustaste auf **Kontingent**, und klicken Sie anschließend auf **Kontingent erstellen** (oder wählen Sie im **Aktionsbereich** die Option **Kontingent erstellen** aus). Das Dialogfeld **Kontingent erstellen** wird geöffnet.

3.  Geben Sie unter **Kontingentpfad** den Namen des übergeordneten Ordner ein (oder navigieren Sie dahin), auf den das Kontingentprofil angewendet wird. Das automatisch zugewiesene Kontingent wird auf jeden Unterordner (aktuell und zukünftig) in diesem Ordner angewendet.

4.  Klicken Sie auf **Vorlage automatisch anwenden und Kontingente für vorhandene und neue Unterordner erstellen**.

5.  Wählen Sie unter **Eigenschaften aus dieser Kontingentvorlage ableiten**die Kontingentvorlage aus der Dropdownliste aus, die Sie anwenden möchten. Beachten Sie, das die Eigenschaften jeder Vorlage unter **Zusammenfassung der Eigenschaften von Kontingenten** angezeigt werden.

6.  Klicken Sie auf **Erstellen**.

> [!Note]
> Sie können alle automatisch generierten Kontingente überprüfen, indem Sie den Knoten **Kontingente** auswählen und dann auf **Aktualisieren** klicken. Sie sehen eine Liste der individuellen Kontingente für jeden Unterordner und das automatisch zugewiesene Kontingentenprofil des übergeordneten Volumes oder Ordners.

## <a name="see-also"></a>Siehe auch

-   [Kontingentverwaltung](quota-management.md)
-   [Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents](edit-auto-apply-quota-properties.md)