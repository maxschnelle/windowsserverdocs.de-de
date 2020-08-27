---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: Technische Referenz für virtualisierte Domänencontroller, Anhang
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6387abbe150630d2fd8f6f14724618a6ab32b94a
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88940280"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>Technische Referenz für virtualisierte Domänencontroller, Anhang

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema behandelt Folgendes:

-   [Terminologie](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)

-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)

## <a name="terminology"></a><a name="BKMK_Terms"></a>Begriff

-   **Snapshot** : der Zustand einer virtuellen Maschine zu einem bestimmten Zeitpunkt. Es hängt von der Kette früherer, auf der Hardware und der Virtualisierungsplattform ausgeführten Momentaufnahmen ab.

-   **Klonen** : eine komplette und separate Kopie eines virtuellen Computers. Es hängt von der virtuellen Hardware (Hypervisor) ab.

-   **Vollständiger Klon** : ein vollständiger Klon ist eine unabhängige Kopie eines virtuellen Computers, der nach dem Klon Vorgang keine Ressourcen mit der übergeordneten virtuellen Maschine freigibt. Der laufende Vorgang eines vollständigen Klons ist vollständig von dem übergeordneten virtuellen Computer getrennt.

-   **Differenzierender** Datenträger: eine Kopie eines virtuellen Computers, der virtuelle Datenträger mit der übergeordneten virtuellen Maschine in laufender Weise freigibt. Dadurch wird normalerweise der Speicherplatz auf dem Datenträger belegt, und mehrere virtuelle Computer können dieselbe Software Installation verwenden.

-   **VM Copy (Kopie**des virtuellen Computers): eine Dateisystem Kopie aller zugehörigen Dateien und Ordner einer virtuellen Maschine.

-   **VHD-Datei kopieren** -eine Kopie der VHD eines virtuellen Computers

-   **VM-Generations-ID** : eine 128-Bit-Ganzzahl, die dem virtuellen Computer durch den Hypervisor angegeben wird. Diese ID wird im Arbeitsspeicher gespeichert und jedes Mal zurückgesetzt, wenn eine Momentaufnahme angewendet wird. Beim Entwurf wird ein Hypervisor-agnostischer Mechanismus verwendet, mit dem die VM-Generations-ID auf dem virtuellen Computer angezeigt wird. Die Hyper-V-Implementierung macht die ID in der ACPI-Tabelle der virtuellen Maschine verfügbar.

-   **Import/Export** : eine Hyper-V-Funktion, die es dem Benutzer ermöglicht, den gesamten virtuellen Computer (VM-Dateien, VHD und die Computerkonfiguration) zu speichern. Anschließend können Benutzer diesen Satz von Dateien verwenden, um den Computer auf demselben Computer wie dieselbe VM (Wiederherstellung), auf einem anderen Computer wie die gleiche VM (verschieben) oder auf einem neuen virtuellen Computer (Kopie) wiederherzustellen.

## <a name="fixvdcpermissionsps1"></a><a name="BKMK_FixPDCPerms"></a>FixVDCPermissions.ps1

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



