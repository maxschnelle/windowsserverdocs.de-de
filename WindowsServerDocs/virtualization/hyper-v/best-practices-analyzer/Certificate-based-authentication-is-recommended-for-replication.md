---
title: Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
ms.date: 8/16/2016
ms.openlocfilehash: 3ef11472c042e19de9f7ee52ea5958ca0bf6e44b
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745855"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Mindestens eine für die Replikation ausgewählte virtuelle Maschine ist für die Kerberos-Authentifizierung konfiguriert.*

## <a name="impact"></a>**Auswirkungen**
*Der Netzwerk Datenverkehr für die Replikation vom primären Server zum Replikationsserver ist nicht verschlüsselt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Wenn eine andere Methode zum Durchführen der Verschlüsselung verwendet wird, können Sie dies ignorieren. Andernfalls ändern Sie die Einstellungen der virtuellen Maschine, um die Zertifikat basierte Authentifizierung auszuwählen.*



