# ReactNative初识

>ReactNative  是基于  React  这门框架语法来进行开发的
>
>ReactNative，提供了移动端专用的组件，这时候在网页中常用的一些元素，如div，p，img都不能用了，只能使用  ReactNative  中的组件
>
>最终开发出来的项目是要运行到手机上的，如何把一个  ReactNative  项目发布到手机上，这里需要结合安卓的签名打包步骤，并使用  ReactNative  提供的打包命令，进行完整的  apk  文件的发布，最终发布出来的就是  Release  版本的项目，可以上传到应用商店

## PC端的配置





## 移动端的配置

- 需要先开启手机的  开发模式

- 使用数据线，把手机连接到电脑上

- 在`cmd`上运行`adb devices`的命令，这个命令是安卓开发环境提供的，运行后，会显示自己的设备

- 以上如果还是不能看到自己的设备，则尝试安装**豌豆荚**这样的工具，让这些工具帮助在电脑上安装手机驱动

  



## 创建项目

第一步：`react-native init  app`   app是项目名字

第二步：项目初始化好后，根据  IOS  和  Android的提示，选择相关的系统开发



## 注意事项

- 在ReactNative中，只能使用`.js`为后缀名的文件，不能使用`.jsx`了

- ReactNative中提供了  View  组件，相当于网页上的  div  `import { View } from  'react-native'`
- 在  RN  中，所有的文本，必须使用  RN  组件提供的  Text  组件进行包裹，否则报错 `import {Text} from 'react-native'`
- 使用  flex  布局，在  RN  中，主轴默认是纵向的
- 不推荐使用  npm  下载包

## 常用的组件

- View
- Text
- TextInput
- Image：网络上的图片   需要设置图片的宽高
- Button：button  必须要有  title  属性，作为  value  值显示出来   也必须要有  onPress  属性
- ActivityIndicator：加载中
- ScrollView
- ListView：官方不建议使用了  用  FlatLIst  代替

























