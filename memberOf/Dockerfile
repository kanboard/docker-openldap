FROM ubuntu:14.04

RUN apt-get update && \
    echo "slapd slapd/root_password password password" |debconf-set-selections && \
    echo "slapd slapd/root_password_again password password" |debconf-set-selections && \
    echo "slapd slapd/internal/adminpw password password" |debconf-set-selections && \
    echo "slapd slapd/internal/generated_adminpw password password" |debconf-set-selections && \
    echo "slapd slapd/password2 password password" |debconf-set-selections && \
    echo "slapd slapd/password1 password password" |debconf-set-selections && \
    echo "slapd slapd/domain string kanboard.local" |debconf-set-selections && \
    echo "slapd shared/organization string Kanboard" |debconf-set-selections && \
    echo "slapd slapd/backend string HDB" |debconf-set-selections && \
    echo "slapd slapd/purge_database boolean true" |debconf-set-selections && \
    echo "slapd slapd/move_old_database boolean true" |debconf-set-selections && \
    echo "slapd slapd/allow_ldap_v2 boolean false" |debconf-set-selections && \
    echo "slapd slapd/no_configuration boolean false" |debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y slapd ldap-utils

ADD config/*.ldif /tmp/

RUN mkdir -p /var/ldap/kanboard \
    && chown -R openldap /var/ldap \
    && service slapd start \
    && ldapadd -Y EXTERNAL -H ldapi:/// -f /tmp/memberof.ldif \
    && ldapadd -H ldapi:/// -f /tmp/ou.ldif -x -D "cn=admin,dc=kanboard,dc=local" -w password \
    && ldapadd -H ldapi:/// -f /tmp/users.ldif -x -D "cn=admin,dc=kanboard,dc=local" -w password \
    && ldapadd -H ldapi:/// -f /tmp/groups.ldif -x -D "cn=admin,dc=kanboard,dc=local" -w password \
    && rm /tmp/*.ldif

EXPOSE 389

CMD slapd -h 'ldap:///' -g openldap -u openldap -d 0
