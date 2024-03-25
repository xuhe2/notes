# 显示图片

```python
import cv2 as cv

img = cv.imread('photos/example.png')

cv.imshow('Example Photo', img)

cv.waitKey(0)

cv.destroyAllWindows()
```



# 转换灰度

```python
# Convert to grayscale
gray_img = cv.cvtColor(img, cv.COLOR_BGR2GRAY)

cv.imshow('Example Photo', gray_img)
```



# 修改尺寸

```python
gray_img = cv.resize(gray_img, (500, 500))
```



# 绘制图像

绘制**矩形**

```python
cv.rectangle(img=img, pt1=(100, 100), pt2=(200, 200), color=(0, 0, 255), thickness=2)
```



# 使用摄像头

```python
# 获取摄像头
cap = cv.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break
    face_image = detect_face(frame)
    cv.imshow('Face Detection', face_image)
    if cv.waitKey(1) & 0xFF == ord('q'):
        break
```

使用摄像机, 可以传入视频参数



## 录入人脸

使用`cv.imwrite`写入图片

`cv.waitKey(1) & 0xFF == ord('q')`可以获得输入的按键比较

* 可以直接使用`if cv.waitKey(1) == ord('q'):`来判断, 不需要使用`0xFF`.



# 识别人脸

```python
def detect_face(img):
    gray_img = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
    face_classifier = cv.CascadeClassifier('.venv/Lib/site-packages/cv2/data/haarcascade_frontalface_default.xml')
    faces = face_classifier.detectMultiScale(gray_img)
    for x, y, width, height in faces:
    cv.rectangle(img, (x, y), (x + width, y + height), (0, 255, 0), 2)

    return img
```

改变灰度

使用分类器



# 识别手势

当识别**RGB图像**的时候, 从摄像头中获取的**BGR图像**, 需要**使用`cvtColor`**, 使用的



获取识别手势的模型

```python
# 初始化MediaPipe手势识别模型
mp_hands = mp.solutions.hands
hands = mp_hands.Hands()
```

* 可以传入参数, 使得可以检测更多的数字



转换BGR作为RGB

```python
# 将图像从BGR转换为RGB
image = cv.cvtColor(frame, cv.COLOR_BGR2RGB)
```



处理图像

```python
# 使用MediaPipe模型检测手势
results = hands.process(image)
```

返回值`results`包含参数`multi_hand_landmarks`, 代表手的节点内容

如果判断是否存在被检测到的节点, 进行下一步处理



```python
if results.multi_hand_landmarks:
    for hand_landmarks in results.multi_hand_landmarks:
        mp_drawing.draw_landmarks(frame, hand_landmarks, mp_hands.HAND_CONNECTIONS)
```

绘制函数的第三个参数代表**连接节点的线**



## 设置特殊的连接方法

在`mp_drawing`中设置

```python
# 设定样式
hand_landmark_style = mp_drawing.DrawingSpec(color=(0, 255, 0), thickness=2, circle_radius=4)
hand_connection_style = mp_drawing.DrawingSpec(color=(0, 255, 0), thickness=2)
```

在**绘制的时候传入参数**



## 位置参数

使用的是比例, 从0到1, 最后位置和视窗的大小有关(需要乘上视窗的高度和宽度)

* 视图的大小可以使用`img.shape`来获取(这是一个数组)

```python
# 获取图像的宽度和高度
image_height, image_width, _ = frame.shape
```



获取每个节点的位置

```python
    if results.multi_hand_landmarks:
        for hand_landmarks in results.multi_hand_landmarks:
            mp_drawing.draw_landmarks(frame, hand_landmarks, mp_hands.HAND_CONNECTIONS)
            for i, landmark in enumerate(hand_landmarks.landmark):
                x = int(landmark.x * image_width)
                y = int(landmark.y * image_height)
```



绘制节点文本信息

```python
cv.putText(frame, f"{i}", (x, y), cv.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 1)
```

