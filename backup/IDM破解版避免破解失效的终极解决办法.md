很多IDM破解版本会在使用一段时间后失效，并弹窗提示你购买。经过研究，这主要是因为IDM在浏览器中的插件 **IDM Integration Module** 自动更新导致的。因此，解决方法也很明确，即禁止 **IDM Integration Module** 插件自动更新。

然而，浏览器本身无法设置是否自动更新插件，因此只能通过修改插件所在文件夹的读写权限来实现这一目标，将其设置为只读即可一劳永逸。

## 附：Edge浏览器插件文件存放目录
- `%localappdata%\Microsoft\Edge\User Data\Default\Extensions\`