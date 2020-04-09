---
title: Bereitstellen von abgeschirmten VMs
ms.prod: windows-server
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f4550f8a92330c8f483e332ab9e4b36fda853b0a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856863"
---
# <a name="deploy-shielded-vms"></a>Bereitstellen von abgeschirmten VMs


>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In den folgenden Themen wird beschrieben, wie ein Mandant mit abgeschirmten VMS arbeiten kann.

1. Optionale [Erstellen Sie einen Windows-Vorlagen](guarded-fabric-create-a-shielded-vm-template.md) Datenträger, oder [Erstellen Sie einen Linux-Vorlagen](guarded-fabric-create-a-linux-shielded-vm-template.md) Der Vorlagen Datenträger kann entweder vom Mandanten oder vom hostingdienstanbieter erstellt werden. 

2. Optionale [Konvertieren einer vorhandenen Windows-VM in eine abgeschirmte VM](guarded-fabric-vm-shielding-helper-vhd.md) 

3. [Erstellen Sie Schutz Daten, um eine abgeschirmte VM zu definieren](guarded-fabric-tenant-creates-shielding-data.md).

    Eine Beschreibung und ein Diagramm für eine geschützte Datendatei finden [Sie unter Was sind geschützte Daten? und warum ist es notwendig?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)
    
    Informationen zum Erstellen einer Antwortdatei, die in eine geschützte Datendatei aufgenommen werden soll, finden Sie unter [abgeschirmte VMS: Generieren einer Antwortdatei mithilfe der New-shieldingdatabeantworungsdateifunktion](guarded-fabric-sample-unattend-xml-file.md).

4. Erstellen einer abgeschirmten VM:
 
    - Verwenden von **Windows Azure Pack**: bereitstellen [einer abgeschirmten VM mithilfe Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - Verwenden von **Virtual Machine Manager**: bereitstellen [einer abgeschirmten VM mithilfe Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Erstellen einer abgeschirmten VM-Vorlage](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>Siehe auch

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
