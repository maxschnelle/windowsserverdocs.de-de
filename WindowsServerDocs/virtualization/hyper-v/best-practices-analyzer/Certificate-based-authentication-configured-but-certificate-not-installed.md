---
title: Die Zertifikat basierte Authentifizierung ist konfiguriert, aber das angegebene Zertifikat ist nicht auf dem Replikat Server oder den Failoverclusterknoten installiert.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
ms.date: 8/16/2016
ms.openlocfilehash: 545a51f110a264e1fb456039362e373a51bcb2f8
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745865"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>Die Zertifikat basierte Authentifizierung ist konfiguriert, aber das angegebene Zertifikat ist nicht auf dem Replikat Server oder den Failoverclusterknoten installiert.

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Das Sicherheitszertifikat, mit dem das Hyper-V-Replikat konfiguriert wurde, um die Zertifikat basierte Replikation bereitzustellen, ist nicht auf dem Replikat Server (oder einem Failoverclusterknoten) installiert.*

## <a name="impact"></a>Auswirkung

*Wenn ein Cluster Failover oder ein Wechsel zu einem anderen Knoten ausgeführt wird, wird die Hyper-V-Replikation angehalten, wenn auf dem neuen Knoten nicht auch das entsprechende Zertifikat installiert ist. Dies wirkt sich auf die folgenden Knoten aus:*

\<list of nodes>

## <a name="resolution"></a>Lösung

*Installieren Sie das konfigurierte Zertifikat auf dem Replikat Server (und ggf. auf allen zugehörigen Knoten im Failovercluster).*



