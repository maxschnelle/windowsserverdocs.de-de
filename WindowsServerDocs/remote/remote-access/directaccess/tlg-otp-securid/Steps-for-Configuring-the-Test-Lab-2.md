---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0607506f2b6dd49284e6b377fb87da4f731eb94d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283084"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Schritte beschreiben das Konfigurieren der remotezugriffinfrastruktur, RAS-Server und Client konfigurieren und Testen der DirectAccess-Konnektivität aus dem Homenet und Internet-Subnetz.  
  
In dieser testumgebungsanleitung erstellen Sie einen Remotezugriff mit OTP-Umgebung durch die folgenden Schritte ausführen:  
  
-   [SCHRITT 1: Schließen Sie die DirectAccess-Konfiguration](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6). Führen Sie alle Schritte in der [Test Lab Guide: Veranschaulichen von DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6-](https://go.microsoft.com/fwlink/p/?LinkId=237004).  
  
-   [SCHRITT 2: Konfigurieren von APP1](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff). Konfigurieren von APP1 mit OTP-Zertifikatvorlagen für die Verwendung von EDGE1.  
  
-   [SCHRITT 3: Konfigurieren von DC1](assetId:///904a6edc-a771-45ed-9630-a34a680bb522). Stellen Sie sicher, dass User Principal Name auf DC1 definiert.  
  
-   [SCHRITT 7: Installieren und Konfigurieren von RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a). Installieren und Konfigurieren von EDGE1 für OTP RSA, eine RADIUS- und der OTP-Server konfigurieren.  
  
-   [SCHRITT 11: Überprüfen der OTP-Integrität auf EDGE1](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba). Stellen Sie sicher, dass der Status von OTP auf dem RAS-Server fehlerfrei ist.  
  
-   [SCHRITT 8: Testen der DirectAccess-Konnektivität aus dem Subnetz "Homenet"](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14). Testen der DirectAccess-OTP-Funktionalität hinter einem NAT-Gerät.  
  
-   [SCHRITT 10: Testen der DirectAccess-Konnektivität über das Internet](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9). Testen der DirectAccess-Clientkonnektivität aus dem Internet.  
  
-   [SCHRITT 12: Eine Momentaufnahme der Konfiguration](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4). Nach Abschluss der testumgebung können eine Momentaufnahme der arbeiten DirectAccess mit OTP-Konfiguration, damit Sie zurückkehren können, um diese später, um zusätzliche Szenarien zu testen.  
  


