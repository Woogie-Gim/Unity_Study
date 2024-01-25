# Photon PUN2 활용 멀티 플레이 구현
## 유니티 UI 사용을 위한 Canvas와 EventSystem
- Canvas나 EventSystem은 Hierachy - UI - Canvas or EventSystem 을 통해 생성 가능

![Alt text](<Images/login 1.PNG>)

- Canvas를 생성할 때 씬에 EventSystem이 없다면 EventSystem이 같이 생성
- EventSystem을 생성할 땐 Canvas가 없어도 따로 생성되지 않는다
  
- Canvas와 EventSystem이 없는 상태에서 UI (Button, Text 등)를 생성하면 Canvas, EventSystem이 자동으로 생성되며 UI는 Canvas의 자식 오브젝트로 생성

### Canvas

![Alt text](<Images/ui 2.PNG>)

- 모든 UI 요소들이 속해야 하는 영역
- 버튼, 토글, 이미지, 텍스트 등 모든 Unity UI 요소는 Canvas 오브젝트의 자식으로 존재해야 하며 그렇지 않은 UI는 그려지지 않는다
- 말 그대로 UI를 그리는 도화지
- Canvas와 UI들은 모두 RectTransform 이라는 UI용 트랜스폼을 가진다
- RectTransform을 이용해 Canvas 위에서 상대적 위치가 지정된 UI 는 Canavas의 렌더 모드, 타겟 디스플레이 등 컴포넌트 설정에 따라 게임 화면의 특정 부분에 나타낸다
  
![Alt text](<Images/ui 3.PNG>)

- Canvas 자식인 UI들은 배치된 순서에 따라 맨 위에 UI가 가장 먼저 (뒤에) 그려지고 맨 아래 UI 가 가장 나중에 (앞에) 그려진다

![Alt text](<Images/ui 4.PNG>)

- Canvas는 GameObject로써 씬에 존재하며 하나 이상 존재할 수 있다
- Canvas 단위로 Draw Call 이 관리되고 이를 어떻게 사용하느냐가 게임 성능에 영향을 주므로 최적화 시 고려해야 한다
- 생성된 Canvas들은 개별 Component를 가지며 기본적으로 Canvas, Canvas Scaeler, Graphic Raycaster 컴포넌트를 가지고 생성된다

![Alt text](<Images/ui 5.PNG>)

### Component
- Canvas
  - 캔버스 컴포넌트는 UI가 배치(구성)되고 그려지는 추상적인 공간
  - 모든 UI 요소는 캔버스 컴포넌트가 붙은 GameObject의 하위 요소가 되어야 한다
  - Render Mode 프로퍼티를 이용해 UI가 단순히 스크린에 렌더링 되도록 할 수도 있고 3D 공간 내의 오브젝트 처럼 렌더링 되도록 할 수 있다
  - 기본 Canvas 오브젝트에서 Canvas 컴포넌트를 삭제하려고 할 경우 CanvasScaler(Script), GraphicRaytcaster(Script)가 의존하고 있어 삭제할 수 없다고 경고한다
  
![Alt text](<Images/ui 6.PNG>)

- Canvas Scaler
  - 본 컴포넌트는 해당 캔버스에 배치된 모든 UI의 스케일과 픽셀 밀도를 컨트롤 한다
  - 이 값은 폰트 사이즈, 이미지 테두리 등 캔버스 아래에 있는 모든 요소에 영향을 준다
  - 따라서 본 값이 바뀌면 해당 Canvas 아래 모든 요소의 값도 변할 수 있다는 것을 주의 해야 한다
  - UI Scale Mode 프로퍼티로 캔버스 내 UI 요소들의 크기를 어떻게 할 것인지 결정한다
  
![Alt text](<Images/ui 7.PNG>)

- Canvas Scaler 활용 반응형 UI 만들기
  - UI Scale Mode : Constant Pixel Size 는 UI의 요소들이 해상도에 상관 없이 동일한 픽셀 수를 유지하는 설정
  
