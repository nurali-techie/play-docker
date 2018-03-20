1. Build docker image - docker build -t mynginx .
2. Run docker image - docker run -p 9090:9090 mynginx
3. Curl two time same URL - http://localhost:9090/Code/JarDownload/abbot/abbot-0.12.3.jar.zip derived from http://www.java2s.com/Code/JarDownload/abbot/abbot-0.12.3.jar.zip

First time - curl http://localhost:9090/Code/JarDownload/abbot/abbot-0.12.3.jar.zip -v --output j1.jar
Output:
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 9090 (#0)
> GET /Code/JarDownload/abbot/abbot-0.12.3.jar.zip HTTP/1.1
> Host: localhost:9090
> User-Agent: curl/7.55.1
> Accept: */*
> 
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0< HTTP/1.1 200 OK
< Server: nginx/1.13.9
< Date: Tue, 20 Mar 2018 06:34:28 GMT
< Content-Type: application/zip
< Content-Length: 624959
< Connection: keep-alive
< Last-Modified: Fri, 10 May 2013 07:00:00 GMT
< ETag: "162313-9893f-4dc57b7289c00"
< X-Cache: MISS
< Accept-Ranges: bytes
< 
{ [3383 bytes data]
100  610k  100  610k    0     0   152k      0  0:00:04  0:00:04 --:--:--  128k
* Connection #0 to host localhost left intact
```
Check - X-Cache: MISS -- it has value MISS

Second time - curl http://localhost:9090/Code/JarDownload/abbot/abbot-0.12.3.jar.zip -v --output j1.jar
Output:
```  
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 9090 (#0)
> GET /Code/JarDownload/abbot/abbot-0.12.3.jar.zip HTTP/1.1
> Host: localhost:9090
> User-Agent: curl/7.55.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: nginx/1.13.9
< Date: Tue, 20 Mar 2018 06:34:35 GMT
< Content-Type: application/zip
< Content-Length: 624959
< Connection: keep-alive
< Last-Modified: Fri, 10 May 2013 07:00:00 GMT
< ETag: "162313-9893f-4dc57b7289c00"
< X-Cache: HIT
< Accept-Ranges: bytes
< 
{ [7240 bytes data]
100  610k  100  610k    0     0   610k      0  0:00:01 --:--:--  0:00:01 99.3M
* Connection #0 to host localhost left intact
```
Check - X-Cache: HIT -- it has value HIT

Also check, connect to container with bash and check content of nginx cache directory - /var/cache/nginx/m2cache
