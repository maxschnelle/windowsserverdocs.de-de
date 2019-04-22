---
title: Konfigurieren von Firewalls für den RADIUS-Datenverkehr
description: 'Dieses Thema enthält eine Übersicht über Vorgehensweise: Konfigurieren von Firewalls, damit der RADIUS-Verkehr für Netzwerkrichtlinienserver unter Windows Server 2016 zu ermöglichen.'
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 94b03349f21a40f9bf42508d5a2878a5cf2946cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819451"
---
# <a name="configure-firewalls-for-radius-traffic"></a>Konfigurieren von Firewalls für den RADIUS-Datenverkehr

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Firewalls können so konfiguriert werden, zu genehmigen oder verweigern Typen von IP-Datenverkehr zu und von dem Computer oder Gerät, auf dem die Firewall ausgeführt wird. Wenn Firewalls zum Zulassen von RADIUS-Datenverkehr zwischen RADIUS-Clients nicht ordnungsgemäß konfiguriert sind, kann RADIUS-Proxys und RADIUS-Server authentifizieren des Netzwerkzugriffs fehl verhindert, dass Benutzer den Zugriff auf Netzwerkressourcen. 

Möglicherweise müssen Sie zwei Arten von Firewalls zum Zulassen von RADIUS-Datenverkehr zu konfigurieren:

- Windows Defender Firewall mit erweiterter Sicherheit auf dem lokalen Server (Network Policy Server, NPS) ausgeführt.
- Firewalls auf andere Computer oder Hardwaregeräten ausgeführt wird.

## <a name="windows-firewall-on-the-local-nps"></a>Windows-Firewall auf den lokalen NPS

In der Standardeinstellung NPS sendet und empfängt den RADIUS-Datenverkehr mithilfe des User Datagram-Protokoll \(UDP\) Ports 1812, 1813, 1645 und 1646. Windows Defender Firewall für den NPS wird automatisch mit Ausnahmen konfiguriert, während der Installation von NPS, um diesen RADIUS-Datenverkehr senden und empfangen werden.

Aus diesem Grund, wenn Sie den Standard-UDP-Ports verwenden, müssen nicht Sie die Windows Defender Firewall-Konfiguration zum Zulassen von RADIUS-Datenverkehr zu und von NPSs zu ändern.

In einigen Fällen empfiehlt es sich zum Ändern der Ports, mit denen NPS RADIUS-Datenverkehr. Wenn Sie konfigurieren die NPS- und Ihre Netzwerkzugriffsserver, zum Senden und Empfangen von RADIUS-Verkehr über andere Ports als die Standardwerte, gehen Sie folgendermaßen vor:

- Entfernen Sie die Ausnahmen, die RADIUS-Datenverkehr über die Standardports zu ermöglichen.
- Erstellen Sie neue Ausnahmen, die RADIUS-Datenverkehr auf die neuen Ports zulassen.

Weitere Informationen finden Sie unter [Konfigurieren von NPS UDP-Portinformationen](nps-udp-ports-configure.md).

## <a name="other-firewalls"></a>Andere firewalls

In der am häufigsten verwendete Konfiguration die Firewall, die mit dem Internet verbunden ist, und der NPS ist eine Intranetressource, die mit dem Umkreisnetzwerk verbunden ist.

Um den Domänencontroller im Intranet erreichen, kann der NPS aufweisen:

- Eine Schnittstelle in dem Umkreisnetzwerk und eine Schnittstelle im Intranet (IP-routing ist nicht aktiviert). 
- Eine einzige Schnittstelle im Umkreisnetzwerk. In dieser Konfiguration kommuniziert NPS mit Domänencontrollern über eine andere Firewall, der das Umkreisnetzwerk zum Intranet verbindet.

## <a name="configuring-the-internet-firewall"></a>Konfigurieren die Internetfirewall

Die Firewall, die mit dem Internet verbunden ist, muss mit Eingabe- und Ausgabedaten Filtern an seiner Internetschnittstelle konfiguriert werden \(und, optional, seine Netzwerkschnittstelle Umkreis\), um die Weiterleitung von RADIUS-Nachrichten zwischen den NPS zu ermöglichen. und RADIUS-Clients oder Proxys über das Internet. Zusätzliche Filter können verwendet werden, um die Übergabe von Datenverkehr an den Webserver, VPN-Server und andere Arten von Servern im Umkreisnetzwerk zu ermöglichen.

Trennen Sie die Eingabe- und -Paket, das an die Internetschnittstelle und das Umkreisnetzwerk-Schnittstelle konfiguriert werden können.

### <a name="configure-input-filters-on-the-internet-interface"></a>Eingabefilter an der Internetschnittstelle konfigurieren

Konfigurieren Sie die folgenden Paketfilter für Eingabe, für die Internetschnittstelle von der Firewall für die folgenden Arten von Datenverkehr:

- Ziel IP-Adresse dem Umkreisnetzwerk und der UDP-Zielport 1812 (0 x 714), der den NPS.  Dieser Filter lässt die RADIUS-Authentifizierung-Datenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1812 durch.
- Ziel IP-Adresse dem Umkreisnetzwerk und der UDP-Zielport 1813 (0 x 715) des NPS. Dieser Filter lässt die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1813 durch.
- \(Optionale\) Ziel-IP-Adresse des dem Umkreisnetzwerk und der UDP-Zielport 1645 \(0x66D\) von NPS. Dieser Filter lässt die RADIUS-Authentifizierung-Datenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optionale\) Ziel-IP-Adresse des dem Umkreisnetzwerk und der UDP-Zielport 1646 \(0x66E\) von NPS. Dieser Filter lässt die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-internet-interface"></a>Konfigurieren Sie Ausgabefilter, auf die Internet-Schnittstelle

