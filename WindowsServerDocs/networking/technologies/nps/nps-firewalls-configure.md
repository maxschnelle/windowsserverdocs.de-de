---
title: Konfigurieren von Firewalls für RADIUS-Datenverkehr
description: Dieses Thema enthält eine Übersicht über das Konfigurieren von Firewalls für Netzwerkrichtlinienserver in Windows Server 2016 RADIUS-Datenverkehr zulassen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 140111e10eabbece098ae9b7c36746cc663c9cce
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-firewalls-for-radius-traffic"></a>Konfigurieren von Firewalls für RADIUS-Datenverkehr

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Firewalls können so konfiguriert werden, dass zulassen oder blockieren Typen von IP-Datenverkehr zu und von dem Computer oder Gerät, auf dem die Firewall ausgeführt wird. Wenn Firewalls zum Zulassen von RADIUS-Datenverkehr zwischen RADIUS-Clients nicht ordnungsgemäß konfiguriert sind, kann RADIUS-Proxys und RADIUS-Servern, die Netzwerkzugriffsauthentifizierung fehlschlagen, verhindert, dass Benutzer den Zugriff auf Netzwerkressourcen. 

Möglicherweise müssen Sie zwei Arten von Firewalls zum Zulassen von RADIUS-Datenverkehr zu konfigurieren:

- Windows Defender-Firewall mit erweiterter Sicherheit auf dem lokalen Server (Network Policy Server, NPS) ausgeführt.
- Firewalls auf andere Computer oder Geräte.

## <a name="windows-firewall-on-the-local-nps-server"></a>Windows-Firewall auf dem lokalen NPS-server

In der Standardeinstellung NPS sendet und empfängt RADIUS-Datenverkehr mithilfe des User Datagram-Protokoll \(UDP\) Ports 1812, 1813, 1645 und 1646. Windows Defender-Firewall auf dem NPS-Server wird automatisch mit Ausnahmen konfiguriert, während der Installation von NPS, um diesen RADIUS-Datenverkehr gesendet und empfangen werden.

Daher, wenn Sie die Standard-UDP-Ports verwenden, nicht müssen Sie zum Ändern der Windows Defender-Firewall-Konfiguration, um RADIUS-Datenverkehr zu und von NPS-Servern zu ermöglichen.

In einigen Fällen möchten möglicherweise die Ports ändern, die NPS RADIUS-Datenverkehr verwendet. Wenn Sie konfigurieren NPS und Ihre Netzwerkzugriffsserver, zum Senden und Empfangen von RADIUS-Datenverkehr auf andere Ports als die Standardeinstellungen, müssen Sie Folgendes tun:

- Entfernen Sie die Ausnahmen, die RADIUS-Datenverkehr über die Standardports zu ermöglichen.
- Erstellen Sie neue Ausnahmen, die RADIUS-Datenverkehr über die neuen Ports zulassen.

Weitere Informationen finden Sie unter [Konfigurieren von NPS-UDP-Portinformationen](nps-udp-ports-configure.md).

## <a name="other-firewalls"></a>Anderer firewalls

In der am häufigsten verwendeten Konfiguration die Firewall mit dem Internet verbunden ist, und der Netzwerkrichtlinienserver ist eine Intranetressource, die mit dem Umkreisnetzwerk verbunden ist.

Um den Domänencontroller im Intranet erreichen, möglicherweise der NPS-Server:

- Eine Schnittstelle für das Umkreisnetzwerk und eine Schnittstelle im Intranet (IP-routing ist nicht aktiviert). 
- Eine Oberfläche im Umkreisnetzwerk. In dieser Konfiguration kommuniziert der Netzwerkrichtlinienserver mit Domänencontrollern über eine andere Firewall, der das Umkreisnetzwerk zum Intranet verbindet.

## <a name="configuring-the-internet-firewall"></a>Konfigurieren die Internetfirewall

Die Firewall, die mit dem Internet verbunden ist, muss mit Eingabe- und Ausgabedateien Filter an der Internetschnittstelle konfiguriert werden \ (und optional dessen Netzwerk Umkreisnetzwerk Interface\), um die Weiterleitung von RADIUS-Nachrichten zwischen den NPS-Server und RADIUS-Clients oder Proxys im Internet zu ermöglichen. Zusätzliche Filter können verwendet werden, um die Übergabe von Datenverkehr an Webserver, VPN-Server und andere Arten von Servern im Umkreisnetzwerk zu ermöglichen.

Trennen Sie die Eingabe- und Ausgabedateien Paketfilter an der Internetschnittstelle und dem Umkreisnetzwerk-Schnittstelle konfiguriert werden können.

### <a name="configure-input-filters-on-the-internet-interface"></a>Eingabe Filter für die Internetschnittstelle konfigurieren

