---
title: bitsadmin setclientcertificatebyname
description: Referenz Artikel für den Befehl "bitadmin setclientcertificatebyname", der den Antragsteller Namen des Client Zertifikats angibt, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung verwendet werden soll.
ms.topic: reference
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f5a29448641d7d92594e229396146169c3f6a9f4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631047"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

Gibt den Antragsteller Namen des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS-Anforderung (SSL) verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /setclientcertificatebyname <job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| store_location | Gibt den Speicherort eines Systemspeicher an, der zum Nachschlagen des Zertifikats verwendet werden soll. Mögliche Werte sind:<ul><li>1 (CURRENT_USER)</li><li>2 (LOCAL_MACHINE)</li><li>3 (CURRENT_SERVICE)</li><li>4 (Dienste)</li><li>5 (Benutzer)</li><li>6 (CURRENT_USER_GROUP_POLICY)</li><li>7 (LOCAL_MACHINE_GROUP_POLICY)</li><li>8 (LOCAL_MACHINE_ENTERPRISE)</li></ul> |
| store_name | Der Name des Zertifikatspeichers. Mögliche Werte sind:<ul><li>CA (Zertifizierungsstellen Zertifikate)</li><li>Meine (persönliche Zertifikate)</li><li>Root (Stamm Zertifikate)</li><li>SPC (Software Herausgeber Zertifikat)</li></ul> |
| subject_name | Name des Zertifikats. |

## <a name="examples"></a>Beispiele

So geben Sie den Namen des Client Zertifikats *myCertificate* an, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung für den Auftrag mit dem Namen *mydownloadjob*verwendet werden soll:

```
bitsadmin /setclientcertificatebyname myDownloadJob 1 MY myCertificate
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
