---
ms.assetid: 3ecb6e87-17f1-4d38-97d2-9c4d52b7cf39
title: Planen der Verbundserverproxy-Kapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: eedb0f2ae4b6f600eb578c5db857cc1d79bccbd1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407985"
---
# <a name="planning-for-federation-server-proxy-capacity"></a>Planen der Verbundserverproxy-Kapazität

Mithilfe der Kapazitätsplanung für Verbund Server Proxys können Sie Folgendes schätzen:  
  
-   Die erforderlichen Hardwareanforderungen für jeden Verbund Server Proxy.  
  
-   Die Anzahl der Verbund Server und Verbund Server Proxys, die in jeder Organisation platziert werden sollen.  
  
Verbund Server Proxys leiten Sicherheits Token von einem geschützten Verbund Server im Unternehmensnetzwerk an Verbund Benutzer um. Der Zweck der Bereitstellung eines Verbund Server Proxys besteht darin, externen Benutzern das Herstellen einer Verbindung mit einem Verbund Server zu ermöglichen. In der AD FS Konfigurations Datenbank werden keine Token signiert oder in Daten geschrieben. Daher sind die Hardwareanforderungen für den Verbund Server Proxy in der Regel niedriger als die Hardwareanforderungen für einen Verbund Server.  
  
Da jede Anforderung an einen Verbund Server Proxy zu einer Anforderung an einen Verbund Server oder eine Verbund Serverfarm führt, muss die Kapazitätsplanung für Verbund Server und Verbund Server Proxys parallel ausgeführt werden.  
  
Wenn Sie die Spitzen Signatur\-pro Sekunde für den Verbund Server Proxy schätzen, müssen Sie sich mit den Verwendungs Mustern der Verbund Benutzer, die sich über den Verbund Server Proxy anmelden werden, vertraut machen. In vielen bereit Stellungen befinden sich die Verbund Benutzer, die sich mit dem Verbund Server Proxy anmelden, im Internet. Sie können die Spitzen\-pro Sekunde schätzen, indem Sie sich die Nutzungsmuster dieser Verbund Benutzer auf den vorhandenen Webanwendungen ansehen, die durch AD FS geschützt werden.  
  
> [!NOTE]  
> Bei Produktions Bereitstellungen wird empfohlen, für jede bereitgestellte Instanz der Verbund Serverfarm mindestens zwei Verbund Server Proxys zu installieren.  
  
## <a name="estimate-the-number-of-federation-server-proxies-required-for-your-organization"></a>Schätzen Sie die Anzahl der für Ihre Organisation benötigten Verbund Server Proxys.  
Bevor Sie die Anzahl der erforderlichen AD FS Verbund Server Proxy-Computer einschätzen können, müssen Sie zuerst die Gesamtzahl der Verbund Server ermitteln, die Sie in Ihrer Organisation bereitstellen werden. Weitere Informationen hierzu finden Sie unter [Planning for Federation Server Capacity](Planning-for-Federation-Server-Capacity.md).  
  
Nachdem Sie sich für die Anzahl der Verbund Server entschieden haben, Multiplizieren Sie diese Anzahl von Servern mit dem Prozentsatz der eingehenden Verbund Authentifizierungsanforderungen, die von externen Benutzern durchgeführt werden, \(sich außerhalb des Unternehmensnetzwerks\)befinden. Der Wert dieser Berechnung bietet Ihnen die geschätzte Anzahl von Verbund Server Proxys, die die eingehenden Authentifizierungsanforderungen Ihrer externen Benutzer verarbeiten.  
  
Wenn beispielsweise die Anzahl der empfohlenen Verbund Server 3 beträgt und Sie erwarten, dass die Gesamtzahl der Authentifizierungsanforderungen, die von externen Benutzern durchgeführt werden, ungefähr 60% der Gesamtanzahl der Verbund Authentifizierungsanforderungen beträgt, wäre ihre Berechnung gleich 1,8 \(3 X. 60\) den Sie auf 2 Runden können.  Daher müssen Sie in diesem Fall zwei Verbund Server Proxy-Computer bereitstellen, um die Auslastung der Authentifizierungsanforderungen externer Benutzer für die drei Verbund Server zu ermöglichen.  
  
In den vom AD FS-Produktteam ausgeführten Tests war die CPU-Gesamtauslastung auf den einzelnen Verbund Server Proxys erheblich niedriger als die CPU-Auslastung, die auf den Verbund Servern für dieselbe Farm beobachtet wurde.  In einem Test, während eine Verbund Server-CPU darauf hinweist, dass Sie vollständig ausgelastet war, wurde die CPU eines Verbund Server Proxys, der Proxy Dienste für dieselbe Farm bereitstellt, nur mit einer Auslastung von 20% beobachtet. Aus diesem Grund haben unsere Tests ergeben, dass die Auslastung der CPU eines Verbund Server Proxys, der ähnliche Hardware Spezifikationen verwendet, wie weiter oben in diesem Abschnitt erläutert, die Verarbeitungs Last für ungefähr drei Verbund Server in angemessener Weise verarbeiten kann.  
  
Aus Gründen der Fehlertoleranz empfiehlt es sich jedoch, für jede bereitgestellte Verbund Serverfarm mindestens zwei Verbund Server Proxys zu erhalten.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
