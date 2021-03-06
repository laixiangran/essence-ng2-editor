# e-ngx-editor

基于Angular的富文本编辑组件，依赖第三方插件：[neditor](https://github.com/notadd/neditor)（neditor 基于 [UEditor](http://fex.baidu.com/ueditor/)）

需要使用后台相关的功能（如上传图片、视频等等）请部署对应的后端，[后端部署说明](http://fex.baidu.com/ueditor/#server-deploy)

## Usage

1. Install

	```shell
	npm install --save e-ngx-editor@latest
	```
	
2. 在index.html引入neditor [下载安装包](https://github.com/notadd/neditor#%E5%AE%8C%E6%95%B4%E5%AE%89%E8%A3%85%E5%8C%85-%E6%97%A0%E9%9C%80%E7%BC%96%E8%AF%91)

	```html
    <script src="./assets/scripts/neditor/neditor.config.js"></script>
    <script src="./assets/scripts/neditor/neditor.all.min.js"></script>
    <script src="./assets/scripts/neditor/i18n/zh-cn/zh-cn.js"></script>
	```

3. Add the ENgxEditorModule

	```typescript
	import {ENgxEditorModule} from "e-ngx-editor";
	@NgModule({
	    imports: [
	        ENgxEditorModule
	    ]
	})
	```

4. Use in the template

	```html
	<e-ngx-editor #editor [(ngModel)]="model_text"
                        (contentChange)="contentChange($event)"
                        (ready)="editorReady($event)"
                        (click)="test(editor.text)">
    </e-ngx-editor>
	```

5. Use in the component

	```typescript
	model_text: string = '<p style="font-weight: bold;"><a href="http://ueditor.baidu.com/website/index.html" target="_blank" title="去UEditor官网">UEditor Component for Angular2</a></p>';

    contentChange ($event) {
        console.log("contentChange：", $event);
    }

    editorReady ($event) {
        console.log("ready：", $event);
    }

    test (text: string): void {
        console.log(text);
    }
	```

## API

### Inputs

- `[(ngModel)]`（`string`） - 绑定编辑器内容
- `ueOption`（`?Object`） - 属性参数（[参照官网配置](http://fex.baidu.com/ueditor/#start-config)），默认defaultConfig如下：
```typescript
    defaultConfig: any = {
        autoHeightEnabled: false
    };
```

### Outputs

- `ready` - 编辑器准备就绪后会触发该事件

- `destroy` - 执行destroy方法会触发该事件

- `reset` - 执行reset方法会触发该事件

- `focusEvent` - 执行focus方法会触发该事件

- `langReady` - 语言加载完成会触发该事件

- `beforeExecCommand` - 运行命令之后会触发该命令

- `afterExecCommand` - 运行命令之后会触发该命令

- `firstBeforeExecCommand` - 运行命令之前会触发该命令

- `beforeGetContent` - 在getContent方法执行之前会触发该事件

- `afterGetContent` - 在getContent方法执行之后会触发该事件

- `getAllHtml` - 在getAllHtml方法执行时会触发该事件

- `beforeSetContent` - 在setContent方法执行之前会触发该事件

- `afterSetContent` - 在setContent方法执行之后会触发该事件

- `selectionchange` - 每当编辑器内部选区发生改变时，将触发该事件。**警告： 该事件的触发非常频繁，不建议在该事件的处理过程中做重量级的处理**

- `beforeSelectionChange` - 在所有selectionchange的监听函数执行之前，会触发该事件

- `afterSelectionChange` - 在所有selectionchange的监听函数执行完之后，会触发该事件

- `contentChange` - 编辑器内容发生改变时会触发该事件

### Methods

- `setHeight (height: number): void` - 设置编辑器高度。当配置项autoHeightEnabled为真时，该方法无效
	- height 编辑器高度（不带单位）
	
- `setContent (html: string, isAppendTo: boolean = false): void` - 设置编辑器的内容，可修改编辑器当前的html内容
	- html 要插入的html内容
    - 若传入true，不清空原来的内容，在最后插入内容，否则，清空内容再插入
    
- `getContent (): any` - 获取编辑器html内容

- `getContentTxt (): any` - 获取编辑器纯文本内容

- `getPlainTxt (): any` - 获取编辑器带格式的纯文本内容

- `hasContents (): boolean` - 判断编辑器是否有内容

- `focus (): void` - 让编辑器获得焦点

- `blur (): void` - 让编辑器失去焦点

- `isFocus (): boolean` - 判断编辑器是否获得焦点

- `setDisabled (): void` - 设置当前编辑区域不可编辑

- `setEnabled (): void` - 设置当前编辑区域可以编辑

- `setHide (): void` - 隐藏编辑器

- `setShow (): void` - 显示编辑器

- `getSelectionText (): string` - 获得当前选中的文本

- `executeCommand (command: string, content?: string)` - 执行指定命令
	- command 执行的命令
    - content 执行要操作的内容

## Develop

	```shell
	npm install // 安装依赖包
	
	npm start // 启动项目
	```

# License

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](/LICENSE)
