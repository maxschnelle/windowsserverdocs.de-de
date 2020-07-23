---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: Unterstützung für szenariozugriff verweigert
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2d3f0f7f0fa611ab34145aa35291ff9d07b0b205
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955952"
---
# <a name="scenario-access-denied-assistance"></a>Szenario: Unterstützung nach "Zugriff verweigert"

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benutzern wird die Meldung „Zugriff verweigert“ angezeigt, wenn sie versuchen, auf freigegebene Dateien und Ordner auf einem Dateiserver zuzugreifen, für den Sie keine Berechtigungen haben. Administratoren liegt oftmals nicht der entsprechende Kontext vor, um das Zugriffsproblem zu lösen, wodurch das Lösen des Problems schwierig wird.  
  
## <a name="scenario-description"></a>Beschreibung des Szenarios  
Die Unterstützung nach "Zugriff verweigert" ist ein neues Feature in Windows Server 2012, das die folgenden Möglichkeiten bietet, um Probleme im Zusammenhang mit dem Zugriff auf Dateien und Ordner zu beheben:  
  
-   **Selbstunterstützung** Wenn ein Benutzer das Problem bestimmen und rekonstruieren kann, sodass er den erforderlichen Zugriff erhält, ist die Auswirkung auf das Unternehmen gering. Ferner sind in diesem Fall keine besonderen Ausnahmen in der zentralen Zugriffsrichtlinie erforderlich. Die Unterstützung nach „Zugriff verweigert“ stellt die Meldung „Zugriff verweigert“ bereit, die Dateiserveradministratoren mit Informationen anpassen können, die für ihre Organisationen spezifisch sind. Ein Administrator könnte die Meldung beispielsweise so festlegen, dass Benutzer den Zugriff von einem Datenbesitzer anfordern könnten, ohne den Dateiserveradministrator einbeziehen zu müssen.  
  
-   **Unterstützung durch den Datenbesitzer.** Sie können eine Verteilerliste für freigegebene Ordner definieren und so konfigurieren, dass der Ordnerbesitzer eine E-Mail-Benachrichtigung erhält, wenn ein Benutzer Zugriff darauf benötigt. Wenn der Datenbesitzer nicht weiß, wie er dem Benutzer in Bezug auf den Zugriff helfen kann, kann der Besitzer diese Informationen an den Dateiserveradministrator weiterleiten.  
  
-   **Unterstützung durch den Dateiserveradministrator.** Dieser Unterstützungstyp steht zur Verfügung, wenn der Benutzer ein Problem nicht beheben kann und ihm der Datenbesitzer dabei nicht helfen kann.  Windows Server 2012 bietet eine Benutzeroberfläche, auf der Datei Server Administratoren die effektiven Berechtigungen für einen Benutzer für eine Datei oder einen Ordner anzeigen können, sodass Zugriffs Probleme einfacher behoben werden können.  
  
Die Unterstützung nach "Zugriff verweigert" in Windows Server 2012 stellt Datei Server Administratoren die relevanten Zugriffs Details bereit, sodass Sie das Problem und entsprechende Tools ermitteln können, damit Sie Konfigurationsänderungen vornehmen können, um die Zugriffs Anforderung zu erfüllen. Beispielsweise könnte ein Benutzer diesem Vorgang folgen, um auf eine Datei zuzugreifen, für die er zurzeit keine Zugriffsrechte hat:  
  
-   Der Benutzer versucht, eine Datei im frei \\ gegebenen Ordner "\financeshares" zu lesen, der Server zeigt aber die Meldung "Zugriff verweigert" an.  
  
-    Windows Server 2012 zeigt dem Benutzer die Informationen Unterstützung nach "Zugriff verweigert" mit einer Option zum Anfordern von Unterstützung an.  
  
-   Wenn der Benutzer Zugriff auf die Ressource anfordert, sendet der Server eine E-Mail mit den Zugriffsanforderungsinformationen an den Ordnerbesitzer.  
  
Planungsinformationen für das Konfigurieren der Unterstützung nach „Zugriff verweigert“ finden Sie unter [Plan für die Unterstützung nach "Zugriff verweigert"](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1).  
  
Schritte zum Konfigurieren der Unterstützung nach "Zugriff verweigert" finden Sie unter Bereitstellen der [Unterstützung nach "Zugriff verweigert" &#40;Demonstrations Schritte&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>Praktische Anwendung  
Die Unterstützung nach "Zugriff verweigert" in Windows Server 2012 trägt zu dynamischen Access Control bei, indem Benutzern der Zugriff auf freigegebene Dateien und Ordner direkt über die Meldung "Zugriff verweigert" gewährt wird.  
  
## <a name="features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Funktion|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[File Server Resource Manager Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11))|Die Unterstützung nach „Zugriff verweigert“ kann mithilfe der Konsole für den Ressourcen-Manager für Dateiserver auf dem Dateiserver konfiguriert werden.|  
|[Datei- und Speicherdienste: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))|Der Ressourcen-Manager für Dateiserver ist ein Datei- und Speicherdienst-Rollendienst und besteht aus einem Satz an Features, die zum Verwalten der Dateiserver in Ihrem Netzwerk verwendet werden können.|  
  
