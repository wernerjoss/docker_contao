# 4.9-manager
The file docker-compose.yml provided here is mainly for the purpose of developing a contao Site locally.  
As stated in the comments, the locally mapped volumes ./contao_data/files and ./contao_data/templates
provide a convenient way to access these from your favourite IDE, but note that they MUST NOT be activated
before the complete contao Installation.    
After that, stop your docker instances with `docker-compose down`, edit docker-compose.yml (uncomment volumes)
and restart: `docker-compose up -d`  
As already mentioned, the locally mapped volumes are mainly useful for those who use this Image for website development, anyone who has other priorities (e.g. Contao Plugin development) should of course map other/additional Directories.  
As of 04/2021 this is especially true as now Xdebug has been incorporated in the Image, thus making it far easier to develop and debug Plugins.
There is now also included a Launch configuration for VS Code (see Folder .vscode) which turns this into a full featured IDE for PHP development, see e.g.
[this](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) description.
