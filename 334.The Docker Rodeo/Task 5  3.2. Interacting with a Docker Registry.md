As with any system that we are going to be penetration testing, we need to enumerate the services running to understand any potential entry points. In our case, **Docker Registry runs on port 5000 by default**, however, this can be easily changed, so it is worth confirming via with a nmap scan like so: `sudo nmap -sV 10.10.13.105`

![](https://i.imgur.com/rz4orgs.png)  

Not only is Nmap capable of discovering the Docker Registry, but also the API version - this is important to note for how we will interact with it.

The Docker Registry is a JSON endpoint, so we cannot just simply interact with it like we would a normal website - we will have to query it. Whilst this can be done via the terminal or browser, dedicated tools such as [Postman](https://www.postman.com/downloads/) or [Insomnia](https://insomnia.rest/download/) are much better suited for the job. I will be using Postman in this room.

To understand what routes are available to us, we need to read the [Docker Registry Documentation](https://docs.docker.com/registry/spec/api/). Please take the time to read this at your leisure.

3.2.1. Discovering Repositories 

We need to send a `GET` request to `http://docker-rodeo.thm:5000/v2/_catalog` to list all the repositories registered on the registry.

![](https://resources.cmnatic.co.uk/TryHackMe/rooms/docker-rodeo/dockerregistry/catalog1.png)

In this example, we're given a response of three repositories. For now, we are only going to focus on "cmnatic/myapp1".

Before we can begin analysing a repository, we need two key pieces of information: 

1. The repository name

2. Any repository tag(s) published

We currently have the repository name (**cmnatic/myapp1**) now we just need to list all tags that have been published. Every repository will have a minimum of one tag. This tag is the "**latest**" tag, but there can be many tags, all with different code, for example, major software versions or two tags for "**production**" and "**development**".

Send a `GET` request to`http://docker-rodeo.thm:5000/v2/**repository/name**/tags/list` to query all published tags. For our application, our request would look like so: `http://docker-rodeo.thm:5000/v2/**cmnatic**/**myapp1**/tags/list`:

![](https://resources.cmnatic.co.uk/TryHackMe/rooms/docker-rodeo/dockerregistry/listingtags.png)  

Note here we have three tags? That **"notsecure"** tag sure sounds interesting. We now have both pieces of information to retrieve the manifest files of the image for analysis.

3.2.2. Grabbing the Data!  

With these two important pieces of information about a repository known, we can enumerate that specific repository for a manifest file. This manifest file contains various pieces of information about the application, such as size, layers and other information. I'm going to grab the manifest file for the **"notsecure"** tag via the following `GET`request: `http://docker-rodeo.thm:5000/v2/**cmnatic/myapp1**/manifests/**notsecure**`

Note the response - specifically the "**history**" key;  albeit slightly hard to read, we have a command that was executed during the image building stage stored in plaintext (``echo \\\"here's a flag\\\" \\u003e /root/root.txt\"]` `` ). In this image, it's a string insert into **/root/root.txt** on the container. Although imagine if this was a password!

![](https://resources.cmnatic.co.uk/TryHackMe/rooms/docker-rodeo/dockerregistry/manifest1.png)  

3.2.3. Now it's Your Turn...

Apply what we have done above, enumerate the 2nd Docker registry running on the Instance, find out what repositories are stored within it and ultimately extract some credentials for a database.

Answer the questions below

What is the port number of the 2nd Docker registry?

	 7000

What is the name of the repository within this registry?  

	 securesolutions/webserver

What is the name of the tag that has been published?  

	 production

What is the Username in the database configuration?  

	 admin

What is the Password in the database configuration?

	production_admin

```shell
Starting Nmap 7.80 ( https://nmap.org ) at 2022-03-28 20:28 CDT
Nmap scan report for 10.10.13.105
Host is up (0.21s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
5000/tcp open  http    Docker Registry (API: 2.0)
7000/tcp open  http    Docker Registry (API: 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 46.09 seconds
```

```shell
curl http://docker-rodeo.thm:5000/v2/_catalog

{"repositories":["cmnatic/myapp1","dive/challenge","dive/example"]}
```

```shell
curl http://docker-rodeo.thm:5000/v2/_catalog

{"repositories":["cmnatic/myapp1","dive/challenge","dive/example"]}
```

```shell
curl http://10.10.13.105:7000/v2/_catalog
{"repositories":["securesolutions/webserver"]}
```

```shell
curl http://10.10.13.105:7000/v2/securesolutions/webserver/tags/list

{"name":"securesolutions/webserver","tags":["production"]}
```

```shell
curl http://10.10.13.105:7000/v2/securesolutions/webserver/manifests/production

{
   "schemaVersion": 1,
   "name": "securesolutions/webserver",
   "tag": "production",
   "architecture": "amd64",
   "fsLayers": [
      {
         "blobSum": "sha256:7a668bba7a1a84d9db8a2fb2826f777e64233780a110041db8d42b797515cf57"
      },
      {
         "blobSum": "sha256:bc4544ab6267aaf520480ea4cc98e3169d252eab631801ef199b1ded807f306d"
      },
      {
         "blobSum": "sha256:07813898d5e66ad253cf5bb594a47c6963a75412ee3562d212d3bc1e896ad62f"
      },
      {
         "blobSum": "sha256:fdbb44f75d5b29f06c779f6eec33e886d165053275497583a150c9c2b444f3af"
      },
      {
         "blobSum": "sha256:a3ed95caeb02ffe68cdd9fd84406680ae93d633cb16422d00e8a7c22955b46d4"
      },
      {
         "blobSum": "sha256:bb79b6b2107fea8e8a47133a660b78e3a546998fcf0427be39ac9a0af4a97e90"
      }
   ],
   "history": [
      {
         "v1Compatibility": "{\"architecture\":\"amd64\",\"config\":{\"Hostname\":\"\",\"Domainname\":\"\",\"User\":\"\",\"AttachStdin\":false,\"AttachStdout\":false,\"AttachStderr\":false,\"Tty\":false,\"OpenStdin\":false,\"StdinOnce\":false,\"Env\":[\"PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin\"],\"Cmd\":[\"bash\"],\"ArgsEscaped\":true,\"Image\":\"sha256:1e4a2d11384ed8ac500f2762825c3f3d134ad5d78813a5d044357b66d4c91800\",\"Volumes\":null,\"WorkingDir\":\"\",\"Entrypoint\":null,\"OnBuild\":null,\"Labels\":null},\"container\":\"72913ee3dc1d3bf6af92d8412b87a5803f04f7088ba7a8a4d8baf2de9078300d\",\"container_config\":{\"Hostname\":\"\",\"Domainname\":\"\",\"User\":\"\",\"AttachStdin\":false,\"AttachStdout\":false,\"AttachStderr\":false,\"Tty\":false,\"OpenStdin\":false,\"StdinOnce\":false,\"Env\":[\"PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin\"],\"Cmd\":[\"/bin/sh\",\"-c\",\"printf \\\"Username: admin\\\\nPassword: production_admin\\\\n\\\" \\u003e /var/www/html/database.config\"],\"Image\":\"sha256:1e4a2d11384ed8ac500f2762825c3f3d134ad5d78813a5d044357b66d4c91800\",\"Volumes\":null,\"WorkingDir\":\"\",\"Entrypoint\":null,\"OnBuild\":null,\"Labels\":null},\"created\":\"2020-10-24T19:48:37.160476683Z\",\"docker_version\":\"19.03.13\",\"id\":\"7b05b529c51e9322588fe7ef7e9be250681641b9f207900c035a26abc2b7eac2\",\"os\":\"linux\",\"parent\":\"a3531d00ed14133152959cb0bc77cb214a65638bb5e295f0a57262049f56add3\"}"
      },
      {
         "v1Compatibility": "{\"id\":\"a3531d00ed14133152959cb0bc77cb214a65638bb5e295f0a57262049f56add3\",\"parent\":\"a64c6dae778e931d83b59934a5b58f97b85e09c743ed1b18cb053ca0ecd2c58a\",\"created\":\"2020-10-24T19:48:36.298388069Z\",\"container_config\":{\"Cmd\":[\"/bin/sh -c #(nop) COPY file:2c21f1c2caced37ec7c49be85e912509576e3aa6c68101bc90d3f56ae682b19c in /var/www/html/database.config \"]}}"
      },
      {
         "v1Compatibility": "{\"id\":\"a64c6dae778e931d83b59934a5b58f97b85e09c743ed1b18cb053ca0ecd2c58a\",\"parent\":\"2f585dc1662c7b0b99f93dfea45dd83e4b2bebdbf3e470c01e0569b941cb2cea\",\"created\":\"2020-10-24T19:48:36.007380392Z\",\"container_config\":{\"Cmd\":[\"/bin/sh -c mkdir -p /var/www/html/\"]}}"
      },
      {
         "v1Compatibility": "{\"id\":\"2f585dc1662c7b0b99f93dfea45dd83e4b2bebdbf3e470c01e0569b941cb2cea\",\"parent\":\"3a41447eea9358b0bfca1df658a78a9fcfe2f8281da222f9bea7a70e2dc0a03c\",\"created\":\"2020-10-24T19:46:44.83701677Z\",\"container_config\":{\"Cmd\":[\"/bin/sh -c apt-get update -y\"]}}"
      },
      {
         "v1Compatibility": "{\"id\":\"3a41447eea9358b0bfca1df658a78a9fcfe2f8281da222f9bea7a70e2dc0a03c\",\"parent\":\"5bd584b8f9464a6553e557ab0eceb484a63e77ab1b552c05eab75eeedde7c6d0\",\"created\":\"2020-10-13T01:39:05.467867564Z\",\"container_config\":{\"Cmd\":[\"/bin/sh -c #(nop)  CMD [\\\"bash\\\"]\"]},\"throwaway\":true}"
      },
      {
         "v1Compatibility": "{\"id\":\"5bd584b8f9464a6553e557ab0eceb484a63e77ab1b552c05eab75eeedde7c6d0\",\"created\":\"2020-10-13T01:39:05.233816802Z\",\"container_config\":{\"Cmd\":[\"/bin/sh -c #(nop) ADD file:0dc53e7886c35bc21ae6c4f6cedda54d56ae9c9e9cd367678f1a72e68b3c43d4 in / \"]}}"
      }
   ],
   "signatures": [
      {
         "header": {
            "jwk": {
               "crv": "P-256",
               "kid": "QHPR:B54B:QYBN:6HDH:OZ6E:RWXY:5GRN:2WL7:NXBI:626Y:ALEQ:LEKO",
               "kty": "EC",
               "x": "fmOeRiHvzpBMzCQjunmO8Btr4yBZ66AScZI2cIc2vdU",
               "y": "IlI0hZv602C51Dul7EeLV-JBdkCOxc7dSSCRecuzNvM"
            },
            "alg": "ES256"
         },
         "signature": "hoHMWtjqOZ3GigBr8YVMS_Uy5Pbbs8IVqqOblaBI7elw4TZvA2MMJO1e8z6C79jQQLobnTFjPIOytKQpM-zyMQ",
         "protected": "eyJmb3JtYXRMZW5ndGgiOjQwMTksImZvcm1hdFRhaWwiOiJDbjAiLCJ0aW1lIjoiMjAyMi0wMy0yOVQwMTo1MTo1OFoifQ"
      }
   ]
}
```