# Docker 시작

## 설치(생략)

## 이미지 받기
```
docker pull ubuntu:latest
docker pull ubuntu:16.04

# 이미지가 없으면 다운로드 후 컨테이너 생성
docker run ubuntu:16.04
```

## 포트 포워딩
```
docker run -d -p 1234:6379 redis
```

## 이미지 리스트업
```
docker images -a
```

## 이미지 삭제
```
# 특정 이미지만 삭제
docker rmi {IMAGE ID / imageName:tag}

# 특정 이미지만 강제 삭제
docker rmi {IMAGE ID} -f

# 전체삭제
docker rmi $(docker images -a -q)
```

## 이미지를 컨테이너로 생성 후 bash shell 모드로 들어가기
```
# docker run -i -t --name {이미지이름} {실행할 파일}/bin/bash

# 1 (--rm : bash 종료 시 컨테이너도 함께 종료됨)
docker run (--rm) -i -t --name dev ubuntu /bin/bash

# 2 (실행중인 컨테이너에 접속하기)
docker attach dev(or id)
```

## 컨테이너 목록 확인
```
docker ps -a

# -a 생략시 실행중인 컨테이너만 표시
```

## 컨테이너 (재)시작하기
```
docker (re)start dev
```
## 외부에서 명령하기
```
docker exec dev echo "hi"
```

## 컨테이너 중지(컨테이너 삭제)하기
```
docker stop(rm) hello
```

## 중지된 컨테이너 일괄 중지/삭제
```
docker rm -v $(docker ps -a -q -f status=exited)
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

## 참고
* [가장 빨리 만나는 도커] (http://www.pyrasis.com/book/DockerForTheReallyImpatient/)
* [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
* [subicura](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html#%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0)