# docker_contao
Dockerfiles for Contao-Installations coming along with sample configuration files for the docker composer.

These are derived from Holger Janßen-Kroll's [Contao Docker Repo](https://github.com/hojak/docker_contao) which seem to be abandoned (somehow) - at least they are not adapted to current contao 4.x needs.

If not mentioned otherwise, the images require a mysql database somewhere reachbale via network. In the docker-compose.yml files I use the standard mysql:5.7 image of the docker library (mysql:8.0 for contao 4.13).

Building and running follows the general rules for Docker Images, however, this is not always clear to novice / casual users, so I will explain here step by step what to do:

1. build and tag an image from the provided Dockerfile:
cd to the directory where the Dockerfile resides, e.g. 4.9-manager and then do  
`docker build -t contao4.9:latest .`
2. save the generated image:  
`docker image save contao4.9:latest -o contao4.9.tar`  
this will save the generated image to the file contao4.9.tar - you can then load this later without having to re-build in case you deleted it in the meantime.
3. now you are ready to start - enjoy :smile:

The easiest way to do this is to use the provided file docker-compose.yml with just running:  
`docker-compose up -d`

After starting the image, the installation of contao has to be completed via the standard installation tool. In the 4.9-manager variant, the manager has to be called on the address http://localhost:80/contao-manager.phar.php as mentioned in the installation manual of the contao menager.

Currently available are the following version / tags:

- 4.13-manager: manager installation variant of the 4.13 contao release
- 4.9-manager: manager installation variant of the 4.9 contao release - note you can no more install 4.4 LTS, the latest contained contao-manager will prevent this !  
- 3.5.40: this is the last Contao 3.5 Version, with PHP 7.2 on Debian Buster  
- 2.11: old Contao 2.11.17, PHP 5.4/Mysql 5.5, Debian jessie, for legacy Projects
