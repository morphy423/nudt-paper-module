# nudt本科毕业设计模板
本工作围绕国防科技大学本科毕业论文LaTeX模板展开系统性修改与适配。基于nudtpaper文档类，采用XeLaTeX编译引擎，对模板类文件nudtpaper.cls及主文件main.tex进行深度定制，以严格契合学校论文撰写规范。
修改和使用方法如下




一、项目概述
本项目基于 nudtpaper 文档类，采用 XeLaTeX 编译，支持 Biber 或 BibTeX 参考文献管理。项目结构采用主文件（main.tex）+ 分章节文件（data/ 目录）的组织方式，便于模块化撰写与版本控制。

二、快速开始
2.1 编译方式
基础编译命令：
xelatex main.tex
若使用 Biber 管理参考文献：
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
若使用 BibTeX 管理参考文献（默认）：
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
2.2 文件组织建议
project/
├── main.tex                  # 主文档（仅含框架与配置）
├── nudtpaper.cls             # 模板类文件（一般不动）
├── mynudt.sty                # 自定义宏包（如有）
├── fonts/                    # 字体目录（ttf模式需要）
│   ├── simsun.ttc
│   ├── simhei.ttf
│   ├── fangsong_GB2312.ttf
│   └── simkai.ttf
├── data/                     # 论文章节内容
│   ├── abstract.tex          # 中英文摘要
│   ├── 第一章绪论.tex
│   ├── 第二章建模.tex
│   ├── 第三章算法设计.tex
│   ├── 第四章实验.tex
│   ├── 第五章总结.tex
│   └── ack.tex               # 致谢
├── ref/
│   ├── bstutf8.bst           # BibTeX样式文件
│   └── refs.bib              # 参考文献数据库
└── image/                    # 图片资源目录

三、文档类选项详解（\documentclass）
在 main.tex 顶部修改：
\documentclass[ttf,anon]{nudtpaper}
选项	功能说明	使用建议
ttf	使用本地 TrueType 字体（宋体、黑体、楷体、仿宋）	推荐 Windows 用户使用，需确保 fonts/ 目录存在
otf	使用 OpenType 字体	字体文件后缀为 .otf 时使用
fz	使用方正字体	需安装方正字库
fandol	使用 Fandol 开源字体	Linux/Mac 用户无 Windows 字体时的备选
anon	盲审模式：隐藏封面个人信息（姓名、学号、导师等）	送审前开启
twoside	双面打印模式（奇偶页边距对称、章节从奇数页开始）	正式装订时开启
biber	使用 biblatex + biber 处理参考文献	需配合 .bib 文件，支持更现代的引用格式

修改示例：
% 双面打印 + 盲审 + Biber参考文献
\documentclass[ttf,twoside,anon,biber]{nudtpaper}

% 单面打印 + 正常显示个人信息 + BibTeX
\documentclass[ttf]{nudtpaper}
四、封面信息配置
在 main.tex 的导言区（\begin{document} 之前）修改以下命令：
\title{xxxx }   % 论文题目
\author{xxxx }                                            % 学员姓名
\serialno{xxxxx}                                    % 学号
\firstmajor{xxxx }                                  % 首次任职专业
\major{xxxx }                                       % 学历教育专业
\college{xxxx }                                     % 所属学院
\grade{xxxx }                                            % 年级
\supervisor{xxxx }                                        % 指导教员
\teachtitle{xxxx }                                    % 职称
\department{xxxxxx}                    % 所属单位
4.1 题目换行
若题目过长需要换行，使用 \ 手动断行：
\title{多类型反舰导弹在对抗舰艇编队中\\的优化分配策略研究}
4.2 首次任职专业换行
若首次任职专业名称过长，取消以下注释并使用 \ 换行：
\firstmajor{\parbox[c]{108pt}{ \rule{0pt}{10pt}
\centering \banxiaosi {你的任职专业也\\可以换行} }}
五、章节文件组织
在 main.tex 的 \mainmatter 之后，通过 \input 引入各章节：
\mainmatter
\input{data/第一章绪论}
\input{data/第二章建模}
\input{data/第三章算法设计}
\input{data/第四章实验}
\input{data/第五章总结}
\input{data/ack}
修改建议：
• 增删章节：直接添加或删除 \input{data/新章节} 行
• 调整顺序：调换 \input 行的先后顺序
• 独立编译某章：临时注释掉其他 \input 行以加速编译
六、字体与排版参数
6.1 正文字号与行距（全局控制）
在 nudtpaper.cls 中，正文参数由 \normalsize 定义：
\renewcommand\normalsize{%
    \@setfontsize\normalsize{12bp}{22.35bp}%   % 字号12bp，基线间距22.35bp
    \renewcommand{\baselinestretch}{1.0}%       % 行距倍数
    ...
}
参数	含义	修改建议
12bp	正文字号	毕业设计规范一般为小四（12pt/bp），不建议修改
22.35bp	基线间距	决定行距的绝对值，增大则行距变宽
baselinestretch	行距拉伸系数	设为 1.0 表示单倍行距（相对于字号）

