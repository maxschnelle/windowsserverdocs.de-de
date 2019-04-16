---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: "Technische Referenz zu virtualisierten Domänencontroller, Anhang"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e7f264a098b6f67d98c9aa47ec5794374b8920d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>Technische Referenz zu virtualisierten Domänencontroller, Anhang

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema behandelt:  
  
-   [Terminologie](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [Fixvdcpermissions. ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>Terminologie  
  
-   **Momentaufnahme** -den Zustand einer virtuellen Maschine zu einem bestimmten Zeitpunkt. Sie sind abhängig, in der Kette des vorherigen Momentaufnahmen, die Hardware, und klicken Sie auf der Virtualization-Plattform.  
  
-   **Klon** : ein abzuschließen und das Kopieren eines virtuellen Computers zu trennen. Es ist die virtuelle Hardware (Hypervisor) abhängig.  
  
-   **Vollständige Klon** -vollständige Klon wird eine separate Kopie einer virtuellen Maschine, die keine Ressourcen für die übergeordnete virtuelle Maschine nach der Klonvorgang freigegeben. Vollständige Klon laufenden Betrieb ist vollkommen unabhängig von der übergeordneten virtuellen Maschine.  
  
-   **Differenzierende Datenträger** -eine Kopie eines virtuellen Computers, der virtuelle Datenträger mit dem übergeordneten virtuellen Computer auf eine laufende Weise freigibt. Dies wird in der Regel spart Speicherplatz, und ermöglicht mehreren virtuellen Computern, die gleiche Softwareinstallation verwenden.  
  
-   **VM-Kopie**– eine Datei Kopieren aller zugehörigen Dateien und Ordner von einer virtuellen Maschine.  
  
-   **VHD-Datei kopieren** -eine Kopie der virtuellen Festplatte eines virtuellen Computers  
  
-   **VM-Generations-ID** – eine 128-Bit-Ganzzahl mit dem virtuellen Computer vom Hypervisor zugewiesen. Diese ID ist im Arbeitsspeicher gespeichert und jeder Anwendung eine Momentaufnahme zurückgesetzt. Der Entwurf verwendet einen Hypervisor-unabhängige Mechanismus zum Einblenden von VM-Generations-ID auf dem virtuellen Computer. Die Hyper-V-Implementierung gibt die ID der ACPI-Tabelle des virtuellen Computers an.  
  
-   **Importieren/Exportieren von** – ein Hyper-V-Feature, das dem Benutzer ermöglicht, speichern Sie den ganzen virtuellen Computer (VM-Dateien, virtuelle Festplatte und die Konfiguration des Computers). Sie können dann Benutzer mithilfe dieser Gruppe von Dateien, schalten Sie den Computer wieder auf demselben Computer wie den gleichen virtuellen Computer (Wiederherstellen), auf einem anderen Computer als dem gleichen virtuellen Computer (verschieben) oder eine neue virtuelle Maschine (Kopieren)  
  
## <a name="BKMK_FixPDCPerms"></a>Fixvdcpermissions. ps1  
  
```  
# Unsigned script, requires use of set-executionpolicy remotesigned -force  
# You must run the Windows PowerShell console as an elevated administrator  
  
# Load Active Directory Windows PowerShell Module and switch to AD DS drive  
import-module activedirectory  
cd ad:  
  
## Get Domain NC  
$domainNC = get-addomain  
  
## Get groups and obtain their SIDs   
$dcgroup = get-adgroup "Cloneable Domain Controllers"  
  
$sid1 = (get-adgroup $dcgroup).sid  
  
## Get the DACL of the domain  
$acl = get-acl $domainNC  
  
## The following object specific ACE grants extended right 'Allow a DC to create a clone of itself' for the CDC group to the Domain NC  
## 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e is the schemaIDGuid for 'DS-Clone-Domain-Controller"  
  
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e  
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid  
  
## Add the ACE in the ACL and set the ACL on the object   
  
$acl.AddAccessRule($ace1)  
set-acl -aclobject $acl $domainNC  
write-host "Done writing new VDC permissions."  
cd c:   
```  
  


