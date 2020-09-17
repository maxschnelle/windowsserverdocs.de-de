---
title: Alle Integration Services auf virtuellen Computern aktivieren
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 16e202ad-3795-40c9-8176-7ca319e56d26
ms.date: 8/16/2016
ms.openlocfilehash: ca614074035678f50dd55b82864d989b789e61fb
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746875"
---
# <a name="enable-all-integration-services-in-virtual-machines"></a>Alle Integration Services auf virtuellen Computern aktivieren

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Mindestens ein Integrations Dienst ist deaktiviert oder funktioniert nicht auf einem virtuellen Computer.*

## <a name="impact"></a>Auswirkung

*Die Dienst-oder Integrationsfunktion funktioniert möglicherweise nicht ordnungsgemäß für die folgenden virtuellen Computer:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie das Snap-in "Dienste" oder das Befehlszeilen Tool SC config, um zu überprüfen, ob der Dienst für den automatischen Start konfiguriert ist und nicht beendet wurde.*

#### <a name="to-configure-how-a-service-is-started-using-the-services-snap-in"></a>So konfigurieren Sie, wie ein Dienst mit dem Dienste-Snap-in gestartet wird

1.  Verwenden Sie Remotedesktopdienste-oder virtuelle Computerverbindung, um eine Verbindung mit dem virtuellen Computer herzustellen und sich beim Gast Betriebssystem anzumelden.

2.  Öffnen Sie Dienste. (Klicken Sie auf **Start**, klicken Sie in das Feld **Suche starten** , geben Sie **Services. msc**ein, und drücken Sie dann die EINGABETASTE.)

3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Dienst, den Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **Allgemein** unter **Starttyp** auf **automatisch**.

#### <a name="to-configure-how-a-service-is-started-using-sc-config"></a>So konfigurieren Sie, wie ein Dienst mit SC config gestartet wird

1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)

2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.

3.  Ersetzen Sie <Service-Name> durch den Namen des Dienstanbieter, und geben Sie dann Folgendes ein:

    ```
    sc config <service-name> start=auto
    ```



