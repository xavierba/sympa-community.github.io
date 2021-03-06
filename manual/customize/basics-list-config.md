---
title: 'Configuration for each list'
prev: basics-configuration.md
up: ../customize.md#customization-basics
next: basics-templates.md
---

Configuration for each list
===========================

A list has a directory of its own.  Most of configuration files and
control files specific to the list is placed there.
List also has several other directories to provide extensive features.

Directories
-----------

Following directories may be used so that a list will work.
"List directory" must be created at the time of
[list creation](../admin/list-creation.md#list-creation).
The others will be created as their necessities.

  * List directory

    Directory which contains configuration specific to a list (see also
    [below](#configuration-files-under-list-directory)).

    Default location is
    [``$EXPLDIR``](../layout.md#expldir)`/`_mail domain_`/`_list name_`/`.

    ----
    Note:

      * Exceptionally, [``$EXPLDIR``](../layout.md#expldir)`/`_list name_`/`
        is also allowed for primary mail domain (mail domain defined by
        `domain` parameter in [``sympa.conf``](../man/sympa.conf.5.md)).
        However, full path described above is recommended for new
        installation.

    ----

  * Bounce directory

    Base directory of bounce and tracking information (see also
    "[Bounce management](../customize/bounce-management.md)").

    Default location is
    [``$BOUNCEDIR``](../layout.md#bouncedir)`/`_list name_`@`_mail domain_`/`.

  * Archive directory

    Base directory of list archives (see also
    "~~[Archives](../customize/archives.md)~~").

    Default location is
    [``$ARCDIR``](../layout.md#arcdir)`/`_list name_`@`_mail domain_`/`.

  * Pictures directory

    Directory for subscribers' pictures.

    Default location is
    [``$PICTURESDIR``](../layout.md#picturesdir)`/`_list name_`@`_mail domain_`/`.

  * Shared document repository

    Base directory of Shared document repository (see also
    "~~[Shared document repository](../customize/shared-repository.md)~~").

    Location is the subdirectory named `shared/` under list directory
    described above.

Configuration files under list directory
----------------------------------------

There may be following configuration files under list directory.
Among them, `config` file is required.
The others may be created during list creation, or configuration works by
listmasters or owners.

### `config`

The file which keeps most of list configuration.
See also
"[Configuration files](basics-configuration.md#configuration-files)"
in "Configuration hierarchy".
See [`list_config(5)`](../man/list_config.5.md) for details of format and
configuration parameters.

### `info` file and `homepage` file

  * `info`

    Long description of the list.
    Content of this file will be included in welcome message
    (`mail_tt2/welcome.tt2`) sent to new subscribers
    or response to `INFO` ~~[mail command](../mail-commands.md)~~.

    This file contains the text entered as "Description" in list creation page
    of web interface.

  * `homepage`

    Content of this file will be included in list information page of
    web interface.  HTML format is allowed.
    If it does not exist, content of `info` file will be used.

### Message header and footer

  * `message.footer`
  * `message.footer.mime`

    If either of these files exists, it will be appended at end of
    distributed messages (see also
    [`footer_type`](../man/list_config.5.md#footer_type) parameter).

  * `message.header`
  * `message.header.mime`

    Similar to files above, but they will be appended at beginning of
    distributed messages.

### Templates

Mail templates (_list directory_`/mail_tt2/`_file name_`.tt2`)
and web templates (_list directory_`/web_tt2/`_file name_`.tt2`)
for specific list may customize templates.
See also "[Templates](basics-templates.md)".

### Tasks

List task files (_list directory_`/`_file name_`.task`)
for specific list may customize data source definitions.
See also "[Data sources](basics-tasks.md)".

### Data inclusion files

Data inclusion files (_list directory_`/data_sources/`_file name_`.incl`)
for specific list may customize data source definitions.
See also "[Data sources](../customize/data-sources.md)".

Control files
-------------

### Dump files

----
Note:

  * Feature of dump files was introduced on Sympa 6.2.33b.1.

----

(Work in progress)

### `stats`

`stats` file under list directory contains accumulated amount of message
delivery.  It contains following four integer numbers separated by space
characters:

  1. Number of messages the list has distributed.
     This number is assigned as value of `list.sequence` template variable
     used with [`custom_subject`](../man/list_config.5.md#custom_subject)
     parameter.
  2. Total number of messages the list has distributed.
  3. Sum of message sizes the list has distributed.
  4. Total sum of message sizes the list has distributed.

----
Note:

  * In general, this file should not be modified manually.

  * This file on earlier versions of Sympa might contain additional
    information.  Format of this file may be changed in the future.

----

### `msg_count`

----
Note:

  * This file should not be modified manually.

----

`msg_count` file under list directory contains number of messages distributed
by days.  Its content will be imported in database, and shown in
"List statistics" page of web interface.

### `config_changes`

----
Note:

  * This file should not be modified manually.

----

`config_changes` file under list directory tracks modification of list
configuration by users, if the list belongs to family.

(Work in progress)

Deprecated files
----------------

  * _list directory_`/subscribers`

    On Sympa prior to 5.4, this file retained subscriber information.
    Recently, information of subscribers are solely stored in database,
    and this file has been deprecated.

