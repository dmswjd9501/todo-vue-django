# Vue - DRF

## 1. 기본 설정

1. Django

   1. 가상환경 설정

      ```bash
      $ python -V
      3.7.4
      $ python -m venv venv
      $ source venv/Scripts/activate
      (venv) $
      ```

   2. 패키지 설치

      ```bash
      (venv) $ pip install django djangorestframework
      (venv) $ pip freeze > requirements.txt
      ```

   3. django 프로젝트 생성

      ```bash
      $ django-admin startproject {프로젝트명} .
      ```

2. Vue

   1. VueCLI 설치

      ```bash
      $ npm install -g @vue/cli
      ```

   2. Vue 프로젝트 생성

      ```bash
      $ vue create {프로젝트 이름}
      ```

3. 프로젝트 폴더 구조

   ```
   todo-django-vue/
   	.git/
   	todo-django/
   		venv/
   		manage.py
   		todo_django/
   	todo-vue/
   		node_moduels/
   		public/
   		src/
   		package.json
   ```


## 2. DRF 모델링

## 3. Vue

### Vue-router

```bash
$ npm i vue-router
$ vue add router
> Still proceed? y
> Use history mode for router? (Requires proper server setup for index fallback in production) y
```

## 4. Todos axios 요청

1. getTodos 메소드 정의

   ```javascript
   // Home.vue    
   getTodos() {
    axios.get('http://127.0.0.1:8000/api/v1/todos/')
           .then(response => {
             console.log(response)
             this.todos = response.data
           })
           .catch(error => {
             console.log(error)
           })
       }
   ```

2. mounted에서 호출

   ```javascript
   // Home.vue   
   mounted() {
     this.getTodos()
   }
   ```

3. CORS 오류 발생

   * 해결하기 위해서는 django 서버에서 설정이 필요

4. `django-cors-headers` 패키지 활용

   * [Github 참고](https://github.com/adamchainz/django-cors-headers)

   ```bash
   $ pip install django-cors-headers
   ```

   * `INSTALLED_APPS` , `MIDDLEWARE` 설정
   * `CORS_ORIGIN_ALLOW_ALL` : True시 모든 도메인에서 요청 가능
   * `CORS_ORIGIN_WHITELIST` : 위의 옵션을 False로 하고, 화이트리스트에 직접 도메인 등록
   * 기타 옵션들도 확인 해볼것

5. Vue에서 다시 요청 보내보기

## 5. TodoForm component를 통해 투두 등록하기



## 6. 로그인 기능

> JWT (JSON Web Token) : 토큰 기반 로그인 인증
>
> 1. 클라이언트(Vue) 로그인 정보(username, password)를 서버(Django)로 전송
> 2. 서버는 해당 정보를 바탕으로 Token을 발급 및 암호화
> 3. 클라이언트는 Token을 받아서 매 요청때마다 헤더에 해당 Token정보를 추가해서 보냄
> 4. 서버에서는 매번 Token이 유효한지 확인 및 데이터 전송
> 5. 클라이언트는 전송된 값을 디코딩하여 사용자 정보 활용
>
> JWT는 기본적으로 헤더, Payload, Verify signature로 구성된다.
>
> https://jwt.io에서 직접 디코딩을 해볼 수 있다.

### 1) Django

```bash
$ pip install djangorestframework-jwt
```

### 2) Vue

1. 로그인 관련 컴포넌트 생성

2. 이벤트를 통해 axios 요청

3. token 값 저장

   1. `vue-session`

      ```bash
      $ npm i vue-session
      ```

   2. `src/main.js`

      ```javascript
      import VueSession from 'vue-session'
      Vue.use(VueSession)
      ```

   3. `vue-session` 활용하여 저장

      ```java
      this.$session.start()
      this.$session.set('jwt', token)
      ```


### 3) 활용

1. axios 요청시마다 아래의 `options`을 포함하여 전송

   ```javascript
   this.$session.start()
   const token = this.$session.get('jwt')
   const options = {
       headers: {
           Authorization: `JWT ${token}` 
           // JWT 다음에 공백있음.
       }
   }
   ```

### 4) 사용자 정보 활용

> 사용자 정보를 활용하고 싶다면, token을 디코딩하여 활용한다.

1. 패키지 설치

```bash
$ npm i jwt-decode
```

2. 활용

   ```javascript
   import jwtDecode from 'jwt-decode'
   this.$session.start()
   const token = this.$session.get('jwt')
   console.log(jwtDecode(token))
   //  {user_id: 1, username: "tak", exp: 1574217878, email: "tak@hphk.kr"}
   ```

## 7. User별 Todo

### 1. Django

### 2. Vue 

## 8. 비로그인시 로그인 페이지로 이동

## 9. delete, update

# 10. Vue

> Vuex는 Vue에서 활용하는 상태 관리 패턴이다.

# 핵심개념

1. `state` : 상태, Vue 컴포넌트 상에서 `data`

   * 직접 변경이 불가능하고, 항상 `mutation`을 통해 변경한다.
   * `state`가 변경되면 view (화면) 가 업데이트 된다.

2. `mutation` : `state`를 변경하기 위한 `methods`

   * `mutation` 함수는 첫번째 인자로 항상 `state`를 받는다.
   * `mutation`함수는 보통 `commit`을 통해 호출된다.

3. `action` : 비동기 처리를 하는 `methods`, `mutation`도 호출 가능하다. (`state` 변화를 `mutation` `commit`을 통해 가능하다.)

   * `action`함수는 첫번째 인자로 항상 `context`를 받는다.
     * `state`, `commit`, `dispatch`, ...
   * `action`함수는 항상 `dispatch`를 통해 호출된다.

4. `getters` : Vue component 상에서의 `computed`

   * 일반적인 `state` 값을 활용하는 변수의 경우 `getters`에 정의한다.

     









