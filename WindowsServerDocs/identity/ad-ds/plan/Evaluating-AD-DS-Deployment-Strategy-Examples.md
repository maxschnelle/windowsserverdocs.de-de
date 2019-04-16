---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: 'Auswerten von AD DS-Bereitstellungsstrategie: Beispiele'
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4cac1e344cfed078927f2945048807d686deebd1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>Auswerten von AD DS-Bereitstellungsstrategie: Beispiele

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Berücksichtigen Sie das folgende Beispiel für einen fiktiven Unternehmen Contoso Pharmaceuticals, die Active Directory-Domänendienste (AD DS) in ihrer Umgebung bereitgestellt wird. Die Contoso-Umgebung besteht aus vier Domänen. Funktionsebene der Gesamtstruktur ist Windows Server2003. Die folgende Abbildungzeigt die aktuelle Domänenstruktur für die Contoso-Organisation.  
  
![AD DS-Bereitstellungsstrategie](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
Nach dem Überprüfen der vorhandenen Umgebung ist, und Identifizieren der Bereitstellungsziele, hergestellt Contoso die folgende AD DS-Bereitstellungsstrategie:  
  
-   Aktualisieren von Windows Server2003-Domänen auf Windows Server2008-Domänen.  
  
-   Aktivieren Sie erweiterte AD DS-Features, durch das Auslösen von Domänen- und Gesamtstrukturfunktionsebenen auf Windows Server2008.  
  
-   Strukturieren der africa.concorp.contoso.com Domänen innerhalb der Gesamtstruktur, die Domäne mit dem emea.concorp.contoso.con zu konsolidieren.  
  
Heraufstufen der Gesamtstrukturfunktionsebene auf Windows Server2008 können Contoso die neue AD DS-Features uneingeschränkt nutzen. Umstrukturieren von Domänen innerhalb der Gesamtstruktur, wie in der folgenden Abbildungdargestellt wird die Verwaltung reduzieren, die für die Verwaltung von Domänen erforderlich ist.  
  
![AD DS-Bereitstellungsstrategie](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