Konfigurieren Sie die folgende Eingabe Paketfilter für die Internetschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse dem Umkreisnetzwerk und UDP-Zielport 1812 (0 x 714) des NPS-Servers.  Mit diesem Filter kann RADIUS-Authentifizierungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie 1812 Portnummer.
- Ziel-IP-Adresse dem Umkreisnetzwerk und UDP-Zielport 1813 (0 x 715) des Netzwerkrichtlinienservers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie Portnummer 1813.
- \(Optional\) IP-Adresse des dem Umkreisnetzwerk und UDP-Zielport 1645 \(0x66D\) des NPS-Servers. Mit diesem Filter kann RADIUS-Authentifizierungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optional\) IP-Adresse des dem Umkreisnetzwerk und UDP-Zielport 1646 \(0x66E\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-internet-interface"></a>Konfigurieren von Ausgabefiltern auf der Internet-Schnittstelle

Konfigurieren Sie die folgende Ausgabefilter für die Internetschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- IP-Quelladresse Umkreisnetzwerk und UDP-Quellport 1812 (0 x 714) des NPS-Servers. Mit diesem Filter kann die RADIUS-Authentifizierungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie 1812 Portnummer.
- IP-Quelladresse Umkreisnetzwerk und UDP-Quellport 1813 (0 x 715) des Netzwerkrichtlinienservers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie Portnummer 1813.
- \(Optional\) Quell-IP-Adresse des dem Umkreisnetzwerk und UDP-Quellport 1645 \(0x66D\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Authentifizierungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optional\) Quell-IP-Adresse des dem Umkreisnetzwerk und UDP-Quellport 1646 \(0x66E\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>Konfigurieren von Eingabe Filtern auf der Perimeternetzwerk-Schnittstelle

Konfigurieren Sie die folgende Eingabe Filter auf der Perimeternetzwerk-Schnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- IP-Quelladresse Umkreisnetzwerk und UDP-Quellport 1812 (0 x 714) des NPS-Servers. Mit diesem Filter kann die RADIUS-Authentifizierungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie 1812 Portnummer.
- IP-Quelladresse Umkreisnetzwerk und UDP-Quellport 1813 (0 x 715) des Netzwerkrichtlinienservers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie Portnummer 1813.
- \(Optional\) Quell-IP-Adresse des dem Umkreisnetzwerk und UDP-Quellport 1645 \(0x66D\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Authentifizierungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optional\) Quell-IP-Adresse des dem Umkreisnetzwerk und UDP-Quellport 1646 \(0x66E\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr vom Netzwerkrichtlinienserver an internetbasierte RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>Konfigurieren von Ausgabefiltern auf der Perimeternetzwerk-Schnittstelle

Konfigurieren Sie die folgenden Paketfilter für die Ausgabe an das Umkreisnetzwerk-Schnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse dem Umkreisnetzwerk und UDP-Zielport 1812 (0 x 714) des NPS-Servers. Mit diesem Filter kann RADIUS-Authentifizierungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie 1812 Portnummer.
- Ziel-IP-Adresse dem Umkreisnetzwerk und UDP-Zielport 1813 (0 x 715) des Netzwerkrichtlinienservers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der Standard-UDP-Port, der vom Netzwerkrichtlinienserver verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie Portnummer 1813.
- \(Optional\) IP-Adresse des dem Umkreisnetzwerk und UDP-Zielport 1645 \(0x66D\) des NPS-Servers. Mit diesem Filter kann RADIUS-Authentifizierungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(Optional\) IP-Adresse des dem Umkreisnetzwerk und UDP-Zielport 1646 \(0x66E\) des NPS-Servers. Mit diesem Filter kann die RADIUS-Kontoführungsdatenverkehr von internetbasierten RADIUS-Clients an den Netzwerkrichtlinienserver. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

Zur Erhöhung der Sicherheit können Sie die IP-Adressen für jeden RADIUS-Client, die die Pakete über die Firewall definieren Sie Filter für den Datenverkehr zwischen dem Client und die IP-Adresse des NPS-Servers im Umkreisnetzwerk sendet.

### <a name="filters-on-the-perimeter-network-interface"></a>Filter für das Umkreisnetzwerk

Konfigurieren Sie die folgende Eingabe Paketfilter auf dem Umkreisnetzwerk-Schnittstelle des Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Quelle IP-Adresse der Perimeternetzwerk-Schnittstelle des NPS-Servers. Mit diesem Filter kann Datenverkehr aus dem NPS-Server im Umkreisnetzwerk.

Konfigurieren Sie die folgende Ausgabefilter auf das Umkreisnetzwerk-Schnittstelle des Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Perimeternetzwerk-Schnittstelle des NPS-Servers. Mit diesem Filter können Datenverkehr an den NPS-Server im Umkreisnetzwerk.

### <a name="filters-on-the-intranet-interface"></a>Filter für die Intranetschnittstelle

Konfigurieren Sie die folgende Eingabe Filter auf der Intranetschnittstelle des Firewalls, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Perimeternetzwerk-Schnittstelle des NPS-Servers. Mit diesem Filter können Datenverkehr an den NPS-Server im Umkreisnetzwerk.

Konfigurieren Sie die folgenden Paketfilter für die Ausgabe auf der Intranetschnittstelle des Firewalls, um die folgenden Arten von Datenverkehr zuzulassen:

- Quelle IP-Adresse der Perimeternetzwerk-Schnittstelle des NPS-Servers. Mit diesem Filter kann Datenverkehr aus dem NPS-Server im Umkreisnetzwerk.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).




