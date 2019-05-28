---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: Eigenständiger Verbundserver mit WID
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 31e2e1b04383adc8bec12e7290a7acec80e0402f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190788"
---
# <a name="stand-alone-federation-server-using-wid"></a>Eigenständiger Verbundserver mit WID

Ein eigenständiger\-allein Verbundserver in Active Directory Federation Services \(AD FS\) besteht aus einem einzelnen Server, der einen Verbunddienst für die Verwendung der internen Windows-Datenbank konfiguriert hostet \(WID\). Dieser AD FS-Topologie ist für Test-Labs. Nicht empfohlen es für produktionsumgebungen, da es ein Limit von nur einem Verbundserver hat, und er nicht verwendet werden, um weitere Server zentral hochskalieren.  
  
Wenn Sie das Testlabor Weitere Verbundserver hinzufügen möchten, müssen Sie den Verbunddienst von Grund auf neu erstellen, durch die Bereitstellung von allen anderen Topologien erläuterungen weiter unten in diesem Abschnitt. Daher wird empfohlen, dass die Verwendung dieser Topologie für eine testumgebung oder einer Proof\-von\-Concept-Umgebung in Ihrem privaten testen Netzwerk, in denen ein einzelnen Verbundservers ausreichend, ist wie in der folgenden Abbildung dargestellt.  
  
![Server mit WID](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>Überlegungen zum Test-lab  
Dieser Abschnitt beschreibt verschiedene Überlegungen zu den Zielgruppe, Vorteile und Einschränkungen, die diese Topologie wird für den Test Lab-Umgebungen zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Informationstechnologie \(IT\) -Experten oder IT-Architekten, die zu auszuwertenden oder einen Proof of Concept für diese Technologie entwickeln möchten  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Einfach in eine testumgebung einrichten  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Einschränkungen bei der Verwendung dieser Topologie?  
  
-   Nur einem Verbundserver pro Verbunddienst \(keine Möglichkeit, die auf einer Farm zentral hochskalieren\)  
  
-   Nicht redundante \(nur eine einzige Instanz der AD FS-Konfigurationsdatenbank vorhanden ist.\)  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
