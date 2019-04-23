---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: Überprüfen von DNS-Konzepten
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d077ecc30caca9b8f3b382af624121fec729afae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890501"
---
# <a name="reviewing-dns-concepts"></a>Überprüfen von DNS-Konzepten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domain Name System (DNS) ist eine verteilte Datenbank, die einen Namespace darstellt. Der Namespace enthält alle Informationen für jeden Client, um einen beliebigen Namen suchen erforderlich sind. Jeder DNS-Server kann Abfragen über einen beliebigen Namen in seinem Namespace beantworten. Ein DNS-Server werden Abfragen in einem der folgenden Methoden:  
  
- Wenn die Antwort im jeweiligen Cache ist, werden die Abfrage aus dem Cache beantwortet.  
- Wenn die Antwort in einer Zone, die von den DNS-Server gehostet ist, werden die Abfrage aus der Zone beantwortet. Eine Zone ist ein Teil der DNS-Struktur, die auf einem DNS-Server gespeichert. Wenn ein DNS-Server eine Zone hostet, ist es für die Namen in dieser Zone autorisierend (d. h. der DNS-Server kann Antworten Abfragen für einen beliebigen Namen in der Zone). Beispielsweise kann ein Server, der die Zone "contoso.com" hostet, Abfragen für einen beliebigen Namen in "contoso.com" beantworten.  
- Wenn der Server die Abfrage von den Cache oder Zonen nicht beantworten kann, wird der andere Server für die Antwort abgefragt.  

Es ist wichtig zu verstehen, die Kernfunktionen von DNS, wie z. B. die Delegierung, rekursive namensauflösung und Active Directory-integrierte DNS-Zonen, da sie einen direkten Einfluss auf Ihre Active Directory-Entwurf der logischen Struktur aufweisen.  
  
Weitere Informationen zu DNS und Active Directory Domain Services (AD DS) finden Sie unter [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md).  
  
## <a name="delegation"></a>Delegierung

Für einen DNS-Server zur Beantwortung von Abfragen über einen beliebigen Namen müssen sie einen direkten oder indirekten Pfad zu jeder Zone im Namespace. Diese Pfade werden mithilfe der Delegierung erstellt. Eine Delegation ist ein Datensatz in einer übergeordneten Zone, die einen Namenserver auflistet, der für die Zone in der nächsten Ebene der Hierarchie autorisierend ist. Delegierungen können für Server in einer Zone, um Clients auf Servern in anderen Zonen zu verweisen. Die folgende Abbildung zeigt ein Beispiel der Delegierung.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
Der DNS-Stammserver hostet die Stammzone als Punkt dargestellt (. ). Die Stammzone enthält eine Delegierung zu einer Zone in der nächsten Ebene der Hierarchie, die com-Zone. Die Delegierung in der Stammzone weist dem DNS-Stammserver, um die Zone com zu suchen, sie den Com-Server wenden muss. Ebenso die Delegierung in der com-Zone weist den Com-Server an, die um die Zone "contoso.com" zu suchen, sie den-Server von Contoso wenden sich an.  
  
> [!NOTE]  
> Eine Delegierung verwendet zwei Arten von Datensätzen. Die Namenserver (NS)-Ressourceneintrag enthält den Namen des einen autoritativen Server. Host (A) und der Host (AAAA)-Ressourceneinträge Geben Sie IP-Version 4 (IPv4) und IP-Version 6 (IPv6)-Adressen von einem autorisierenden Server.  
  
Dieses System von Zonen und Delegierungen erstellt eine hierarchische Struktur, die DNS-Namespace darstellt. Jede Zone stellt eine Ebene in der Hierarchie dar, und jede Delegierung stellt eine Verzweigung der Struktur dar.  
  
Verwenden Sie die Hierarchie von Zonen und Delegierungen, finde ein DNS-Stammserver einen beliebigen Namen in der DNS-Namespace. Die Stammzone enthält Delegierungen, die direkt oder indirekt auf alle anderen Zonen in der Hierarchie zu führen. Ein Server, der den DNS-Stammserver Abfragen kann können die Informationen in die Delegierungen einen beliebigen Namen im Namespace gefunden.  
  
## <a name="recursive-name-resolution"></a>Rekursive namensauflösung

Rekursive namensauflösung bezeichnet den Vorgang mit dem ein DNS-Server die Hierarchie von Zonen und Delegierungen auf Abfragen reagieren kann, für die er nicht autorisierend ist.  
  
