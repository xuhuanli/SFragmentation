![](https://img.shields.io/github/v/release/weikaiyun/EasyFragmentation.svg)
[![](https://jitpack.io/v/weikaiyun/EasyFragmentation.svg)](https://jitpack.io/#weikaiyun/EasyFragmentation)
# SFragmentation(Super Fragmentation)


### fork from https://github.com/weikaiyun/SFragmentation
#### 框架负责管理fragment的各种操作，相比于google新出的navigation框架，更加灵活多变，易于使用。
#### 框架对于fragment可见性判断，懒加载，转场动画有比较好的处理。
#### 框架的源码简单易懂， 不存在复杂的逻辑。

### 推荐使用NoBackStack分支。

#### gradle使用:

```
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```
```
dependencies {
	//请使用最新版本
	implementation 'com.github.weikaiyun.SFragmentation:fragmentation:latest'
	//滑动返回，可选
	implementation 'com.github.weikaiyun.SFragmentation:fragmentation_swipeback:latest'
}
```
##### demo有比较详细的使用示例， 欢迎star。
下面2,3,4,5中API的用法，有对应的childFragment的操作接口，使用过程中请务必弄清楚fragment的层级关系，使用对应的接口！！！

##### 1. Application初始化API

```
Fragmentation.builder() // 设置 栈视图 模式为 （默认）悬浮球模式   SHAKE: 摇一摇唤出  NONE：隐藏， 仅在Debug环境生效
            .stackViewMode(Fragmentation.BUBBLE)
            .debug(true) // 实际场景建议.debug(BuildConfig.DEBUG)
            .animation(R.anim.v_fragment_enter, R.anim.v_fragment_pop_exit, R.anim.v_fragment_pop_enter, R.anim.v_fragment_exit) //设置默认动画
            .install()
```

##### 2. 装载根Fragment
```
// 装载根Fragment, 即Activity内的第一个Fragment 或 Fragment内的第一个子Fragment
loadRootFragment(int containerId, SupportFragment toFragment)

// 装载多个根Fragment，用于同级Fragment的场景，详情见DemoMainFragment
loadMultipleRootFragment(int containerId, int showPosition, SupportFragment... toFragments);

```

##### 3. 同级fragment切换

```
showHideFragment(SupportFragment showFragment, SupportFragment hideFragment);
```

##### 4. 启动fragment
```
// 启动新的Fragment，启动者和被启动者是平级的
start(SupportFragment fragment)

// 以某种启动模式，启动新的Fragment
start(SupportFragment fragment, int launchMode)

// 启动新的Fragment，并能接收到新Fragment的数据返回
startForResult(SupportFragment fragment,int requestCode)

// 启动目标Fragment，并关闭当前Fragment
startWithPop(SupportFragment fragment)

// 启动目标Fragment，并关闭targetFragment之上的Fragments
startWithPopTo(SupportFragment fragment, Class targetFragment, boolean includeTargetFragment)

// 你可以使用extraTransaction() + start() 来实现上面的各种startXX()设置更多功能
supportFragment.extraTransaction()

```

##### 5. 回退fragment
```
// 出栈当前Fragment(在当前Fragment所在栈内pop)
pop();

// 出栈targetFragment之上的所有Fragments
popTo(Class targetFragment, boolean includeTargetFragment);

```

##### 6. 输入法相关
```
// 隐藏软键盘 一般用在hide时
hideSoftInput();

// 显示软键盘，调用该方法后，会在onPause时自动隐藏软键盘
showSoftInput(View view);

```

##### 7. 可见性
```
//可见
onVisible();

//不可见
onInvisible();

```

#####  如有使用问题欢迎提交issues


***
#### Thanks to [Fragmentation](https://github.com/YoKeyword/Fragmentation)。
***
### LICENSE
```
Copyright 2019 weikaiyun

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
