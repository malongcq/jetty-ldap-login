###simple configuration example

* 1. Edit ldap-login.conf and put it into [jetty-home]/etc/
* ldap-login.conf example:
```
ldap
{
    org.eclipse.jetty.plus.jaas.spi.SimpleLdapLoginModule required
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
```
* 2. Edit [jetty-home]/etc/jetty-jaas.xml, add following lines:
```
<Call class="java.lang.System" name="setProperty">
 <Arg>java.security.auth.login.config</Arg>
 <Arg><SystemProperty name="jetty.home" default="."/>/etc/login.conf</Arg>
</Call>
    
<Call name="addBean">
 <Arg>
    <New class="org.eclipse.jetty.plus.jaas.JAASLoginService">
      <Set name="Name">LDAP</Set>
      <Set name="LoginModuleName">*ldap*</Set>
    </New>
 </Arg>
</Call>
```
