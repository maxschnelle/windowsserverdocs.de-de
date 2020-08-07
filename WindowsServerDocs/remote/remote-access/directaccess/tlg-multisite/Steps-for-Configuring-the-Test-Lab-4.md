---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7fc886d8b4f68c86885cbe5c032247722d88e269
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955206"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, die RAS-Server und-Clients konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen Internet und homenet testen.

In dieser Test Umgebungs Anleitung erstellen Sie eine Remote Zugriffs Bereitstellung für mehrere Standorte, indem Sie die folgenden Schritte ausführen:

-   [Schritt 1: vervollständigen der Basiskonfiguration](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed). Führen Sie alle Schritte in der [Test Umgebungs Anleitung zum Veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004)aus.

-   [Schritt 2: Installieren und Konfigurieren von ROUTER1](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9). ROUTER1 bietet Routing-und Weiterleitungs Funktionen zwischen den Subnetzen Corpnet und 2-Corpnet.

-   [Schritt 3: Installieren und Konfigurieren von CLIENT2](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee). CLIENT2 ist ein Windows 7-Client Computer, der verwendet wird, um die Abwärtskompatibilität einer Windows Server 2016-, Windows Server 2012 R2-oder Windows Server 2012-Remote Zugriffs Bereitstellung zu veranschaulichen.

-   [Schritt 4: Konfigurieren von App1](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810). Konfigurieren Sie App1 mit ROUTER1 als Standard Gateway und 2 DC1 als alternativen DNS-Server.

-   [Schritt 5: Konfigurieren von DC1](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a). Konfigurieren Sie DC1 mit einer zusätzlichen Active Directory Site und zusätzlichen Sicherheitsgruppen für Windows 7-Client Computer.

-   [Schritt 6: Installieren und Konfigurieren von 2-DC1](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127) Bei einer Bereitstellung mit mehreren Standorten verfügen Sie über zwei oder mehr Domänen und Standorte. 2 DC1 stellt Domänen Controller und DNS-Dienste für die corp2.Corp.contoso.com-Domäne bereit.

-   [Schritt 7: Installieren und Konfigurieren von 2-App1](assetId:///7d04b54e-590a-4d33-9766-415789859f29) 2 App1 ein Web-und Dateiserver im Netzwerk "2-Corpnet".

-   [Schritt 8: Konfigurieren von INET1](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231). INET1 simuliert das Internet in dieser Test Umgebungs Anleitung. Sie müssen einen DNS-Eintrag konfigurieren, der in die öffentliche IP-Adresse von 2-Edge1 aufgelöst wird.

-   [Schritt 9: Konfigurieren von Edge1](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e). Konfigurieren Sie den DNS-Server 2-Corpnet und das Routing auf Edge1.

-   [Schritt 10: Installieren und Konfigurieren von 2-Edge1](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130) Bei einer Bereitstellung mit mehreren Standorten sind zwei Remote Zugriffs Server erforderlich. 2 Edge1 bietet Remote Zugriffs Dienste für die zweite Domäne.

-   [Schritt 11: Konfigurieren der Bereitstellung für mehrere Standorte](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2). Nach dem Konfigurieren von Remote Zugriffs Servern können Sie die Bereitstellung für mehrere Standorte konfigurieren.

-   [Schritt 12: Testen der DirectAccess-Konnektivität](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c). Testen Sie die DirectAccess-Konnektivität von beiden Client Computern aus dem Subnetz Internet über Edge1 und 2-Edge1.

-   [Schritt 13: Testen der DirectAccess-Konnektivität hinter einem NAT-Gerät](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c). Testen Sie die DirectAccess-Konnektivität hinter einem NAT-Gerät.

-   [Schritt 14: Erstellen einer Momentaufnahme der Konfiguration](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84) Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme der funktionierenden Remote Zugriffs Bereitstellung für mehrere Standorte, damit Sie Sie später wieder aufrufen können, um weitere Szenarios zu testen.



