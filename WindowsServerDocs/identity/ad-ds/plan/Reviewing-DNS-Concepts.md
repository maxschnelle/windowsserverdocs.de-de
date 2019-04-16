---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: "Überprüfen von DNS-Konzepten"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 29c4c3d1d785d1b3b1fa1926eca8298aab2b3ee3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="reviewing-dns-concepts"></a>Überprüfen von DNS-Konzepten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Domain Name System (DNS) ist eine verteilte Datenbank, die einen Namespace darstellt. Der Namespace enthält alle Informationen für einen beliebigen Namen suchen Clients erforderlich. Alle DNS-Server können Sie Abfragen, die über einen beliebigen Namen in seinem Namespace beantworten. Ein DNS-Server beantwortet Abfragen in einem der folgenden Methoden:  
  
-   Die Antwort im Cache ist, antwortet die Abfrage aus dem Cache an.  
  
-   Die Antwort in einer Zone vom DNS-Server gehostet wird, antwortet die Abfrage in der Zone an. Eine Zone ist ein Teil der DNS-Struktur, die auf einem DNS-Server gespeichert. Wenn ein DNS-Server eine Zone hostet, ist es für die Namen in dieser Zone autorisierend (d.h. der DNS-Server kann beantworten Abfragen für alle Namen in der Zone). Beispielsweise kann ein Server, der die Zone contoso.com hostet Abfragen für einen beliebigen Namen in contoso.com beantworten.  
  
-   Wenn die Abfrage aus der Cache oder Zonen nicht erfüllen kann, wird der andere Server für die Antwort abgefragt.  
  
Es ist wichtig zu verstehen, die Kernfunktionen von DNS, z.B. Delegierung rekursive Namensauflösung und Active Directory-integrierte DNS-Zonen, da sie keinen direkten Einfluss auf die Active Directory-Entwurf der logischen Struktur aufweisen.  
  
Weitere Informationen zu DNS und Active Directory-Domänendienste (AD DS) finden Sie unter [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md).  
  
## <a name="delegation"></a>Delegierung  
Für eine DNS-Server zur Beantwortung von Abfragen über einen beliebigen Namen müssen sie einen direkten oder indirekten Pfad auf jede Zone im Namespace haben. Diese Pfade werden durch die Delegierung erstellt. Eine Delegierung ist ein Datensatz in einer übergeordneten Zone, die einen Namenserver aufgeführt, der für die Zone in der Ebene der Hierarchie maßgeblich ist. Delegierungen können für Server in einer Zone Clients auf Servern in anderen Zonen verweisen. Die folgende Abbildungzeigt ein Beispiel für Delegierungszwecke vertraut wird.  
  