![Alt text](<Images/ui 8.png>)

  - 해상도 마다 UI 크기를 같게 해주고 싶다면 Scale With Screen Size를 선택 해야한다
  - Reference Resolution은 기준이 되는 해상도를 입력해야 한다

![Alt text](<Images/ui 9.png>)

![Alt text](<Images/ui 10.PNG>)

- Graphic Raycaster
  - 캔버스에 레이캐스트 하기 위한 컴포넌트
  - 레이캐스터가 캔버스에 있는 모든 그래픽을 감시하고 충돌했는지 체크
  - 해당 컴포넌트를 활용한다면 마우스에 닿은 UI를 스크립트에서 찾아 직접 제어하는 등의 작업도 가능
  - Event System이 이를 사용하며 이 컴포넌트가 없으면 버튼 클릭 등의 이벤트를 감지할 수 없다


### 텍스트 이동 애니메이션 구현 코드

![Alt text](<Images/ui 1.PNG>)

```C#
using UnityEngine;

public class textMoving : MonoBehaviour
{
    private RectTransform rectTransform;
    private Vector3 targetPosition;

    private void Start()
    {
        rectTransform = GetComponent<RectTransform>();
        targetPosition = rectTransform.anchoredPosition;
    }

    public void Update()
    {
        // 엔터는 Return
        if (Input.GetKeyDown(KeyCode.Return) && targetPosition.y > 0)
        {
            targetPosition = new Vector3(253.5f, -7.8f, 0.0f);
        }
        else if (Input.GetKeyDown(KeyCode.Return) && targetPosition.y < 0)
        {
            targetPosition = new Vector3(253.5f, 1200f, 0.0f);
        }

        MoveTowardsTarget();
    }

    private void MoveTowardsTarget()
    {
        // Lerp 함수를 사용하여 부드럽게 이동
        rectTransform.anchoredPosition = Vector3.Lerp(rectTransform.anchoredPosition, targetPosition, Time.deltaTime * 2.0f);
    }
}
```

### Event Sytem

![Alt text](<Images/event 1.PNG>)

- Canvas를 생성할 때 같이 생성되며 한 씬에 하나만 생성된다
- empty object를 만들어 Event sytem 컴포넌트들을 추가해 억지로 event system을 한 개 이상 만들고 게임을 실행하면 Event system이 하나만 있는지 확인하라고 경고가 뜬다

- input(마우스, 키보드 등) 기반 애플리케이션에 포함되는 오브젝트에 이벤트를 보내는 시스템
- Event System에는 이를 위한 컴포넌트들이 존재
- EventSystem 자체가 EventSystem 모듈 사이의 관리자 및 퍼실리 데이터로 설계되어 많은 기능이 노출되지는 않는다

- 이벤트시스템은 다음과 같은 일을 한다
  - 어떤 GameObject가 선택되었는지 관리
  - 사용되는 Input Moduole이 무엇인지 관리
  - Raycasting을 관리 (필요한 경우)
  - 필요에 따라 모든 Input Module을 업데이트

- Event Sytem의 Input Module은 앱이 지원할 입력 시스템 (터치, 조이스틱, 마우스 등)에 따라 어떻게 동작하게 할지 등을 커스터마이징 할 수 있는데 이런 설정에 따라 이벤트를 수신하고 처리한다

![Alt text](<Images/event 2.PNG>)

- Event System이 지원하는 이벤트에는 OnPointerEnter(포인터가 오브젝트에 들어간 경우 호출), On Select (오브젝트를 선택하는 순간 호출), OnMove(이동 이벤트 발생했을 때 호출) 등이 있으며, 개발자가 작성한 Input Module에 따라 커스터마이징도 가능

- EventSystem의 입력 이벤트를 감지하기 위해서 꼭 필요한 것이 Rycaster이며 이 중 하나가 바로 Canvas의 Graphic Raycaster이다.

