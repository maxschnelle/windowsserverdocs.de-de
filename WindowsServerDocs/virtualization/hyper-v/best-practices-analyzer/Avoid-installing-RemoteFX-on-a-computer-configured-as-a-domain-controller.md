---
title: Vermeiden Sie die Installation von RemoteFX auf einem Computer, der als Active Directory-Domänencontroller konfiguriert ist
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9e1c642e3f36b5fe25f34bb417a83b8510adcc02
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832561"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Vermeiden Sie die Installation von RemoteFX auf einem Computer, der als Active Directory-Domänencontroller konfiguriert ist

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*RemoteFX ist auf einem Domänencontroller installiert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Virtuelle Computer, die für RemoteFX konfiguriert, können nicht auf diesen Computern verwendet werden.*  
  
## <a name="resolution"></a>**Lösung**  
*Entscheiden Sie, ob Sie möchten diese Server werden entweder mit RemoteFX konfiguriert werden, für Hyper-V oder als eine Active Directory-Domänencontroller, und klicken Sie dann den Server nach Bedarf neu konfigurieren.*  
  


