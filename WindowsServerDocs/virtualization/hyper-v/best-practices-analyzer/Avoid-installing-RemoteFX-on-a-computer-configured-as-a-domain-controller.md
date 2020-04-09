---
title: Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 597dd26d0a317ca026cd94ab29138ce679d7c3b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857763"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Remotefx ist auf einem Domänen Controller installiert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Für remotefx konfigurierte virtuelle Computer können auf diesen Computern nicht verwendet werden.*  
  
## <a name="resolution"></a>**Lösung**  
*Entscheiden Sie, ob dieser Server entweder mit remotefx für Hyper-V oder als Active Directory-Domäne Controller konfiguriert werden soll, und konfigurieren Sie den Server bei Bedarf neu.*  
  


