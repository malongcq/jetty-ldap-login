#simple configuration example

1. Edit ldap-login.conf and put it into [jetty-home]/etc/<br>
_ldap-login.conf example:_<br>
*ldap* <br>
{
    org.eclipse.jetty.plus.jaas.spi.SimpleLdapLoginModule required<br>
    ldapURL="ldap://10.10.10.10:389"<br>
    bindDn="uid=admin,ou=admin_groups,dc=example,dc=com"<br>
    bindPassword="xxx"<br>
    userBaseDn="ou=people,dc=example,dc=com"<br>
    userId="uid"<br>
    userPassword="userPassword"<br>
    userObjectClass="inetOrgPerson"<br>
    userRoleName="app"<br>
    roleUserId="uid"<br>
    roleBaseDn="ou=role_group,dc=example,dc=com"<br>
    roleName="cn"<br>
    roleMember="uniqueMember"<br>
    roleObjectClass="groupOfUniqueNames";
};<br>

2. Edit [jetty-home]/etc/jetty-jaas.xml, add following lines:<br>

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
