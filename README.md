# Cloud Operating System Image Recommendations for NRENs and other Scientific Service Providers

October 2017

Authors: Kalle Happonen, Oscar Kraemer, Saverio Proto, Stig Telfer

This document will updated regularly and be kept up to date with the operating system versions.

This document has been discussed in the following forums (not officially endorsed yet): Géant SIG-CISS, NeIC Glenna2 project  

## Background and Reasoning

Cloud Operating System Image management in NRENs and other scientific service providers is currently in an incoherent state. This both duplicates effort and fragments the different platforms from the end user point of view.

This document recommends a set way of handling operating system images. The recommendations are based on using unmodified upstream cloud images from the operating system vendors. The benefits of this approach includes

To cloud service providers

 * The scientific service providers approach matches that of many other cloud providers.
 * This reduces the work for the service providers.
 * With a common large use base, the problems are common, and fixed together.
 * A large use base with one voice has a larger change of affecting the upstream image providers in case of problems.
 * Easier to provide and trust virtual appliances.

To cloud users

 * Standard experience for cloud providers, e.g. naming, image availability.
 * Images are on the same level, so same code works against all the providers.
 * Better availability and compatibility of virtual appliances.

There are naturally drawbacks to this approach, including possible lack of tooling for doing timely fixes when problems in upstream images occur. The option to do site-specific optimizations for the images are also lost. Each service provider has to weigh the pros and cons of this approach in their own case.

## General image management rules

All images are updated at least once a month to ensure that the included software is up to date.

When an updated image is added, it's recommended that the old image is hidden, if possible. In recent enough OpenStack versions this can be done by marking the image visibility to "community". In case this is not possible, images can also be marked "private", but this reduces the usefulness of the older images. It is recommended that no images are deleted if there still are virtual machines based on them.

The image format (QCOW/RAW) can be chosen freely based on the best fit for the installation.

## Mandatory images
If you adhere to these guidelines the following images must exist on your installation.

Image | Recommended name | Image source
--- | --- | ---
CentOS 7  | CentOS-7 | https://cloud.centos.org/centos/7/images/
Ubuntu 14.04 | Ubuntu-14.04 | https://cloud-images.ubuntu.com/trusty/
Ubuntu 16.04 | Ubuntu-16.04 | https://cloud-images.ubuntu.com/xenial/

## Optional images
If the following images are used, these are the recommended names and sources

Image | Recommended name | Image source
--- | --- | ---
CentOS 6 | CentOS-6 | https://cloud.centos.org/centos/6/images/
CoreOS | CoreOS | https://stable.release.core-os.net/amd64-usr/current
Debian 9 | Debian-9 | https://cdimage.debian.org/cdimage/openstack/
Fedora 26 | Fedora-26 | https://cloud.fedoraproject.org/
Fedora Atomic 26 | Atomic-26 | https://getfedora.org/en/atomic/download/
Ubuntu 17.04 | Ubuntu-17.04 | https://cloud-images.ubuntu.com/zesty/

## Virtual machine appliances
For this to benefit users and providers more, these policies can be extended to virtual machine appliances. These are in place to enable easy sharing of these appliances. To adhere to these policies an appliance must

 * be based on one of the base images mentioned above.
 * adhere to the same security policies as the base image. Namely no extra users with password logins. Only ssh key authentication with the OS default account.
 * be automatically buildable. Some tools that can be used are are disk-image-builder or packer.io. The code to build these must be publicly accessible.
 * be in qcow format, not raw format for space reasons. Conversion can be done at import time.
 * be accessible via an URL provided by the person/organization responsible for the image.
 * be updated at least once a month.

These rules only consider virtual machine appliances that are meant to be shared. Service providers may provide any site specific virtual machine appliances they see fit.

## Available virtual machine appliances
Recommended name | Base Image | Description | Build source | Image source
--- | --- | --- | --- | --- 
CentOS-7-CUDA | CentOS 7 | CentOS 7 with newest CUDA packages | https:// | https://
Ubuntu-16.04-CUDA | Ubuntu 16.04 | Ubuntu 16.04 with newest CUDA packages | https:// | https://

## Additional images
The service provider may provide any additional images they see fit.

## Tooling
This section contains links to tools. Not all tools are usable out of the box, and not all tools adhere to these recommendations.

Organization | Adheres to these recommendations | URL
---|---|---
SWITCH | | https://github.com/switch-ch/SWITCHengines-image-builder

