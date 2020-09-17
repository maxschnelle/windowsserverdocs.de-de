---
title: Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss für den automatischen Start konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 222bbe76-c514-4a3f-b61b-860a4dc2826a
ms.date: 8/16/2016
ms.openlocfilehash: 8245e425adb1b1187918e9ee213135c16a190cde
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746495"
---
# <a name="the-hyper-v-virtual-machine-management-service-should-be-configured-to-start-automatically"></a>Der Hyper-V-Verwaltungsdienst für virtuelle Computer muss für den automatischen Start konfiguriert werden.

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

*Der Hyper-V-Verwaltungsdienst für virtuelle Computer ist nicht für den automatischen Start konfiguriert.*

## <a name="impact"></a>Auswirkung

*Virtuelle Computer können erst verwaltet werden, nachdem der Dienst gestartet wurde.*

Virtuelle Computer, auf denen ausgeführt wird, werden weiterhin ausgeführt. Es ist jedoch nicht möglich, virtuelle Computer zu verwalten oder zu erstellen oder zu löschen, bis der Dienst ausgeführt wird.

## <a name="resolution"></a>Lösung

*Verwenden Sie das Snap-in "Dienste" oder das Befehlszeilen Tool "SC config", um den Dienst für den automatischen Start neu zu konfigurieren.*

> [!TIP]
> Wenn Sie den Dienst nicht in der Desktop-App finden oder das Befehlszeilen Tool meldet, dass der Dienst nicht vorhanden ist, sind die Hyper-V-Verwaltungs Tools wahrscheinlich nicht installiert. Gehen Sie bei der Installation wie folgt vor:
>
> - Öffnen Sie unter Windows Server Server-Manager, und verwenden Sie den Assistenten zum Hinzufügen von Rollen und Features. Weitere Informationen finden Sie unter [Installieren der Hyper-V-Rolle auf Windows Server 2016](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).
> - Starten Sie unter Windows auf dem Desktop die Eingabe **Programme**, klicken Sie auf **Programme und Funktionen** (Systemsteuerung), > Windows-Features ein- **oder ausschalten**Hyper-v-  >  **Hyper-V**  >  **Verwaltungs Tools**für Hyper-v. Klicken Sie dann auf **OK**.

#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>So konfigurieren Sie den Dienst für den automatischen Start mithilfe der Desktop-App für Dienste neu

1.  Öffnen Sie die Desktop-App für Dienste. (Klicken Sie auf **Start**, klicken Sie in das Suchfeld, geben Sie **Dienste**ein, und klicken Sie dann auf Dienste in der Ergebnisliste.

2.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **Hyper-V-Verwaltung virtueller Computer**, und klicken Sie dann auf **Eigenschaften**.

3.  Klicken Sie auf der Registerkarte **Allgemein** unter **Starttyp** auf **automatisch**.

#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-sc-config-command"></a>So konfigurieren Sie den Dienst so neu, dass er automatisch mit dem Befehl sc config gestartet wird

1.  Öffnen Sie Windows PowerShell.

2.  Typ:

    ```
    set-service  vmms -startuptype automatic
    ```

3.  Wenn der Dienst nicht bereits ausgeführt wird, geben Sie Folgendes ein:

    ```
    start-service -name vmms
    ```



