---
layout: post
title:  "Enabling Subaddressing in Exchange Online"
date:   2021-06-01 14:15:00 -0400
categories: powershell office365
---
Subaddressing, also known as plus addressing, is a feature which allows an individual to append a tag to their email address by following this format: email+tag@domain.com. This allows a user to create as many unique email addresses as they would like, while still receiving them to their single inbox. This comes in handy when you want to filter through emails, as you could use a unique tag for every website, or use more general tags like "+shopping" or "+entertainment". 

Microsoft has added this capability to Exchange Online as of September of 2020, and while it is not enabled for organizations by default nor can you enable it in the Admin Center. You can only enable it using the Exchange Online PowerShell Cmdlets, which I will breakdown the installation and use of below.

## How to Enable

The first step is to install the Exchange Online module on your workstation, you may do so by opening PowerShell and running the following command:
{% highlight powershell %}
Install-Module -Name ExchangeOnlineManagement
{% endhighlight %}

Note, you may get an error message about PowerShellGet, generally this just means the policy setting on your workstation is not allowing the command to run, you can temporarily get around this by running the following, then running the above command again:
{% highlight powershell %}
Set-ExecutionPolicy Unrestricted
{% endhighlight %}

After the install has completed, you must import the module, like so:
{% highlight powershell %}
Import-Module ExchangeOnlineManagement
{% endhighlight %}

Next, you must connect to your organization:
{% highlight powershell %}
Connect-ExchangeOnline -UserPrincipleName user@email.com
{% endhighlight %}

Then run the following:
{% highlight powershell %}
Set-OrganizationConfig -AllowPlusAddressInRecipients $true
{% endhighlight %}

Then if all is well, be sure to disconnect using:
{% highlight powershell %}
Disconnect-ExchangeOnline
{% endhighlight %}

That's all there is to it, the change takes effect immediately so you can begin enjoying the ability to use subaddresses.