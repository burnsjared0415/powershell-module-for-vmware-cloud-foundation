# New-VCFvRSLCM

### Synopsis
The New-VCFvRSLCM cmdlet deploys vRealize Suite Lifecycle Manager

### Syntax
```
New-VCFvRSLCM -json <path to json file> -validate
```

### Description
The New-VCFvRSLCM cmdlet deploys vRealize Suite Lifecycle Manager based on a JSON spec. Supports VLAN or Application Virtual Network based deployments.

### Examples
#### Example 1
```
New-VCFvRSLCM -json .\SampleJson\vRealize\New-VCFvRSLCM-AVN.json 
```
This example deploys vRealize Suite Lifecycle Manager using a supplied json file

#### Example 2
```
New-VCFvRSLCM -json .\SampleJson\vRealize\New-VCFvRSLCM-AVN.json -validate
```
This example performs a validation of vRealize Suite Lifecycle Manager using a supplied json file


### Parameters
#### -json
- Path to the JSON spec

```yaml
Type: JSON
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
```

### Sample VLAN JSON
```
{
    "apiPassword": "VMw@re1!",
    "fqdn": "vrslcmsrv01.rainpole.io",
    "networkSpec": {
        "gateway": "172.16.225.1",
        "subnetMask": "255.255.255.0",
        "vlanId": "2225"
    },
    "sshPassword": "VMw@re1!"
}
```

### Sample Application Virtual Network JSON
```
{
    "apiPassword": "VMw@re1!",
    "fqdn": "xreg-vrslcm01.rainpole.io",
    "sshPassword": "VMw@re1!"
}
```

### Related Links
