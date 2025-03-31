# 《高级Web技术》实验和课程设计指导书

本指导书可以帮助你从0开始搭建一个基于Vue.js和Spring Boot的前后端分离工程，并提交到GitHub仓库中。

项目前端使用Vue3框架和Element Plus组件库。后端使用Spring Boot、MyBatis，使用Gradle作为构建工具，使用MySQL 8.4作为数据库。

本教程假定你使用的操作系统是Windows。

## 0. 开始之前的准备工作

**需要安装的软件：**

- [Visual Studio Code](https://code.visualstudio.com/)（适合用于前端开发，是Vue推荐使用的开发工具）
- [IntelliJ IDEA](https://www.jetbrains.com/idea/download/?section=windows)（专业的Java集成开发环境，适合用于后端开发）
  - 建议下载Ultimate版本，功能更强大，在官网进行学生认证后可以免费使用
- [Git](https://registry.npmmirror.com/binary.html?path=git-for-windows/v2.49.0.windows.1/)（最流行的版本管理工具，必须安装Git才能操作Git仓库，将项目提交到GitHub；Git记录你每次提交代码的历史记录，你可以轻松查看文件修改历史或回退到之前的版本；它还可以实现多人协作开发）
  - 打开网页后，请下载第一个exe文件（Git-2.49.0-64-bit.exe）
  - **为了避免其他软件无法自动识别到Git，建议把Git安装在默认位置！**
- [Node.js](https://nodejs.org/zh-cn)（前端开发用到的各种工具，都依赖Node.js运行环境才能使用）

- [Java17 JDK](https://www.azul.com/downloads/?version=java-17-lts&os=windows&architecture=x86-64-bit&package=jdk#zulu)（如果你的电脑上没有合适的JDK，请点击链接下载，请下载.msi格式安装包并安装）
  - 安装完成后，打开终端输入`java --version`命令来检查是否已正确安装，若成功打印出关于OpenJDK版本的信息，则代表安装成功
- [MySQL](https://dev.mysql.com/downloads/mysql/)（如果你电脑上已经有MySQL了则不用安装，若没有请点击链接，选择8.4.4 LTS版本下载）
- [Navicat Premium Lite](https://www.navicat.com.cn/products/navicat-premium-lite)（Navicat的免费版，用来查看和操作数据库，在软件里免费注册账号并登录即可使用）
- [ApiFox](https://apifox.com/)（可用于API开发、测试和Mock，全中文界面，比Postman更加强大）

**此外，你还需要：**

- 对Web技术的兴趣
- 一定的耐心。

对新手来说，第一次开发Web项目会让你接触到大量陌生的技术和名词，若想顺利完成整个工程，你需要足够的耐心。

但当你的项目真正运行起来的那一刻，无比的成就感将会涌上心头。

## 1. 软件的初始设置

**VSCode的设置：**

打开VSCode，你首先需要安装一下做前端开发必备的插件：

- Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code
- HTML CSS Support
- Live Server（在做原生前端开发的时候可以用来实时预览HTML）
- Vue - Official（Vue官方支持插件）

**IDEA的设置：**

- 建议进入插件市场下载中文包

## 2. 初始化Git本地仓库（从GitHub上克隆你的仓库）

> 进行这一步的原因是：要向网络上的Git仓库提交代码，应该将仓库克隆到本地，在其中编写自己的代码，然后提交到本地仓库，并推送到远程仓库。
>
> 建议上网搜索关于Git的介绍视频，了解Git的基本原理。

首先在GitHub上找到你的实验2代码仓库并打开，点击绿色的**Code**按钮然后点击复制按钮复制仓库的HTTPS链接：

![image-20250329123303563](./images/image-20250329123303563.png)

然后在你电脑上用来存放项目的文件夹里打开终端，执行以下命令：

````bash
git clone <刚刚复制的链接>
````

此时会开始从GitHub上下载你的仓库，期间可能会要求你通过浏览器登录GitHub，按照指导操作即可。

> 若因为网络问题导致无法克隆，请使用代理服务器（科学上网）。请上网搜索“git设置http代理”了解让Git连接代理服务器的方法。

克隆完成后，在电脑上打开刚刚克隆的仓库文件夹，文件夹的内容应该和GitHub网站上显示的内容相同。

为了能够正常将自己的更改提交到远程仓库，需要设置一下Git的用户名和邮箱。参照这篇教程：[如何配置 Git 用户名和邮件地址](https://zhuanlan.zhihu.com/p/120862483)。你只需要设置全局用户名和邮箱即可。

## 3. 开发前的准备工作

请在仓库的根目录创建`frontend`和`backend`两个文件夹，分别存放前端和后端项目。

前端和后端是两个独立的项目，在各自的文件夹分别管理可以避免混乱，方便使用。

## 4. 创建前端项目

项目的前端使用Vue3框架，并使用Element Plus组件库来简化开发。

[Vue官网](https://cn.vuejs.org/)

[Element Plus官网](https://element-plus.org/zh-CN/)

现在我们开始创建前端项目。

1. **设置国内镜像源**

在确保你已经安装好Node.js后（在“准备工作”一节中提到过），打开终端执行以下命令：

```bash
npm config set registry https://registry.npmmirror.com
```

这条命令的作用是将NPM的包管理器镜像源设置为国内镜像，这样做可以显著加速NPM包的下载。

NPM镜像源设置是全局生效的，这意味着你不一定需要在项目目录中执行这条命令，且以后创建或使用别的前端项目的时候，不需要再次设置。

2. **使用官方工具创建示例项目**

在你的仓库根目录执行以下命令：

```bash
npm create vue@latest
```

系统可能会询问你是否要安装create-vue，请选择是：

```
Need to install the following packages:
create-vue@3.15.1
Ok to proceed? (y) y  <--输入y然后按下回车
```

等待它下载安装完成后，系统会要求你输入要创建的项目名称，请输入`backend`。

然后你会看到以下的选择界面：

![image-20250331222243904](D:\04_文档\2025\高级Web实验指导书\images\image-20250331222243904.png)

其中必选的功能是Router、Pinia、ESLint和Prettier。

- Router用于单页面的页内导航，各种页面切换都应该基于它来实现。

- Pinia用于创建一个可以被各个页面共享的数据存储，普通的`ref`或`reactive`响应式变量都仅在当前页面生效，Pinia可以让你在多个页面之间共享数据。

- ESLint提供了强大的语法检查功能，可以减少代码错误。

- Prettier可以自动格式化代码，保持代码整洁美观。
- TypeScript是可选项，它是JavaScript的升级版本，它在JavaScript的基础上添加了完善的类型系统，是一门强类型编程语言。TypeScript的语法提示功能更强，强类型的特性让它更不容易出现编程错误。它和JavaScript有着轻微的不同，需要一点时间来适应。
- 端到端测试是可选项，你可以利用端到端测试技术来对页面功能进行自动化测试，你可以用它自动模拟用户操作，并判断屏幕上的内容是否正确。若你希望对前端进行自动化测试，可以勾选这个功能。

然后系统会询问“是否引入 Oxlint 以加快检测？（试验阶段）”，请选择否。

然后项目创建完成。打开`frontend`文件夹，你会看到一系列的文件和文件夹，这便是你刚刚创建的Vue示例项目。

使用VSCode打开`frontend`文件夹（不是仓库根目录），在VSCode中打开终端（点击“终端”菜单中的“新建终端”），输入以下命令来将项目的所有依赖项下载到本地：

```bash
npm install
```

若VSCode提示你在父目录发现了Git仓库，是否打开，请选择是（点击后可能还需要在屏幕上方进行选择）。

> 如果不打开Git仓库，你就无法在VSCode中使用Git来进行代码提交和推送了，因此你应该打开。

若VSCode建议你安装ESLint、Prettier等插件，请根据提示进行安装。

> 安装这些插件后，VSCode中的代码分析、错误纠正和自动格式化代码等功能才会生效。

3. **尝试运行项目并查看示例页面**

在VSCode的终端中输入命令`npm run dev`，等待片刻即可看到Vite测试服务器的运行界面：

![image-20250331225631256](D:\04_文档\2025\高级Web实验指导书\images\image-20250331225631256.png)

你可以通过链接打开网页，也可以通过输入字母o后按下回车打开浏览器查看页面。

> 在npm run dev运行期间，若你修改前端代码并保存，浏览器里会实时同步你的更改。
>
> 若要关闭测试服务器，可以在终端中按下Ctrl+C或者输入q后按下回车。

打开浏览器后，你会看到如下测试页面：

![image-20250331230810007](D:\04_文档\2025\高级Web实验指导书\images\image-20250331230810007.png)

把鼠标移动到页面下方中间的Vue图表处，会显示两个按钮，它们分别为**Vue开发工具**和**组件定位工具**。Vue开发工具可以让你查看页面结构和各种数据，组件定位工具可以让你使用鼠标来选取任一元素，通过点击即可在VSCode中跳转到这个元素的代码位置。这都是Vite测试服务器提供的十分实用的工具，在后续的开发中可以发挥很大的作用。

4. **引入Element Plus**

Element Plus是适用于Vue 3的一款组件库，它预置了各种各种常用的前端组件，可以提高开发效率，并制作美观的界面。

在[Element Plus 组件总览](https://element-plus.org/zh-CN/component/overview)中可以查看Element Plus提供的各种组件。

现在，我们开始在项目里安装Element Plus。

> 提示：以下的操作步骤，均参照了Element Plus官网的“指南”中的“安装”和“快速开始”章节。

关闭Vite测试服务器，在VSCode终端中执行以下命令：

```bash
npm install element-plus --save
```

然后执行以下命令：

```bash
npm install -D unplugin-vue-components unplugin-auto-import
```

然后编辑前端项目根目录的`vite.config.ts`文件，在文件合适位置插入以下内容：

```ts
// ...
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
  // ...
})
```

然后编辑`tsconfig.app.json`，在相应位置添加以下代码：

```json
{
  // ...
  "compilerOptions": {
	// ...
    "types": ["element-plus/global"],
  }
}
```

现在你已经完成了Element Plus的安装，在`App.vue`中添加一个Element Plus组件（例如按钮`el-button`），你就可以看到一个比较漂亮的按钮被添加到了页面上。这代表你的Element Plus已经可以使用了。

5. **清理示例项目，开始编写自己的前端页面**

// 未完待续

## 5. 创建后端项目

// TODO

## 6. 后续工作：打包和部署

// TODO

