---
title: Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: c5e356792ba93d21d9ce130a46e1d60336c99844
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857673"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Mindestens eine für die Replikation ausgewählte virtuelle Maschine ist für die Kerberos-Authentifizierung konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Der Netzwerk Datenverkehr für die Replikation vom primären Server zum Replikationsserver ist nicht verschlüsselt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Wenn eine andere Methode zum Durchführen der Verschlüsselung verwendet wird, können Sie dies ignorieren. Andernfalls ändern Sie die Einstellungen der virtuellen Maschine, um die Zertifikat basierte Authentifizierung auszuwählen.*  
  


