# docker-lam
docker for ldap-account-manager

# Usage 

### start ldap server 
```
docker run -d --restart=always \
-p 389:389 -p 636:636 \
--privileged=true \
--name openldap \
-e DOMAIN="Jermine.com" \
-e ORGANIZATION="Vdo.Pub" \
-e PASSWORD=123456 \
-v ~/ldap/etc:/etc/ldap \
-v ~/ldap/data:/var/lib/ldap \
-v ~/ldap/ssl:/ssl \
-v ~/ldap/backups:/var/backups \
-v ~/ldap/restore:/var/restore \
jermine/openldap
```

### start ldap client

```
docker run -d --restart unless-stopped \
-p 1001:80 \
--name lam \
--link openldap:ldap  \
-e LAM_LANG="zh_CN" \
-e LAM_PASSWORD="passwdxxx" \
-e LAM_TIMEZONE="Asia/Shanghai" \
-e LDAP_DOMAIN="com" \
-e LDAP_PASSWORD="passwdxxx" \
-e LDAP_BASE_DN="ou=dev,dc=sample,dc=com" \
-e LDAP_USER="cn=admin,dc=com" \
jermine/lam
```

