---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: "Unterstützung nach \"Zugriff verweigert\" Szenario"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d6b8d8a094aa86fd5be78d2eae13bae50df3fd79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-access-denied-assistance"></a>Szenario: Unterstützung nach "Zugriff verweigert"

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Benutzer erhalten die Fehlermeldung "Zugriff verweigert", wenn sie versuchen, den Zugriff auf freigegebene Dateien und Ordner auf einem Dateiserver für den sie nicht über Berechtigungen verfügen. Administratoren müssen häufig keinen Zugriff, Problembehandlung zum Beheben des Problems schwierig ist den entsprechenden Kontext.  
  
## <a name="scenario-description"></a>Beschreibung des Szenarios  
Zugriff verweigert Unterstützung ist ein neues Feature in Windows Server2012, die folgenden Arten von Problemen, die verknüpft sind bietet Zugriff auf Dateien und Ordner:  
  
-   **Self-Unterstützung.** Wenn ein Benutzer kann das Problem bestimmen und das Problem zu beheben, damit sie den angeforderten Zugriff erhalten, die Auswirkung auf das Unternehmen ist niedrig, und keine besonderen Ausnahmen in der zentralen Zugriffsrichtlinie erforderlich sind. Unterstützung nach "Zugriff verweigert" enthält die Fehlermeldung "Zugriff verweigert", die dateiserveradministratoren mit Informationen, die für ihre Organisationen spezifisch anpassen können. Beispielsweise kann ein Administrator die Nachricht festlegen, damit Benutzer den Zugriff von einem Datenbesitzer anfordern können, ohne den dateiserveradministrator.  
  
-   **Unterstützung durch den Datenbesitzer.** Sie können eine Verteilerliste für freigegebene Ordner definieren und es so konfigurieren, dass der Besitzer des Ordners eine E-Mail-Benachrichtigung empfängt, wenn ein Benutzer Zugriff benötigt. Wenn der Datenbesitzer nicht wie die Benutzer zugreifen kann, kann der Besitzer diese Informationen an dem dateiserveradministrator weiterleiten.  
  
-   **Unterstützung durch den dateiserveradministrator.** Diese Art von Hilfe ist verfügbar, wenn der Benutzer ein Problem nicht beheben kann, und der Datenbesitzer dabei nicht helfen.  Windows Server2012 bietet eine Benutzeroberfläche, in denen dateiserveradministratoren die effektiven Berechtigungen für einen Benutzer auf eine Datei oder einen Ordner anzeigen können, damit es einfacher Zugriffsprobleme zu beheben ist.  
  
Unterstützung nach "Zugriff verweigert" in Windows Server2012 bietet dateiserveradministratoren die relevanten Zugriffsdetails, sodass sie das Problem und entsprechende Tools bestimmten können, damit sie die Änderungen an der Konfiguration, die die Zugriffsanforderung erfüllen vornehmen können. Beispielsweise kann ein Benutzer diesen Vorgang, um eine Datei zuzugreifen, die sie derzeit nicht den Zugriff auf folgen:  
  
-   Der Benutzer versucht, eine Datei im freigegebenen Ordner \\\financeshares zu lesen, aber der Server Zeigt eine Meldung "Zugriff verweigert".  
  
-    Windows Server2012 zeigt die Information Unterstützung nach "Zugriff verweigert", um dem Benutzer eine Option zum Anfordern von Hilfe.  
  
-   Wenn der Benutzer Zugriff auf die Ressource anfordert, sendet der Server eine E-Mail mit den Zugriffsanforderungsinformationen an den Besitzer des Ordners.  
  
Sie finden die Planungsinformationen für das Konfigurieren der Unterstützung nach "Zugriff verweigert" in [Denied Assistance planen](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1).  
  
Sehen Sie die Schrittezum Konfigurieren der Unterstützung nach "Zugriff verweigert" in [Denied Assistance & 40; Schrittezur Veranschaulichung & 41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Dieses Szenario ist Teil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>In der Praxis  
Unterstützung nach "Zugriff verweigert" in Windows Server2012 trägt zur dynamischen Zugriffssteuerung bei, indem Sie Benutzern die Möglichkeit zum Zugriff auf freigegebene Dateien und Ordner direkt über eine Meldung "Zugriff verweigert" gewährt wird.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgende Tabelle werden die Features, die in diesem Szenario sind aufgeführt und beschrieben, wie sie unterstützen.  
  
|Funktion|Wie sie dieses Szenario unterstützt|  
|-----------|---------------------------------|  
|[File Server Resource Manager (Übersicht)](https://technet.microsoft.com/library/hh831701.aspx)|Unterstützung nach "Zugriff verweigert" kann mithilfe der Ressourcen-Manager-Konsole auf dem Dateiserver konfiguriert werden.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|File Server Resource Manager ist ein Rollendienst der Datei- und Speicherdienste und besteht aus einer Reihe von Features, die zum Verwalten der Dateiserver in Ihrem Netzwerk verwendet werden kann.|  
  


