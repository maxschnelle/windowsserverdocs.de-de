---
title: Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ec5415d0bdad10c4b0f4f0560141dd290eca8e36
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954497"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.

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
*Mindestens eine für die Replikation ausgewählte virtuelle Maschine ist für die Kerberos-Authentifizierung konfiguriert.*

## <a name="impact"></a>**Auswirkungen**
*Der Netzwerk Datenverkehr für die Replikation vom primären Server zum Replikationsserver ist nicht verschlüsselt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Wenn eine andere Methode zum Durchführen der Verschlüsselung verwendet wird, können Sie dies ignorieren. Andernfalls ändern Sie die Einstellungen der virtuellen Maschine, um die Zertifikat basierte Authentifizierung auszuwählen.*



