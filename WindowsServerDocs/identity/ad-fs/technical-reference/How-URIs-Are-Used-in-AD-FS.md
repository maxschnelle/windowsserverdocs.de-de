---
ms.assetid: 53ee93e2-09ea-4f8b-adb7-c24c59f055ea
title: Verwendung von URIs in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 305bf0cece742c961604dacda7e27b8eac8065e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812221"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2

# <a name="how-uris-are-used-in-ad-fs"></a>Verwendung von URIs in AD FS
Ein Uniform Resource Identifier \(URI\) ist eine Zeichenfolge, die als eindeutiger Bezeichner verwendet wird.  In AD FS dienen URIs zum Identifizieren von Netzwerkadressen von Partnern und Konfigurationsobjekten.  Bei Verwendung zum Identifizieren von Netzwerkadressen von Partnern ist der URI stets eine URL.  Bei Verwendung zum Identifizieren von Objekten kann der URI ein URN oder eine URL sein.  Weitere allgemeine Informationen zu URIs finden Sie unter [RFC 2396](https://go.microsoft.com/fwlink/?LinkId=48289) und [RFC 3986](https://go.microsoft.com/fwlink/?LinkId=90453).  
  
## <a name="uris-as-partner-network-addresses"></a>URIs als Netzwerkadressen von Partnern  
Es folgen die Netzwerkadressen-URLs, mit denen es AD FS-Administratoren am häufigsten zu tun haben.  
  
-   Die URLs des Verbunddiensts, wie z. B. WS\-Verbund, SAML, WS\-Trust, Verbundmetadaten, WS\-MetadataExchange, Datenschutz und Unternehmens-URLs  
  
-   Die URLs der Anspruchsanbieter-Vertrauensstellung, wie z. B. WS\-Federation, SAML und Verbundmetadaten-URLs  
  
-   Die URLs von einem Anspruchsanbieter-Vertrauensstellung einschließlich WS\-Federation, SAML und Verbundmetadaten-URLs  
  
## <a name="uris-as-object-identifiers"></a>URIs als Objektbezeichner  
In der folgenden Tabelle werden die Bezeichner beschrieben, mit denen es AD FS-Administratoren am häufigsten zu tun haben.  
  
|Bezeichnername|Beschreibung|Vergleiche|  
|-------------------|---------------|---------------|  
|Bezeichner des Verbunddiensts|Dieser Bezeichner wird verwendet, um den Verbunddienst zu identifizieren.  Die ID wird von vertrauenden Seiten, die Ansprüche von diesem Verbunddienst nutzen, sowie von Anspruchsanbietern verwendet, die Ansprüche für diesen Verbunddienst ausstellen.|Wenn ein Benutzer Ansprüche vom Anspruchsanbieter für diesen Verbunddienst anfordert, wird der Bezeichner des Verbunddiensts genutzt, um das Ziel der Ansprüche zu bestimmen.<br /><br />Wenn dieser Verbunddienst die Ansprüche von einem Anspruchsanbieter empfängt, prüft er dessen Verbunddienstbezeichner, um sicherzustellen, dass die Ansprüche entsprechend begrenzt sind.<br /><br />Wenn eine vertrauende Seite Ansprüche von diesem Verbunddienst empfängt, prüft die vertrauende Seite, ob der Aussteller der Ansprüche mit dem Verbunddienstbezeichner übereinstimmt.|  
|Bezeichner der vertrauenden Seite|Dieser Bezeichner wird verwendet, um die vertrauende Seite für den Verbunddienst zu bestimmen.  Er wird verwendet, wenn Ansprüche für die vertrauende Seite ausgestellt werden.|Wenn ein Benutzer Ansprüche von diesem Verbunddienst für die vertrauende Seite anfordert, wird der Bezeichner der vertrauenden Seite verwendet, um die vertrauende Seite zu identifizieren, der die Ansprüche zugewiesen werden sollen.  Dieser Vergleich erfolgt anhand der präfixübereinstimmung \(siehe unten\).<br /><br />Wenn die vertrauende Seite die Ansprüche erhält, sucht sie ihren Bezeichner im Sicherheitstoken, um sicherzustellen, dass die Ansprüche für sie gelten.|  
|Anspruchsanbieterbezeichner|Dieser Bezeichner wird verwendet, um den Anspruchsanbieter für den Verbunddienst zu bestimmen.  Er wird verwendet, wenn Ansprüche vom Anspruchsanbieter empfangen werden.|Wenn dieser Verbunddienst Ansprüche vom Anspruchsanbieter empfängt, prüft dieser Verbunddienst, ob der Aussteller der Ansprüche mit dem Bezeichner des Anspruchsanbieters übereinstimmt.|  
|Anspruchstyp|Dieser Bezeichner wird verwendet, um den Typ des Anspruchs zu definieren.  Er wird beim Senden und Empfangen von Ansprüchen von diesem Verbunddienst, Anspruchsanbietern und vertrauende Seiten verwendet.|Wenn der Verbunddienst Ansprüche von einem Anspruchsanbieter erhält, ermöglichen die Anspruchsregeln, die der entsprechenden Anspruchsanbieter-Vertrauensstellung zugeordnet sind, dem Administrator das Vergleichen von Anspruchstypen und Verarbeiten von Ansprüchen.  Die Anspruchsregeln, die der Anspruchsanbieter-Vertrauensstellung zugeordnet sind, ermöglichen dem Administrator auch das Vergleichen von Anspruchstypen, die aus Regeln für die Anspruchsanbieter-Vertrauensstellung stammen, und das Entscheiden, welche Ansprüche ausgestellt werden sollen.|  
  
## <a name="uri-prefix-matching-for-relying-party-identifiers"></a>URI-Präfixabgleich für Bezeichner der vertrauenden Seite  
Die Pfadsyntax eines URIs ist hierarchisch aufgebaut ist getrennt, indem Sie entweder alle "\/"Zeichen oder alle":" Zeichen.  Auf Grundlage der Trennzeichen kann der Pfad daher in Abschnitte aufgeteilt sein.  Beim präfixabgleich, muss jeder Abschnitt eine vollständige Übereinstimmung gemäß den abgleichregeln \(diese Regeln bestimmen die Groß-/Kleinschreibung der Übereinstimmungen\). Weitere Informationen zu den Abgleichregeln finden Sie in den oben erwähnten RFCs.  
  
Wenn eine vertrauende Seite in einer Anforderung an den Verbunddienst erkannt wird, verwendet AD FS die Präfixabgleichlogik zum Bestimmen, ob es in der AD FS-Konfigurationsdatenbank eine übereinstimmende Vertrauensstellung der vertrauenden Seite gibt.  
  
Z. B. Wenn Bezeichner der vertrauenden Seite in der AD FS-Konfigurationsdatenbank \(URI1\) ist ein Präfix für den Bezeichner der vertrauenden Seite in der eingehenden Anforderung \(URI2\), und klicken Sie dann die folgenden Bedingungen erfüllt sein müssen:  
  
-   Nachfolgende Trennzeichen \(Schrägstriche und Doppelpunkte\) des Pfads Abschnitte oder stellen müssen ignoriert werden  
  
-   Die Schema- und Autoritätsteile von URI1 und URI2 müssen unabhängig von Groß-und Kleinschreibung genau übereinstimmen.  
  
-   Jeden Pfadabschnitt von URI1 muss eine genaue Übereinstimmung \(basierend auf der gewählten Groß-/Kleinschreibung\) auf dem entsprechenden Pfadabschnitt von URI2  
  
-   URI2 hat möglicherweise mehr Pfadabschnitte als URI1, aber URI1 darf nicht mehr Pfadabschnitte als URI2 haben.  
  
-   URI1 kann nicht mehr Pfadabschnitte als URI2 haben.  
  
-   Wenn URI1 eine Abfragezeichenfolge enthält, muss sie genau einer URI2-Abfragezeichenfolge entsprechen.  
  
-   Wenn URI1 ein Fragment enthält, muss es genau einem URI2-Fragment entsprechen.  
  
Die folgende Tabelle enthält weitere Beispiele.  
  
|Bezeichner der vertrauenden Seite in der AD FS-Konfigurationsdatenbank|Bezeichner der vertrauenden Seite in der Anforderungsnachricht|Entspricht der Anforderungsbezeichner dem Konfigurationsbezeichner?|Grund|  
|------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------|----------|  
|http:\/\/"contoso.com"|http:\/\/"contoso.com"|TRUE|Genaue Übereinstimmung|  
|http:\/\/contoso.com\/|http:\/\/"contoso.com"|TRUE|Nachgestellte Schrägstriche werden ignoriert.|  
|http:\/\/"contoso.com"|http:\/\/contoso.com\/|TRUE|Nachgestellte Schrägstriche werden ignoriert.|  
|http:\/\/"contoso.com"|http:\/\/"contoso.com"\/hr|TRUE|URI1 enthält keinen Pfad und stimmt mit Schema und Autorität in URI2 überein.|  
|http:\/\/"contoso.com"\/hr|http:\/\/"contoso.com"\/hr\/Web|TRUE|Die ersten Pfadabschnitte stimmen überein, URI1 hat keinen zweiten Pfadabschnitt.|  
|http:\/\/"contoso.com"\/hr|http:\/\/contoso.com\/hr\/web\/?m\=t|TRUE|Selbe Gründen wie oben. Die Abfragezeichenfolge ändert nichts.|  
|http:\/\/"contoso.com"\/hr\/|http:\/\/"contoso.com"\/Hrw\/main|FALSE|Der Pfadabschnitt 1 von URI1 entspricht nicht dem Pfadabschnitt 1 von URI2.|  
|http:\/\/"contoso.com"\/hr|http:\/\/"contoso.com"|FALSE|URI1 hat mehr Pfadabschnitte als URI2.|  
|http:\/\/"contoso.com"\/hr|http:\/\/"contoso.com"\/Hrweb|FALSE|Die ersten Pfadabschnitte stimmen nicht überein.|  
|http:\/\/contoso.com\/?m\=t|http:\/\/contoso.com\/?m\=f|FALSE|Teile der Abfragezeichenfolge stimmen nicht überein.|  
|https:\/\/contoso.com|http:\/\/"contoso.com"|FALSE|Teile des Schemas stimmen nicht überein.|  
|http:\/\/sts.contoso.com|http:\/\/"contoso.com"|FALSE|Teile der Autorität stimmen nicht überein.|  
|http:\/\/"contoso.com"|http:\/\/sts.contoso.com|FALSE|Teile der Autorität stimmen nicht überein.|  
  

