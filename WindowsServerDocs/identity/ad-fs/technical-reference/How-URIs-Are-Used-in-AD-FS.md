---
ms.assetid: 53ee93e2-09ea-4f8b-adb7-c24c59f055ea
title: Wie werden die URIs in AD FS verwendet
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 305bf0cece742c961604dacda7e27b8eac8065e5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server 2016, Windows Server2012 R2

# <a name="how-uris-are-used-in-ad-fs"></a>Wie werden die URIs in AD FS verwendet
Ein Uniform Resource Identifier \(URI\) ist eine Zeichenfolge, die als eindeutiger Bezeichner verwendet wird.  In AD FS URIs zum Identifizieren von Netzwerkadressen von Partnern und Konfigurationsobjekten verwendet.  Bei Verwendung zum Identifizieren von Netzwerkadressen von Partnern ist der URI stets eine URL.  Wenn zum Identifizieren von Objekten verwendet, kann der URI ein URN oder eine URL sein.  Weitere allgemeine Informationen zu URIs finden Sie unter [RFC 2396](https://go.microsoft.com/fwlink/?LinkId=48289) und [RFC 3986](https://go.microsoft.com/fwlink/?LinkId=90453).  
  
## <a name="uris-as-partner-network-addresses"></a>URIs als Netzwerkadressen von Partnern  
Es folgen die Netzwerkadressen-URLs, die am häufigsten von Administratoren in AD FS behandelt werden.  
  
-   Die URLs des Verbunddiensts, einschließlich WS-Federation, SAML, WS-Trust, Verbundmetadaten, ws-MetadataExchange, Datenschutz und Unternehmens-URLs  
  
-   Die URLs der eine Vertrauensstellung für vertrauende Seiten, einschließlich WS-Federation, SAML und Verbundmetadaten-URLs  
  
-   Die URLs der von einem Anspruchsanbieter-Vertrauensstellung einschließlich WS-Federation, SAML und Verbundmetadaten-URLs  
  
## <a name="uris-as-object-identifiers"></a>URIs als Objektbezeichner  
Die folgende Tabelle beschreibt die Bezeichner, die am häufigsten von Administratoren in AD FS behandelt werden.  
  
|Bezeichnername|Beschreibung|Vergleiche|  
|-------------------|---------------|---------------|  
|Bezeichner des Verbunddiensts|Dieser Bezeichner wird verwendet, um den Verbunddienst zu identifizieren.  Es wird von vertrauenden Seiten verwendet, die Ansprüche von diesem Verbunddienst als auch Anspruchsanbietern Problem für den Verbunddienst Ansprüche verwenden.|Wenn ein Benutzer Ansprüche von einem Anspruchsanbieter für diesen Verbunddienst anfordert, wird Bezeichner des Verbunddiensts verwendet werden, um das Ziel der Ansprüche zu identifizieren.<br /><br />Wenn dieser Verbunddienst die Ansprüche von einem Anspruchsanbieter empfängt, prüft er um sicherzustellen, dass die Ansprüche entsprechend begrenzt sind anhand dessen verbunddienstbezeichner.<br /><br />Wenn eine vertrauende Seite Ansprüche von diesem Verbunddienst empfängt, prüft die vertrauende Seite, ob der Aussteller der Ansprüche Bezeichner des Verbunddiensts übereinstimmt.|  
|Bezeichner der vertrauenden Seite|Dieser Bezeichner wird verwendet, um die vertrauende Seite für den Verbunddienst zu identifizieren.  Er wird beim Ausstellen von Ansprüchen auf die vertrauende Seite verwendet.|Wenn ein Benutzer Ansprüche von diesem Verbunddienst für die vertrauende Seite anfordert, wird Bezeichner der vertrauenden Seite verwendet werden, um die vertrauende Seite zu identifizieren, für die die Ansprüche zugewiesen werden sollen.  Dieser Vergleich erfolgt mithilfe von übereinstimmenden \(see below\) Präfix.<br /><br />Wenn die vertrauende Seite die Ansprüche erhält, sucht sie ihren Bezeichner im Sicherheitstoken, um sicherzustellen, dass die Ansprüche für sie gelten.|  
|Anspruchsanbieterbezeichner|Dieser Bezeichner wird verwendet, um den Anspruchsanbieter für diesen Verbunddienst zu identifizieren.  Es wird verwendet, wenn Ansprüche vom Anspruchsanbieter empfängt.|Wenn dieser Verbunddienst Ansprüche vom Anspruchsanbieter empfängt, prüft dieser Verbunddienst, ob der Aussteller der Ansprüche Bezeichner des Anspruchsanbieters übereinstimmt.|  
|Typ des Anspruchs|Dieser Bezeichner wird verwendet, um den Typ des Anspruchs zu definieren.  Es wird von diesem Verbunddienst, Anspruchsanbietern und vertrauende Seiten beim Senden und Empfangen von Ansprüchen verwendet.|Wenn der Verbunddienst Ansprüche von einem Anspruchsanbieter erhält, ermöglichen die Anspruchsregeln, die den entsprechenden Anspruchsanbieter-Vertrauensstellung zugeordnet den Administrator zum Vergleichen von Anspruchstypen und Verarbeiten von Ansprüchen.  Die Anspruchsregeln, die eine Vertrauensstellung der vertrauenden Seite zugeordnet auch können der Administrator zum Vergleichen von Anspruchstypen von den Anspruchsregeln für Anbieter Vertrauensstellung stammen, und entscheiden, welche Ansprüche auszugeben.|  
  
## <a name="uri-prefix-matching-for-relying-party-identifiers"></a>URI-präfixabgleich für Bezeichner der vertrauenden Seite  
Die Pfadsyntax eines URIs ist hierarchisch aufgebaut und getrennt durch alle "\ /"Zeichen oder alle":" Zeichen.  Daher kann der Pfad in basierend auf der Trennzeichen Abschnitte aufgeteilt werden.  Beim präfixabgleich, muss jeder Abschnitt eine vollständige Übereinstimmung gemäß den Übereinstimmungsregeln \ (diese Regeln bestimmen die Groß-/Kleinschreibung der Matches\). Weitere Informationen zur Suche von Regeln finden Sie unter des RFCs genannten.  
  
Wenn eine vertrauende Seite in einer Anforderung an den Verbunddienst erkannt wird, verwendet AD FS die präfixabgleichlogik um zu bestimmen, ob eine übereinstimmende Vertrauensstellung in der AD FS-Konfigurationsdatenbank.  
  
Beispielsweise ist der Bezeichner der vertrauenden Seite in der AD FS-Konfigurationsdatenbank \(URI1\) ein Präfix für Bezeichner der vertrauenden Seite in der eingehenden anfordern \(URI2\), und klicken Sie dann die folgenden Bedingungen erfüllt sein müssen:  
  
-   Nachfolgende Trennzeichen \(slashes and colons\) des Pfads Abschnitte oder stellen müssen ignoriert werden  
  
-   Die und autoritätsteile von URI1 und URI2 müssen eine Groß-/Kleinschreibung exakt sein.  
  
-   Jeden Pfadabschnitt von URI1 muss eine genaue Übereinstimmung \ (basierend auf der Groß-/Kleinschreibung Chosen\) auf dem entsprechenden Pfadabschnitt von uri2.  
  
-   Uri2 hat möglicherweise mehr pfadabschnitte als URI1 muss, aber URI1 nicht mehr pfadabschnitte als uri2 haben.  
  
-   URI1 kann nicht mehr pfadabschnitte als URI2 haben.  
  
-   Wenn URI1 eine Abfragezeichenfolge enthält, muss es genau einem URI2-Abfragezeichenfolge entsprechen.  
  
-   Wenn URI1 ein Fragment enthält, muss es genau einem URI2-Fragment entsprechen.  
  
Die folgende Tabelle enthält weitere Beispiele.  
  
|Vertrauensstellungen der vertrauenden Seite Bezeichner in AD FS-Konfigurationsdatenbank|Vertrauensstellungen der vertrauenden Seite Bezeichner in der Anforderungsnachricht|Anforderungsbezeichner entspricht der dem Konfigurationsbezeichner?|Grund|  
|------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------|----------|  
|http:///\/contoso.com|http:///\/contoso.com|"TRUE"|Genaue Übereinstimmung|  
|http:///\/contoso.com\/|http:///\/contoso.com|"TRUE"|Nachgestellte Schrägstriche werden ignoriert.|  
|http:///\/contoso.com|http:///\/contoso.com\/|"TRUE"|Nachgestellte Schrägstriche werden ignoriert.|  
|http:///\/contoso.com|http:///\/contoso.com\/HR|"TRUE"|URI1 enthält keinen Pfad und stimmt mit Schema und Autorität in uri2 überein.|  
|http:///\/contoso.com\/HR|http:///\/contoso.com\/hr\/Web|"TRUE"|Die ersten pfadabschnitte überein, URI1 hat keinen zweiten Pfadabschnitt|  
|http:///\/contoso.com\/HR|http:///\/contoso.com\/hr\/web\/?m\=t|"TRUE"|Selbe Gründen wie oben beschrieben, keine Abfragezeichenfolge ändert nichts|  
|http:///\/contoso.com\/hr\/|http:///\/contoso.com\/hrw\/Main|"FALSE"|URI1 Pfadabschnitt 1 entspricht nicht dem Pfadabschnitt 1 von uri2.|  
|http:///\/contoso.com\/HR|http:///\/contoso.com|"FALSE"|URI1 hat mehr pfadabschnitte als uri2 haben.|  
|http:///\/contoso.com\/HR|http:///\/contoso.com\/hrweb|"FALSE"|Die ersten pfadabschnitte stimmen nicht überein.|  
|http:///\/contoso.com\/?m\=t|http:///\/contoso.com\/?m\=f|"FALSE"|Teile der Abfragezeichenfolge stimmen nicht überein.|  
|https:\/\/contoso.com|http:///\/contoso.com|"FALSE"|Teile des Schemas stimmen nicht überein.|  
|http:///\/STS.contoso.com|http:///\/contoso.com|"FALSE"|Teile der Autorität stimmen nicht überein.|  
|http:///\/contoso.com|http:///\/STS.contoso.com|"FALSE"|Teile der Autorität stimmen nicht überein.|  
  