![Alt text](<Images/event 3.PNG>)

- 이 밖에 Physics 2D Raycaster (2D 물리 요소용), Physics Raycaster (3D 물리 요소용)가 기본으로 제공된다

- 아래와 같은 방식으로 동작한다
  1. screnn space 상에서 어떤 위치가 주어지면
  2. Raycaster는 Ray에 충돌 가능한 모든 오브젝트 (Canvas의 상호작용 가능한 UI 등)을 탐색 수집하고
  3. Ray에 충돌한 오브젝트가 있는지 이 중 화면과 가장 가까운 오브젝트가 무엇인지 찾아낸다

## 로그인 씬

### UI 생성
- 로그인을 위한 UI 생성
- 서버 연결 상태 출력을 위한 UI - Text (TextMeshPro)
- 유저 아이디 입력을 위한 Input Field(TextMeshPro)
- 아이디 입력 후 사용할 접속 버튼 Button(TextMeshPro)
- 로그인 화면 작업을 담당할 LobbyManager(Empty)

![Alt text](<Images/login 1.PNG>)

### Text Mesh Pro 한글 세팅
- 폰트 TTF 파일을 유니티 프로젝트 Assets > Text Mesh Pro > Fonts 폴더에 넣는다

![Alt text](<Images/tmp 2.png>)

- 혹시 Assets에 Text Mesh Pro 폴더가 ㅇ벗을 경우 Hierachy 창에 UI > Text를 생성하게 되면 뜬다
- TMP Importer 창이 뜬다면 "Import TMP Essentials"를 눌러서 텍스트 메시 프로를 임포트 한다

![Alt text](<Images/tmp 1.PNG>)


- TMP 전용 폰트 생성
  - 유니티 Window > TextMeshPro > FontAsset Creator
  - 원하는 폰트를 넣고 다음과 같이 세팅
  - CharacterSet을 ASCII 로 설정
  
![Alt text](<Images/tmp 3.PNG>)

  - Generate Font Atals를 적용

![Alt text](<Images/tmp 5.PNG>)

  - Save를 눌러 Assets > Text Mesh Pro > Fonts 폴더에 저장

![Alt text](<Images/tmp 6.PNG>)

  - 생성된 파일을 선택해 Inspector 창에 Generation Setting 부분에 Atlas population Mode에서 Dynamic을 선택해주고 Sampling Point Size를 60 정도로 맞추고 Apply 적용

![Alt text](<Images/tmp 8.PNG>)

  - TMP에 폰트 적용

![Alt text](<Images/tmp 7.PNG>)

![Alt text](<Images/tmp 9.PNG>)

### LobbyManager 코드

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
using Photon.Pun;
using Photon.Realtime;

// MonoBehaviour 이 아닌 Pun 내에 함수를 사용하기 위한 MonoBehaviourPunCallbacks
public class LobbyManager : MonoBehaviourPunCallbacks
{
    public Button loginBtn;
    // TMP_Text 형 변수 선언
    public TMP_Text IDtext;
    public TMP_Text ConnectionStatus;

    // Start is called before the first frame update
    private void Start()
    {
        PhotonNetwork.ConnectUsingSettings();
        // 버튼 활성화 상태 기본 false로 비활성화 적용
        loginBtn.interactable = false;
        ConnectionStatus.text = "서버에 연결 중 입니다...";
    }

    public void Connect()
    {
        // Equals ==
        if (IDtext.text.Equals(""))
        {
            return;
        }
        else
        {
            PhotonNetwork.LocalPlayer.NickName = IDtext.text;
            loginBtn.interactable = false;

            // 연결에 성공했을 때
            if (PhotonNetwork.IsConnected)
            {
                ConnectionStatus.text = "방에 연결 중 입니다...";
                // 방에 랜덤으로 입장
                PhotonNetwork.JoinRandomOrCreateRoom();
            }
            // 연결에 실패했을 때
            else
            {
                ConnectionStatus.text = "오프라인 : 연결에 실패 했습니다. \n 재연결 중...";
                PhotonNetwork.ConnectUsingSettings();
            }
        }
    }

