# Scriptable Object

- 스크립터블 오브젝트(Scriptable Object)는 유니티에서 제공하는 대량의 데이터를 저장하는데 사용할 수 있는 데이터 컨테이너
- 스크립터블 오브젝트를 사용하면 값의 사본이 생성되는 것을 방지하여 프로젝트의 메모리 사용을 줄일 수 있다
- 이것은 모노비헤이비어(MonoBehaviour) 스크립트에 변경되지 않는 데이터를 저장하는 프리팹을 사용하는 프로젝트에서 유용
- 변경되지 않는 데이터를 사용하는 프리팹의 데이터를 일반 변수로 구현할 경우 인스턴스화 할 때마다 프리팹에 이 데이터에 대한 자체 사본이 생성되는데 스크립터블 오브젝트를 사용하면 메모리에 스크립터블 오브젝트의 데이터 사본만을 저장하고 이를 참조하는 방식으로 작동 된다.

- 스크립터블 오브젝트 클래스는 유니티에서 기본적으로 제공하는 것으로 모노비헤이비어 클래스와 마찬가지로 기본 유니티 오브젝트(Unity Object)에서 파생되지만, 모노비헤이비어와 달리, 게임 오브젝트에 컴포넌트로 부착할 수 없고, 프로젝트에 에셋으로 저장된다.

## Scriptable Object 만들기

![Alt text](<Images/Scriptable Object 1.png>)

- 굳이 Object에 컴포넌트 추가를 할 필요가 없다
- 아이템의 경우 아이템 클래스를 여러 개 만들어 주면 된다

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = "New Item", menuName = "New Item/item")]
public class Item : ScriptableObject
{
    // 아이템의 이름
    public string itemName;
    // 아이템의 유형
    public ItemType itemType;
    // 아이템의 이미지
    public Sprite itemImage;
    // 아이템의 프리팹
    public GameObject itemPrefab;
    // 무기 유형
    public string weaponType;

    public enum ItemType
    {
        Equipment,
        Used,
        Ingredient,
        ETC
    }

}
```

![Alt text](<Images/Scriptable Object 2.PNG>)