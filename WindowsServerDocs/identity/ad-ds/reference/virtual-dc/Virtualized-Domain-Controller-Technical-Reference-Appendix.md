---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: Technische Referenz für virtualisierte Domänencontroller, Anhang
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9e3a5cc2c71455bb040f1311bdbfed1ac7e213fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832231"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>Technische Referenz für virtualisierte Domänencontroller, Anhang

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden folgende Inhalte behandelt:  
  
-   [Terminologie](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>Terminologie  
  
-   **Momentaufnahme** -der Status eines virtuellen Computers zu einem bestimmten Zeitpunkt. Es richtet sich in der Kette der vorherigen Momentaufnahmen, auf der Hardware, und klicken Sie auf der Virtualization-Plattform.  
  
-   **Klon** : abgeschlossen, und trennen Sie die Kopie eines virtuellen Computers. Es ist die virtuelle Hardware (Hypervisor) abhängig.  
  
-   **Vollständiger Klon** – ein vollständiger Klon ist eine unabhängige Kopie einer virtuellen Maschine, die keine Ressourcen mit dem übergeordneten virtuellen Computer nach der Klonvorgang freigibt. Aufrechterhaltung der ein vollständiger Klon ist vollständig von der übergeordneten virtuellen Computer getrennt.  
  
-   **Differenzierende Datenträger** -eine Kopie eines virtuellen Computers, der virtuelle Datenträger mit dem übergeordneten virtuellen Computer in einer laufenden Weise freigibt. Dadurch in der Regel spart Speicherplatz und mehrere virtuelle Computer, die gleiche Softwareinstallation verwenden.  
  
-   **VM kopieren**– eine Datei kopieren alle zugehörigen Dateien und Ordner eines virtuellen Computers.  
  
-   **Kopieren einer VHD-Datei** -eine Kopie eines virtuellen Computers VHD  
  
-   **VM-Generations-ID** : Ein 128-Bit-Ganzzahl, die mit dem virtuellen Computer vom Hypervisor zugewiesen. Diese ID wird im Arbeitsspeicher gespeichert und zurückgesetzt wird jedes Mal, wenn eine Momentaufnahme angewendet wird. Der Entwurf verwendet einen Unabhängigkeit von der Hypervisor-Mechanismus für die VM-Generations-ID auf dem virtuellen Computer anzeigen. Die Hyper-V-Implementierung stellt die ID des virtuellen Computers der ACPI-Tabelle.  
  
-   **Import/Export-** – ein Hyper-V-Feature, das dem Benutzer ermöglicht, den gesamten virtuellen Computer (VM-Dateien, virtuelle Festplatte und die Konfiguration des Computers) zu speichern. Damit können dann Benutzer mit diesem Satz von Dateien, schalten Sie den Computer wieder auf dem gleichen Computer wie den gleichen virtuellen Computer (Wiederherstellung), auf einem anderen Computer als dem gleichen virtuellen Computer (verschieben) oder einen neuen virtuellen Computer (Kopie)  
  
## <a name="BKMK_FixPDCPerms"></a>FixVDCPermissions.ps1  
  
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
  