In einigen Konfigurationen enthalten DNS-Server Stammhinweise (d. h. eine Liste mit Namen und IP-Adressen), mit die sie die DNS-Server Abfragen können. In anderen Konfigurationen weiter Server alle Abfragen, die sie nicht auf einen anderen Server beantworten. Weiterleitung und die Stamm-Hinweise werden beide Methoden, mit denen DNS-Servern zum Auflösen von Abfragen für die sie nicht autorisierend sind.  
  
### <a name="resolving-names-by-using-root-hints"></a>Auflösen von Namen mithilfe von Stammhinweisen

Stammhinweise ermöglichen einen DNS-Server, die DNS-Stammserver gesucht werden soll. Nachdem Sie ein DNS-Server den DNS-Stammserver gefunden wurde, kann jede Abfrage für diesen Namespace aufgelöst werden. In der folgende Abbildung wird beschrieben, wie DNS einen Namen unter Verwendung von Stammhinweisen auflöst.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse:  
  
1. Ein Client sendet eine rekursive Abfrage an einen DNS-Server die IP-Adresse anfordern, die den Namen ftp.contoso.com entspricht. Eine rekursive Abfrage gibt an, dass der Client eine definitive Antwort auf ihre Abfrage wünscht. Die Antwort auf die rekursive Abfrage muss eine gültige Adresse oder eine Meldung, dass die Adresse kann nicht gefunden werden.  
2. Da der DNS-Server für den Namen nicht autorisierend ist und verfügt nicht über die Antwort in seinem Cache, verwendet der DNS-Server Stammhinweise, um die IP-Adresse der DNS-Stammserver zu suchen.  
3. Der DNS-Server wird mit einer iterativen Abfrage den DNS-Stammserver zum Auflösen der Namen ftp.contoso.com aufgefordert. Eine iterative Abfrage gibt an, dass der Server einen Verweis auf einen anderen Server anstelle von definitive Antwort auf die Abfrage akzeptiert wird. Da die Namen ftp.contoso.com mit der Bezeichnung endet com, der DNS-Stammserver gibt einen Verweis an den Com-Server, die die com-Zone hostet.  
4. Der DNS-Server wird mit einer iterativen Abfrage den Com-Server zum Auflösen der Namen ftp.contoso.com aufgefordert. Da die ftp.contoso.com Name mit dem Namen "contoso.com" endet, gibt der Com-Server einen Verweis auf den Contoso-Server, der die Zone "contoso.com" hostet zurück.  
5. Der DNS-Server wird mit einer iterativen Abfrage den Contoso-Server zum Auflösen der Namen ftp.contoso.com aufgefordert. Der Contoso-Server sucht die Antwort in seiner Zonendaten aus und gibt die Antwort an den Server.  
6. Der Server hat das Ergebnis dann an den Client zurückgegeben.  
  
### <a name="resolving-names-by-using-forwarding"></a>Auflösen von Namen mithilfe von Weiterleitung

Weiterleitung ermöglicht Ihnen, Route namensauflösung über bestimmte Server anstelle von Stammhinweisen. Die folgende Abbildung beschreibt, wie DNS einen Namen aufgelöst wird mithilfe von Weiterleitung.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse:  
  
1. Ein Client fragt einen DNS-Server für die Name-ftp.contoso.com.  
2. Der DNS-Server leitet die Abfrage auf einen anderen DNS-Server, bekannt als Weiterleitung.  
3. Da die Weiterleitung für den Namen nicht autorisierend ist und die Antwort im jeweiligen Cache verfügt nicht über, verwendet sie Stammhinweise, um die IP-Adresse der DNS-Stammserver zu suchen.  
4. Die Weiterleitung wird mit einer iterativen Abfrage den DNS-Stammserver zum Auflösen der Namen ftp.contoso.com aufgefordert. Da die ftp.contoso.com Name mit dem Namen endet com, der DNS-Stammserver gibt einen Verweis an den Com-Server, die die com-Zone hostet.  
5. Die Weiterleitung wird mit einer iterativen Abfrage den Com-Server zum Auflösen der Namen ftp.contoso.com aufgefordert. Da die ftp.contoso.com Name mit dem Namen "contoso.com" endet, gibt der Com-Server einen Verweis auf den Contoso-Server, der die Zone "contoso.com" hostet zurück.  
6. Die Weiterleitung wird mit einer iterativen Abfrage den Contoso-Server zum Auflösen der Namen ftp.contoso.com aufgefordert. Der Contoso-Server die Antwort in seinen Zonendateien sucht und gibt dann die Antwort an den Server zurück.  
7. Die Weiterleitung wird das Ergebnis dann an den ursprünglichen DNS-Server zurückgegeben.  
8. Die ursprüngliche DNS-Server wird das Ergebnis dann an den Client zurückgegeben.  
