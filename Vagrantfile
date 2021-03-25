##################################################################################
#TBZ - M300 LB2 
#
#Author:            Shanuyaan Thangavadviel
#Project:           Display current date and time + processes in website
#Creation Date:     19.03.2021<
#Description:       Simple webserver with vagrant                               
#                   template (from github.com/mc-b/M300).                       
#                   Creates a BASH-Script which displays                        
#                   current date and time and processes.                        
#                   Creates a automated cronjob for script execution            
#                   every 2 minutes.                                           
#                   Site is available at localhost:8080/enjoyit
################################################################################

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "myhost.enjoyit"
  config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
  config.vm.synced_folder ".", "/var/www/html"
config.vm.provider "virtualbox" do |vb|
  vb.memory = "2048"  
end
config.vm.provision "shell", inline: <<-SHELL
  # Packages vom lokalen Server holen
  # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
  sudo apt-get update
  sudo apt-get -y install apache2
  cd / 
  mkdir bashscripts
  cd bashscripts
  #Create script to write current date and time, processes to textfile
  touch dateproc.sh
  echo "env TZ=CET-1 date > /var/www/html/enjoyit" > dateproc.sh
  echo "ps aux >> /var/www/html/enjoyit" >> dateproc.sh
  chmod +x /bashscripts/dateproc.sh
  # Initial execution of script
  ./dateproc.sh
  # Create automated execution for up-to-date data
  crontab -l | {  cat; echo "*/2 * * * * /bashscripts/dateproc.sh"; } | crontab -
SHELL
end