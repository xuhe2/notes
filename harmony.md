题目:

```
@Link变量不能在组件内部进行初始化。
```

```
API9及以上，router.pushUrl()方法的mode参数可以配置为以下哪几种跳转页面使用的模式？
A. Standard B. Single
```

```
UIAbility有哪几种的启动模式？
A. multiton
B. singleton
C. specified
```

```
UIAbility启动模式需要在module.json5文件中配置哪个字段？
launchType
```



# 组件状态管理

当用户交互的时候, 带动UI自动的更新界面



## 组件内的状态管理：@State

```
@Component
export default struct TargetListItem {
  @State isExpanded: boolean = false;
  ...

  build() {
    ...
      Column() {
        ...
        if (this.isExpanded) {
          Blank()
          ProgressEditPanel(...)
        }
      }
      .height(this.isExpanded ? $r('app.float.expanded_item_height')                  
      : $r('app.float.list_item_height'))
      .onClick(() => {
        ...
             this.isExpanded = !this.isExpanded;
        ...
       })
    ...
  }
}
```



## 从父组件单向同步状态：@Prop

当子组件中的状态依赖从父组件传递而来时，需要使用@Prop装饰器，@Prop修饰的变量可以和其父组件中的状态建立单向同步关系。当父组件中状态变化时，该状态值也会更新至@Prop修饰的变量；对@Prop修饰的变量的修改不会影响其父组件中的状态。

```
@Component
export default struct TargetListItem {
   @Prop isEditMode: boolean;
   ...
       Column() {
        ...
       }
       .padding({
        ...
        right: this.isEditMode ? $r('app.float.list_edit_padding') 
               : $r('app.float.list_padding')
       })
       ...

       if (this.isEditMode) {
        Row() {
           Checkbox()...
        }
       }
  ...
}
```



## 与父组件双向同步状态：@Link

若是父子组件状态需要相互绑定进行双向同步时，可以使用@Link装饰器。父组件中用于初始化子组件@Link变量的必须是在父组件中定义的状态变量。



## 跨组件层级双向同步状态：@Provide和@Consume



# Video组件

| 参数名              | 参数类型                            | 必填 |
| ------------------- | ----------------------------------- | ---- |
| src                 | string \| Resource                  | 否   |
| currentProgressRate | number \| string \| PlaybackSpeed8+ | 否   |
| previewUri          | string \| PixelMap8+ \| Resource    | 否   |
| controller          | VideoController                     | 否   |

```
@Component
export struct VideoPlayer {
  private source: string | Resource;
  private controller: VideoController;
  private previewUris: Resource = $r('app.media.preview');
  ...

  build() {
    Column() {
      Video({
        src: this.source,
        previewUri: this.previewUris,
        controller: this.controller
      })
        ...
      VideoSlider({ controller: this.controller })
    }
  }
}
```



# 弹窗

- 确认类：例如警告弹窗AlertDialog。
- 选择类：包括文本选择弹窗TextPickerDialog 、日期滑动选择弹窗DatePickerDialog、时间滑动选择弹窗TimePickerDialog等。



使用`primary button`和`second button`设置按钮

使用`confirm`来设置只能点击**确定**的情况