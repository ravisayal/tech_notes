# How to send email from Oracle Database using PLSQL

> Note: That this requires to setting up Network ACL rules in Database, these are are in addtion to OS or networking ACLs
> This does not work in Oracle OCI Autonomous Database Database for ATP Database, users need to use Email Delivery Service.

> PLSQL procedure to send email

``` sql
drop PROCEDURE testmail;

create or replace procedure  testmail
(
  fromm varchar2,
  too   varchar2,
  sub   varchar2,
  body  varchar2,
  port  number
)
is
objConnection utl_smtp.connection;
vrData varchar2(32000);
username varchar2(30) := 'ravi.aws.20@gmail.com';
password varchar2(20) := 'India47@gl';
begin
  objConnection := utl_smtp.open_connection('smtp.gmail.com',port);
  utl_smtp.helo(objConnection, 'oracloud.com');
  utl_smtp.command(objConnection, 'AUTH LOGIN');
  utl_smtp.command(objConnection,utl_raw.cast_to_varchar2(utl_encode.base64_encode(utl_raw.cast_to_raw(username))));
  utl_smtp.command(objConnection,utl_raw.cast_to_varchar2(utl_encode.base64_encode(utl_raw.cast_to_raw(password))));
  utl_smtp.mail(objConnection, fromm);
  utl_smtp.rcpt(objConnection, too);
  utl_smtp.open_data(objConnection);
  /*** Sending the header information */
  utl_smtp.write_data(objConnection, 'From: '||fromm || utl_tcp.crlf);
  utl_smtp.write_data(objConnection, 'To: '||too || utl_tcp.crlf);

  utl_smtp.write_data(objConnection, 'Subject: ' || sub || utl_tcp.crlf);
  utl_smtp.write_data(objConnection, 'MIME-Version: ' || '1.0' || utl_tcp.crlf);
  utl_smtp.write_data(objConnection, 'Content-Type: ' || 'text/html;');

  utl_smtp.write_data(objConnection, 'Content-Transfer-Encoding: ' || '"8Bit"' ||utl_tcp.crlf);
  utl_smtp.write_data(objConnection,utl_tcp.crlf);
  utl_smtp.write_data(objConnection,utl_tcp.crlf||'<HTML>');
  utl_smtp.write_data(objConnection,utl_tcp.crlf||'<BODY>');
  utl_smtp.write_data(objConnection,utl_tcp.crlf||'<FONT COLOR="red" FACE="Courier New">'||body||'</FONT>');
  utl_smtp.write_data(objConnection,utl_tcp.crlf||'</BODY>');
  utl_smtp.write_data(objConnection,utl_tcp.crlf||'</HTML>');
  utl_smtp.close_data(objConnection);
  utl_smtp.quit(objConnection);
exception
  when utl_smtp.transient_error OR utl_smtp.permanent_error then
    utl_smtp.quit(objConnection);
    dbms_output.put_line(sqlerrm);
  when others then
    utl_smtp.quit(objConnection);
    dbms_output.put_line(sqlerrm);
end testmail;
/
```

> PLSQL snippet to send email

``` sql
declare
vdate Varchar2(25);
begin
  vdate := to_char(sysdate,'dd-mon-yyyy HH:MI:SS AM');
  testmail('true.no.reply@oraclecloud.com', 'ravinder_sayal@g.harvard.edu', 'Oracle Email','This is a UTL_SMTP-generated email at '|| vdate,25);
end;
/
```
