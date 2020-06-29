---
title: Auswählen zwischen Standard-oder Produktions Prüfpunkten in Hyper-V
description: Enthält Anweisungen zum Konfigurieren einer virtuellen Maschine für die Verwendung von Standard-oder Produktions Prüfpunkten.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 92bb573b-03b7-470e-b72e-e35edf52b349
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 4e5e3d2d81f9ee1b7cbb4a60a1ade2c218d1e769
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474287"
---
# <a name="choose-between-standard-or-production-checkpoints-in-hyper-v"></a>Auswählen zwischen Standard-oder Produktions Prüfpunkten in Hyper-V

>Gilt für: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019


Ab Windows Server 2016 und Windows 10 können Sie zwischen Standard-und Produktions Prüfpunkten für jeden virtuellen Computer wählen. Produktions Prüfpunkte sind die Standardeinstellungen für neue virtuelle Computer.

- Produktions Prüfpunkte sind "Zeitpunkt"-Images einer virtuellen Maschine, die später auf eine Weise wieder hergestellt werden können, die für alle produktionsworkloads vollständig unterstützt wird. Dies erfolgt mithilfe von Sicherungstechnologie innerhalb des Gastbetriebssystems zum Erstellen des Prüfpunkts anstatt mit Technologie zum Speichern des Zustands.

- Standard Prüfpunkte erfassen den Zustand, die Daten und die Hardwarekonfiguration eines ausgelaufenden virtuellen Computers und sind für die Verwendung in Entwicklungs-und Testszenarien vorgesehen. Standard Prüfpunkte können nützlich sein, wenn Sie einen bestimmten Zustand oder eine bestimmte Bedingung eines ausgelaufenden virtuellen Computers neu erstellen müssen, damit Sie ein Problem beheben können.

  ## <a name="change-checkpoints-to-production-or-standard-checkpoints"></a>Ändern von Prüfpunkten in Produktions-oder Standard Prüfpunkte

1.  Klicken Sie im **Hyper-V-Manager**mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Einstellungen**.

2.  Wählen Sie im Abschnitt **Verwaltung** die Option **Prüfpunkte**aus.

3.  Wählen Sie entweder „Produktionsprüfpunkte“ oder „Standardprüfpunkte“ aus.

    Wenn Sie Produktions Prüfpunkte auswählen, können Sie auch angeben, ob der Host einen Standard Prüf Punkt akzeptieren soll, wenn ein Produktions Prüf Punkt nicht verwendet werden kann. Wenn Sie dieses Kontrollkästchen deaktivieren und kein Produktions Prüf Punkt erstellt werden kann, wird kein Prüfpunkt erstellt.

4.  Wenn Sie die Prüf Punkt Konfigurationsdateien an einem anderen Ort speichern möchten, ändern Sie Sie im Abschnitt **Speicherort** der Prüf Punkt Datei.

5.  Klicken **Sie auf über** nehmen, um die Änderungen zu speichern. Wenn Sie fertig sind, klicken Sie auf **OK** , um das Dialogfeld zu schließen.

> [!NOTE]
> Nur **Produktions Prüfpunkte** werden auf Gast Computern unterstützt, auf denen Active Directory Domain Services Rolle (Domänen Controller) oder Active Directory Lightweight Directory Services Rolle ausgeführt wird.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Produktionsprüfpunkte](../What-s-new-in-Hyper-V-on-Windows.md#production-checkpoints-new)

-   [Aktivieren oder Deaktivieren von Prüfpunkten](Enable-or-disable-checkpoints-in-Hyper-V.md)



