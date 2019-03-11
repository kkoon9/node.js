JSON-RPC
-----------------------
- - -
- RPC가 서버와 데이터를 주고받는 기능을 담당한다.
![RPC를 사용한 요청과 응답](https://github.com/kkoon9/node.js/blob/master/img/RPC.PNG)  
- 웹 서버에 add 함수를 만들어 둔다.
- 이 함수를 클라이언트에서 호출한다.
- 라이브러리에서는 stub을 통해 서버로 요청을 보낸다.
- 서버에서는 add 함수를 실행한 후 그 결과 값을 응답으로 보내준다.
- 이 과정은 라이브러리를 통해 이루어지기 때문에 개발자는 클라이언트와 서버 사이에 어떤 데이터를 어떻게 주고받는지 신경 쓰지 않아도 된다.
- 노드와 익스프레스 환경에서는 jayson 모듈을 사용한다.
- 핸들러 : JSON-RPC를 사용하기 위해 등록한 각 함수
## 스텁(stub)
- 본래의 뜻은 연필 토막이나 담배꽁초처럼 쓰고 남은 조각을 뜻한다.
- 그 자체로 제 기능은 발휘하지 못하지만 원래 개체가 무엇인지 알아낼 수 있는 참조 역할을 하고 원 개체의 기능조작을 위임받은 위임자 역할을 하는 작은 개체이다.
### 스텁의 작동 원리
- 클라이언트는 그에 해당하는 스텁의 메소드를 불러내면 이 스텁이 대신하여 해당 메소드를 수행한다.
- 클라이언트가 메소드를 불러내어 조작하는 과정
1. 클라이언트는 조작하고자 하는 서버에 접속하여 개체를 찾는다.
2. 서버는 개체에 대응하는 스텁을 클라이언트에게 전달한다.
3. 클라이언트는 대상 스텁의 원하는 메소드를 불러낸다.

## Express
- 서버 제작 시 불편함을 해소하고, 편의 기능을 추가한 웹 서버 프레임워크
- http 모듈의 요청과 응답 객체에 추가 기능들을 부여했다.
- 기존 메서드들도 계속 사용할 수 있지만 편리한 메서드들을 추가하여 기능을 보완
- 코드를 분리하기 쉽게 만들어 관리가 용이
- if문으로 요청 메서드와 주소를 구별하지 않아도 된다.
![express 디렉터리 구조](https://github.com/kkoon9/node.js/blob/master/img/express.PNG)
### bin/www
- 서버를 실행하는 스크립트이다.
- http 모듈에 express 모듈을 연결하고 포트를 지정하는 부분
~~~javascript
// 1. app, debug, http 모듈을 가져온다.
var app = require('../app');
var debug = require('debug')('폴더명:server');
var http = require('http');

// 2
var port = normalizePort(process.env.PORT || '3000');
// process.env 객체에 PORT 속성이 있다면 그 값을 사용하고 없다면 기본값으로 3000번 포트를 이용한다. 
app.set('port',port); // 서버가 실행될 포트를 설정한다.

// 3. http.crateServer에 불러온 app모듈을 넣어준다. app모듈이 createServer 메서드의 콜백 함수 역할을 한다.
var server = http.createServer(app);

// 4.listen을 하는 부분은 포트를 연결하고 서버를 실행한다.
server.listen(port);
server.on('error',onError);
server.on('listening', onListening);
~~~
### app.js
- 핵심적인 서버 역할을 수행한다.
~~~javascript
// 1. express 패키지를 호출하여 app 변수 객체 생성
var app = express();

// 2. app.set 메서드로 익스프레스 앱을 설정한다.
//view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'pug');

// 3. 미들웨어를 연결하는 부분
app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname,'public')));

app.use('/', indexRouter);
app.use('/users', usersRouter);

//catch 404 and forward to error handler
app.use(function(req, res, next) {
    next(createError(404));
});

//error handler
app.use(function(err, req, res, next) {
    //set locals, only providing error in development
    res.locals.message = err.message;
    res.locals.error = req.app.get('env') === 'development' ? err : {};

    //render the error page
    res.status(err.status || 500);
    res.render('error');
});

// 4. app 객체를 모듈로 만든다. bin/www에서 사용될 app 모듈
module.exports = app;
~~~
![express 구조도](https://github.com/kkoon9/node.js/blob/master/img/express_a.PNG)
- 클라이언트의 요청을 받아서 처리한 후, 다시 클라이언트에게 응답한다.
### public 폴더
- 외부(클라이언트)에서 접근 가능한 파일들을 모아둔 폴더. 이미지, 자바스크립트, CSS 파일들이 들어있다.

### routes 폴더
- 주소별 라우터들을 모아둔 곳이다.
- 서버의 로직은 모두 이 폴더에서 작성된다.

### views 폴더
- 템플릿 파일을 모아둔 곳이다.
- 화면 부분은 모두 이 폴더에서 작성된다.

### models 폴더
- 데이터베이스를 작성하는 폴더이다.

## 미들웨어
- 익스프레스의 핵심
- 요청과 응답의 중간(middle)에 위치한다.
- 라우터와 에러 핸들러 또한 미들웨어의 일종이다.
- 주로 app.use와 함께 사용된다.