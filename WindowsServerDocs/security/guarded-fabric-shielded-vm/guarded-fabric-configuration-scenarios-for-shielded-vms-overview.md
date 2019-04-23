---
title: Bereitstellen von abgeschirmten VMs
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: fa6da3f4a98686f83fff3937c2dc44fd4d623fe3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871011"
---
# <a name="deploy-shielded-vms"></a>Bereitstellen von abgeschirmten VMs


>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Themen wird beschrieben, wie ein Mandant mit abgeschirmten virtuellen Computern arbeiten kann.

1. (Optional) [Erstellen eines Windows-vorlagedatenträgers](guarded-fabric-create-a-shielded-vm-template.md) oder [Erstellen eines vorlagedatenträgers Linux](guarded-fabric-create-a-linux-shielded-vm-template.md). Der vorlagendatenträger kann durch den Mandanten oder der hosting-Anbieter erstellt werden. 

2. (Optional) [Konvertieren von einer vorhandenen Windows-VM in eine abgeschirmte VM](guarded-fabric-vm-shielding-helper-vhd.md). 

3. [Erstellen Sie Schutzdaten, die zum Definieren einer abgeschirmten VM](guarded-fabric-tenant-creates-shielding-data.md).

    Eine Beschreibung und ein Diagramm der schutzdatendatei, finden Sie unter [welche Daten Schutz ist und warum dies erforderlich ist?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)
    
    Weitere Informationen zum Erstellen einer Antwortdatei an eine geschützte Datendatei einschließt, finden Sie unter [abgeschirmte VMs: Generieren einer Antwortdatei mithilfe der Funktion New-ShieldingDataAnswerFile](guarded-fabric-sample-unattend-xml-file.md).

4. Erstellen einer abgeschirmten VMs:
 
    - Mithilfe von **Windows Azure Pack**: [Bereitstellen einer abgeschirmten VM mithilfe von Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - Mithilfe von **Virtual Machine Manager-**: [Bereitstellen einer abgeschirmten VM mithilfe von Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Erstellen einer abgeschirmten VM-Vorlage](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>Siehe auch

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
