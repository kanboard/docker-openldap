OpenLDAP test images for Kanboard
=================================

Docker images to test Kanboard automatically.

There are two kind of configuration:

- OpenLDAP configured with memberUid
- OpenLDAP configured with the overlay memberOf

Authors and License
-------------------

- Frédéric Guillot
- MIT License

Users and Groups
----------------

### Groups

- `cn=Kanboard Admins,ou=Groups,dc=kanboard,dc=local`
- `cn=Kanboard Managers,ou=Groups,dc=kanboard,dc=local`
- `cn=Kanboard Users,ou=Groups,dc=kanboard,dc=local`

### Users

- `uid=user,ou=Users,dc=kanboard,dc=local`
- `uid=manager,ou=Users,dc=kanboard,dc=local`
- `uid=superuser,ou=Users,dc=kanboard,dc=local`

### Credentials

- `cn=admin,DC=kanboard,DC=local`
- All passwords are `password`

Docker images
-------------

- `kanboard/openldap:memberUid` (port 3389)
- `kanboard/openldap:memberOf` (port 4389)