6.2 各级标题字号
命令	字号	用途	修改位置
\chuhao	42bp	超大标题	nudtpaper.cls 中 \thu@define@fontsize
\xiaochu	36bp	封面"本科毕业论文"	同上
\yihao	26bp	—	同上
\erhao	22bp	—	同上
\xiaoer	18bp	—	同上
\sanhao	16bp	章标题	同上
\sihao	14bp	节标题、参考文献标题	同上
\xiaosi	12bp	正文、小节标题	同上
\wuhao	10.5bp	图表标题、页眉页脚	同上

6.3 标题格式修改
在 nudtpaper.cls 中搜索并修改：
% 章标题：黑体，三号，居中
\titleformat{\chapter}{\filcenter \heiti\sanhao[1.25]}{第\thechapter 章\,}{1em}{}

% 节标题：黑体，四号
\titleformat{\section}{\bfseries \heiti\sihao[1.25]}{\thesection}{1em}{}

% 小节标题：黑体，小四
\titleformat{\subsection}{\bfseries \heiti\xiaosi[1.25]}{\thesubsection}{1em}{}

% 小小节标题：黑体，小四
\titleformat{\subsubsection}{\bfseries \heiti\xiaosi[1.25]}{\thesubsubsection}{1em}{}
参数说明：
• [1.25]：行距倍数为 1.25，可改为 [1.5] 或 [1.0]
• 1em：标题编号与标题文本的间距
七、页面布局调整
7.1 页边距
在 nudtpaper.cls 中：
\geometry{top=25mm,bottom=25mm,left=30mm,right=30mm}
\geometry{headheight=5mm,headsep=5mm,footskip=8mm}
参数	含义	建议
top	上边距	25mm
bottom	下边距	25mm
left	左边距（装订侧）	30mm（可适当增至 32mm）
right	右边距	30mm
headheight	页眉高度	5mm
headsep	页眉与正文间距	5mm
footskip	页脚基线与正文基线间距	8mm

