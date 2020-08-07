---
title: Autorisierungs Einträge sollten unterschiedliche Vertrauens Gruppennamen für primäre Server mit virtuellen Computern aufweisen, die nicht zur gleichen Vertrauens Gruppe gehören.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8827a3a7-9f3c-4f51-826a-8e2ec43e01df
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 53cb81e0071dee09feffb6e37f2ab6dbece27d28
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970007"
---
# <a name="authorization-entries-should-have-distinct-trust-group-names-for-primary-servers-with-virtual-machines-that-are-not-part-of-the-same-trust-group"></a>Autorisierungs Einträge sollten unterschiedliche Vertrauens Gruppennamen für primäre Server mit virtuellen Computern aufweisen, die nicht zur gleichen Vertrauens Gruppe gehören.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Der Server akzeptiert Replikations Anforderungen für den virtuellen Replikat Computer von einem beliebigen Server in der Autorisierungs Liste, der dem gleichen replikationstag wie der virtuelle Computer zugeordnet ist.*

## <a name="impact"></a>**Auswirkungen**
*Es kann zu Datenschutz-und Sicherheitsproblemen mit einem virtuellen Computer kommen, der die Replikation von primären Servern mit unterschiedlichen Autorisierungs Einträgen akzeptiert. Dies wirkt sich auf die folgenden Autorisierungs Einträge aus:\<list of authorization entries>*

## <a name="resolution"></a>**Lösung**
*Verwenden Sie unterschiedliche Tags in den Autorisierungs Einträgen für primäre Server mit virtuellen Maschinen, die nicht zur gleichen Sicherheitsgruppe gehören. Ändern Sie die Hyper-V-Einstellungen, um die Replikations Tags zu konfigurieren.*



