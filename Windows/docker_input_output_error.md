I got the following error today:

C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: driver failed programming external connectivity on endpoint gracious_zhukovsky (891a0bd43372eed8769b7145dbc73a46a78234e2efedbfc2b04fcc7fc301db7c): Error starting userland proxy: mkdir /port/tcp:0.0.0.0:8181:tcp:172.17.0.2:1234: input/output error.


I resolved it by turning Docker off and on again.