    // 서버를 사용할 수 있기 전에 최초 연결이 성립될 때 호출 
    public override void OnConnectedToMaster()
    {
        loginBtn.interactable = true;
        ConnectionStatus.text = "서버에 연결되었습니다!";
    }
    public override void OnDisconnected(DisconnectCause cause)
    {
        loginBtn.interactable = false;
        ConnectionStatus.text = "오프라인 : 연결에 실패 했습니다. \n 재연결 중...";
    }
    public override void OnJoinRandomFailed(short returnCode, string message)
    {
        ConnectionStatus.text = "빈 방이 없습니다. 방을 생성 중 입니다...";
    }
    public override void OnJoinedRoom()
    {
        ConnectionStatus.text = "방에 연결되었습니다.";
        PhotonNetwork.LoadLevel("Main");
    }
}

```

![Alt text](<Images/login 10.PNG>)

- LobbyManager에 스크립트 적용

![Alt text](<Images/login 9.PNG>)

- 버튼을 눌렀을 때 연결해야 하기 때문에 버튼 OnClick 설정


![Alt text](<Images/login 2.PNG>)

- LobbyManager는 MonoBehaviorPunCallbacks를 상속 받는다

![Alt text](<Images/login 3.PNG>)

- Start 메소드는 시작과 동시에 PhotonNetwork.ConnectUsingSettings(); 메소드를 이용해 Photon 서버와 연결하며,
연결하는 동안 loginBtn.interactoable = false; 로 접속 버튼을 누르지 못하게 하고 연결상태를 출력

![Alt text](<Images/login 4.PNG>)

- Connect 메소드는 접속 버튼을 누르면 실행할 메소드로, ID를 입력하지 않았다면 아무 반응을 하지 않는다
- PhotonNetwork.LocalPlayer.NickName = IDtext.text; 코드를 통해 해당 로컬플레이어의 닉네임(ID)을 입력한 텍스트로 저장
- 그 후 Start 메소드에서 성공적으로 Photon 서버와 연결되었다면 PhotonNetwork. JoinRandomOrCreateRoom() 메소드를 통해 채팅할 방에 입장하며, Start 메소드에서 Photon 서버와 연결이 되지 않았다면 재접속을 시도

![Alt text](<Images/login 5.PNG>)

- OnConnectedToMaster 메소드는 Photon 서버(Master서버)와 연결되면 실행되는 메소드로, 접속 버튼을 사용 가능케 하며 연결 상태를 온라인으로 바꾼다

![Alt text](<Images/login 6.PNG>)

- OnDisconnected 메소드는 Photon 서버와 연결이 끊겼을 경우 접속 버튼을 다시 사용 불가능하게 하며 연결 상태를 오프라인으로 바꿔 출력
- 그 후 서버와 재접속을 시도

![Alt text](<Images/login 7.PNG>)

- OnJoinRandomFailed 메소드는 Connect 메소드에서 JoinRandomRoom 메소드를 실행했으나 방에 들어가지 못한 경우 실행되는 메소드로, 적합한 방이 없으면 PhotonNetwork.CreateRoom을 이용해 새 방을 만든다. 
- 여기서 CreateRoom의 첫번째 인자는 방의 이름, 두번째 인자는 방의 옵션 여기선 방의 최대 인원을 4로 설정했습니다. (참고로 MaxPlayers = 0으로 하면 인원 제한을 없앨 수 있다.)

![Alt text](<Images/login 8.PNG>)

- OnJoinedRoom 메소드는 방에 성공적으로 입장했을 경우 실행되는 메소드로, 씬을 Main으로 옮긴다. 
- SceneManager.LoadScene()과 달리 PhotonNetwork.LoadLevel() 메소드를 사용한 이유는 네트워크의 정보를 그대로 가져가기 위함입니다.
  
## 채팅 씬 구현

- Scroll View, Input Field, Send버튼, ChattingList를 Hierachy에서 생성
- ChattingBox Empty Object를 생성하여 묶어주고 조절의 편의성을 줌

![Alt text](<Images/chat 1.PNG>)

![Alt text](<Images/chat 2.PNG>)

- 채팅을 띄워주기 위해 Scroll View- ViewPort - UI-Text를 만들어 채팅 로그를 띄워주는 역할로 사용
- ChatLog로 이름을 변경 후 TMP 폰트 수정 후 Content Size Filter 컴포넌트 추가하고 Vertical Fit을 Preferred Size로 설정

![Alt text](<Images/chat 3.PNG>)

- Scroll View - ViewPort - Content에도 Content Size Filter, Vertical Layout Group 을 추가하고 다음과 같이 설정

![Alt text](<Images/chat 4.PNG>)

- 빈 오브젝트 ChatManager 생성 후 ChatManager.cs 스크립트 작성

## 스크립트

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
using Photon.Realtime;
using Photon.Pun;
public class ChatManager : MonoBehaviourPunCallbacks
{
    public List<string> chatList = new List<string>();
    public Button sentBtn;
    public TMP_Text chatLog;
    public TMP_Text chattingList;
    public TMP_InputField input;
    public ScrollRect scroll_rect;
    string chatters;

    // Start is called before the first frame update
    void Start()
    {
        PhotonNetwork.IsMessageQueueRunning = true;
        scroll_rect = GameObject.FindObjectOfType<ScrollRect>();
    }

    public void SendButtonOnClicked()
    {
        if (input.text.Equals(""))
        {
            Debug.Log("Empty");
            return;
        }
        string msg = string.Format("[{0}] {1}", PhotonNetwork.LocalPlayer.NickName, input.text);
        photonView.RPC("ReciveMsg", RpcTarget.OthersBuffered, msg);
        ReceiveMsg(msg);
        input.text = "";
    }
    private void Update()
    {
        ChatterUpdate();
        if (Input.GetKeyUp(KeyCode.Return) && !input.isFocused)
        {
            SendButtonOnClicked();
        }
    }
    void ChatterUpdate()
    {
        chatters = "Player List\n";
        foreach (Player p in PhotonNetwork.PlayerList)
        {
            chatters += p.NickName + "\n";
        }
        chattingList.text = chatters;
    }
    [PunRPC]
    public void ReceiveMsg(string msg)
    {
        chatLog.text += "\n" + msg;
        scroll_rect.verticalNormalizedPosition = 0.0f;
    }
}
```

