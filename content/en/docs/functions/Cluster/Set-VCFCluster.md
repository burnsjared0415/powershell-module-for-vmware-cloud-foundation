---
title: "Set-VCFCluster"
weight: 5
description: >
    Expands, compacts or marks a cluster for deletion for a Workload Domain
---

## Syntax
``` powershell
Set-VCFCluster -id <string> -json <json_file> -markForDeletion <boolean>
```

### Parameters

| Required | Parameter       | Type     |  Description                                                                |
| ---------| ----------------|----------| --------------------------------------------------------------------------- |
| required | id              | String   | Specifies the unique ID of the cluster                                      | 
| optional | json            | String   | Specifies the JSON specification file to be used                            |
| optional | markForDeletion | Switch   | Specifies a switch to mark the cluster for deletion                         |


## Examples
### Example 1
``` powershell
Set-VCFCluster -id a511b625-8eb8-417e-85f0-5b47ebb4c0f1 -json .\Cluster\clusterExpansionSpec.json
```
Expand a cluster by adding a host(s)

### Example 2
``` powershell
Set-VCFCluster -id a511b625-8eb8-417e-85f0-5b47ebb4c0f1 -json .\Cluster\clusterCompactionSpec.json
```
Compact a cluster by removing a host(s)

### Example 3
``` powershell
Set-VCFCluster -id a511b625-8eb8-417e-85f0-5b47ebb4c0f1 -markForDeletion
```
Marks a cluster for deletion

## Sample JSON
### Add an NSX-V Cluster Multi pNIC
``` json
{
  "nsxVClusterSpec": {
    "vdsNameForVxlanConfig": "w01-c02-vds02",
    "vlanId": 0
  },
  "hostSpec": {
    "hostSystemSpec": [
      {
        "license": "AAAAA-AAAAA-AAAAA-AAAAA-AAAAA",
        "id": "c2398611-23cd-4b94-b2e3-9d84848b73cb",
        "vmnicToVdsNameMap": {
             "vmnic0": "w01-c02-vds01",
             "vmnic1": "w01-c02-vds01",
             "vmnic2": "w01-c02-vds02",
             "vmnic3": "w01-c02-vds02"
            }
      },
      {
        "license": "AAAAA-AAAAA-AAAAA-AAAAA-AAAAA",
        "id": "8dbe7dcb-f409-4ccd-984b-711e70e9e767",
        "vmnicToVdsNameMap": {
             "vmnic0": "w01-c02-vds01",
             "vmnic1": "w01-c02-vds01",
             "vmnic2": "w01-c02-vds02",
             "vmnic3": "w01-c02-vds02"
            }
      },
      {
        "license": "AAAAA-AAAAA-AAAAA-AAAAA-AAAAA",
        "id": "e9ba66e0-4670-4973-bdb1-bc05702ca91a",
        "vmnicToVdsNameMap": {
             "vmnic0": "w01-c02-vds01",
             "vmnic1": "w01-c02-vds01",
             "vmnic2": "w01-c02-vds02",
             "vmnic3": "w01-c02-vds02"
            }
      }
    ]
  },
  "clusterName": "c02",
  "highAvailabilitySpec": {
    "enabled": true
  },
  "domainId": "983840c1-fa13-4edd-b3cb-907a95c29652",
  "datastoreSpec": {
    "vsanDatastoreSpec": {
      "license": "BBBBB-BBBBB-BBBBB-BBBBB-BBBBB",
      "ftt": 1,
      "name": "w01-c02-vsan01"
    }
  },
  "vdsSpec": [
    {
      "name": "w01-c02-vds01",
      "portGroupSpec": [
        {
          "name": "w01-c02-vds01-management",
          "transportType": "MANAGEMENT"
        },
        {
          "name": "w01-c02-vds01-vmotion",
          "transportType": "VMOTION"
        },
        {
          "name": "w01-c02-vds01-vsan",
          "transportType": "VSAN"
        }
      ]
    },
    {
       "name": "w01-c02-vds02",
       "portGroupSpec": [
        {
          "name": "w01-c02-vds02-ext",
          "transportType": "PUBLIC"
        }
        ]
    }
  ]
}
```

### Add a host(s) to a cluster
``` json
{
  "clusterExpansionSpec" : {
    "hostSpecs" : [ {
      "id" : "edc4f372-aab5-4906-b6d8-9b96d3113304"
    } ]
  }
}
```

### Add a multi pNIC host(s) to a cluster
``` json
{
  "clusterExpansionSpec" : {
    "hostSpecs" : [ {
      "id" : "1d539f62-d85a-48a3-b5db-a165e06ae6ba",
      "license": "AAAAA-AAAAA-AAAAA-AAAAA-AAAAA",
      "hostNetworkSpec" : {
        "vmNics" : [ {
          "id" : "vmnic0",
          "vdsName" : "SDDC2-Dswitch-Private1"
        }, {
          "id" : "vmnic1",
          "vdsName" : "SDDC2-Dswitch-Private1"
        }, {
          "id" : "vmnic2",
          "vdsName" : "SDDC2-Dswitch-Private2"
        }, {
          "id" : "vmnic3",
          "vdsName" : "SDDC2-Dswitch-Private2"
        } ]
      }
    } ]
  }
}
```

### Remove a host from a cluster
``` json
{
  "clusterCompactionSpec" : {
    "hosts" : [ {
      "id" : "edc4f372-aab5-4906-b6d8-9b96d3113304"
    } ]
  }
}
```