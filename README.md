# LaTeX-a-simple-tutorial-of-Win-and-Mac
这是个人使用LaTeX的一些心得体会。
## 1.基本配置(在线直接使用overleaf，这里主要讲本地文本编辑器：VSCode，主要是因为这玩意颜值高，更可以免费换皮肤，以下尽量不使用需要科学surf的地址)
### Windows (X64)
首先到https://link.zhihu.com/?target=http%3A//vscode.cdn.azure.cn/stable/78a4c91400152c0f27ba4d363eb56d2835f9903a/VSCodeUserSetup-x64-1.43.0.exe
下载VSCode，这是一个国内的镜像站点。
或者从百度网盘下载：
链接：https://pan.baidu.com/s/1E788D9EIesLRi0j-lhldfQ 
提取码：u26o 
安装，要么默认位置，要么放在自己好找的路径，把所有能勾选的都勾上，然后放在一边。、

现在下载Summtra PDF阅读器，这阅读器比VSCode自己的Tab功能多一些，而且可以秒开PDF。给出我的网盘分享链接：
链接：https://pan.baidu.com/s/1u7k3VK2pavlal6A2hzrmmQ 
提取码：2fo2 
解压即用。最好放在一个好写的路径里。

之后下载TeXLive，这里用的是TeXLive2021，注意：
##### 不要下载CTeX
##### 不要下载CTeX
##### 不要下载CTeX
CTeX会污染系统环境变量以及造成一些其他对系统有破坏性的事件。
在清华大学镜像站下载：https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/
选择TexLive2021.iso(4.1GiB)下载，下载完成后双击打开.iso文件，以管理员身份运行里面的
##### install-tl-windows.bat
。接着就会出现安装器GUI，直接点安装，这里十分建议直接装在设置好的默认位置(C盘)，也不要去省略什么包不装，避免不必要的麻烦（不会真有人C盘只有100G吧？）。
下面的安装将会把一堆包（几千个）安到电脑上，这个过程非常慢。装好之后打开cmd输入`tex -v`检验即可。

回到VSCode，使用快捷键ctrl+shift+x打开扩展功能，搜索Latex Workshop，Install，如果嫌VSCode界面没有中文不舒服可再安装一个Chinese (Simplified) Language Pack for Visual Studio Code。
现在配置设置，使用快捷键ctrl+,打开设置，搜索latex，得到一个“在settings.json中编辑”，点击后该json文件将被打开，清空后粘贴如下代码并按照注释（灰色内容）中的要求修改路径和个性化，然后ctrl+s保存（建议直接将仓库中的代码文件复制走）：
`{
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
              "-synctex=1",
              "-interaction=nonstopmode",
              "-file-line-error",
              "%DOC%"
            ]
          },
        {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
          "%DOCFILE%"
        ]
      }
    ],
  
  
    "latex-workshop.latex.recipes": [
      {
        "name": "xelatex",
        "tools": [
          "xelatex"
        ]
      },
      {
        "name": "pdflatex",
        "tools": [
          "pdflatex"
        ]
      },
      {
        "name": "xe->bib->xe->xe",
        "tools": [
          "xelatex",
          "bibtex",
          "xelatex",
          "xelatex"
        ]
      },
      {
        "name": "pdflatex -> bibtex -> pdflatex*2",
        "tools": [
          "pdflatex",
          "bibtex",
          "pdflatex",
          "pdflatex"
        ]
      }
    ],
  
    
    "latex-workshop.latex.autoBuild.run": "never", 
    "latex-workshop.synctex.afterBuild.enabled": true,
  
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.external.viewer.command": "D:/SumatraPDF/SumatraPDF.exe", //路径自选该.exe文件所在位置
  
    "latex-workshop.view.pdf.external.synctex.command": "D:/SumatraPDF/SumatraPDF.exe", //同上
    "latex-workshop.view.pdf.external.synctex.args": [
      "-forward-search",
      "%TEX%",
      "%LINE%",
      "-reuse-instance",
      "-inverse-search",
      "\"D:/Microsoft VS Code/Code.exe\" -g \"%f:%l\"", //反向搜索配置，里面改成Code.exe的位置！
      "%PDF%"
    ],
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
    "workbench.colorTheme": "Solarized Light",  //这里是我自己的皮肤设置，如果不喜欢可以之后去设置里改
    "editor.fontSize": 25, //这是我自己的字号设置，同样可以自己改设置
    "[latex]": {
      
      


      "editor.formatOnPaste": false,
      "editor.suggestSelection": "recentlyUsedByPrefix"
    },
    "editor.wordWrap": "on",
    "latex-preview.command": "xelatex",
    "editor.tabCompletion": "on",
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
    "workbench.editorAssociations": [
      {
        "viewType": "jupyter.notebook.ipynb",
        "filenamePattern": "*.ipynb"
      }
    ]
  }`
  到此为止已经完成了所有的配置，自此可以导入.tex文件或新建文件并将类型设置为latex，开始写作。
  
  
  ### MacOS (X86)
  现在再来说一说Mac上的VSCODE+TeX如何实现，这里的教程是给intel版mac使用的，我没有m1的mac所以也不知道怎么弄。
  首先随便用一个搜索引擎搜索MacTeX，下载并全部按照默认操作安装即可；
  
  接着下载VSCODE for mac，我没有找到国内镜像站，就把链接直接放上来了：
  https://cloud.189.cn/t/I7JrEram67Fj（访问码：9u5y）
  
  下载后安装，之后和windows的操作基本是一致的，安装扩展，然后粘贴如下代码：
  
  `{
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [

        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "latex-workshop.latex.autoBuild.run":"never",
    "workbench.iconTheme": "vs-seti",
    "workbench.colorTheme": "Solarized Light",
    "files.autoSave": "afterDelay",
    "editor.fontSize": 25,
    "[latex]": {
        

    
    
    

        "editor.formatOnPaste": false,
        "editor.suggestSelection": "recentlyUsedByPrefix"
    },
    "editor.wordWrap": "on",
    "latex-workshop.view.pdf.viewer": "tab",
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue"
}`
  接着打开任意的.tex文件即可command+option+B编译。
  
  
  
  
  
  