![Alt text](<Images/chat 5.PNG>)

- 스크립트 작성 후 스크립트 컴포넌트 Chat Manager에 추가하고 드로그앤 드랍을 통해 적절한 컴포넌트를 넣어줌

![Alt text](<Images/chat 6.PNG>)

- Photon View 컴포넌트 추가

![Alt text](<Images/chat 7.PNG>)

- Send 버튼의 On Click()에 ChatManager의 SendButtonOnClicked 메소드 추가
  
![Alt text](<Images/chat 8.PNG>)

- Start메소드에선 PhotonNetwork.IsMessageQueueRunning의 값을 true로 설정합니다. 또한, scroll_rect는 씬에서 ScrollRect 타입의 오브젝트를 찾아 할당
- scroll_rect를 만든 이유는 채팅이 많이 쌓일 경우 스크롤바의 위치를 아래로 고정시키기 위함

![Alt text](<Images/chat 9.png>)

- PhotonNetwork.IsMessageQueueRunning

![Alt text](<Images/chat 10.PNG>)

- SendButtonOnClicked 메소드는 전송 버튼이 눌리면 실행될 메소드로, 메세지 전송을 담당할 메소드
- input이 비어있으면 아무것도 전송하지 않고, 비어있지 않다면 "[ID] 할 말"의 형식으로 메세지를 전송
- 메세지 전송은 photonView.RPC 메소드를 이용해 각 유저들에게 ReceiveMsg 메소드를 실행
- 자기 자신에게도 메세지를 띄워야하니 ReceiveMsg(msg); 를 실행
- input.ActivateInputField();는 메세지 전송 후 바로 메세지를 입력할 수 있게 포커스를 Input Field로 옮긴다. (편의기능)
- 그 후 input.text를 빈칸으로 만듦