Konfigurieren Sie die folgenden Ausgabefilter an der Internetschnittstelle von der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Quelle IP-Adresse dem Umkreisnetzwerk und der UDP-Quellport 1812 (0 x 714), der den NPS. Dieser Filter lässt RADIUS-Authentifizierung-Datenverkehr aus den NPS RADIUS internetbasierten Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1812 durch.
- Quelle IP-Adresse dem Umkreisnetzwerk und der UDP-Quellport 1813 (0 x 715) des NPS. Dieser Filter lässt RADIUS-Kontoführungsdatenverkehr aus dem NPS RADIUS internetbasierten Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1813 durch.
- \(Optionale\) Quell-IP-Adresse des dem Umkreisnetzwerk und der UDP-Quellport 1645 \(0x66D\) von NPS. Dieser Filter lässt RADIUS-Authentifizierung-Datenverkehr aus den NPS RADIUS internetbasierten Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optionale\) Quell-IP-Adresse des dem Umkreisnetzwerk und der UDP-Quellport 1646 \(0x66E\) von NPS. Dieser Filter lässt RADIUS-Kontoführungsdatenverkehr aus dem NPS RADIUS internetbasierten Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>Konfigurieren Sie die Eingabefilter auf der Umkreisnetzwerk-Schnittstelle

Konfigurieren Sie die folgenden Eingabefilter, auf dem Umkreisnetzwerk-Schnittstelle von der Firewall für die folgenden Arten von Datenverkehr:

- Quelle IP-Adresse dem Umkreisnetzwerk und der UDP-Quellport 1812 (0 x 714), der den NPS. Dieser Filter lässt RADIUS-Authentifizierung-Datenverkehr aus den NPS RADIUS internetbasierten Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1812 durch.
- Quelle IP-Adresse dem Umkreisnetzwerk und der UDP-Quellport 1813 (0 x 715) des NPS. Dieser Filter lässt RADIUS-Kontoführungsdatenverkehr aus dem NPS RADIUS internetbasierten Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1813 durch.
- \(Optionale\) Quell-IP-Adresse des dem Umkreisnetzwerk und der UDP-Quellport 1645 \(0x66D\) von NPS. Dieser Filter lässt RADIUS-Authentifizierung-Datenverkehr aus den NPS RADIUS internetbasierten Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optionale\) Quell-IP-Adresse des dem Umkreisnetzwerk und der UDP-Quellport 1646 \(0x66E\) von NPS. Dieser Filter lässt RADIUS-Kontoführungsdatenverkehr aus dem NPS RADIUS internetbasierten Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>Konfigurieren Sie Ausgabefilter, auf dem Umkreisnetzwerk-Schnittstelle

Konfigurieren Sie die folgenden Paketfilter für die Ausgabe auf der Umkreisnetzwerk-Schnittstelle von der Firewall für die folgenden Arten von Datenverkehr an:

- Ziel IP-Adresse dem Umkreisnetzwerk und der UDP-Zielport 1812 (0 x 714), der den NPS. Dieser Filter lässt die RADIUS-Authentifizierung-Datenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1812 durch.
- Ziel IP-Adresse dem Umkreisnetzwerk und der UDP-Zielport 1813 (0 x 715) des NPS. Dieser Filter lässt die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die entsprechende Portnummer 1813 durch.
- \(Optionale\) Ziel-IP-Adresse des dem Umkreisnetzwerk und der UDP-Zielport 1645 \(0x66D\) von NPS. Dieser Filter lässt die RADIUS-Authentifizierung-Datenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optionale\) Ziel-IP-Adresse des dem Umkreisnetzwerk und der UDP-Zielport 1646 \(0x66E\) von NPS. Dieser Filter lässt die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

Zur Erhöhung der Sicherheit können Sie jeden RADIUS-Client die IP-Adressen, die die Pakete über die Firewall für den Filter für den Datenverkehr zwischen dem Client und die IP-Adresse des NPS im Umkreisnetzwerk definieren sendet.

### <a name="filters-on-the-perimeter-network-interface"></a>Filter für das Umkreisnetzwerk-Schnittstelle

Konfigurieren Sie die folgenden Paketfilter für Eingabe, auf dem Perimeternetzwerk-Schnittstelle des Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Quelle IP-Adresse der Umkreisnetzwerkschnittstelle von NPS. Dieser Filter lässt Datenverkehr von den NPS auf dem Umkreisnetzwerk.

Konfigurieren Sie die folgenden Ausgabefilter, auf dem Perimeternetzwerk-Schnittstelle des Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel IP-Adresse der Umkreisnetzwerkschnittstelle von NPS. Dieser Filter lässt Datenverkehr an den NPS im Umkreisnetzwerk.

### <a name="filters-on-the-intranet-interface"></a>Filter für die Intranetschnittstelle

Konfigurieren Sie die folgenden Eingabefilter auf der Intranetschnittstelle des Firewalls, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel IP-Adresse der Umkreisnetzwerkschnittstelle von NPS. Dieser Filter lässt Datenverkehr an den NPS im Umkreisnetzwerk.

Konfigurieren Sie die folgenden Paketfilter für die Ausgabe auf der Intranetschnittstelle des Firewalls, um die folgenden Arten von Datenverkehr zuzulassen:

- Quelle IP-Adresse der Umkreisnetzwerkschnittstelle von NPS. Dieser Filter lässt Datenverkehr von den NPS auf dem Umkreisnetzwerk.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).




