---
title: NPM学习
date: 2017-07-02 14:02:44
tags:
---

- 查看node版本： node -v

- 更新npm版本： npm install npm -g

- 查看全局包安装文件夹地址： npm config get prefix

- 列出所有安装在当前node_modules的node包： ls node_modules

- 生成默认的package.json： npm init --yes

- 根据package.json中的版本规则更新包： npm update

- 卸载本地安装的包： npm uninstall <package>

- 卸载本地安装的包并同时更新package.json： npm uninstall <package> --save 或者 --save-dev

- 查看全局需要更新的包：npm outdated -g --depth=0

- 添加npm账户：npm adduser

- 登录npm：npm login

- 检查登录认证是否保存到本地：npm config ls

- 发布npm包：npm publish

- 更新npm包：npm version <update_type> updateype是版本号，执行之后再次执行npm publish

- 查看包的版本信息： npm view package_name

- 设置包的访问级别： npm acess

- 获取npm的所有配置：npm config list

- 设置npm的某个配置： npm config set key value

- 获取npm的某个配置：npm config get key

- 删除npm的某个配置：npm config delete key

- 编辑npm的某个配置：npm config edit