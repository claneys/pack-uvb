pack-uvb
=========

Unitrend Virtual Backup checks for Shinken. You'll need to use booster-nrpe 
module. Install it with :

::

  shinken install uvb

Then load it in poller cfg file.

You need to activate nrpe server on UVB appliance following this page :
https://phdtechsupport.zendesk.com/hc/en-us/articles/202532530-Using-Nagios-with-UVB

And add the following line into /etc/nagios/nrpe.cfg
to monitor job status :

::

  command[check_ntp]=/usr/lib/nagios/plugins/check_ntp_time -w 0.128 -c 0.5 -H ntp
  command[check_disks]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -R "/dev/[hs]d[a-z][0-9]"
  command[check_joblog]=/usr/lib/nagios/plugins/check_log -F /var/log/phdvb/job.log -O /tmp/old.job.log -q "items_with_error"

Then restart nrpe server : 
sudo /etc/init.d/nagios-nrpe-server restart
