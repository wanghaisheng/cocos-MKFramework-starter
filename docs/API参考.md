# MKFramework API 参考文档

## 概述

本文档提供了 MKFramework 核心 API 的详细参考，帮助开发者更好地理解和使用框架提供的功能。

## 装饰器 API

### 类型装饰器

```typescript
/**
 * 类型装饰器，用于标记和注册类
 * @param name 类型名称
 */
mk.type(name: string): ClassDecorator
```

**示例：**

```typescript
@mk.type("PlayerController")
class PlayerController extends cc.Component {
    // 组件实现
}
```

### 方法装饰器

#### 日志装饰器

```typescript
/**
 * 日志装饰器，记录方法的调用信息
 */
mk.method.log: MethodDecorator
```

**示例：**

```typescript
@mk.method.log
public movePlayer(x: number, y: number): void {
    // 方法实现
}
```

#### 防抖装饰器

```typescript
/**
 * 防抖装饰器，限制方法在指定时间内只能调用一次
 * @param wait 等待时间（毫秒）
 */
mk.method.debounce(wait: number): MethodDecorator
```

**示例：**

```typescript
@mk.method.debounce(300)
private onButtonClick(): void {
    // 按钮点击处理
}
```

#### 节流装饰器

```typescript
/**
 * 节流装饰器，限制方法在指定时间内的调用频率
 * @param wait 等待时间（毫秒）
 */
mk.method.throttle(wait: number): MethodDecorator
```

**示例：**

```typescript
@mk.method.throttle(100)
private onMouseMove(event: cc.Event.EventMouse): void {
    // 鼠标移动处理
}
```

### 导出装饰器

```typescript
/**
 * 导出装饰器，将类导出到全局命名空间
 */
mk.export: ClassDecorator
```

**示例：**

```typescript
@mk.export
@mk.type("GameManager")
class GameManager {
    // 实现
}
```

## 工具类 API

### 数学工具 (tool_math)

```typescript
/**
 * 生成指定范围内的随机数
 * @param min 最小值
 * @param max 最大值
 * @returns 随机数
 */
mk.tool.math.random(min: number, max: number): number

/**
 * 角度转弧度
 * @param degrees 角度
 * @returns 弧度
 */
mk.tool.math.degToRad(degrees: number): number

/**
 * 弧度转角度
 * @param radians 弧度
 * @returns 角度
 */
mk.tool.math.radToDeg(radians: number): number

/**
 * 线性插值
 * @param a 起始值
 * @param b 目标值
 * @param t 插值系数 (0-1)
 * @returns 插值结果
 */
mk.tool.math.lerp(a: number, b: number, t: number): number
```

### 节点工具 (tool_node)

```typescript
/**
 * 查找子节点
 * @param node 父节点
 * @param path 路径
 * @returns 子节点
 */
mk.tool.node.find(node: cc.Node, path: string): cc.Node | null

/**
 * 创建节点
 * @param name 节点名称
 * @returns 新节点
 */
mk.tool.node.create(name: string): cc.Node

/**
 * 获取节点上的组件，如果不存在则添加
 * @param node 目标节点
 * @param type 组件类型
 * @returns 组件实例
 */
mk.tool.node.getOrAddComponent<T extends cc.Component>(node: cc.Node, type: new () => T): T
```

### 字符串工具 (tool_string)

```typescript
/**
 * 格式化字符串
 * @param format 格式字符串
 * @param args 参数列表
 * @returns 格式化后的字符串
 */
mk.tool.string.format(format: string, ...args: any[]): string

/**
 * 生成UUID
 * @returns UUID字符串
 */
mk.tool.string.uuid(): string

/**
 * 检查字符串是否为空或仅包含空白字符
 * @param str 要检查的字符串
 * @returns 是否为空
 */
mk.tool.string.isEmpty(str: string): boolean
```

### 对象工具 (tool_object)

