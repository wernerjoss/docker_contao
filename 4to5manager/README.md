# 4.13-manager
The file docker-compose.yml provided here is mainly for the purpose of developing a contao Site locally.  
As stated in the comments, the locally mapped volumes ./contao_data/files and ./contao_data/templates
provide a convenient way to access these from your favourite IDE, but note that they MUST NOT be activated
before the complete contao Installation.    
After that, stop your docker instances with `docker-compose down`, edit docker-compose.yml (uncomment volumes)
and restart: `docker-compose up -d`  
As already mentioned, the locally mapped volumes are mainly useful for those who use this Image for website development, anyone who has other priorities (e.g. Contao Plugin development) should of course map other/additional Directories.  
