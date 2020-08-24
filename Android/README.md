# Android
>- [MVC](#mvc)
>- [MVP](#mvp)

<a name="mvc"></a>
## MVC
- Model, View, Controller의 약자
  - Model : 데이터를 가집니다.
  - View : 사용자에 보일 화면을 표현합니다.
  - Controller : 사용자로부터 입력을 받고, 이를 Model에 의해 View를 정의하게 됩니다.
- Android에서는 Activity/Fragment 같은 View들이 View와 Controller 모두 가지고 있습니다.  
![MVC](https://user-images.githubusercontent.com/44170716/90515128-24b24780-e19d-11ea-8387-cad480e602b1.PNG)
```
1. Activity에서 사용자 이벤트 발생
2. Model로부터 데이터 갱신이 필요한지 확인
3. Model로부터 전달받은 데이터를 통해 View 갱신 여부 판단
4. View에서 UI 갱신 처리
```

<a name="mvp"></a>
## MVP
- Model, View, Presenter의 약자
  - Model : Data와 관련된 처리를 담당
    - Data의 전반적인 부분을 Model에서 담당하고 네트워크, 로컬 데이터 등을 포함
  - View : 사용자의 실질적인 이벤트가 발생하고, 이를 처리 담당자인 Presenter로 전달
    - 완전한 View의 형태를 가지도록 설계. 계산을 하거나 데이터를 가져오는 등의 행위는 Presenter에서 처리하도록 함
  - Presenter : View에서 전달받은 이벤트를 처리하고, 이를 다시 View에 전달
    - View와는 무관한 Data등을 가지고, 이를 가공하고 View에 다시 전달하는 역할
![mvp](https://user-images.githubusercontent.com/44170716/90516283-bbcbcf00-e19e-11ea-9c1a-acfae3d81295.PNG)
```
1. View : View에서 터치 이벤트 발생
2. View -> Presenter : Presenter에 이벤트 전달
3. Presenter / Presenter -> Model : 이벤트의 형태에 따라 캐시 데이터를 가져오거나 Model에 요청
4. Model : 데이터를 로컬 또는 서버에서 가져옴
5. Model -> Presenter : 데이터 통보
6. Presenter : 전달받은 데이터를 가공
7. Presenter -> View : 가공한 데이터를 View에 전달
8. View : UI 갱신 처리
```
</br>

- Presenter 구분 방법들
1. View에 대한 interface만 정의하는 방법
    - interface View : View에 대한 interface만 정의
    - Presenter : interface 정의 없이 함수를 생성하여 사용
    - View : interface View를 상속받아서 정의
2. Google Architecture를 따름
    - Contract : View와 Presenter에 대한 interface를 작성
    - Presenter : Contract.Presenter를 상속받아서 구현
    - View : Contract.View를 상속받아서 구현
3. PresenterImpl을 구현
    - Presenter : Presenter와 View에 대한 interface를 구현
    - PresenterImpl : Presenter를 상속받아서 구현
    - View : Presenter.View를 상속받아서 구현
</br>

- Adapter Contract

![mvp_adapter contract](https://user-images.githubusercontent.com/44170716/90950929-275cb780-e491-11ea-8256-0159d2289ef7.PNG)

- Google Architecture의 Model
  - Repository : Remote/Local을 구분하며, memory cache를 포함
  - Remote : 서버를 통한 데이터를 불러옴
  - Local : 단말기 상의 SQL, Realm 등을 통한 데이터를 불러옴
![mvp_model](https://user-images.githubusercontent.com/44170716/91030724-90cbfa00-e63a-11ea-9f75-7e9199ffb2ae.PNG)
