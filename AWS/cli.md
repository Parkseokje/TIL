# CLI 사용하기

## 준비
1. pip 설치/업그레이드
```
# 설치
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
sudo python get-pip.py
# 업그레이드
pip install --upgradepip
```

2. pip 사용하여 cli 설치
```
sudo pip install awscli
aws --version
# aws-cli/1.15.4 Python/3.6.3 Darwin/17.4.0 botocore/1.10.4

# 제거
pip uninstall awscli
```

3. cli 구성
```
aws configure

AWS Access Key ID [None]: ****
Secret Access Key [None]: ****
Default region name [None]: ap-northeast-2
awDefault output format [None]: json
```

##  참고
* [설치 및 구성 - 1](https://docs.aws.amazon.com/ko_kr/streams/latest/dev/kinesis-tutorial-cli-installation.html)
* [설치 및 구성 - 2](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/installing.html)