![DNS-Konzepten](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
Die Stamm-DNS-Server hostet die Stammzone als einen Punkt (. ). Die Stammzone enthält eine Delegierung zu einer Zone in der Ebene der Hierarchie, die COM-Zone. Die Delegierung in der Stammzone weist die Stamm-DNS-Server, dass die COM-Zone, es den COM-Server erhalten muss. Entsprechend wird die Delegierung in der COM-Zone weist dem COM-Server, die muss die Zone contoso.com, es den Contoso-Server erhalten.  
  
> [!NOTE]  
> Eine Delegierung verwendet zwei Arten von Einträgen. Der Namenserver (NS)-Ressourceneintrag enthält den Namen eines autorisierenden Servers. Host (A) und Host (AAAA)-Ressourceneinträge bieten IP Version 4 (IPv4) und IP-Version 6 (IPv6)-Adressen von einem autorisierenden Server.  
  
Dieses System von Zonen und Delegierungen erstellt eine hierarchische Struktur, die den DNS-Namespace darstellt. Jede Zone steht eine Ebene in der Hierarchie und jede Delegation einen Zweig der Struktur.  
  
Mithilfe der Hierarchie von Zonen und Delegierungen kann DNS-Stammserver einen beliebigen Namen im DNS-Namespace finden. Die Stammzone enthält Delegierungen, die direkt oder indirekt zu allen anderen Zonen in der Hierarchie führen. Ein Server, der die Stamm-DNS-Server Abfragen kann können die Informationen in Delegierungen Sie um einen beliebigen Namen im Namespace finden.  
  
## <a name="recursive-name-resolution"></a>Rekursive Namensauflösung  
Rekursive Namensauflösung bezeichnet den Vorgang mit dem DNS-Server die Hierarchie der Zonen und Delegierungen zur Beantwortung von Abfragen für die er nicht autorisierend ist.  
  
In einigen Konfigurationen umfassen DNS-Server Stammhinweise (d.h., eine Liste mit Namen und IP-Adressen), mit die sie die DNS-Server Abfragen können. In anderen Konfigurationen weiterleiten Server alle Abfragen, die sie nicht auf einen anderen Server beantworten. Hinweise für die Weiterleitung und Stamm sind beide Methoden, mit dem DNS-Server Auflösen von Abfragen für die sie nicht autorisierend sind.  
  
### <a name="resolving-names-by-using-root-hints"></a>Auflösen von Namen mithilfe von Stammhinweisen  
Stammhinweise aktivieren Sie einen DNS-Server, die DNS-Server gesucht werden soll. Nachdem ein DNS-Server die Stamm-DNS-Server gefunden hat, kann dieser eine Abfrage für diesen Namespace verweisen. Die folgende Abbildungbeschreibt, wie DNS einen Namen mithilfe von Stammhinweisen verweist.  
  
![DNS-Konzepten](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse:  
  
1.  Ein Client sendet eine rekursive Abfragen an einen DNS-Server die IP-Adresse anfordern, die den Namen ftp.contoso.com entspricht. Eine rekursive weist darauf hin, dass der Client eine endgültige Antwort auf die Abfrage möchte. Die Antwort auf die rekursive Abfrage muss eine gültige Adresse oder eine Meldung angezeigt, dass die Adresse nicht gefunden werden kann.  
  
2.  Da der DNS-Server nicht autorisierend für den Namen ist und verfügt nicht über die Antwort in den Cache, verwendet der DNS-Server Stammhinweise, um die IP-Adresse des DNS-Stammservers finden.  
  
3.  Der DNS-Server wird eine iterative Abfrage die Stamm-DNS-Server zum Auflösen des Namens ftp.contoso.com anfordern. Eine iterative Abfrage gibt an, dass der Server einen Verweis auf einen anderen Server anstelle einer endgültigen Antwort auf die Abfrage akzeptiert. Da der Name ftp.contoso.com mit der Bezeichnung endet com, die Stamm-DNS-Server gibt einen Verweis auf den Com-Server, die die COM-Zone hostet.  
  
4.  Der DNS-Server wird eine iterative Abfrage den COM-Server zum Auflösen des Namens ftp.contoso.com anfordern. Da der Name ftp.contoso.com mit dem Namen contoso.com endet, der com-Server gibt einen Verweis zurück an den Contoso-Server die Hosts die contoso.com Zone.  
  
5.  Der DNS-Server wird eine iterative Abfrage an den Contoso-Server zum Auflösen des Namens ftp.contoso.com Fragen. Der Contoso-Server wird die Antwort gefunden wird, in die Zonendaten aus und gibt die Antwort auf dem Server.  
  
6.  Der Server gibt das Ergebnis dann an den Client zurück.  
  
### <a name="resolving-names-by-using-forwarding"></a>Auflösen von Namen mithilfe von Weiterleitung  
Weiterleitung ermöglicht Ihnen, Namensauflösung über bestimmte Server anstelle von Stammhinweisen Route. Die folgende Abbildungbeschreibt, wie DNS einen Namen mithilfe von Weiterleitung verweist.  
  
![DNS-Konzepten](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse:  
  
1.  Ein Client fragt einen DNS-Server für den Namen ftp.contoso.com.  
  
2.  Der DNS-Server leitet die Abfrage an einen anderen DNS-Server, der als Weiterleitung bezeichnet.  
  
3.  Da die Weiterleitung nicht autorisierend für den Namen und verfügt nicht über die Antwort in den Cache, stellt er finden Sie die IP-Adresse des DNS-Stammservers Stammhinweise.  
  
4.  Die Weiterleitung wird eine iterative Abfrage die Stamm-DNS-Server zum Auflösen des Namens ftp.contoso.com anfordern. Da der Name ftp.contoso.com mit dem Namen endet com, die Stamm-DNS-Server gibt einen Verweis auf den Com-Server, die die COM-Zone hostet.  
  
5.  Die Weiterleitung verwendet eine iterative Abfrage, um den COM-Server zum Auflösen des Namens ftp.contoso.com Fragen. Da der Name ftp.contoso.com mit dem Namen contoso.com endet, der com-Server gibt einen Verweis zurück an den Contoso-Server die Hosts die contoso.com Zone.  
  
6.  Die Weiterleitung wird eine iterative Abfrage an den Contoso-Server zum Auflösen des Namens ftp.contoso.com Fragen. Der Contoso-Server wird die Antwort in der Zonendateien gefunden und gibt dann die Antwort auf dem Server.  
  
7.  Die Weiterleitung gibt das Ergebnis an den ursprünglichen DNS-Server zurück.  
  
8.  Die ursprüngliche DNS-Server wird das Ergebnis dann an den Client zurückgegeben.  
  


