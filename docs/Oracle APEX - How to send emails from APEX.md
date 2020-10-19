# How to send Email from Oracle APEX 

* Oracle OCI Reference Doc [https://docs.cloud.oracle.com/en-us/iaas/Content/Email/Reference/apex.htm]
* Dimitri Gielis Blog [http://dgielis.blogspot.com/2019/10/free-oracle-cloud-11-sending-emails.html]

> Note: If is not required to use email delivery service from same Oracle OCI tenancy. It can be from any `Oracle OCI Account`

```SQL
BEGIN
	APEX_INSTANCE_ADMIN.SET_PARAMETER('SMTP_HOST_ADDRESS', 'smtp.us-ashburn-1.oraclecloud.com');
	APEX_INSTANCE_ADMIN.SET_PARAMETER('SMTP_USERNAME', 'ocid1.user.oc1..yy7qg22uxsxuz4tthie5mzecmngqhq.nb.com');
	APEX_INSTANCE_ADMIN.SET_PARAMETER('SMTP_PASSWORD', 'C3b+qeZ>0HCd');
	COMMIT;
END;
/

```
```SQL
BEGIN
	APEX_MAIL.SEND(p_from => 'true.no.reply@oraclecloud.com',
		       p_to   => 'ravinder_sayal@harvard.edu',
		       p_subj => 'Fujitsu-TRUE Login Code',
	               p_body => 'Sent using APEX_MAIL pn 08/16');
END;
/			
```
