---
title: Windows Hypervisor muss ausgeführt werden
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 501a9beb-c464-46c0-88c5-e3e7e3e70101
author: KBDAzure
ms.date: 10/03/2016
ms.openlocfilehash: f34e10918c60fb602c3a88ef3434cda619b11d8d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884141"
---
# <a name="windows-hypervisor-must-be-running"></a>Windows Hypervisor muss ausgeführt werden

>Gilt für: Windows Server 2016
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorraussetzungen|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Windows Hypervisor wird nicht ausgeführt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer kann nicht gestartet werden, bis Windows Hypervisor ausgeführt wird.*  
  
## <a name="resolution"></a>Auflösung  
  
*Überprüfen Sie die Windows Server-Katalog, um festzustellen, ob dieser Server qualifiziert wird, Hyper-V ausführen. Als Nächstes stellen Sie sicher, dass das BIOS für die hardwareunterstützte Virtualisierung und der Hardware erzwungene Datenausführungsverhinderung aktiviert ist. Klicken Sie dann überprüfen Sie die Hyper-V-Hypervisor-Ereignisprotokoll.*  
  
Der Katalog finden Sie unter [Windows Server-Katalog](https://go.microsoft.com/fwlink/?LinkId=111228) (https://go.microsoft.com/fwlink/?LinkId=111228).  
  
> [!CAUTION]  
> Ändern bestimmte Parameter im BIOS Systems von einem Computer kann dazu führen, dass dieser Computer nicht mehr Laden des Betriebssystems oder kann es Hardwaregeräte, wie z. B. Festplatten, nicht verfügbar machen. Immer finden Sie im Benutzerhandbuch für den Computer aus, um die richtige Methode zum Konfigurieren von BIOS des Systems zu ermitteln. Darüber hinaus ist es immer eine gute Idee, zu verfolgen die Parameter, die Sie ändern und die ursprünglichen Wert, sodass Sie sie bei Bedarf später wiederherstellen können. Wenn Sie Probleme auftreten, nach dem Ändern der Parameter im BIOS Systems, die Einstellungen der Standardrichtlinie laden (eine Option ist in der Regel in den BIOS-Serverkonfigurations-Hilfsprogramm verfügbar), oder wenden Sie sich an den Hersteller des Computers, um Unterstützung zu erhalten.  
  
#### <a name="to-verify-virtualization-support-in-the-bios-or-uefi"></a>Um zu überprüfen, ob die Virtualisierungsunterstützung im BIOS oder UEFI  
  
1.  Starten Sie den Computer neu, und greifen Sie auf das BIOS oder UEFI über das Konfigurationstool. Zugang zu diesem Tool ist in der Regel verfügbar, wenn der Computer über einen Startvorgang wechselt. Sofort, nachdem Sie die meisten Computer aktivieren, wird eine Meldung, ein paar Sekunden, die die Schlüssel oder die Tastenkombination drücken, um das Konfigurationstool öffnen auflistet.  
  
2.  Suchen Sie die Einstellungen für die Virtualisierung und der Hardware erzwungene Data Execution Prevention (DEP), und stellen Sie sicher, dass sie sich befinden. Es folgen allgemeine Menü-Standorten für diese Einstellungen in der Configuration-Tool, und klicken Sie auf Beispiele für deren Namen werden möglicherweise:  
  
    -   Virtualisierungsunterstützung:  
  
        -   In der Regel unter den Einstellungen für die main-Prozessor oder Leistung verfügbar. Manchmal ist es unter der Sicherheitseinstellungen.  
  
        -   Suchen Sie nach dem Parameternamen, die "Netzwerkvirtualisierung" oder "Virtualisierungstechnologie" enthalten.  
  
    -   Von der Hardware erzwungene Datenausführungsverhinderung:  
  
        -   In der Regel unter "Einstellungen" die Sicherheits- oder Arbeitsspeicher verfügbar.  
  
        -   Suchen Sie nach dem Parameternamen, die "Ausführung", "execute" oder "Prävention" enthalten.  
  
3.  Bei Bedarf aktivieren Sie die Einstellungen gemäß die Anweisungen im Konfigurationstool. Die Änderungen zu speichern und beenden.  
  
4.  Wenn die vorgenommenen Änderungen schalten, und klicken Sie dann auf wieder beendet werden.  
  
    > [!IMPORTANT]  
    > Es wird empfohlen, dass Sie die Leistungsfähigkeit deaktivieren und wieder einschalten (einem Energiezyklus bezeichnet), da die Änderungen auf einigen Computern zugewiesen sind, bis dies erfolgt.  
  
Als Nächstes überprüfen Sie die Hyper-V-Hypervisor-Ereignisprotokoll. Wenn Probleme vorhanden sind, müssen Sie auch das Systemprotokoll überprüfen.  
  
#### <a name="to-check-the-event-logs"></a>Überprüfen Sie die Ereignisprotokolle  
  
1.  Öffnen Sie die Ereignisanzeige. Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Ereignisanzeige**.  
  
2.  Öffnen Sie das Hyper-V-Hypervisor-Ereignisprotokoll. Erweitern Sie im Navigationsbereich **Anwendungs- und Dienstprotokolle** >> **Microsoft** >> **Windows**  >>   **Hyper-V-Hypervisor**, und klicken Sie dann auf **Operational**.  
  
3.  Wenn Windows-Hypervisor ausgeführt wird, ist keine weitere Aktion erforderlich. Wenn Windows-Hypervisor ausgeführt wird, müssen Sie dies:  
  
4.  Öffnen Sie das Systemprotokoll. (Erweitern Sie im Navigationsbereich **Windows-Protokolle** und wählen Sie dann **System**.)  
  
5.  Verwenden Sie einen Filter, um die Hyper-V-Hypervisor-Ereignissen zu suchen:   
    1. In der **Aktionen** Bereich, klicken Sie auf **Aktuelles Protokoll filtern**. Für **Ereignisquellen**, geben Sie "Hyper-V-Hypervisor".   
    2. Suchen Sie nach Ereignissen, die Probleme zu melden. Ereignis-ID 41 gibt beispielsweise ein Problem mit der BIOS-Konfiguration an: "Fehler beim Starten des Hyper-V; Entweder VMX nicht vorhanden oder nicht im BIOS aktiviert."  
  
### <a name="see-also"></a>Siehe auch  
Ausführliche Informationen zur Verwendung von Hyper-V unter Windows 10, einschließlich Informationen zu überprüfen, ob Hyper-V, von der Computer ausgeführt werden kann finden Sie unter [Systemanforderungen für Windows 10 Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility). 


