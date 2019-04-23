---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: 'Bewerten der AD DS-Bereitstellungsstrategie: Beispiele'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 169d0a55f9fb167390c13ac1c89f8d68427f318d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842111"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>Bewerten der AD DS-Bereitstellungsstrategie: Beispiele

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Betrachten Sie das folgende Beispiel ein fiktives Unternehmen, Contoso Pharmaceuticals, mit denen Active Directory Domain Services (AD DS) in ihrer Umgebung bereitgestellt wird. Die Contoso-Umgebung besteht aus vier Domänen. Die Gesamtstruktur-Funktionsebene ist Windows Server 2003. Die folgende Abbildung zeigt die aktuelle Domänenstruktur für die Contoso-Organisation.  
  
![AD DS-Bereitstellungsstrategie](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
Nach dem Überprüfen der vorhandenen Umgebung und Identifizieren der Bereitstellungsziele hat Contoso die folgende AD DS-Bereitstellungsstrategie:  
  
-   Aktualisieren Sie Windows Server 2003-Domänen auf Windows Server 2008-Domänen.  
  
-   Aktivieren Sie erweiterte AD DS-Features, durch Auslösen der Funktionsebenen der Domäne und Gesamtstruktur auf Windows Server 2008.  
  
-   Strukturieren Sie die Domäne "africa.concorp.contoso.com" innerhalb der Gesamtstruktur, Domäne, mit dem emea.concorp.contoso.con zu konsolidieren.  
  
Heraufsetzen der Funktionsebene der Gesamtstruktur auf Windows Server 2008 können Contoso, der die neue AD DS-Features optimal nutzen. Umstrukturieren von Domänen innerhalb der Gesamtstruktur, wie in der folgenden Abbildung gezeigt wird die Verwaltung reduzieren, die für die Verwaltung von Domänen erforderlich ist.  
  
![AD DS-Bereitstellungsstrategie](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


