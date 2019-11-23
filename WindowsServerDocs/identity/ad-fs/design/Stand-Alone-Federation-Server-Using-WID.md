---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: Eigenständiger Verbundserver mit WID
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5fa89a4a57c618fd711234b8770a35750f3099bd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358964"
---
# <a name="stand-alone-federation-server-using-wid"></a>Eigenständiger Verbundserver mit WID

Ein eigenständiger\-Verbund Server in Active Directory-Verbunddienste (AD FS) \(AD FS\) besteht aus einem einzelnen Server, der einen Verbunddienst hostet, der für die Verwendung der internen Windows-Datenbank \(wid\)konfiguriert ist. Diese AD FS Topologie ist für Testumgebungen vorgesehen. Dies wird für Produktionsumgebungen nicht empfohlen, da es nur einen Verbund Server beschränkt und nicht zum zentralen hochskalieren auf weitere Server verwendet werden kann.  
  
Wenn Sie der Testumgebung weitere Verbund Server hinzufügen möchten, müssen Sie die Verbunddienst von Grund auf neu erstellen, indem Sie alle anderen Topologien bereitstellen, die weiter unten in diesem Abschnitt erwähnt werden. Aus diesem Grund wird empfohlen, diese Topologie für eine Testumgebung oder einen Nachweis\-\-Konzept Umgebung in Ihrem privaten Test Netzwerk zu verwenden, in dem ein einzelner Verbund Server angemessen ist, wie in der folgenden Abbildung dargestellt.  
  
![Server mit wid](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>Überlegungen zu Test Labors  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Topologie für Testumgebungen verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Informationstechnologie \(IT\) Spezialisten oder IT-Architekten, die einen Proof of Concept für diese Technologie evaluieren oder entwickeln möchten  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Einfache Einrichtung in einer Testumgebung  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Nur ein Verbund Server pro Verbunddienst \(keine Möglichkeit zum zentralen hochskalieren auf eine Farm\)  
  
-   Nicht redundant \(nur eine einzige Instanz der AD FS Konfigurations Datenbank vorhanden ist\)  
  

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
