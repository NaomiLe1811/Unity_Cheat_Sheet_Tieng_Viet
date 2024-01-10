# Unity_Cheat_Sheet_Tieng_Viet
Bản Unity cheat sheet phiên dịch cho cộng đồng người Việt từ Naomi Le. Cảm ơn các bạn vì đã quan tâm.

# Unity_Cheat_Sheet
## Mục lục
- [Cơ bản](#cơ-bản)
  - [Phím tắt Unity](#phím-tắt-unity)
  - [MonoBehaviour](#monobehaviour)
  - [Sự kiện vật lý (Physics Events)](#sự-kiện-vật-lý)
  - [Serializing](#serializing)
  - [Khởi tạo](#khởi-tạo)
  - [Tìm Đối Tượng Trong Game](#tìm-đối-tượng-trong-game)
  - [Hủy Đối Tượng Trò Chơi](#hủy-đối-tượng-trò-chơi)
  - [Các Thành Phần (Components)](#các-thành-phần)
  - [Hằng Số (Constants)](#hằng-số)
  - [Vectors](#vectors)
  - [Quaternion](#quaternion)
  - [Góc Euler](#góc-euler)
  - [Giữ Tỉ Lệ Màn Hình](#giữ-tỉ-lệ-màn-hình)
- [Di Chuyển & Xoay](#di-chuyển--xoay)
  - [Di Chuyển Đối Tượng](#di-chuyển-đối-tượng)
    - [Transform.Translate()](#transformtranslate)
    - [Vector3.MoveTowards()](#vector3movetowards)
    - [Vector3.Lerp()](#vector3lerp)
    - [Vector3.SmoothDamp()](#vector3smoothdamp)
  - [Xoay Đối Tượng](#xoay-đối-tượng)
    - [Transform.rotation](#transformrotation)
    - [Transform.eulerAngles](#transformeulerangles)
    - [Transform.Rotate()](#transformrotate)
    - [Transform.RotateAround()](#transformrotatearound)
    - [Transform.LookAt()](#transformlookat)
    - [Quaternion.LookRotation()](#quaternionlookrotation)
    - [Quaternion.FromToRotation()](#quaternionfromtorotation)
    - [Quaternion.ToAngleAxis()](#quaterniontoangleaxis)
- [Input](#input)
  - [Bàn Phím](#bàn-phím)
  - [Chuột](#chuột)
  - [Chạm](#chạm)
- [Giao Diện Người Dùng (UI)](#giao-diện-người-dùng-ui)
  - [Nút (Button)](#nút-button)
  - [Thanh Trượt (Slider)](#thanh-trượt-slider)
- [Âm Thanh](#âm-thanh)
  - [Chơi Âm Thanh Cơ Bản](#chơi-âm-thanh-cơ-bản)
- [Mô Hình Thiết Kế](#mô-hình-thiết-kế)
  - [Singleton](#singleton)
- [Các Ứng Dụng Thực Tế](#các-ứng-dụng-thực-tế)
- [Refernces](#refernces)

 ## Cơ Bản

### Phím tắt Unity
  
  | Hành động                         | Phím tắt                                             |
| ---------------------------------- | ---------------------------------------------------- |
| Công cụ Xem (View Tool            |Q                                                        |
| Công cụ Di Chuyển (Move Tool)     |W                                                        |
| Công cụ Xoay (Rotate Tool)        |E                                                        |
| Công cụ Thay Đổi Kích Thước (Scale Tool)      |R                                                        |
| Công cụ Hình Chữ Nhật (Rect Tool)            |T                                                        |
| Công cụ Biến Đổi (Transform Tool)                 |Y                                                        |
| Đối Tượng Trò Chơi Mới (New Game Object)         |Windows: CTRL + SHIFT + N <br> Mac: CMD + SHIFT + N      |
| Đối Tượng Con Mới (New Child Game Object)                |ALT + SHIFT + N                                          |
| Nhân Bản (Duplicate)               |Windows: CTRL + D <br> Mac: CMD +D                       |              
| Chuyển đổi Kích thước cửa sổ (Toggle Window Size)      |SHIFT + SPACE                                            |
| Chơi/Tạm Dừng (Play/Pause)        |Windows: CTRL + P <br> Mac: CMD + P                      |                            
| Tập Trung Đối Tượng Trò Chơi (Focus Game Object)      |F                                                        |
### Visual Studio Code

  | Hành động                         | Phím tắt                                             |
| ---------------------------------- | ---------------------------------------------------- |
| Command Palette                  | Windows: CTRL + SHIFT + P Mac: CMD + SHIFT + P            |
| Quick File Open                   | Windows: CTRL + P Mac: CMD + P                           |
| Toggle Sidebar                    | Windows: CTRL + B Mac: CMD + B                           |
| Multi-Select Cursor               | Windows: CTRL + D Mac: CMD + D                           |
| Copy Line                         | Windows: SHIFT + ALT + UP or SHIFT + ALT + DOWN Mac: OPT + SHIFT + UP or OPT + SHIFT + DOWN |
| Comment Code Block                | Windows: SHIFT + ALT + A (Multi-line comment), CTRL + K + C (Single-line comment) Mac: SHIFT + OPT + A |
| Show All Symbols                  | Windows: CTRL + T Mac: CMD + T                           |
| Trigger suggestion and parameter hints | Windows: Ctrl + Space, Ctrl + Shift + Space Mac: CMD + Space, CMD + Shift + Space |
| Show References                   | Windows: Shift + F12 Mac: Shift + F12                    |
| Global Find                       | Windows: CTRL + SHIFT + F Mac: CMD + SHIFT + F            |

### [MonoBehaviour](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html)
[Đồ thị vòng Lifecycle của MonoBehaviour](https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg)

Tất cả các thành phần được thừa kế từ lớp MonoBehaviour thực hiện một loạt các hàm sự kiện theo một thứ tự xác định. Các hàm này bao gồm:
```csharp
Awake(): Được gọi sau khi một đối tượng trò chơi được khởi tạo.
OnEnable(): Được gọi khi một đối tượng trò chơi được kích hoạt.
Start(): Được gọi trước khi khung hình đầu tiên được cập nhật.
Update(): Gọi mỗi khung hình.
LateUpdate(): Được gọi mỗi khung hình sau khi hàm Update().
OnBecameVisible(): Được gọi khi đối tượng trò chơi hiện tại trở nên hiển thị thông qua bất kỳ camera nào.
OnBecameInvisible(): Được gọi khi đối tượng trò chơi hiện tại không còn hiển thị qua bất kỳ camera nào.
OnDrawGizmos(): Được gọi để vẽ gizmos trong cửa sổ scene.
OnGUI(): Được gọi nhiều lần cho các sự kiện GUI.
OnApplicationPause(): Được gọi khi trò chơi tạm dừng thông qua Unity editor.
OnDisable(): Thực thi khi đối tượng trò chơi bị tắt.
OnDestroy(): Được kích hoạt khi đối tượng trò chơi bị hủy.
```
Có một hàm vòng đời được gọi là `FixedUpdate`, được kích hoạt một số lần cố định mỗi giây. Bạn có thể cấu hình tần suất trong `Edit ▸ Project Settings ▸ Time ▸ Fixed Timestep`.

## Sự kiện vật lý
Nếu bạn thêm một thành phần collider vào một đối tượng trong game, bạn có thể phát hiện sự kiện va chạm từ các thành phần của bạn bằng cách định nghĩa một bộ phận cụ thể của các phương thức. Các phương thức sau chỉ được gọi khi bạn có một Collider hoặc Rigid Body component trên cả hai đối tượng trong game.
- OnCollisionEnter - Phương thức này được gọi một lần khi một đối tượng khác va chạm với đối tượng game hiện tại.
- OnCollisionStay - Phương thức này được gọi trong mỗi khung hình khi một đối tượng khác va chạm với đối tượng game hiện tại.
- OnCollisionExit - Phương thức này được gọi một lần khi một đối tượng rời khỏi vùng va chạm của đối tượng hiện tại.

```csharp
private void OnCollisionEnter(Collision hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnCollisionStay(Collision hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnCollisionExit(Collision hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```
Các hàm sau chỉ được gọi khi tùy chọn "On Trigger" được bật từ thành phần collider tương ứng.
-OnTriggerEnter - Hàm này được gọi khi một đối tượng khác va chạm với đối tượng game hiện tại.
-OnTriggerStay - Hàm này được gọi trong mỗi khung hình khi một đối tượng khác va chạm với đối tượng game hiện tại.
-OnTriggerExit - Hàm này được gọi một lần khi một đối tượng rời khỏi vùng va chạm của đối tượng hiện tại.
```csharp
private void OnTriggerEnter(Collider hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnTriggerStay(Collider hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnTriggerExit(Collider hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```
Cuối cùng, có các hàm tương ứng cho các collider 2D. Các hàm này chia sẻ cùng tên với các hàm 3D, nhưng có từ "2D" được thêm vào cuối. Tương tự, kiểu tham số cũng giống nhau, nhưng thay vì Collision, ta có Collision2D.
- OnCollisionEnter2D
- OnCollisionStay2D
- OnCollisionExit2D
- OnTriggerEnter2D
- OnTriggerStay2D
- OnTriggerExit2D
```csharp
private void OnCollisionEnter2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnCollisionStay2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnCollisionExit2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
private void OnTriggerEnter2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnTriggerStay2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnTriggerExit2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```

### Serializing
Unity có khả năng serialize các biến, chuyển đổi dữ liệu thành một định dạng có thể chỉnh sửa từ trình soạn thảo Unity. Quá trình serialization phụ thuộc vào các thuộc tính hoặc các trình điều khiển truy cập được áp dụng cho biến.

Nếu một biến là public, nó sẽ được tự động serialize:

```csharp
public int age = 10;
```

Nếu bạn không muốn biến public được serialize, bạn có thể sử dụng thuộc tính NonSerialized từ namespace System như sau:

```csharp
[NonSerialized] public int age = 10;
```

Biến private không được serialize mặc định. Tuy nhiên, nếu bạn muốn chúng được serialize, Unity có một thuộc tính gọi là SerializeField trong namespace Unity. Bạn có thể áp dụng nó như sau:

```csharp
[SerializeField] private int age = 10;
```
## Khởi tạo
Các đối tượng game mới có thể được chèn vào cảnh một cách tự động thông qua việc gọi hàm sau. Hàm này có ba đối số.

- Đối tượng Game - The Game Object 
- (Optional) Vị trí Toàn cầu - Global Position
- (Optional) Quay - Rotation
```csharp
Instantiate(someGameObject);
Instantiate(someGameObject, new Vector3(0, 0, 10));
Instantiate(someGameObject, new Vector3(0, 0, 10), Quaternion.identity);
```
## Tìm Đối Tượng Trong Game
Lớp GameObject có một số phương thức để tìm kiếm đối tượng game trong cấu trúc thư mục.

- Find() - Tìm kiếm một đối tượng game dựa trên tên của nó.
- FindGameObjectsWithTag() - Tìm nhiều đối tượng game được lưu trữ trong một mảng và trả về. Sử dụng tag của đối tượng game để tìm chúng.
- FindWithTag() - Tìm một đối tượng game dựa trên tag của nó.
```csharp
GameObject myObj = GameObject.Find("NAME IN HIERARCHY");
GameObject myObj = GameObject.FindGameObjectsWithTag("TAG");
GameObject myObj = GameObject.FindWithTag("TAG");
```

## Hủy Đối Tượng Trò Chơi
Đối tượng game có thể bị hủy bằng cách gọi hàm Destroy():
```csharp
Destroy(gameObject);
```
## Các Thành Phần (Components)
Các đối tượng game tự nhiên không có nhiều chức năng. Chúng ta cần thêm các thành phần để có các chức năng cụ thể. Nếu bạn đang sử dụng các thành phần tùy chỉnh và cần chọn lựa các thành phần khác, Unity cung cấp cách để lấy chúng. Phương pháp đầu tiên là sử dụng hàm GetComponent(), thường bằng cách chỉ định tên lớp thành phần.
```csharp
AudioSource audioSource = GetComponent<AudioSource>();
```
Hoặc bạn có thể sử dụng từ khóa typeof và xác nhận giá trị như sau:
```csharp
AudioSource audioSource = GetComponent(typeof(AudioSource)) as AudioSource;
```
Cuối cùng, bạn có thể truyền vào tên của thành phần dưới dạng chuỗi như sau:
```csharp
AudioSource audioSource = GetComponent("AudioSource") as AudioSource;
```
## Hằng Số (Constants)
Trong Unity, bạn có thể sử dụng hằng số để định nghĩa các giá trị giữ nguyên trong toàn bộ kịch bản của bạn. Dưới đây là cách bạn có thể sử dụng hằng số trong Unity:

1. Khai Báo Một Hằng Số:
Sử dụng từ khoá const để khai báo một hằng số. Hằng số phải được khởi tạo giá trị tại thời điểm khai báo và không thể thay đổi sau đó. Dưới đây là một ví dụ:
```csharp
public class ExampleScript : MonoBehaviour
{
    // Define a constant for gravity
    private const float Gravity = 9.8f;

    void Start()
    {
        // Use the constant in your code
        float fallSpeed = Gravity * Time.deltaTime;
    }
}
```
2. Lợi Ích của Hằng Số:
Hằng số mang lại những lợi ích quan trọng khi định nghĩa các giá trị được sử dụng ở nhiều nơi trong mã của bạn và không nên được sửa đổi trong thời gian chạy. Chúng giúp mã của bạn trở nên dễ đọc và dễ bảo trì hơn.

3. Sử Dụng Trong Unity:
Bạn có thể sử dụng hằng số trong nhiều kịch bản Unity khác nhau, chẳng hạn như các kịch bản MonoBehaviour được đính kèm vào GameObjects hoặc các kịch bản tiện ích. Hằng số thường được sử dụng cho các giá trị như tốc độ mặc định, kích thước cố định hoặc các tham số không thay đổi khác.

4. Phạm Vi của Hằng Số:
Hằng số có phạm vi giới hạn trong lớp hoặc phương thức mà chúng được khai báo. Nếu bạn cần hằng số có thể truy cập từ nhiều kịch bản, hãy xem xét việc sử dụng một lớp public static.

Dưới đây là một ví dụ đơn giản:
```csharp
public static class GameConstants
{
    public const int MaxScore = 100;
}

public class ScoreManager : MonoBehaviour
{
    void Update()
    {
        // Access the constant from another script
        int currentScore = CalculateScore();
        if (currentScore >= GameConstants.MaxScore)
        {
            Debug.Log("You reached the maximum score!");
        }
    }

    int CalculateScore()
    {
        // Your score calculation logic here
        return 50;
    }
}
```
## Vectors
Vectors quyết định vị trí của các đối tượng trong game và hỗ trợ trong các phép tính về khoảng cách và chuyển động. Unity có hai lớp vector: Vector2 cho các trò chơi 2D với tọa độ (x, y), và Vector3 cho các trò chơi 3D với tọa độ (x, y, z). Trong các lớp này, X đại diện cho Bên trái/Phải, Y biểu thị Lên/Xuống, và Z cho Tiến lên/Lùi lại. Unity cung cấp các hằng số có thể truy cập từ lớp vector tương ứng.
#### Vector 3
```csharp
Vector3 V = new Vector3(0f; 0f; 0f);
```
```csharp
Vector3.right /* (1, 0, 0)  */
Vector3.left /* (-1, 0, 0)  */
Vector3.up /* (0, 1, 0)  */
Vector3.down /* (0, -1, 0)  */
Vector3.forward /* (0, 0, 1)  */
Vector3.back /* (0, 0, -1) */
Vector3.zero /* (0, 0, 0)  */
Vector3.one /* (1, 1, 1)  */
```
#### Vector 2

```csharp
Vector2.right /* (1, 0)  */
Vector2.left  /* (-1, 0) */
Vector2.up    /* (0, 1)  */
Vector2.down  /* (0, -1) */
Vector2.zero  /* (0, 0)  */
Vector2.one   /* (1, 1)  */
```
Nếu bạn chỉ quan tâm đến hướng của một vector cụ thể, bạn có thể truy cập thuộc tính normalized của nó như sau:
```csharp
myVector.normalized
```
Khoảng cách giữa hai vector có thể được tính bằng phương thức Vector3.Distance(), trả về một giá trị kiểu float:
```csharp
float distance = Vector3.Distance(vectorOne, vectorTwo);
```
### Quaternion
Quaternions điều khiển xoay của game object. Bạn có thể kiểm tra hoặc thay đổi xoay của đối tượng bằng cách sử dụng transform.rotation. Hàm Quaternion.LookRotation() của Unity tạo ra một xoay dựa trên một vị trí mục tiêu.
```csharp
Quaternion.LookRotation(gameObjectPosition);
```
Một xoay 30 độ quanh trục y:
```csharp
Quaternion rotation = Quaternion.Euler(0, 30, 0);
```
### Góc Euler
Góc Euler là "góc độ" như 90, 180, 45, 30 độ. Tuy nhiên, quaternion khác biệt so với góc Euler ở chỗ nó biểu diễn một điểm trên Mặt cầu Đơn vị (bán kính là 1 đơn vị).

Ví dụ sử dụng Quaternion để biểu diễn 30 độ xoay quanh trục X và 10 độ xoay quanh trục Y:
```csharp
Quaternion rotation = Quaternion.Euler(30, 10, 0);
```
Sử dụng một Vector để biểu diễn cũng là một cách khác:
```csharp
Vector3 EulerRotation = new Vector3(30, 10, 0);
Quaternion rotation = Quaternion.Euler(EulerRotation);
```
Chuyển đổi góc Quaternion của một transform thành góc Euler
```csharp
Quaternion quaternionAngles = transform.rotation;
Vector3 eulerAngles = quaternionAngles.eulerAngles;
```
### Giữ Tỉ Lệ Màn Hình
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ScaleBackground : MonoBehaviour
{
    private SpriteRenderer background;
    private Camera cam;

    void Start()
    {
        background = GetComponent<SpriteRenderer>();
        cam = Camera.main;

        // Lấy kích thước của camera
        float cameraHeight = 2f * cam.orthographicSize;
        float cameraWidth = cameraHeight * cam.aspect;

        // Lấy kích thước của nền hiện tại
        float bgHeight = background.sprite.bounds.size.y;
        float bgWidth = background.sprite.bounds.size.x;

        // Tính tỉ lệ tỷ lệ
        float scaleX = cameraWidth / bgWidth;
        float scaleY = cameraHeight / bgHeight;

        // Áp dụng tỷ lệ cho nền
        transform.localScale = new Vector3(scaleX, scaleY, 1f);
    }
  }
}
```
## Di Chuyển & Xoay
### Di Chuyển Đối Tượng
#### Transform.Translate()
```csharp
// Cũng có thể nhảy bằng cách đặt nút Space trong Input Manager
public void Translate(Vector3 translation);
public void Translate(Vector3 translation, Space relativeTo = Space.Self);

transform.Translate(Vector3.right * movementSpeed);
```

#### Vector3.MoveTowards()
```csharp
// Tính toán vị trí giữa các điểm được chỉ định bởi current và target
// Di chuyển không xa hơn khoảng cách được chỉ định bởi maxDistanceDelta
public static Vector3 MoveTowards(Vector3 current, Vector3 target, float maxDistanceDelta);

Vector3 targetPosition;
transform.position = Vector3.MoveTowards(transform.position, targetPosition, Time.deltaTime);
```

#### Vector3.Lerp()
```csharp
// Nội suy tuyến tính giữa hai điểm. Kết quả là một chuyển động mượt mà.
public static Vector3 Lerp(Vector3 startValue, Vector3 endValue, float interpolationRatio);

Vector3 targetPosition;
float t = 0;
t += Time.deltaTime * speed;
transform.position = Vector3.Lerp(transform.position, targetPosition, t);
```

#### Vector3.SmoothDamp()
```csharp
// Dần dần thay đổi một vector đến một mục tiêu mong muốn trong thời gian.
// Vector được làm mịn bằng một hàm giống như lò xo-dẫn, sẽ không bao giờ vượt quá.
// Sử dụng phổ biến nhất là để làm mịn cho camera theo dõi.
public static Vector3 SmoothDamp(Vector3 current, Vector3 target, ref Vector3 currentVelocity, float smoothTime, float maxSpeed = Mathf.Infinity, float deltaTime = Time.deltaTime);

float smoothTime = 1f;
Vector3 velocity;
Vector3 targetPosition = target.TransformPoint(new Vector3(0, 5, -10));
// Di chuyển mượt mà camera đến vị trí mục tiêu đó
transform.position = Vector3.SmoothDamp(transform.position, targetPosition, ref velocity, smoothTime);
```

### Xoay Đối Tượng
#### Transform.rotation
```csharp
// Một Quaternion lưu trữ sự quay của Transform trong không gian thế giới.
// Quaternions dựa trên số phức và không gặp vấn đề gimbal lock.
// Unity sử dụng Quaternion để biểu diễn tất cả các phép quay nội tại.

transform.rotation = new Quaternion(rotx, roty, rotz, rotw);
```

#### Transform.eulerAngles
```csharp
// Transform.eulerAngles biểu diễn phép quay trong không gian thế giới. 
// Quan trọng để hiểu rằng mặc dù bạn cung cấp các giá trị quay X, Y và Z để mô tả phép quay của bạn
// những giá trị đó không được lưu trữ trong phép quay. Thay vào đó, các giá trị X, Y & Z được chuyển đổi vào định dạng nội tại của Quaternion.

transform.eulerAngles = Vector3(rotx, roty, rotz);
```

#### Transform.Rotate()
```csharp
// Áp dụng phép quay xung quanh tất cả các trục được cung cấp.
public void Rotate(Vector3 eulers, Space relativeTo = Space.Self);
public void Rotate(float xAngle, float yAngle, float zAngle, Space relativeTo = Space.Self);

transform.Rotate(rotx, roty, rotz);
```

#### Transform.RotateAround()
```csharp
// Quay đối tượng xung quanh trục đi qua điểm trong tọa độ thế giới với góc quay là angle độ.
public void RotateAround(Vector3 point, Vector3 axis, float angle);

// Xoay đối tượng xung quanh mục tiêu ở 20 độ/giây.
Transform target;
transform.RotateAround(target.position, Vector3.up, 20 * Time.deltaTime);
```

#### Transform.LookAt()
```csharp
// Chỉ hướng phía trước ('Z' tích cực) của đối tượng đến một vị trí trong không gian thế giới.
public void LookAt(Transform target);
public void LookAt(Transform target, Vector3 worldUp = Vector3.up);

// Quay vector phía trước của đối tượng để chỉ đến Transform mục tiêu.
Transform target;
transform.LookAt(target);

// Giống như trên, nhưng đặt tham số worldUp thành Vector3.left trong ví dụ này làm cho đối tượng nghiêng về một bên.
transform.LookAt(target, Vector3.left);
```

#### Quaternion.LookRotation()
```csharp
// Tạo một quay xoay với hướng cụ thể của forward và upwards được chỉ định.
public static Quaternion LookRotation(Vector3 forward, Vector3 upwards = Vector3.up);

// Đoạn mã dưới đây quay đối tượng hướng về một đối tượng mục tiêu.
Vector3 direction = target.position - transform.position;
Quaternion rotation = Quaternion.LookRotation(direction);
transform.rotation = rotation;
```

#### Quaternion.FromToRotation()
```csharp
// Tạo ra một quay (Quaternion) xoay từ hướng fromDirection đến toDirection.
public static Quaternion FromToRotation(Vector3 fromDirection, Vector3 toDirection);

// Đặt quay sao cho trục y của transform nằm dọc theo trục z.
transform.rotation = Quaternion.FromToRotation(Vector3.up, transform.forward);
```

#### Quaternion.ToAngleAxis()
```csharp
// Chuyển đổi quay thành biểu diễn góc-trục (góc theo đơn vị độ).
// Nói cách khác, trích xuất góc cũng như trục mà quaternion này đại diện.
public void ToAngleAxis(out float angle, out Vector3 axis);

// Trích xuất góc quay - trục từ quay của transform
float angle = 0.0f;
Vector3 axis = Vector3.zero;
transform.rotation.ToAngleAxis(out angle, out axis);
```
## Input

### Bàn Phím

```csharp
// Trả về true trong suốt frame khi người dùng bắt đầu nhấn xuống phím
if (Input.GetKeyDown(KeyCode.Space)) {
    Debug.Log("Space key was pressed");
}

// Chức năng nhảy cũng được đặt cho phím Space trong Input Manager
if (Input.GetButtonDown("Jump")) {
    Debug.Log("Do something");
}
```

### Chuột

```csharp
if (Input.GetAxis("Mouse X") < 0) {
    Debug.Log("Mouse moved left");
}

if (Input.GetAxis("Mouse Y") > 0) {
    Debug.Log("Mouse moved up");
}

if (Input.GetMouseButtonDown(0)) {
    Debug.Log("Pressed primary button.");
}

if (Input.GetMouseButtonDown(1)) {
    Debug.Log("Pressed secondary button.");
}

if (Input.GetMouseButtonDown(2)) {
    Debug.Log("Pressed middle click.");
}
```

### Chạm
```csharp
if (Input.touchCount > 0) {
    touch = Input.GetTouch(0);

    if (touch.phase == TouchPhase.Began) {
        Debug.Log("Touch began");
    }

    if (touch.phase == TouchPhase.Moved) {
        Debug.Log("Touch moves");
    }

    if (touch.phase == TouchPhase.Ended) {
        Debug.Log("Touch ended");
    }
}
```

## Giao Diện Người Dùng (UI)

```csharp

### Nút (Button)
// Button được sử dụng để xử lý sự nhấn và tương tác của người dùng.
// Gắn kịch bản này vào một thành phần Button để phản ứng với sự nhấp vào nút.

using UnityEngine.UI;

Button myButton = GetComponent<Button>();
myButton.onClick.AddListener(MyButtonClickHandler);

void MyButtonClickHandler() {
    Debug.Log("Button Clicked!");
}
```

### Thanh Trượt (Slider)
```csharp
// Slider được sử dụng để chọn một giá trị trong khoảng.
// Gắn kịch bản này vào một thành phần Slider để phản ứng với sự thay đổi giá trị.

using UnityEngine.UI;

Slider mySlider = GetComponent<Slider>();
mySlider.onValueChanged.AddListener(MySliderValueChangedHandler);

void MySliderValueChangedHandler(float value) {
    Debug.Log("Slider Value: " + value);
}
```

## Âm Thanh

### Chơi Âm Thanh Cơ Bản

```csharp
public class PlayAudio : MonoBehaviour {
    public AudioSource audioSource;

    void Start() {
        // Gọi Play trên một Audio Source đang phát sẽ khiến nó bắt đầu từ đầu.
        audioSource.Play();
    }
}
```


## Mô Hình Thiết Kế
### Singleton

```csharp
// Định nghĩa lớp singleton
public class SingletonClass: MonoBehaviour {
    private static SomeClass instance;

    public static SomeClass Instance { get { return instance; } }

    private void Awake() {
        if (instance != null && instance != this) {
            Destroy(this.gameObject);
        } else {
            instance = this;
        }
    }
}

// Sử dụng nó trong một lớp khác
public class AnotherClass: MonoBehaviour {
    public Singleton instance;

    private void Awake() {
       instance = Singleton.Instance;
    }
}
```
## References

LUIS RAMIREZ JR. (Unity Game Development Cheat Sheet)

Ozan Kaşıkçı (Unity Cheat Sheet)

