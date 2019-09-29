---
ms.assetid: 53ee93e2-09ea-4f8b-adb7-c24c59f055ea
title: Verwendung von URIs in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2ae91b16448c5acd61712332310544c1fd66789f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385490"
---
# <a name="how-uris-are-used-in-ad-fs"></a>Verwendung von URIs in AD FS
Ein Uniform Resource Identifier \(-\) URI ist eine Zeichenfolge, die als eindeutiger Bezeichner verwendet wird.  In AD FS dienen URIs zum Identifizieren von Netzwerkadressen von Partnern und Konfigurationsobjekten.  Bei Verwendung zum Identifizieren von Netzwerkadressen von Partnern ist der URI stets eine URL.  Bei Verwendung zum Identifizieren von Objekten kann der URI ein URN oder eine URL sein.  Weitere allgemeine Informationen zu URIs finden Sie unter [RFC 2396](https://go.microsoft.com/fwlink/?LinkId=48289) und [RFC 3986](https://go.microsoft.com/fwlink/?LinkId=90453).  
  
## <a name="uris-as-partner-network-addresses"></a>URIs als Netzwerkadressen von Partnern  
Es folgen die Netzwerkadressen-URLs, mit denen es AD FS-Administratoren am häufigsten zu tun haben.  
  
-   Die URLs der Verbunddienst, einschließlich WS\--Verbund, SAML, WS\-Trust, Verbund Metadaten, WS\-MetadataExchange, Datenschutz und Organisations-URLs  
  
-   Die URLs einer Vertrauensstellung der vertrauenden Seite,\-einschließlich WS-Verbund-, SAML-und Verbund Metadaten-URLs  
  
-   Die URLs einer Anspruchs Anbieter-Vertrauensstellung, einschließlich\-WS-Verbund-, SAML-und Verbund Metadaten-URLs  
  
## <a name="uris-as-object-identifiers"></a>URIs als Objektbezeichner  
In der folgenden Tabelle werden die Bezeichner beschrieben, mit denen es AD FS-Administratoren am häufigsten zu tun haben.  
  
|Bezeichnername|Beschreibung|Vergleiche|  
|-------------------|---------------|---------------|  
|Bezeichner des Verbunddiensts|Dieser Bezeichner wird verwendet, um den Verbunddienst zu identifizieren.  Die ID wird von vertrauenden Seiten, die Ansprüche von diesem Verbunddienst nutzen, sowie von Anspruchsanbietern verwendet, die Ansprüche für diesen Verbunddienst ausstellen.|Wenn ein Benutzer Ansprüche vom Anspruchsanbieter für diesen Verbunddienst anfordert, wird der Bezeichner des Verbunddiensts genutzt, um das Ziel der Ansprüche zu bestimmen.<br /><br />Wenn dieser Verbunddienst die Ansprüche von einem Anspruchsanbieter empfängt, prüft er dessen Verbunddienstbezeichner, um sicherzustellen, dass die Ansprüche entsprechend begrenzt sind.<br /><br />Wenn eine vertrauende Seite Ansprüche von diesem Verbunddienst empfängt, prüft die vertrauende Seite, ob der Aussteller der Ansprüche mit dem Verbunddienstbezeichner übereinstimmt.|  
|Bezeichner der vertrauenden Seite|Dieser Bezeichner wird verwendet, um die vertrauende Seite für den Verbunddienst zu bestimmen.  Er wird verwendet, wenn Ansprüche für die vertrauende Seite ausgestellt werden.|Wenn ein Benutzer Ansprüche von diesem Verbunddienst für die vertrauende Seite anfordert, wird der Bezeichner der vertrauenden Seite verwendet, um die vertrauende Seite zu identifizieren, der die Ansprüche zugewiesen werden sollen.  Dieser Vergleich erfolgt mithilfe eines Präfix \(Vergleichs.\)siehe unten.<br /><br />Wenn die vertrauende Seite die Ansprüche erhält, sucht sie ihren Bezeichner im Sicherheitstoken, um sicherzustellen, dass die Ansprüche für sie gelten.|  
|Anspruchsanbieterbezeichner|Dieser Bezeichner wird verwendet, um den Anspruchsanbieter für den Verbunddienst zu bestimmen.  Er wird verwendet, wenn Ansprüche vom Anspruchsanbieter empfangen werden.|Wenn dieser Verbunddienst Ansprüche vom Anspruchsanbieter empfängt, prüft dieser Verbunddienst, ob der Aussteller der Ansprüche mit dem Bezeichner des Anspruchsanbieters übereinstimmt.|  
|Anspruchstyp|Dieser Bezeichner wird verwendet, um den Typ des Anspruchs zu definieren.  Er wird beim Senden und Empfangen von Ansprüchen von diesem Verbunddienst, Anspruchsanbietern und vertrauende Seiten verwendet.|Wenn der Verbunddienst Ansprüche von einem Anspruchsanbieter erhält, ermöglichen die Anspruchsregeln, die der entsprechenden Anspruchsanbieter-Vertrauensstellung zugeordnet sind, dem Administrator das Vergleichen von Anspruchstypen und Verarbeiten von Ansprüchen.  Die Anspruchsregeln, die der Anspruchsanbieter-Vertrauensstellung zugeordnet sind, ermöglichen dem Administrator auch das Vergleichen von Anspruchstypen, die aus Regeln für die Anspruchsanbieter-Vertrauensstellung stammen, und das Entscheiden, welche Ansprüche ausgestellt werden sollen.|  
  
## <a name="uri-prefix-matching-for-relying-party-identifiers"></a>URI-Präfixabgleich für Bezeichner der vertrauenden Seite  
Die Pfad Syntax eines URIs ist hierarchisch organisiert und wird entweder durch alle "\/"-Zeichen oder alle ":"-Zeichen getrennt.  Auf Grundlage der Trennzeichen kann der Pfad daher in Abschnitte aufgeteilt sein.  Beim Präfix Abgleich muss jeder Abschnitt eine vollständige Übereinstimmung gemäß den abgleichsregeln \(aufweisen. diese Regeln bestimmen die Schreibweise von Übereinstimmungen.\) Weitere Informationen zu abgleichsregeln finden Sie in den oben erwähnten RFC.  
  
Wenn eine vertrauende Seite in einer Anforderung an den Verbunddienst erkannt wird, verwendet AD FS die Präfixabgleichlogik zum Bestimmen, ob es in der AD FS-Konfigurationsdatenbank eine übereinstimmende Vertrauensstellung der vertrauenden Seite gibt.  
  
Wenn beispielsweise der Bezeichner der vertrauenden Seite in der AD FS \(-\) Konfigurations Datenbank URI1 ein Präfix des Bezeichners der vertrauenden \(Seite\)in der eingehenden Anforderung URI2 ist, muss Folgendes zutreffen:  
  
-   Nachfolgende Trenn \(Zeichen, Schrägstriche und\) Doppelpunkte von Pfad Abschnitten oder Autoritäten müssen ignoriert werden.  
  
-   Die Schema- und Autoritätsteile von URI1 und URI2 müssen unabhängig von Groß-und Kleinschreibung genau übereinstimmen.  
  
-   Jeder Pfad Abschnitt von URI1 muss eine genaue Übereinstimmung \(auf der Grundlage der groß-\) /Kleinschreibung aufweisen, die für den entsprechenden Pfad Abschnitt von URI2 gewählt wurde.  
  
-   URI2 hat möglicherweise mehr Pfadabschnitte als URI1, aber URI1 darf nicht mehr Pfadabschnitte als URI2 haben.  
  
-   URI1 kann nicht mehr Pfadabschnitte als URI2 haben.  
  
-   Wenn URI1 eine Abfragezeichenfolge enthält, muss sie genau einer URI2-Abfragezeichenfolge entsprechen.  
  
-   Wenn URI1 ein Fragment enthält, muss es genau einem URI2-Fragment entsprechen.  
  
Die folgende Tabelle enthält weitere Beispiele.  
  
|Bezeichner der vertrauenden Seite in der AD FS-Konfigurationsdatenbank|Bezeichner der vertrauenden Seite in der Anforderungsnachricht|Entspricht der Anforderungsbezeichner dem Konfigurationsbezeichner?|Grund|  
|------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------|----------|  
|http:\/\/contoso.com|http:\/\/contoso.com|TRUE|Genaue Übereinstimmung|  
|http:\/\/contoso.com\/|http:\/\/contoso.com|TRUE|Nachgestellte Schrägstriche werden ignoriert.|  
|http:\/\/contoso.com|http:\/\/contoso.com\/|TRUE|Nachgestellte Schrägstriche werden ignoriert.|  
|http:\/\/contoso.com|http:\/\/contoso.comHR\/|TRUE|URI1 enthält keinen Pfad und stimmt mit Schema und Autorität in URI2 überein.|  
|http:\/\/contoso.comHR\/|http:\/\/contoso.comHR\/Web\/|TRUE|Die ersten Pfadabschnitte stimmen überein, URI1 hat keinen zweiten Pfadabschnitt.|  
|http:\/\/contoso.comHR\/|http:\/\/contoso.comHR\/Web\/?m\=t\/|TRUE|Dieselben Gründe wie oben, die Abfrage Zeichenfolge ändert nichts.|  
|http:\/\/contoso.comHR\/\/|http:\/\/contoso.com\/HRW\/Main|FALSE|Der Pfadabschnitt 1 von URI1 entspricht nicht dem Pfadabschnitt 1 von URI2.|  
|http:\/\/contoso.comHR\/|http:\/\/contoso.com|FALSE|URI1 hat mehr Pfadabschnitte als URI2.|  
|http:\/\/contoso.comHR\/|http:\/\/contoso.com\/HRweb|FALSE|Die ersten Pfadabschnitte stimmen nicht überein.|  
|http:\/\/contoso.com?\/mt\=|http:\/\/contoso.com?\/mf\=|FALSE|Teile der Abfragezeichenfolge stimmen nicht überein.|  
|https:\/\/contoso.com|http:\/\/contoso.com|FALSE|Teile des Schemas stimmen nicht überein.|  
|http:\/\/STS.contoso.com|http:\/\/contoso.com|FALSE|Teile der Autorität stimmen nicht überein.|  
|http:\/\/contoso.com|http:\/\/STS.contoso.com|FALSE|Teile der Autorität stimmen nicht überein.|  
  

