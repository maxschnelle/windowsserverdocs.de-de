---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: 'Szenario: der Zugriff verweigert-Unterstützung'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d6b8d8a094aa86fd5be78d2eae13bae50df3fd79
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829091"
---
# <a name="scenario-access-denied-assistance"></a>Szenario: Unterstützung nach "Zugriff verweigert"

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benutzern wird die Meldung „Zugriff verweigert“ angezeigt, wenn sie versuchen, auf freigegebene Dateien und Ordner auf einem Dateiserver zuzugreifen, für den Sie keine Berechtigungen haben. Administratoren liegt oftmals nicht der entsprechende Kontext vor, um das Zugriffsproblem zu lösen, wodurch das Lösen des Problems schwierig wird.  
  
## <a name="scenario-description"></a>Beschreibung des Szenarios  
Zugriff verweigert Unterstützung ist ein neues Feature in Windows Server 2012 bietet die folgenden Möglichkeiten, Probleme zu beheben, die verknüpft sind, die Zugriff auf Dateien und Ordner:  
  
-   **Selbstunterstützung** Wenn ein Benutzer das Problem bestimmen und rekonstruieren kann, sodass er den erforderlichen Zugriff erhält, ist die Auswirkung auf das Unternehmen gering. Ferner sind in diesem Fall keine besonderen Ausnahmen in der zentralen Zugriffsrichtlinie erforderlich. Die Unterstützung nach „Zugriff verweigert“ stellt die Meldung „Zugriff verweigert“ bereit, die Dateiserveradministratoren mit Informationen anpassen können, die für ihre Organisationen spezifisch sind. Ein Administrator könnte die Meldung beispielsweise so festlegen, dass Benutzer den Zugriff von einem Datenbesitzer anfordern könnten, ohne den Dateiserveradministrator einbeziehen zu müssen.  
  
-   **Unterstützung durch den Datenbesitzer.** Sie können eine Verteilerliste für freigegebene Ordner definieren und so konfigurieren, dass der Ordnerbesitzer eine E-Mail-Benachrichtigung erhält, wenn ein Benutzer Zugriff darauf benötigt. Wenn der Datenbesitzer nicht weiß, wie er dem Benutzer in Bezug auf den Zugriff helfen kann, kann der Besitzer diese Informationen an den Dateiserveradministrator weiterleiten.  
  
-   **Unterstützung durch den Dateiserveradministrator.** Dieser Unterstützungstyp steht zur Verfügung, wenn der Benutzer ein Problem nicht beheben kann und ihm der Datenbesitzer dabei nicht helfen kann.  Windows Server 2012 bietet eine Benutzeroberfläche, in denen dateiserveradministratoren die effektiven Berechtigungen für einen Benutzer in einer Datei oder Ordner anzeigen können, damit sie einfacher Probleme behoben werden.  
  
Zugriff verweigert-Unterstützung in Windows Server 2012 stellt dateiserveradministratoren die relevanten Zugriffsdetails, sodass sie das Problem und entsprechende Tools bestimmten können, damit konfigurationsänderungen an die zugriffsanforderung erfüllen erfolgen kann. Beispielsweise könnte ein Benutzer diesem Vorgang folgen, um auf eine Datei zuzugreifen, für die er zurzeit keine Zugriffsrechte hat:  
  
-   Der Benutzer versucht, eine Datei im Lesen der \\\financeshares freigegebenen Ordner, der Server zeigt aber ein Zugriff-verweigert.  
  
-    Windows Server 2012 werden die Zugriff Informationen angezeigt, für den Benutzer mit einer Option zum Anfordern von Hilfe an.  
  
-   Wenn der Benutzer Zugriff auf die Ressource anfordert, sendet der Server eine E-Mail mit den Zugriffsanforderungsinformationen an den Ordnerbesitzer.  
  
Planungsinformationen für das Konfigurieren der Unterstützung nach „Zugriff verweigert“ finden Sie unter [Plan for Access-Denied Assistance](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1).  
  
Finden Sie Schritte zum Konfigurieren der Unterstützung bei der Zugriff verweigert [Denied Assistance &#40;Demonstrationsschritte&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
Zugriff verweigert-Unterstützung in Windows Server 2012 trägt zur dynamischen Zugriffssteuerung durch gewährt Benutzern den Zugriff auf freigegebene Dateien und Ordner direkt über ein Zugriff-verweigert.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[Übersicht über die Ressourcen-Manager](https://technet.microsoft.com/library/hh831701.aspx)|Die Unterstützung nach „Zugriff verweigert“ kann mithilfe der Konsole für den Ressourcen-Manager für Dateiserver auf dem Dateiserver konfiguriert werden.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|Der Ressourcen-Manager für Dateiserver ist ein Datei- und Speicherdienst-Rollendienst und besteht aus einem Satz an Features, die zum Verwalten der Dateiserver in Ihrem Netzwerk verwendet werden können.|  
  


