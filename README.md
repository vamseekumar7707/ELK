# ELK  
https://sematext.com/guides/elk-stack/
https://sysadminxpert.com/steps-to-install-and-configure-filebeat-on-linux/
https://www.javainuse.com/elasticsearch/filebeat-elk
https://www.elastic.co/guide/en/elasticsearch/reference/master/ingest.html
https://discuss.elastic.co/t/network-host-0-0-0-0-is-not-working-in-elasticsearch-7-3-0/195697
https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-ubuntu-20-04
https://www.youtube.com/watch?v=MRMgd6E9AXE
https://phoenixnap.com/kb/how-to-install-elk-stack-on-ubuntu
https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-ubuntu-20-04
https://www.elastic.co/guide/en/logstash/current/installing-logstash.html
https://www.elastic.co/guide/en/logstash/current/use-ingest-pipelines.html
https://meet.google.com/linkredirect?authuser=0&dest=https%3A%2F%2Fwww.elastic.co%2Fguide%2Fen%2Flogstash%2Fcurrent%2Flogstash-config-for-filebeat-modules.html%23parsing-nginx

input {
beats {
  port => "5044"
  ssl  => false
 # host => "10.0.0.91"
}
}
output {
elasticsearch {
  hosts => ["10.0.0.75:9200"]
  manage_template => false
  index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
}
}


https://discuss.elastic.co/t/not-able-to-see-filebeat-index-pattern-in-kibana/127072

https://stackoverflow.com/questions/58742845/multiple-filebeat-to-one-logstash-how-to-optimize-the-configuration

https://discuss.elastic.co/t/multiple-filebeat-inputs-with-logstash-output/146343

https://docs.axway.com/bundle/EmbeddedAnalyticsAPIM_allOS_en_HTML5/page/install_and_configure_filebeat.html

https://stackoverflow.com/questions/51984622/how-to-write-a-multiple-input-and-logstash-filter-for-hostname-based-on-message











###NAGIOS MONITORING         
	https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/quickstart.html
  http://www.fosteringlinux.com/2011/12/get-started-with-nagios-nrp/
  https://youtu.be/7KxVSK9yP-Y
   
##### BackEnd Host ##########


## Default
define host{
           use                             linux-box
           host_name                       Remote-BackEnd          ; The name we're giving to this ser>
           alias                           CentOS 6                ; A longer name for the server
           address                         10.0.0.226              ; IP address of Remote Linux host
}
#services  
define service{
        use                     generic-service
        host_name               Remote-BackEnd
        service_description     Total Processes
        check_command           check_nrpe!check_total_procs
        }

define service{
        use                     generic-service
        host_name               Remote-BackEnd
        service_description     Current Users
        check_command           check_nrpe!check_users
        }

define service{
        use                     generic-service
        host_name               Remote-BackEnd
        service_description     SSH Monitoring
        check_command           check_nrpe!check_ssh
        }

define service{
        use                     generic-service
        host_name               Remote-BackEnd
        service_description     FTP Monitoring
        check_command           check_nrpe!check_ftp
 }
define service {

    use                     generic-service           ; Name of service template to use
    host_name               Remote-BackEnd
    service_description     Disk-load
    check_command           check_nrpe!check_hda1
}
define service{
        use                     generic-service
        host_name               Remote-BackEnd
        service_description     Zombie-process
        check_command           check_nrpe!check_zombie_procs
        }
 
 
 
 
