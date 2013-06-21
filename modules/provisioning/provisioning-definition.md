---
layout: modules-provisioning
title: Creating The Provisioning Definition
prev: '<a href="../../modules/provisioning/index.html">Prev: The Provisioning Module</a>'
next: '<a href="../../modules/provisioning/useProvisioningEngine.html">Next: useProvisioningEngine()</a>'
---

# Creating The Provisioning Definition

Before you can use a provisioning engine, you need to create a _provisioning definition_.  This contains information about what you want the engine to do to your host(s).

__Note__: none of these actions make any changes to your hosts.  Your hosts are only changed when you use a provisioning engine to apply your completed definition.

## Step 1: Create An Empty Provisioning Definition

This step is very straight-forward, and it creates an empty definition to work with.

{% highlight php %}
$def = $st->usingProvisioning()->createDefinition();
{% endhighlight %}

## Step 2: Add Roles To The Provisioning Definition

Provisioning engines such as [Ansible](http://ansible.cc/), [Chef](http://www.opscode.com/chef/) and [Puppet](https://puppetlabs.com/) support the concept of _roles_, where a role is something that a host can do (e.g. be a webserver).  Hosts can have multiple roles.

{% highlight php %}
$st->usingProvisioningDefinition($def)->addRole($roleName)->toHost($hostName);
{% endhighlight %}

where:

* _$def_ is the _provisioning definition_ created in Step 1
* _$roleName_ is the name of a role to add to a host (this must be a role that you've added to your chosen provisioning engine)
* _$hostName_ is the name of the host you want to add the role to (this is normally the same name that you've passed into _$st->usingVagrant()->createBox())

## Step 3: Add Parameters To The Provisioning Definition

Provisioning engines normally used some form of _parameterised instructions_, which allow you to inject variables into the rules and templated config files at deployment time.

{% highlight php %}
$st->usingProvisioningDefinition($def)->addParams($params)->toHost($hostName);
{% endhighlight php %}

where:

* _$def_ is the _provisioning definition_ created in Step 1
* _$params_ is an array listing the variable names and values to use when the provisioning engine runs against _$hostName_
* _$hostName_ is the name of the host you want to add the role to (this is normally the same name that you've passed into _$st->usingVagrant()->createBox())

## Next Step

Once you've build your provisioning definition, your next step is to [use a provisioning engine](useProvisioningEngine.html) to apply the definition to your hosts.