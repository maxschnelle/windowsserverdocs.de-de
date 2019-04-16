---
ms.assetid: 3ecb6e87-17f1-4d38-97d2-9c4d52b7cf39
title: "Planen der Verbundserverproxy-Kapazität"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e57f34b173c10e9e753c7f3b8dcd88d7bf6742c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-federation-server-proxy-capacity"></a>Planen der Verbundserverproxy-Kapazität

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Kapazitätsplanung für Verbundserverproxys können Sie die schätzen:  
  
-   Die entsprechenden Hardwareanforderungen für jeden Verbundserverproxy.  
  
-   Die Anzahl der Verbundserver und Verbundserverproxys in jeder Organisation platzieren.  
  
Verbundserverproxys umleiten Sicherheitstoken aus einer geschützten Verbundserver im Unternehmensnetzwerk verbundene Benutzer. Der Zweck der Bereitstellung eines Verbundserverproxys werden externe Benutzer zum Herstellen eines Verbundservers zu ermöglichen. Es wird nicht tatsächlich Token zu signieren, oder Schreiben von Daten in der AD FS-Konfigurationsdatenbank. Aus diesem Grund sind die Hardwareanforderungen für den Verbundserverproxy normalerweise niedriger als die Hardwareanforderungen für einen Verbundserver.  
  
Da bei jeder Anfrage an einen Verbundserverproxy in einer Anforderung an einen Verbundserver oder eine Verbundserverfarm führt, muss Kapazitätsplanung für Verbundserver und Verbundserverproxys parallel ausgeführt werden.  
  
Schätzen die Spitze Standardparameter-ins pro Sekunde für den Verbundserverproxy muss über die Verwendungsmuster der die Verbundbenutzer, die durch den Verbundserverproxy anmelden. Melden Sie sich mit der Verbundserverproxy verbundenen Benutzer befinden sich in vielen Bereitstellungen im Internet. Sie können die maximale Standardparameter-ins pro Sekunde schätzen, anhand der Verwendungsmuster diese Verbundbenutzer auf den vorhandenen Web-Apps, die durch AD FS geschützt werden.  
  
> [!NOTE]  
> Für den Praxiseinsatz empfehlen wir mindestens zwei Verbundserverproxys für jede Federation Serverfarm-Instanz, die Sie bereitstellen.  
  
## <a name="estimate-the-number-of-federation-server-proxies-required-for-your-organization"></a>Abschätzen der Anzahl der Verbundserverproxys für Ihre Organisation erforderlich  
Bevor Sie die Anzahl der abschätzen können erforderlich AD FS Federation Server Proxy Maschinen, müssen Sie zunächst die Gesamtanzahl der Verbundserver zu bestimmen, die Sie in Ihrer Organisation bereitstellen. Weitere Informationen hierzu finden Sie unter [Planen der Verbundserverkapazität](Planning-for-Federation-Server-Capacity.md).  
  
Nachdem Sie mehrfach auf der Anzahl der Verbundserver entschieden haben diese Anzahl von Servern mit dem Prozentsatz der eingehenden Verbundauthentifizierung angefordert wird, dass Sie davon ausgehen, dass von externen Benutzern erfolgen \ (befindet sich außerhalb der Unternehmen vom Netzwerk). Der Wert dieser Berechnung wird die geschätzte Anzahl der Verbundserverproxys bereitgestellt werden, die eingehenden Authentifizierungsanforderungen für externe Benutzer behandelt.  
  
Wenn beispielsweise die Anzahl der empfohlenen Verbundserver 3, und Sie erwarten, dass die Gesamtanzahl der Authentifizierungsanforderungen, die von externen Benutzern erfolgt ca. 60% der Gesamtzahl der Verbundauthentifizierung Anforderungen werden, die Berechnung der würde gleich 1,8 \ (3 X. 60\) der Sie runden können bis zu 2.  Daher wäre in diesem Fall müssen Sie zum Bereitstellen von zwei Federation Server Proxy-Computer das Laden von externen Benutzer Authentifizierungsanforderungen für die drei Verbundserver angepasst.  
  
In von der AD FS-Produktteam ausgeführten Tests war die CPU-Gesamtauslastung auf jedem Verbundserverproxy deutlich niedriger als die CPU-Auslastung sein, die auf den Verbundservern für die gleichen Farm festgestellt wurde.  Während ein Verbundserver CPU, der angibt, war, dass es vollständig ausgelastet war, wurde CPU für einen Verbundserverproxy Proxy Dienste für die derselben Farm in einen Test nur 20% Auslastung beobachtet. Aus diesem Grund eingeblendet unsere Tests, dass die Belastung der CPU-Kapazität eines Verbundserverproxys, das ähnliche Hardwarespezifikationen verwendet wie beschrieben weiter oben in diesem Abschnitt, die Verarbeitungslast für ungefähr drei Verbundserver verarbeiten konnte.  
  
Es wird jedoch empfohlen für Fehlertoleranz sollten mindestens zwei Verbundserverproxys für jede Verbundserverfarm, die Sie bereitstellen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
