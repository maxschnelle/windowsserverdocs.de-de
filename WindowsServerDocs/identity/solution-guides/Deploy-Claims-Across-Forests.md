---
ms.assetid: ceb9ce18-5a94-4166-9edd-2685b81fc15f
title: "Bereitstellen von Ansprüchen über Gesamtstrukturen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7d78258d8f1db9889b6d2db8c497780940ed35a1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-claims-across-forests"></a>Bereitstellen von Ansprüchen über Gesamtstrukturen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In Windows Server2012 ist ein Anspruchstyp eine Aussage zum Objekt, mit dem sie verknüpft ist. Anspruchstypen werden pro Gesamtstruktur in Active Directory definiert. Es gibt viele Szenarien, in denen ein Sicherheitsprinzipal für den Zugriff auf Ressourcen in einer vertrauenswürdigen Gesamtstruktur eine vertrauensstellungsgrenze durchlaufen muss. Gesamtstrukturübergreifende Anspruchstransformation in Windows Server2012 können Sie ein- und ausgehender Ansprüche zu transformieren, die Gesamtstrukturen, damit durchlaufen die Ansprüche werden erkannt und in den vertrauenden und vertrauenswürdigen Gesamtstrukturen akzeptiert. Einige praktische Szenarien für die Transformation von Ansprüchen sind:  
  
-   Vertrauende Gesamtstrukturen kann Transformation von Ansprüchen als Schutz gegen die Erhöhung von Berechtigungen verwenden, indem die eingehenden Ansprüche mit bestimmten Werten filtern.  
  
    Vertrauende Gesamtstrukturen kann auch Ansprüche für Prinzipale eine Vertrauensgrenze überqueren, wenn die vertrauenswürdige Gesamtstruktur nicht unterstützt oder Ansprüche ausstellen ausstellen.  
  
-   Vertrauenswürdige Gesamtstrukturen können Transformation von Ansprüchen verwenden, um zu verhindern, dass bestimmte Anspruchstypen und Ansprüche mit bestimmten Werten für die vertrauende Gesamtstruktur gelangen.  
  
-   Sie können auch Ansprüche Transformation zum Zuordnen verschiedener Anspruchstypen zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen verwenden. Dies kann verwendet werden, um den Anspruchstyp, den Anspruchswert oder beides generalisieren. Ohne diesen Schrittmüssen Sie standardisieren Sie die Daten zwischen den Gesamtstrukturen, bevor Sie die Ansprüche verwenden können. Verallgemeinern von Ansprüchen zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen werden die IT-Kosten reduziert.  
  
## <a name="claim-transformation-rules"></a>Transformation von Anspruchsregeln  
Die Syntax der Transformation unterteilt eine einzelne Regel in zwei Hauptkomponenten: eine Reihe von bedingungsanweisungen und eine ausstellungsanweisung. Jede bedingungsanweisung hat zwei Unterkomponenten: Anspruchs-ID und die Bedingung. Die ausstellungsanweisung enthält Schlüsselwörter, Trennzeichen und einen ausstellungsausdruck. Die bedingungsanweisung beginnt optional mit einer Anspruchs-ID-Variablen, die den übereinstimmenden Eingabeanspruch darstellt. Der Ausdruck überprüft die Bedingung. Wenn der Eingabeanspruch nicht mit der Bedingung übereinstimmt, kann das Transformationsmodul die "Issue"-Anweisung ignoriert und wertet den nächsten Eingabeanspruch mit der Transformation Regel. Wenn alle Bedingungen der Eingabeanspruch übereinstimmen, wird die ausstellungsanweisung verarbeitet.  
  
Ausführliche Informationen zur anspruchsregelsprache finden Sie unter [Ansprüche Transformation Regeln Sprache](Claims-Transformation-Rules-Language.md).  
  
## <a name="linking-claim-transformation-policies-to-forests"></a>Verknüpfen von anspruchstransformationsrichtlinien mit Gesamtstrukturen  
Bei der Einrichtung von anspruchstransformationrichtslinien sind zwei Komponenten: Anspruchsregel Richtlinienobjekten und die transformationsverknüpfung. Die Richtlinienobjekte befinden sich im Konfigurationsnamenskontext in einer Gesamtstruktur und enthalten Zuordnungsinformationen für die Ansprüche. Die Verknüpfung gibt an, welche vertrauenden und vertrauenswürdigen Gesamtstrukturen die Zuordnung gilt.  
  
Es ist wichtig zu verstehen, wenn die Gesamtstruktur die vertrauende oder vertrauenswürdige Gesamtstruktur ist, da dies die Grundlage für das Verknüpfen von Richtlinienobjekten ist. Beispielsweise ist die vertrauenswürdige Gesamtstruktur die Gesamtstruktur, die die Benutzerkonten enthält, die Zugriff benötigen. Die vertrauende Gesamtstruktur ist die Gesamtstruktur, die Ressourcen enthält, denen Benutzerzugriff erhalten sollen. Ansprüche Reise in die gleiche Richtung wie der Sicherheitsprinzipal, der Zugriff benötigt. Beispielsweise ist eine unidirektionale Vertrauensstellung aus der Gesamtstruktur contoso.com adatum.com-Gesamtstruktur, fließt die Ansprüche von adatum.com contoso.com, in dem Benutzer Zugriff auf Ressourcen in contoso.com adatum.com können.  
  
In der Standardeinstellung erlaubt eine vertrauenswürdige Gesamtstruktur allen ausgehende Ansprüchen die Weiterleitung, und eine vertrauende Gesamtstruktur löscht alle eingehenden Ansprüche, die es empfängt.  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Die folgende Anleitung ist für dieses Szenario verfügbar:  
  
-   [Bereitstellen von Ansprüchen über Gesamtstrukturen & 40; Schrittezur Veranschaulichung & 41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)  
  
-   [Ansprüche Transformation Regeln Sprache](Claims-Transformation-Rules-Language.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die Rollen und Features, die in diesem Szenario sind und wird beschrieben, wie sie unterstützen.  
  
|Rollen- und Feature|Wie sie dieses Szenario unterstützt|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste|In diesem Szenario müssen Sie zwei Active Directory-Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung einrichten. Sie haben Ansprüche in beiden Gesamtstrukturen. Zentrale Zugriffsrichtlinien stellen Sie auch auf die vertrauende Gesamtstruktur, in dem sich die Ressourcen befinden.|  
|Datei- und Speicherdienste-Rolle|In diesem Szenario wird die Klassifizierung von Daten auf die Ressourcen auf den Dateiservern angewendet. Die zentrale Zugriffsrichtlinie gilt, zu dem Ordner, in denen Sie Zugriff gewähren möchten. Nach der Transformation gewährt der Anspruch Benutzerzugriff auf Ressourcen auf Grundlage der zentralen Zugriffsrichtlinie, die auf den Ordner auf dem Dateiserver angewendet wird.|  
  


