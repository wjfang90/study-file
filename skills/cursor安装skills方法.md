# cursor 安装skills教程

在cursor setting中单独成立一个【Rules, Skills, Subagents】菜单管理skills功能

## 安装使用 Agent Skills

### 1.安装node软件

skills功能是 通过node程序进行安装使用的，你需要具备一个node环境
注意：Node的版本要大于20，否则下面的安装可能报错

1️⃣ 在cmd中安装 Node.js 20（官方方式）

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | bash - apt install -y nodejs
```

2️⃣ 验证版本

```npm
node -v # 应该看到 v20.x.x
```

### 2.安装skills的管理模块

运行以下命令将OpenSkills安装到系统全局，此命令只需执行一次：

```npm
npm i -g openskills
```

### 3.安装 Skills

安装Anthropic官方Skills
--安装到当前项目：

```npm
openskills install anthropics/skills
```

--安装到全局：

```npm
openskills install anthropics/skills --global
```

这个OpenSkills命令会帮助你 克隆Anthropic官方的Skills仓库，你可以通过空格键选择要安装的具体技能。

--单独安装一个skills

此命令运行时是使用 HTTPS协议 连接代码仓库`https://github.com/` ，在cmd中不能成功连接代码仓库，需要在git中才成功连接

```bash
npx add-skill vercel-labs/agent-skills --skill "web-design-guidelines"
```

cmd工具只要我们加上git@的前缀就可以

```ps/cmd
npx add-skill git@github.com:skillcreatorai/Ai-Agent-Skills --skill "webapp-testing"
```

-- From Anthropic Marketplace

```npm
npx openskills install anthropics/skills
```

-- From Any GitHub Repo

```npm
npx openskills install your-org/your-skills
```

--From a Local Path

```npm
npx openskills install ./local-skills/my-skill
```

-- From Private Git Repos

```npm
npx openskills install git@github.com:your-org/private-skills.git
```

### 4.创建AGENTS.md文件

安装技能后，还需要创建AGENTS.md文件让Cursor能够发现和使用这些技能：

在项目根目录创建一个空白的 AGENTS.md 文件
运行同步命令：openskills sync
选择你要写入AGENTS.md的技能
按回车确认，所选技能将被写入AGENTS.md文档

### 5.调用Skills

Skills可以被Agent自动调用，也可以在提示词中手动指定：
prompt： 调用 frontend-design skills，用HTML开发一个视频剪辑软件的SaaS介绍页

### 6.openskills其它命令

```npm
npx openskills install <source> [options]  # Install from GitHub, local path, or private repo
npx openskills sync [-y] [-o <path>]       # Update AGENTS.md (or custom output)
npx openskills list                        # Show installed skills
npx openskills read <name>                 # Load skill (for agents)
npx openskills update [name...]            # Update installed skills (default: all)
npx openskills manage                      # Remove skills (interactive)
npx openskills remove <name>               # Remove specific skill
```

更多命令参考`https://github.com/numman-ali/openskills`