7.2 页眉页脚
在 nudtpaper.cls 中：
\renewpagestyle{plain}{
    \sethead{}{\raisebox{.4\baselineskip}{\songti \xiaowu 国防科技大学本科毕业论文}}{}%
    \setfoot{}{}{\raisebox{4pt}{\songti \xiaowu 第~\thepage~页}}{}%
    \headrule%
    \footrule%
}
可修改项：
• 页眉文字："国防科技大学本科毕业论文" → 其他文字
• 页眉字号：\xiaowu（小五，9bp）→ \liuhao（六号，7.5bp）
• 页眉位置：\raisebox{.4\baselineskip} 调整垂直偏移
• 页脚格式："第~\thepage~页" → 仅 \thepage
八、图表与公式格式
8.1 图表标题格式
在 nudtpaper.cls 中：
\DeclareCaptionLabelFormat{thu}{{\wuhao[1.25]\song#1~\rmfamily #2}}
\DeclareCaptionLabelSeparator{thu}{\hspace{1em}}
\DeclareCaptionFont{thu}{\wuhao[1.25]}
\captionsetup{labelformat=thu,labelsep=thu,font=thu}
修改建议：
• 图表标题字号：\wuhao（小五）→ \xiaowu（五号）
• 编号与标题间距：\hspace{1em} → \hspace{0.5em}
8.2 图表编号格式
默认格式为 章-序号（如 图 3-5、表 2-1）：
\renewcommand\thefigure{\thechapter-\arabic{figure}}
\renewcommand\thetable{\thechapter-\arabic{table}}
若需改为 图 3.5 格式：
\renewcommand\thefigure{\thechapter.\arabic{figure}}
8.3 公式编号格式
\renewcommand\theequation{\thechapter-\arabic{equation}}
8.4 浮动体间距
控制图表与正文的垂直间距：
\setlength{\floatsep}{12bp}      % 图表之间
\setlength{\intextsep}{12bp}      % 图表与正文（若使用 [H]）
\setlength{\textfloatsep}{12bp}   % 图表与正文（顶部/底部浮动）
九、参考文献配置
9.1 BibTeX 模式（默认）
在 main.tex 中：
\bibliographystyle{ref/bstutf8}
\nocite{*}
\bibliography{ref/refs}
修改建议：
• 更换样式文件：将 bstutf8.bst 替换为其他 .bst 文件
• 取消 \nocite{*}：仅引用文中实际出现的文献
9.2 Biber 模式
在 \documentclass 中添加 biber 选项，并将 main.tex 中参考文献部分改为：
\ifisbiber
{\hyphenpenalty=500 %
    \tolerance=9900 %
    \printbibliography[heading=bibliography, title=参考文献]
}
\else
\bibliographystyle{ref/bstutf8}
\bibliography{ref/refs}
\fi
9.3 参考文献悬挂缩进与格式
在 nudtpaper.cls 的 thebibliography 环境中：
\enumerate[label={[
\arabic*]},
    itemsep=0pt,
    parsep=0pt,
    labelwidth=\biblabelwd,
    labelsep=0.75em,
    leftmargin=\dimexpr\biblabelwd+\labelsep\relax,
    align=left,
    itemindent=0pt,
    topsep=0pt,
    partopsep=0pt]
参数	作用
labelwidth	编号宽度（如 [99] 的宽度）
labelsep	编号与作者名的间距
leftmargin	左缩进总量
itemsep	条目间距

十、摘要与符号表
10.1 摘要环境
在 data/abstract.tex 中撰写：
\begin{cabstract}
% 中文摘要内容
\end{cabstract}

\begin{eabstract}
% English abstract content
\end{eabstract}
格式控制：
• 摘要字号：\xiaosi（小四，12bp）
• 摘要行距：22.35bp（固定值）
• 关键词格式：\hei\xiaosi 关键词： + \songti\xiaosi 内容
10.2 符号表（可选）
默认使用 denotation 环境。在 main.tex 中：
% 默认使用 denotation.tex
%\input{data/denotation}

% 或使用 nomencl 宏包（需取消注释）
% \cleardoublepage
% \printnomenclature
符号表格式在 nudtpaper.cls 中定义：
\newenvironment{denotation}[1][2.71828cm]{
    \noindent\vskip-4bp\begin{list}{}%
    {\vskip-30bp\xiaosi[1.5]
    \renewcommand\makelabel[1]{\textbf{##1}\hfil}
    \setlength{\labelwidth}{#1} % 标签盒子宽度
    \setlength{\labelsep}{0cm}
    \setlength{\leftmargin}{\labelwidth+\labelsep+2em}
    ...}
}{\end{list}}
十一、算法环境使用
11.1 可跨页算法框（自定义）
在 main.tex 中已定义：
\newtcolorbox{algframe}{
    enhanced,
    breakable,          % 允许跨页
    colback=white,
    colframe=black,
    boxrule=0.4pt,
    top=2pt, bottom=2pt, left=4pt, right=4pt,
    arc=0pt, outer arc=0pt,
    before skip=0pt, after skip=0pt
}
使用示例：
\begin{algframe}
\begin{algorithmic}[1]
\STATE 初始化参数
\FOR{$i = 1$ to $N$}
    \STATE 执行操作
\ENDFOR
\end{algorithmic}
\end{algframe}
11.2 算法框内部行距调整
若需单独调整算法框内行距，在算法内容前添加：
\begin{algframe}
\renewcommand{\baselinestretch}{1.2}\selectfont  % 单独设置算法框行距
\begin{algorithmic}[1]
...
\end{algorithmic}
\end{algframe}
十二、盲审模式
12.1 开启盲审
在 main.tex 中：
\newif\ifreview\reviewtrue   % true = 盲审模式
效果：
• 封面个人信息（姓名、学号、导师等）被清空
• 致谢内容变为白色（\color{white}），打印时不可见但保留占位
12.2 关闭盲审
\newif\ifreview\reviewfalse  % false = 正常模式
十三、其他实用参数速查
13.1 首行缩进
\settowidth\CJK@twochars{中国}  % 测量"中国"宽度
\parindent\CJK@twochars         % 设置为首行缩进量
13.2 段落间距
\setlength{\parskip}{0bp \@minus 1bp}  % 段间距，可改为 6bp
13.3 目录深度
\setcounter{secnumdepth}{3}  % 编号深度到 subsubsection
13.4 交叉引用格式（cleveref）
已预配置中文引用格式：
命令	输出示例
\cref{fig:1}	图 3-1
\cref{tab:1}	表 2-1
\cref{eq:1}	式 (3-1)
\cref{chap:1}	第 1 章

十四、常见修改场景速查表
修改目标	修改位置	具体参数
论文题目	main.tex	\title{...}
个人信息	main.tex	\author, \serialno, \supervisor 等
增加章节	main.tex	添加 \input{data/新章节}
切换盲审	main.tex	\reviewtrue / \reviewfalse
调整页边距	nudtpaper.cls	\geometry{...}
调整正文字号	nudtpaper.cls	\@setfontsize\normalsize{12bp}{22.35bp}
调整行距	nudtpaper.cls	\baselinestretch 或基线间距值
调整章标题字号	nudtpaper.cls	\titleformat{\chapter}{\sanhao[1.25]...}
调整图表标题字号	nudtpaper.cls	\wuhao[1.25] → 其他字号
调整参考文献格式	main.tex	\bibliographystyle{...}
算法框跨页	main.tex	breakable 已默认开启
页眉文字	nudtpaper.cls	\sethead{...} 中的文字
公式编号格式	nudtpaper.cls	\thechapter-\arabic{equation}

十五、注意事项
1. 字体文件：使用 ttf 选项时，必须确保 fonts/ 目录包含 simsun.ttc、simhei.ttf、fangsong_GB2312.ttf、simkai.ttf，否则编译报错。
2. 编译链：首次编译或修改目录/交叉引用后，需执行 XeLaTeX → BibTeX/Biber → XeLaTeX → XeLaTeX 四次编译以正确生成目录和引用。
3. 模板文件：nudtpaper.cls 为模板核心，修改前建议备份。一般仅需修改 main.tex 和 data/ 下的内容文件。
4. 图片路径：模板已预定义 \graphicspath，支持 image/、images/、figure/、figures/ 等常见目录名，建议统一放入 image/。
5. 盲审提交：开启 anon 选项并设置 \reviewtrue，确认封面信息为空且致谢不可见后再提交。
如需进一步调整特定细节（如封面下划线间距、目录缩进、参考文献悬挂缩进量等），可对照上述参数位置进行精确修改。
