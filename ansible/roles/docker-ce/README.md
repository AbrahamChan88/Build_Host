## docker-ce Role
This role is a very simple installation of docker-ce (ce meaning community edition). It handles both Debian and RHEL derivatives. This is detected automatically via fact gathering.

### Description
Just installs the specified version of docker community edition

### When will I invoke this role?
Any time you need to install docker.

### Dependencies
This role is standalone

### Contents
* Install docker depenendencies for the detected platform
* Add docker stable repo
* Install latest stable version of docker-ce
* lay down and enable docker systemd unit

### Parameters
* {{ docker_version }} - docker version | expects version number like "17.09.0"
* {{ docker_log_level }} - docker log level | expects string like "error"
* {{ docker_storage_driver }} - docker storage driver | expects string like "overlay"
