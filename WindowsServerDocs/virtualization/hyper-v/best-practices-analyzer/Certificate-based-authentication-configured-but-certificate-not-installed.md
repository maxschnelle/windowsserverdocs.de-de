---
title: Zertifikatbasierte Authentifizierung konfiguriert ist, aber das angegebene Zertifikat ist nicht installiert, auf dem Replikatserver oder -Failoverclusterknoten
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: feef30d2f798057e4bd8e53ebab240af6b1d25b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832941"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>Zertifikatbasierte Authentifizierung konfiguriert ist, aber das angegebene Zertifikat ist nicht installiert, auf dem Replikatserver oder -Failoverclusterknoten

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Das Sicherheitszertifikat, das Hyper-V-Replikat konfiguriert wurde. um angeben, dass das Zertifikat-basierte Replikation nicht auf dem Replikatserver (oder alle Failoverclusterknoten) installiert ist.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Im Falle eines clusterfailovers durchgeführt oder in einem anderen Knoten verschieben hält Hyper-V-Replikation, wenn der neue Knoten nicht auch das entsprechende Zertifikat installiert haben. Dies wirkt sich auf die folgenden Knoten aus:*  
  
\<Liste der Knoten >  
  
## <a name="resolution"></a>Auflösung  
  
*Installieren Sie das konfigurierte Zertifikat auf dem Replikat-Server (und alle zugehörigen Knoten im Failovercluster wird ausgeführt, sofern vorhanden).*  
  


