Active Directory LDAP Authentication
=========

Laravel 5 Active Directory LDAP Authentication driver.

Fork
====

This is a fork of Manuel Strebel's Package, which is a fork of Cody Covey's ldap-auth package. Manuel Strebel has kindly updated the package to support
Laravel 5. This fork will simply add the ability to authenticated against LDAP without the needed for persistent storage of user accounts in
a database.

Contribution
------------
Just post an issue or create a pull request on this repository. I'll really appreciate it.

Installation
============

Laravel 5
---------
To install this package add the following to your composer.json

```json
require {
	"TwinLakes/ldap-auth": "~2.0",
}
```

Then run

`composer install` or `composer update` as appropriate

Open `config/app.php` and find

`Illuminate\Auth\AuthServiceProvider`

and replace it with

`TwinLakes\LdapAuth\LdapAuthServiceProvider`

This tells Laravel 5 to use the service provider from the vendor folder.

You also need to direct Auth to use the ldap driver instead of Eloquent or Database, edit `config/auth.php` and change driver to `ldap`


Configuration
=============
To specify the username field to be used in `config/auth.php` set a key / value pair `'username_field' => 'fieldname'` This will default to `username` if you don't provide one.

To set up your adLDAP for connections to your domain controller, create a file config/adldap.php This will provide all the configuration values for your connection. For all configuration options an array like the one below should be provided.

It is important to note that the only required options are `account_suffix`, `base_dn`, and `domain_controllers`The others provide either security or more information. If you don't want to use the others simply delete them.

```php
return array(
	'account_suffix' => "@domain.local",

	'domain_controllers' => array("dc1.domain.local", "dc2.domain.local"), // An array of domains may be provided for load balancing.

	'base_dn' => 'DC=domain,DC=local',

	'admin_username' => 'user',

	'admin_password' => 'password',

	'real_primary_group' => true, // Returns the primary group (an educated guess).

	'use_ssl' => true, // If TLS is true this MUST be false.

	'use_tls' => false, // If SSL is true this MUST be false.

	'recursive_groups' => true,
);
```