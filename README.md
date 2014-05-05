# Oracle Java

## Overview
Due the Oracle Java policy, new distribution of the linux are not shipped
with their java virtual machine implementation. This playbook will install
the oracle java vm from the tar.gz file.

You need to download the files form oracle site manually and put them on your own http/ftp server.

## Requirements

Any server comaptible with the module get_url.
Tested on ansoble version 1.5.4, but older releases shoud by fine.

## Role Variables

### Distribution specific

N/A

### Global 

The `java_download_prefix` url to http/ftp server.

The most important variable is `java_list`, where you can specify one or more java version for each architecture. The 

- **filename** path relative to the `java_download_prefix`.
- **dirname** is direcory created when the tar.gz is extracetrd
- **alternative_priority** is debian specific, command _update-alternatives_

`java_vesrion` is the version of the java to be installed.

`java_extra_files` is the list of the files to be installed. It could be extra libs or JCE policy or ... The *src* is relative to the `java_download_prefix`, **dest** is reative to the `java_install_dir` and **filename** value for the jaa version in the `java_list`.

### Example

    java_list:
      v1.7.45:
        'i386':
          filename: 'oracle-java/jdk-7u45-linux-i586.tar.gz'
           dirname: 'jdk1.7.0_45'
           alternative_priority: 1745
         'x86_64':
           filename: 'oracle-java/server-jre-7u45-linux-x64.tar.gz'
           dirname: 'jdk1.7.0_45'
           alternative_priority: 1745
    java_version: v1.7.45
    java_install_dir: /opt/oracle_java
    java_download_prefix: http://download.acme.org/java

    java_extra_files:
      - src: log4j/logging-log4j-1.2.9/dist/lib/log4j-1.2.9.jar
        dest: jre/lib/ext
        state: enabled

License
-------

BSD

Author Information
------------------

Peter Hudec
