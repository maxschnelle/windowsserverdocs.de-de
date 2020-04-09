---
title: Neues in Windows Server 2016 Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: affff774-5fa6-4944-887a-9bfde05f6a3f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 420d3b043959b8b1201aad7a5b3210fd9bd6a0da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817753"
---
# <a name="whats-new-in-windows-server-2016-essentials"></a>Neues in Windows Server 2016 Essentials

> Gilt für: Windows Server 2016 Essentials

Im folgenden finden Sie neue und erweiterte Features in Windows Server 2016 Essentials.

## <a name="integration-with-azure-site-recovery-services"></a>[Integration in Azure Site Recovery Services](azure-site-recovery-services-integration.md)

** --&reg;** , wenn ein virtueller Computer, der geschützt ist, fehlschlägt oder der Host Server, auf dem der geschützte virtuelle Computer ausgeführt wird, fehlschlägt, behält das Failover mit Azure Site Recovery Diensten die Geschäftskontinuität bei, bis der lokale virtuelle Computer oder der lokale Host Server repariert und verfügbar ist. 

**Funktionsweise** : Azure Site Recovery Dienste, die in Microsoft Azure angeboten werden, ermöglichen die Echt Zeit Replikation ihrer virtuellen Computer in einem Sicherungs Tresor in Azure. Wenn Ihr Server oder Standort aufgrund eines Hardwarefehlers oder eines anderen Fehlers ausfällt, können Sie ein Failover mit Azure Site Recovery-Diensten ausführen, sodass das in Ihrem Sicherungs Tresor gespeicherte VM-Image als laufender virtueller Computer in Azure bereitgestellt wird. In Kombination mit einem virtuellen Azure-Netzwerk stellen Client-PCs, die zuvor mit dem lokalen Server verbunden waren, eine transparente Verbindung mit dem Server her, der in Azure ausgeführt wird.     
                                                                                                                                                                                                                                                                                                               

## <a name="integration-with-azure-virtual-network"></a>[Integration in Azure Virtual Network](azure-virtual-network-integration.md)

Funktions **Weise: Wenn**Organisationen ihre Cloud Computing machen, verschieben Sie Ihre Ressourcen selten gleichzeitig. Vielmehr verschieben Sie einige Ressourcen in die Cloud und behalten einige vor Ort. Auf diese Weise ist es ganz einfach, eine Organisation in Phasen im Laufe der Zeit in die Cloud zu verlagern. Die Azure Virtual Network-Integration bietet die Netzwerkinfrastruktur, mit der dieser Prozess nahtlos und verwaltbar wird.

**Funktionsweise** : virtuelle Azure-Netzwerke sind ein Dienst, der in Microsoft Azure angeboten wird, mit dem Organisationen ein virtuelles privates Netzwerk (Punkt-zu-Punkt-oder Standort-zu-Standort) erstellen können, in dem die in Azure (z. b. virtuelle Computer und Speicher) laufenden Ressourcen so aussehen, dass Sie sich im lokalen Netzwerk befinden, um den Zugriff auf Anwendungen und Ressourcen zu ermöglichen.



## <a name="support-for-larger-deployments"></a>[Unterstützung für größere bereit Stellungen](support-for-larger-deployments.md) 

Einige größere kleine Unternehmen benötigen mehr Funktionalität und Kapazität für eine effektive Implementierung von Windows Server Essentials. Windows Server 2016 Essentials bietet eine bessere Verwaltbarkeit von Domänen, Benutzern und Geräten durch Hinzufügen von Unterstützung für größere bereit Stellungen mit:                                                                                                                                                                                                 

 - mehrere Domänen
 - mehrere Domänen Controller                                                                                                                                                                                                                                        
 - Möglichkeit zum Angeben eines bestimmten Domänen Controllers                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

<a name="see-also"></a>Siehe auch
--------

[Beginnen Sie mit der Verwendung von Windows Server Essentials](get-started.md) &copy;&reg;