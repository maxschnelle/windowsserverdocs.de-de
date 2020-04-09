---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: Überprüfen von DNS-Konzepten
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 37c33ca181394c66ef149715c3f1477774061660
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822063"
---
# <a name="reviewing-dns-concepts"></a>Überprüfen von DNS-Konzepten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domain Name System (DNS) ist eine verteilte Datenbank, die einen Namespace darstellt. Der-Namespace enthält alle Informationen, die für jeden Client benötigt werden, um einen beliebigen Namen zu suchen. Alle DNS-Server können Abfragen über einen beliebigen Namen innerhalb des Namespace beantworten. Ein DNS-Server beantwortet Abfragen auf eine der folgenden Arten:  
  
- Wenn sich die Antwort im Cache befindet, wird die Abfrage aus dem Cache beantwortet.  
- Wenn sich die Antwort in einer vom DNS-Server gehosteten Zone befindet, wird die Abfrage aus der zugehörigen Zone beantwortet. Eine Zone ist ein Teil der DNS-Struktur, die auf einem DNS-Server gespeichert ist. Wenn ein DNS-Server eine Zone hostet, ist er autorisierend für die Namen in dieser Zone (d. h., der DNS-Server kann Abfragen für einen beliebigen Namen in der Zone beantworten). Beispielsweise kann ein Server, auf dem die Zone contoso.com gehostet wird, Abfragen für beliebige Namen in contoso.com beantworten.  
- Wenn der Server die Abfrage nicht aus dem Cache oder den Zonen beantworten kann, fragt er andere Server nach der Antwort ab.  

Es ist wichtig, die Kernfunktionen von DNS zu verstehen, wie z. b. die Delegierung, die rekursive Namensauflösung und Active Directory integrierte DNS-Zonen, da Sie sich direkt auf den Entwurf Ihrer Active Directory logischen Struktur auswirken.  
  
Weitere Informationen zu DNS und Active Directory Domain Services (AD DS) finden Sie unter [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md).  
  
## <a name="delegation"></a>Delegierung

Damit ein DNS-Server Abfragen zu einem beliebigen Namen beantworten kann, muss er über einen direkten oder indirekten Pfad zu jeder Zone im-Namespace verfügen. Diese Pfade werden mithilfe der Delegierung erstellt. Eine Delegierung ist ein Datensatz in einer übergeordneten Zone, in der ein Namen Server aufgeführt wird, der für die Zone auf der nächsten Ebene der Hierarchie autorisierend ist. Delegierungen ermöglichen es Servern in einer Zone, Clients auf Server in anderen Zonen zu verweisen. Die folgende Abbildung zeigt ein Beispiel für die Delegierung.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
Der DNS-Stamm Server hostet die Stammzone, die als Punkt () dargestellt wird. ). Die Stammzone enthält eine Delegierung für eine Zone auf der nächsten Ebene der Hierarchie, der com-Zone. Durch die Delegierung in der Stammzone wird dem DNS-Stamm Server mitgeteilt, dass zum Auffinden der com-Zone der com-Server kontaktiert werden muss. Ebenso teilt die Delegierung in der com-Zone dem com-Server mit, dass zum Suchen der contoso.com-Zone der Server von Configuration Manager kontaktiert werden muss.  
  
> [!NOTE]  
> Eine Delegierung verwendet zwei Arten von Datensätzen. Der Nameserver (NS)-Ressourcen Daten Satz stellt den Namen eines autorisierenden Servers bereit. Host (A)-und Host (AAAA)-Ressourcen Einträge stellen IP-Version 4 (IPv4) und IPv6-Adressen (IP Version 6) eines autoritativen Servers bereit.  
  
Dieses System von Zonen und Delegierungen erstellt eine hierarchische Struktur, die den DNS-Namespace darstellt. Jede Zone stellt eine Ebene in der Hierarchie dar, und jede Delegierung stellt eine Verzweigung der Struktur dar.  
  
Durch die Verwendung der Hierarchie von Zonen und Delegierungen kann ein DNS-Stamm Server einen beliebigen Namen im DNS-Namespace finden. Die Stammzone schließt Delegierungen ein, die direkt oder indirekt alle anderen Zonen in der Hierarchie leiten. Jeder Server, der den DNS-Stamm Server Abfragen kann, kann anhand der Informationen in den Delegierungen einen beliebigen Namen im-Namespace finden.  
  
## <a name="recursive-name-resolution"></a>Rekursive Namensauflösung

Rekursive Namensauflösung ist der Prozess, bei dem ein DNS-Server die Hierarchie von Zonen und Delegierungen verwendet, um auf Abfragen zu antworten, für die er nicht autoritativ ist.  
  
