---
title:  "[Android] 구성요소 (4대 컴포넌트)"
excerpt: "Android Application이 가지는 4대 구성요소에 대해 알아보자."
last_modified_at: 2019-10-23T08:06:00-05:00
 #categories:
 #  - Blog
 #tags:
 #  - Blog
---

## 안드로이드의 4대 컴포넌트 (Component)

안드로이드는 4개의 `컴포넌트 (Component)`를 가지고 있는데, 이 컴토넌트들은 제각각 하나의 독립된 형태를 가지고 있으며, 각자 정해진 역할을 수행을 하게 됩니다.

또한, 이 컴포넌트들은 인텐트(Intent) 라는 일종의 메시지 객체를 통하여 상호 작용을 하게 됩니다. 예를 들어, 액티비티에서 다른 구성요소를 호출 할때는 인텐트를 거쳐야 한다는 것입니다.  

아래의 그림은 안드로이드의 4대 컴포넌트를 그림으로 나타낸 것입니다.

![이미지](/assets/images/component.png){: .align-center}

여기서 추가적으로 안드로이드 3.0부터는 프래그먼트(Fragment)가 추가되었습니다. 물론 프래그먼트(Fragment)가 안드로이드 뷰도 아니고 구성 요소로 보긴 어렵지만, 3.0 (API Level 11) 버전 이후부터는 핵심 컴포넌트로 봐도 무방할 정도로 매우 활용도가 높아지고 있습니다.

### 각 컴포넌트(Component)들의 정의와 특징

> **액티비티 (Activity)**

화면 UI를 담당하는 컴포넌트 입니다. 액티비티는 기본적으로 생명주기라는 것을 가지고 있는데 이 생명주기 메소드를 재정의 하긴 위해서 자바 소스에서 Activity클래스를 상속해야 합니다. 안드로이드를 하면서 가장 많이 쓰이는 컴포넌트이기 때문에 굉장히 중요한 컴포넌트라 할 수 있습니다.
* 반드시 하나이상의 Activity를 가지고 있어야 한다.
* 두 개의 액티비티를 동시에 Display할 수 없다.
* 액티비티 내에 프래그먼트(Fragment)를 추가하여 화면을 분할 시킬 수 있다.

---

> **서비스 (Service)**

서비스는 백그라운드에서 실행되는 프로세스를 의미합니다. 서비스는 화면에 존재하진 않지만 애플리케이션의 구성요소이므로 새로 만든 후에는 항상 매니페스트에 등록을 해주어야 합니다. startService()라는 메서드를 이용하여 서비스를 실행시킬 수 있습니다.

* 그저 백그라운드에서 돌아가는 컴포넌트입니다.
* 한번 시작된 서비스는 애플리케이션이 종료되어도 계속해서 백그라운드에서 돌아갑니다.
* 모든 서비스는 Service클래스를 상속 받습니다.
* 네트워크를 통해 데이터를 가져올 수 있습니다.

--- 

> **방송수신자 (Broadcast Receiver)**

안드로이드에서 다양한 이벤트와 정보를 받아 반응하는 컴포넌트입니다. 메시지를 여러 객체에게 전달하는 방법을 의미하는데 이렇게 전달되는 브로드캐스팅 메시지를 방송 수신자(Broadcast Receiver) 라고 합니다.

* 대부분 UI를 가지고 있지 않습니다.
* 수신기를 통해 디바이스의 상황을 감지하고 적절한 작업을 수행합니다.

---

> **콘텐트 제공자 (Content Provider)**

데이터를 관리하고 다른 애플리케이션 데이터를 제공해주는 컴포넌트로, 주로 데이터베이스의 데이터를 전달할 때 많이 사용합니다. 콘텐트 제공자는 다른 컴포넌트와는 다르게 생명주기를 가지고 있지 않습니다.

* SQLiteDB, Web등을 통해서 데이터를 관리합니다.
* 콘텐트 제공자를 통하여 다른 애플리케이션의 데이터도 변경할 수 있습니다.

---