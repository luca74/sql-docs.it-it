---
title: Usa data e ora tipi | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a2aa5644-1e39-4d78-b149-0599d3502cda
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f80954ed7a502fcd95f1d6343cd424cda0df9a12
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="use-date-and-time-types"></a>Utilizzare tipi di data e ora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In questo esempio viene illustrato come inizializzare le strutture dati di data e ora aggiunte in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Successivamente vengono preparati i valori di input e associati i parametri e viene eseguita la query. Per ulteriori informazioni sull'utilizzo di questi tipi, vedere [data e ora miglioramenti &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="example"></a>Esempio  
 È necessaria anche un'origine dati ODBC denominata DateTime. Il database predefinito per DateTime deve essere tempdb. Tale origine dati deve essere basata sul driver ODBC per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Se questo esempio viene compilato ed eseguito come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
 In questo esempio viene eseguita la connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer in uso. Per connettersi a un'istanza denominata, modificare la definizione dell'origine dati ODBC per specificare l'istanza in base al formato: server\istanzadenominata. Per impostazione predefinita, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] viene installato in un'istanza denominata.  
  
 Il primo listato di codice ([!INCLUDE[tsql](../../includes/tsql-md.md)]) consente di creare una tabella utilizzata dall'esempio.  
  
 Compilare il secondo listato di codice (C++) con odbc32.lib e user32.lib. Verificare che nella variabile di ambiente INCLUDE sia presente la directory che contiene sqlncli.h.  
  
 Il terzo listato di codice ([!INCLUDE[tsql](../../includes/tsql-md.md)]) consente di eliminare la tabella utilizzata dall'esempio.  
  
```  
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'DateTimeTypes')  
DROP TABLE DateTimeTypes  
GO  
  
CREATE TABLE DateTimeTypes (datecol date, time2col time(7), datetime2col datetime2(7), datetimeoffsetcol datetimeoffset(7))  
GO  
```  
  
