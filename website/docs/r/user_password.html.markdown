---
layout: "mysql"
page_title: "MySQL: mysql_user_password"
sidebar_current: "docs-mysql-resource-user-password"
description: |-
  Creates and manages the password for a user on a MySQL server.
---
# mysql_user_password

The `mysql_user_password` resource sets and manages a password for a given 
user on a MySQL server.

~> **NOTE on MySQL Passwords:** This resource conflicts with the `password` 
   argument for `mysql_user`. This resource uses PGP encryption to avoid 
   storing unencrypted passwords in the provider state.
   
~> **NOTE on How Passwords are Created:** This resource **automatically**
   generates a **random** password. The password will be a random UUID.

## Example Usage

 ```hcl
resource "mysql_user" "jdoe" {
  user = "jdoe"
}

resource "mysql_user_password" "jdoe" {
  user    = "${mysql_user.jdoe.user}"
  pgp_key = "keybase:joestump"
}
```

## Argument Reference
The following arguments are supported:

* `user` - (Required) The IAM user to associate with this access key.
* `pgp_key` - (Required) Either a base-64 encoded PGP public key, or a keybase username in the form `keybase:some_person_that_exists`.
* `host` - (Optional) The source host of the user. Defaults to `localhost`.

## Attributes Reference

The following additional attributes are exported:

* `key_fingerprint` - The fingerprint of the PGP key used to encrypt the password 
* `encrypted_password` - The encrypted password, base64 encoded.

~> **NOTE:** The encrypted password may be decrypted using the command line,
   for example:  `output | base64 --decode | keybase pgp decrypt`.
