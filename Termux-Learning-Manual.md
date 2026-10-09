# Termux + GitHub 学习工作站 使用与速查手册

适用：Termux / Linux 命令 / Java / Python / Git / GitHub / SQLite

目标：在 Termux 中快速进入学习环境、记录笔记，并把笔记同步到 GitHub。

## 一、当前环境与目录

- GitHub 用户名：rjwsr1216
- 本地仓库目录：~/cybersecurity-notes
- Linux 笔记目录：~/cybersecurity-notes/02-linux
- Java 示例文件：~/Hello.java（如果仍在主目录）
- SQLite 数据库示例：~/study.db（快捷命令 db 指向此路径）
注意：以上路径依据当前配置记录。如果你后来移动或重命名了文件夹，请按实际路径修改命令。

## 二、常用快捷命令

| 命令 | 作用 | 备注 |
| --- | --- | --- |
| notes | 进入本地 GitHub 笔记仓库 | 不是打开网页，也不会自动上传 |
| linuxnotes | 进入 02-linux 笔记目录 | 目录必须存在 |
| javahome | 回到主目录 ~ | 当前 Java 示例文件预计在主目录 |
| javahello | 编译并运行 Hello.java | 需要单独配置；文件须存在 |
| py | 启动 Python 交互环境 | 通常出现 >>> 提示符 |
| db | 打开 ~/study.db | 需要 sqlite3 已安装 |
| gs | 查看笔记仓库 Git 状态 | 相当于 git -C ~/cybersecurity-notes status |
| cd ~ | 返回 Termux 主目录 | 不会退出 GitHub 账号或删除文件 |

## 三、配置快捷命令

如果此前已经配置过这些命令，不要反复追加相同配置。先检查：

tail -n 30 ~/.bashrc

type notes

type linuxnotes

type javahome

type javahello

type py

type db

type gs

若需要一次性新增缺少的快捷命令，可在 Bash 的普通 $ 提示符下执行下面配置。执行前请确认 ~/.bashrc 中没有重复定义：

```bash
# === My Learning Shortcuts ===
alias notes='cd ~/cybersecurity-notes'
alias linuxnotes='cd ~/cybersecurity-notes/02-linux'
alias javahome='cd ~'
alias py='python'
alias db='sqlite3 ~/study.db'
alias gs='git -C ~/cybersecurity-notes status'
alias javahello='cd ~ && javac Hello.java && java Hello'
```

把配置写入 ~/.bashrc 后，执行 source ~/.bashrc 让当前会话加载。若你使用的不是 Bash（例如 Zsh），配置文件可能不同。

## 四、Linux / Termux 常用命令

| 命令 | 作用 |
| --- | --- |
| pwd | 显示当前路径 |
| ls -la | 显示当前目录中的文件（包括隐藏文件） |
| cd 目录名 | 进入指定目录 |
| cd .. | 返回上一级目录 |
| cd ~ | 回到主目录 |
| mkdir -p 目录名 | 创建目录；父目录不存在时一并创建 |
| cat 文件名 | 查看文本文件 |
| nano 文件名 | 用 Nano 编辑文件 |
| clear | 清理终端屏幕显示，不会删除文件 |

## 五、Java：打开、编译、运行与退出

java --version

cd ~

ls Hello.java

javac Hello.java

java Hello

javahello

java --version 用于查看版本；javac Hello.java 编译源文件；java Hello 运行编译后的类，通常不写 .java。正常结束后会返回 Shell。运行卡住时可按 Ctrl+C 中断。若使用 jshell 交互环境，输入 /exit 退出。

如果 javahome 执行后看起来没变化，这是因为它只执行 cd ~；它不是启动 Java 的命令。javahello 是专门针对主目录下 Hello.java 的快捷运行命令。

## 六、Python：打开、运行与退出

py

python --version

python script.py

exit()

输入 py 通常进入 Python 交互环境，提示符通常是 >>>。在 >>> 中输入 exit() 或按 Ctrl+D 返回 Termux Shell。运行脚本时将 script.py 换成实际文件名。

## 七、SQLite：打开、查询与退出

db

.tables

.schema

SELECT name FROM sqlite_master;

.quit

