---
title: Die Zertifikat basierte Authentifizierung ist konfiguriert, aber das angegebene Zertifikat ist nicht auf dem Replikat Server oder den Failoverclusterknoten installiert.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0b107a4760cc3470c7f80d53feef00a2f8f789c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365202"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>Die Zertifikat basierte Authentifizierung ist konfiguriert, aber das angegebene Zertifikat ist nicht auf dem Replikat Server oder den Failoverclusterknoten installiert.

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Das Sicherheitszertifikat, mit dem das Hyper-V-Replikat konfiguriert wurde, um die Zertifikat basierte Replikation bereitzustellen, ist nicht auf dem Replikat Server (oder einem Failoverclusterknoten) installiert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*bei einem Cluster Failover oder zum Verschieben auf einen anderen Knoten wird die Hyper-V-Replikation angehalten, wenn auf dem neuen Knoten nicht auch das entsprechende Zertifikat installiert ist. Dies wirkt sich auf die folgenden Knoten aus:*  
  
\<liste der Knoten >  
  
## <a name="resolution"></a>Auflösung  
  
*Installieren Sie das konfigurierte Zertifikat auf dem Replikat Server (und ggf. auf allen zugehörigen Knoten im Failovercluster).*  
  


