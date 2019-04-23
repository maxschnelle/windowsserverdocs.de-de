---
title: Domänenmitgliedschaft empfiehlt sich für Server mit Hyper-V
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e9db1d28cfe1ae4afd6c5dc1a93253c83fc42113
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860901"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>Domänenmitgliedschaft empfiehlt sich für Server mit Hyper-V

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Dieser Server ist ein Mitglied einer Arbeitsgruppe.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Es gibt keine zentrale Verwaltung für diesen Server aus.*  
  
Hinzufügen von diesem Computer zur Domäne ermöglicht die zentralisierte Verwaltung über Richtlinien für Identität, Sicherheit und Überwachung.  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn Sie eine domänenumgebung verfügbar haben, Verbinden des Servers mit der Domäne.*  
  
> [!IMPORTANT]  
> Es wird empfohlen, die arbeitsauslastungen auf dem virtuellen Computer auf diesem Computer zu ermitteln, ob es sind Sicherheitsaspekte bei der diese Computer zu einer Domäne beitreten zu überprüfen. Wenn die virtuellen Computer virtualisierte Domänencontroller sind, finden Sie unter [erwägungen bezüglich der Kapazitätsplanung für virtualisierte Domänencontroller](https://go.microsoft.com/fwlink/?LinkId=190192) (https://go.microsoft.com/fwlink/?LinkId=190192).  
  
Hinzufügen eines Computers zu einer Domäne erfordert die Berechtigungen auf dem Computer und der Domäne:   
- Auf dem Computer benötigen Sie ein Benutzerkonto, das Mitglied der Gruppe "Administratoren" ist. Melden Sie sich bei dieser Art von Konto, oder geben Sie den Benutzernamen und das Kennwort für das Konto, wenn Sie aufgefordert werden.   
- Auf die Domäne benötigen Sie ein Benutzerkonto an, die zum Beitritt zur Domäne autorisiert wurde. Sie werden für den Benutzernamen und Kennwort aufgefordert werden.  
  
Anweisungen hierzu finden Sie unter [fügen Sie den Computer der Domäne](https://go.microsoft.com/fwlink/?LinkId=190193) (https://go.microsoft.com/fwlink/?LinkId=190193).  
  


