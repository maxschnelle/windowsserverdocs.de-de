---
title: Erstellen eines Kontingents
description: In diesem Artikel wird beschrieben, wie ein Kontingent basierend auf einer Vorlage erstellt wird.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b3513510ef00eec7ea78a3193cf44c25ddb17c7e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475217"
---
# <a name="create-a-quota"></a>Erstellen eines Kontingents

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Kontingente können aus einer Vorlage oder mit benutzerdefinierten Eigenschaften erstellt werden. Im folgenden Verfahren wird beschrieben, wie Sie ein Kontingent erstellen, das auf einer Vorlage basiert (empfohlen). Wenn Sie ein Kontingent mit benutzerdefinierten Eigenschaften erstellen müssen, können Sie diese Eigenschaften als Vorlage speichern, um Sie zu einem späteren Zeitpunkt wiederzuverwenden.

Wenn Sie ein Kontingent erstellen, wählen Sie einen Kontingent Pfad aus. Hierbei handelt es sich um ein Volume oder einen Ordner, für das das Speicherlimit gilt. In einem bestimmten Kontingent Pfad können Sie eine Vorlage verwenden, um einen der folgenden Kontingent Typen zu erstellen:

-   Ein einzelnes Kontingent, das den Speicherplatz für ein gesamtes Volume oder einen Ordner einschränkt.
-   Ein automatisches Apply-Kontingent, das die Kontingent Vorlage einem Ordner oder einem Volume zuweist. Kontingente, die auf dieser Vorlage basieren, werden automatisch generiert und auf alle Unterordner angewendet. Weitere Informationen zum Erstellen von automatischen Apply-Kontingenten finden Sie unter [Erstellen eines automatischen Apply-Kontingents](create-auto-apply-quota.md).


> [!Note]
> Indem Sie Kontingente exklusiv aus Vorlagen erstellen, können Sie Ihre Kontingente zentral verwalten, indem Sie die Vorlagen anstelle der individuellen Kontingente aktualisieren. Anschließend können Sie auf der Grundlage der geänderten Vorlage Änderungen auf alle Kontingente anwenden. Diese Funktion vereinfacht die Implementierung von Speicher Richtlinien Änderungen, indem Sie einen zentralen Punkt bereitstellt, an dem alle Updates vorgenommen werden können.

## <a name="to-create-a-quota-that-is-based-on-a-template"></a>So erstellen Sie ein Kontingent, das auf einer Vorlage basiert

1.  Klicken Sie unter **Kontingentverwaltung** auf den Knoten **Kontingentvorlagen**.

2.  Wählen Sie im Ergebnisbereich die Vorlage aus, auf der das neue Kontingent basieren soll.

3.  Klicken Sie mit der rechten Maustaste auf die Vorlage, und klicken Sie auf **Kontingent aus Vorlage erstellen** (oder wählen Sie im **Aktions** Bereich die Option **Kontingent aus Vorlage erstellen** ). Dadurch wird das Dialogfeld **Kontingent erstellen** geöffnet, in dem die Zusammenfassungs Eigenschaften der angezeigten Kontingent Vorlage angezeigt werden.

4.  Geben Sie unter **Kontingent Pfad**den Ordner ein, auf den das Kontingent angewendet werden soll, oder navigieren Sie zu diesem.

5.  Klicken Sie auf die Option **Kontingent für Pfad erstellen** . Beachten Sie, dass die Kontingent Eigenschaften auf den gesamten Ordner angewendet werden.

     > [!Note]
     > Zum Erstellen eines automatischen Apply-Kontingents klicken Sie auf die Option **Vorlage automatisch anwenden und Kontingente für vorhandene und neue Unterordner erstellen** . Weitere Informationen zu automatischen Anwendungs Kontingenten finden Sie unter [Erstellen eines automatischen Apply-Kontingents](create-auto-apply-quota.md) .

6.  Unter **Eigenschaften von dieser Kontingent Vorlage ableiten**ist die Vorlage, die Sie in Schritt 2 zum Erstellen des neuen Kontingents verwendet haben, vorab ausgewählt (oder Sie können eine andere Vorlage aus der Liste auswählen). Beachten Sie, dass die Eigenschaften der Vorlage unter **Zusammenfassung der Kontingent Eigenschaften**angezeigt werden.

7.  Klicken Sie auf **Erstellen**.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen einer Kontingent Vorlage](create-quota-template.md)


