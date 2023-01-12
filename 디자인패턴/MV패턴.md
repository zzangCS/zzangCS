MVC 패턴
이벤트 기반
재사용성, 확장성이 좋음
but, 복잡해질수록 model-view 복잡
mvc.jpg

Untitled

model : 데이터 관리 (정보) ⇒ 비즈니스 로직
view : 사용자 인터페이스 요소 ⇒ 서비스 로직
controller : 조종 ⇒ 메인 로직
MVC 패턴을 지키면서 코딩을 하는 방법 5가지

```
class Student {
constructor(name, age){
this.name = name;
this.age = age;
}
getName(){
return this.name;
}
getAge(){
return this.age;
}
}

class OutputView extends Student {
printProfile() {
return `나는 ${this.getName()}이고, ${this.getAge()}살 입니다.`
}
}

let realStudent = new OutputView('지원','25');

console.log(realStudent.printProfile());
```

모델 내부에 컨트롤러와 뷰의 코드가 있으면 안된다.

```
class Student {
constructor(){
this.name = name;
this.age = age;
}
getName(){
return this.name;
}
getAge(){
return this.age;
}
}
```

뷰 내부에 모델의 코드만 있을 수 있고, 컨트롤러 코드가 있으면 안된다.

```
class OutputView extends Student {
printProfile() {
return `나는 ${this.getName()}이고, ${this.getAge()}살 입니다.`
}
}
```

뷰가 모델로부터 데이터를 받을 때는 사용자마다 상이한 데이터만 받아야 한다.

Untitled

Untitled

컨트롤러 내부에는 모델과 뷰 코드가 있을 수 있다. //

```
class Controller {
let realStudent = new OutputView('지원','25');
}
```

console.log(realStudent.printProfile());
뷰가 모델로부터 데이터를 받을 때, 반드시 컨트롤러에서 받아야 한다.

백엔드
Untitled

클라이언트의 request를 받는다.
request를 분석한다. → 라우팅
필요한 데이터를 수집/가공한다.
뷰를 생성하고 response한다.
이 경우 뷰가 모델을 알아야 하는 강한 의존성이 생겨버린다!! → mvc패턴 사용

프론트엔드
Untitled

jQuery가 도입되면서

ajax로부터 받는 데이터 → model
html,css로 만들어지는 화면 → view
js로 서버에서 데이터를 받아 화면을 바꾸고 이벤트 처리해서 서버에 데이터를 전달 → controller
📝 백에서처럼 사용은 불가능 하다 왜냐!!! view에서 너무 많은 이벤트들이 벌어지니까!!!!!
Untitled

뷰 변경으로 모델을 바꿔야 하는 경우 (ex. 사용자 입력 값)
모델의 변경으로 뷰를 바꿔야 하는 경우 (ex. 서버로 받은 데이터)
⇒ 1)뷰와 모델의 양방향이 프론트엔드의 복잡도를 높이고, 2)뷰가 너무 많고, 3) 뷰는 계층적인 구조를 가져야 하기에(tree구조, 렌더링) 의존성과 복잡도가 높아 더 잘게 쪼갤 필요성이 있다!!!

복잡한 view, model 관계를 단순화하고, view 계층처리로 쉽고 효율적인 DOM 처리가 필요하다.
그래서 나온 기술들

데이터 바인딩 - 뷰-모델의 데이터가 자동으로 변경(리렌더링도 자동으로)

MVVM - 뷰용 모델

Flux 아키텍쳐

MVVM 패턴
클라이언트 개발도 서버처럼 템플릿과 같은 선언적 방식으로 개발할 수 있지 않을까?

뷰를 더 추상화한 계층
커맨드, 데이터 바인딩
UI 재사용이 용이하고, 단위테스트하기 쉽다.
mvvm.jpg

중요 키워드 : 템플릿, 바인딩
mvc 패턴의 방식은 그대로지만, jQuery 같은 DOM 조작에서 템플릿 & 바인딩을 통한 선언적 방법

⇒ 뷰를 그리는 모델만 따로 생겼다!! ViewModel

viewModel은 한 마디로, model에서 view에 적합한 데이터로 가공해서 주는 역할!

MVC vs MVVM
컨트롤러의 반복적인 기능이 선언적인 방식으로 개선되었다.

모델과 뷰의 관점을 분리하지 않고 하나의 템플릿으로 관리한다.

(class나 id로 간접적으로 HTML에 접근하려 했다면, 이제는 직접적으로 접근)
