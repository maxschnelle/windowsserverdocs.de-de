---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: "Eigenständiger Verbundserver mit WID"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9ec4150a7d3adfaac786219d253e1d0898c18204
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="stand-alone-federation-server-using-wid"></a>Eigenständiger Verbundserver mit WID

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Eigenständige Verbundserver in Active Directory Federation Services \(AD FS\) besteht aus einem einzelnen Server, den Hosts einen Verbunddienst so konfiguriert, dass die interne Windows-Datenbank \(WID\) verwenden. Diese AD FS-Topologie wird für Testlabors. Nicht empfohlen er für Produktionsumgebungen, da es ein Limit von nur einem Verbundserver hat und nicht für die Skalierung auf mehrere Server verwendet werden.  
  
Wenn Sie das Testlabor Weitere Verbundserver hinzufügen möchten, müssen Sie den Verbunddienst von Grund auf neu erstellen, durch die Bereitstellung von allen anderen in diesem Abschnittgenannten Topologien. Aus diesem Grund empfehlen wir Sie dieser Topologie für ein Testlabor oder einer Proof\-Of\-Konzept-Umgebung in Ihrem privaten testen Netzwerk verwenden, in dem ein einzelnen Verbundservers ausreichend, ist wie in der folgenden Abbildungdargestellt.  
  
![Server mit WID](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>Test Lab-Überlegungen  
Dieser Abschnittbeschreibt die verschiedenen Aspekte über die Zielgruppe, Vorteile und Einschränkungen, die diese Topologie wird für Testumgebungen zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   IT-Experten \(IT\) oder IT-Architekten, die zu bewerten, oder entwickeln eine Machbarkeitsstudie für diese Technologie  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Einfach in einer Testumgebung einrichten  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Grenzen der Verwendung dieser Topologie?  
  
-   Nur einem Verbundserver pro Verbunddienst \ (keine Möglichkeit, um eine Farm\ skalieren)  
  
-   Nicht redundant \ (nur eine einzelne Instanz der AD FS-Konfiguration Datenbank Exists\)  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
