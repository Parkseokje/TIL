# lambda 함수 생성하기

## 1. policy.json 만들기
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## 2. role 생성하기(CLI 사용)
```
aws iam create-role
--role-name basic-lambda-role
--assume-role-policy-document file://policy.json
(주의: 줄바꿈(개행) 안먹힘. 가독성 위해 줄바꿈 삽입)
```

## 3. 어플리케이션 압축
```
zip -r lb-test.zip index.js
```

## 4. 배포 및 람다함수 생성
```
aws lambda create-function --region ap-northeast-2 --function-name lb-test --zip-file fileb://lb-test.zip --role arn:aws:iam::************:role/basic-lambda-role --handler index.handler --runtime nodejs4.3 --memory-size 128
```

## 5. 람다함수 생성여부 파일로 출력
```
aws lambda list-functions --profile **** > lambda-functions.txt
(주의 : aws account 가 여러개일 경우 --profile {aws ID 입력})
```

## 6. 람다함수 호출 및 결과로그 출력
```
aws lambda invoke --invocation-type RequestResponse --function-name lb-test --region ap-northeast-2 --log-type Tail --payload '{"username": "seokje"}' output.txt
```