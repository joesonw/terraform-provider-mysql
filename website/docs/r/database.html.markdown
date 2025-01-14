---
layout: "mysql"
page_title: "MySQL: mysql_database"
sidebar_current: "docs-mysql-resource-database"
description: |-
  Creates and manages a database on a MySQL server.
---

# mysql\_database

The ``mysql_database`` resource creates and manages a database on a MySQL
server.

## Example Usage

```hcl
resource "mysql_database" "app" {
  name = "my_awesome_app"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the database. This must be unique within
  a given MySQL server and may or may not be case-sensitive depending on
  the operating system on which the MySQL server is running.

* `default_character_set` - (Optional) The default character set to use when
  a table is created without specifying an explicit character set. Defaults
  to "utf8".

* `default_collation` - (Optional) The default collation to use when a table
  is created without specifying an explicit collation. Defaults to
  ``utf8_general_ci``. Each character set has its own set of collations, so
  changing the character set requires also changing the collation.

Note that the defaults for character set and collation above do not respect
any defaults set on the MySQL server, so that the configuration can be set
appropriately even though this provider cannot see the server-level defaults. If
you wish to use the server's defaults you must consult the server's
configuration and then set the ``default_character_set`` and
``default_collation`` to match.

## Attributes Reference

The following attributes are exported:

* `name` - The name of the database.
* `id` - The id of the database.
* `default_character_set` - The default_character_set of the database.
* `default_collation` - The default_collation of the database.

## Import

Databases can be imported using their name, e.g.

```
$ terraform import mysql_database.example my-example-database
```
