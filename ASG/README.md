## Autoscale Groups Stylebooks

Autoscale Groups Stylebooks are stylebooks that are applied on a
Citrix ADM instance that has at least one autoscale groups configured.

Details of how to setup the Autoscale Group feature can be found
[here](https://docs.citrix.com/en-us/citrix-application-delivery-management-service/hybrid-multi-cloud-deployments/autoscale-for-aws/autoscale-for-aws-configuration.html)

Stylebooks are the last stage of the configuration setup described in
the previous document and is the topic of this README file and relevant
stylebooks found here.

## Autoscale group stylebooks vs regular stylebooks

### Deployment

First point of difference for a ASG stylebook vs a regular
stylebook is how they are applied.

Regular stylebooks are applied from the menu item
Applications -> Stylebooks.

ASG stylebooks instead are applied from the menu 
Network -> AutoScale Groups, and then selecting an already
created Autoscale Group and selection the option `Configure`


### Configuration actions

The second and most important point of difference is what configuration
actions take place.

A regular stylebook is pretty transparent to the author. Whatever configuration
is defined that is what will be applied to the Citrix ADC instance.

ASG stylebooks on the other hand have some additional configuration that is applied
to the Citrix ADC instance as well as some configuration that happens in AWS services.

The best way to introduce the differences is to show the parameters that are required
as input for any ASG stylebook.


```yaml
--- 
name: autoscale-params
namespace: com.citrix.adc.commontypes
version: "1.0"
description: "This StyleBook defines the parameters required for Autoscale Deployment."
display-name: "Autoscale Parmeters StyleBook"
private: true
type: autoscale
schema-version: "1.0"
parameters:
  
  - 
    name: app_name
    label: "Application Name"
    description: "Name of the Application"
    type: string
    key: true
    gui:
      updatable: false
    required: true
  
  -
    name: ip_address
    label: "IP Address of the LoadBalancer"
    description: "IP Address of the LoadBalancer"
    type: ipaddress
    gui:
        hidden: true
          
  -
    name: domain_name
    label: "Name for the domain"
    description: "Name for the domain"
    type: string
    required: true
    gui:
      updatable: false
    
  -
    name: zone_name
    label: "Zone of the domain"
    description: "Zone of the domain"
    type: string   
    required: true
    gui:
      updatable: false
      
  -
    name: ipset
    label: "IPSet"
    description: "Configuration for network ipset resource"
    type: string
    gui:
        hidden: true
```

#### `app_name` 
is used as an id string used for various ADC and AWS
configuration entities created.

At the very least it is used to name the ipset created in the ADC and
also some Route53 and NLB entities.


#### `ip_address`
is used for the address of the created lb vserver or cs vserver.

Note that this is a hidden parameter so the user does not input
the value. It is provided by the ASG code.

#### `domain_name`
is the domain for the application. Usually this is the top level
domain name

#### `zone_name`
is the rest of the domain name that will through Route53 and NLB
will point to our created lb or cs vserver.

For example if we wanted to have an application publisized to
the internet under `myapp.test.com` `test.com` would be the domain name
and `myapp` would be the zone name.

#### `ipset`
is an ipset that is created by the ASG code in the target ADC.
It is attached to the created lb or cs vserver to have them respond
to these ips as requests come in routed by our NLB.


Notice that the values for ipset and ip\_address are provided as input to
the ASG stylebook. These are the values which the author of the stylebook
must use as an entry point to the configuration that will be applied.

Conceptually any stylebook that has these input variables can be used as
an ASG stylebook. The checks that happen are that the input variables exist
and at least one type of vserver is created.

From then on one could for example configure WAF rules that are totally
unrelated with the ASG setup done so far.

It is therefore logical to only deploy ASG stylebooks that have a vserver entry
point ( cs or lb vserver ) which will receive traffic routed by the AWS entities' setup.

A typical tie in between an lb vserver and ASG configuration is the following.

```yaml
components:
  - 
    name: lbvserver-comp
    type: ns::lbvserver
    properties: 
      ipv46: $parameters.ip_address
      ipset: $parameters.ipset
```

From then on whatever configuration is related to the lb vserver should comprise
the rest of the stylebook.

For regular stylebooks that need to be applied to the whole cluster
going through Applications -> Stylebooks and selecting the cluster ip as target
is enough.

The only other point of difference is that an ASG stylebook should have
the following top level property defined.

```yaml
type: "autoscale"
```

This is needed so that the stylebook is available under the Autoscale
Groups configuration and not under regular stylebooks.

Seeing one of the stylebooks in this [directory ](./stylebooks)
should give you an insight for the structure your stylebook should follow.