```  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <Sqlext.h>  
#include <mbstring.h>  
#include <sqlncli.h>  
#include <stdio.h>  
  
#define MAX_DATA 1024  
#define MYSQLSUCCESS(rc) ( (rc == SQL_SUCCESS) || (rc == SQL_SUCCESS_WITH_INFO) )  
  
class direxec {  
   RETCODE rc;   // ODBC return code  
   HENV henv;   // Environment  
   HDBC hdbc;   // Connection Handle  
   HSTMT hstmt;   // Statement Handle  
   SQLHDESC hdesc;   // Descriptor handle  
   unsigned char szData[MAX_DATA];   // Returned Data Storage  
   SDWORD cbData;   // Output Lenght of data  
   unsigned char char_ds_name[SQL_MAX_DSN_LENGTH];   // Data Source Name  
  
   SQL_DATE_STRUCT date;   // date structure  
   SQL_SS_TIME2_STRUCT time2;   // time2 structure  
   SQL_TIMESTAMP_STRUCT datetime2;   // datetime2 structure  
   SQL_SS_TIMESTAMPOFFSET_STRUCT dateTimeOffset;   // datetimeoffset structure  
  
   SQLLEN cbdate;   // size of date structure  
   SQLLEN cbtime2;   // size of time structure  
   SQLLEN cbdatetime2;   // size of datetime2  
   SQLLEN cbtimestampoffset;   //size of dateTimeOffset  
  
public:  
   direxec();   // Constructor  
   void sqlconn();   // Allocate env, stat and conn  
  
   void sqldisconn();   // Free pointers to env, stat, conn and disconnect  
   void error_out();   // Display errors  
   void check_rc(RETCODE rc);   // Checks for success of the return code  
  
   void sqlinsert();   // Insert into the table  
};  
  
// Constructor initializes the string char_ds_name with the data source name and  
// initialize the data structures to with the date to be inserted.  
direxec::direxec() {  
   _mbscpy_s(char_ds_name, (const unsigned char *)"DateTime");  
  
   // Initialize the date structure  
   date.day = 12;  
   date.month = 10;  
   date.year = 2001;  
  
   // Initialize the time structure  
   time2.hour = 21;  
   time2.minute = 45;  
   time2.second = 52;  
   time2.fraction = 100  ;  
  
   // Initialize the datetime2 structure  
   datetime2.year = 2007;  
   datetime2.month = 12;  
   datetime2.day = 26;  
   datetime2.hour = 0;  
   datetime2.minute = 0;  
   datetime2.second = 0;  
   datetime2.fraction = 100;   
  
   // Initialize the timestampoffset structure  
   dateTimeOffset.year = 2007;  
   dateTimeOffset.month = 3;  
   dateTimeOffset.day = 11;  
   dateTimeOffset.hour = 2;  
   dateTimeOffset.minute = 30;  
   dateTimeOffset.second = 29;  
   dateTimeOffset.fraction = 200;  
   dateTimeOffset.timezone_hour = -8;  
   dateTimeOffset.timezone_minute = 0;  
  
   // Size of structures   
   cbdate = sizeof(SQL_DATE_STRUCT);  
   cbtime2 = sizeof(SQL_SS_TIME2_STRUCT);  
   cbdatetime2 = sizeof(SQL_TIMESTAMP_STRUCT);  
   cbtimestampoffset = sizeof(SQL_SS_TIMESTAMPOFFSET_STRUCT);  
  
}   // direxec  
  
// Allocate environment handles, connection handle, connect to data source, and allocate statement handle  
void direxec::sqlconn() {  
   // Allocate the enviroment handle  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   check_rc(rc);  
  
   // Set the ODBC version to version 3  
   rc = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   check_rc(rc);  
  
   // Allocate the database connection handle  
   rc = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   check_rc(rc);  
  
   // Connect to the database  
   rc = SQLConnect(hdbc, char_ds_name, SQL_NTS, NULL, 0, NULL, 0);  
   check_rc(rc);  
  
   // Allocate the statement handle  
   rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
   check_rc(rc);    
  
   // Allocate the descriptor handle  
   rc = rc = SQLAllocHandle(SQL_HANDLE_DESC, hdbc, &hdesc);  
   check_rc(rc);  
  
}   // direxec::sqlconn  
  
// Display error message from the DiagRecord  
void direxec::error_out() {  
   // String to hold the SQL State  
   unsigned char szSQLSTATE[10];  
  
   // Error code  
   SDWORD nErr;  
  
   // The error message  
   unsigned char msg[SQL_MAX_MESSAGE_LENGTH + 1];  
  
   // Size of the message  
   SWORD cbmsg;  
  
   // If hstmt is not null use that for getting the DiagRec  
   if (hstmt)  
      rc = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
   // else get the diag record from the env  
   else  
      rc = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
  
   // If the rc is successful, show the message using a message box  
   if ( rc == SQL_SUCCESS) {  
      char hold_err[100];  
      _itoa_s(nErr, hold_err, 100, 10);  
      _snprintf_s((char *)szData, MAX_DATA, MAX_DATA - 1, "%s" "%s" "%s" "%s" "%s" "%s" "%s" "%s",   
        "Error:", "\n", "SQLSTATE= ", szSQLSTATE, ", Native error=", hold_err, ", msg = ", msg);  
      MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
   }  
}   // direxec::error_out  
  
// Checks the return code.  If failure, displays the error, free the memory and exits the program  
void direxec::check_rc(RETCODE rc) {  
   if (!MYSQLSUCCESS(rc)) {  
      error_out();  
      SQLFreeEnv(henv);  
      SQLFreeConnect(hdbc);  
      exit(-1);  
   }   
}   // direxec::check_rc  
  
// Function to insert dates into the table.  
void direxec::sqlinsert() {     
   rc = SQLPrepare(hstmt, (SQLCHAR *) "INSERT INTO DateTimeTypes (datecol, time2col, datetime2col, datetimeoffsetcol) VALUES (?, ?, ?, ?)", SQL_NTS);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, &date, 0, &cbdate);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_SS_TIME2, 16, 7, &time2, 0, &cbtime2);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TIMESTAMP, SQL_TYPE_TIMESTAMP, 27, 7, &datetime2, 0, &cbdatetime2);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_SS_TIMESTAMPOFFSET, 34, 7, &dateTimeOffset, 0, &cbtimestampoffset);  
   check_rc(rc);  
  
   rc = SQLExecute(hstmt);  
   check_rc(rc);  
}   // direxec::sqlinsert  
  
int main() {  
   direxec x;  
  
   // Allocate handles, and connect.  
   x.sqlconn();   
  
   // Insert all into the table  
   x.sqlinsert();  
}  
```  
  
```  
USE tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'DateTimeTypes')  
DROP TABLE DateTimeTypes  
GO  
```  
  
  