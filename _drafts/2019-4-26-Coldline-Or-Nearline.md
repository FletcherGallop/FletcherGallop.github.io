---
layout: post
title: "Coldline or Nearline: Knowing Which to Use and When"
---

_What to look for in your use-cases to know which GCP Storage options suits best. Helpful for GCP Cloud Engineer Exam Prep._

# What is GCP Cloud Storage

In the world of Cloud there are many different providors offering similar services, same basic foundations, but different names. 

Anyone from the AWS world would perhaps view Cloud Storage as S3 or Simple Storage Service equivalent.

Anyone from Azure will know it as something a kin to Blob Storage Service. 

It is essentialy flat file, or object based storage in the cloud. Typically used to store documents, videos, images, and other static content. The respective services are often used to host static content for websites.


## What Are My Options?

- Multi-Regional
- Regional
- Nearline
- Coldline

| Class          | Use-Cases                  | Price (per GB/month)* |
| :---           | :---                       | :---:                 |
| Multi-regional | Frequent and Global Access | $0.026                | 
| Regional       | Frequently used in one region, ie, where GCP resources are | $0.020 |
| Nearline       | Accessed no more than once a month. Back-ups | $0.010 |
| Coldline       | Accessed no more than once a year. Archive or Disaster Recovery | $0.007 |

* Pricing accurate as of April 2019. Likely to change.

## Knowing What to Pick

There are three or so criteria to look for when deciding which Cloud Storage option to use:

- Access Volume
- Cost Effectiveness
- Lifecycling

### Example Use Case Scenario 

`
You currently have 850TB of Closed-Circuit Television (CCTV) capture data and are adding new data at a rate of 80TB/month. The rate of data captured and needing to be stored is expected to grow to 200TB/month within one year because new locations are being added, each with 4-10 cameras. Archival data must be stored indefinitely, and as inexpensively as possible. The users of your system currently need to access 250TB of current-month footage and 100GB of archival footage, and access rates are expected to grow linearly with data volume.
`

<span style="background-color: #FFFF00">Marked text</span>


_Feel free to message me at @fletchergallop on Twitter for any questions or comments! - Thanks!_

## Read More

[GCP Docs - Storage Classes](https://cloud.google.com/storage/docs/storage-classes)
[GCP Docs - Lifecycle](https://cloud.google.com/storage/docs/lifecycle)
[GCP Docs - Archival](https://cloud.google.com/storage/archival/)