```typescript
/**
 * 深拷贝对象
 * @param obj 源对象
 * @returns 拷贝后的对象
 */
mk.tool.object.deepCopy<T>(obj: T): T

/**
 * 合并对象
 * @param target 目标对象
 * @param source 源对象
 * @returns 合并后的对象
 */
mk.tool.object.merge<T>(target: T, source: Partial<T>): T
```

### 字节工具 (tool_byte)

```typescript
/**
 * 字符串转字节数组
 * @param str 字符串
 * @returns 字节数组
 */
mk.tool.byte.stringToBytes(str: string): Uint8Array

/**
 * 字节数组转字符串
 * @param bytes 字节数组
 * @returns 字符串
 */
mk.tool.byte.bytesToString(bytes: Uint8Array): string
```

### 贝塞尔曲线工具 (tool_bezier_curve)

```typescript
/**
 * 计算二次贝塞尔曲线上的点
 * @param t 参数 (0-1)
 * @param p0 起点
 * @param p1 控制点
 * @param p2 终点
 * @returns 曲线上的点
 */
mk.tool.bezierCurve.quadratic(t: number, p0: cc.Vec2, p1: cc.Vec2, p2: cc.Vec2): cc.Vec2

/**
 * 计算三次贝塞尔曲线上的点
 * @param t 参数 (0-1)
 * @param p0 起点
 * @param p1 控制点1
 * @param p2 控制点2
 * @param p3 终点
 * @returns 曲线上的点
 */
mk.tool.bezierCurve.cubic(t: number, p0: cc.Vec2, p1: cc.Vec2, p2: cc.Vec2, p3: cc.Vec2): cc.Vec2
```

### 加载工具 (tool_loading)

```typescript
/**
 * 显示加载界面
 * @param text 加载提示文本
 */
mk.tool.loading.show(text?: string): void

/**
 * 隐藏加载界面
 */
mk.tool.loading.hide(): void

/**
 * 更新加载进度
 * @param progress 进度值 (0-1)
 */
mk.tool.loading.updateProgress(progress: number): void
```

## 热更新 API

```typescript
/**
 * 检查是否有更新
 * @returns 是否有更新
 */
mk.hotUpdate.check(): Promise<boolean>

/**
 * 执行更新
 * @param progressCallback 进度回调
 * @returns 更新结果
 */
mk.hotUpdate.update(progressCallback?: (progress: number) => void): Promise<boolean>

/**
 * 重启应用以应用更新
 */
mk.hotUpdate.restart(): void
```

## 资源管理 API

```typescript
/**
 * 加载资源包
 * @param name 资源包名称
 * @returns 资源包
 */
mk.resource.loadBundle(name: string): Promise<cc.AssetManager.Bundle>

/**
 * 预加载资源
 * @param bundle 资源包名称
 * @param path 资源路径
 * @param type 资源类型
 */
mk.resource.preload<T extends cc.Asset>(bundle: string, path: string, type: new () => T): Promise<void>

/**
 * 加载资源
 * @param bundle 资源包名称
 * @param path 资源路径
 * @param type 资源类型
 * @returns 资源
 */
mk.resource.load<T extends cc.Asset>(bundle: string, path: string, type: new () => T): Promise<T>

/**
 * 释放资源
 * @param asset 要释放的资源
 */
mk.resource.release(asset: cc.Asset): void

/**
 * 释放资源包
 * @param name 资源包名称
 */
mk.resource.releaseBundle(name: string): void
```

## 多语言 API

```typescript
/**
 * 设置当前语言
 * @param lang 语言代码
 */
mk.i18n.setLanguage(lang: string): void

/**
 * 获取当前语言
 * @returns 当前语言代码
 */
mk.i18n.getLanguage(): string

/**
 * 获取翻译文本
 * @param key 翻译键
 * @param params 替换参数
 * @returns 翻译后的文本
 */
mk.i18n.t(key: string, params?: Record<string, any>): string
```

## 音频 API

