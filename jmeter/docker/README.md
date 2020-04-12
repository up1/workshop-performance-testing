## Step to run

### 1. Build Docker Image of Apache JMeter
$docker image build -t somkiat/jmeter .

### 2. Deploy with Docker swarm
$docker swarm init
$docker stack deploy --compose-file docker-compose.yml stackdemo
$docker container run --network=stackdemo_default --rm alpine nslookup jmeter
Name:	jmeter
Address: 10.0.1.3
Name:	jmeter
Address: 10.0.1.2

### 3. Start distributed testing with JMeter
$docker container run --rm --network=stackdemo_default -v $(pwd):/result  --entrypoint /bin/bash -it somkiat/jmeter
#/apache-jmeter-5.2.1/bin/jmeter -n -t sample.jmx -l /result/result.csv -R 10.0.2.2,10.0.2.3
#wc -l /result/result.csv


