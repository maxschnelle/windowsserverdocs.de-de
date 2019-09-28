---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: Unterstützung für szenariozugriff verweigert
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d3c1354c54cf421e59d6b37a44ce703f52b6f4b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357481"
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
  
-   Der Benutzer versucht, eine Datei im freigegebenen Ordner "\\ \ financeshares" zu lesen, der Server zeigt aber die Meldung "Zugriff verweigert" an.  
  
-    Windows Server 2012 zeigt dem Benutzer die Informationen Unterstützung nach "Zugriff verweigert" mit einer Option zum Anfordern von Unterstützung an.  
  
-   Wenn der Benutzer Zugriff auf die Ressource anfordert, sendet der Server eine E-Mail mit den Zugriffsanforderungsinformationen an den Ordnerbesitzer.  
  
Planungsinformationen für das Konfigurieren der Unterstützung nach „Zugriff verweigert“ finden Sie unter [Plan for Access-Denied Assistance](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1).  
  
Schritte zum Konfigurieren der Unterstützung nach "Zugriff verweigert" finden Sie unter Bereitstellen von [ &#40;Hilfe&#41;Demonstrations Schritten "Zugriff verweigert](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)".  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
Die Unterstützung nach "Zugriff verweigert" in Windows Server 2012 trägt zu dynamischen Access Control bei, indem Benutzern der Zugriff auf freigegebene Dateien und Ordner direkt über die Meldung "Zugriff verweigert" gewährt wird.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[Übersicht über Datei Server Ressourcen-Manager](https://technet.microsoft.com/library/hh831701.aspx)|Die Unterstützung nach „Zugriff verweigert“ kann mithilfe der Konsole für den Ressourcen-Manager für Dateiserver auf dem Dateiserver konfiguriert werden.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|Der Ressourcen-Manager für Dateiserver ist ein Datei- und Speicherdienst-Rollendienst und besteht aus einem Satz an Features, die zum Verwalten der Dateiserver in Ihrem Netzwerk verwendet werden können.|  
  


