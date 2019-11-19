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

### 4. getTodos

1. getTodos 메소드 정의

``` javascript
// Home.vue 
getTodos() {
    // axios 요청
    axios.get('http://127.0.0.1:8000/api/v1/todos/')
    .then(response => {
      console.log(response) // 만약 오류가 발생하게 되면 ESLint 설정을 안해줬기때문에 
      this.todos = response.data
    })
  },

```

2. mounted에서 호출

```javascript
  mounted() {
    this.getTodos()
  }
```

3. CORS 오류 발생

   * 해결하기 위해서는 django 서버에서 설정이 필요

4. `django-cors-headers`패키지 활용

   * [Github 참고]( https://github.com/adamchainz/django-cors-headers )

   ```bash
   $ pip install django-headers
   ```

   * `INSTALLED_APPS`, `MODDLEWARE`설정
   * `CORS_ORIGIN_ALLOW_ALL` : True 시 모든 도메인에서 요청가능
   * `CORS_ORIGIN_WHITELIST` : 위의 옵션을 False로 하고, 위의 도메인 등록
   * 기타 옵션들도 확인해 보기

5. vue에서 다시 요청 보내보기

### 5. TodoForm component를 통해 투두 등록하기

## 6. 로그인 기능

> JWT(JSON Web Token) : 토큰 기반 로그인 인증
>
> 1. 클라이언트(Vue) 로그인 정보(username, password)를 서버(Django)로 전송
> 2. 서버는 해당 정보를 바탕으로  Token을 발금 및 암호화
> 3. 클라이언트는 Token을 받아서 매 요청때마다 헤더에 비해 Toke정보를 추가해서 보냄
> 4. 서버에서는 매번 Token이 유효한지 확인 및 데이터 전송
> 5. 클라이언트는 전송괸 값을 디코딩 하여 사용자 정보 활용
>
> JWT는 기본적으로 헤더 ,payliad, Verify signature로 구성된다.
>
> https://jwt.io

```bash
$ pip install djangorestframework-jwt
```



