pack-uvb
=========

Unitrend Virtual Backup checks for Shinken
You need to activate nrpe server on UVB appliance
following this page :
https://phdtechsupport.zendesk.com/hc/en-us/articles/202532530-Using-Nagios-with-UVB

And add the following line into /etc/nagios/nrpe.cfg
to monitor job status :
command[check_joblog]=/usr/lib/nagios/plugins/check_log -F /var/log/phdvb/job.log -O /tmp/old.job.log -q "items_with_error"

Then restart nrpe server : 
sudo /etc/init.d/nagios-nrpe-server restart
