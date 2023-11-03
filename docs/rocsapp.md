# gros_web

## 打包安卓apk

工具: Hbuilder

1.项目打包npm run build

2.打开Hbuider，新建项目。项目类型要选择5+App,项目名称和地址自己设置。

3.创建完成后，保留upackage文件夹和manifest.json，其余替换为打包后dist文件夹内的静态资源

4.打开manifest.json按需求进行相关配置

5.发行->原生app-云打包

6.等待生成apk