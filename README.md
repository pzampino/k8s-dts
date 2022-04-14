# k8s-dts
Getting and using HDFS delegation tokens from Kubernetes job containers with Apache Knox

## HDFS Delegation Tokens
Kerberos users can use the WEBHDFS API to get a Hadoop Delegation Token from the NameNode service.

(e.g., kinit’d as systest)
curl --negotiate -u: "http://HOST:20101/webhdfs/v1/?op=GETDELEGATIONTOKEN"

`{
  "Token":
  {
    "urlString":"IgAHc3lzdGVzdAdzeXN0ZXN0AIoBcwV2oHyKAXMpgyR8HwQU3F03Ce4LNg45X9Vz_YV-n5Y9ZXoSV0VCSERGU
yBkZWxlZ2F0aW9uEzE3Mi4zMS4xMTIuMTI5OjgwMjA"
  }
}
`


## Knox [HD]FS Token Service
A new Knox service (like the KnoxToken Service) that can request HDFS delegation tokens from the NameNode on behalf of the calling user. If implemented more generically, this service could be a general-purpose Hadoop FileSystem delegation token provider, satisfying requests for a variety of FS types (e.g., hdfs, s3a, abfs, etc…)

This service could be responsible for renewal and cancellation of these delegation tokens, doing something similar to what YARN does with Delegation Tokens.


[Knox HDFS Token Service source](https://github.com/pzampino/knox/tree/k8s-dt-poc)