![Alt text](<Images/chat 11.PNG>)

- ReceiveMsg 메소드는 RPC 메소드로 사용할 수 있게 [PunRPC]를 메소드 위에 써주시면 되고, 하는 동작은 chatLog.text에 msg와 \n(개행문자)를 더해주고, scroll_rect.verticalNormalizedPosition = 0.0f; 로 메세지를 받을 때마다 스크롤을 가장 아래로 오게끔 한다

![Alt text](<Images/chat 12.PNG>)

- chatterUpdate 메소드는 채팅 플레이어 리스트를 업데이트
- Player List 텍스트 아래에 플레이어들의 ID를 더해주는 식으로 하며, 실시간으로 출입하는 유저들의 ID를 반영

![Alt text](<Images/chat 13.PNG>)

- Update 메소드에선 chatterUpdate(); 메소드로 주기적으로 플레이어 리스트를 업데이트하며, input에 포커스가  맞춰져있고 엔터키가 눌려졌을 경우에도 SendButtonOnClicked(); 메소드를 실행하는 기능을 추가

- 스크롤 수정 스크립트

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
using Photon.Realtime;
using Photon.Pun;

public class ChatManager : MonoBehaviourPunCallbacks
{
    public List<string> chatList = new List<string>();
    public Button sentBtn;
    public TMP_Text chatLog;
    public TMP_Text chattingList;
    public TMP_InputField input;
    public ScrollRect scroll_rect;
    string chatters;

    private float scrollSensitivity = 0.1f; // 스크롤 감도 조절

    // Start is called before the first frame update
    void Start()
    {
        PhotonNetwork.IsMessageQueueRunning = true;
        scroll_rect = FindObjectOfType<ScrollRect>();
    }

    public void SendButtonOnClicked()
    {
        if (input.text.Equals(""))
        {
            Debug.Log("Empty");
            return;
        }
        string msg = string.Format("[{0}] {1}", PhotonNetwork.LocalPlayer.NickName, input.text);
        photonView.RPC("ReceiveMsg", RpcTarget.OthersBuffered, msg);
        ReceiveMsg(msg);
        input.ActivateInputField();
        input.text = "";
    }

    private void Update()
    {
        ChatterUpdate();
        if (Input.GetKeyUp(KeyCode.Return) && !input.isFocused)
        {
            SendButtonOnClicked();
        }

        // 스크롤 위치 조절
        if (Input.GetMouseButtonDown(0))
        {
            StopCoroutine("ScrollToBottom");
        }
        else if (Input.GetMouseButtonUp(0))
        {
            StartCoroutine("ScrollToBottom");
        }
    }

    void ChatterUpdate()
    {
        chatters = "참가자\n";
        foreach (Player p in PhotonNetwork.PlayerList)
        {
            chatters += p.NickName + "\n";
        }
        chattingList.text = chatters;
    }

    [PunRPC]
    public void ReceiveMsg(string msg)
    {
        chatLog.text += "\n" + msg;
        StartCoroutine("ScrollToBottom");
    }

    IEnumerator ScrollToBottom()
    {
        yield return null;
        float normalizedPosition = 1f - scrollSensitivity;
        scroll_rect.verticalNormalizedPosition = normalizedPosition;
    }
}

```