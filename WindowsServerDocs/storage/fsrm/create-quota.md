---
title: Erstellen eines Kontingents
description: "Dieser Artikel enthält Informationen zum Erstellen von Kontingenten basierend auf einer Vorlage"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f3c677f5ebf7dda44f4b99a64d0fbf8d2c72b92e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="create-a-quota"></a>Erstellen eines Kontingents

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Kontingente können aus einer Vorlage oder mit benutzerdefinierten Eigenschaften erstellt werden. Die folgenden Anweisungen beschreiben, wie ein Kontingent basierend auf einer Vorlage (empfohlen) erstellt wird. Wenn Sie ein Kontingent mit benutzerdefinierten Eigenschaften erstellen müssen, können Sie diese Eigenschaften als Vorlage zur Wiederverwendung zu einem späteren Zeitpunkt speichern.

Wenn Sie ein Kontingent erstellen, wählen Sie einen Kontingentpfad aus, der ein Volume oder ein Ordner ist, auf den die Speicherbeschränkungen zutreffen. Sie können für jeden angegebenen Pfad eine Vorlage verwenden, um einen der folgenden Typen von Kontingent zu erstellen:

-   Ein einzelnes Kontingent, das den Platz für ein gesamtes Volume oder einen Ordner beschränkt.
-   Ein automatisch zugewiesenes Kontingent, das die Kontingentvorlage einem Volume oder Ordner zuweist. Kontingente, die auf dieser Vorlage basieren, werden automatisch generiert und auf alle Unterordner angewendet. Weitere Informationen zum Erstellen von automatisch zugewiesene Kontingenten finden Sie unter [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md).


> [!Note]
> Wenn Sie Kontingente ausschließlich auf der Grundlage von Vorlagen erstellen, können Sie die Kontingente zentral verwalten, indem Sie die Vorlagen anstatt die verschiedenen Kontingente aktualisieren. Anschließend können Sie die Änderungen auf alle Kontingente basierend auf der geänderten Vorlage anwenden. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

## <a name="to-create-a-quota-that-is-based-on-a-template"></a>So erstellen Sie ein Kontingent, das auf der Vorlage basiert.

1.  Klicken Sie unter **Kontingentverwaltung** auf den Knoten **Kontingentvorlagen**.

2.  Wählen Sie im Ergebnisbereich die Vorlage, auf der Ihr neues Kontingent basieren soll.

3.  Klicken Sie mit der rechten Maustaste auf die Vorlage, und klicken Sie anschließend auf **Kontingent mithilfe einer Vorlage erstellen** (oder wählen Sie im **Aktionsbereich** die Option **Kontingentvorlage erstellen** aus). Daraufhin wird das Dialogfeld **Kontingent erstellen** mit der Zusammenfassung der Eigenschaften der Kontingentvorlage angezeigt.

4.  Geben Sie unter **Kontingentpfad** den Ordner ein (oder navigieren Sie dahin), auf den das Kontingent angewendet wird.

5.  Klicken Sie auf die Option **Kontingent im Pfad erstellen**. Beachten Sie, dass die Kontingenteigenschaften auf den gesamten Ordner angewendet werden.

     > [!Note]
     > Um ein automatisch zugewiesenes Kontingent zu erstellen, klicken Sie auf die Option **Vorlage automatisch anwenden und Kontingente für vorhandene und neue Unterordner erstellen**. Weitere Informationen über automatisch zugewiesene Kontingente finden Sie unter [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md).

6.  Unter **Eigenschaften aus dieser Kontingentvorlage ableiten** ist die zum Erstellen des neuen Kontingents in Schritt2 verwendete Vorlage aktiviert (oder Sie können eine andere Vorlage aus der Liste auswählen). Beachten Sie, das die Eigenschaften der Vorlage unter **Zusammenfassung der Eigenschaften von Kontingenten** angezeigt werden.

7.  Klicken Sie auf **Erstellen**.

## <a name="see-also"></a>Weitere Informationen:

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen einer Kontingentvorlage](create-quota-template.md)


