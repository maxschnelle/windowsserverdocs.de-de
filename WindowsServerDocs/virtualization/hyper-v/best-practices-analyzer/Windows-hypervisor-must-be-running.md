---
title: Der Windows-Hypervisor muss ausgeführt werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 501a9beb-c464-46c0-88c5-e3e7e3e70101
author: KBDAzure
ms.date: 10/03/2016
ms.openlocfilehash: 51f863425bd1107894fb5e4d44ed7c742a806394
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393046"
---
# <a name="windows-hypervisor-must-be-running"></a>Der Windows-Hypervisor muss ausgeführt werden.

>Gilt für: Windows Server 2016
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Erforderliche Komponenten|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Der Windows-Hypervisor wird nicht ausgeführt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer können erst gestartet werden, wenn der Windows-Hypervisor ausgeführt wird.*  
  
## <a name="resolution"></a>Auflösung  
  
*über prüfen Sie den Windows Server-Katalog, um festzustellen, ob dieser Server zum Ausführen von Hyper-V qualifiziert ist. Stellen Sie als nächstes sicher, dass das BIOS für die Hardware gestützte Virtualisierung und die durch die Hardware erzwungene Daten Ausführungs Verhinderung aktiviert ist. Überprüfen Sie dann das Hyper-V-Hypervisor-Ereignisprotokoll.*  
  
Informationen zum Überprüfen des Katalogs finden Sie unter [Windows Server-Katalog](https://go.microsoft.com/fwlink/?LinkId=111228) (https://go.microsoft.com/fwlink/?LinkId=111228).  
  
> [!CAUTION]  
> Wenn bestimmte Parameter im System-BIOS eines Computers geändert werden, kann dies dazu führen, dass der Computer das Betriebssystem nicht mehr lädt oder Hardware Geräte, z. b. Festplattenlaufwerke, nicht mehr verfügbar machen. Wenden Sie sich stets an das Benutzerhandbuch für den Computer, um zu bestimmen, wie das System-BIOS ordnungsgemäß konfiguriert werden kann. Außerdem ist es immer ratsam, die von Ihnen ändernden Parameter und deren ursprünglichen Wert nachzuverfolgen, damit Sie Sie später bei Bedarf wiederherstellen können. Wenn nach dem Ändern der Parameter im System-BIOS Probleme auftreten, versuchen Sie, die Standardeinstellungen zu laden (eine Option ist normalerweise im BIOS-Konfigurations Hilfsprogramm verfügbar), oder wenden Sie sich an den Computerhersteller, um Unterstützung zu erhalten.  
  
#### <a name="to-verify-virtualization-support-in-the-bios-or-uefi"></a>So überprüfen Sie die Virtualisierungsunterstützung im BIOS oder UEFI  
  
1.  Starten Sie den Computer neu, und greifen Sie über das-Konfigurationstool auf das BIOS oder UEFI zu. Der Zugriff auf dieses Tool ist in der Regel verfügbar, wenn der Computer einen Startvorgang durchläuft. Unmittelbar nachdem Sie die meisten Computer eingeschaltet haben, wird eine Meldung für einige Sekunden angezeigt, in der der Schlüssel oder die Kombination von Schlüsseln aufgelistet ist, um das Konfigurationstool zu öffnen.  
  
2.  Suchen Sie die Einstellungen für die Virtualisierung und die von der Hardware erzwungene Daten Ausführungs Verhinderung (Data Execution Prevention, DEP), und überprüfen Sie, ob Sie Im folgenden finden Sie allgemeine Menü Speicherorte für diese Einstellungen im-Konfigurationstool sowie Beispiele dafür, wie Sie benannt werden können:  
  
    -   Virtualisierungsunterstützung:  
  
        -   Normalerweise unter den Einstellungen für den Hauptprozessor oder die Leistung verfügbar. Manchmal befindet er sich unter den Sicherheitseinstellungen.  
  
        -   Suchen Sie nach Parameternamen, die "Virtualisierung" oder "Virtualisierungstechnologie" enthalten.  
  
    -   Von der Hardware erzwungene Dep:  
  
        -   Normalerweise unter den Sicherheits-oder Arbeitsspeicher Einstellungen verfügbar.  
  
        -   Suchen Sie nach Parameternamen, die ' Execution ', ' Execute ' oder ' Prevention ' einschließen.  
  
3.  Aktivieren Sie bei Bedarf die Einstellungen, indem Sie die Anweisungen im-Konfigurationstool befolgen. Speichern Sie die Änderungen, und beenden Sie.  
  
4.  Wenn Sie Änderungen vorgenommen haben, schalten Sie das Ausschalten und dann wieder ein, um den Abschluss zu beenden.  
  
    > [!IMPORTANT]  
    > Es wird empfohlen, dass Sie den ausschalten und dann wieder einschalten (manchmal auch als Stromkreislauf bezeichnet), da die Änderungen erst nach diesem Vorgang auf einigen Computern angewendet werden.  
  
Überprüfen Sie als nächstes das Hyper-V-Hypervisor-Ereignisprotokoll. Wenn Probleme auftreten, überprüfen Sie auch das System Protokoll.  
  
#### <a name="to-check-the-event-logs"></a>So überprüfen Sie die Ereignisprotokolle  
  
1.  Öffnen Sie die Ereignisanzeige. Klicken Sie auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Ereignisanzeige**.  
  
2.  Öffnen Sie das Hyper-V-Hypervisor-Ereignisprotokoll. Erweitern Sie im Navigationsbereich die Option **Anwendungs-und Dienst Protokolle** >> **Microsoft** >> **Windows** >> **Hyper-V-Hypervisor**, und klicken Sie dann auf **Operational**.  
  
3.  Wenn der Windows-Hypervisor ausgeführt wird, ist keine weitere Aktion erforderlich. Wenn Windows-Hypervisor nicht ausgeführt wird, gehen Sie wie folgt vor:  
  
4.  Öffnen Sie das System Protokoll. (Erweitern Sie im Navigationsbereich die Option **Windows-Protokolle** , und wählen Sie dann **System**aus.)  
  
5.  Verwenden Sie einen Filter, um Hyper-V-Hypervisor-Ereignisse zu suchen:   
    1. Klicken Sie im Bereich **Aktionen** auf **Aktuelles Protokoll filtern**. Geben Sie für **Ereignis Quellen**"Hyper-V-Hypervisor" an.   
    2. Suchen Sie nach Ereignissen, die Probleme melden. Die Ereignis-ID 41 zeigt beispielsweise ein Problem mit der BIOS-Konfiguration an: "Fehler beim Starten von Hyper-V. VMX ist im BIOS nicht vorhanden oder nicht aktiviert. "  
  
### <a name="see-also"></a>Siehe auch  
Ausführliche Informationen zur Verwendung von Hyper-v unter Windows 10, einschließlich der Überprüfung, ob Hyper-v auf Ihrem Computer ausgeführt werden kann, finden Sie unter [System Anforderungen für Windows 10 Hyper-v](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility). 


