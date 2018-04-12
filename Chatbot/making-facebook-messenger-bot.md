# Facebook 챗봇 만들기(Mac OS 기준)

## 1. Set up Your Environment (환경설정)
* 메신저 봇은 메시지를 받거나 전송하기 위해 웹서버를 이용한다.
* 봇이 웹서버와 대화할 수 있으려면 웹서버와 인증을 거쳐야 한다.
* 페이스북을 통해 대중과 대화하려면 페이스북의 승인절차도 필요하다.

### 1.1 Build the Server (서버구축)

* Heroku [가입](https://www.heroku.com)
* 로컬에 Heroku CLI [설치](https://devcenter.heroku.com/articles/heroku-cli)

* brew 로 Heroku CLI 설치시 오류나는 경우:
```
Target /usr/local/bin/heroku
already exists. You may want to remove it:
  rm '/usr/local/bin/heroku'..
```
[여기](http://theoveranalyzed.net/2015/10/12/heroku-toolbelt-and-mac-os-x-1011-el-capitan) 참고.

* 서버코드 작성(index.js)
```javascript
var express = require('express')
var bodyParser = require('body-parser')
var request = require('request')
var app = express()

app.set('port', (process.env.PORT || 5000))

// Process application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({extended: false}))

// Process application/json
app.use(bodyParser.json())

// Index route
app.get('/', function (req, res) {
    res.send('Hello world, I am a chat bot')
})

// for Facebook verification
app.get('/webhook/', function (req, res) {
    if (req.query['hub.verify_token'] === 'my_voice_is_my_password_verify_me') {
        res.send(req.query['hub.challenge'])
    }
    res.send('Error, wrong token')
})

// Spin up the server
app.listen(app.get('port'), function() {
    cons
```

* 서버 실행
```
node index.js
running on port 5000
```

* 서버 테스트
```javascript
curl http://localhost:5000
Hello world, Im a chat bot
```

* Procfile 생성
```
web: node index.js
```

* Heroku 로그인(터미널에서)
```
heroku login
```

* git 커밋
```
git init
git add .
git commit -m "first commit"
heroku create
git push heroku master
```


[The Secret To Making Your Own Facebook Messenger Bot In Less Than 15 Minutes]
https://chatbotsmagazine.com/have-15-minutes-create-your-own-facebook-messenger-bot-481a7db54892