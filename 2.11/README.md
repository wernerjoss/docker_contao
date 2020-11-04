## This is for old Contao 2.11, no longer available in the contao.org repository

see corresponding Dockerfile, which pulls contao tarball from here.  

## how to use:
1. build image contao-2.11 from Dockerfile: docker build -t contao-2.11:latest .
2. for a fresh Install, comment all lines under volumes: except tl_files, then start docker (docker-compose up -d)
3. proceed with usual procedure, using http://localhost/contao/install.php, note that localconfig.php is already populated, install PW=contaoadm
4. accept License, create administrator account, log into Backend, have fun :)

Note that with this procedure, you end up with a contao 2.11 core installation, no plugins, no theme whatsoever.  
if you want to have your consequent work to be persistent, you will have to add entries to the volumes: section depending on what you install/configure.  
everything that resides in the database, will be persistent as this is kept in your local ./mysql-data folder.  
the same holds for all (uploaded or edited) files under ./tl_files.  
but, be aware, that with this setup, consequently installed contao extensions via the Backend, will NOT persist, the same is true for templates !  
in order to make these persistent, too, be sure to:  
copy directorys inside docker that have changed (templates, system/modules) to your local contao_data folder, e.g.
docker cp contao2:/var/www/html/templates ./contao_data  
once done, you can stop docker, edit docker-compose.yml, uncommenting the corresponding entry under volumes:  
then, upon docker restart, you will have your latest changes in templates in place.  

Additional note for those who want to move an existing Project to docker:  
just copy the folders tl_files, templates and system/modules to your local ./contao_data folder and uncomment the corresponding lines in docker-compose.yml.  
then import the database from the Project into the docher mysql instance, e.g. via http://localhost:8888  
then start docker and all should be there.
