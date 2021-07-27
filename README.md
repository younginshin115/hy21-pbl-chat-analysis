# Description

## 프로젝트 개요
라이브 커머스 방송을 원활하게 진행할 수 있도록 보조하는 머신러닝 기반 챗봇 'JAVAS' 개발

## 프로젝트 기간
2021.06.07~2021.8.17

## 주요 기능
- 다양한 라이브커머스 채널 지원(유튜브, 트위치, 네이버 쇼핑라이브) 

- 채팅 텍스트를 머신러닝으로 분석하여 비속어 필터링 

- 채팅창의 긍/부정 감정 분석 및 시각화 

- 채팅창의 트렌드를 파악하기 위해 실시간 빈도순 워드 클라우드 제공 

## 프로젝트 팀(총 6명)
|이름|이메일|
|:----:|:---|
|이수현|lshyun955@gmail.com|
|신영인|younginshin115@gmail.com|
|임재일|jaeillim89@naver.com|
|맹광국|ggmaeng@gmail.com|
|손덕기|deokki9880@gmail.com|
|장지연|delayeon9934@naver.com|

# 현재 배포되고 있는 서비스 URL
http://52.149.146.199:5307

### 각 서비스 접속 URL
|서비스|주소|
|:---|:---|
|airflow|http://52.149.146.199:8083/|
|grafana|http://52.149.146.199:3000/|

<br>

# Environment

|분류|이름|버전|
|:---|:---|:---|
|운영체제|ubuntu|18.04|
||Docker|20.10.7|
||Docker-compose|3.2|
||Nvidia Driver|470.57.02|
||CUDA|11.2.2|
||cuDNN|8|
|개발언어|Java|1.8|
||Python|Spark Container - 3.8.3<br>Flask Container - 3.9.5|
||Scala|2.12|
|DB|MongoDB|4.4.6|
||InfluxDB|TBD|
|파이프라인|Kafka|2.8.0|
||Spark|3.1.2|
||Hadoop|3.2|
||Airflow|2.1.2|
||Flink|TBD|
|ML|Tensorflow|2.5.0|
||Keras|2.4.3|
||NLTK|2.6.2|
||KoNLPy|0.5.2|
|협업툴|Gitlab, Onedrive, Slack||


ML: Keras, CNN-LSTM 


# Usage

## Ubuntu에서 컨테이너 실행
1. docker-compose.yml 파일이 있는 Dockerfiles 디렉토리로 이동

2. 아래 명령어를 입력하면 docker-compose 개발 환경 실행
```
docker-compose up -d
```

3. 아래 명령어로 컨테이너 이름 확인
```
docker ps -a
```

4. 아래 명령어로 원하는 컨테이너 접속
```
docker exec -it [컨테이너 이름 또는 아이디] /bin/bash
```
<br>

## 윈도우 환경에서 컨테이너 실행
1. WSL2 설치(참고 링크: https://www.44bits.io/ko/post/wsl2-install-and-basic-usage)

2. 윈도우에 Docker Desktop 설치(설치 링크: https://www.docker.com/products/docker-desktop)

3. Vivual Studio Code 설치 후 Docker Extension 설치

4. 터미널에서 아래 명령어를 실행하여 도커가 제대로 설치되었는 지 확인
```
docker version
```

5. 터미널에서 docker-compose.yml 파일이 있는 Dockerfiles 디렉토리로 이동

6. 아래 명령어를 입력하면 docker-compose 개발 환경 실행
```
docker-compose up -d
```

7. 아래 명령어로 컨테이너 이름 확인
```
docker ps -a
```

8. 아래 명령어로 원하는 컨테이너 접속
```
docker exec -it [컨테이너 이름 또는 아이디] /bin/bash
```

<br><br>

## 컨테이너가 실행되어있을 경우 서비스 실행

1. 아래 명령어로 spark 컨테이너에 submit을 한다.
```
docker exec -it spark-master /spark/bin/spark-submit --master spark://spark-master:7077 --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2 /spark/streamingspark.py
```

2. IP:5307로 접속한다(포트가 열려있지 않은 경우 포트 열어주기)

3. 원하는 채널과 URL을 입력하여 서비스를 실행한다

## 모니터링을 원하는 경우
1. 도커를 swarm 모드로 변경한다
```
docker swarm init
```

2. docker-compose up을 실행한다
```
docker-compose up -d
```