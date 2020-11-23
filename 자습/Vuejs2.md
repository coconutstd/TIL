# Vuejs 자습 2

Vue-router 라이브러리를 쓰는 이유? 클라이언트 렌더링을 구현하기 위해 

```vue
routes = {
	{path : '/' , component: Home},
	{path : '/login', component: Login},
}
```

Axios를 쓰는 이유? XMLHttpRequest를 간편하게 전송하기 위함, 다양한 브라우저 지원 

```shell
npm install -g axios
```

```javascript
import axios from 'axios'
```

(method, path, data) 의 데이터를 요청으로 넘겨줌

Then, catch, finally  정상, 오류, 최종

$route, $router 

Computed 에는 토큰유무 등,