---
layout: post
title: "用 Python 实现一个 Cocos Creator 项目打包脚本"
date: 2019-04-15 10:57:59 +0800
categories: Programming
tags: python cocos-creator scripts
---

项目需求：每一次打包总是需要进行一堆繁琐易错的操作，如压缩配置表、构建发布、压缩图片，有没有办法写一个脚本自动完成这些操作？有。

## Settings

创建一个 `settings.py` 文件，给打包人员用于设置参数。

```python
# 项目路径
project_path = ""

# 项目配表路径
project_data_path = ""

# 项目配表压缩文件名
project_data_zip_name = ""

# 构建参数
build_args = {
    # 项目名
    'title':              '',
    # 构建的平台 [web-mobile、web-desktop、android、win32、ios、mac、qqplay、wechatgame、fb-instant-games]
    'platform':           '',
    # 构建目录，相对于 project_path 的路径
    'buildPath':          '',
    # 主场景的 uuid 值（参与构建的场景将使用上一次的编辑器中的构建设置）
    'startScene':         '',
    # 是否为 debug 模式
    'debug':              '',
    # web desktop 窗口宽度
    'previewWidth':       '',
    # web desktop 窗口高度
    'previewHeight':      '',
    # 是否需要加入 source map，建议开启以方便 debug，参考 http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html
    'sourceMaps':         '',
    # web mobile 平台（不含微信小游戏）下的旋转选项 [landscape、portrait、auto]
    'webOrientation':     '',
    # 是否内联所有 SpriteFrame
    'inlineSpriteFrames': '',
    # 是否合并初始场景依赖的所有 JSON
    'mergeStartScene':    '',
    # 是否将图集中的全部 SpriteFrame 合并到同一个包中
    'optimizeHotUpdate':  '',
    # 是否在 web 平台下插入 vConsole 调试插件
    'embedWebDebugger':   '',
    # 是否开启 md5 缓存
    'md5Cache':           '',
}
```

## 压缩配置表

`zipconfig.py`:

```python
import os
import re
import zipfile
from settings import project_data_path
from settings import project_data_zip_name

# 删除 meta 文件
for f in os.listdir(project_data_path):
    if re.search('.meta', f):
        os.remove(os.path.join(project_data_path, f))          

# 把所有 json 压缩为 zip 格式
outfpath = project_data_path + project_data_zip_name + '.zip'
outf = zipfile.ZipFile(outfpath, 'w', zipfile.ZIP_DEFLATED)
for f in os.listdir(project_data_path):
    if re.search('.json', f):
        fpath = os.path.join(project_data_path, f)     
        outf.write(fpath)
outf.close()
```

## 构建发布

`build.py`:

```python
# 参考 https://docs.cocos.com/creator/manual/zh/publish/publish-in-command-line.html

import os
import platform
from string import Template
from settings import build_args
from settings import project_path

creator_name = 'CocosCreator'

build_args_array = []
for k in build_args:
    build_args_array.append(k + '=' + build_args[k])

build_args_str = ';'.join(build_args_array)

command_template = Template('$creator --path $project_path --build "$build_args"')
command = command_template.substitute(creator=creator_name, project_path=project_path, build_args=build_args_str)

os.system(command)
```

注意需要把 Cocos Creator 的安装路径添加到 `PATH` 环境变量。

## 压缩 png 图片

首先需要安装 [PNGoo](https://github.com/NikkiDelRosso/PNGoo)，把 `pngquanti.exe` 的路径（`PNGoo/src/PNGoo/libs/pngquanti/`）添加到 `PATH` 环境变量。

`compress_images.py`:

```python
from settings import build_args
from settings import project_path
from string import Template
import os
import platform
import glob
import shutil

root = project_path + '/' + build_args['buildPath'] + build_args['platform'] + '/res/raw-assets/'
backup = root.replace('raw-assets', 'raw-assets-backup')

try:
    shutil.copytree(root, backup)
# Directories are the same
except shutil.Error as e:
    print('Directory not copied. Error: %s' % e)
# Any error saying that the directory doesn't exist
except OSError as e:
    print('Directory not copied. Error: %s' % e)

command_template = Template("pngquanti -force $filename")
for filename in glob.iglob(root + '/**/*.png', recursive=True):
    command = command_template.substitute(filename=filename)
    os.system(command)
    os.remove(filename)

# 压缩后的图片后缀为 `-fs8.png` 或者 `-or8.png`，需要重命名
for filename in glob.iglob(root + '/**/*-fs8.png', recursive=True):
    dst = filename.replace('-fs8.png', '.png')
    os.rename(filename, dst)
```

## Put It All Together

`main.py`:

```python
import sys

def main():
    try:
        import zipconfig
        import build
        import compress_images
        sys.exit(0)
    except Exception as e:
        print(e)
        sys.exit(1)
        
if __name__ == '__main__':
    main()
```