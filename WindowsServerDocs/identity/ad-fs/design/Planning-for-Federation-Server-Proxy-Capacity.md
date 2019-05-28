---
ms.assetid: 3ecb6e87-17f1-4d38-97d2-9c4d52b7cf39
title: Planen der Verbundserverproxy-Kapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c3efbb4081336ebfdfe9d3ab8a2b91412aa82dee
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191079"
---
# <a name="planning-for-federation-server-proxy-capacity"></a>Planen der Verbundserverproxy-Kapazität

Planen der Kapazität für Verbundserverproxys können Sie besser einschätzen:  
  
-   Die entsprechenden hardwareanforderungen für jeden Verbundserverproxy.  
  
-   Die Anzahl der Verbundserver und Verbundserverproxys in jeder Organisation platziert.  
  
Verbundserverproxys umleiten Sicherheitstoken von einem geschützten Verbundserver im Unternehmensnetzwerk für Verbundbenutzer. Der Zweck der Bereitstellung eines Verbundserverproxys werden externe Benutzer auf die mit einem Verbundserver herstellen können. Es ist nicht tatsächlich Signatur von Token, oder Schreiben von Daten in der AD FS-Konfigurationsdatenbank. Aus diesem Grund sind die hardwareanforderungen für den Verbundserverproxy in der Regel geringer als die hardwareanforderungen für einen Verbundserver.  
  
Da jede Anforderung an eines Verbundserverproxys in einer Anforderung an einen Verbundserver oder eine Verbundserverfarm ausgeführt werden, muss die kapazitätsplanung für den Verbundserver und Verbundserverproxys parallel ausgeführt werden.  
  
Einschätzen der Spitze anmelden\-ins pro Sekunde für den Verbundserverproxy muss über die Verwendungsmuster der Partnerbenutzer, die durch den Verbundserverproxy anmelden werden. Der verbundene Benutzer melden Sie sich mit dem Verbundserverproxy befinden sich in vielen Bereitstellungen im Internet. Können Sie schätzen, die maximale anmelden\-ins pro Sekunde anhand der Verwendungsmuster diese Verbundbenutzer für die vorhandenen Webanwendungen, die von AD FS geschützt werden.  
  
> [!NOTE]  
> Für produktionsbereitstellungen empfehlen wir mindestens zwei Verbundserverproxys für jede Verbund-Server-farmverwaltungsdatenbank-Instanz, die Sie bereitstellen.  
  
## <a name="estimate-the-number-of-federation-server-proxies-required-for-your-organization"></a>Abschätzen der Anzahl der Verbundserverproxys für Ihre Organisation erforderlich sind  
Bevor Sie die Anzahl der einschätzen können AD FS Federation Server Proxy-Computer erforderlich sind, müssen Sie zunächst die Gesamtanzahl der Verbundserver zu bestimmen, die Sie in Ihrer Organisation bereitstellen. Weitere Informationen hierzu finden Sie unter [Planen der verbundserverkapazität](Planning-for-Federation-Server-Capacity.md).  
  
Wenn Sie mehrfach auf die Anzahl der Verbundserver, entschieden haben diese Anzahl von Servern anhand des Prozentsatzes der eingehenden Verbundauthentifizierung fordert an, dass Sie erwarten, dass von externen Benutzern erfolgt \(befindet sich außerhalb des Unternehmensnetzwerks\). Der Wert, der Berechnung wird mit der geschätzten Anzahl von Verbundserverproxys bereitgestellt werden, die die eingehenden authentifizierungsanforderungen für die für externe Benutzer behandelt.  
  
Z. B. wenn die Anzahl der empfohlenen Verbundserver 3 beträgt, und Sie, dass erwarten die Gesamtanzahl von authentifizierungsanforderungen, die von externen Benutzern vorgenommen werden, werden ca. 60 % der Gesamtanzahl von Anforderungen mit Verbundauthentifizierung, Ihre Berechnung würde 1.8 gleich \(3 X.60\) die Sie runden können bis zu 2.  Aus diesem Grund würde in diesem Fall sollen zwei Federation Server Proxy-Computer zur Aufnahme das Laden der externe Benutzer-authentifizierungsanforderungen für die drei Verbundserver bereitstellen.  
  
Tests, die vom AD FS-Produktteam ausgeführt wurde die gesamte CPU-Auslastung auf jedem Verbundserverproxy deutlich niedriger als die CPU-Auslastung sein, die auf den Verbundservern für die der gleichen Farm beobachtet wurde gefunden.  Zwar einen Verbundserver CPU, der angibt, wurde, dass es vollständig ausgeschöpft wurde, wurde die CPU für einen Verbundserverproxy Proxydienste für diese gleichen Farm Bereitstellen in einem Test nur 20 % Auslastung festgestellt. Aus diesem Grund offengelegt unsere Tests an, dass die Last für die CPU eines Verbundserverproxys, das ähnliche Hardwarespezifikationen verwendet wie beschrieben weiter oben in diesem Abschnitt, die Verarbeitungslast für ungefähr drei Verbundserver angemessen verarbeiten kann.  
  
Es wird jedoch empfohlen für Fehlertoleranz sollten mindestens zwei Verbundserverproxys für jede Verbundserverfarm, die Sie bereitstellen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
