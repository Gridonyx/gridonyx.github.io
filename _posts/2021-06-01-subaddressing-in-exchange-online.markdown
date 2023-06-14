---
layout: post
title:  "Enabling Subaddressing in Exchange Online"
date:   2021-06-01 14:15:00 -0400
categories: microsoft365 powershell
---
Subaddressing, also known as plus addressing, is a feature which allows an individual to append a tag to their email address by following this format: email+tag@domain.com. This allows a user to create as many unique email addresses as they would like, while still receiving them to their single inbox. This comes in handy when you want to filter through emails, as you could use a unique tag for every website, or use more general tags like "+shopping" or "+entertainment". 

Microsoft has added this capability to Exchange Online as of September of 2020. While it is not enabled for organizations by default (UPDATE: As of May 2022 this is [enabled by default in new organizations](https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/plus-addressing-in-exchange-online)) , nor can you enable it in the Admin Center, you may enable it using the Exchange Online PowerShell Cmdlets, which I will breakdown the installation and use of below.

## How to Enable

The first step is to install the Exchange Online module on your workstation.
You may do so by opening PowerShell as an administrator and running the following command:
{% highlight powershell %}
Install-Module -Name ExchangeOnlineManagement
{% endhighlight %}

Note, you may get an error message about PowerShellGet, generally this just means the excution policy setting on your workstation is not allowing the install to run due to it being from a non-local source. You can  get around this by running the following, then running the above command again:
{% highlight powershell %}
Set-ExecutionPolicy Unrestricted
{% endhighlight %}

After the install has completed, you must import the module into PowerShell, like so:
{% highlight powershell %}
Import-Module ExchangeOnlineManagement
{% endhighlight %}

Then you must connect to your organization, where `user@email.com` is an account with appropriate role assignments in your tenant:
{% highlight powershell %}
Connect-ExchangeOnline -UserPrincipalName user@email.com
{% endhighlight %}

Then run the following to enable the subaddress option:
{% highlight powershell %}
Set-OrganizationConfig -AllowPlusAddressInRecipients $true
{% endhighlight %}

If all is well, you may then disconnect using:
{% highlight powershell %}
Disconnect-ExchangeOnline
{% endhighlight %}

I recommend setting the execution policy back to the default of Restricted when you're done:
{% highlight powershell %}
Set-ExecutionPolicy Restricted
{% endhighlight %}

That's all there is to it, the change takes effect immediately so you can begin enjoying the ability to use subaddresses.


### Update
As of May 2022, you may now also enable this through the Exchange Online Admin Center:

- Navigate to the new Exchange admin center at [https://admin.exchange.microsoft.com](https://admin.exchange.microsoft.com)
- Click on **Settings**
- Click on **Mail flow**
- Uncheck *Turn off plus addressing for your organization*
- Click **Save**
