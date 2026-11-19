# 拿到一个 GitHub 项目，到底该从哪个文件开始看？

凌晨一点，刷到一个挺有意思的 GitHub 项目。介绍看着不错，演示效果也不错，点个 Star，顺手 clone 到电脑上。

打开文件夹，几十个文件排在那里。点进一个，三百多行；换一个，连开头的 import 都没认全。

「算了，明天再看。」

然后这个项目就在硬盘里住下了。

第一次读别人的项目，容易卡在这里：每个文件好像都有用，又不知道该先点哪个。尤其是带着「我要把它读懂」的想法进去，很快就会发现，这个目标实在有点大。

不如先缩小一点：它怎么用？刚才那个功能，是在哪儿实现的？

## 先看看这些文件都是干什么的

先把常见文件认个大概，后面会省事不少。

- `README`、`docs/`：项目介绍和使用文档，给人看。
- `src/`、`tests/`：程序的实现和测试，看看它怎么工作。
- `.gitignore` 等配置文件：告诉 Git 或其他工具该怎么处理这个项目。
- `LICENSE`、`CONTRIBUTING.md`、`CODE_OF_CONDUCT.md`：复用代码、参与贡献时要了解的规矩。

![Requests 仓库主页：文件列表中有 docs、src/requests、tests 和 .gitignore，右侧可找到 README、许可证和贡献指南](img/requests-repository.jpg)

*图 1：Requests 仓库的实际页面。先认出文档、源码和测试的位置，再按需要点进去；右侧也能找到许可证和贡献指南。*

真实项目未必长这样：有的没有 `src/`，有的文档放在单独的网站。先认用途，名字对不上也没关系。

## README 看完，再往哪走？

先看 `README`，通常没什么争议。但也不用一口气读到底。先找它是做什么的、怎么安装、有没有一段能直接跑的例子。

拿 Python 的 Requests 来说，README 里很快就能找到安装命令和 `requests.get(...)` 的用法。跑通之后，再挑一个你想弄明白的地方。比如：`params` 接收的那个字典，最后怎么变成了网址后面的参数？

有了这个问题，后面的文件就好找了。

### src/：从你刚用过的功能找起

有些项目有 `main.py`、`index.js` 这样的启动文件，可以从那里往下看。但 Requests 是一个供别的程序调用的库，找 `get()` 比找一个叫 main 的文件有用得多。

在 `src/requests/api.py` 里找到 `get()`，会发现它没有直接拼网址，而是把参数继续传了下去。沿着调用找，处理 URL 的代码在 `src/requests/models.py` 的 `prepare_url()` 里。

中间碰到认证、Cookie、连接管理，暂时跳过去也没事。先把 `params` 的去向看明白，其他问题以后再说。

### docs/：源码看不下去，就回来查用法

如果还不清楚 `params` 到底接受什么，先别急着猜源码。Requests 的快速入门就有一节讲 URL 参数，字典怎么传、结果长什么样，都有例子。

读文档也不用从第一页开始。带着问题搜到相关章节，看完继续；如果你只是想把库用起来，问题解决了就可以收工。

### tests/：有些细节，例子比解释好懂

测试里经常藏着文档没展开讲的情况。在 `tests/test_requests.py` 里搜 `params`，就能找到一个很具体的测试：原网址已经有参数，还带着 `#fragment`，新参数应该放在哪儿？

它给出的预期是：保留原参数，把新参数加在 `#fragment` 前面。

![Requests 参数测试：高亮部分给出原网址与预期结果，并用断言检查新增参数位于 fragment 前面](img/requests-params-test.jpg)

*图 2：高亮部分就是这个测试。`url` 是原网址，`expected` 是预期结果，最后的 `assert` 检查两者是否按预期对应。截图中的新增参数是 `a=b`，下面的示例换成了 `page=2`，规则一样。*

装好 Requests 后，可以自己试试。下面这段只准备请求，不会真的访问网站：

```python
import requests

request = requests.Request(
    "GET",
    "https://example.com/search?lang=zh#results",
    params={"page": 2},
)
print(request.prepare().url)
```

输出的网址结尾是 `?lang=zh&page=2#results`。再回头看测试里的输入和断言，刚才那几行就容易懂了。

### .gitignore：顺手看一眼就行

这个文件告诉 Git 哪些文件不用跟踪。像本地虚拟环境、缓存、构建产物，通常不需要提交进仓库。

顺便还能猜猜技术栈：Requests 的 `.gitignore` 里有 `*.pyc`、`.venv/` 和 `.pytest_cache/`，Python 和 pytest 的痕迹就很明显。它不能代替文档，不过扫两眼也挺有意思。

## 还有几个文件，别一直跳过

想把一段代码用进自己的项目，先看看 **`LICENSE`**。MIT、Apache-2.0 和 GPL 都允许在一定条件下复用代码，条件却不一样。比如，MIT 要求保留版权和许可声明；Apache-2.0 还有专利许可等条款；分发受 GPLv3 约束的修改版本时，则涉及提供对应源代码和沿用许可证的要求。不能只凭一句「开源的，随便用」就搬走代码。没找到许可证，也别默认作者已经授权复用。

想给作者提 PR，就翻翻 **`CONTRIBUTING.md`**。开发环境怎么装、测试怎么跑、改之前要不要先开 Issue，往往都写在这里。有时候照着 README 装完，还是跑不了测试，因为 README 教的是怎么使用，贡献指南才会补上开发需要的东西。

**`CODE_OF_CONDUCT.md`** 讲的是社区里的行为约定，也可能写着遇到骚扰等问题该联系谁。准备参与讨论的话，可以先扫一遍。

根目录找不到这些文件，可以再看仓库侧栏或 `.github/`。另外，`CHANGELOG.md` 常用来查版本变化；发现安全问题时，先按 `SECURITY.md` 的说明联系维护者。

## 别忘了 GitHub 网页上也有东西可看

报错之后，可以把报错里比较特别的一小段拿去搜 **Issues**。记得也看看已经关闭的：你碰到的问题，可能早就有人问过，解决办法就在下面的回复里。

如果你想知道某段代码为什么要绕个弯，可以找相关的 **PR**。改了哪几行，源码里能看到；为什么放弃另一种写法，有时得看讨论才知道。

提交历史也值得翻，但别只数提交有多勤。想把项目用起来，还是要看 **Releases** 的说明、兼容性和已知问题，选适合自己的版本。`main` 上最新的代码未必经过了同样的发布检查。

## 下次打开，可以这样试试

先看 README，跑通一个最小例子，再从例子里挑个感兴趣的功能，去找实现。卡住了，回来查文档、翻测试、搜 Issues。准备复用代码前看许可证，准备贡献前看贡献指南。

不用第一次打开就把整个仓库看完。能弄明白一个参数是怎么传的、一个按钮点下去发生了什么，就已经有东西可记了。下次再打开，也知道自己上次看到哪儿。

你收藏夹里放得最久、还没认真看过的项目是哪个？不妨就从它开始。

## 参考资料

> Requests 项目仓库：https://github.com/psf/requests
>
> 图 1 截自上述仓库主页；图 2 截自参数测试：https://github.com/psf/requests/blob/6f66281a1d6326b1b9c4ac09ca30de0fc4e6ef43/tests/test_requests.py#L150-L165
>
> Requests 快速入门：https://requests.readthedocs.io/en/latest/user/quickstart/
>
> GitHub 许可证说明：https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
>
> GNU GPLv3 正文：https://www.gnu.org/licenses/gpl-3.0.html
