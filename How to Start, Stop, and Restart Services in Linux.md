原文地址：https://www.tecmint.com/systemd-service-commands/



# How to Start, Stop, and Restart Services in Linux



If you’re new to [Linux](https://www.tecmint.com/what-is-linux/), understanding how to manage services is an essential skill. Services are [processes that run in the background](https://www.tecmint.com/12-top-command-examples-in-linux/) to provide various functions, such as web servers, databases, or network services.

As a Linux user with over a decade of experience, I can assure you that [mastering the commands](https://www.tecmint.com/essential-linux-commands/) to start, stop, and restart services will make your experience smoother.

This article will guide you through the basics so that you can start, stop, or restart services depending on what you need.

## Why Do You Need to Start, Stop, or Restart Services?

- **Starting a Service**: You may need to start a service after installing software or when the system boots up without automatically starting certain services.
- **Stopping a Service**: Stopping a service can free up system resources or prevent unwanted programs from running.
- **Restarting a Service**: If a service is malfunctioning or after making configuration changes, restarting is often the quickest way to resolve issues.

## Key Commands for Managing Services

In Linux, the most common way to manage services is through the `systemd` system, which controls services on [modern Linux distributions](https://www.tecmint.com/top-most-popular-linux-distributions/).

The basic commands are:

### 1. Start a Service in Linux



To start a service, use the following command:

```
sudo systemctl start apache2
```

This command starts the **Apache** web server. If the service is not running, it will begin.

### 2. Stop a Service in Linux

To stop a running service, you can use the command:

```
sudo systemctl stop apache2
```

This will stop the Apache web server. If it’s already stopped, the command does nothing.

### 3. Restart a Service in Linux

If a service needs to be restarted (for example, after a configuration change), use:

```
sudo systemctl restart apache2
```

This will stop the Apache service and immediately start it again, which is useful for applying new configuration changes.

### 4. Checking the Status of a Service

You can also check the status of a service to see if it is running properly.

```
sudo systemctl status apache2
```

<iframe id="google_ads_iframe_/15184186,18758028/tecmint_incontent_dynamic_0" name="google_ads_iframe_/15184186,18758028/tecmint_incontent_dynamic_0" title="3rd party ad content" width="1" height="1" scrolling="no" marginwidth="0" marginheight="0" frameborder="0" aria-label="Advertisement" tabindex="0" data-load-complete="true" data-google-container-id="8" style="box-sizing: inherit; margin: 0px; padding: 0px; border: 0px; max-width: 100%; vertical-align: bottom;"></iframe>

This will display information about the Apache service, including whether it is active (running), inactive, or failed.

## Enabling and Disabling Services in Linux

By default, some services are set to start automatically when your system boots. If you want to make sure a service starts automatically (or stops starting automatically), you can enable or disable it:

```
sudo systemctl enable apache2
sudo systemctl disable apache2
```

##### Conclusion

Now that you know how to start, stop, and restart services in Linux, you’re well-equipped to [manage essential services](https://www.tecmint.com/chkconfig-vs-systemctl/) on your system.

These commands are fundamental to ensuring your services run smoothly, whether you’re setting up a web server or troubleshooting issues. Keep [practicing these commands](https://www.tecmint.com/most-used-linux-commands/), and soon they’ll feel like second nature.

If you’re new to Linux, take your time and explore the [systemctl command](https://www.tecmint.com/manage-services-using-systemd-and-systemctl-in-linux/). It’s a powerful tool that makes service management easier than ever.