In einigen Konfigurationen enthalten DNS-Server Stamm Hinweise (d. h. eine Liste von Namen und IP-Adressen), mit deren Hilfe die DNS-Stamm Server abgefragt werden können. In anderen Konfigurationen leiten Server alle Abfragen weiter, die Sie nicht auf einen anderen Server beantworten können. Weiterleitungs-und Stamm Hinweise sind beide Methoden, die DNS-Server zum Auflösen von Abfragen verwenden können, für die Sie nicht autoritativ sind.  
  
### <a name="resolving-names-by-using-root-hints"></a>Auflösen von Namen mithilfe von Stamm hinweisen

Mit root-hinweisen können alle DNS-Server die DNS-Stamm Server finden. Nachdem ein DNS-Server den DNS-Stamm Server lokalisiert hat, kann er jede beliebige Abfrage für diesen Namespace auflösen. In der folgenden Abbildung wird beschrieben, wie DNS einen Namen mithilfe von root-hinweisen auflöst.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse auf:  
  
1. Ein Client sendet eine rekursive Abfrage an einen DNS-Server, um die IP-Adresse anzufordern, die dem Namen ftp.contoso.com entspricht. Eine rekursive Abfrage gibt an, dass der Client eine definitive Antwort auf seine Abfrage wünscht. Die Antwort auf die rekursive Abfrage muss eine gültige Adresse oder eine Meldung sein, die angibt, dass die Adresse nicht gefunden werden kann.  
2. Da der DNS-Server für den Namen nicht autorisierend ist und die Antwort nicht in seinem Cache hat, verwendet der DNS-Server Stamm Hinweise, um die IP-Adresse des DNS-Stamm Servers zu ermitteln.  
3. Der DNS-Server verwendet eine iterative Abfrage, um den DNS-Stamm Server zum Auflösen des Namens ftp.contoso.com aufzufordern. Eine iterative Abfrage gibt an, dass der Server einen Verweis auf einen anderen Server anstelle einer definitive Antwort auf die Abfrage akzeptiert. Da der Name FTP.contoso.com mit der Bezeichnung com endet, gibt der DNS-Stamm Server einen Verweis an den com-Server zurück, der die com-Zone hostet.  
4. Der DNS-Server verwendet eine iterative Abfrage, um den com-Server zum Auflösen des Namens ftp.contoso.com aufzufordern. Da der Name FTP.contoso.com mit dem Namen contoso.com endet, gibt der com-Server einen Verweis an den Verbindungs Server von Configuration Manager zurück, der die contoso.com-Zone hostet.  
5. Der DNS-Server verwendet eine iterative Abfrage, um den Server von "FTP.contoso.com" zum Auflösen des Namens "" aufzufordern. Der Server von "Configuration Manager" findet die Antwort in den Zonendaten und gibt dann die Antwort an den Server zurück.  
6. Der Server gibt dann das Ergebnis an den Client zurück.  
  
### <a name="resolving-names-by-using-forwarding"></a>Auflösen von Namen mithilfe der Weiterleitung

Mithilfe der Weiterleitung können Sie die Namensauflösung über bestimmte Server weiterleiten, anstatt Stamm Hinweise zu verwenden. In der folgenden Abbildung wird beschrieben, wie DNS einen Namen mithilfe der Weiterleitung auflöst.  
  
![DNS-Konzepte](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
In diesem Beispiel treten die folgenden Ereignisse auf:  
  
1. Ein Client fragt einen DNS-Server nach dem Namen ftp.contoso.com ab.  
2. Der DNS-Server leitet die Abfrage an einen anderen DNS-Server weiter, der als Weiterleitung bezeichnet wird.  
3. Da die Weiterleitung nicht autorisierend für den Namen ist und nicht die Antwort im Cache hat, verwendet Sie Stamm Hinweise, um die IP-Adresse des DNS-Stamm Servers zu ermitteln.  
4. Die Weiterleitung verwendet eine iterative Abfrage, um den DNS-Stamm Server aufzufordern, den Namen ftp.contoso.com aufzulösen. Da der Name FTP.contoso.com mit dem Namen com endet, gibt der DNS-Stamm Server einen Verweis an den com-Server zurück, der die com-Zone hostet.  
5. Die Weiterleitung verwendet eine iterative Abfrage, um den com-Server zum Auflösen des Namens ftp.contoso.com aufzufordern. Da der Name FTP.contoso.com mit dem Namen contoso.com endet, gibt der com-Server einen Verweis an den Verbindungs Server von Configuration Manager zurück, der die contoso.com-Zone hostet.  
6. Die Weiterleitung verwendet eine iterative Abfrage, um den Server von "FTP.contoso.com" zum Auflösen des Namens "" aufzufordern. Der Server von "Configuration Manager" findet die Antwort in den zugehörigen Zonendateien und gibt dann die Antwort an den Server zurück.  
7. Die Weiterleitung gibt dann das Ergebnis an den ursprünglichen DNS-Server zurück.  
8. Der ursprüngliche DNS-Server gibt dann das Ergebnis an den Client zurück.  
