---
ms.assetid: ceb9ce18-5a94-4166-9edd-2685b81fc15f
title: Bereitstellen von Ansprüchen über Gesamtstrukturen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 99af1022870c891c75bb2008f57e8d8e171961ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861233"
---
# <a name="deploy-claims-across-forests"></a>Bereitstellen von Ansprüchen über Gesamtstrukturen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server 2012 ist ein Anspruchstyp eine Aussage über das Objekt, dem es zugeordnet ist. Anspruchstypen werden pro Gesamtstruktur in Active Directory definiert. Es gibt viele Szenarien, in denen ein Sicherheitsprinzipal für den Zugriff auf Ressourcen in einer vertrauenswürdigen Gesamtstruktur eine Vertrauensstellungsgrenze durchlaufen muss. Die Gesamtstruktur übergreifende Anspruchs Transformation in Windows Server 2012 ermöglicht es Ihnen, ausgehende und eingehende Ansprüche zu transformieren, die Gesamtstrukturen durchlaufen, damit die Ansprüche in den vertrauenden und vertrauenswürdigen Gesamtstrukturen erkannt und akzeptiert werden. Es folgen einige praktische Szenarien für die Transformation von Ansprüchen:  
  
-   Vertrauende Gesamtstrukturen können die Transformation von Ansprüchen als Schutz gegen die Erhöhung von Berechtigungen nutzen, indem die eingehenden Ansprüche mit bestimmten Werten gefiltert werden.  
  
    Vertrauende Gesamtstrukturen können auch Ansprüche für Prinzipale ausstellen, die eine Vertrauensgrenze überqueren, wenn die vertrauenswürdige Gesamtstruktur Ansprüche nicht unterstützt oder ausstellt.  
  
-   Vertrauenswürdige Gesamtstrukturen können die Transformation von Ansprüchen nutzen, um zu verhindern, dass bestimmte Anspruchstypen und Ansprüche mit bestimmten Werten in die vertrauende Gesamtstruktur gelangen.  
  
-   Sie können die Transformation von Ansprüchen auch zum Zuordnen verschiedener Anspruchstypen zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen verwenden. Dies kann zum Verallgemeinern des Anspruchstyps, des Anspruchswerts oder von beidem dienen. Ohne diesen Schritt müssen Sie die Daten zwischen den Gesamtstrukturen standardisieren, bevor Sie die Ansprüche verwenden können. Durch das Verallgemeinern von Ansprüchen zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen werden die IT-Kosten reduziert.  
  
## <a name="claim-transformation-rules"></a>Regeln für die Transformation von Ansprüchen  
Die Syntax der Transformationsregelsprache unterteilt eine einzelne Regel in zwei Hauptkomponenten: in eine Folge von Bedingungsanweisungen und eine Ausstellungsanweisung. Jede Bedingungsanweisung hat zwei Unterkomponenten: Anspruchs-ID und Bedingung. Die Ausstellungsanweisung enthält Schlüsselwörter, Trennzeichen und einen Ausstellungsausdruck. Die Bedingungsanweisung beginnt optional mit einer Anspruchs-ID-Variablen, die den übereinstimmenden Eingabeanspruch darstellt. Der Ausdruck überprüft die Bedingung. Wenn der Eingabeanspruch nicht mit der Bedingung übereinstimmt, ignoriert das Transformationsmodul die Ausstellungsanweisung und gleicht den nächsten Eingabeanspruch mit der Transformationsregel ab. Wenn alle Bedingungen mit dem Eingabeanspruch übereinstimmen, wird die Ausstellungsanweisung verarbeitet.  
  
Ausführliche Informationen zur Anspruchsregelsprache finden Sie unter [Claims Transformation Rules Language](Claims-Transformation-Rules-Language.md).  
  
## <a name="linking-claim-transformation-policies-to-forests"></a>Verknüpfen von Anspruchstransformationsrichtlinien mit Gesamtstrukturen  
An der Einrichtung von Anspruchstransformationrichtslinien sind zwei Komponenten beteiligt: Richtlinienobjekte für die Anspruchstransformation und die Transformationsverknüpfung. Die Richtlinienobjekte befinden sich im Konfigurationsnamenskontext in einer Gesamtstruktur und enthalten Zuordnungsinformationen für die Ansprüche. Die Verknüpfung gibt an, für welche vertrauenden und vertrauenswürdigen Gesamtstrukturen die Zuordnung gilt.  
  
Es ist wichtig zu verstehen, ob die Gesamtstruktur die vertrauende oder vertrauenswürdige Gesamtstruktur ist, da dies die Basis für das Verknüpfen von Richtlinienobjekten für die Transformation ist. Beispielsweise ist die vertrauenswürdige Gesamtstruktur die Gesamtstruktur, die Benutzerkonten enthält, die Zugriff benötigen. Die vertrauende Gesamtstruktur ist die Gesamtstruktur, die Ressourcen enthält, auf die Benutzer Zugriff erhalten sollen. Ansprüche werden in die gleiche Richtung wie der Sicherheitsprinzipal übertragen, der Zugriff benötigt. Bei beispielsweise einer unidirektionalen Vertrauensstellung der Gesamtstruktur "contoso.com" mit der Gesamtstruktur "adatum.com" werden die Ansprüche von "adatum.com" zu "contoso.com" übertragen, was Benutzern in "adatum.com" den Zugriff auf Ressourcen in "contoso.com" ermöglicht.  
  
In der Standardeinstellung erlaubt eine vertrauenswürdige Gesamtstruktur allen ausgehenden Ansprüchen die Weiterleitung, und eine vertrauende Gesamtstruktur löscht alle eingehenden Ansprüche, die sie erhält.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Für dieses Szenario gilt folgende Leitlinie:  
  
-   [Stellen Sie Anspruchs übergreifende &#40;Demonstrations Schritte bereit&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)  
  
-   [Sprache zum Schreiben von Regeln für die Transformation von Ansprüchen](Claims-Transformation-Rules-Language.md)  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
In der folgenden Tabelle sind die Rollen und Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste|In diesem Szenario müssen Sie zwei Active Directory-Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung einrichten. Sie haben Ansprüche in beiden Gesamtstrukturen. Sie legen außerdem die zentralen Zugriffsrichtlinien für die vertrauende Gesamtstruktur fest, in der sich die Ressourcen befinden.|  
|Datei- und Speicherdienste (Rolle)|Bei diesem Szenario wird die Datenklassifizierung auf die Ressourcen auf den Dateiservern angewendet. Die zentrale Zugriffsrichtlinie gilt für den Ordner, auf den Benutzerzugriff gewährt werden soll. Nach der Transformation gewährt der Anspruch Benutzerzugriff auf Ressourcen basierend auf einer zentralen Zugriffsrichtlinie, die für den Ordner auf dem Dateiserver gilt.|  
  


