# jetty-ldap-login
an alternative LDAP login module for jetty

#simple configuration example

1. Edit ldap-login.conf and put it into [jetty-home]/etc/
ldap-login.conf example:
ldap 
{

org.eclipse.jetty.plus.jaas.spi.SimpleLdapLoginModule? required
ldapURL="ldap://10.10.10.10:389"
bindDn="uid=admin,ou=admin_groups,dc=example,dc=com"
bindPassword="xxx"
userBaseDn="ou=people,dc=example,dc=com"
userId="uid"
userPassword="userPassword"
userObjectClass="inetOrgPerson"
userRoleName="app"
roleUserId="uid"
roleBaseDn="ou=role_group,dc=example,dc=com"
roleName="cn"
roleMember="uniqueMember"
roleObjectClass="groupOfUniqueNames";
};
2. Edit [jetty-home]/etc/jetty-jaas.xml, add following lines:
<call class="java.lang.System" name="setProperty">
<arg>
java.security.auth.login.config
</arg>
<arg>
<systemproperty name="jetty.home" default=".">
</systemproperty>
/etc/login.conf
</arg>
</call>
<call name="addBean">
<arg>
<new class="org.eclipse.jetty.plus.jaas.JAASLoginService">
<set name="Name">
LDAP
</set>
<set name="LoginModuleName">
ldap
</set>
</new>
</arg>
</call>