```typescript
/**
 * 播放音效
 * @param clip 音频剪辑或路径
 * @param volume 音量 (0-1)
 * @returns 音频ID
 */
mk.audio.playEffect(clip: cc.AudioClip | string, volume?: number): number

/**
 * 播放背景音乐
 * @param clip 音频剪辑或路径
 * @param volume 音量 (0-1)
 */
mk.audio.playMusic(clip: cc.AudioClip | string, volume?: number): void

/**
 * 停止音效
 * @param audioId 音频ID
 */
mk.audio.stopEffect(audioId: number): void

/**
 * 停止背景音乐
 */
mk.audio.stopMusic(): void

/**
 * 设置音效音量
 * @param volume 音量 (0-1)
 */
mk.audio.setEffectVolume(volume: number): void

/**
 * 设置背景音乐音量
 * @param volume 音量 (0-1)
 */
mk.audio.setMusicVolume(volume: number): void
```

## MVVM API

```typescript
/**
 * 创建数据模型
 * @param data 初始数据
 * @returns 响应式数据模型
 */
mk.mvvm.createModel<T extends object>(data: T): T

/**
 * 绑定视图
 * @param node 视图节点
 * @param model 数据模型
 * @returns 绑定控制器
 */
mk.mvvm.bindView(node: cc.Node, model: object): any

/**
 * 监听数据变化
 * @param model 数据模型
 * @param path 属性路径
 * @param callback 回调函数
 */
mk.mvvm.watch(model: object, path: string, callback: (newValue: any, oldValue: any) => void): void
```

## 网络 API

```typescript
/**
 * 创建WebSocket连接
 * @param url 服务器地址
 * @param protocols 协议
 * @returns WebSocket实例
 */
mk.network.createWebSocket(url: string, protocols?: string | string[]): WebSocket

/**
 * 发送HTTP请求
 * @param url 请求地址
 * @param options 请求选项
 * @returns 响应数据
 */
mk.network.request<T>(url: string, options?: RequestOptions): Promise<T>

/**
 * 下载文件
 * @param url 文件地址
 * @param path 保存路径
 * @param progressCallback 进度回调
 * @returns 下载结果
 */
mk.network.download(url: string, path: string, progressCallback?: (progress: number) => void): Promise<boolean>
```

## 新手引导 API

```typescript
/**
 * 开始引导
 * @param guideId 引导ID
 */
mk.guide.start(guideId: string): void

/**
 * 结束引导
 */
mk.guide.end(): void

/**
 * 高亮节点
 * @param node 目标节点
 * @param shape 高亮形状 ('circle' | 'rect')
 */
mk.guide.highlight(node: cc.Node, shape?: 'circle' | 'rect'): void

/**
 * 显示引导提示
 * @param text 提示文本
 * @param position 位置
 */
mk.guide.showTip(text: string, position?: cc.Vec2): void
```

## 注意事项

- 所有返回 Promise 的 API 都可以使用 async/await 语法进行调用
- 资源加载 API 应当在适当的生命周期中调用，并处理可能的异常
- 在组件销毁前，应当释放已加载的资源，避免内存泄漏
- 使用装饰器时，确保 TypeScript 配置中启用了相关的实验性功能

## 类型定义

框架提供了完整的 TypeScript 类型定义，可以在开发过程中获得良好的代码提示和类型检查。类型定义文件位于 `@types` 目录下。

## 扩展 API

如果需要扩展框架功能，可以参考以下方式：

```typescript
// 扩展工具类
mk.tool.myCustomTool = {
    someFunction() {
        // 实现
    }
};

// 扩展装饰器
mk.decorator.method.myCustomDecorator = function() {
    return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        // 实现
        return descriptor;
    };
};
```

## 版本兼容性

本文档基于 MKFramework 最新版本编写，如果使用较早版本，部分 API 可能不可用或行为有所不同。请参考对应版本的文档或源码了解详情。