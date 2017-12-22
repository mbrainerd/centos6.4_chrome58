# centos6.4_chrome58

This is my own side project, a modification of a script provided freely by Richard K. Lloyd so most credit goes to him, and is in no way supported so use at your own risk. This script allows you to build Google Chrome 58 for CentOS 6.4.

#### You will need root access on your local host and internet access to do the install.
1. First you will need to install an updated version of the nss libs
    1. `cd <repo>/nss`
    2. `sudo yum install *.rpm`
2. Then you can install Chrome
    1. `cd <repo>/google-chrome`
    2. `sudo ./install_chrome.sh --rpm google-chrome-stable-58.0.3029.110-1.x86_64.rpm`
        * This will, by default, install chrome to /opt/google/chrome-local
3. Running chrome-local
    1. `/opt/google/chrome-local/google-chrome --no-sandbox`
        * The --no-sandbox flag is required as chrome hardcodes the reference to the old /opt/google/chrome/chrome-sandbox location, which is not compatible
4. If google-chrome fails to run, try running this:
    1. `sudo /opt/google/chrome-local/modify_wrapper`
        * It should get run as part of the install process, but sometimes it doesn't
5. Update your launch/desktop icon to use the command described in step 3
6. Profit

As a note, this script does not modify/uninstall the old version of Chrome that is installed via yum at /opt/google/chrome, so that version should continue to be functional. It also does not use yum to install the new version of Chrome (though it does use yum to install a custom rpm it creates called chrome-deps-stable), so if you want to uninstall it the best option is to use `install_chrome.sh -u`. Lastly, Chrome 58 is the last version of Chrome that has any chance of running on CentOS 6 as 59+ uses GTK3, which isn't available until CentOS 7, so I would not recommend attempting using this script with a newer rpm.

Best of luck!