db 这个快捷命令指向 ~/study.db；如果数据库路径不同，请修改别名。看到 sqlite> 后可输入 SQL 语句；.tables、.schema、.quit 是 SQLite 点命令，不是普通 SQL。

## 八、Git 与 GitHub：状态、提交、同步

| 命令 | 作用 |
| --- | --- |
| git status 或 gs | 查看工作区和暂存区状态 |
| git branch | 查看本地分支 |
| git diff | 查看未暂存的文本修改 |
| git add 文件名 | 暂存指定文件 |
| git commit -m "Update notes" | 创建本地提交 |
| git push | 将已提交内容推送到 GitHub |
| git pull --rebase | 拉取远程更新并尝试整理本地提交 |
| git remote -v | 查看仓库关联的远程地址 |

Git 命令执行完通常自动返回 Shell，无需专门退出。notes 只是进入本地仓库，不会自动同步；git push 才会上传已提交的内容。首次克隆仓库只需执行一次。

## 九、在 GitHub 仓库中记录 Linux 笔记

notes

cat 02-linux/README.md

nano 02-linux/README.md

git status

git add 02-linux/

git commit -m "Update Linux notes"

git push

若 README.md 已有内容，先查看再编辑，避免无意覆盖。Nano 保存：Ctrl+O，回车确认，再 Ctrl+X 退出。git add 02-linux/ 只暂存该目录下的变更；提交前先 git status 检查。

## 十、各环境退出速查表

| 当前环境 | 退出方式 |
| --- | --- |
| Termux Shell ($) | 通常不用退出；输入下一条命令即可。exit 会结束当前 Shell 会话。 |
| Python (>>> ) | exit() 或 Ctrl+D |
| SQLite (sqlite>) | .quit |
| Nano | Ctrl+X |
| Vim | 按 Esc，再输入 :q 并回车；有未保存修改时先决定保存或放弃 |
| 正在运行的程序 | 通常 Ctrl+C 中断；具体取决于程序 |
| SSH 远程 Shell | exit |
| 本地 Git 仓库 | 没有专门的“退出 GitHub”命令；cd ~ 只是切换回主目录 |

## 十一、日常学习推荐流程

1. 进入仓库：notes
1. 进入相应笔记目录：例如 linuxnotes
1. 练习命令或学习代码，并把原理、步骤、结果和错误原因记录在 Markdown 文件里
1. 检查变更：gs 或 git status
1. 暂存需要上传的文件：git add 文件名（优先指定文件或目录）
1. 提交：git commit -m "Update learning notes"
1. 上传：git push
1. 在 GitHub 网页刷新，确认文件已更新
## 十二、常见错误与排查

| 报错 | 处理建议 |
| --- | --- |
| fatal: repository 'cd' does not exist | 可能把 cd 当成仓库地址使用了。cd 是切换目录命令；克隆仓库需使用真实 Git URL。 |
| not a git repository | 当前目录不是 Git 仓库。先执行 cd ~/cybersecurity-notes，再执行 git status。 |
| cd: 仓库名: No such file or directory | “仓库名”是占位文字，需替换为真实目录名；本仓库名为 cybersecurity-notes。 |
| 快捷命令 not found | 检查 type 命令名；确认 ~/.bashrc 中配置正确后执行 source ~/.bashrc。 |
| git push 认证失败 | 根据实际提示检查网络和 GitHub 认证方式；不要把密码或 Token 发给他人。 |
| -17: not a valid identifier | 这通常与 Shell 配置或复制的字符格式有关。不要盲目删除配置；先检查 echo $0 和 tail -n 25 ~/.bashrc。 |

## 十三、重要提醒

- Termux 的 $ 提示符通常表示 Shell；Python 常见 >>>；SQLite 常见 sqlite>。不要把一种环境的指令输到另一种环境里。
- 不要把访问令牌、密码、私钥或含有个人信息的配置文件提交到公开仓库。
- git add . 会暂存当前仓库中所有未忽略的修改；提交前先检查 git status。
- GitHub 远程仓库与 Termux 本地仓库不是同一个位置，需要用 push/pull 同步。
- 如果命令结果与本手册不同，以你设备上的实际路径和报错为准，先检查再修改。
